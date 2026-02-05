# Follow these installation steps on the AMI EC2 instance:


## Add the following EC2 instance userdata to the Launch Template:

```
#!/bin/bash
dnf update -y
dnf install -y nginx git
cd /tmp
git clone https://github.com/akashsawan1/three-tier-architecture-aws.git
rm -rf /usr/share/nginx/html/*
cp -r /tmp/three-tier-architecture-aws/frontend/* /usr/share/nginx/html/
cp /tmp/three-tier-architecture-aws/infrastructure/nginx_config_ksh /etc/nginx/nginx.conf
sed -i 's/update-me/alb-dns/g' /etc/nginx/nginx.conf
systemctl enable nginx
systemctl restart nginx
rm -rf /tmp/three-tier-architecture-aws
```

### What you need to change in the sed commands above :

* **ALB Endpoint:** `alb-dns` $\rightarrow$ `alb_endpoint`