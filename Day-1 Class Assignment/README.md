# AWS-Basics-Assignment

In this Assignment we are Walking through the basics AWS infrastructure on creating keypairs,VPCs,Subnets,Route Tables,Security Groups.

First, I started by creating a key pair in EC2. This key pair allows me to securely connect to my EC2 instance using SSH if required. 
Without the key pair, I wouldn't have access to my server directly.
![Screenshot 2025-06-11 121845](https://github.com/user-attachments/assets/12582633-2278-4c2a-811c-a444f4739d0c)

![Screenshot 2025-06-11 121900](https://github.com/user-attachments/assets/b227216f-fd28-4d9c-86c5-7be86907e613)

After that, I moved on to set up the networking part by creating a Virtual Private Cloud (VPC), which basically acts like my own private network inside AWS where all my resources would be deployed. While creating the VPC, I specified a CIDR block to define the IP address range.
![Screenshot 2025-06-11 121913](https://github.com/user-attachments/assets/572e258b-0553-4a89-b7d9-3c31885a1ade)

![Screenshot 2025-06-11 121926](https://github.com/user-attachments/assets/ad077ae3-887e-4e58-bd94-b0c85047d52a)

Once the VPC was ready, I created a subnet within the VPC. Subnets help divide the VPC into smaller, manageable networks. In this case, I created a public subnet because I wanted my EC2 instance to be accessible from the internet.
![Screenshot 2025-06-11 122006](https://github.com/user-attachments/assets/84d1a9bb-80d7-4172-a1c8-a6dca75c3942)

Then I created an Internet Gateway. This component allows my VPC and its resources to communicate with the internet. After creating it, I attached the Internet Gateway to my VPC to enable external access.
![Screenshot 2025-06-11 122114](https://github.com/user-attachments/assets/2792b2ab-88eb-428d-b0fd-d56e707763b4)

![Screenshot 2025-06-11 122208](https://github.com/user-attachments/assets/b83f9479-1e68-4a1e-82f0-8ea85556cb8f)

![Screenshot 2025-06-11 122220](https://github.com/user-attachments/assets/fc04ec23-32fb-4be7-8173-7b5dec7eaf0b)

Next, I configured the routing by creating a Route Table. Inside the route table, I added a route that directs all outbound internet traffic (0.0.0.0/0) to the Internet Gateway. After configuring the route, I associated this route table with my public subnet so any resource inside the subnet can access the internet.
![Screenshot 2025-06-11 122601](https://github.com/user-attachments/assets/7cf51ae5-9c5f-4738-94e6-3bb2b3db5796)

![Screenshot 2025-06-11 122612](https://github.com/user-attachments/assets/b96eb9bd-e263-4dc2-a5c8-7e171ebb7824)

![Screenshot 2025-06-11 122642](https://github.com/user-attachments/assets/c25bd242-9dfa-4904-be79-1772fb9a858a)

![Screenshot 2025-06-11 122709](https://github.com/user-attachments/assets/4a0974fc-f727-4595-8cc1-f41c13ec0b86)

The resource Map Looks something like this after creating and connecting each of them.
![Screenshot 2025-06-11 123018](https://github.com/user-attachments/assets/a629752c-958b-44b9-9310-b558c0b3a3d4)

After networking was complete, I created a Security Group, which acts like a virtual firewall for my EC2 instance. I allowed inbound traffic on port 80 (HTTP) so that my application can be accessed via browser. For outbound traffic, I allowed all traffic so that my instance can freely communicate with external services.
![Screenshot 2025-06-11 123238](https://github.com/user-attachments/assets/8824874b-e3f5-4f6c-a877-b3e3b9592b33)

![Screenshot 2025-06-11 123310](https://github.com/user-attachments/assets/f080df82-aeff-42d7-b708-d2595bf9d3d1)

With all the setup complete, I finally launched my EC2 instance inside the subnet I created. During the launch, I selected the key pair I had created earlier, attached the Security Group, and selected the correct subnet. After the instance was launched, I deployed my application on it, and because the routing and security configurations were correct, I was able to successfully access my application from the browser using the public IP of the instance.

![Screenshot 2025-06-11 123508](https://github.com/user-attachments/assets/01390516-9cba-4a3f-9a08-d2ed5ad7a64a)

![Screenshot 2025-06-11 123517](https://github.com/user-attachments/assets/1d197d28-05ad-4004-91f0-b752b7303d83)

in this image the Auto assign Public IP is Disabled but later it was enabled but the Screenshot wasnt taken for that
![Screenshot 2025-06-11 123522](https://github.com/user-attachments/assets/c94fba69-5ba5-4efa-8e75-4cf98bcba61c)

![image](https://github.com/user-attachments/assets/bbb21315-3459-4fd3-a460-8cc9782aaa64)

![Screenshot 2025-06-11 131638](https://github.com/user-attachments/assets/05b65636-68f0-435f-bfd0-387d28a889de)

![Screenshot 2025-06-11 131415](https://github.com/user-attachments/assets/b75c6ab2-1c84-4d18-a036-84e02b5633ca)

Make sure when you are running the IP address it shouldnt be https it should be http then only it will run as you have given the inbound rule only for http.
![Screenshot 2025-06-11 131313](https://github.com/user-attachments/assets/48f63550-3bde-48b2-9eda-da7ad469cf6d)

Now that the Application has runned Successfully we have to follow up the cleanup Process which includes deleting all the created AWS services such as EC2 Instances,VPCs,Subnets etc..

After completing my testing and deployment, I made sure to clean up all the resources to avoid unnecessary charges. I started by terminating the EC2 instance. Once the instance was terminated, I deleted the Security Group that I had created for this deployment. After that, I disassociated and deleted the Route Table. Then I detached the Internet Gateway from the VPC and deleted it. Following that, I deleted the Subnet that was part of the VPC. Finally, I deleted the VPC itself. As the last step, I also deleted the key pair that was originally created for accessing the EC2 instance. This way, I ensured that all resources were properly cleaned up and nothing was left running in my AWS account.

Ec2 Instance Deleted
![Screenshot 2025-06-11 132329](https://github.com/user-attachments/assets/ca1ab580-43cc-4e48-bcf5-acd43ede5dde)

![Screenshot 2025-06-11 132710](https://github.com/user-attachments/assets/469d84b4-1ab8-4a6a-a244-dd837bbb9580)

Detaching and Deleting Internet gateway
![Screenshot 2025-06-11 133459](https://github.com/user-attachments/assets/790e6493-7007-4727-ace6-40f8340895b6)

![Screenshot 2025-06-11 133526](https://github.com/user-attachments/assets/449f4c1f-f0e3-45af-9a4c-b64879191e35)

Deleting Subnet
![Screenshot 2025-06-11 133312](https://github.com/user-attachments/assets/ff15a214-1587-41a4-a579-857844dac67c)

Deleting VPCs which automatically deletes the Route Table attached to it
![Screenshot 2025-06-11 133616](https://github.com/user-attachments/assets/a3cb091e-bf2c-4d37-955e-28ede01fcae1)

The after CleanUp Screenshots which confirms there is nothing except the default ones:
![Screenshot 2025-06-11 133628](https://github.com/user-attachments/assets/58d68b4f-3ed8-4344-af6e-613529b9e0fb)

![Screenshot 2025-06-11 133638](https://github.com/user-attachments/assets/3056929a-a5bb-4926-be4a-6a69502b163d)

![Screenshot 2025-06-11 133653](https://github.com/user-attachments/assets/086ff0a1-b653-44ce-9d2e-d46458873b71)

![Screenshot 2025-06-11 133659](https://github.com/user-attachments/assets/440e34cb-b954-4a9b-9576-3fe25c5802bc)

![Screenshot 2025-06-11 133725](https://github.com/user-attachments/assets/11fa3fde-dec1-40c7-bc61-f21708f46bae)

![Screenshot 2025-06-11 133831](https://github.com/user-attachments/assets/6fe91fd6-8c3d-468c-b6e9-873f9f5b7bc8)

The CleanUp is Also done Successfully.

### **End of Assignment** 











