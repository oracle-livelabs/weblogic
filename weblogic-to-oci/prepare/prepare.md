# Prepare the OCI Account

## Introduction

We will prepare the OCI environment to provision WebLogic Server for Oracle Cloud Infrastructure from the marketplace.

Estimated Completion Time: 5 minutes.

### Objectives

- Create a Vault.
- Create a Key.
- Create a Secret to hold the WebLogic Admin password.
- Copy the Secret OCID to use during the provisioning stage.

### Prerequisites

- an OCI account with a compartment created.

## Task 1: Create a Vault

1. Go to **Security -> Vault**.

   ![vault menu](./images/prereq-vault1.png " ")

2. Make sure you are in the compartment where you want to deploy WebLogic.

3. Click **Create Vault**.

   ![create vault](./images/prereq-vault2.png " ")

4. Name the vault `WebLogic Vault` or a name of your choosing. Make sure the `private` option is **not checked** and click **Create Vault**.

   ![create](./images/prereq-vault3.png " ")

## Task 2: Create a Key in the Vault

1. Once the vault is provisioned, select the vault.

   ![select vault](./images/prereq-vault4.png " ")

2. Click **Create Key**.

   ![create key](./images/prereq-key1.png " ")

3. Name the key `WebLogicKey` or a name of your choosing and click **Create Key**.

   ![settings for key](./images/prereq-key2.png " ")

## Task 3: Create a Secret for the WebLogic Admin Password

1. Once the key is provisioned, click **Secrets** then **Create Secret**.

   ![create secret](./images/prereq-secret1.png " ")

3. Name the **Secret** as `WebLogicAdminPassword`, select the `WebLogicKey` created at the previous step as the **Encryption Key**, keep the default `plaintext` option and type `welcome1` or any WebLogic compliant password (at least 8 chars and 1 uppercase or number) in the **Secret Content** text field, and click **Create Secret**.

  ![create secret](./images/prereq-secret3.png " ")

## Task 4: Check Policies Needed to Deploy and Create Dynamic Group if needed.

If you don't have the following policy for your group and you are not an admin in your tenancy:

```
<copy>
Allow group MyGroup to manage dynamic-groups in tenancy
Allow group MyGroup to manage policies in tenancy
</copy>
```

You will need to create a Dynamic Group and associated Policies:

1. From the navigation menu, select Identity & Security. Under the Identity group, click Compartments.

2. Copy the OCID for the compartment that you plan to use for the Oracle WebLogic Server compute instances.
   
   If you use another compartment just for network resources, copy also the OCID of the network compartment.

3. Click Dynamic Groups.

4. Click Create Dynamic Group.

5. Enter a Name and Description. In the policies below we assume the name is *MyInstancesPrincipalGroup*

6. For Rule 1, create a rule that includes all instances in the selected compartment in this group.

   ```
   <copy>
   ALL {instance.compartment.id = 'WLS_Compartment_OCID'}
   </copy>
   ```

   Provide the OCID for the compartment you copied previously.

7. Click Create Dynamic Group.

8. Create the policy for the dynamic group

   ```
   <copy>
   Allow dynamic-group MyInstancesPrincipalGroup to manage all-resources in compartment MyCompartment
   Allow service oke to read app-catalog-listing in compartment MyCompartment
   Allow dynamic-group MyInstancesPrincipalGroup to read secret-bundles in compartment VaultCompartment where target.secret.id = '<OCID for OCIR token secret>'
   Allow dynamic-group MyInstancesPrincipalGroup to inspect subnets in NetworkCompartment
   Allow dynamic-group MyInstancesPrincipalGroup to use dynamic-groups in MyCompartment
   </copy>
   ```

9. To use the OS Management Service, you can add the following policies as well:

   ```
   <copy>
   Allow dynamic-group MyInstancesPrincipalGroup to use osms-managed-instances in compartment MyCompartment
   Allow dynamic-group MyInstancesPrincipalGroup to read instance-family in compartment MyCompartment
   </copy>
   ```

## Acknowledgements

 - **Author** - Emmanuel Leroy, May 2020
 - **Last Updated By/Date** - Emmanuel Leroy, March 2023
