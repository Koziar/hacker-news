# Hand-in of the assignment
This is a hand-in document of the [02-Setup of CD chain with MVP](https://github.com/datsoftlyngby/soft2017fall-lsd-teaching-material/blob/master/assignments/02-Setup%20of%20CD%20chain%20with%20MVP.ipynb) assignment
for the [Development of Large Systems](https://github.com/datsoftlyngby/soft2017fall-lsd-teaching-material) course.

# Link
[http://fe-hacker-news.s3-website-eu-west-1.amazonaws.com/](http://fe-hacker-news.s3-website-eu-west-1.amazonaws.com/)

# Content
In order to achieve continuous delivery we as a group decided to use two different technologies. We are using Travis CI and Jenkins. The reason being to gain experience with both technologies as well as functional reasons. 

Our project is split up into two different services, the back-end project and the front-end project. The reason being so that we achieve low coupling between the projects and the development of both being completely separate, as should be. The back-end project is using Jenkins for CD and is releasing to Digital Ocean. Meanwhile the front-end is using Travis CI and is releasing to a AWS.

Jenkins is an automation server that helps you do many different automated tasks. It is highly configurable. Although Jenkins being highly configurable that, is the exact reason for which we chose to use Travis CI. Travis CI is a Continuous Integration service which solely focuses on the process of Continuous Integration. Which is exactly what was necessary for our task. But both tools are able to achieve the same goal. So for the sake of experimentation and experience we decided to use both.

Both tools are used in a similar manner, the tools are hooked up to Github which we are using for code versioning. When a change is made in the respective master project the tools run and build the newly updated project version. Once the build is done and successful it will be deployed to its respective cloud storage. 

## Jenkins setup and config
Unfortunately we were unable to automate the deployment using Jenkins due to some unexpected errors which led us to run out of time. The Project is manually deployed for now but should be fully automated very shortly. In order to run our server there are two simple commands to run. 

```
mvn compile
mvn exec:java -Dexec.mainClass="api.Main"
```
## Travis setup and config
Travis CI is rather simple to use. All you have to do is create a config file in the project which will run in Travis and tell Github that it will be using Travis on that certain project. Here is an image of our config file which is written in a .yml file named .travis.yml. This file is located in the root of our front-end project.

![alt text](https://github.com/HackerNews-lsd2017/hacker-news/blob/master/screenshots/Screen%20Shot%202017-09-19%20at%2022.10.44.png)

Within this file we are telling Travis what commands to run in the Travis Environment in order to get the project up and running. We then specify where Travis will deploy the project. This is specified after “deploy:”. Here we give Travis information about the AWS S3 bucket in which it will deploy the project. The variables such as $AWS_BUCKET is taken from the github repository in which we specify what variables are in the config file and Travis then replaces with the variables.

![alt text](https://github.com/HackerNews-lsd2017/hacker-news/blob/master/screenshots/Screen%20Shot%202017-09-19%20at%2022.23.28.png)

This is an image of setting up Travis within our GitHub project. We have only set it so that fe-hacker-news will be using Travis.

![alt text](https://github.com/HackerNews-lsd2017/hacker-news/blob/master/screenshots/Screen%20Shot%202017-09-19%20at%2022.33.16.png)

Here we can see the conditions selected in order for running the project in Travis. The third section is where we set the variables which are used in the Travis config file.