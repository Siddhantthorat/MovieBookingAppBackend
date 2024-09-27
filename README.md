Here's the properly formatted content for your `README.md` file, which you can upload to GitHub for the `MovieBookingAppBackend` project.

---

# MovieBookingAppBackend

## Kafka Configuration and Installation

### Steps:
1. **Download Kafka and Offset Tool:**
   - Download Kafka from [Kafka downloads](https://kafka.apache.org/downloads).
   - Download the offset tool if needed.

2. **Extract Kafka Folder:**
   - Extract the Kafka folder and place it in `C:\`. Name the folder `kafka`.

3. **Edit `server.properties`:**
   - Navigate to `kafka/config/server.properties`.
   - Update the following line for log basics:

     ```properties
     ############################# Log Basics #############################
     log.dirs=C:/kafka/kafka-logs
     ```

4. **Edit `zookeeper.properties`:**
   - Navigate to `kafka/config/zookeeper.properties`.
   - Update the following line for Zookeeper data directory:

     ```properties
     # the directory where the snapshot is stored
     dataDir=C:/kafka/zookeeper-data
     ```

5. **Start Zookeeper:**
   - Open a command prompt and run Zookeeper:

     ```bash
     .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
     ```

6. **Start Kafka Server:**
   - In another command prompt, start the Kafka server:

     ```bash
     .\bin\windows\kafka-server-start.bat .\config\server.properties
     ```

7. **Create Kafka Topic:**
   - To create a topic, navigate to the `bin/windows` directory in CMD and type:

     ```bash
     kafka-topics.bat --create --bootstrap-server localhost:9092 --topic movieapptopic
     ```

   - You can also add partitions and replication factors if needed.

8. **Run Kafka Consumer:**
   - To run the consumer and read files from the beginning, use the command:

     ```bash
     kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic movieapptopic --from-beginning
     ```

### Ports:
- **Zookeeper Port:** 2181
- **Kafka Server/Broker:** 9092

---

## Deployment in Docker (Using Docker Desktop)

### Steps:

1. **Create JAR File:**
   - Use Maven to install dependencies and generate the JAR file:

     ```bash
     mvn clean install -DskipTests
     ```

   - Ensure you provide the `finalName` in the `pom.xml` for the JAR file name.

2. **Write Dockerfile:**
   - In your project's root directory, create a `Dockerfile`.

3. **Build Docker Image:**
   - In your project root, run the following command to build the Docker image:

     ```bash
     docker build -t moviebookingapp-image:m1 .
     ```

4. **Check Docker Image:**
   - Verify that the image is created by using:

     ```bash
     docker images
     ```

5. **Run Docker Container:**
   - Run the Docker container using the command:

     ```bash
     docker run --name moviebookingapp-container -dp 8082:8081 moviebookingapp-image:m1
     ```

   - This will run the application on port `8082` in Docker and on port `8081` in Eclipse.

6. **Check Running Docker Containers:**
   - Use the following command to check running containers:

     ```bash
     docker container ps
     ```

7. **Check Docker Logs:**
   - View logs using:

     ```bash
     docker logs moviebookingapp-container
     ```

8. **Stop Docker Container:**
   - Stop the running container:

     ```bash
     docker stop moviebookingapp-container
     ```

9. **Start Docker Container:**
   - Start the container again if needed:

     ```bash
     docker start moviebookingapp-container
     ```

10. **Remove Docker Container:**
    - To remove the container, use the command:

      ```bash
      docker rm moviebookingapp-container
      ```

11. **MongoDB in Docker:**
    - Pull the MongoDB image:

      ```bash
      docker pull mongo
      ```

    - Verify the MongoDB image:

      ```bash
      docker images
      ```

12. **Run MongoDB Container:**
    - Start the MongoDB container with a specific name and port:

      ```bash
      docker run -d --name mongodb-container -p 27017:27017 mongo
      ```

---

## Using Profiles in Docker

- You can use different profiles for creating separate application properties, e.g.:
  - For local environment:

    ```properties
    spring.profiles.active=dev
    ```

  - For Docker environment:

    ```properties
    spring.profiles.active=docker
    ```

- To specify the active profile while running in Docker, use the following command:

  ```bash
  docker run -d -p 8082:8081 --name moviebookingapp-container -e "SPRING_PROFILE_ACTIVE=docker" moviebookingapp-image
  ```

- In Eclipse, go to **Run Configurations → Arguments Tab** and add:

  ```bash
  -Dspring.profiles.active=docker
  ```

- In CMD, you can run the JAR with the profile:

  ```bash
  java -jar spring-boot-docker.jar --spring.profiles.active=docker
  ```

  This step is optional as it might run without specifying the profile as well.

---

This `README.md` can now be uploaded to GitHub for documentation.

--- 

Let me know if you need any further formatting adjustments!
