# -VPC-Peering-Between-Two-AWS-VPCs
This project demonstrates how to design and implement a secure VPC Peering connection between two AWS Virtual Private Clouds (VPCs) to enable private communication across isolated networks — without using the public internet.

By completing this project, I strengthened my understanding of AWS networking, routing, and IAM-based access controls — key skills for cloud and DevOps engineers.

📅 Project Duration

May 2024 – June 2024

🧠 Objective

To establish a VPC Peering connection between two isolated AWS VPCs, configure CIDR blocks, route tables, and security groups, and verify inter-VPC communication between EC2 instances securely over AWS’s private network.

⚙️ Architecture Overview
+-------------------+                     +-------------------+
|     VPC-A         |                     |     VPC-B         |
|  CIDR: 10.0.0.0/16 |                   |  CIDR: 192.168.0.0/16 |
|                   |                     |                   |
| +---------------+ |                     | +---------------+ |
| | EC2 Instance  | | <-- Private Peering --> | EC2 Instance  | |
| +---------------+ |                     | +---------------+ |
|   Subnet: 10.0.1.0/24                  |   Subnet: 192.168.1.0/24
|   Route Table → VPC Peering Connection |   Route Table → VPC Peering Connection
+-------------------+                     +-------------------+
              ↑                                         ↑
              |------------> IAM Roles + Security Groups <------------|

🧰 AWS Services Used
Service	Purpose
Amazon VPC	Created two isolated virtual networks
VPC Peering	Enabled private communication between VPCs
EC2 Instances	Deployed test servers for validation
Route Tables	Configured custom routes for cross-VPC traffic
Security Groups	Controlled inbound/outbound traffic
IAM	Managed permissions for secure operations
🔧 Configuration Steps
1. Create Two VPCs

VPC A → CIDR: 10.0.0.0/16

VPC B → CIDR: 192.168.0.0/16
(Ensure CIDR ranges don’t overlap)

2. Launch EC2 Instances

One instance in each VPC for testing connectivity.

Attached respective subnets, route tables, and security groups.

3. Create VPC Peering Connection

From VPC A → request peering with VPC B.

From VPC B → accept the peering request.

4. Update Route Tables

Add routes in both VPCs:

In VPC A: Destination 192.168.0.0/16 → Target: Peering Connection ID

In VPC B: Destination 10.0.0.0/16 → Target: Peering Connection ID

5. Modify Security Groups

Allow inbound ICMP (ping) and SSH traffic only from the other VPC’s CIDR block.

6. Validate Connectivity

SSH into EC2 instance of VPC A → Ping private IP of EC2 in VPC B.

Confirm private communication established.

🧩 Key Learning Outcomes

✅ Understood AWS network isolation and VPC design
✅ Configured custom route tables for inter-VPC routing
✅ Applied IAM roles & least-privilege security principles
✅ Validated private communication without internet access
✅ Strengthened troubleshooting skills for AWS networking

🔒 Security Practices

Used non-overlapping CIDR blocks to avoid route conflicts

Restricted security groups to internal CIDR ranges only

Applied IAM least privilege for managing VPC peering permissions

Disabled public IPs and verified traffic stayed within AWS private backbone

🧪 Testing

Commands used:

# On EC2 in VPC A
ping 192.168.1.10    # Private IP of EC2 in VPC B

# On EC2 in VPC B
ping 10.0.1.10       # Private IP of EC2 in VPC A


Expected Result: Successful ping responses without public internet access.

📊 Challenges Faced
Challenge	Solution
Overlapping CIDR blocks	Recreated VPCs with non-overlapping ranges
No ping response initially	Updated route tables and SGs properly
IAM permission denied	Attached correct IAM role for VPC management
💬 Interview Talking Points

Q1. What is VPC Peering?
→ It’s a networking connection that allows traffic between two VPCs using private IPs without traversing the public internet.

Q2. What are the limitations of VPC Peering?
→ No transitive peering (A↔B↔C not allowed), overlapping CIDR not supported, and it’s region-specific unless using inter-region peering.

Q3. How do you ensure security in a VPC Peering setup?
→ Restrict routes, use least-privilege security groups, and limit access to internal CIDR ranges only.

🧾 Author

👤 Himanshu Sharma
🎓 B.Tech CSE | AWS & DevOps Enthusiast | Cloud Learner
📍 Jalandhar, Punjab, India
🌐 LinkedIn
 | GitHub

🏷️ License

This project is licensed under the MIT License – feel free to use and modify it for learning purposes.
