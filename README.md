# MovieBookingAppBackend
configuration and installation

1.Kafka download and offset tool download
2.Extract kafka folder and place it in c drive name it kafka folder
3.Change server.properties file in kafka/config  ############################# Log Basics #############################
# A comma separated list of directories under which to store log files
log.dirs=C:/kafka/kafka-logs
make the above changes
4.Change zookeeper.properties file in kafka/config # the directory where the snapshot is stored.
dataDir=C:/kafka/zookeeper-data
make above changes
use cmd below
5.run the zookeeper:- .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
6.run the kafka server :- .\bin\windows\kafka-server-start.bat .\config\server.properties
7. to create topics go to bin/windows in cmd , type >kafka-topics.bat --create --bootstrap-server localhost:9092 --topic movieapptopic
this will create topic 
we can alsoi add partition and replication factor(broker k clone hote hai)

8.>kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic movieapptopic --from-beginning   ,
for running the consumer and read the flesfrom beginning

Note:
Zookeeper port =2181
Kafka server/broker =9092


deployment in Docker , using docker desktop 
1. create jar file by maven install or command prompt , disable test case if getting error mvn clean install -DskipTests(give finalname in pom for jar file name)
2.write DockerFile   
3.go to your project root directory , "build -t moviebookingapp:m1 ." ,"docker build -t moviebookingapp-image:m1 ." run this command to generate docker image  image name is moviebookingapp 
and m1 is tag
4.to check image by command "docker images".
5.to run application we need to create run docker container  :docker run --name moviebookingapp-container -dp 8082:8081 moviebookingapp:m1
docker me 8082 me run hoga or eclipse me 8081 me d bole toh detached mode me run hoga , p port no, 
ye command container run karega or docker image bhi .
6. how many docker container are running to check this type , "docker container ps"
7.to check logs docker  logs  moviebookingapp-container
8.to stop docker stop moviebookingapp-container
9.If you want yo start container docker start moviebookingapp-container
10 . to remove container docker rm moviebookingapp-container

11.To connect application with mongo , you can type command "docker pull mongo" or "docker pull mongo:latest"
12.to check image by command "docker images".
13 . Start mongodb container with specific name and port command "docker run -d --name mongodb-container -p 27017:27017 mongo"

NOTE: # we can use profile as well for creating to seperate application properties for
# ex: spring.profiles.active=dev for local environment
# ex: spring.profiles.active=docker for docker environment
#in docker while running we can specify command below
#docker run -d -p 8082:8081 --name moviebookingapp-container -e "SPRING_PROFILE_ACTIVE=docker" moviebookingimage

in eclipse run as configurations arguments tab add = -Dspring.profiles.active=docker
in cmd =java -jar spring-boot-docker.jar --spring.profiles.active=docker use to run profile optional I guess because its running without it as well
