Deploying an End to End solution with a Windows virtual Machine on AWS
Understand the scenario

In this project, you will deploy an End-to-End Solution in AWS. First, you will create a Virtual Private Cloud (VPC) environment for the EC2 instances. Next, you will create an Amazon S3 bucket that will hold the static web content for the website, and then you will create a custom EC2 launch template that includes the web server engine and an initial homepage for the website. Finally, you will deploy a web server based on the custom launch template, and then you will verify that the website is publicly available from the new EC2 instance.

Build a VPC environment

1. Verify that you are in the US East 2 (Ohio) region.
   
2. Create a new VPC by using the values in the following table. For any property that is not specified, use the default value.
   
Setting	Value

Name tag-	Web VPC 34115490
IPv4 CIDR block-	10.0.0.0/16
IPv6 CIDR block-	No IPv6 CIDR block
Tenancy	Default

3. You can use the Copy to clipboard feature to copy the associated text, and then you can paste the text into the browser.

4. Create two public subnets for Web VPC 34115490 by using the values in the following tables. For any property that is not specified, use the default value.
   
Web Subnet 1
Property	Value
Subnet name-	Web Subnet 1
Availability Zone-	us-east-2a
IPv4 CIDR block	-10.0.1.0/24

Web Subnet 2
Property	Value
Subnet name-	Web Subnet 2
Availability Zone-	us-east-2b
IPv4 CIDR block-	10.0.2.0/24

5. Configure both subnets to automatically assign public IPv4 addresses.
   
6. Create an internet gateway named Internet Gateway 34115490, and then attach it to Web VPC 34115490.
 
7. Associate Web Subnet 1 and Web Subnet 2 to the route table for the Web-VPC 34115490 VPC, and then change the name of the route table to Web RT 34115490.

8 . Add a route to the Web RT 34115490 route table by using 0.0.0.0/0 as the destination Internet Gateway 34115490 as the target.
Create an S3 storage solution

9. Download the AWS_TE.pdf and expert-logo.jpg files, and then save the files on your local computer.
    
10. Create a new S3 bucket named myrcbfiles-34115490, enable versioning for the bucket, and then enable server-side encryption by using the Amazon S3 key (SSE-S3) encryption key.
    
11. Create two folders named images and docs in the webfiles-34115490 bucket.
  
12. Upload expert-logo.jpg to the images folder, and then upload AWS_TE.pdf to the docs folder.
  
13. Enable public access for the webfiles-34115490 bucket, and then make the two folders public.
    
14. Create a lifecycle rule named docs policy that will transition current versions of all objects in the docs/ folder to the Intelligent-Tiering storage class after 90 days and will delete previous versions after 30 days.
    
15. Create a security group named Web34115490-sg that uses the Web VPC and the description Allow RDP and HTTP, and then add inbound rules that allow RDP from My IP and HTTP from Anywhere.
    
16. Create an EC2 key pair named 34115490KeyPair by using the pem format.
    
17. Launch an EC2 instance by using the values in the following table. For any property that is not specified, use the default value.
    
Property	Value

Name-	Web-starter-34115490
AMI-	Microsoft Windows Server 2019 Base
Instance type-	t2.micro
Key pair-	34115490KeyPair
Network VPC-	Web VPC 34115490
Subnet-	Web Subnet 1 | us-east-2a
Security group-	Web34115490-sg
User data-	insert user data script
 
18. onnect to the Web-starter-34115490 instance from the AWS Management Console by using the RDP client, generate a password, and then sign in as Administrator using the password that you copied.
    
19. You may need to wait up to four minutes before you can generate the password you will need for the RDP connection.
    
20. In the RDP session, create a file named index.html in c:\inetpub\wwwroot, and then add the appropriate content.

21. Create a file named hw.css in c:\inetpub\wwwroot, and then add the appropriate content.

22. Create a new AMI named IIS-Starter-34115490 by using the Web-starter-34115490 EC2 instance.

23. Create a launch template by using the values in the following table. For any property that is not specified, use the default value.

Property	Value

Launch template name-	IIS-template-34115490
Template version description-	Custom IIS web server
AMI	IIS-Starter- 34115490
Key pair-	34115490KeyPair
Security group-	Web34115490-sg

24. Launch a new EC2 instance by using the IIS-Starter-34115490 launch template and the values in the following table. For any property that is not specified, use the default value.
    
Property	Value

Instance type-	t2.micro
Subnet-	Web Subnet 2
Tag Key-	Name
Tag Value-	Web-Final-34115490

25. Record the public IP address of the Web-Final-34115490 instance in the following Public IP Address text box: Public IP Address

Verify that you can connect to Public IP Address

![output](https://github.com/sumukhsm/Deploying-an-End-to-End-solution-with-a-Windows-virtual-Machine-on-AWS/assets/144142565/7ea8956b-056e-4d01-a9c4-85ae9cc06390)
