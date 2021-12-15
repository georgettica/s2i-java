OpenShift S2I Builder for Java Docker images
====

[![Build Status](https://travis-ci.org/luiscoms/s2i-java.svg?branch=master)](https://travis-ci.org/luiscoms/s2i-java)

Supported tags and respective `Dockerfile` links
---------

- [`1.8-all`, `latest` (*Dockerfile*)](http://github.com/luiscoms/s2i-java/blob/master/1.8-all/Dockerfile)
- [`1.8-gradle` (*Dockerfile*)](http://github.com/luiscoms/s2i-java/blob/master/1.8-gradle/Dockerfile)
- [`1.8-maven` (*Dockerfile*)](http://github.com/luiscoms/s2i-java/blob/master/1.8-maven/Dockerfile)


This repository contains the source for building various versions of
the Java application as a reproducible Docker image using
[source-to-image](https://github.com/openshift/source-to-image).
Users can choose between RHEL and CentOS based builder images.
The resulting image can be run using [Docker](http://docker.io).

For more information about using these images with OpenShift, please see the
official [OpenShift Documentation](https://docs.openshift.org/latest/using_images/s2i_images/python.html).

For a very similar S2I Java builder with some more options and flexibility, consider [fabric8io-images/s2i](https://github.com/fabric8io-images/s2i), AKA [fabric8/s2i-java on Docker Hub](https://hub.docker.com/r/fabric8/s2i-java/).
It [also supports Java 11, in addition to Gradle, Maven and Java 8 as per this blog post](http://blog2.vorburger.ch/2018/11/s2i-with-java-11-gradle-builds-for.html).


Versions
--------
Java versions currently provided are:
* JDK-1.8 + Gradle 2
* JDK-1.8 + Maven 3
* JDK-1.8 + Gradle 2 + Maven 3

CentOS versions currently supported are:
* CentOS7


Installation
------------

To build a Java image, choose either the Maven or Gradle with:

*  **Gradle image**

    This image is also available on DockerHub. To download it run:

    ```
    $ docker pull luiscoms/s2i-java:1.8-gradle
    ```

    To build a Java image with Gradle from scratch run:

    ```
    $ git clone https://github.com/luiscoms/s2i-java.git
    $ cd s2i-java
    $ make build VERSION=1.8-gradle
    ```

*  **Maven image**

    To build a Java image with Maven, you need to run the build on a properly.

    ```
    $ git clone https://github.com/luiscoms/s2i-java.git
    $ cd s2i-java
    $ make build VERSION=1.8-maven
    ```

    This image is also available on DockerHub. To download it run:

    ```
    $ docker pull luiscoms/s2i-java:1.8-maven
    ```


*  **Gradle + Maven image**

    To build a Java image with Gradle and Maven, you need to run the build on a properly.

    ```
    $ git clone https://github.com/luiscoms/s2i-java.git
    $ cd s2i-java
    $ make build VERSION=1.8-all
    ```

    This image is also available on DockerHub. To download it run:

    ```
    $ docker pull luiscoms/s2i-java:1.8-all
    ```

Or

    ```
    $ docker pull luiscoms/s2i-java
    ```

**Notice: By omitting the `VERSION` parameter, the build/test action will be performed on all provided versions of Java.**


Usage
-----

For information about usage of Dockerfile for Java 1.8 with Gradle,
see [usage documentation](1.8-gradle/README.md).

For information about usage of Dockerfile for Java 1.8 with Maven,
see [usage documentation](1.8-maven/README.md).

For information about usage of Dockerfile for Java 1.8 with Gradle and Maven,
see [usage documentation](1.8-all/README.md).

Test
----

This repository also provides a [S2I](https://github.com/openshift/source-to-image) test framework,
which launches tests to check functionality of a simple Java application built on top of the s2i-java image.

Users can choose between testing a Java test application with Gradle or Maven.

*  **Gradle image**

    ```
    $ cd s2i-java
    $ make test VERSION=1.8-gradle
    ```

*  **Maven image**

    ```
    $ cd s2i-java
    $ make test VERSION=1.8-maven
    ```

*  **Gradle + Maven image**

    ```
    $ cd s2i-all
    $ make test VERSION=1.8-all
    ```


Repository organization
------------------------
* **`<jdkVersion-(gradle|maven|all)>`**

    Dockerfile and scripts to build container images from.

* **`hack/`**

    Folder containing scripts which are responsible for build and test actions performed by the `Makefile`.
