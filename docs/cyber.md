# Cyber Security Learning

## 1. Introduction to cyber security

Cybersecurity is the practice of protecting systems, networks, and programs from digital attacks. These cyberattacks are usually aimed at accessing, changing, or destroying sensitive information; extorting money from users; or interrupting normal business processes.

### 1.1 Offensive Security

Offeensive security is a process of breakting into computer sysytem , exploiting software bugs and finding loopholes in application to gain access to unauthorized datas.

To neat a hacker you need to think like a hacker by finding vulnerability and recommending patches before cyber crime occures.

offensive security includes :

* **Web application security** (practice of protecting websites, application and API from cyber attacks)
*  **Network Security** ( Protecting the underlying networking infrastructure from unauthorized access, misuse, malfunction, modification, destruction, or improper disclosure. it incolves creating a secure infrastructure for devices and users for smooth communication)
*  **Operating System Security** (practice of securing operating system from cyber attacks like threats, viruses, worms, malware or remote hacker intrusions.)

### 1.2 Defensive Security

Defensive security is a process of securing an orginazations data from cyber attacks by implementing security measures to protect the data from unauthorized access.

Defensive security includes Check for :

* **Vulnerabilities** (weekness and oppertunity for cyber attacks to exploit into an organization system)
* **Policy violations**  (protecting acces to data of an orgination)
* **Unauthorized activity** (protecting data from unauthorized access)
* **Network intrusions** (unauthorized penetration into an computer system)

### **What is GoBuster?**

**Gobuster** Tool **enumerates hidden directories and files in the target domain** by performing a brute-force attack.

```
gobuster -h 
```
For listing all the gobuster commands avalible in the tool.

#### **Gobuster DIR (Directory Enumeration Mode)**

DIR commands in gobuster is used to **enumerate directories and files** in the target domain.

##### **Common Options for `gobuster dir`**

| Option | Description |
|--------|-------------|
| `-u`   | Specifies the target URL (e.g., `http://example.com`). |
| `-w`   | Specifies the wordlist file to use for brute-forcing directories/files (e.g., `/usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`). |
| `-x`   | Specify file extensions to search for (e.g., `.php`, `.html`). |
| `-t`   | Sets the number of threads (higher values can speed up the process). |
| `-o`   | Outputs results to a file (e.g., `results.txt`). |
| `-s`   | Show only specific status codes (e.g., `200, 301`). |
| `-b`   | Blacklist certain status codes from the output (e.g., `403`). |
| `-r`   | Follow redirects. |
| `-k`   | Skip SSL certificate verification (useful for self-signed certs). |
| `-q`   | Enable "quiet" mode (show fewer messages). |


