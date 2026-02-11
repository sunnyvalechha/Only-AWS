Regions and Availability zones map: https://aws.amazon.com/about-aws/global-infrastructure/

# Cloud Watch

* Comprehensive Monitoring: CloudWatch allows you to monitor various AWS resources such as EC2 instances, RDS databases, Lambda functions, and more. You get a unified view of your entire AWS infrastructure.

* Real-Time Metrics: It provides real-time monitoring of metrics, allowing you to respond quickly to any issues or anomalies that might arise.

* Automated Actions: With CloudWatch Alarms, you can set up automated actions like triggering an Auto Scaling group to scale in or out based on certain conditions.

* Log Insights: CloudWatch Insights lets you analyze and search log data from various AWS services, making it easier to troubleshoot problems and identify trends.

* Dashboards and Visualization: Create custom dashboards to visualize your application and infrastructure metrics in one place, making it easier to understand the overall health of your system.



# Cloud Trail

# Cloud cost optimization

* Cloud cost optimization is the process of strategically managing and reducing cloud computing expenses while maintaining or improving performance and functionality. It involves analyzing cloud resource usage, identifying inefficiencies, and implementing strategies to minimize waste and maximize the value derived from cloud investments.

* Write a Lambda function in Python using boto3 module and this function will talk to the Aws API's.
* We have to write the function for a individual resource like EBS volume this function will also delete the stale resources.
* Trigger this lambda function with the help of cloudwatch.
* In Lambda function default execution time is 3 seconds we can increase as per the requirement. Aws will charge us for this execution time.
=========================================
# IAM 

Identitiy and Access management, It is a Global service consist Users, Groups, Roles, Policies

* Users and Groups are assigned json documents called Policies.

* These policies defines the permission of the users.

* In AWS we apply the least privilege principal don't give more permission than a user needs.

**IAM Password policies**

* Strong Password = Higher security for the account.
* In AWS you can set a password policy.
* Set a minimum password length
* Require specific character types:
    - Include upper case letters
    - Lower case letters
    - Numbers
    - Non-alphanumeric characters

* Allow all IAM users to change their own passwords

* Must change the password between 60 days

* Prevent password re-use

* Protect account with MFA
    - Password you know + security device you own.
 
**IAM Security Tools**

* IAM credentials report (account-level)
    - A report that list's all your account's users and the status of their various credentials.
 
Iam section > Under Access reports > Credential report

* IAM access advisor (user-level)
    - Access advisor shows the service permission granted to a user and when those were last access.

Iam section > Inside specific user > Access Report

# EC2

**EC2 user data** 

* It is possible to bootstrap our instance using an EC2 user data script.
* Bootstrap - launching an commands when an machine starts
* The script will only run once when the machine first starts.
* Ec2-user-data is used to automate boot tasks such as:
    - Installing Updates
    - Installing Software
    - Downloading common files from the internet

* Ec2 User data runs with root privilege so we must use sudo when using any command.

**EC2 Instance Types**:

![image](https://github.com/user-attachments/assets/7e8e751b-b109-41a0-a649-655ee3bbb4f2)

7 Different type of Ec2 Instances, each Instance type have different families.

1. General Purpose
2. Compute Optimize
3. Memory Optimize
4. Accelerated Computing
5. Storage Optimize
6. Instance Features
7. Measuring Instance Performance

AWS follows Instance naming convetion:

m5.2xLarge

* M - Instance class
* 5 - generation (Aws improves over time, after sometime it will be 6)
* 2xLarge - Size within the Instance class (micro, small, large, 2x Large) More size means more memory, CPU on the instance

- General purpose: Great for diversity of workloads like webservers or code repositories. Balance between compute, memory and Networking. T - Series
  
- Compute Optimize: Great for compute intesive tasks that require high performance processors: C - Series
      * Batch processing workloads.
      * Media Transcoding
      * High Performance web servers
      * High Performance computing
      * Scientific Modeling and machine learning
      * Dedicated gaming servers

- Memory Optimize - Fast performance for workloads that process large data sets in memory (RAM) R - Series
      *   High Performance relational / Non relational database
      *   Distributed web scale cache stores
      *   In-memory database optimize for BI (business Intelligence)
      *   Applications performing real time processing of big unstructured data.

- Storage Optimize Instances - Great for storage Intensive tasks that require high, sequential read and write access to large data sets on local storage. I, D, H - Series
      * High frequency online transaction processing (OLTP) systems.
      * Relational and NoSQL Databases
      * Cache for In-memory Databases (Redis)
      * Data warehouse applications
      * Distributed File System

  **Ec2 Instance Purchasing Options**

* On demand Instance - Short workloads, predictible pricing, pay by seconds

* Reserved Instance have terms of (1 year and 3 years)
    - used for long duration workloads like database used for years.
    - Convertible Reserve Instance - longs workloads with flexible instances.

* Savings Plan - (1 year and 3 years) plans with the commitment to an amount of usage and long workloads.

* Spot Instances - Short Workloads, Cheap, Can loose Instance (less reliable)

* Dedicated Hosts - book an entire physical server, control Instance placement.

* Dedicated Instances - no other customer will share your hardware

* Capacity Reservation - reserve capacity in a specific AZ for any duration.

**Spot Instances**

* Get on 90% discount in compared with On demand.

Spot Request:

1. Define how many Instances we want.
2. Maximu price
3. Launch specification
4. AMI
5. Request valid from and till when.
6. Request type:

There are two types of request:

* One time request for spot Instances - As soon as the requst is full filled the instance launched the spot request will go away.
* Persistent request - If the Instance get interupt the request will again initiated automatically and fullfil, If the Instance are not in use we have to terminate the instance because it will not done automatic and delete the spot request first then delete instance else it will again some instance as per the request.

**Spot Fleet**

* Set of Spot Instance + On-demand Instances
* The spot fleet will try to meet the target capacity with price constraints.

![image](https://github.com/user-attachments/assets/f070064a-3c93-46a3-85be-efd862bb4d67)


**Placement Groups**

* Control over the EC2 instance placement strategy
* When creating a placement group we have to define a strategy

1. Cluster - Cluster Instances into a low-latency group in a single AZ
2. Spread - Spread instances into a underlying hardware (max 7 instances per group per AZ)
3. Partition - Spread instances accross many different partitions which rely on different set of racks with an AZ. Can scales 100's of Ec2 instances. (Use case Hadoop)



Cluster

![image](https://github.com/user-attachments/assets/0352778c-b821-49fb-b3f1-b223a70786d0)


Spread

![image](https://github.com/user-attachments/assets/faee179d-ec2c-434d-8fcf-62e725d8d190)


Partition

![image](https://github.com/user-attachments/assets/b0d350d5-2534-4dce-ba99-2bbbff67f42e)


ENI - Elastic Network Interface

A virtual Network Card like **eth0** is the default we are adding **eth1**

We can create a ENI and attach to EC2 instances on the fly. 

It will bound to a specific AZ


**EC2 Hibernate**

When we stop the instance it will shut down the OS completely and then start if we start again it will take more time. This is not for empty instance. Imagine one heavy script is running in User data along with the web application.

In Hibernate the instance will not stop or restarted it will just frozen so the boot will be much faster. Under the hood the RAM state is written in a file in the root EBS volume. Just instance RAM size should be less than 150 GB

Use Cases:

* Long running processes.
* Store the RAM state
* Service that take time to start again.

![image](https://github.com/user-attachments/assets/652774fe-712e-4eb0-b28f-5599c81279b2)

Practical:

At the time when launching the Instance select the option Hibernate, check uptime of the instance when launched, Stop & Start the Instance again then check uptime it will be more min not less because if the instance had fully stopped so uptime will be 0

![image](https://github.com/user-attachments/assets/1b25df3d-d710-4b8d-8312-ff313e2333fd)


**How to copy Instance and its data from one AZ to another ?**

* EBS Volume Snapshot - Important !
      - EBS Volumes > Actions > Create Snapshot
      - Snapshot > Actions > Copy Snapshot (this can copy in same region or in another region)
      - Snapshots > Recycle bin > Retention policy (called as Accidental deletion protect)
      - Select resource type (EBS Snapshot)> retention 1 day > Create # So if snapshot is delete we can recover again

  ![image](https://github.com/user-attachments/assets/c0c79f89-c05f-4b1c-b090-12b8f53ebe77)


* Create AMI from an running Instance.
      - Instance > Actions (Image & Templates) > Create Image
      - AMI > Launch Instance from AMI

**EBS Multi Attach**

* Attach the same ec2 instance with multiple ec2 instances.
* Each instance have full read write access to the EBS volume.
* Attach upto 16 instance at a time.
* Must use a file-system that cluster aware (not ext3,4 xfs)

**EBS Encryption** 

*  When we create a encrypted EBS volume all data transfer inside the volume already encrypted. AMI and snapshot also encrypted.
*  Encryption and decryption are handled by AWS
*  EBS encryption leverage keys from KMS (AES 256)

Note: A volume created without encryption so if we make snapshot of this EBS volume this also uncrypted.

How to fix ?

Go to Snapshot > Copy snapshot > Select encryption > Create

Once this is created, Create volume from Snapshot

![image](https://github.com/user-attachments/assets/f2ddbf7b-82e5-411e-9cd2-4e840f72ade3)

**EC2 Instance Store**

These are more high performance from EBS volume then use EC2 instance store.

Features:

* Better I/O performance
* EC2 Instance store lose their storage if they're stopped.
* Good for Cache and Temporary content.

**AWS Load Balancers**

In AWS there are 3 types of Load Balancers:
1. Application LB
2. Network LB
3. Gateway LB
4. Classic LB (old generation)

What is Load Balancer?
- Suppose, I have a application it could be any shopping website or a online game and it is hosted on ec2 server, on its initial phase the application was not much popular so the traffic coming to the ec2 is manageble but gradually people found it intresting or theere might a sale going on the huge traffic comes to the server and 1 server is not able to handle the traffic.
- Eventually users might face the slowness and downtime while accessing the app.
- So deploy the application in 3 different vm's and in front of these 3 instances you will place a load balancer.
- We have route the traffic instead to the instances to the Load balancer. Now, the Load balancer will manage the request and traffic comming to the instances.
- A basic Load balancer will distribute the traffic in a round robin manner, let's say there are 100 request coming and 3 instances are deployed so each instance will get 33 requests.
- A load balancer can distribute traffic in a ration based like 50 request sends on 1 instance rest 2 instances get 25-25. This also can be done with other LB's.
- Doing this we made this application an **Highly available** (HA) application.

There are lots of Load balancers are present in the market, few are listed below:
1. Nginx
2. F5
3. Envoy
4. Traefik
5. Ambassador

First, understand how data packets flows within 7 layers of OSI model?

* Osi model is a journey of a data, how we request for some information on the internet and the information we receive back in fraction of seconds is gone through this journey.

1. Application layer          - layer7
2. Presentation layer         - layer6
3. Session layer              - layer5
4. Data-segmentation layer    - layer4  # transport layer
5. Network layer              - layer3
6. Data link layer            - layer2
7. Physical layer             - layer1

* If we want to perform traffic load balancing on layer 7, then choose the Application Load Balancer (Application layer)
* If we want to perform traffic load balancing on layer 4, then choose the Network Load Balancer (Network Layer).


# RDS

1. Overview of RDS
2. Databases on EC2 instances
3. Migrating traditional DB from EC2 to RDS
4. HA - Multi AZ architecture
5. RDS - Automatic backups, snapshot & restore
6. RDS - read replicas
7. RDS - data security

* Database on EC2 vs Database on RDS we place webserver & application on 1 ec2 and database on another db


<img width="1894" height="738" alt="image" src="https://github.com/user-attachments/assets/26ea3188-1fbb-4e49-87f5-d9dc875f59a6" />


**Relational Databases** - A managed service from AWS. AWS provide many features along with database.

* Automated provisioning, OS Patching.
* Continues backups and restore to specific timestamp **(Point in Time Restore)**
* Monitoring Dashboards
* Read replicas for Improved Read performance.
* Multi AZ setup for Disaster Recovery (DR)
* Scaling Capabilities (Vertical & Horizontal)

**Read replicas for read scalability**

* Read replicas helps us to scale our reads on database.
* Suppose 1 application is read and write to the database and 1 database is not enough because there are too many read / write.
* So we can increase 15 Read replicas, within AZ, Cross AZ or cross region.
* Read replicas are in sync with main RDS database engine.

**Use Case:**

![image](https://github.com/user-attachments/assets/b3f4cbb4-f416-49d5-984b-8212d9ed47cb)

**RDS - Mutli AZ Disaster Recovery**

* 1 Application which is continuesly read & write to the Main databases.
* SYNC replication.
* 1 DNS name is assigned to the RDS Instance (Standby) for automatic failover condition.
* If there is failure of main RDS Database it will automatic make the Standy Database to main Database with the help of DNS.
* No intervention is required.

![image](https://github.com/user-attachments/assets/f4ff38ee-77ec-4512-96bb-5834a8db8582)


**RDS - From Single AZ to multi AZ**

* Zero downtime operation ( no need to stop the AZ )
* Just click on 'modify' the database and enable multi AZ

Under the hood what happened, when we do this ?

* A snapshot will taken of your main database.
* Snapshot db will restore to new Standby database.
* Once the DB is restore, Syncronization have estabilished. Now we are in multi AZ setup

![image](https://github.com/user-attachments/assets/ee8cf487-40de-4c8d-9a24-be92a35443e2)


Important: Once the RDS is created connect with "SQL Electron". Provide Endpoint, DB and Password to the SQL Electron and connect.


![image](https://github.com/user-attachments/assets/3fccb3ad-893c-4386-ae6b-6ffe781c90a8)


Point in Time Recovery - Restore last backup or any specific custom time backup.

* Go to RDS > Automated Backups > Replicated > Restore to point in time > Choose restore time (custom / latest) 

![image](https://github.com/user-attachments/assets/541b3305-f0dd-4202-9863-7b7d06dfbbec)


# S3

- Simple Storage Service

* Create Bucket
* Upload any object in the bucket        (We can't access the object with public URL / Object URL)
* Go to bucket permissions               [Block public access (bucket settings)]
* Edit and Untick all blocks             (Still not accessible)
* Bucket Policy > Edit > Copy Bucket ARN > Policy Generator
   - Type of policy - S3 bucket policy
   - Effect - Allow
   - Principal - *
   - Actions - GetObject
   - ARN - arn:aws:s3:::sunnydevopsbucket/*    # paste arn along /*
   - Add statement / Generate policy
   - Copy policy | paste in the bucket policy | Save changes

* The object is now accessible

* 7 Storage Classes:

1. Standard - General Purpose
2. Standard - Infrequent Access
3. One Zone - Infrequent Access
4. Glacier Instant Retrieval
5. Glacier Flexible Retrieval
6. Glacier Deep Archive
7. Intelligent Tiering

* S3 Durability and Availability

- Durability - 99.99999999999% (11 times 9) of object accross multiple Az's.
- Same durability for all storage classes.

- Availability - Measure how ready a service is. It depends on storage class.
- Example: S3 standard has 99.99% of availability = not available 53 minutes in a year.
- 


# S3 Static website hosting

 - S3 can also host static websites and have them accessible on the internet.
 - It will work only if the bucket policy allows public access else it will throw "403 Forbidden error"

* Under Bucket > Properties tab
* At the end "Static website hosting"
* Enable
* Upload index.html file in bucket
* Open with Bucket website endpoint under Static website hosting - http://sunnydevopsbucket.s3-website.ap-south-1.amazonaws.com

# S3 Versioning

* Bucket Permissions > Bucket Versioning
* Enable Versioning
* Make some changes in 'index.html' and re-upload file.
* In Bucket you'll see toggle of 'show versions' enable it and see the old and new version.
* New uploads have the "Version ID", "Null" means older version
* Validate the content with the 'Static website hosting' URL
* Rollback - delete the version having "Version ID", again validate.
* Delete marker on objects - Disable toggle of show versions and delete any object
* After deleting, enable the toggle and you'll see the deleted version.
* Restore the deleted version - delete the "delete marker" version.

# S3 Replication

* CRR - Cross region replication, 2 regions are different
* SRR - Same region replication, 2 regions are the same.

- Versioning must enabled in source and destination buckets.
- Must have proper IAM permissions to S3 buckets.

* Create 2 buckets in different regions
* Source bucket > management > replication rules
* rule scope - apply to all objects
* Choose bucket in same account
* Create new IAM role
* Save
* Upload object in source bucket it will replicate in destination bucket

 # AWS Config

 AWS Config provides a detailed view of the configuration of AWS resources in your AWS account. It deals with compliance it make sure that the Aws account and resources alligns with the rules and regulations of the organization.

 Example:
 * EC2 instance should have monitoring enabled.
 * S3 buckets have Lifecycle policy enabled and block the public access.

But there must be thousand of buckets and EC2 instances how to check if it's according to compliance or not.

# AWS Secret Management

We can secure our environment by three ways:-

1. Systems Manager - Parameter Store
2. Secrets manager
3. Hashicorp vault

* Systems manager: Information which is not sensitve can be stored.
* Secret manager: Information which is highly sensitive can stored either secret manager or vault. This feature can rotate certificates and passwords once in a 90 or 120 days we set.
* We can integrate the combination both system manager and secret manager to use our sensitive and non-sensitive data due to the cost also because Aws will charge to make you data safe.

# 3 tier architecture

* 3 tier is where frontend + backend + database is required.
* 2 tier is where only frontend and backend is required no database.





  

