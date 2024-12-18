# Lamp-ENV
create a EC2 t2.micro instance, configure LAMP environment and deploy the sample PHP Code.

Step 1: Launch a t2.micro EC2 Instance
Go to the EC2 Dashboard in AWS Management Console.
Click Launch Instances.
Choose Amazon Linux 2 or Ubuntu Server 20.04 LTS as the AMI.
Select t2.micro (eligible for Free Tier) as the instance type.
Configure instance details:
Default settings are fine for this demo.
Add storage (default 8 GiB is sufficient).
Add tags (optional).
Configure security group:
Allow SSH (port 22).
Allow HTTP (port 80) for web access.
Allow HTTPS (port 443) (optional).
Launch the instance and download the SSH key pair.

Step 2: Connect to Your Instance
Open a terminal or SSH client.
Connect using the SSH key:
ssh -i "your-key.pem" ec2-user@your-ec2-public-ip

Step 3: 
Install LAMP Stack
Update your system:
sudo yum update -y

Install Apache:
sudo yum install httpd -y
sudo systemctl start httpd
sudo systemctl enable httpd

Install PHP:
sudo amazon-linux-extras enable php8.0
sudo yum install php php-mysqlnd -y

Install MySQL (optional):
sudo yum install mariadb-server -y
sudo systemctl start mariadb
sudo systemctl enable mariadb

Step 4: 
Deploy Sample PHP Code

Create a sample PHP file:
echo "<?php phpinfo(); ?>" | sudo tee /var/www/html/index.php

Adjust file permissions:
sudo chown -R apache:apache /var/www/html
sudo chmod -R 755 /var/www/html

Restart Apache:
sudo systemctl restart httpd

Step 5: 
Access Your Application
Visit http://your-ec2-public-ip in your web browser.
You should see the PHP info page.
