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
