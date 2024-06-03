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

1. Log into your AWS Console, then proceed to navigate to the EC2 Console. Once there, in the Instances section, select 'Instances,' and subsequently click on 'Launch Instance

![EC2-creation](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/23e61820-9926-4e6e-97ea-113e691a1933)

2. Next, navigate to the 'Elastic Block Store' section and select "Volumes". You will notice that a default volume has already been created for you. 
 ![volume](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/a68d91f2-b810-4d44-b478-3edc06d9a841)
 
3. Then, click on 'Snapshots' and proceed to click on the "Create Snapshot" button. This action will prompt you with a page resembling the one shown. Lastly, in the Volume ID section, select the default Volume ID that was created when the instance was created.
 ![Snapshot](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/35a82796-5ae5-4c01-a2a0-264e19116059)
   
5. After clicking "Next", you should provide a name for your snapshot. Then, scroll down and click "Create Snapshot". Navigate to the Snapshot option in the EC2 Dashboard and verify whether the snapshot was successfully created or not.

![snapshot created](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/c278494c-fdec-405b-b56f-7a401b30ccb0)

## Step2:
### Steps:
1. After creating a snapshot, navigate to the Lambda Console. In the user interface, you will see options such as 'Create Function'. Click on 'Functions'. Select 'Author from Scratch,' then enter the Function name, and choose the latest Python version. Scroll down and click 'Create Function'.

![lambda function created](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/23a32fc4-3792-438f-bc79-d5e0b23f2bbe)


3.  After creating the function, scroll down, and you will see something similar to the image below. Click on the 'Code' section. Next, clear the existing code and replace it with the "ebs_stale_snapshots.py".

4.  ![code](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/0deca2e9-4157-41bd-a5da-0d9c47465b04)
5.  Click 'Deploy' to save your changes, and then click 'Test'. This action will prompt a page that resembles the one shown below. 
   
!

Please configure the settings as displayed above and then scroll down. Next, click on 'Create Event'.Once you've created the event, proceed to the IAM Console(Identity and Access Management) and then navigate policies section to create a new policy.
![configuration](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/b79fb401-9ed6-4ea3-93c8-6ada5ff09e1c)

Select the service as 'EC2'
In the 'Actions' section, grant permissions for the following actions: DescribeInstances, DescribeVolumes, DescribeSnapshots, DeleteSnapshots.

After Creating the Policies , Navigate to the Lambda Sections.
![Creating policies](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/1af09ff7-29ff-412d-9b6b-a455db6fa024)

Next, navigate to the page of the Lambda function you've created. In the "Permissions" section, click on the role name. Click on 'Add Permissions' and then select 'Attach Policy'. Choose the correct policy you created. Then, scroll down and click 'Add Permissions
![adding role permission](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/dbc5b2b3-3ea6-45be-90d6-c6b5a7159e08)

After that, you can go to the Lambda function page and run the code; it will display some outputs as shown below.
![Final output](https://github.com/JDNSaiCharanKatta/aws_cost_optimization/assets/170161500/cac5ff80-6d72-4fa9-8c80-ba5f68d3efdd)









   







