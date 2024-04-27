Login to AWS account search for VPC and click on "create VPC"
Go for " VPC and more " for better and easy config of network components
Select a project name 
Keep the CIDR range as same 
keep the availability zones as 2 for better traffic management
Keep the public and private subnet as 2 
Nat Gateaway as 1 per AZ
Keep endpoint as NONE 
Click on Create VPC
VPC gets created successfully 
Create Auto Scaling group by going to EC2 instance and scroll down
Auto Scaling group cannot be created directly so you need to first create Launch Templete 
Click on Create launch temeplete and provide necessary details
In network setting part in launch tempelete click on create security group and provide details
## it is always recommended to open the port in which your app is running instead of opening all the ports 
For this project first open ssh port from anywhere second add another rule and open port which is required for eg- port 8000 using custome TCP
Keep rest config as same and click on Create Launch templete
Now go back to auto scaling group page refresh the page and provide name for auto scaling group and choose the templete you just created and click next
Select the VPC you created in network settings and choose both private subnet in Availability Zones and subnets and click next
Do not create any load balancer as of now and click next
Select your desired number of ec2 instances in the provided feild for eg- desired-2, min-1, max-4
Skip the notification and tags settings and click on create auto scaling group
Now got to EC2 instance and check where the ec2 instances are running, it must in 2 private subnet of your VPC
For deploying app in private subnet you need to login to ec2 instance but you cannot as it is running in private subnet so for to login into ec2 you need Bastion Host
## Bastion host acts as jump server or mediator between private and public subnet 
Create an ec2 instance and name it as bastion host
make sure to add security group which has access to SSH and in network setting click edit and add the same VPC you created 
Enable auto add public address ( without public address it cannot access inside VPC ) and click on launch instance
To deploy app first you need to login to bastion host from your PC and from bastion host login to private subnet ec2 instance
To ssh to private subnet you need key value pair whick is present in your PC
Copy the key value pair from your PC to bastion host
## command- ssh -i /home/ashu/Downlods/aws-login.pem /home/ashu/Downlods/aws-login.pem ubuntu@ip_address:/home/ubuntu



