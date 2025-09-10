<p align="center">
  <img src="https://github.com/user-attachments/assets/a0b5a5cf-0053-45e4-a7cf-b0e09d0b4eba" alt="image" width="110%" />
</p>

---

# **Hashcat:** Password Cracking (NTLM)
### Hector M. Reyes  | Cybersecurity Analyst
**Focus:** End-to-end password cracking workflow using Hashcat in a Kali Linux VM.

![password_strength](https://github.com/user-attachments/assets/46e0c415-8cd6-4246-a453-21666509c475)

## TL;DR
- Crack a provided **NTLM** hash with **Hashcat** + **rockyou.txt** in a Kali VM.
- Output results to `cracked.txt` and document defender takeaways (policies, MFA).


---

# 🔐 Hashcat: Password Cracking

## What This Lab Covers
This lab demonstrates a reproducible, ethical workflow to crack a single NTLM hash. You’ll identify the hash type, prepare the environment, run a dictionary attack, verify results, and note blue-team implications.

**You will:**
- Verify the hash type (NTLM / Hashcat `-m 1000`)
- Prepare Hashcat + wordlist
- Run a dictionary attack
- Validate results and capture evidence
- Summarize key lessons for defenders

> **Ethics:** Use only in labs/authorized environments.

---

### 🧰 Tools Reference

| **Category**   | **Tool / Feature**                  | **Purpose**                                    |
| -------------- | ----------------------------------- | ---------------------------------------------- |
| **OS**         | Kali Linux (VMware / VirtualBox)    | Controlled lab environment for cracking tasks  |
| **Cracking**   | Hashcat                             | Password hash cracking via GPU/CPU acceleration|
| **Wordlists**  | rockyou.txt, custom wordlists       | Dictionary/brute-force attacks on hashes       |
| **Lookup**     | Hashes.org / crackstation.net       | Online hash identification & verification      |
| **Utilities**  | gzip / gunzip, echo, cat, ls        | Manage wordlists, create hash files, verify output |

> 🕵️‍♂️ **Happy Hunting!**

<img src="https://github.com/user-attachments/assets/6dfc9198-6054-44b3-9cdc-51d3a9cf02b3" width="80%" />

---

---
# **Hashcat:** Password Cracking

**Challenge Description**  
This challenge focuses on password cracking through hash analysis, a key aspect of cybersecurity and ethical hacking. It involves reversing cryptographic hash functions used to securely store passwords, testing skills critical for identifying security vulnerabilities.

**Relation to Ethical Hacking Course**  
The exercise emphasizes the necessary skills for cracking passwords, which are essential in both ethical hacking and cybersecurity defense. It highlights the importance of strong password policies and the risks associated with weak passwords, aligning with the objectives of the ethical hacking course.

**Lab Topic**  
The lab focused on password security and cracking techniques, including brute-force and dictionary attacks, as well as the use of tools such as Hashcat. Participants learned to analyze various hash types and improve password security.

**Hash Algorithms**  
Understanding hash algorithms (e.g., MD5, SHA-1, NTLM) is vital, as each has unique characteristics and vulnerabilities.  

![image](https://github.com/user-attachments/assets/4b5ea32f-e265-47a2-b3ff-e3e1c9166e35)

## 🔑 Key Hash Algorithms (quick reference)
| Algorithm | Notes (Strengths/Weaknesses)               | Common Use |
|---|---|---|
| MD5 | Very fast, **broken** (collisions)               | Legacy apps/DBs |
| SHA-1 | Better than MD5, **broken** for modern use     | Legacy systems |
| SHA-256 | Strong, widely used                          | Modern apps |
| NTLM | Windows hash; fast → **brute-forceable**        | AD/Windows |
| bcrypt | Salted, slow → **resists cracking**           | Modern DBs |

**Wordlists**  
Familiarity with precompiled lists like rockyou.txt for dictionary attacks and skills to manage and update wordlists are crucial.

![image](https://github.com/user-attachments/assets/4f654418-056c-4e3e-bdbb-68a1062989c3)

**Hashcat: Installation and Setup**  
Participants learned to install and configure Hashcat and understand commands for various attack types.

**Cryptography Basics**  
Key concepts include differences between symmetric and asymmetric encryption, the role of salting, and best practices for key management.

**Operating Systems**  
Proficiency in Linux, particularly Kali Linux, and strong command-line skills are essential for executing scripts and managing files.

**Cybersecurity Concepts**  
Knowledge of strong password policies, attack vectors that exploit weak passwords, and defense mechanisms such as multi-factor authentication is crucial for effective cybersecurity.

---

# The Problem
The first step in addressing this challenge was to identify the hash type. I used hash.com. After using a hash analyzer, it was established that the hash type was NTLM. With this knowledge in hand, I configured my Kali Linux environment to commence the password-cracking process.

![image](https://github.com/user-attachments/assets/5764b952-cd99-4e34-9b14-6fc31e981a43)

### Working Toward a Solution
To crack the NTLM hash, I used the rockyou.txt word list with Hashcat. The environment setup involved ensuring that Hashcat was installed and configured correctly, as well as preparing the necessary files for the Attack. <br/>
To crack the NTLM hash, I utilized the rockyou.txt wordlist with Hashcat. The environment setup involved ensuring that Hashcat was installed and configured correctly, as well as preparing the necessary files for the Attack. <br/>
![image](https://github.com/user-attachments/assets/57efc0ae-fbb4-4195-9dd1-942c02c12d22)

## 🚀 Setup & Pre-Engagement (One-Time Prep)
Stand up a minimal, reproducible environment to avoid false starts.

- Update Kali and install Hashcat.
- Create `hash.txt` with the target hash.
- Prepare the `rockyou.txt` dictionary.
- (Optional) Validate GPU access for speed.

**Pro Tips**
- Confirm the **hash type first**—misidentification wastes cycles.
- Keep cracked output separate (`-o cracked.txt`) for audit/evidence.
- Start with **dictionary/hybrid**; escalate to masks/brute only if needed.
- Log commands, options, timing, and outcomes as you go.

### 1) Environment Setup
Kali Linux VM Configuration: Deployed Kali Linux via VirtualBox, ensuring the virtual machine was up-to-date and configured for optimal performance.
```
sudo apt-get update && sudo apt-get upgrade
```

![image](https://github.com/user-attachments/assets/5a2425ad-46ef-4a06-9cd5-40577842d6e1)

### 2) Hashcat Installation
It was verified that Hashcat was installed correctly on the Kali Linux VM. If you're using another Linux Distribution, install hashcat. 
```
sudo apt-get install hashcat
```

### 3) Verify Installation  
Run a simple command to check the installation if hashcat is installed.
```
hashcat-- version
```

### 4) Preparation
Hash File Creation: Create a text file containing the hash, for example, hash.txt. Use the "ls" command to verify the file location.
```
echo "A675081AAF0B43D60A819653635AC405" > hash.txt
```

### 5) Wordlist Selection: 
I selected the rockyou.txt wordlist, a comprehensive and widely used list of common passwords, to ensure it was available and accessible on the Kali Linux VM.
> Locate the rockyou.txt or wordlists on the VM
```
/usr/share/wordlists/rockyou.txt
```

### 6) Unzip the wordlist if it is compressed
```
gunzip /usr/share/wordlists/rockyou.txt.gz
```

### 7) Execution
Command Configuration: Constructed the Hashcat command with the necessary parameters to target the NTLM hash type, specifying the hash file and the wordlist. The command included options for efficient processing, such as selecting the attack mode and enabling GPU acceleration.

### Explanation of parameters
```
1.	-m 1000: Specifies the hash type as NTLM.
2.	-a 0: Sets the attack mode to dictionary attack.
3.	-o cracked.txt: Outputs the cracked passwords to a file named cracked.txt.
4.	hash.txt: The file containing the NTLM hash.
5.	/usr/share/wordlists/rockyou.txt: The wordlist file.
```

### 9) Initiating the Attack 
I ran the configured Hashcat command, initiating the password-cracking process. I monitored the progress and ensured the system resources were optimally utilized to complete the task efficiently.
```
hashcat -m 1000 -a 0 -o hash.txt hash.txt /usr/share/wordlists/rockyou.txt
```
### 10) Password Recovery
Upon completion, check the hash.txt file for the cracked password:
```
cat hash.txt
```

![image](https://github.com/user-attachments/assets/1147dab0-4318-4a7b-b654-52b7ef7f0a9b)

![image](https://github.com/user-attachments/assets/a59eaf46-29a9-40e4-86dd-38e69b847279)

---

## 🧭 Strategies, Pitfalls, Lessons

### Strategies
- Validate hash type first; pivot attack based on type (NTLM ≠ SHA1).
- Start with high-quality dictionaries; add hybrid rules if needed.
- Save outputs and keep a short evidence log (time, mode, wordlist).

### Common Pitfalls
- Attacking with the wrong mode (results in 0 cracks).
- Forgetting to unzip rockyou.txt.
- Running purely on CPU when GPU is available.

### Key Lessons
1. Identification First: Correct hash mode makes or breaks the crack.
2. Wordlist Quality: Up-to-date lists dramatically improve success.
3. Defense Matters: Strong policies + MFA blunt these attacks.


### Relationship to the Workplace
Understanding and executing hash-cracking methodologies is indispensable for cybersecurity professionals. This expertise is precious for Red Team members, such as penetration testers, who must simulate real-world attacks to identify vulnerabilities within an organization's security infrastructure. Blue Team members, such as SOC analysts and security evaluators, benefit from this knowledge by gaining insight into potential threats and developing effective defense strategies. <br /> 

Cybersecurity experts can master password-cracking techniques to proactively address and mitigate security weaknesses, thereby ensuring a more resilient security posture. This proficiency helps identify and rectify vulnerabilities, playing a crucial role in educating stakeholders about the importance of strong password policies and comprehensive security measures. In essence, the skills and insights gained from this project contribute significantly to the overarching goal of safeguarding organizational assets and maintaining robust cybersecurity defenses.

![Hashcat-Animation](https://github.com/user-attachments/assets/647d783c-6964-4b87-ac18-106ba69903c7)
<br /> 

---

🔎 Background Aids (Optional Reading)
Hash Function Basics

### Hash Algorithms 
Types of Hash Algorithms </b>
> Understanding different types of hash algorithms, such as MD5, SHA-1, SHA-256, and NTLM, is crucial. Each algorithm has unique characteristics and vulnerabilities that affect how it can be cracked.

### 🔑 Key Hash Algorithms

| **Algorithm** | **Strengths**            | **Weaknesses**              | **Where Seen**                |
| ------------- | ------------------------ | --------------------------- | ----------------------------- |
| MD5           | Fast, lightweight        | Broken, collisions easy     | Legacy apps, old DBs          |
| SHA-1         | More secure than MD5     | Broken, weak for modern use | SSL certs, legacy systems     |
| SHA-256       | Strong, widely used      | Slower than MD5/SHA-1       | Modern apps, blockchain       |
| NTLM          | Windows authentication   | Vulnerable to brute force   | Active Directory environments |
| bcrypt        | Salted, slow, resistant  | Performance cost            | Modern password databases     |


---

## **Summary**
This project showcases essential skills for solving Capture the Flag (CTF) challenges, with a focus on password cracking through hash analysis. I identified the hash type as NTLM and successfully cracked the password using Hashcat and the rockyou.txt wordlist. This experience underscores the importance of hash identification, tool selection, and detail verification in cybersecurity.

The techniques applied are crucial for cybersecurity professionals, especially in penetration testing, to effectively combat password-based threats. Overall, this project underscores the importance of hands-on exercises in developing the skills necessary for maintaining robust security infrastructures.

![image](https://github.com/user-attachments/assets/79b5cba3-2343-4b3d-b4dd-f6e6f7874b8a)

