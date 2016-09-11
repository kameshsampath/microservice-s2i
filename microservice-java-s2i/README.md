# Microservices Java App Builder 

This base builder image could be used to build the java based microservices using frameworks like [spring-boot](http://projects.spring.io/spring-boot/), [wildfly-swarm](http://wildfly-swarm.io/) etc.,

# Pre-Requsites

* Docker installed 
* [Source to Image tools](https://github.com/openshift/source-to-image/releases) installed

# Anatomy 
* [Dockerfile](./Dockerfile) - the base docker image which is built from [openshift/base-centos7](https://hub.docker.com/r/openshift/centos7/), this will result in a builder image called `kameshsampath/microservice-java-s2i` which will be later used to build the actual java based microservice container
* [assemble](./s2i/assemble) - the script used to assemble the application using maven
* [run](./s2i/run) - the script to run the application via docker typically the java -jar $artifactId.jar 
* [save-artifacts](./s2i/save-artifacts) - to save the artifacts for future builds
* [usage](./s2i/usage) - the help and usage script that will be fired when executing the command `s2i -h`

# Environment Variables

* __artifactId__ - The maven build `finalName` which will be used to generate the fat jar

# Usage 
Lets take an example of making the [Simple Calcuator Microservice](https://github.com/kameshsampath/microservice-demos/simple-calculator) as docker image.  To build the Docker image we need to execute the following `s2i` command 
`s2i build https://github.com/kameshsampath/microservice-demos/simple-calculator -e "artifactId=simple-calculator" kameshsampath/microservice-java-s2i msa-simplecalc-app`

The above command will pull the sources from the Git Repo https://github.com/kameshsampath/microservice-demos/simple-calculator and build the code inside the builder image __kameshsampath/microservice-java-s2i__ and produces a springboot microservice example application by name __msa-simplecalc-app__

Instead of using Git Repo, the local file system directoy of the application could also be specified, the command corresponding to local file repo looks like 

`s2i build file:///$HOME/microservices/simple-calculator -e "artifactId=simple-calculator" kameshsampath/microservice-java-s2i-candidate msa-simplecalc-app`

# LICENSE
Copyright 2016 Kamesh Sampath

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

# References
* [s2i](http://docs.projectatomic.io/registry/latest/creating_images/s2i.html)
* [spring-boot](http://projects.spring.io/spring-boot/)
* [wildfly-swarm](http://wildfly-swarm.io/)
