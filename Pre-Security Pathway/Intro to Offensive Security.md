# Introduction to Offensive Security

## Tools
- [Gobuster](/Tools/Gobuster.md)

## Table of Contents
- [Introduction to Offensive Security](#introduction-to-offensive-security)
  - [Tools](#tools)
  - [Table of Contents](#table-of-contents)
    - [What is Offensive Security?](#what-is-offensive-security)
    - [Defensive Security Overview](#defensive-security-overview)
  - [Your First Hack](#your-first-hack)
    - [Start Machine](#start-machine)
    - [Step 1: Open a Terminal](#step-1-open-a-terminal)
    - [Step 2: Find Hidden Website Pages](#step-2-find-hidden-website-pages)
    - [Step 3: Hack the Bank](#step-3-hack-the-bank)
  - [Careers in Cybersecurity](#careers-in-cybersecurity)
    - [How to Start Learning](#how-to-start-learning)
    - [Offensive Security Careers](#offensive-security-careers)
  - [Next Steps](#next-steps)

### What is Offensive Security?
Offensive Security is process of :
- Breaking into computer systems.
- Exploiting software bugs.
- Finding loopholes in applications to gain unauthorized access.

To counter hackers, you must think like one. By identifying vulnerabilities and recommending patches before a cybercriminal does, you can secure systems effectively.

### Defensive Security Overview
In contrast, Defensive Security focuses on:
- Protecting an organization's network and computer systems.
- Analyzing and securing against digital threats.
- Investigating hacked devices, tracking cybercriminals, and monitoring infrastructure for malicious activity.

---

## Your First Hack

### Start Machine
When you begin this task, the virtual machine (VM) will launch automatically in split-screen mode, displaying a fake bank application called *FakeBank*.

- **Tip**: If the screen doesn't split, click on the blue "Show Split View" button.

### Step 1: Open a Terminal
A terminal (command-line interface) allows interaction with a computer without a graphical interface. Open the terminal using the Terminal icon on the machine.

### Step 2: Find Hidden Website Pages
Use "GoBuster," a command-line tool, to brute-force hidden directories and pages on the FakeBank website. It tries accessing the website with each word from a list to reveal hidden pages.

- [Gobuster](/Tools/Gobuster.md)

**Command to Run**:
```bash
gobuster -u http://fakebank.com -w wordlist.txt dir
```
```bash
=====================================================
Gobuster v2.0.1
=====================================================
[+] Mode         : dir
[+] Url/Domain   : http://fakebank.com/
[+] Threads      : 10
[+] Wordlist     : wordlist.txt
[+] Status codes : 200,204,301,302,307,403
[+] Timeout      : 10s
=====================================================
2022/04/11 18:23:28 Starting gobuster
=====================================================
/images (Status: 301)
/DIRECTORY_NAME_OUTPUT (Status: 200)
=====================================================
2022/04/11 18:23:38 Finished
=====================================================
```

This command scans the website, identifying pages that exist based on the list of potential names. The output will list discovered pages, indicated by `Status: 200`.

### Step 3: Hack the Bank
Using the hidden page (`/bank-transfer`) found in the previous step:
- Access the bank transfer page on the FakeBank website.
- Transfer $2000 from account number **2276** to your account **8881**.

If successful, your account balance will reflect the transfer after refreshing the page. 

**Note**: As an ethical hacker, your role is to find such vulnerabilities and report them to the bank to fix before they are exploited.

---

## Careers in Cybersecurity

### How to Start Learning
To become a hacker (security consultant) or defender (security analyst), break down the field into areas of interest and practice regularly. Build a habit of learning a little bit each day on TryHackMe, and you'll acquire the knowledge needed for your first job in cybersecurity.

### Offensive Security Careers
- **Penetration Tester**: Finds exploitable vulnerabilities in technology products.
- **Red Teamer**: Simulates adversary attacks to provide feedback from an enemy's perspective.
- **Security Engineer**: Designs, monitors, and maintains security controls to prevent cyberattacks.

---

## Next Steps
- Explore the **cyber careers room** for a deeper dive into different cybersecurity roles.
- Continue practicing and learning to build a strong foundation in cybersecurity.

**Good Luck!**
