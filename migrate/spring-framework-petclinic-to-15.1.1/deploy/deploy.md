# Build and Deploy the Application

## Introduction

On this lab, you will build and deploy the migrated Spring Framework Pet Clinic (Now on Spring Framework 6.2.x) application to WebLogic Server 15.1.1.

Estimated Workshop Time: ***5 minutes***

### Objectives

*In this lab, you will:*

* Build the migrated Spring Framework Pet Clinic sample application
* Deploy to WebLogic Server 15.1.1
* Test the application

### Prerequisites

*This lab assumes you have:*

* Basic knowledge of Java and Maven
* You have Maven 3.6.x or higher, Java 21 or higher installed
* You have a terminal (local or OCI Cloud Shell) with access to the internet
* You have a ***WebLogic 15.1.1 domain running*** to test the migrated application

## Task 1: Build the Application

Run the following command to build the application:

```shell
<copy>
mvn clean package -DskipTests
</copy>
```

> ***NOTE*** </br>
> The `mvn clean package` command will build the application and create a WAR file in the `target` directory. The WAR file will be named `petclinic.war`.
> </br></br>
> The `-DskipTests` option is used to skip the tests during the build process. This use lab does not cover the migration of the tests.

![Package the application](images/mvn-package.svg " ")

## Task 2: Deploy the Application

There are several ways to deploy the application to WebLogic Server 15.1.1, like using the [WebLogic Deployment Tool](https://oracle.github.io/weblogic-deploy-tooling/), [WebLogic Remote Console](https://oracle.github.io/weblogic-remote-console/) and WLST (WebLogic Scripting Tool). In this lab, we will use the WebLogic Remote Console to deploy the application.

### Download the WebLogic Remote Console if you do not have yet

1. Go to [github.com/oracle/weblogic-remote-console/releases](https://github.com/oracle/weblogic-remote-console/releases)

1. Download the latest release of the WebLogic Remote Console. The file will be named `WebLogic-Remote-Console-<version>-<platform>.<dmg|zip>`. Select the correct file for your platform (Windows, arm64-Mac, x86-Mac, Linux).

1. Install the WebLogic Remote Console.

### Open the WebLogic Remote Console and configure the connection to your WebLogic Server

> ***NOTE*** </br>
> This step is just to configure the connection to your WebLogic Server. If you already have the connection configured, you can skip this step.

1. Open the WebLogic Remote Console.
1. Click on the `providers` icon to add a new connection.

### Deploy the application

1. Click on the `Edit Tree` tab.
1. Click on the `Deployments` folder, and then to the `App Deployments`.
1. Click on the `⨁ New` icon to add a new application deployment.
1. Add a name for the application on the `Name*`. For this lab, we will use `petclinic`.
1. Select a target for the application on the `Targets*`. For this lab, we will use `AdminServer`.
1. On the `Source*` section, click on the `Chose file` button and select the `petclinic.war` file from the `target` directory of the `spring-framework-petclinic` application.
1. Select `Start Application` on the `On Deployment` section.
1. Click on the `⨁ Create` button.
1. Click on the `Shopping Cart` icon and then `Commit Changes` to commit the changes.

At this point, the application should be deployed and started on WebLogic Server 15.1.1.

![Deploy the application using WebLogic Remote Console](images/deploy-with-wrc.gif " ")

## Task 3: Test the Application

1. Open a web browser and go to the following URL: `https://<your-weblogic-server-host-and-port>/petclinic/`

> ***NOTE*** </br>
> The host and port will depend on your WebLogic Server configuration. You may have a loadbalancer or a reverse proxy in front of your WebLogic Server if deployed on Kubernetes or in a Cloud Provider.

![Running the Migrated Pet Clinic on a local WebLogic](images/petclinic-weblogic.gif " ")

## Learn More

* [How to install Maven](https://maven.apache.org/install.html)
* [How to install Java 21](https://www.oracle.com/java/technologies/downloads/#java21)
* [WebLogic Remote Console](https://oracle.github.io/weblogic-remote-console/)
* [WebLogic Deployment Tool](https://oracle.github.io/weblogic-deploy-tooling/)
* [Deploy WebLogic in a Kubernetes Cluster](https://docs.oracle.com/en/solutions/deploy-wls-on-oke/index.html#GUID-79EC097D-DC13-4B92-92A7-CB09D594EF78)
* [WebLogic on Oracle Cloud Infrastructure](https://docs.oracle.com/en/cloud/paas/weblogic-cloud/user/oracle-weblogic-server-oracle-cloud-infrastructure.html)
* [Running WebLogic on the Azure Kubernetes Service](https://learn.microsoft.com/en-us/azure/virtual-machines/workloads/oracle/weblogic-aks)

## Acknowledgements

* **Author** - Adao Oliveira Junior, Solutions Architect, Oracle ECNJ Architects
* **Contributors** - Adao Oliveira Junior, ECNJ Architects
* **Last Updated By/Date** - Adao Oliveira Junior, April 2025
