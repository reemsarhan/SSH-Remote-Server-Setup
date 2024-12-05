# SSH-Remote-Server-Setup


## Project URL  
[project URL](https://roadmap.sh/projects/ssh-remote-server-setup) 


# Remote Linux Server Setup with SSH Configuration

## Project Overview
The goal of this project is to set up a remote Linux server and configure it to allow SSH connections. The steps below guide you through creating an EC2 instance in AWS, configuring SSH access, and connecting to the server using an SSH key. This project fulfills the basic requirement of SSH setup and provides a foundation for future server configuration tasks.

---

## Requirements
1. Set up a remote Linux server using AWS EC2 or any other provider.
2. Configure the server to allow SSH connections using two new SSH key pairs.
3. Ensure you can connect to the server using both SSH keys.
4. Create an SSH alias in `~/.ssh/config` for simplified connections.
5. Stretch Goal: Install and configure `fail2ban` to prevent brute force attacks.

---

## Steps to Complete the Task

### 1. Launch an EC2 Instance
- Navigate to the AWS Management Console.
- Launch a new Amazon Linux EC2 instance.
- During instance creation, download the SSH private key (`EC2SSHKEY.pem`).

---

### 2. Configure Your SSH Key
After downloading your private key, follow these steps to set up permissions and prepare the key for use:

#### Commands to Secure the Key
```bash
chmod 700 /mnt/d/aws
chmod 600 /mnt/d/aws/EC2SSHKEY.pem
sudo chown $USER:$USER /mnt/d/aws/EC2SSHKEY.pem
mv /mnt/d/aws/EC2SSHKEY.pem ~/.ssh/
```


#### 3.  Connect to Your EC2 Instance
Use the following command to connect to the server:
```
ssh -i ~/.ssh/EC2SSHKEY.pem ec2-user@16.171.5.4
```
If everything is set up correctly, you will see a success message similar to the following:
```
   ,     #_
   ~\_  ####_        Amazon Linux 2023
  ~~  \_#####\
  ~~     \###|
  ~~       \#/ ___   https://aws.amazon.com/linux/amazon-linux-2023
   ~~       V~' '->
    ~~~         /
      ~~._.   _/
         _/ _/
       _/m/'
[ec2-user@ip-172-31-47-210 ~]$
```


### 4. Create a Second SSH Key
To meet the requirement of connecting with two SSH keys, create another key pair and add it to your server.

Generate a New SSH Key Pair
Run the following commands to generate a new SSH key:

```
ssh-keygen -t rsa -b 2048 -f ~/.ssh/SecondSSHKey
```

This creates a new key pair:

Private key: ~/.ssh/SecondSSHKey
Public key: ~/.ssh/SecondSSHKey.pub

### 5. Add the Public Key to the EC2 Instance
Connect to your instance using the first SSH key.
Append the contents of ~/.ssh/SecondSSHKey.pub to the ~/.ssh/authorized_keys file on the server:
```
cat ~/.ssh/SecondSSHKey.pub >> ~/.ssh/authorized_keys
```

### 6. Test the Second Key
To test the second key, use the following command:
```
ssh -i ~/.ssh/SecondSSHKey ec2-user@16.171.5.4
```

 
