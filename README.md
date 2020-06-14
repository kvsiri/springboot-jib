# Spring boot Jib Example

## Overview
>A sample spring boot rest service with docker packaging using [Jib](https://github.com/GoogleContainerTools/jib/)  maven plugin.

>[Project Jib](https://cloud.google.com/blog/products/gcp/introducing-jib-build-java-docker-images-better) is an open-source Java containerizer from Google that lets Java developers build containers using the Java tools they know.
>The detailed blog and instructions of using the project is described in [blog](https://medium.com/@prgnr173/containerize-your-spring-boot-app-with-jib-plugin-50127d99a22f?sk=f48f1c31816cacdcd3c47c2e1d0e9bbc).

## Run Command
* Clean compile and Build

`$ mvn clean compile jib:dockerBuild`

* Compile and push image

`$ mvn compile jib:build -Djib.to.auth.username= -Djib.to.auth.password=`

## Result
See the logs and you can find the containerizing steps and image gets pushed to the defined registry.