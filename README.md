# JIRA_software-deployment-in-containers-using-Ansible-and-Docker
![e194738a-a1d4-4932-b5b2-7049dde1007c](https://github.com/user-attachments/assets/fa08b432-3def-4197-bfab-ee6f33b7cf23)

1. Launching 3 Amazon Linux 2 instances and naming them **“Ansible_Control”**, **“Worker_Node_1”** and **“Worker_Node_2”**. (The security group of Ansible_Control is configured to allow just SSH requests from a desired IP (e.g., my IP) address. The security group of the Worker_Node_1 and Worker_Node_2 is configured to allow SSH traffic from the Ansible_Control and SSH traffic from a desired IP (e.g., my IP).

## Ansible security group inbound rule
![image-20240717-192750 (1)](https://github.com/user-attachments/assets/6e465feb-a63b-41e8-9c98-4f2ed36a1574)

## Security Group inbound rules of Worker Nodes
![image-20240717-193102](https://github.com/user-attachments/assets/4c815241-91c1-417d-a7ca-0cd4dccec07a)

## Created Instances
![image-20240717-193325](https://github.com/user-attachments/assets/09a90b0e-fb51-4946-8c68-e320b45e2242)

2. Login to 3 three instances using Git Bash

![image-20240717-193457](https://github.com/user-attachments/assets/e2ae4bec-945f-444d-8148-90f63829042e)

To determine which Git Bash belongs to which node, rename the servers.
- In each server, Switch as a root user
  ```sh
  sudo su –

- Get into the **“hostname”** file in the /etc/ directory then edit the hostname of each server
  ```sh
  nano /etc/hostname

![image-20240717-194643](https://github.com/user-attachments/assets/d5aa3bfc-3691-4cae-a19d-f8d4814ea04a)

- Save the changes and reboot the servers
  ```sh
  reboot

- Log into the instances again and you will realize that you can identify which Git bash belongs to which server

![image-20240717-194927](https://github.com/user-attachments/assets/695fe011-e358-4735-aa18-783b1ffc1244)

3. For all 3 servers create a common user called “ansible”, set a common password, and allow for “Password authentication”  using the following commands for all 3 servers.
  ```sh
  sudo su - # Login as Root User
  useradd ansible
  passwd ansible # pass a password
  sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config # change password authentication permission to "yes"

- Navigate to the /etc/ssh/sshd_config path, and uncomment **"PermitRootLogin"** in the sshd_config file.
  ```sh
  nano /etc/ssh/sshd_config

- Restart the sshd service.
  ```sh
  sudo systemctl restart sshd

4. Add ansible to the “sudoers” group in each server.
- Navigate to the sudoers group file via the following command.
  ```sh
  nano /etc/sudoers

- Add “ansible” user in each of the following points in the file.


