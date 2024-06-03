## Efficient AWS Cost Management through Stale Resource Detection

## Problem: 

<p> In cloud environments like AWS, developers often provision resources such as EC2 instances and associated storage volumes for various tasks. However, over time, these resources can become obsolete or unused, leading to unnecessary costs. One common scenario is when developers create EC2 instances with attached storage volumes and generate snapshots for backup purposes. When these instances are terminated, the associated snapshots are sometimes forgotten, leading to continued costs for unused resources.
</p>

## Solution:
<p>To tackle the challenge of inefficient AWS cost management due to stale resources, we've developed a proactive solution leveraging AWS services. Our approach involves implementing a Smart Lambda function that continuously monitors snapshots and EC2 instances. This Lambda function employs AWS SDKs to analyze the relationships between snapshots and active EC2 instances. If it identifies snapshots that are no longer associated with any active instances, it automatically triggers deletion actions, effectively eliminating unnecessary costs. By implementing this solution, we ensure that our AWS infrastructure remains lean, optimized, and cost-efficient, contributing to significant savings over time.</p>

## Note
<p> In the world of managing cloud infrastructure, even small mistakes can lead to unnecessary expenses. Picture a scenario where an Elastic IP is connected to an EC2 instance but forgotten after termination. In such instances, the inactive Elastic IP quietly accumulates costs, underscoring the vital importance of meticulous resource management to reduce expenses.</p>

## Steps:
### Step1:

1. Log into your AWS Console.<br>
2. Navigate to the EC2 Console.<br>
3. In the Instances section, select 'Instances,' and then click on 'Launch Instance'.<br>

![EC2-creation](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/23e61820-9926-4e6e-97ea-113e691a1933)

4. Next, navigate to the 'Elastic Block Store' section and select "Volumes"

   
6. You Will notice that a default volume has already been created for us.
7. Next, click on 'Snapshots' and then click on "Create Snapshot" button. It will Prompt you with a page that looks like this.
8. In Volume ID section choose your default Volume ID created when we create instance.
9. Nexxt, click 'next' provide a name for your snapshot, and then scroll down and click "Create Snapshot".

