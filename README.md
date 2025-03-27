# POC-task-5:

🔹 Task : Automated Security Auditing & Scripting:

✅ Step 1: Writing the Security Auditing Script:

1️⃣ Create the Script File:
   
   # Open the terminal and type.
       
      ┌──(monish㉿vbox)-[~]
      └─$ nano audit.sh
   # This will open the Nano text editor.

2️⃣ Copy and Paste the Following Script:

      #!/bin/bash

      echo " Security Audit Report - $(date)"
      echo "======================================"

      # 1️. Check user login attempts
      echo -e "\n User Login Attempts (last command):"
      last -n 10  # Show last 10 login attempts

      echo -e "\n Authentication Log (Failed SSH Logins):"
      grep "Failed password" /var/log/auth.log | tail -n 10  # Show last 10 failed login attempts

      # 2️. Detect running services
      echo -e "\n Running Services:"
      systemctl list-units --type=service --state=running | tail -n 10  # Show last 10 services

      # 3️. Monitor disk usage
      echo -e "\n Disk Usage:"
      df -h | grep "^/dev"  # Show disk usage for mounted devices

      echo -e "\n Security Audit Completed!"

3️⃣ Save and Exit:

     Press CTRL + X, then Y, and hit Enter to save the script.

✅ Step 2: Give Execution Permission:

  # Run the following command to make the script executable:

      ┌──(monish㉿vbox)-[~]
      └─$ chmod +x audit.sh

  # Run the script with

      ┌──(monish㉿vbox)-[~]
      └─$ ./audit.sh

✅ Step 4: Identify Weak Configurations (Exploitation Phase):

1️⃣ Old user accounts with weak passwords:

  # Check users on the system.

      ┌──(monish㉿vbox)-[~]
      └─$ cat /etc/passwd

  # Check for users who haven’t logged in recently.

       ┌──(monish㉿vbox)-[~]
       └─$ lastlog

2️⃣ Unnecessary Running Services:

  # Identify unnecessary services.

       ┌──(monish㉿vbox)-[~]
       └─$ systemctl list-units --type=service --state=running

  # Disable any unwanted service.

        ┌──(monish㉿vbox)-[~]
        └─$ sudo systemctl disable <service-name>

✅ Step 5: Mitigation & Automation:

1️⃣ Automate the Script with Cron:

  # Edit the cron jobs.

        ┌──(monish㉿vbox)-[~]
        └─$ crontab -e

  # Add this line to run the script daily at midnight.

         ┌──(monish㉿vbox)-[~]
         └─$ 0 0 * * * /path/to/audit.sh >> /var/log/security_audit.log

  # (Replace /path/to/audit.sh with the actual script location.)

✅ Step 6: Final Deliverables:

1️⃣ Report:    

In this task, we developed a Bash script to automate security auditing by:
✅ Checking user login attempts
✅ Detecting running services
✅ Monitoring disk usage

🔹 Key Steps & Findings
Created and executed audit.sh to collect security-related information.

Identified vulnerabilities, including:

Old user accounts with weak passwords

Unnecessary running services

Repeated failed SSH login attempts (brute-force attempts)

Exploited weak configurations to demonstrate security risks.

Mitigated risks by:

Automating security monitoring using cron

Implementing email alerts for unauthorized SSH login attempts

Disabling inactive accounts & unnecessary services
  






      
