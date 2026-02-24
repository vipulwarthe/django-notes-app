# Simple Notes App
This is a simple notes app built with React and Django.

Declarative CI/CD Pipeline in Jenkins demo link

    https://medium.com/@m.qasimnauman/declarative-ci-cd-pipeline-in-jenkins-5e636a4976dc 

## Requirements
1. Python 3.9
2. Node.js
3. React

## Installation
1. Clone the repository
```
git clone https://github.com/LondheShubham153/django-notes-app.git
```

2. Build the app
```
docker build -t notes-app .
```

3. Run the app
```
docker run -d -p 8000:8000 notes-app:latest
```

## Nginx

Install Nginx reverse proxy to make this application available

    sudo apt-get update
    sudo apt install nginx -y`
    sudo systemctl start nginx
    sudo systemctl enable nginx
    sudo systemctl status nginx

Allow Firewall (If UFW Enabled)

sudo ufw status

    sudo ufw allow 'Nginx Full'

Test in Browser

    http://YOUR_SERVER_IP

Nginx Main Config Location

    /etc/nginx/nginx.conf

Site configs:

    /etc/nginx/sites-available/
    /etc/nginx/sites-enabled/

Use Nginx as Reverse Proxy for Jenkins:

    sudo nano /etc/nginx/sites-available/jenkins

    server {
        listen 80;
        server_name your_domain_or_ip;

        location / {
            proxy_pass http://localhost:8080;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }

Enable site:

    sudo ln -s /etc/nginx/sites-available/jenkins /etc/nginx/sites-enabled/

Test config:

    sudo nginx -t

Restart:

    sudo systemctl restart nginx

Now access:

    http://your_domain_or_ip



