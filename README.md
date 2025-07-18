
<p align="center">
  <img src="https://github.com/user-attachments/assets/a0b5a5cf-0053-45e4-a7cf-b0e09d0b4eba" alt="image" width="110%" />
</p>

---


# **Hashcat:** Password Cracking

<h3> Hector M. Reyes  | Cybersecurity Analyst  </h3>

### [Google Docs Link | Hashcat: Password Cracking](https://docs.google.com/document/d/17igSscDJUErcfI_waof9F4CHnfXhgeABef__AKM4daQ/pub)


---

## **Intro**
**Description** 
Welcome to the **Hashcat:** Password Cracking project. This initiative focuses on systematically tackling a password-cracking challenge. The primary objective is to provide a detailed, step-by-step explanation of identifying and exploiting a hashed password using various cybersecurity tools and methodologies. This challenge highlights essential skills in ethical hacking, particularly in password security. 

### Steps to Solve 
> 1. Identify the hash type.
> 2. Crack the hash.
> 3. Obtain the password.

### Tools Used 
>- Kali Linux | VMware  
>- Hashcat | Wordlists (e.g., rockyou.txt)
>- Hashes.org | crackstation.net 

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

### Hash Function Behavior 
> Knowledge of how hash functions work, including converting input data into a fixed-size string of characters, typically a hash code.

![image](https://github.com/user-attachments/assets/4b5ea32f-e265-47a2-b3ff-e3e1c9166e35)
<br /> 

### Wordlists 
- **Precompiled Lists:** </b>
Familiarity with widely used word lists, such as rockyou.txt, which contain common passwords and phrases that can be used in dictionary attacks.
- **Wordlist Management:** </b>
Skills in managing and updating wordlists to ensure they remain relevant and comprehensive, incorporating new and emerging password trends.
- **Hashcat:** </b>
Installation and Setup: Proficiency in installing and configuring Hashcat in various environments, including virtual machines and cloud instances, including standard commands, options, and flags used for different types of attacks.

![image](https://github.com/user-attachments/assets/4f654418-056c-4e3e-bdbb-68a1062989c3)

### Cryptography Basics 
- **Symmetric vs. Asymmetric Encryption:** </b>
Understanding the differences between these two main types of encryption and their respective uses.
- **Salting:** </b>
Knowledge of how salts enhance security by adding randomness to hash functions and how to handle salted hashes during cracking attempts.
- **Key Management:** </b>
This section offers insights into best practices for key management and how weak critical practices can lead to vulnerabilities..

### Operating Systems 
- **Linux Fundamentals:** </b>
Proficiency in navigating and operating within Linux environments, particularly Kali Linux, which is commonly used for cybersecurity tasks.
- **Command-Line Skills:** </b>
Strong command-line skills for executing scripts, managing files, and troubleshooting issues during cracking.

### Cybersecurity Concepts
1.	**Password Policies:** </b>
Understanding the principles of strong password policies and how weak passwords compromise security.
2.	**Attack Vectors:** </b>
Awareness of various attack vectors that leverage weak passwords and hash vulnerabilities, and how to defend against them.
3.	**Defense Mechanisms:** </b>
Knowledge of defense mechanisms such as multi-factor authentication (MFA) and how they mitigate the risks associated with password cracking.

---

# Introduction to the Problem
The first step in addressing this challenge was to identify the hash type. I used hash.com. After using a hash analyzer, it was established that the hash type was NTLM. With this knowledge in hand, I configured my Kali Linux environment to commence the password-cracking process.

![image](https://github.com/user-attachments/assets/5764b952-cd99-4e34-9b14-6fc31e981a43)

### Working Toward a Solution
To crack the NTLM hash, I used the rockyou.txt word list with Hashcat. The environment setup involved ensuring that Hashcat was installed and configured correctly, as well as preparing the necessary files for the Attack. <br/>
To crack the NTLM hash, I utilized the rockyou.txt wordlist with Hashcat. The environment setup involved ensuring that Hashcat was installed and configured correctly, as well as preparing the necessary files for the Attack. <br/>
![image](https://github.com/user-attachments/assets/57efc0ae-fbb4-4195-9dd1-942c02c12d22)


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

Execution <br/>
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
<br /> 


---

## Breakdown: Steps, Strategies, Pitfalls, and Lessons Learned

#### Steps
> 1. Identified the hash type as NTLM.
> 2. Utilized the rockyou.txt wordlist with Hashcat.
> 3. Successfully cracked the hash to reveal the password.

### Strategies:

#### Identifying Hash Type: 
> Accurate identification using online tools or command-line utilities.

#### Choosing the Right Tools and Environment:
> 1. **Kali Linux VM:** Deployed via VirtualBox for a controlled environment.
> 2. **Hashcat:** Selected for its powerful and flexible password-cracking capabilities.
> 3. **Wordlist:** Utilized the comprehensive rockyou.txt wordlist.

#### Pitfalls:
Misidentifying the hash type.
> Employing an outdated or incomplete wordlist.

## Key Lessons Learned
1.	**Accurate Hash Identification:** <br /> 
Correctly identifying the hash type is crucial for successful password cracking. Reliable hash analyzers and a solid understanding of different hashing algorithms are essential first steps.
2.	**Tool Proficiency:** <br /> 
Familiarity with powerful tools like Hashcat, combined with effective use in environments like Kali Linux VM, ensures efficient and effective cracking processes. Understanding the features of these tools can help you achieve better results.
3.	**Importance of Wordlists:** <br /> 
The quality and comprehensiveness of wordlists, such as rockyou.txt, significantly impact success rates. Up-to-date and extensive wordlists increase the likelihood of successful password cracking.
4.	**Attention to Detail:** <br /> 
Meticulous preparation and verification of all details, including the hash type, word list, and tool settings, are crucial. Oversight can lead to failure, making accuracy critical at every step.
5.	**Strategic Approach:** <br /> 
A methodical approach to solving challenges involves systematic planning and execution. Identifying potential pitfalls and strategizing can improve success rates.
6.	**Continuous Learning:** <br /> 
Engaging in practical exercises, such as CTF challenges, keeps skills sharp and ensures understanding of current trends. The dynamic nature of cybersecurity necessitates ongoing learning and adaptation.
7.	**Application in Real-World Scenarios:** <br /> 
The knowledge gained directly applies to professional cybersecurity roles, emphasizing practical skills in anticipating and defending against threats.

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

