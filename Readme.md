# SSH and SFTP Connection Guide

Guide for connecting to remote systems using SSH and transferring files using SFTP.

## Terminology

- **Local Machine**: Your personal computer that you're working from
- **Remote Machine**: The server or computer you're connecting to via SSH/SFTP

## SSH Connection

Connect to a remote system using SSH:  
(example command use original command given by your vps provider)
```bash
ssh -p 12345 root@12.123.123.12 -L 8080:localhost:8080  # Command given by your vps provider to connect to remote pc
```
**Structure**  
- ***ssh*** - This is the command to start a Secure Shell (SSH) connection
- **-p 12345** - This tells SSH to connect to port 12345 on the remote server
- **root@12.123.123.12** - This specifies the username and IP address of the remote server:
  - root — the user you're logging in as
  - 12.123.123.12 — the remote server's IP address
- It creates a tunnel from your local machine's port 8080 to the remote machine's port 8080, via SSH.
  - First (8080) - The Local port on your computer
  - Second (8080) - The Port on remote server you want to connect to

## File Transfer with SFTP (How to construct SFTP command from SSH command given to you by VPS provider)

To transfer files between your local and remote machines, open a new terminal in local machine and use SFTP:  

Copy your ssh command and:
- Remove everything after IP address
- Change ssh to sftp
- Change small p to capital P 

```bash
sftp -P 12345 root@12.123.123.12  #Constructed from example command above
```

## Get Current Folder
After connecting to sftp you need to have two paths(file locations):

- Where you have swarm.pem saved on remote machine 
- Where you need to save swarm.pem on local machine

Navigate to folders whose paths you need, paste this command and copy paths printed in terminal:

```bash
pwd
```
## Navigation Commands in SFTP (After Connecting to SFTP)  

How it looks after connecting to SFTP:  

![Image](https://github.com/user-attachments/assets/bcd99798-24d6-489b-8d42-aba23412464b)

Now continue with commands below:

```bash
cd "path on remote machine" # Example : /root/rl-swarm
lcd "path on local machine" # Example: /mnt/e/key
```

## File Transfer Commands

Once connected with SFTP:

```bash
get swarm.pem      # Download swarm.pem from remote to local machine 
put swarm.pem      # Upload swarm.pem from local to remote machine 
```

## Example Workflow

1. Connect to remote machine:
   ```bash
   ssh -p 12345 root@12.345.678.79 -L 8080:localhost:8080
   ```

2. In new terminal on local machine, start SFTP session:
   ```bash
   sftp -P 12345 root@12.345.678.79
   ```

3. Navigate and transfer files:
   ```bash
   # Navigate to desired directories
   cd root/rl-swarm    # On remote where you have swarm.pem
   lcd /mnt/e/key       # On local where you want to save swarm.pem
   
   # Transfer files
   get swarm.pem     # Download from remote to local
   put swarm.pem      # Upload to remote from local
   ```

4. Exit SFTP session:
   ```bash
   exit
   ```

## Additional Tips
  
- For transferring large directories, consider zipping folder and transfer zipped files over sftp:

  ```bash
  zip -r output.zip Folder
  ```
  - Output.zip - Zipped output file
  - Folder - Folder to zipped

## Image for Reference
Getting paths:


Remote machine:    
![Image](https://github.com/user-attachments/assets/3ac2df54-7633-48ce-baf4-d6ad036fcd88)


Local machine:  
![Image](https://github.com/user-attachments/assets/17beb1bd-46d1-45c8-8e23-1e8e9d25db57)


Sample Image:
![Image](https://github.com/user-attachments/assets/fb43276b-8bc2-4f52-b67e-22ce3d58788c)
