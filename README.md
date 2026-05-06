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
this lab is taking about invastion brut force attack in ssh service and they give us some qoutions to answer
the lab is in HackTheBox the lab name is Brutus

<img width="1854" height="912" alt="{0B5B8106-97BB-49A7-8760-E6890354FF07}" src="https://github.com/user-attachments/assets/a55175db-f7cc-44ad-ac26-12d3a88d9c8b" />


the qoution answers will be shown, since i previsly slove this lab the answer

so lets biggine by install and unzip the file
after we unzip the file we will get three files 
- auth.log
- utmp

<img width="1920" height="947" alt="Screenshot_2026-05-06_18_16_58" src="https://github.com/user-attachments/assets/f44333b0-42d5-48ee-a04f-f566fd686e13" />

we will use that files to answer the qoutions

let is start our invastion by take look at auth.log

<img width="1920" height="947" alt="Screenshot_2026-05-06_18_19_42" src="https://github.com/user-attachments/assets/fc7d5652-0d5b-4439-adc4-f159533ea688" />

as we see there is a lot of logs, let is be spicsfic and see all the Failed login

<img width="1920" height="947" alt="Screenshot_2026-05-06_18_23_13" src="https://github.com/user-attachments/assets/1211564b-7a8c-4ddb-b844-4a4425d9afaa" />

here we see that 







