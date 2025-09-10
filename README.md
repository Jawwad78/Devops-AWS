

## 🧠 AWS Networking & Auto Scaling Assignment

This project shows how I built a full VPC setup with public and private subnets, NAT, a Bastion Host, EC2 web servers, an Application Load Balancer, CloudWatch monitoring, and an Auto Scaling Group that replaces unhealthy instances automatically.

### ✅ What I Set Up

1. **VPC** with `10.0.0.0/16` CIDR
   Two subnets

   * Public → `10.0.1.0/24`
   * Private → `10.0.2.0/24`

2. **Internet Gateway** for public subnet
   **NAT Gateway** to give internet access to private subnet EC2s
   Custom **route tables** linked properly

3. **Bastion Host EC2** in public subnet with SSH access from my IP
   Used `ssh -A` and `ssh-add` to connect to private EC2 via Bastion

4. **Private EC2** in private subnet
   Accessed internet through NAT
   Installed packages via `yum`, tested `curl`
   Confirmed no direct SSH access from internet

5. **Apache Web Server** running on EC2
   Installed with user data script
   Showed hostname in browser

6. **Application Load Balancer**

   * Public access via ALB DNS
   * Target group with health checks on `/`
   * Only ALB SG allowed to talk to EC2s on port 80

7. **CloudWatch Agent** installed
   Monitored EC2 metrics (CPU, memory, etc.)

8. **Auto Scaling Group**

   * Launch template included Apache setup
   * ASG launched EC2s into public subnets across AZs
   * ALB target group used for health checks
   * ASG replaced unhealthy EC2s
   * Scaling worked with desired capacity changes
   * ALB load balanced between instances correctly

### 🔍 Key Things I Learned

* ASG EC2s inherit security groups from the launch template
* ALB health checks must be working for ASG to replace instances
* Testing should be done via ALB DNS, not EC2 IP
* Bastion Host is needed to reach private instances securely
* Security Groups must be scoped properly — no public HTTP on EC2s

---

📸 I also took screenshots of each setup (VPC, ALB, EC2s, ASG, CloudWatch etc.) and will upload them to this repo manually.

