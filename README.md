# bacit-payara
A directory structure for a simple j2ee project which can be deployed to the Payara server (former Glassfish). Directory structure is made based on maven archetype. 

    $ mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-j2ee-simple -DarchetypeVersion=1.4




Build with the container 

    $ docker run --rm --name java_maven2_build -it -v "$PWD":/usr/src/app  -v "$HOME"/.m2:/root/.m2 janisdocker/javabuilder clean install

janisdocker/javabuilder is based on openjdk:8-jdk-alpine and MAVEN_VERSION=3.3.9


Run the application:

    $ docker run -p 8080:8080 -p 4848:4848 -v <RELEVANT_DIRECTORY_ON_A_LOCAL_MOUNT>:/opt/payara/deployments payara/server-full


To run pure html code from index.js use:

    $ docker run -p 8080:8080 -p 4848:4848 -v $PWD/servlets/servlet/target:/opt/payara/deployments payara/server-full


To check if it is up and running use:
    http://localhost:8080/servlet-0.0.1/
To check the admin interface use:
    http://localhost:4848

payara/server-full image is based on azul/zulu-openjdk:8u222 
(see https://github.com/payara/docker-payaraserver-full/blob/master/Dockerfile and  https://www.azul.com/products/zulu-enterprise/supported-platforms/)

2020-07-31: Build the application (locally on a macbookpro; requires maven and java installed):

    $ mvh clean install

For example, with a local installation of maven

    $ mvn --version
    Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
    Maven home: /usr/local/apache-maven-3.6.3
    Java version: 13.0.2, vendor: Oracle Corporation, runtime: $HOME/openjdk/jdk-13.0.2.jdk/Contents/Home
    Default locale: nb_GB, platform encoding: UTF-8
    OS name: "mac os x", version: "10.14.4", arch: "x86_64", family: "mac"

    $ java -version
    openjdk version "13.0.2" 2020-01-14
    OpenJDK Runtime Environment (build 13.0.2+8)
    OpenJDK 64-Bit Server VM (build 13.0.2+8, mixed mode, sharing)
