# Migrate the application database

## Introduction

We will walk you through the steps to migrate the on-premises application database to the database provisioned on Oracle Cloud Infrastructure (OCI) using DataPump.

Estimated Completion Time: 10 minutes.

### About Product/Technology

- DataPump is a tool that is part of the Oracle database set of utilities.
- DataPump export function creates a DDL and data dump of the user schema.
- DataPump import function imports the data into the database.

We will be using wrapper scripts to export, move the data to the destination, and import to complete a full migration.

### Objectives

- Get shell access to the on-premises database.
- Use a DataPump script to export the database schema to migrate.
- Edit the DataPump import script with the information collected during the database provisioning stage.
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

    Then:

    ```bash
    <copy>
    sudo su - oracle
    <copy>
    ```

2. Get into the `/datapump` folder:

    ```
    <copy>
    cd ~/datapump
    </copy>
    ```

    The script itself is commented to explain what it does.

    It sets up the directory to backup to, and uses DataPump `expdp` export command to dump the `RIDERS` schema, which is the schema the application depends on.

    The `datapump_export.sh` script appears as follows.

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

Run the `datapump_export.sh` script:

```
<copy>
./datapump_export.sh
</copy>
```

The output will look like:

![script output](./images/migrate-db-1.png " ")

## Task 3: Edit the `datapump_import.sh` script

Once the schema and data are exported, we'll import it into the OCI DBaaS database.

First, we'll need to edit the `datapump_import.sh` script to target the OCI database found in the datapump folder.

1. Open the script in an editor. We'll use the popular `nano` editor:

    ```
    <copy>
    nano datapump_import.sh
    </copy>
    ```

2. Enter the `BASTION_IP`.

   The `BASTION_IP` is the **public IP** of the Bastion Instance.
   
    Find it in **Resource Manager** under **Stack**, **stack details** then select the job and look at **Outputs**.

    ![bastion IP](./images/migrate-db-2.png " ")

3. Enter the `TARGET_DB_HOST` **private IP address**.

   This IP address was gathered from the Database System details, under the following settings: **Database System**, **details**, followed by **Nodes**.

   ![database host IP](./images/provision-db-26-nodeip.png " ")

4. Enter the `TARGET_DB_DOMAIN` name from the database connection string.

   If you followed the default naming conventions, it should be `nonjrfdbsubnet.nonjrfvcn.oraclevcn.com`.

   ![database domain](./images/provision-db-27-connection2.png " ")

5. Enter your DB SYS password for `TARGET_DB_PWD`.

## Task 4: Import the Data into the Target Database

1. Run the `datapump_import.sh` script you edited at the previous step:

    ```bash
    <copy>
    ./datapump_import.sh
    </copy>
    ```

2. You will be prompted to continue connection twice. Type `yes` each time to proceed.

   The import script runs in 4 phases:

    - It copies the files over to the OCI database node.

    - It runs the `impdp` import command once.

      You may notice this first try imports the schema but fails at importing the data, because the user `RIDERS` does not have a quota on the local `USERS` tablespace.

    - The script edits the `RIDERS` user tablespace quota.

    - And re-runs the `impdb` command that now succeeds at importing the data, but will show an error related to the user `RIDERS` already existing. This is normal.

The database is now migrated to OCI.

## Acknowledgements

 - **Author** - Emmanuel Leroy, May 2020
 - **Last Updated By/Date** - Emmanuel Leroy, March 2023
