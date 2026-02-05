# Follow these installation steps on the AMI EC2 instance:


## Add the following EC2 instance userdata to the Launch Template:
```
#!/bin/bash
dnf update -y
dnf install -y httpd wget git php php-fpm php-mysqli php-json php-devel mariadb105
systemctl enable httpd
systemctl start httpd
cd /var/www/html
git clone https://github.com/akashsawan1/three-tier-architecture-aws.git
mkdir -p api
mv three-tier-architecture-aws/backend/api/* api/
rm -rf three-tier-architecture-aws
sed -i 's/update-me-host/database-1.cpk2gqigedbg.us-east-2.rds.amazonaws.com/g' api/db_connection.php
sed -i 's/update-me-username/admin/g' api/db_connection.php
sed -i 's/update-me-password/akash1234/g' api/db_connection.php
chown -R apache:apache /var/www/html
chmod -R 755 /var/www/html
systemctl restart httpd
```

### What you need to change in the sed commands above :
* **Endpoint:** `database-1.cpk2gqigedbg.us-east-2.rds.amazonaws.com` $\rightarrow$ `database_endpoint`
* **Username:** `admin` $\rightarrow$ `database_username`
* **Password:** `akash1234` $\rightarrow$ `database_password`

### Also, in the backend target group health check, please specify the 403 status code.