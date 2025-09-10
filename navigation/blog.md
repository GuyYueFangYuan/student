---
layout: blogs 
title: Blog Chromebook guide
search_exclude: true
permalink: /blogs/
---

# 💻 Chromebook Ubuntu Troubleshooting and Device Switching Guide

This blog requires **0 prior coding experience** and starts from the very basics.  
If you were lost in class, this will pull you back to the right track.

---

## ✅ When to Use This Blog
Use this guide if:
1. You are currently using a **Chromebook** or a **KASM device**.
2. You are having trouble setting up the **virtual environment and VS Code**.
3. You’re done with how slow Chromebooks are and want to **switch to a new device**.

---

##  Why Do We Need Ubuntu?
You *can* access VS Code directly on your Chromebook.  
However, running VS Code this way removes many important features.  

To get the full development experience, we’ll:
1. Set up **Ubuntu** (Linux environment).
2. Run **VS Code inside Linux**.

---

##  Prerequisites
Before starting:
- You must have already created an **Open Coding Society account**.  
  👉 If not, go to [pages.opencodingsociety.com](https://pages.opencodingsociety.com/) and log in.

---

## 🖥️ Setting Up on Chromebook (KASM)

1. Go to [kasm.opencodingsociety.com/#/login](https://kasm.opencodingsociety.com/#/login).  
   - Log in with your **GitHub username** (typed in the *email* field) and the same password.

2. On the right, click the **orange Ubuntu Noble** → **Launch Session**.

3. Right-click inside the session → **Open Terminal Here**.

4. In the terminal, run:
   ```bash
   mkdir opencs
   cd opencs
   git clone <your forked GitHub repository link>
⚠️ If you don’t have your own repository, go to this link and click Fork.

Continue setup:
cd student/
./scripts/activate.sh   # Enter your GitHub username and email
./scripts/venv.sh
code .
When VS Code opens, go to Extensions (icon with 4 small squares) and install:

Python

Jupyter Notebook

🔄 Next Time You Log In
When you come back later:
cd opencs/student
source venv/bin/activate
code .
⚠️ Common Chromebook Issues
Ubuntu Freezing
Close the window and reopen Ubuntu through kasm.opencodingsociety.com.

In the session list, delete the old one, wait until it fully disappears, then start a new session.



source venv/bin/activate Not Working
Usually caused because you forgot
cd opencs/student
If you are in the correct directory and it still fails → ask your peers or Mr. Mortensen.

👉 Always check your spelling when typing commands — many errors are just typos.

🖥️ Switching to Windows (with WSL)
If Chromebooks are too slow and you’ve moved to a Windows system, here’s how to set up Ubuntu via WSL (Windows Subsystem for Linux):

In the Windows search bar, type and run:


wsl --install -d Ubuntu-24.04
Set up a username and password (save these somewhere safe).

Exit WSL:
exit
Set Ubuntu 24.04 as the default:
wsl --set-default Ubuntu-24.04
Start Ubuntu again:
wsl
Inside Ubuntu, run:
mkdir opencs
cd opencs
git config --global credential.helper "/mnt/c/Program Files/Git/mingw64/bin/git-credential-manager.exe"
git clone https://github.com/Open-Coding-Society/student.git
cd student/
./scripts/activate_ubuntu.sh
./scripts/activate.sh
After setup, close the terminal.

🔄 Next Time on Windows
When reopening Ubuntu:

bash
cd opencs/student
source venv/bin/activate
code .
⚠️ Common Windows Issues
PowerShell Error:
File Activate.ps1 cannot be loaded because running scripts is disabled on this system.

Fix:

Run PowerShell as Administrator.

Enter:
powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
🚨 Important: The setup process will not work inside PowerShell.
You must type commands inside the Ubuntu terminal that WSL installed.

🎉 That’s it! You now know how to set up your coding environment on both Chromebooks (KASM) and Windows (WSL).

If you run into problems, ask your peers, Mr. Mortensen, or ChatGPT — don’t push forward on the wrong path.













































































