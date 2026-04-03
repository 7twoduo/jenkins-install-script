# 🚀 Jenkins Setup — Local Docker + AWS EC2

<p align="center">
  <img src="https://img.shields.io/badge/Jenkins-Automated-red?style=for-the-badge&logo=jenkins&logoColor=white" />
  <img src="https://img.shields.io/badge/Docker-Containerized-blue?style=for-the-badge&logo=docker&logoColor=white" />
  <img src="https://img.shields.io/badge/AWS-EC2-orange?style=for-the-badge&logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/Terraform-Included-844FBA?style=for-the-badge&logo=terraform&logoColor=white" />
</p>

<p align="center">
  <b>Custom Jenkins controller for local use or cloud deployment.</b><br>
  Built with Docker, preloaded plugins, and automatic admin bootstrap.
</p>

---

## ✨ What this script does

> [!NOTE]
> This setup creates a custom Jenkins Docker image and starts Jenkins with a persistent volume.

✅ Builds a custom Jenkins image  
✅ Installs Jenkins plugins from `plugins.txt`  
✅ Creates the admin user automatically  
✅ Disables the setup wizard  
✅ Starts Jenkins in Docker  
✅ Persists Jenkins data with a Docker volume  

---

## 🧭 Choose your path

```markdown
flowchart LR
    A[Start] --> B{Where do you want Jenkins?}
    B --> C[Local Machine]
    B --> D[AWS EC2]
    C --> E[Run local script]
    D --> F[Run EC2 script]
    E --> G[Open localhost:8080]
    F --> H[Open EC2-Public-IP:8080]
```

## 💻 Local Docker Setup

[!TIP]

```markdown
Use this option if you want Jenkins running on your own laptop or desktop.

What happens

Builds the Jenkins image

Creates the Docker volume

Starts the container

Exposes Jenkins on port 8080

Run it

chmod +x local-jenkins.sh

./local-jenkins.sh

Open Jenkins

http://localhost:8080

Logs

docker logs -f jenkins-admin

```

## ☁️ AWS EC2 Setup

[!TIP]
```markdown
Use this option if you want Jenkins running in the cloud on an EC2 instance.

What happens

Updates the EC2 server

Installs Docker

Starts and enables Docker

Adds ec2-user to the Docker group

Builds the same Jenkins image

Starts the same Jenkins container

Run it

chmod +x ec2-jenkins.sh

./ec2-jenkins.sh

Open Jenkins

http://<EC2-PUBLIC-IP>:8080

Security group ports


8080 → Jenkins UI

50000 → Jenkins agents

Logs

docker logs -f jenkins-admin

```
## 🔐 Optional admin credentials
```markdown
export JENKINS_ADMIN_ID=admin
export JENKINS_ADMIN_PASSWORD='YourStrongPasswordHere'

Run the script after setting them.
```

## 🗂️ Files created by the script
```markdown
jenkins-admin/
├── Dockerfile
├── plugins.txt
└── init.groovy.d/
    └── 01-create-admin.groovy
```
## ⚡ Quick visual

```markdown
flowchart LR
    A[Run Script] --> B[Build Image] --> C[Install Plugins + Tools] --> D[Create Admin] --> E[Start Container] --> F[Port 8080]
```
---

## 🌌 Access Matrix

<table align="center">
  <tr>
    <th>Environment</th>
    <th>Run From</th>
    <th>Access URL</th>
  </tr>
  <tr>
    <td>🖥️ <b>Local Docker</b></td>
    <td>Your machine</td>
    <td><code>http://localhost:8080</code></td>
  </tr>
  <tr>
    <td>☁️ <b>AWS EC2</b></td>
    <td>EC2 instance</td>
    <td><code>http://&lt;EC2-PUBLIC-IP&gt;:8080</code></td>
  </tr>
</table>

---





# 🌍 Cloudflare Hosting
```markdown
Use Cloudflare when you want to expose Jenkins without relying only on localhost or raw EC2 public access.
```
## 🖥️ Local Cloudflare Hosting
```markdown
Temporary public URL from your local machine.

Install cloudflared

winget install --id Cloudflare.cloudflared

Run Cloudflare tunnel

cloudflared tunnel --url http://localhost:8080

In case that doesn't work use this other one and set it to your drive.

"/c/Program Files (x86)/cloudflared/cloudflared.exe" tunnel --url http://localhost:8080

```
## ☁️ EC2 Cloudflare Hosting
```markdown
Temporary public URL from your EC2 instance.

Install cloudflared

curl -fsSL https://pkg.cloudflare.com/cloudflared.repo | sudo tee /etc/yum.repos.d/cloudflared.repo

sudo yum update -y

sudo yum install -y cloudflared

cloudflared --version

Run Cloudflare tunnel

cloudflared tunnel --url http://localhost:8080

```
## 🚀 Permanent Hosting

Use this when you want a stable Cloudflare tunnel with your own domain.

1. Login
cloudflared tunnel login
2. Create tunnel
cloudflared tunnel create my-tunnel
3. Route DNS
cloudflared tunnel route dns my-tunnel yourdomain.com
4. Create config file
nano ~/.cloudflared/config.yml
tunnel: my-tunnel
credentials-file: /root/.cloudflared/<tunnel-id>.json

ingress:
  - hostname: yourdomain.com
    service: http://localhost:8080
  - service: http_status:404
5. Run tunnel
cloudflared tunnel run my-tunnel

## 🧠 Quick Notes
```markdown

Local Docker is best for testing Jenkins on your machine.

AWS EC2 is best for running Jenkins in the cloud.

Cloudflare Quick Tunnel gives you a fast temporary public URL.

Permanent Hosting gives you a custom domain and a persistent tunnel.

Jenkins still runs on:

http://localhost:8080

```
#                      🚀🚀🚀🚀🚀 Cloudflare just exposes that service securely. 🚀🚀🚀🚀🚀



# Beware, don't close the console with the cloudflare tunnel, it shuts down the tunnel. 

# TODOS: Ask AI if you have any questions, it will give you a 90%+ accurate answer, most likely 














## 👨‍💻 About the Author

<p align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Inter&weight=600&size=22&pause=1000&color=58A6FF&center=true&vCenter=true&width=760&lines=Cloud+Engineer+focused+on+AWS%2C+Terraform%2C+and+automation;Building+production-inspired+infrastructure+projects;Turning+cloud+concepts+into+real-world+implementations" alt="Typing SVG" />
</p>

<p align="center">
  I build hands-on cloud projects designed to reflect practical engineering work rather than simple demos.
  My focus is on <b>AWS infrastructure</b>, <b>Infrastructure as Code</b>, <b>automation</b>, <b>security-minded design</b>,
  and <b>real implementation patterns</b> that translate into production environments.
</p>

<p align="center">
  Through projects like this, I aim to demonstrate the ability to design, provision, and integrate modern cloud services
  in ways that are scalable, structured, and operationally relevant.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/AWS-Architecting-232F3E?style=for-the-badge&logo=amazonaws&logoColor=white" />
  <img src="https://img.shields.io/badge/Terraform-Infrastructure-7B42BC?style=for-the-badge&logo=terraform&logoColor=white" />
  <img src="https://img.shields.io/badge/Cloud-Engineering-1F6FEB?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Automation-Building-success?style=for-the-badge" />
</p>

<p align="center">
  <a href="https://www.linkedin.com/in/gavin-fogwe/">
    <img src="https://img.shields.io/badge/LinkedIn-Let's%20Connect-blue?style=for-the-badge&logo=linkedin" />
  </a>
  <a href="https://github.com/gavinxenon0-arch">
    <img src="https://img.shields.io/badge/GitHub-See%20More%20Projects-black?style=for-the-badge&logo=github" />
  </a>
  <a href="https://gavinfogwe.win/">
    <img src="https://img.shields.io/badge/Portfolio-Explore-orange?style=for-the-badge&logo=googlechrome&logoColor=white" />
  </a>
</p>



