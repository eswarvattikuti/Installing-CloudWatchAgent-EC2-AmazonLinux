# Installing-CloudWatchAgent-EC2-AmazonLinux
#Installing CloudWatch agent on AmazonLinux EC2 Instances using SSM

Steps:
#Creating IAM role and launching EC2 instance
1. Create an IAM role (eg. name, cloudWatchWithSSM) with permissions policies AmazonSSMManagedInstanceCore, CloudWatchAgentServerPolicy & CloudWatchAgentAdminPolicy.
2. Launch an EC2 Amazon Linux instance by assigning the above created role "cloudWatchWithSSM".

#Downloading CloudWatch agent package
3. Open SSM on AWS management console >> Run command. Click on "Run a command".
4. Select the document "AWS-ConfigureAWSPackage".
5. Under command parameters, select action as "Install", name as you wish & version as latest.
6. Select the target.
7. Click on "Run".

#Creating CloudWatch agent configuration file with wizard
8. Connect to AWS EC2 instance and issue the following command, #sudo /opt/aws/amazon-cloudwatch-agent/bin/amazon-cloudwatch-agent-config-wizard
9. Make your necessary selections. For "Do you want to store the config in the SSM parameter store?", please select "yes" as this will automatically create a parameter for us in parameter store.

#Installing collectd (Optional. Only required if you've selected yes for "Do you want to monitor metrics from CollectD?")
10. Run this command on your EC2 instance: #sudo amazon-linux-extras install collectd

#Installing CloudWatch agent
11. Open SSM on AWS management console >> Run command. Click on "Run a command".
12. Select the document "AmazonCloudWatch-ManageAgent".
13. Under command parameters, select action as "Configure", Optional Configuration Source as "SSM", Optional Configuration Location as "SSM parameter name" & Optional Restart as "Yes".
14. Select the target.
15. Click on "Run".
