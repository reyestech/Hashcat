<p align="center">
  <img src="https://github.com/user-attachments/assets/a0b5a5cf-0053-45e4-a7cf-b0e09d0b4eba" alt="image" width="110%" />
</p>

---

# **Hashcat:** Password Cracking
### Hector M. Reyes  | Cybersecurity Analyst

---

# 🔐 Hashcat: Password Cracking
This lab demonstrates password cracking with Hashcat in a controlled Kali Linux environment. The goal is to walk through the process of identifying a hash, configuring the environment, and cracking the password. The exercise highlights both red-team offensive skills and blue-team defensive lessons for password security.

- Identify and verify the hash type (NTLM).
- Configure Kali Linux VM with Hashcat.
- Prepare hash files and select an appropriate wordlist.
- Run Hashcat attack and monitor cracking process.
- Recover and validate the cracked password.
- Document lessons learned for both offensive and defensive use cases.

### 📂 Evidence Artifacts
The challenge began with a single NTLM hash string to be analyzed and cracked. Supporting resources included:
- NTLM hash provided as input (hash.txt).
- Wordlist: rockyou.txt for dictionary attacks.
- Online tools for verification (Hashes.org, crackstation.net).

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

# **Hashcat:** Password Cracking
Challenge Description <br/>
This challenge involves password cracking through hash analysis, a vital component of cybersecurity, particularly ethical hacking. Hash analysis involves understanding and decrypting cryptographic hash functions, which are commonly used to store passwords securely. The challenge tests one's ability to reverse-engineer these hashes to retrieve the original password, an essential skill for identifying and mitigating security vulnerabilities.

![password_strength](https://github.com/user-attachments/assets/46e0c415-8cd6-4246-a453-21666509c475)

### Relation to Ethical Hacking Course
This exercise highlights the practical skills needed to crack passwords, which are crucial for both ethical hacking and cybersecurity defense strategies. Password cracking is not just about bypassing security, but also about understanding the importance of strong password policies and the consequences of using weak passwords. These goals align with the objectives of the ethical hacking course, which aims to equip learners with the knowledge to test, improve, and enhance security systems.

### Lab Topic
The laboratory focused on password security and cracking techniques, providing practical experience in ethical hacking methods. The lab explored various approaches to password cracking, including brute force attacks, dictionary attacks, and the use of advanced tools such as Hashcat. Participants learned how to analyze different hash types, utilize word lists effectively, and apply practical solutions to enhance password security in their systems.

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


### Hash Function Behavior 
> Knowledge of how hash functions work, including converting input data into a fixed-size string of characters, typically a hash code.

![image](https://github.com/user-attachments/assets/4b5ea32f-e265-47a2-b3ff-e3e1c9166e35)

### Wordlists 
- **Precompiled Lists:** Familiarity with widely used word lists, such as rockyou.txt, which contain common passwords and phrases that can be used in dictionary attacks.
- **Wordlist Management:** Skills in managing and updating wordlists to ensure they remain relevant and comprehensive, incorporating new and emerging password trends.
- **Hashcat:** Installation and Setup: Proficiency in installing and configuring Hashcat in various environments, including virtual machines and cloud instances, including standard commands, options, and flags used for different types of attacks.

![image](https://github.com/user-attachments/assets/4f654418-056c-4e3e-bdbb-68a1062989c3)

### Cryptography Basics 
- **Symmetric vs. Asymmetric Encryption:** Understanding the differences between these two main types of encryption and their respective uses.
- **Salting:** Knowledge of how salts enhance security by adding randomness to hash functions and how to handle salted hashes during cracking attempts.
- **Key Management:** This section offers insights into best practices for key management and how weak critical practices can lead to vulnerabilities..

### Operating Systems 
- **Linux Fundamentals:** Proficiency in navigating and operating within Linux environments, particularly Kali Linux, which is commonly used for cybersecurity tasks.
- **Command-Line Skills:** Strong command-line skills for executing scripts, managing files, and troubleshooting issues during cracking.

### Cybersecurity Concepts
1.	**Password Policies:** Understanding the principles of strong password policies and how weak passwords compromise security.
2.	**Attack Vectors:** Awareness of various attack vectors that leverage weak passwords and hash vulnerabilities, and how to defend against them.
3.	**Defense Mechanisms:** Knowledge of defense mechanisms such as multi-factor authentication (MFA) and how they mitigate the risks associated with password cracking.

---

# The Problem
The first step in addressing this challenge was to identify the hash type. I used hash.com. After using a hash analyzer, it was established that the hash type was NTLM. With this knowledge in hand, I configured my Kali Linux environment to commence the password-cracking process.

![image](https://github.com/user-attachments/assets/5764b952-cd99-4e34-9b14-6fc31e981a43)

### Working Toward a Solution
To crack the NTLM hash, I used the rockyou.txt word list with Hashcat. The environment setup involved ensuring that Hashcat was installed and configured correctly, as well as preparing the necessary files for the Attack. <br/>
To crack the NTLM hash, I utilized the rockyou.txt wordlist with Hashcat. The environment setup involved ensuring that Hashcat was installed and configured correctly, as well as preparing the necessary files for the Attack. <br/>
![image](https://github.com/user-attachments/assets/57efc0ae-fbb4-4195-9dd1-942c02c12d22)


### Environment Setup
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

### Environment Setup
Kali Linux VM Configuration: Deployed Kali Linux via VirtualBox, ensuring the virtual machine was up-to-date and configured for optimal performance.
```
sudo apt-get update && sudo apt-get upgrade
```

![image](https://github.com/user-attachments/assets/5a2425ad-46ef-4a06-9cd5-40577842d6e1)

### Hashcat Installation
It was verified that Hashcat was installed correctly on the Kali Linux VM. If you're using another Linux Distribution, install hashcat. 
```
sudo apt-get install hashcat
```

### Verify Installation  
Run a simple command to check the installation if hashcat is installed.
```
hashcat-- version
```

### Preparation
Hash File Creation: Create a text file containing the hash, for example, hash.txt. Use the "ls" command to verify the file location.
```
echo "A675081AAF0B43D60A819653635AC405" > hash.txt
```

### Wordlist Selection: 
I selected the rockyou.txt wordlist, a comprehensive and widely used list of common passwords, to ensure it was available and accessible on the Kali Linux VM.

Locate the rockyou.txt or wordlists on the VM
```
/usr/share/wordlists/rockyou.txt
```

### Unzip the wordlist if it is compressed
```
gunzip /usr/share/wordlists/rockyou.txt.gz
```

#### Execution
Command Configuration: Constructed the Hashcat command with the necessary parameters to target the NTLM hash type, specifying the hash file and the wordlist. The command included options for efficient processing, such as selecting the attack mode and enabling GPU acceleration.

### Explanation of parameters
```
1.	-m 1000: Specifies the hash type as NTLM.
2.	-a 0: Sets the attack mode to dictionary attack.
3.	-o cracked.txt: Outputs the cracked passwords to a file named cracked.txt.
4.	hash.txt: The file containing the NTLM hash.
5.	/usr/share/wordlists/rockyou.txt: The wordlist file.
```

### Initiating the Attack 
I ran the configured Hashcat command, initiating the password-cracking process. I monitored the progress and ensured the system resources were optimally utilized to complete the task efficiently.
```
hashcat -m 1000 -a 0 -o hash.txt hash.txt /usr/share/wordlists/rockyou.txt
```
### Password Recovery
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

## **Summary**
This project exemplifies the critical skills required to solve a Capture the Flag (CTF) challenge, with a focus on password cracking through hash analysis. By accurately identifying the hash type as NTLM and utilizing the robust password-cracking tool Hashcat, along with the comprehensive rockyou.txt wordlist, I successfully cracked the password for the given user. This process highlighted the importance of identifying hash types, strategically selecting tools and resources, and meticulously verifying all details to ensure success.  <br />

The knowledge and techniques applied in this project are directly relevant to cybersecurity, emphasizing the necessity for cybersecurity professionals, particularly those involved in penetration testing and security operations, to effectively understand and counter password-based threats. The experience gained from this project reinforces the value of practical, hands-on exercises in developing and honing the skills essential for maintaining robust security infrastructures in real-world scenarios.

![image](https://github.com/user-attachments/assets/79b5cba3-2343-4b3d-b4dd-f6e6f7874b8a)

