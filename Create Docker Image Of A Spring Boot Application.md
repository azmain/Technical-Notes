* Create a Dockerfile.txt inside the project root directory.
* Write below text inside the Dockerfile.txt
    > FROM openjdk:8 | FROM [java]:[version]

    > ADD target/spring-boot-0.0.1-SNAPSHOT.jar app.jar | ADD target/[packaged jar file name] [custom name]
    
    > ENTRYPOINT ["java", "-jar", "app.jar"] | ENTRYPOINT ["java", "-jar", "[custom name]"]
    
    > EXPOSE 8080
    
    CMD1: Pull Java Image (we need this to run java application)
    CMD2: Build the image as our custom name from our packaged jar file which is in the target folder.
    CMD3: Run the commnad "java -jar customAppName" at the entrypoint when we run a container from the image.
    CMD4: Expose the internal port 8080 to others.
    
* Docker must be installed & running on windows machine.
* Few docker commands are as belows.
    > docker images | list all images
    > docker ps | list all running containers
    > docker ps -a | list all containers
    > docker rm container_name or id | remove a container

* Package the spring boot project. It will create a jar file inside target folder.
* Go to the project root directory where we have the Dockerfile.
* Open Command Line there & run the below command.
    > docker build --tag=myapp:latest --rm=true .

    CMD1: This command will build a docker image named as myapp, tagged as latest. --rm=true removes any intermediate images.
    
* Run the docker image by executing the below command.
    > docker run -p 8888:8080 --name myapp -t myapp
    
    > docker stop myapp

    CMD1: This command run the myapp image & create a container named myapp.
    Local 8888 port will act as container 8080 port.
    CMD2: Stops the running container.
    

### Resources
1. [Docker](https://docs.docker.com/engine/reference/commandline/build/)






