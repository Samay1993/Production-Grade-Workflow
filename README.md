# Production Grade Workflow using Dockerfile, Dockerfile.dev, docker-compose.yml and Nginx server later deploying the app on AWS Elastic Beanstalk using Travis-CI and serve it to the end user(s).

## This is a simple web app bootstrapped with **[Create React App](https://github.com/facebook/create-react-app/ "Visit Facebook Open Source Git Repo")**.

This is a demo app built with an intention to successfully deploy a react.js app on **AWS BEANSTALK** and can be served to end user. 
>Note: You can also deploy this app on your local server by just using *Dockerfile* present in the root directory of this project, it will get deployed on **NGINX server**

**Some pre-requisites to start with this projects:**
1. Docker and docker-compose should be installed on your local machine.
2. Basic knowledge of GitHub.
3. Basic knowledge of Travis-CI
4. Basic knowledge of AWS and it's services will be plus.

>If you are new to Docker find out how docker works [here](https://github.com/Samay1993/Production-Grade-Workflow/blob/master/DockerIntro.md/ "Open DockerIntro.md").<br>

## Production flows implemented:
* Development Flow and running the application on development server.
* Running Unit Test Suite.
* Creating a Production ready build and deploying it to Nginx Server which further serves the application to end user.

## Files which I have created to make this project Production Ready are below:
* Dockerfile.dev
* Dockerfile
* docker-compose.yml

## Docker Features Implemented:
* Multi-Container
* Port-Mapping
* Volume-Mapping 

## Purpose of each file is described below:
| Command | Description |
| --- | --- |
**Dockerfile.dev** | It's sole purpose is to run the project in Development environment by creating a Development Server and Unit Tests can also be run using this.
**docker-compose.yml** | This is just an extenstion for Dockerfile.dev, allowing us to run the containers without using long command in terminal as explained below, such as for volume mapping flow.
**Dockerfile** | This will create a production ready build and push it to Nginx container for Deployment purpose.
<br>

## Using Dockerfile.dev to run the project in Development Environment:

| Command | Description |
| --- | --- |
docker build -t image-name -f Dockerfile.dev . | *This will create an image for the whole project and tagging it with a name.*
docker run -p host_port:3000 image-name | *This will start the Development Environment server and you can access the project on [localhost:3000](http://localhost:3000 "Visit localhost:3000 Development Server") (**If you have mapped it to port 3000 on host machine**).*
docker run image-name npm run test | *This will start Unit Tests in the project by overriding the primary command of the container to npm run test.*
docker run -v /home/node/app/node_modules -v $(pwd):/home/node/app -p 3000:3000 container-id | This will start running docker container with volume mapping of host system directory with container's file system, this enable the changes to be reflected on browser without rebuilding the docker file.
<br>

## Using docker-compose.yml to run the project in Development Environment:
| Command | Description |
| --- | --- |
docker-compose up | *This will start building the project using the provided configuration and start Development server and start running the test suite too.*

### **Note: Volume Mapping is also implemented in *docker-compose.yml*.**
**Make a small change to your src/App.js file in the greeting text and see the changes getting reflected on your browser realtime without you having to rebuild the image that's the power of volume mapping.**
<br>


## Using Dockerfile to start project in Deployment server:
| Command | Description |
| --- | --- |
docker build -t image-name . | *This will create a production optimized build ready to be served and tagging it with a name.*
docker run -p host_port:80 image-name | *This will start the container with Nginx server and map it to the specified host port and can be viewed on [localhost:8080](http://localhost:8080 "Visit localhost:8080 Nginx Deployment Server") (**If you have mapped it to port 8080 on host machine**). *
<br>


### **Note: Nginx default port is 80.**

## Deployment of AWS using Travis-CI

Once you are satisfied with the way your application work on your deployment server(NGINX) you can go ahead and configure your AWS and Travis CI to automate the build deployment as soon as you push your changes to the *master branch* of the project.
>Steps to configure AWS and Travis-CI to automate the build generation can be found [here](https://github.com/Samay1993/Production-Grade-Workflow/blob/master/AWS_Config.md/ "Open AWS_Cofig.md").

