# AWS sertificates

[website link](http://oleksiiolchedai.s3-website-us-east-1.amazonaws.com)

# Tasks

### 7. Review Getting Started with Amazon EC2. Log Into Your AWS Account, Launch, Configure, Connect and Terminate Your Instance. Do not use Amazon Lightsail. It is recommended to use the t2 or t3.micro instance and the CentOS operating system.

https://aws.amazon.com/ - servise - search - ec2(regular VM RHEL) - launch instance
- Name and tags (e.g. My Web Server) - Choose an Amazon Machine Image (AMI) 'RHEL' -
- Instance type  't2.micro (Free tier)' - Key pair (ssh 4 PuTTy) 'Create new key pair' -
- Enter Key pair name - Key pair type 'RSA' Private key file format '.pem'- Create new key pair -
- Network settings 'Edit' - Auto-assign public IP 'Disable' -
- Configure storage 'Advanced' - Size (GiB) 'Free tier eligible customers can get up to 30 GB of EBS' -
- Delete on termination 'Yes' - Encrypted - KMS key 'aws/ebs' -
- Launch instance -
- EC2 Dashboard 'Elastic Ips' - Allocate Elastic IP address 'Allocate' -
- EC2 Dashboard 'Elastic Ips' - Choose created IP - Action 'Associate Elastic IP address' -
- Associate Elastic IP address - Instance 'Choose what u instance' - Private IP address 'Choose a Ip' -
- Associate -
- Instances - Congrats , instance have Public IPv4 DNS and address -
- EC2 - Instances - Choose instance - Security 'Inbound rules' -> 'Security groups' -> 'Edit inbound rules' ->
-> Add rule -> http port range 80 source 0.0.0.0/0 and https range 443 source 0.0.0.0/0 - save rules -
- Putty key gen - PuTTy - use public IP and key after PuTTyKeyGen -
- We are in our VM by 'ec2-user' - sudo su, yum update, upgrade, yum nano), yum -
- Install the Apache Web - sudo yum update httpd - sudo yum install httpd - 
- sudo systemctl start httpd - sudo systemctl status httpd - active (running) -
- ec2-34-232-246-133.compute-1.amazonaws.com - 34.232.246.133 -

### 8. Create a snapshot of your instance to keep as a backup.
### 10. Launch the second instance from backup.

- Elastic Block Store - Snapshots - Create snapshot - snapshot settings 'instance' -> 'volume ID' -> 'description' -
- Create snapshot - 
- Elastic Block Store - Snapshots - 'Select your snap' - Create image - Name - Delete on Termination - Create -
- Images - AMIs - 'Select your AMI' - Action - Launch - Instanse type - Next - Configure Security group -
- Select an existing security group - Next - Choose key pair - Launch instances -
- EC2 - now we see new instance from snapshot -
Delete snapshot
- Images - AMIs - 'Select your AMI' - Deregister - AMI is gone
- Elastic Block Store - Snapshots - Action - Delete - Snapshot is gone

### 9. Create and attach a Disk_D (EBS) to your instance to add more storage space. Create and save some file on Disk_D
### 11. Detach Disk_D from the 1st instance and attach disk_D to the new instance

- Elastic Block Store - Volumes - Create Volume - Volume Type 'pick what you need' - Size (GiB) - Create Volume -
- 'Select your Volume' - Actions - Attach Volume - Instance - Input instance id - Device '/dev/sdf' - Attach - 
- Go through ssh by PuTTy in linux CLI - lsblk - now we see new volume xvdf 2G - sudo fdisk -l -
- sudo mount /dev/xvdf /mnt - df -h 'Filesystem - /dev/xvdf' 'size - 2.0G ' 'Mounted on - /mnt' -
For Unmounted 
- 'umount -l /dev/xvdf' - 'df -h' - 'lsblk' - we see xvdf is unmounted -
Now go to the AWS - EBS - Volumes - wait when state turn to available - 
- Go through ssh by PuTTy in linux CLI - go to enother instance 
- 'lsblk' - 'df -h' - volume is not available - go to AWS - EBS - Volumes - 'select volume' - actions - Attach -
- choose second instanse - Attach -
- CLI linux - lsblk - now is xvdf is add - 'sudo file -s /dev/xvdf' - we see files inside -
- 'cd /mnt/' - 'sudo mkdir newfile' - 'cd newfile' - 'sudo mount /dev/xvdf /mnt/newfile/' -
- 'df -h' - 'Filesystem - /dev/xvdf' 'size - 2.0G ' 'Mounted on - /mnt/newfile' -
- 'cd /mnt/newfile/' - 'cd' - we see old files -

### 12. Review the 10-minute example. Explore the possibilities of creating your own domain and domain name for your site. Note, that Route 53 not free service. Alternatively you can free register the domain name *.PP.UA and use it.

- Route 53 if not a free so i have to find some instruction how to do this in internet -
https://medium.com/tribalscale/how-to-configure-aws-route-53-c8fa99ce66fb

### 13. Launch and configure a WordPress instance with Amazon Lightsail link 

- lightsail - Instances - Instance location 'Select zone' - Select a platform 'Linux' - Select a blueprint 'WordPress' -
- Change SSH key pair 'wordpresskey'- Choose your instance plan 'select first 3 month free!' -
- Key-value tags 'ServerName - WordPress' - Create instance -
- Connect by ssh - inside instance 'ls' we have few files - cat 'fileWhatUHaveInside - we can see default username and pass' -
- Now cory pass and go through - copy public ip and add /wp-login.php - use our login and pass - 
- For Delete resourses go to the lightsail, instances, click on our instace ... select delete, then yes -
- If we have DNS and static IP delete them too , make sure about all resources have been deleted -

### 14. Review the 10-minute Store and Retrieve a File. Repeat, creating your own repository.

- S3 - Buckets - Create Bucket - Bucket name must be globally unique and must not contain spaces or uppercase letters - AWS Region -
- Set permission settings for your S3 bucket. Leave the default values and select Next -
- You have many useful options for your S3 bucket including Versioning, Tags, Default Encryption, and Object Lock - Create bucket -
- Select Bucket and Upload files in Objects - Add files or Add folder -
- Review destination details and permissions. For this tutorial, leave the default values -
- Set property settings like storage class, server-side encryption, additional checksums, tags, and metadata with your object-
- Leave the default values and select Upload - Your object in your bucket’s home screen -
- Select the checkbox next to the file you would like to download, then select Download -
- Select the checkbox next to the file you want to delete and select Delete - 
- Review and enter permanently delete in the text input field to confirm deletion. Click Delete objects -
- Click on Amazon S3 > Buckets to view all your buckets in the region - Select the button then Delete -
- To confirm deletion, enter the name of the bucket in the text input field and choose Delete bucket -

### 15. Review the 10-minute example Batch upload files to the cloud to Amazon S3 using the AWS CLI. Create a user AWS IAM, configure CLI AWS and upload any files to S3.

- In the search bar and select IAM - click on Users - Add user - User name 'AWS_Admin' - Programmatic access -
- Next: Permissions - Attach existing policies directly option. Select AdministratorAccess then click Next: Tags -
- IAM tags are key-value pairs you can add to your user - Next: Review button - Create user -
- Click the Download Credentials and save the credentials.csv file in a safe location and then click the Close -
- Install and Configure the AWS CLI - installing the AWS CLI bundled installer - Open a terminal window -
- Type aws configure and enter. Following when prompted - Enter the Access Key Id from the credentials.csv file -
- Secret Access Key from the credentials.csv file -
- Using the AWS CLI with Amazon S3 - Create a new bucket named my_backup_bucket type: aws s3 mb s3://my_backup_bucket -
- To upload the file - aws s3 cp “C:\users\my_backup_bucket.bak” s3://my_backup_bucket/
- IAM user, configured your machine for use with the AWS command line interface - 
- And learned how to create, copy, retrieve, and delete files from the cloud -

### 16. Review the 10-minute example Deploy Docker Containers on Amazon Elastic Container Service (Amazon ECS). Repeat, create a cluster, and run the online demo application or better other application with custom settings.

- Set up your first run with Amazon ECS - Choose the Get started button - 
- Create container and task definition - In the Container definition field, select sample-app -
- Review the default values and choose Next - 
- Define your service - Service name - Service options come preloaded with default configuration values -
- Number of desired tasks: Leave the default value of 1 - Load balancing - Select the Application Load Balancer option -
- The default values for Load balancer listener port and Load balancer listener protocol are set up for the sample application -
- Next -
- Configure your cluster - In the Cluster name field, enter sample-cluster and choose Next - 
- Launch and view your resources - Choose Create - Launch Status - View service - 
- Open the sample application - On the sample-app-service page, select the Details tab and select the entry under Target Group Name -
- Target groups page, select the target group name - Details section, choose the Load balancer link - 
- Description tab, select the two page icon next to the load balancer DNS to copy the DNS name to your clipboard -
- Paste it into a new browser window, and press enter to view the sample -
- Clean up - Navigate back to the Amazon ECS console page and select the cluster name - Delete Cluster to delete the cluster -
- Enter delete me in the dialog box and choose Delete -

### 17. Run a Serverless "Hello, World!" with AWS Lambda.

- Search for Lambda and open the AWS Lambda Console - Choose Create function - reate a function to go to the Create function page -
- Select use a blueprint - Filter box enter hello-world-python and select the hello-world-python blueprint - Then choose Configure -
- Basic info - Name: name your Lambda function enter hello-world-python - Role: You will create an IAM role -
- Role name: type lambda_basic_execution - Lambda function code - Example code authored in Python - page and choose Create function -
- Runtime: Lambda function code in Java, Node.js, C#, Go, or Python we use Python 3.7 - Handler: You can specify a handler -
- Invoke Lambda function and verify results - Select Configure Test Event from the drop-down menu called Test -
- The editor pops up so you can enter an event to test your function - Create new event - name like HelloWorldEvent - 
- default setting of Private for Event sharing settings - Choose hello-world - change the values in the sample JSON - Choose Test -
- Upon successful execution, view the results in the console - Execution results tab verifies that the execution succeeded -
- Function Logs section will show the logs generated by the Lambda function execution as well as key information reported in the Log -
- Monitor your metrics - Invoke the Lambda function a few more times by repeatedly choosing the Test button -
- This will generate the metrics that can be viewed in the next step - Select the Monitor tab to view the results -
- View the metrics for your Lambda function, Lambda metrics are reported CloudWatch, leverage these metrics to set custom alarms -
- Delete the Lambda function - Select the Actions button and select Delete function - select Delete -

### 18. Create a static website on Amazon S3, publicly available (link1 or link2 - using a custom domain registered with Route 53).
Post on the page your own photo, the name of the educational program (EPAM Cloud&DevOps Fundamentals Autumn 2022), the list of
AWS services with which the student worked within the educational program or earlier and the full list with links of completed labs
(based on tutorials or qwiklabs).
Provide the link to the website in your report and СV.

http://oleksiiolchedai.s3-website-us-east-1.amazonaws.com/
