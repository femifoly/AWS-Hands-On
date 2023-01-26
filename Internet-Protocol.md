# Internet Protocols - Public and Private IP addresses

### Scenario
Your role is a cloud support engineer at Amazon Web Services (AWS). During your shift, a customer from a Fortune 500 company requests assistance regarding a networking issue within their AWS infrastructure. The following is the email and an attachment regarding their architecture:
```
Ticket from your customer
Hello, Cloud Support!

We currently have one virtual private cloud (VPC) with a CIDR range of 10.0.0.0/16. 
In this VPC, we have two Amazon Elastic Compute Cloud (Amazon EC2) instances:
instance A and instance B. Even though both are in the same subnet and have the same 
configurations with AWS resources, instance A cannot reach the internet, and instance B
can reach the internet. I think it has something to do with the EC2 instances, but I'm not sure.
I also had a question about using a public range of IP address such as 12.0.0.0/16 for a VPC 
that I would like to launch. Would that cause any issues? Attached is our architecture for reference.

Thanks!
Jess
Cloud Admin
```

![Figure: The customer's architecture, which consists of a VPC, internet gateway, public subnet with instance A, and a public subnet with instance B](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/Arch.jpg)

Figure: The customer's architecture, which consists of a VPC, internet gateway, public subnet with instance A, and a public subnet with instance B.

### Task 1: Investigate the customer's environment
In the scenario, Jess, who is the customer requesting assistance, has two EC2 instances in one VPC. Instance A cannot reach the internet, and instance B can even though they are configured the same within the VPC. Currently, the customer's AWS architecture seems sound because one of their instances works. Jess suspects that the instance configuration may be the issue.

She also has a question about using a public range of IP addresses for the new VPC and has asked if you could provide further insight on her question.

You currently have one VPC with the same CIDR of 10.0.0.0/16 with two instances — instance A and instance B — with the same configurations as the customer. When troubleshooting networking and AWS, you can apply a troubleshooting method where you start from the top and work your way down or start from the bottom and work your way up. You start troubleshooting from the bottom and work your way to the top in layers using an example such as the OSI model. At the very bottom of this architecture is the EC2 instance. Although the cloud architecture does not directly translate to the OSI model, the following is an example of how the OSI and cloud relate.
![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/osi.jpg)

* For task 1, I gain an understanding of the customer's environment and replicate their issue.
* At the upper-right of these instructions, choose AWS. The AWS Management Console opens in a new tab.
  Once you are in the AWS console, type and search for EC2 in the search bar on the top-left corner. Select EC2 from the list.
  
  ![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/ec2.jpg)
  
* Please copy and paste the names and IP addresses of both instances for future reference in a text editor. 
  Select the check box next to instance A. At the bottom of the page, choose the Networking tab, and note the Public and Private IPv4 addresses.
  
![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/ec2a.jpg)

Once you copy and paste the name and IP addresses, deselect the instance, and then select instance B and do the same.  

![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/ec2b).jpg

** *Did you notice any differences?***
### ***It can be observered that instance A does not have any Public IP assigned to it***

### Task 2: Use SSH to connect to an Amazon Linux EC2 instance

In this task, you will connect to first connect to instance A and then to instance B instance. Note any observations.
You will use an SSH utility to perform all of these operations

* Open putty.exe
* Configure PuTTY timeout to keep the PuTTY session open for a longer period of time: 30
  Select Connection
  Set Seconds between keepalives to 30
  
![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/putty.jpg)

* Configure your PuTTY session:
  Select Session
  Host Name (or IP address): Paste the IPv4 address of instance A you made a note of earlier. Note: Should you use a Public or Private IP address to connect?
  
![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/putty1.jpg)

* Back in PuTTY, in the Connection list, expand  SSH
  Select Auth (don't expand it)
  Select Browse
  Browse to and select the lab#.ppk file that you downloaded
  Select Open to select it
  Select Open again.
  Select Yes, to trust and connect to the host.
  
![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/putty2.jpg)

* When prompted login as, enter: ec2-user
This will connect you to the EC2 instance.

## Repeat Task 2 for instance B

![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/puttyb.jpg)


![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/puttyb1.jpg)


![](https://github.com/femifoly/AWS-Projects/blob/main/AWS%20Projects/IP/puttyb2.jpg)

```
Question - Were you able to use the SSH to connect to both instances? Why or why not?

Answer: If you were not able to connect to instance A, it was due to this instance being assigned only a private IP address.
Private IP addresses cannot be accessed from outside the VPC. This is why you are only able to connect to instance B. 
Instance B has a public IP address assigned to it allowing access from outside the VPC, which allows you to use the 

SSH utility to connect to the instance.
```
## Task 3: Send the Response to the customer

The customer asked for your insight regarding using a public CIDR for a new VPC that she would like to launch. Refer to module 4 and gather some evidence and summarize a short explanation of your findings to explain to the customer why or why not you recommend this approach.


Recap
In this lab you have investigated the customer's environment and applied troubleshooting techniques that allowed you to resolve the customers’ issue. Within the scenario, you discovered that the customer's EC2 instance (instance A) needed a public IP address to connect to the internet. This was tested by using an SSH utility to connect to the instance. Private IP addresses are used within the VPC and cannot establish a connection to the internet. As module 4 noted, you discovered that using a public range of IP addresses for a VPC can result in complications from having replies back from other unrelated resources.
