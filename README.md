# gitlab

build_job:
 script: 

--- then go to build section -- pipepline - select the pipeline and run pipeline

after it is successful got to jobs and check the log output
jobs are executed by runners
and can check then stages


create stages for job execution 
the order of items define the stages of execution of the jobs order
all our config files are present under - code ---> repository


artifacts are used to transfer info [dependency/modules/files]from one job to another

gitlab runner is an application that works with gitlab cicd to run jobs in a pipeline [ for example windows runner for windows appln]
-------------

create new project
git remote set-url origin - repo url 
check by git remote -v
git branch
it will be main branch
create feature branch
then git checkout - feature branch
git add .
git status
git commit -m "myapp ag"
git push -u origin feature


you can create merge request later

first run the pipeline of the feature branch

.gitlab-ci.yml
stages:
 - build_stage
 - deploy_stage



build job:
 stage: build_stage
 image: node
 script:
   - apt update -y
   - apt install 
 artifacts:
   paths:
    - node_modules:
    - package-lock.json

#you can download the artifacts from build job - from job artifacts


deploy:
  stage : deploy_stage
  script:
   - apt update -y
   - apt install nodejs -y
   - node app.js > /dev/null 2>&1 & #to run in background

commit changes and pipeline is executed


-----------------------------
stages:
 - build_stage
 - deploy_stage

build:
  stage: build_stage
  script: 
      - docker --version
      - docker build -t pyapp .
  tags:
      - ec2
      - server

deploy:
   stage: deploy_stage
   script: 
       - docker run -d --name pythoncontainer -p 80:8080 pyapp
       - docker login -u $DOCKER_USERNAME -p $DOCKER_TOKEN
       - docker tag pyapp $DOCKER_USERNAME/pyapp
       - docker push $DOCKER_USERNAME/pyapp
   tags:
       - ec2
       - server #runner when runner is installed on ec2
-----

variables:
 Name: "CloudChamp"
 Message : "Please"


demo:
  script: 
       - echo "hey $Message subscribe to $Name"
variables are of two types

GLOBAL_VAR:
JOB_VAR:

we can also add variables under CI/CD by using any flags to protect vaiable , mask variable, expand variable reference.
for example adding docker hub username and token

----------------

keywords

stages:
artifacts:
before_script:
after_script:
------------------------

Under Operate -- we can create environment
environments allow you to track deployments of your application
NAME:
external url:
gitlab agent:
---------------

cicd you can change the timeout of 1 hour which is default
pipeline schedules -- and define cron jobs

