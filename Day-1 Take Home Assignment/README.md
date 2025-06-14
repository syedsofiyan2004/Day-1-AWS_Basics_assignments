# DAY-1 Take Home Assignment-1

  ## **Building a Two-tier Application Infrastructure:**

In this assignment, I built a two-tier web application infrastructure using AWS. This setup included creating a VPC, subnets, an Internet Gateway, route tables, security groups, and EC2 instances.

Firstly, I created a Virtual Private Cloud (VPC) named **sofiyan-two-tier-vpc** with CIDR block **10.10.0.0/16**. This VPC acts as a private network inside AWS, isolating my resources securely.
![Screenshot 2025-06-11 192509](https://github.com/user-attachments/assets/41e3b2f0-f0ec-4f04-b05b-669d814b36dc)
![Screenshot 2025-06-11 192531](https://github.com/user-attachments/assets/2d2a5563-89c2-460f-913e-a04a9718895b)

Next, within this VPC, I created two subnets:
A public subnet called **sofiyan-public-subnet-1** with CIDR **10.10.1.0/24**, allowing internet access.
A private subnet named **sofiyan-private-subnet-1** with CIDR **10.10.2.0/24**, which remains isolated from public internet access.
![Screenshot 2025-06-11 192938](https://github.com/user-attachments/assets/420f48ef-831e-4aac-b906-b3e3c18dd0f0)
![Screenshot 2025-06-11 193532](https://github.com/user-attachments/assets/c311ee52-570b-4ba1-9921-ea9077104372)
![Screenshot 2025-06-11 193635](https://github.com/user-attachments/assets/f5d3433a-40bb-4e57-a795-0ed1901a06d8)
![Screenshot 2025-06-11 193645](https://github.com/user-attachments/assets/5f0e659f-b6df-4f62-ab06-19b8ace5b446)

After setting up the subnets, I created an Internet Gateway named **sofiyan-two-tier-igw** and attached it to my VPC. This step is necessary for resources in the public subnet to communicate with the internet.
![Screenshot 2025-06-11 193730](https://github.com/user-attachments/assets/6d56a0d1-e2c4-41dc-9cde-61b6df09df21)
![Screenshot 2025-06-11 193744](https://github.com/user-attachments/assets/79910267-004f-4687-a2fd-7157d9f69a97)
![Screenshot 2025-06-11 193756](https://github.com/user-attachments/assets/f4ac67fb-43c5-4c25-8af7-90d869ffc55c)

Then, I configured the main Route Table of the VPC, adding a route to direct all internet-bound traffic (0.0.0.0/0) to the Internet Gateway. I associated this route table explicitly with the public subnet, keeping the private subnet secure without internet access.
![Screenshot 2025-06-11 193853](https://github.com/user-attachments/assets/fabe17d6-f0b0-4b63-be17-3990eb5de767)
![Screenshot 2025-06-11 193903](https://github.com/user-attachments/assets/eafb8565-1789-46c8-adad-90f18822f4d4)
![Screenshot 2025-06-11 193918](https://github.com/user-attachments/assets/fc82a3ba-e000-4c3e-a47d-2ae2193d748a)
![Screenshot 2025-06-11 193953](https://github.com/user-attachments/assets/aa5cac2c-cbaa-4c09-9c51-effe58bc7816)
![Screenshot 2025-06-11 194007](https://github.com/user-attachments/assets/c2332522-927f-4981-8bf4-182464ca78ef)

Moving on to security, I created two Security Groups:

Web Server Security Group (**sofiyan-webapp-sg**):
Allowed inbound HTTP traffic (**port 80**) from anywhere.
Allowed inbound SSH access (**port 22**) only from my IP.
![Screenshot 2025-06-11 194647](https://github.com/user-attachments/assets/5dda8f78-f14b-4cc5-b999-00874eb644e9)
![Screenshot 2025-06-11 195039](https://github.com/user-attachments/assets/f9f1d06d-a835-42e0-8880-c042238b31a5)

Database Security Group (**sofiyan-database-sg**):
Allowed inbound MySQL/Aurora traffic (**port 3306**) only from the webapp-sg group.
Ensured no public access by restricting other inbound rules.
![Screenshot 2025-06-11 195408](https://github.com/user-attachments/assets/1cca6ea7-cae9-430e-9ef6-de7f40205e5b)
![Screenshot 2025-06-11 195434](https://github.com/user-attachments/assets/d1d90c08-6395-4d22-9fc2-3d692dd2218c)
![Screenshot 2025-06-11 195452](https://github.com/user-attachments/assets/5e310cf2-8178-4c0f-92e4-4bd865097e48)

Meanwhile, I have created a route table for private subnet named **sofiyan-private-rt** without it having an Internet Access and also connected that route table to the Subnet using Subnet Association.
![Screenshot 2025-06-11 195933](https://github.com/user-attachments/assets/e1bd7afb-f2ad-4db6-a470-07f1dd8dece7)
![Screenshot 2025-06-11 195947](https://github.com/user-attachments/assets/ca5d7236-e191-47fb-b519-2dadd36421e6)
![Screenshot 2025-06-11 195958](https://github.com/user-attachments/assets/b5554eb4-6744-4a2d-986f-6c3bb18cc3ae)
![Screenshot 2025-06-11 200009](https://github.com/user-attachments/assets/95356cd1-1c89-4059-86a5-2295dd894f14)

With the security and networking in place, I launched two EC2 instances:
Web-Server, deployed in the **sofiyan-public-subnet-1**, associated with the **sofiyan-webapp-sg**, and enabled public IP assignment.
![Screenshot 2025-06-11 224336](https://github.com/user-attachments/assets/6c65f0f3-6e6f-4719-9332-f0cd7d6757a7)
![Screenshot 2025-06-11 224352](https://github.com/user-attachments/assets/c6f93dff-a3e2-498e-bc8d-ff66f6c27bea)
![Screenshot 2025-06-11 224402](https://github.com/user-attachments/assets/629d8daa-f08a-47a6-9c22-44d4480758be)
![Screenshot 2025-06-11 224414](https://github.com/user-attachments/assets/7a68edb5-354f-4b54-a163-ee0af2372d31)
![Screenshot 2025-06-11 224441](https://github.com/user-attachments/assets/bb91b8ef-c7f5-4119-961a-fba2d34e865f)

After getting the IP of the Ec2 Instance of web-app i have directed to that IP Address and it was working:
![Screenshot 2025-06-11 225130](https://github.com/user-attachments/assets/ff01b06b-ca7d-448c-9485-f3f11edf0370)

DB-Server, deployed in the **sofiyan-private-subnet-1**, associated with the **sofiyan-database-sg**, without a public IP, thus keeping it isolated from the internet.
![Screenshot 2025-06-11 224658](https://github.com/user-attachments/assets/eed00241-4a19-4f6f-9c5e-40f52164bb33)
![Screenshot 2025-06-11 224717](https://github.com/user-attachments/assets/f636db7f-b925-40b6-bb20-136b6038ced6)
![Screenshot 2025-06-11 224747](https://github.com/user-attachments/assets/9f8e3759-b45e-436f-965b-50e15f826e4f)
![Screenshot 2025-06-11 224956](https://github.com/user-attachments/assets/c222f528-1d62-4b73-a63f-27ad9d472e40)
![Screenshot 2025-06-11 225029](https://github.com/user-attachments/assets/8506d8fd-1cf2-4bb9-b922-6305ea960f16)
![Screenshot 2025-06-11 225051](https://github.com/user-attachments/assets/44d0a0c1-e315-4df4-b031-3303c0c79519)

After launching both instances, I verified connectivity by:
Accessing the web server’s public IP via a browser successfully.
![Screenshot 2025-06-11 225130](https://github.com/user-attachments/assets/224d263b-a673-4cc4-837b-dcf8449ad9dc)

SSH into the web server and pinged the database server’s private IP,it was not pinging the database as it was not having any Internet access it looks something like this.
I typed the following command to SSH into web server instance:
```sh
ssh -i sofiyan-kp.pem ec2-user@3.110.120.186
```
then i used this command to ping my database Private IP Address:
```sh
ping 10.10.2.215
```
![Screenshot 2025-06-11 225527](https://github.com/user-attachments/assets/9cbbf0e6-366b-46ce-b9ba-9658977c7268)
![Screenshot 2025-06-11 225730](https://github.com/user-attachments/assets/8d219551-8ca5-49f1-a0e3-a5112cf8c32b)

Confirmed that the database server couldn't access the internet directly, ensuring its secure isolation.

As I didnt get any output even after exiting the command i tried for second time and got this output:
<img width="951" alt="image (1)" src="https://github.com/user-attachments/assets/b2fdc1c1-38cb-4fbb-b91b-d032e4b87475" />

Now to give internet Access to the database Instance without making it public we can give it Internet Access through NAT Gateway.
So first we need to create Elastic IPs:
![Screenshot 2025-06-11 230927](https://github.com/user-attachments/assets/846c7e45-5835-4dcf-a23a-74df442a4d63)
![Screenshot 2025-06-11 231011](https://github.com/user-attachments/assets/99441435-a296-4b45-8e39-aae35e677113)

then i have created a NAT Gateway with name **sofiyan-NAT-gateway**:
![Screenshot 2025-06-11 231123](https://github.com/user-attachments/assets/2c311bcd-2545-41bf-a5e4-088b4498cf61)
![Screenshot 2025-06-11 231137](https://github.com/user-attachments/assets/327a61bb-7795-4076-89ab-3ed30e990e36)

After Creating a NAT Gateway i have connected that NAT Gateway to the Private Route which i have created for private subnet
![Screenshot 2025-06-11 231221](https://github.com/user-attachments/assets/6a5164cf-69f9-455a-af3e-6b97e7b4e648)
![Screenshot 2025-06-11 231229](https://github.com/user-attachments/assets/1622b934-f9b2-4a58-a5b8-4dea53148523)

Finally then Again i tried pinging **google.com** from private Instance of DB and then it got Pinged:
![Screenshot 2025-06-11 233300](https://github.com/user-attachments/assets/004337f3-92fa-4c0c-8b01-a16ab72bd346)

# This is the final Deliverable for this Assignment


Now comes the Cleanup Part i have deleted all the resources after the completion of the Assignment
![Screenshot 2025-06-11 233406](https://github.com/user-attachments/assets/6ba666fe-c70b-4cc5-811a-fc171cbeefcf)
![Screenshot 2025-06-11 233611](https://github.com/user-attachments/assets/039d49fd-5bbc-43be-b6f0-87f147b97bdf)
![Screenshot 2025-06-11 233722](https://github.com/user-attachments/assets/0eef2464-397e-4fd8-88bc-a77bc9917765)
![Screenshot 2025-06-11 233754](https://github.com/user-attachments/assets/d7c092a0-ab72-4b2c-9764-6f6914a22853)

![Screenshot 2025-06-11 234157](https://github.com/user-attachments/assets/781e374f-7ef2-4944-bf77-5da98ac28b23)
![Screenshot 2025-06-11 234207](https://github.com/user-attachments/assets/8ec8dc61-b74e-421f-bf78-d43ee8a8376a)
![Screenshot 2025-06-11 234212](https://github.com/user-attachments/assets/01934dd7-f689-48b6-b87a-98765e304a27)
![Screenshot 2025-06-11 234217](https://github.com/user-attachments/assets/52e33238-f5c3-4924-8a83-41f93540fe69)
![Screenshot 2025-06-11 234224](https://github.com/user-attachments/assets/46e34112-f5f5-4bc9-b5cb-d8f6f460d6fc)
![Screenshot 2025-06-11 234237](https://github.com/user-attachments/assets/8cf22bb7-0e3a-4818-bfd3-97320d4988e2)
![Screenshot 2025-06-11 234304](https://github.com/user-attachments/assets/d6dfa658-643b-4f2a-8969-a8f68fc48f90)

There is Nothing Left except the default ones


# End of the Assignment








































