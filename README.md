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

* IAM access advisor (user-level)
    - Access advisor shows the service permission granted to a user and when those were last access.
