<details>
<summary>Project1:  Use Docker for local development</summary>

### Technologies used:
- Docker
- Node.js
- MongoDB
- MongoExpress

Project Description:

- Create Dockerfile for Nodejs application and build Docker image
- Run Nodejs application in Docker container and connect to MongoDB database container locally.
- AlsorunMongoExpress container as a Ul of the MongoDB database.

### With Docker

#### To start the application

Step 1: Create docker network
```shell
docker network create mongo-network
```
Step 2: start mongodb
```shell
docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo
```
Step 3: start mongo-express
```shell
docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express
```
_NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_

Step 4: open mongo-express from browser

    http://localhost:8081

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express

Step 6: Start your nodejs application locally - go to `app` directory of project

    cd app
    npm install 
    node server.js

Step 7: Access you nodejs application UI from browser

    http://localhost:3000

</details>

<details>
<summary>Project2: Docker Compose - Run multiple Docker containers</summary>

Technologies used:
- Docker
- MongoDB
- MongoExpress

Project Description:
- Write Docker Compose file to run MongoDB and MongoExpress containers

### With Docker Compose
#### To start the application

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up

_You can access the mongo-express under localhost:8080 from your browser_

Step 2: in mongo-express UI - create a new database "user-account"

Step 3: in mongo-express UI - create a new collection "users" in the database "user-account"

Step 4: start node server

    cd app
    npm install
    node server.js

Step 5: access the nodejs application from browser

    http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:1.0 .       

The dot "." at the end of the command denotes location of the Dockerfile.
</details>

<details>
<summary>Project3: Dockerize Nodejs application and push to private Docker registry</summary>

Technologies used:
- Docker
- Nodejs
- Amazon ECR

Project Requirements:
- Write Dockerfile to build a Docker image for a Nodejs application
- Create private Docker registry on AWS (Amazon ECR)
- Push Docker image to this private repository

Step 1: create a repository in AWS ECR.

Step 2: follow the push steps from AWS ECR:

Login:

    aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <account>.dkr.ecr.us-east-1.amazonaws.com

Build:

    docker build -t devops-module7-projects .

Tag:

    docker tag devops-module7-projects:latest <account>.dkr.ecr.us-east-1.amazonaws.com/devops-module7-projects:latest

Push:

    docker push <account>.dkr.ecr.us-east-1.amazonaws.com/devops-module7-projects:latest

</details>
