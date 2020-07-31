# bacit-payara
A directory structure for a simple j2ee project which can be deployed to the Payara server (former Glassfish). Directory structure is made based on maven archetype. 
(
    $ mvn archetype:generate -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-j2ee-simple -DarchetypeVersion=1.4
)



Build with the container 
(
    $ docker run --rm --name java_maven2_build -it -v "$PWD":/usr/src/app  -v "$HOME"/.m2:/root/.m2 janisdocker/javabuilder clean install
)
janisdocker/javabuilder is based on openjdk:8-jdk-alpine and MAVEN_VERSION=3.3.9


Run the application:
(
    $ docker run -p 8080:8080 -p 4848:4848 -v <RELEVANT_DIRECTORY_ON_A_LOCAL_MOUNT>:/opt/payara/deployments payara/server-full
)

To run pure html code from index.js use:
(
    $ docker run -p 8080:8080 -p 4848:4848 -v $PWD/servlets/servlet/target:/opt/payara/deployments payara/server-full
)

To check if it is up and running use:
    http://localhost:8080/servlet-0.0.1/
To check the admin interface use:
    http://localhost:4848

payara/server-full image is based on azul/zulu-openjdk:8u222 
(
    see https://github.com/payara/docker-payaraserver-full/blob/master/Dockerfile and  https://www.azul.com/products/zulu-enterprise/supported-platforms/
)
