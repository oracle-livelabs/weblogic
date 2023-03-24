# Migrating the Application Database

## Introduction

We will walk you through the steps to migrate the on-premises application database to the database provisioned on OCI using DataPump.

Estimated Completion Time: 10 minutes.

### About Product/Technology

- DataPump is a tool that is part of the Oracle database set of utilities.
- DataPump export function creates a DDL + data dump of the user schema.
- DataPump import function imports the data into the database.

In this workshop we will be using wrapper scripts to export, move the data to the destination and import to complete a full migration.

### Objectives

- Get shell access to the on-premises database.
- Use a DataPump script to export the database schema to migrate.
- Edit the DataPump import script with the information collected in the database provisioning tutorial.
- Run a DataPump import script to migrate the database schema to OCI.

### Prerequisites

- To have provisioned the on-premises demo environment that includes the source database to migrate.
- To have provisioned the target database on OCI.
- To have gathered information about the passthrough-server to the database, and the database node IP and domain name which is part of the connection string.

## Task 1: Get a Shell Inside the On-Premises Database Instance

### If you used the Docker environment:

1. You should already be inside the database container from the SSH key creation step. If not, use:

      ```
      <copy>
      docker exec -it weblogic-to-oci-oracledb-1 /bin/bash
      </copy>
      ```

2. Get into the `/datapump` folder:

      ```
      <copy>
      cd ~/datapump
      </copy>
      ```


### If you used the workshop image:

1. You should already be logged into the instance and switched to the `oracle` user. If not use:

      ```bash
      <copy>
      ssh opc@<public-ip>
      </copy>
      ```

      ```bash
      <copy>
      sudo su - oracle
      </copy>
      ```

2. Get into the `/datapump` folder:

      ```
      <copy>
      cd ~/datapump
      </copy>
      ```

      The script itself is commented to explain what it does.

      It sets up the directory to backup to, and uses DataPump `expdp` export command to dump the `RIDERS` schema, which is the schema the application depends on.

      The `datapump_export.sh</code>` script appears as follows.

      ```bash
      EXPORT_DB_DIRNAME=export

      # all other variables are from the local environment

      # clear the folder and recreate
      rm -rf ~/datapump/export && mkdir -p ~/datapump/export

      # drop directory if it exists
      echo "DROP DIRECTORY ${EXPORT_DB_DIRNAME};" | sqlplus system/${DB_PWD}@${DB_HOST}:${DB_PORT}/${DB_PDB}.${DB_DOMAIN}

      # create a directory object in the DB for export with DataPump, pointing to the folder created above
      echo "CREATE DIRECTORY ${EXPORT_DB_DIRNAME} AS '/home/oracle/datapump/export/';" | sqlplus system/${DB_PWD}@${DB_HOST}:${DB_PORT}/${DB_PDB}.${DB_DOMAIN}

      # export the schema 'RIDERS' with DataPump, which is our user schema with the Tour de France Riders data
      expdp system/${DB_PWD}@${DB_HOST}:${DB_PORT}/${DB_PDB}.${DB_DOMAIN} schemas=RIDERS DIRECTORY=${EXPORT_DB_DIRNAME}
      ```

## Task 2: Export the Source Database

1. Run the `datapump_export.sh` script:

      ```
      <copy>
      ./datapump_export.sh
      </copy>
      ```

      The output will look like:

    ![script output](./images/migrate-db-1.png " ")


## Task 3: Install the OCI CLI on the Source Database

This will be needed to get the wallet from the ATP database and put the database dump file into object storage from the source database.

> **Note:** You could also do without the CLI by getting the wallet through the console and uploading the dump file through the console. This requires more manual steps.

1. Install the OCI CLI on the source database:

    ```bash
    <copy>
    bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
    </copy>
    ```

    At first try, you may be prompted to upgrade Python: hit *`Y`*, 

    then run the command again
    
    Hit **enter** to use the defaults for all options.

2. Restart your shell:
    ```
    <copy>
    exec -l $SHELL
    </copy>
    ```

3. Configure UTF8

    you will need to set LOCALE to UTF8 using
    
    ```bash
    <copy>
    export LC_ALL=en_US.utf8 
    export LANG=en_US.utf8
    </copy>
    ```
    

4. Configure the CLI

    ```bash
    <copy>
    oci setup config
    </copy>
    ```

    Enter the following information:
    
    1. Location of the configuration: press **Enter**.
    2. `user_ocid`: enter your user OCID.
        1. In the Oracle Cloud Console, click your **User** icon (top right corner), then click your user name.
            !["user"](images/setup-tf-user.png " ")

       2. Copy the OCID of your user.
            !["user ocid"](images/setup-tf-user-ocid.png " ")

    3. `tenancy_ocid`: enter your tenancy OCID.
        1. In the Oracle Cloud Console, **click** your **User** icon (top right corner), then **Tenancy**.
            !["tenancy"](images/setup-tf-tenancy.png " ")

        2. **Copy** the OCID of the tenancy.
            !["tenancy ocid"](images/setup-tf-tenancy-ocid.png " ")

    4. `region`: enter your region from the list provided.
    5. Generate a RSA key pair: press **Enter** for Yes (default).
    6. Directory for keys: press **Enter** for the default.
    7. Name for the key: press **Enter** for the default.
    8. Passphrase: press **Enter** for no passphrase.

    You should see an output like:

    ```bash
    Private key written to: /home/oracle/.oci/oci_api_key.pem
    Fingerprint: 21:d4:f1:a0:55:a5:c2:ce:e2:...
    Config written to /home/oracle/.oci/config
    ```

4. Upload the public key to your OCI account.

    In order to use the CLI, you need to upload the public key generated to your user account.

    Get the key content with:

    ```
    <copy>
    cat /home/oracle/.oci/oci_api_key_public.pem
    </copy>
    ```

5. Copy the full printed output to clipboard.

6. In the Oracle Cloud Console:

    - Under **User -> User Settings**.
    - Click **API Keys**.
    - Click **Add Public Key**.
    - Click **Paste Public Key**.
    - Paste the key copied above.
    - Click **Add**.

    You can verify that the Fingerprint generated matches the fingerprint output of the config.

7. Test your CLI:

    ```
    <copy>
    oci os ns get
    </copy>
    ```

    This command should output the namespace of your tenancy (usually the name of the tenancy)

    ```
    {
        "data": "your-tenancy-namespace"
    }
    ```

    It may take a few dozen seconds for the API key to be validated, so if at first you see an Unauthorized answer, try again in a minute.

    Note the name of the **namespace** that will be needed later.

## Task 4: Create an Object Storage Bucket

1. Go to **Core Infrastructure** then select **Object Storage**.

    ![object storage menu](./images/migrate-db-oss-1.png " ")

2. Make sure you are in the compartment where you deployed the resources.

3. Click **Create Bucket**.

4. Give the bucket the name **atp-upload**.

5. Click **Create Bucket**.

## Task 5: Edit the `datapump_import_atp.sh` Script


First, we'll need to edit the `datapump_import_atp.sh` script to target the OCI database found in the datapump folder.

1. Open the script in an editor. We'll use the popular `nano` editor:

      ```
      <copy>
      nano datapump_import_atp.sh
      </copy>
      ```

    You'll need to input the following variables (see instruction below to find the data):
    ```
    BASTION_IP=<IP of the Bastion Instance or Public IP of the Admin server, from WLS Admin URL>

    TARGET_DB_NAME=wlsatpdb
    TARGET_DB_OCID=<OCID of the ATP database>
    TARGET_DB_HOST=<Private Endpoint IP>

    BUCKET=atp-upload
    REGION=us-ashburn-1
    NAMESPACE=<Tenancy namespace>

    OCI_USER=<full username, usually email, sometimes prefixed with IDCS service name>
    OCI_TOKEN='<auth token>'

    TARGET_DB_PORT=1522
    TARGET_DB_USER=admin
    TARGET_DB_PWD=<YOUR DB ADMIN PASSWORD>
    ```

2. Enter the `BASTION_IP`.

     The `BASTION_IP` is the **public IP** through which to reach the database subnet (the Bastion Instance Public IP you provisioned in a private subnet). Either are found in the **Output** of the WebLogic deployment stack.

3. Go to **Oracle Database -> Autonomous Transaction Processing**.

4. Make sure you are in the right compartment and **click** the database you provisioned earlier to get to the details.

5. **Enter** the name of the Autonomous Database as the `TARGET_DB_NAME` in the script, making sure it is in *lowercase*. If you followed the naming conventions in this workshop, it should be `wlsatpdb`.

6. **Copy** the **OCID**, and enter it as the `TARGET_DB_OCID` in the script.

7. **Copy** the **Private Endpoint IP address** and enter as the `TARGET_DB_HOST` in the script.

    ![private endpoint](./images/db-info.png " ")

8. **Enter** the name of the Object Storage bucket created earlier as `BUCKET` (`atp-upload`).

9. **Enter** the name of your region as `REGION` (for example `us-ashburn-1`).

10. **Enter** the name of your namespace as `NAMESPACE`. This was output when you tested the OCI CLI.

11. Go to **User -> Settings** and copy your *full username* (it usually consists of your email, sometimes prefixed with the ID service if your login is through Single Sign On). Enter it as the `OCI_USER` variable.

12. In **User -> Settings** click **Auth Tokens**.

    ![auth token](./images/auth-token.png " ")

13. Click **Generate Token**.

14. Give it a name.

15. Click **Generate Token**.

16. Copy the output of the token to the variable `OCI_TOKEN`.

    *Make sure to use single quotes to delimitate the OCI_TOKEN as it may contain characters that would cause script errors.*

17. Enter your DB SYS password for `TARGET_DB_PWD`.

18. scroll down to *`SSL_SERVER_DN_MATCH=yes`* and switch to *`SSL_SERVER_DN_MATCH=no`*.

18. Save the file (with `CTRL+x` then `y`).

## Task 6: Import the Data into the Target Database

1. Run the `datapump_import_atp.sh` script you edited at the previous step:

      ```bash
      <copy>
      ./datapump_import_atp.sh
      </copy>
      ```

2. You will be prompted to continue connection. Type `yes` to proceed.

The import script runs in 8 phases:

- It copies the dump file over to Object Storage.
- It downloads the wallet for the ATP database locally, and unzips it.
- It creates a SSH tunnel to access the ATP database locally.
- It sets up the `sqlnet.ora` file to point to the wallet.
- It adds the hostname of the ATP database into the `/etc/hosts` file to point to `localhost` so that connection attempts go through the tunnel we created.
- It runs the `impdp` import command once.
You may notice this 1st try imports the schema but fails at importing the data, because the user `RIDERS` does not have a quota on the local `USERS` tablespace.
- The script edits the `RIDERS` user tablespace quota.
- It re-runs the `impdb` command that now succeeds at importing the data, but will show an error related to the user `RIDERS` already existing. This is normal.

The database is now migrated to OCI, but we also need to set up the wallet on the WLS servers.

If the tunnel closing step reports failure, it is safe to ignore.

## Task 7: Download the Wallet on Each WebLogic Server

There are 2 ways to download the wallet on to the target WebLogic servers:

We have downloaded the wallet locally already to migrate the database, and we can simply secure-copy that wallet to each server with `scp`. This is what we will do.

1. Gather the IP adresses of the WebLogic server:

    Go to **Core Infrastructure -> Compute -> Instances**.

    View the list of WebLogic servers and gather the IP addresses.

2. Run the following command, to copy the wallet on each server.

    Set the variables:
    ```bash
    <copy>
    export TARGET_WLS_SERVER=<Private IP of a WLS server>
    </copy>
    ```
    ```bash
    <copy>
    export BASTION_IP=<Public IP of the Bastion Instance>
    </copy>
    ```

    Then:

    ```bash
    <copy>
    scp -o ProxyCommand="ssh opc@${BASTION_IP} -W %h:%p" wallet.zip opc@${TARGET_WLS_SERVER}:~/
    </copy>
    ```
    ```bash
    <copy>
    ssh -o ProxyCommand="ssh opc@${BASTION_IP} -W %h:%p" opc@${TARGET_WLS_SERVER} "sudo chown oracle:oracle wallet.zip"
    </copy>
    ```
    ```bash
    <copy>
    ssh -o ProxyCommand="ssh opc@${BASTION_IP} -W %h:%p" opc@${TARGET_WLS_SERVER} "sudo unzip wallet.zip -d /u01/data/domains/nonjrf_domain/config/atp/"

    </copy>
    ```

    Make sure to specify the proper domain name (here `nonjrf_domain`).


3. Repeat for each WLS target server.

> **Note:** the destination path is important as this path is cloned when scaling WLS servers, insuring the wallet is also deployed on any new server instance.


   An alternative method (for info only, no need to apply these commands):

   There is also a helper script on each WebLogic server node to download the wallet.

   For this script to work, you will need to add an extra policy on the **dynamic group** created by the WLS on OCI stack.

   The policy is called `<PREFIX>-wlsc-principal-group`, which you can find under **Identity -> Dynamic Groups**. The Policy to edit will be on the *root* of the tenancy, so you need to be an administrator to edit it. It is called `<PREFIX>-service-policy`. It should contain an extra policy rule as follow:

   ```
   Allow dynamic-group nonjrf-wlsc-principal-group to use autonomous-transaction-processing-database-family in compartment id <your compartment>
   ```
   If you choose this method, you would use the following variables:

   ```bash
   <copy>
   export TARGET_WLS_SERVER=<Public IP>
   export ATP_OCID=<OCID of the ATP database>
   export WALLET_PASSWORD=<password of your choice>
   </copy>
   ```

    Then run the command:

    ```bash
    <copy>
    ssh opc@${TARGET_WLS_SERVER} "sudo su -c \"/opt/scripts/utils/download_atp_wallet.sh ${ATP_OCID} ${WALLET_PASSWORD} /u01/data/domains/nonjrf_domain/config/atp\"" - oracle
    </copy>
    ```

    Make sure to specify the proper domain name in the path (here `nonjrf_domain`).

## Acknowledgements

 - **Author** - Emmanuel Leroy, May 2020
 - **Last Updated By/Date** - Emmanuel Leroy, August 2020
