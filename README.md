# Login to AWS account search for VPC and click on "create VPC"
# Go for " VPC and more " for better and easy config of network components
# Select a project name 
# Keep the CIDR range as same 
# keep the availability zones as 2 for better traffic management
# Keep the public and private subnet as 2 
# Nat Gateaway as 1 per AZ
# Keep endpoint as NONE 
# Click on Create VPC
# VPC gets created successfully 
# Create Auto Scaling group by going to EC2 instance and scroll down
# Auto Scaling group cannot be created directly so you need to first create Launch Templete 
# Click on Create launch temeplete and provide necessary details
# In network setting part in launch tempelete click on create security group and provide details
## it is always recommended to open the port in which your app is running instead of opening all the ports 
# For this project first open ssh port from anywhere second add another rule and open port which is required for eg- port 8000 using custome TCP
# Keep rest config as same and click on Create Launch templete
# Now go back to auto scaling group page refresh the page and provide name for auto scaling group and choose the templete you just created and click next
# Select the VPC you created in network settings and choose both private subnet in Availability Zones and subnets and click next
# Do not create any load balancer as of now and click next
# Select your desired number of ec2 instances in the provided feild for eg- desired-2, min-1, max-4
# Skip the notification and tags settings and click on create auto scaling group
# Now got to EC2 instance and check where the ec2 instances are running, it must in 2 private subnet of your VPC
# For deploying app in private subnet you need to login to ec2 instance but you cannot as it is running in private subnet so for to login into ec2 you need Bastion Host
## Bastion host acts as jump server or mediator between private and public subnet 
# Create an ec2 instance and name it as bastion host
# make sure to add security group which has access to SSH and in network setting click edit and add the same VPC you created 
# Enable auto add public address ( without public address it cannot access inside VPC ) and click on launch instance
# To deploy app first you need to login to bastion host from your PC and from bastion host login to private subnet ec2 instance
# To ssh to private subnet you need key value pair whick is present in your PC
# Copy the key value pair from your PC to bastion host
## command- ssh -i /home/ashu/Downlods/aws-login.pem /home/ashu/Downlods/aws-login.pem ubuntu@ip_address:/home/ubuntu
# login into bastion host and again login into private subnet using bastion host
# create a index.html page and copy a basic html page from the internet and save the file
# type " python3 -m http.server 8000 " to run the server in port 8000
# we have install pyhton app in one of the private subnet to check when we use load balancer wether it shows error for other private subnet
# Go to ec2 scroll down and click on load balancer and then click on create load balancer
# Select Application Load balancer and click on create
# Provide name and click on internet facing option
# Load balancer should always be on public subnet so in network mapping select your VPC and select both public subnet 
# Then you need to add target group so that you can access your ec2 instances so click on create target group
# select Instance and provide target group name and provide the correct port number keep everything else same and click on next 
# select both the private ec2 instances and click on " include as per pending below " and click on create target group
# Go back to creating load balacer and add the target group ( wait for sometime to reflect )
# Create the load balancer using default port 80
# You will see an error saying port 80 is not reachable to fix it go to security group edit inbound rules and add port 80 in the rules
# After adding port 80 in rules the error should dissapear 
### Copy the DNS name paste in browser and you should be able to see the HTML page ( SUCCESS )


