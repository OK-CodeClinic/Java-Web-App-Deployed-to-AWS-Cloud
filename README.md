#  JAVA WEB APP DEPLOYED TO AWS CLOUD (Vprofile Web app)
## DESCRIPTION: 
Vprofile project covers how i deployed on premises java web app, host it and run it on AWS cloud using the Lift and shift strategy. 


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

 ![webapparch](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/093cb01e-c5d9-47ff-a5d8-41676349d142)

## FLOW OF EXECUTION
#### Step 1:
Login to AWS Console
#### Step 2:
Create KeyPair
#### Step 3:
Create Security groups;
- Secuiry group for Application Load Balancer
- Security Group for Apache-tomcat9
- Security Gorup for backend services (mysql, memcahe, rabbitmq). It is important to specify the following inbound rules as follows
  ![Screenshot (106)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/0ff23cc8-4d97-444c-ba10-9a23cc4a06a5)



#### Step 4: 
Launch all EC2 Instances and automate installation of servsers using the ```userdata.sh```
- CentOs for mysql, rabbitmq and memcache
- Ubuntu 22LTS for apache-tomcat9
  ![Screenshot (108)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/015015de-f044-4719-b339-04cff0a9bc3c)


#### Step 5:
SSH into all server for validation if working perfectly
- Rabbitmq working
 ![Screenshot (110)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/0186f627-00b9-4d37-9d39-46d705e95af9)

-Memcache running
 ![Screenshot (111)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/49fe91e3-b611-4101-afe0-5efb72bc4364)

- Mysql running
  ![Screenshot (112)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/c16710a2-0240-426f-b2ad-4a14714bcbe5)

- Apache-Tomcat working
  ![Screenshot (121)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/6ef81215-b933-437e-b6d3-bda88dba35f4)







#### Step 6:
In route 53
- Create a Private Hosted Zone; ```vprofile.in```
  ![Screenshot (113)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/97d2ab82-5afd-4f1c-a9d6-818cb4a8fce8)

- Create 3 simple record for all backened servers with their private IP address.
  ![Screenshot (115)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/f8037de6-2020-41d7-8dc7-38d3320880e8)


#### Step 5:
Build artifacts from source code using maven ```mavn install```
Then,this created the target/ directory where my app resides. Now, app is ready to be deployed

#### Step 6: 
Create an IAM user with s3 full access attached to it

#### Step 7:
I create an s3 bucket using the AWS-CLI
 ```aws s3 mb s3://kehinde-vprofile```

#### Step 8:
I copied built artifact from local repo to the s3 bucket created
```aws s3 cp target/vprofile-v2.war```
  ![Screenshot (120)](https://github.com/OK-CodeClinic/Java-Web-App-Deployed-to-AWS-Cloud/assets/100064229/8283b5a3-0135-4066-be6c-ad09b64714e8)


#### Step 9:
- Give IAM role access to the EC2 instance of Tomcat
- SSH into Tomcat Ec2 instance
- Download the artifact from s3 bucket ```aws cp s3 ://kehinde-vprofile/vprofile-v2.war /tmp/```
- stop tomcat9 server ```systemctl stop tomcat9```
- Remove tomcat ROOT folder ```rm -rf /var/lib/tomcat9/webapps/ROOT```
- Copy artifact to tomcat ROOT ``` cp /tmp/vprofile-v2.war /var/lib/tomcat9/webapps/ROOT.war

#### Step 10:
Create target Group for ALB
- Override the port number from 80 >> 8080, 
- Attach the tomcat EC2 instance.

#### Step 11:
Create Application Load Balancer
- Attach its security group earlier in Step 3
- attach target group created in step 10.
- Attach the Amazon certificate Manager (ACM) to the secure listenig settings.

#### Step 12:
GoDaddy
- Copy the ALb DNS url from step 11
- Create a new DNS record
- Create CNAME; using the ALB DNs url copied as the host value.

#### 
Autoscaling Group




## Author

- [Kehinde Omokungbe](https://www.github.com/OK-CodeClinic)

## Purpose
This is for leaning purpose only.


