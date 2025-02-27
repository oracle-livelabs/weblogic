# Install and configure the operator

## Introduction

An operator is an application-specific controller that extends Kubernetes to create, configure, and manage instances of complex applications. The Oracle WebLogic Server Kubernetes Operator (the "operator") simplifies the management and operation of WebLogic domains and deployments.

This lab walks you through the steps to prepare OCI Cloud shell (client) environment and install WebLogic Kubernetes Operator.

Estimated Lab Time: 15 minutes

## **STEP 1**: Clone the operator repository to a Cloud Shell instance

1. First, clone the operator git repository to OCI Cloud Shell.
    ```bash
    <copy>git clone --branch v4.2.15 https://github.com/oracle/weblogic-kubernetes-operator.git</copy>
    ```
    You should have output similar to the following:

    ```bash
    $ git clone --branch v4.2.15 https://github.com/oracle/weblogic-kubernetes-operator.git
    Cloning into 'weblogic-kubernetes-operator'...
    remote: Enumerating objects: 1572146, done.
    remote: Counting objects: 100% (2423/2423), done.
    remote: Compressing objects: 100% (495/495), done.
    remote: Total 1572146 (delta 1307), reused 2234 (delta 1159), pack-reused 1569723 (from 4)
    Receiving objects: 100% (1572146/1572146), 1.01 GiB | 46.34 MiB/s, done.
    Resolving deltas: 100% (800284/800284), done.
    Note: switching to '78ba3c86b964fa9ce753c85731f54e94e3b2be20'.

    You are in 'detached HEAD' state. You can look around, make experimental
    changes and commit them, and you can discard any commits you make in this
    state without impacting any branches by switching back to a branch.

    If you want to create a new branch to retain commits you create, you may
    do so (now or later) by using -c with the switch command. Example:

    git switch -c <new-branch-name>

    Or undo this operation with:

    git switch -

    Turn off this advice by setting config variable advice.detachedHead to false
    ```


## **STEP 2**: Prepare the Kubernetes environment
Kubernetes distinguishes between the concept of a user account and a service account for a number of reasons. The main reason is that user accounts are for humans while service accounts are for processes, which run in pods. The operator also requires service accounts.  If a service account is not specified, it defaults to `default` (for example, the namespace's default service account). If you want to use a different service account, then you must create the operator's namespace and the service account before installing the operator Helm chart.

1. Create the operator's namespace in advance:
    ```bash
    <copy>kubectl create namespace sample-weblogic-operator-ns</copy>
    ```

2. Create a service account for the operator in the operator’s namespace.
    ```bash
    <copy>kubectl create serviceaccount -n sample-weblogic-operator-ns sample-weblogic-operator-sa</copy>
    ```

3. Finally, add the weblogic-operator repository to Helm.
    ```bash
    <copy>helm repo add weblogic-operator https://oracle.github.io/weblogic-kubernetes-operator/charts --force-update</copy>
    ```

## **STEP 3**: Install the operator using Helm

1. Before you execute the operator helm install, make sure that you are in the operator's local Git repository folder.
    ```bash
    <copy>cd ~/weblogic-kubernetes-operator/</copy>
    ```

2. Use the `helm install` command to install the operator Helm chart. As part of this, you must specify a "release" name for their operator.

    You can override the default configuration values in the operator Helm chart by doing one of the following:

    - Creating a [custom YAML](https://raw.githubusercontent.com/oracle/weblogic-kubernetes-operator/master/kubernetes/charts/weblogic-operator/values.yaml) file containing the values to be overridden, and specifying the `--value` option on the Helm command line.
    - Overriding individual values directly on the Helm command line, using the `--set` option.

    Using the last option, simply define overriding values using the `--set` option.

    Note the values:
    - The name of the Helm release.
    - The relative path to the Helm chart.
    - **namespace**: The namespace where the operator is to be deployed.
    - **serviceAccount**: The service account required to run the operator.

    > Earlier versions of the operator's Helm chart only supported selecting namespaces that the operator would manage using a list. Now, namespaces may be chosen using a list, label selector, or regular expression.


3. Execute the following `helm install`:
    ````bash
    <copy>helm install sample-weblogic-operator weblogic-operator/weblogic-operator \
    --namespace sample-weblogic-operator-ns \
    --set serviceAccount=sample-weblogic-operator-sa \
    --wait</copy>
    ````
    
    The output will be similar to the following:
    ```bash
    NAME: sample-weblogic-operator
    LAST DEPLOYED: Thu Feb 27 06:20:25 2025
    NAMESPACE: sample-weblogic-operator-ns
    STATUS: deployed
    REVISION: 1
    TEST SUITE: None
    ```
   
4. Check the operator pod:
    ```bash
    <copy>kubectl get po -n sample-weblogic-operator-ns</copy>
    ```
    The output will be similar to the following:
    ```bash
    NAME                                         READY   STATUS    RESTARTS   AGE
    weblogic-operator-7cd4cc88bf-2f74n           1/1     Running   0          2m19s
    weblogic-operator-webhook-857cbdf974-nqnkk   1/1     Running   0          2m19s 
    ```

    > Make sure to wait until the pod is in **Running** state.

5. Check the operator Helm chart:
    ```bash
    <copy>helm list -n sample-weblogic-operator-ns</copy>
    ```
    The output will be similar to the following:
    ```bash
    NAME                            NAMESPACE                       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
    sample-weblogic-operator        sample-weblogic-operator-ns     1               2025-02-27 06:20:25.451624895 +0000 UTC        weblogic-operator-4.2.15    4.2.15 
    ```

    The WebLogic Server Kubernetes Operator has been installed. You may now **proceed to the next lab**.

## Acknowledgements
* **Author** -  Ankit Pandey
* **Contributors** - Sid Joshi, Maciej Gruszka 
* **Last Updated By/Date** - Ankit Pandey, March 2025
