Regions and Availability zones map: https://aws.amazon.com/about-aws/global-infrastructure/

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

![image](https://github.com/user-attachments/assets/73e78ef8-855a-430f-8cf0-eaf4e8a278b0)

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


