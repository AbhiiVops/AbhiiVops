---
title: "Unveiling the Blueprint: Scale Your Web Infrastructure on AWS in Minutes"
datePublished: Mon Nov 06 2023 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clueig5wm000308jt7fbv9ixt
slug: unveiling-the-blueprint-scale-your-web-infrastructure-on-aws-in-minutes
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1711827704293/3f03a685-8b25-4bf4-9f9a-b51223126a5b.png
tags: cloud, aws, cloud-computing, aws-lambda, infrastructure-as-code, web-infrastructure, aws-dynamodb

---

![](https://miro.medium.com/v2/resize:fit:1400/1*6nlILj0k_C4wPWaw5E3CFA.png align="left")

Ever dreamed of effortlessly scaling your web infrastructure to handle fluctuating traffic demands? Imagine a setup where your servers dynamically adjust to meet the needs of your users, all while maintaining impeccable performance. Intrigued?

Welcome to the gateway of exploring how to transform this dream into reality using the power of AWS. In this journey, we'll unravel the secrets of building a resilient and scalable web architecture, empowering you to conquer the ever-changing landscape of online traffic. So, buckle up as we embark on a thrilling expedition into the realm of cloud computing and automation.

We'll walk through the process of setting up a scalable web infrastructure on AWS, complete with a Virtual Private Cloud (VPC), public subnets, an autoscaling group, and an Application Load Balancer (ALB).

### In this blog, you'll learn:

1. 1. Create a VPC with cidr 10.10.0.0/16
        
    2. Create three public subnets with 10.10.1.0/24 & 10.10.2.0/24 & 10.10.3.0/24
        
    3. Create an autoscaling group using t2.micro instances. All instances should have apache installed on each instance with the ability to check any random IP address and be able to produce a test page. Ensure the autoscaling group is using the public subnets from #2.
        
    4. The autoscaling min and max should be 2 and 5.
        
    5. Create an Application Load Balancer to distribute traffic to the autoscaling group.
        
    6. Create web server security group that allows inbound traffic from HTTP from your Application Load Balancer.
        
    7. Create a load balancer security group that allows inbound traffic from HTTP from 0.0.0.0/0.
        

By the end of this guide, you'll have the knowledge and skills to build a scalable web infrastructure on AWS, ready to handle the demands of your growing web application. So let's dive in and get started!

## Section 1:

Log into your AWS Management Console: Once at the console, let click and let create the VPC and subnets.

Create a VPC with cidr 10.10.0.0/16:

1. Check VPC and more
    
2. Name the VPC. I went with “weekProject7.”
    
3. In the IPV4 Type 10.10.0.0/16
    

![](https://miro.medium.com/v2/resize:fit:1400/1*G80I1wy6bSUis-UUPNtzcA.jpeg align="left")

4\. Number of Availability zones, select three (3). This will give us us-east-1a, us-east-1b and us-east-c. keep in mind that your availability zone may be different. My region is US East (N. Virginia).

5\. Public Subnets, select three (3) again and for private select zero (0).

![](https://miro.medium.com/v2/resize:fit:1400/1*VA55eWGe1Hxi1kH0nt_kpA.png align="left")

6\. Nat gateway select none; VPC endpoint select S3 Gateway

7\. Once completed with the configurations click Create VPC, in the lower right hand corner. You should see the below screen, if so, you are now cooking with gasoline.

![](https://miro.medium.com/v2/resize:fit:1400/1*7zoRlnDnxhnOkNjxnpzQ2A.png align="left")

8\. Now that our VPCs and Subnets are created. Returned back to the AWS console click on EC2 and then click on the Launch Template.

![](https://miro.medium.com/v2/resize:fit:1400/1*KCAbdGlgnF5FJ3TS9posnw.png align="left")

9\. At the Launch template, name your template and check Auto Scaling guidance. I named my Launch template, “week7project.”

![](https://miro.medium.com/v2/resize:fit:1400/1*xUEJS_KhNjqt3CP0JMysVw.png align="left")

10\. Select Amazon Linux (AWS)

![](https://miro.medium.com/v2/resize:fit:1400/1*H6K13CEqm1Ez4vNCGff0hg.png align="left")

11\. Select Instance type t2.micro

![](https://miro.medium.com/v2/resize:fit:1400/1*XP2iZUfA48O03Vlawq_9Aw.png align="left")

12\. For the key pair, I am going to use a key pair that I have used previous, which “gold-luit-kp.”

![](https://miro.medium.com/v2/resize:fit:1400/1*KHqr6ciyGaWcHM2rrrThYA.png align="left")

12\. Network setting as always are important. It is what allows internet traffic to flow. We are going to allow and Allow SSH and HTTP

![](https://miro.medium.com/v2/resize:fit:1400/1*L_cGxwE_CCnzXezZQWQxrQ.png align="left")

Under Advance details; User data enter the following

```bash
#! /bin/bash
```

```bash
yum update -y 
```

```bash
yum install -y httpd
```

```bash
systemctl start httpd
```

```bash
systemctl enable httpd
```

![](https://miro.medium.com/v2/resize:fit:1226/1*Es4_pPabSlFVEyAwfM3jmw.png align="left")

Once at the end on the right hand side, click “create launch template.”

![](https://miro.medium.com/v2/resize:fit:1400/1*M6wXK6WdHmJC6lFnvfCf9A.png align="left")

If done correct you will see the successfully created, which is always a good thing. Let’s continue, now we need to create our Autoscaling group and Load balancer.

![](https://miro.medium.com/v2/resize:fit:1400/1*4W01Lrzmor-F0AW_Vsw_lg.png align="left")

![](https://miro.medium.com/v2/resize:fit:1400/1*p0ahyQXLHuJLGfq8yXovgA.png align="left")

Once completed, we can verify that our page will work by going to our instance that we created. Click on the instance and grab the IP address. upload the IP address into your web browser. If done correctly you will see the following.

![](https://miro.medium.com/v2/resize:fit:1400/1*ONHVEGtwCzt8DV7YNR1nNg.png align="left")

### Conclusion:

***If you've found this guide helpful, show your love with a 💓. Building a scalable web infrastructure on AWS is key for success in the digital age. Subscribe to our newsletter and follow us for more insightful blogs and stay tuned for future tech wonders. Thank you for joining us in exploring the world of cloud services. Happy building!***