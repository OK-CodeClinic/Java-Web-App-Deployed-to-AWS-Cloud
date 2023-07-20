#  JAVA WEB APP DEPLOYED TO AWS CLOUD
## DESCRIPTION: 
This project covers how i deployed on premises java web app, host it and run it on AWS cloud using the Lift and shift strategy. 


## SCENARIO:
Originally, this web app was first running on Oracle VMs. Having so many server; nginx, rabbitmq,apache-tomcat9, msql, etc is  a big issue to run on data cenetrs creating complex managements like;
- Time and resources consuming.
- Manaual process
- Difficulty to automate
- Upfront Cost
- Scaling Complexity

## OBJECTIVE:
- No upfront Cost
- Flexibile Infrastructure
- Automation (IAAC)
- Easy to set Up
- Easy to maintain
- Modernize effectiveness

## SOLUTION:
To eradicate complex management putting the objective in place, AWS cloud platform is the solution to provide the services needed.

### AWS Services Used;
- Ec2 Instance (Replace; VMs of Apache-Tomcat, RabbitMq, Memcahe, Mysql)
- Elastic Load Balancer (Replaces; Nginx Load Balancer)
- Autoscaling group (Automation for VMs scaling to ensure cost effectiveness)
- s3 (Stores app artifacts)
- Route 53 (Private DNS service)
- Others include; IAM, Amazon Certicate Manager, KeyPairs Security Groups and Target group.

### OS used;
- CentOS 9 (Instance for Mysql, Rabbitmq and Memcahe)
- Ubuntu Server 22.04LTS (Instance for Apache-Tomcat9)

## ARCHITECTURE
  ![webapparch](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/2dec57e3-5271-417e-af42-31505060ef57)

#.
## FLOW OF EXECUTION
1. 

## Author

- [Kehinde Omokungbe](https://www.github.com/OK-CodeClinic)

## Purpose
This is for leaning purpose only.


