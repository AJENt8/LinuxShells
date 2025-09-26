# 🐧 Linux Shells — Bash Scripting (TryHackMe)

> **Summary:** Focused on practical Bash scripting using the default shell `/bin/bash`. Created and executed scripts with variables, loops, conditionals, a simple "locker" utility, and a flag-hunting script that searches `/var/log`. Practiced file editing with `nano`, making scripts executable (`chmod +x`), and running them (`./script_name.sh`).

---

## 🎯 Objective
Demonstrate comfort with the default Linux shell (`/bin/bash`) by writing small, reusable Bash scripts that illustrate variables, input, loops, conditionals, and simple file searching for incident/CTF-style tasks.

---

## 🛠️ Environment
- Platform: TryHackMe — *Linux Shells* room  
- Shell: `/bin/bash` (default)  
- Editor: `nano`  
- Commands used: `chmod +x script_name.sh`, `./script_name.sh`, `grep`, `sudo su` (for root access when needed)

---

## 🚀 Workflow & Example Scripts

### 1) Create & Run scripts
- Created scripts using `nano`:
  ```bash
  nano first_script.sh
- Made scripts executable and ran them:
`chmod +x first_script.sh`
`./first_script.sh`
### 2) First script — user input & variables (`first_script.sh`)
- ```bash
  #!/bin/bash
  echo "Hey, what's your name?"
  read name
  echo "Welcome, $name"
- What this shows: reading stdin into variables and simple output interpolation.
### 3) Loop script (`loop_script.sh`)
- ```bash
  #!/bin/bash
  for i in {1..10};
  do
    echo $i
  done
- What this shows: basic numeric loops and iteration.
### 4) Conditional script with if statement (`conditional_script.sh`)
- ```bash
  #!/bin/bash
  echo "Please enter your name first:"
  read name
  if [ "$name" = "Stewart" ]; then
      echo "Welcome Stewart! Here is the secret: THM_Script"
  else
      echo "Sorry! You are not authorized to access the secret."
  fi
- What this shows: string comparison, `if`/`else` branching, and input validation.
### 5) Locker script (multi-input + conditional logic) (`locker_script.sh`)
- ```bash
  #!/bin/bash

  username=""
  companyname=""
  pin=""

  for i in {1..3}; do
    if [ "$i" -eq 1 ]; then
      echo "Enter your Username:"
      read username
    elif [ "$i" -eq 2 ]; then
      echo "Enter your Company name:"
      read companyname
    else
      echo "Enter your PIN:"
      read pin
    fi
  done

  if [ "$username" = "John" ] && [ "$companyname" = "Tryhackme" ] && [ "$pin" = "7385" ]; then
    echo "Authentication Successful. You can now access your locker, John."
  else
    echo "Authentication Denied!!"
  fi
- What this shows: combining loops with conditional tests and logical `&&` chaining for multi-factor validation logic.
### 6) Flag hunt script — search logs for a flag (`flag_hunt.sh`)
- ```bash 
  #!/bin/bash
  directory="/var/log"
  flag="thm-flag01-script"

  echo "Flag search in directory: $directory in progress..."

  for file in "$directory"/*.log; do
    if grep -q "$flag" "$file"; then
      echo "Flag found in: $(basename "$file")"
    fi
  done
- Usage: run as root or with sufficient permissions (e.g., sudo ./flag_hunt.sh) to search /var/log.
- Follow-up command you used:
`grep "cat" /var/log/authentication.log`
which demonstrates targeted grep usage to reveal hidden/related messages.
## ✅ Outcome
- Wrote, executed, and debugged multiple Bash scripts using `/bin/bash`.
- Practiced file editing (`nano`), permission changes (`chmod +x`), and execution (`./`).
- Demonstrated foundational scripting skills useful for automation, small tooling, and incident triage (e.g., log searching with `grep`).
- Completed a small CTF-style task by locating a flag in system logs via a scripted search.
## 🧩 Skills Demonstrated
- Bash scripting fundamentals: variables, input, loops, conditionals
- File editing and execution workflow (`nano`, `chmod`, `./`)
- Log searching & automation for triage (`grep`, scripted iteration)
- Practical knowledge of when root is required and how to use `sudo su` responsibly

