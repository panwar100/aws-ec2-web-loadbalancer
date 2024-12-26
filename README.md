# aws-ec2-web-loadbalancer
# Load Balancing with Two EC2 Instances for Web Hosting

This guide demonstrates how to set up load balancing for two EC2 instances hosting a web application. We will use an Application Load Balancer (ALB) in AWS to distribute traffic between the instances.

## Prerequisites

1. An AWS account.
2. Two EC2 instances running a web server (e.g., Apache or Nginx) with your web application deployed.
3. Security groups configured to allow HTTP (port 80) traffic.

## Steps

## 1. Launch EC2 Instances
- Launch two EC2 instances in the same VPC.

![Screenshot from 2024-12-26 22-12-07](https://github.com/user-attachments/assets/9b5d50e2-5ad8-407a-9e7f-f9617e481b00)
![Screenshot from 2024-12-26 22-12-47](https://github.com/user-attachments/assets/04963664-0372-4915-95b9-2f961649bc7a)
![Screenshot from 2024-12-26 22-13-16](https://github.com/user-attachments/assets/a1b8a56e-0776-4da2-9a48-0a8e8b796e17)
![Screenshot from 2024-12-26 22-13-45](https://github.com/user-attachments/assets/3c11e323-dc62-4647-81c5-4ee13b11b166)
![Screenshot from 2024-12-26 22-59-37](https://github.com/user-attachments/assets/430611ba-2ce7-4556-8931-bac7750a5715)

- Install and configure a web server (e.g., Apache or Nginx) on each instance.

![Screenshot from 2024-12-26 23-03-55](https://github.com/user-attachments/assets/303b0d17-a091-42bd-b346-9b41b4d99b33)
![Screenshot from 2024-12-26 23-10-26](https://github.com/user-attachments/assets/79af3e2d-d202-4308-93c4-ad8e4a2e23d2)
![Screenshot from 2024-12-26 23-15-41](https://github.com/user-attachments/assets/2d32b5a2-8a0a-4a39-9588-557bc404e0bd)

- Deploy your web application to both instances.

for web1
![Screenshot from 2024-12-26 23-13-53](https://github.com/user-attachments/assets/6c0ec28f-8c32-433c-b1db-004ed59b066d)


for web2
![Screenshot from 2024-12-26 23-28-49](https://github.com/user-attachments/assets/6f258c0c-2fb4-4a90-9b21-a77d6181a1ec)


## 2. Configure Security Groups
- Ensure both instances have a security group allowing inbound traffic on port 80.

## 3. Configure Target Group
- Create a new target group:

![Screenshot from 2024-12-26 23-34-07](https://github.com/user-attachments/assets/987bd66e-e16e-4279-b038-15b48ce8328c)
  
  - **Name**: Provide a name for the target group.
  - **Target type**: Instances.
  - **Protocol**: HTTP.
  - **Port**: 80.
  - **Health Check**: Configure health check settings.

![Screenshot from 2024-12-26 23-35-58](https://github.com/user-attachments/assets/d3d8f42d-585c-4da5-9ddc-15eb8dd45ca7)

- Register your two EC2 instances as targets.

![Screenshot from 2024-12-26 23-36-36](https://github.com/user-attachments/assets/30aa76c6-c4f8-48f7-9d06-79f393cec859)
![Screenshot from 2024-12-26 23-37-04](https://github.com/user-attachments/assets/c8a67871-9628-4eff-8bdd-df46ed955b95)
![Screenshot from 2024-12-26 23-37-19](https://github.com/user-attachments/assets/0e18dcb8-90f9-44d3-9405-3638e8f23124)


## 4. Create an Application Load Balancer (ALB)
- Navigate to the **EC2** dashboard in the AWS Management Console.
- Under **Load Balancing**, select **Load Balancers** and click **Create Load Balancer**.

![Screenshot from 2024-12-26 23-39-05](https://github.com/user-attachments/assets/a5c5e12c-b6eb-4e59-8e98-ead86a665967)


- Choose **Application Load Balancer**.
  - **Name**: Provide a name for the ALB.
  - **Scheme**: Internet-facing.
  - **Listeners**: Add a listener for HTTP (port 80).
  - **Availability Zones**: Select at least two availability zones.
- Click **Next** to configure security settings. 

![Screenshot from 2024-12-26 23-39-22](https://github.com/user-attachments/assets/0593e7c7-4bfc-4e96-86f4-976b269b9719)
![Screenshot from 2024-12-26 23-41-07](https://github.com/user-attachments/assets/09492631-e3f6-4642-9234-8a608a8f92b0)
![Screenshot from 2024-12-26 23-41-19](https://github.com/user-attachments/assets/50005653-3745-4195-b883-bc1d940be32b)
![Screenshot from 2024-12-26 23-41-40](https://github.com/user-attachments/assets/f73e87b1-d39d-4e6f-89d2-55eec367d90e)
![Screenshot from 2024-12-26 23-41-59](https://github.com/user-attachments/assets/09e6c802-04ca-4e70-9d04-01658bb99321)
![Screenshot from 2024-12-26 23-42-51](https://github.com/user-attachments/assets/22bce57b-9f1c-4d73-9bde-bc0ac3c7908c)

## 6. Test the Setup
- Obtain the DNS name of the ALB from the AWS Management Console.

![Screenshot from 2024-12-26 23-45-32](https://github.com/user-attachments/assets/aed14d4a-fbf9-4d2e-aef8-8ffcb92327e7)

- Access the DNS name in your browser. Traffic should be distributed between the two EC2 instances.

![Screenshot from 2024-12-26 23-45-46](https://github.com/user-attachments/assets/86864487-e703-4337-b3cf-f00185a3614a)
![Screenshot from 2024-12-26 23-45-55](https://github.com/user-attachments/assets/a67ff968-a691-4ca0-84ba-c47b332d9675)

**When accessing the ALB DNS name, you should see the messages alternate as traffic is routed to different instances.**

## Diagram

```plaintext
[Client] --> [ALB (DNS Name)] --> [EC2 Instance 1]
                                --> [EC2 Instance 2]
```

## Notes

- Ensure your instances and ALB are in the same VPC.
- Monitor the ALB and target group health status for issues.
- For a production setup, consider using HTTPS and configuring SSL/TLS.

---

Feel free to contribute to this project by submitting issues or pull requests!

