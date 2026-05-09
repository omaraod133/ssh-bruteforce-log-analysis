# ssh-bruteforce-log-analysis

## Objective
To analyze SSH authentication logs from a Hack The Box lab and understand how to identify brute-force attempts, session activity, and basic indicators of suspicious SSH behavior in Linux systems.

### Skills Learned
- Linux log analysis using authentication logs
- Recognizing patterns of automated attack attempts on SSH services
- Ability to generate and recognize attack signatures and patterns.
- Identifying brute-force login attempts and suspicious IP activity
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
- **Linux Command Line** – Used for navigating system logs and performing analysis within the terminal environment.
- **grep** utility – Used to filter and extract relevant log entries from authentication logs for investigation.
- **MITRE ATT&CK Framework** – Used to map observed behaviors in the lab to known adversary techniques

## Steps
This lab is about a brute-force attack against the SSH service. It provides several questions to answer.
The lab is from Hack The Box, and the name is Brutus.

<img width="1854" height="912" alt="{0B5B8106-97BB-49A7-8760-E6890354FF07}" src="https://github.com/user-attachments/assets/a55175db-f7cc-44ad-ac26-12d3a88d9c8b" />


The answers to the questions will be shown since I previously solved this lab.

So let’s begin by installing and unzipping the provided file. After unzipping it, we get three files:
- auth.log
- utmp

<img width="1920" height="947" alt="Screenshot_2026-05-06_18_16_58" src="https://github.com/user-attachments/assets/f44333b0-42d5-48ee-a04f-f566fd686e13" />

As we can see, there are many log entries. Let’s focus specifically on failed login attempts.

<img width="1920" height="947" alt="Screenshot_2026-05-06_18_19_42" src="https://github.com/user-attachments/assets/fc7d5652-0d5b-4439-adc4-f159533ea688" />

as we see there is a lot of logs, let is be spicsfic and see all the Failed login

<img width="1920" height="947" alt="Screenshot_2026-05-06_18_23_13" src="https://github.com/user-attachments/assets/1211564b-7a8c-4ddb-b844-4a4425d9afaa" />

Here we start to see evidence of a brute-force attack.
From this, we can observe that the attacker started the brute-force attack at 06:31:33 and ended at 06:31:42, lasting about 9 seconds.
We also identify valid usernames such as backup and root (we know that from the massage "Failed password for root" )

The attack originated from the IP address 65.2.161.68.

Let’s gather more information about this IP address.

<img width="1920" height="947" alt="Screenshot_2026-05-09_17_33_18" src="https://github.com/user-attachments/assets/a01f9b1a-315c-490f-82ec-c0ae4f2d0a01" />
Interesting — this IP appears to be located in India.

Now let’s check if there were any successful logins from this IP.
<img width="1920" height="947" alt="Screenshot_2026-05-09_17_08_11" src="https://github.com/user-attachments/assets/6f7ff2b7-ba7f-4866-88ed-1e5842537280" />

Here we can see four successful login attempts: three using the root account and one using a user named cyberjunkie.

Three of these logins came from the attacker IP 65.2.161.68, while one login came from a different IP and at a different time rang of attack time

The cyberjunkie user looks suspicious. It is likely that the attacker logged in as root and then created this account.

Let’s investigate further.
<img width="1920" height="947" alt="Screenshot_2026-05-09_17_19_28att" src="https://github.com/user-attachments/assets/edb1b4f5-9a47-408a-b73f-97b88fd0aef4" />

As seen here, the attacker created the cyberjunkie account and granted it sudo privileges. The attacker then used sudo access to read the /etc/shadow file.

After that, the attacker downloaded a script called linper.sh.
What is this tool?

<img width="1867" height="962" alt="{038389A4-52C4-47E5-8E50-8B66C7F79241}" src="https://github.com/user-attachments/assets/72840fe2-cb8b-4576-a0b4-c55a451acb93" />

This tool can:
Provide a reverse shell (allowing remote control of the machine)
Maintain persistence after reboot (allowing the attacker to keep access even after restart)


let is write report:

Summary:
A brute-force attack targeting SSH device IP 172.31.35.28. The attacker successfully got the root password and created an account called cyberjunkie, and he escalated privilege for that account and got sudo. Then he downloaded a tool called linper.sh, which can take control of the machine.

Incident Timeline
- Start time: 06:31:33
- End time: 06:31:42
- Duration: ~9 seconds

Affected Asset
- IP Address: 172.31.35.28
