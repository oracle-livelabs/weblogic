# Clone the PetClinic Repository

## Introduction

This lab will step through cloning and preparing the Spring Framework 5.3.x Pet Clinic example that is available [here](https://github.com/spring-petclinic/spring-framework-petclinic/tree/5.3.x) from the Spring Team, a PetClinic version with a Spring Framework 5.3.x configuration and with a 3-layer architecture (i.e. presentation --> service --> repository).

Estimated Lab Time: ***5 minutes***

### About Spring Framework 5.3.x Pet Clinic Sample

The Spring Pet Clinic sample application is a classic example of a web application that demonstrates the capabilities of the Spring Framework. It is designed to showcase the use of Spring's core features, including dependency injection, aspect-oriented programming, and data access. The application is structured in a way that separates concerns into different layers, making it easy to understand and maintain.

The Pet Clinic application allows users to manage a pet clinic, including features such as:

* Viewing a list of pets
* Adding new pets
* Updating pet information
* Deleting pets
* Managing pet owners
* Simulating an error to catch and handle exceptions

The application is built using the Spring Framework, which provides a robust and flexible foundation for building Java applications. It also uses various Spring projects, such as Spring MVC for web development and Spring Data for data access.

### Objectives

*In this lab, you will:*

* Clone the Spring Framework 5.3.x Pet Clinic sample application
* Resolve any dependencies

### Prerequisites

*This lab assumes you have:*

* [`git`](https://help.github.com/articles/set-up-git) command line tool installed.

## Task 1: Clone the Pet Clinic repo from its original source

1. Clone the **`spring-framework-petclinic`** repo:

    ```shell
    <copy>
    git clone -b 5.3.x --single-branch https://github.com/spring-petclinic/spring-framework-petclinic.git
    </copy>
    ```

1. Change to the **`spring-framework-petclinic`** directory:

    ```shell
    <copy>
    cd spring-framework-petclinic
    </copy>
    ```

![Git Clone](images/git-clone.gif " ")

## Task 2: Resolve Maven dependencies

As a best practice, Maven dependencies must be resolved and downloaded to your local cache, prior to using of tools like OpenRewrite. If needed, run `mvn dependency:resolve` for missing dependencies.

1. Run the following command to resolve and download the dependencies from Maven Central:

    ```shell
    <copy>
    mvn dependency:resolve
    </copy>
    ```

1. If you see any errors, check your internet connection and/or VPN, and try again.

![Resolve Maven Dependencies](images/mvn-resolve.gif " ")


## Learn More

* [Spring Framework 5.3.x PetClinic github repository](https://github.com/spring-petclinic/spring-framework-petclinic/tree/5.3.x)
* [Maven's `dependency:resolve`](https://maven.apache.org/plugins/maven-dependency-plugin/resolve-mojo.html)

## Acknowledgements

* **Author** - Adao Oliveira Junior, Solutions Architect, Oracle ECNJ Architects
* **Contributors** - Adao Oliveira Junior, ECNJ Architects
* **Last Updated By/Date** - Adao Oliveira Junior, April 2025
