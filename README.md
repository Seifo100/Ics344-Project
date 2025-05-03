# Phase 3: Defensive Strategy Proposal

## Defensive Mechanism:
in this phase we apply and implement the fail2ban defensive mechanism against ssh brute-force attack for the metasploitable3 machine.

### setting up fail2ban on metasploitable3:

![Screenshot 2025-05-03 184221](https://github.com/user-attachments/assets/e1bf4fa4-969b-4f53-aeae-3674ed5aee90)
![Screenshot 2025-05-03 185635](https://github.com/user-attachments/assets/8cb37e76-1898-4fcf-a32a-9b795868f4c1)
![Screenshot 2025-05-03 185812](https://github.com/user-attachments/assets/68bc2005-d3c3-4020-af1d-887c6f15f73d)

## The attack before and after implementing the defensive mechanism:


Now we compare the attack before and after the implementation.
### Before Implementation:
![Screenshot 2025-05-03 182204](https://github.com/user-attachments/assets/2d227048-a096-43e9-bd4c-d4b12c263e06)

### After Implementation:
![Screenshot 2025-05-03 190656](https://github.com/user-attachments/assets/f5a897d4-d1f4-458c-93c7-b57b5e2b052a)
![Screenshot 2025-05-03 190727](https://github.com/user-attachments/assets/58e6cd84-42d1-4149-ace1-869f07fe07d4)
![Screenshot 2025-05-03 190746](https://github.com/user-attachments/assets/e8d96140-75ef-47a0-abcf-c02e65f22dcb)

We can see that the ip of the attacker is banned and in the search it does not allow the attacker to connect,which means our defence mechanism worked correctly.

## Before-and-After Security Status.

| **Metric**             | **Before Defense** | **After Defense**   |
| ---------------------- | ------------------ | ------------------- |
| Failed login attempts  | 138                | 3                   |
| Successful logins      | 3                  | 0                   |
| Access to port 22      | Allowed            | Blocked (IP banned) |
| SSH Brute-force result | Successful         | Blocked by Fail2Ban |
