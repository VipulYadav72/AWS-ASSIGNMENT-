

**Student:** Vipul Yadav  
**Prefix used:** Vipul_Yadav

## Design Summary 
Created 1 VPC (`10.0.0.0/16`) and split into two public subnets and two private subnets across two availability zones. Public subnets route to an Internet Gateway (IGW). A NAT **Instance** (t2.micro) is placed in a public subnet with an Elastic IP and configured to perform NAT (IP forwarding + iptables). Private subnets route internet-bound traffic through the NAT instance.

## CIDR Ranges (exact)
- VPC: `10.0.0.0/16`
- Public Subnet A: `10.0.1.0/24`
- Public Subnet B: `10.0.2.0/24`
- Private Subnet A: `10.0.11.0/24`
- Private Subnet B: `10.0.12.0/24`

**Reasoning:** /16 VPC allows many subnets; /24 per subnet is simple and adequate for the assignment. Private/public separated by third-octet for clarity.
- `main.tf` — Terraform single-file that builds all resources
- `screenshots/`
  - `vpc.png`
  - `subnets_all.png`
  - `igw.png`
  - `route_public.png`
  - `nat_instance.png`
  - `route_private.png`
1. Install Terraform >= 1.0 and configure AWS credentials (`aws configure` or environment variables).
2. (Optional) find your public IP: `curl -s ifconfig.me`  
3. From the `question1` directory:
   ```bash
   terraform init
   terraform plan -var="prefix=Vipul_Yadav" -var="aws_region=us-east-1" -var="my_ip=YOUR_IP/32"
   terraform apply -var="prefix=Vipul_Yadav" -var="aws_region=us-east-1" -var="my_ip=YOUR_IP/32"
