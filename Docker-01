# Launch EC2 + Install Docker

A quick guide to spin up an AWS EC2 instance (Amazon Linux 2023) and install Docker on it manually — no Docker Desktop required.

## Prerequisites

- AWS account
- IAM user with EC2 access
- SSH key pair
- Basic terminal knowledge

## 1. Launch EC2 Instance

| Setting | Value |
|---|---|
| AMI | Amazon Linux 2023 |
| Instance Type | t3.large (or t2.micro for testing) |
| Storage | 30 GB |
| Key Pair | Select or create one |
| Security Group | Allow SSH (port 22) |
| Region | Any (e.g., us-east-1) |

## 2. Connect via SSH

```bash
ssh -i your-key.pem ec2-user@<your-ec2-public-ip>
```

## 3. Install Docker

```bash
sudo dnf update -y
sudo dnf install docker -y
sudo systemctl enable --now docker
sudo usermod -aG docker ec2-user
```

> Log out and reconnect for group permissions to apply.

## 4. Test Docker

```bash
docker version
docker run hello-world
docker images
```

If you see `Hello from Docker!`, the installation was successful.

## 5. Cleanup

Remove the test container and image:

```bash
docker rm $(docker ps -aq)
docker rmi hello-world
```

Stop or terminate the EC2 instance when done to avoid AWS charges.
