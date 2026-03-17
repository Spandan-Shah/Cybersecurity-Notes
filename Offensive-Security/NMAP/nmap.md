# 1. Introduction to Cybersecurity Tools

> [!IMPORTANT]
> **Cybersecurity tools** are software utilities used to protect systems, detect vulnerabilities, monitor networks, and assess security posture.

These tools help professionals across the industry—including **ethical hackers**, **penetration testers**, **SOC analysts**, and **administrators**—to understand weaknesses before attackers can exploit them.

---

### Key Highlight
One of the most important and widely used tools in cybersecurity is **`Nmap`**.

## 2. What is Nmap?

**Nmap** stands for **Network Mapper**. It is an open-source cybersecurity and network discovery tool used for:

*   **Host discovery**
*   **Port scanning**
*   **Service detection**
*   **Version detection**
*   **Operating system detection**
*   **Security auditing**

> [!TIP]
> It is mainly used to understand what is exposed on a machine or network.


## 3. Why Nmap is Important in Cybersecurity

In cybersecurity, before doing anything else, we first need to understand the target system or network.

We need to know things like:
*   **Is the system alive or not**
*   **What ports are open**
*   **What services are running**
*   **Is anything unnecessary exposed**
*   **Is the system safe or risky**

> [!NOTE]
> This is where **Nmap** becomes very useful.

Nmap helps us “look at” a machine from the network side. It tells us what that machine is showing to others. In simple words, it helps us see the **visible doors** of a computer.

#### For example, if a server has:
*   **Port 80 open**: It may be running a website.
*   **Port 22 open**: It may allow remote login through SSH.
*   **Port 3306 open**: It may be running a MySQL database.

Now this matters because if too many services are open, the system becomes more exposed. More open services can mean more chances for weakness.

---

### Summary of Importance
Nmap is important because it helps us find:
1.  **What is open**
2.  **What is running**
3.  **What may be risky**

That is why **Nmap** is one of the first tools people learn in cybersecurity.


## 4. Real-Life Use of Nmap

Nmap is not just for theory. It is used in real life by professionals such as:

*   **Ethical Hackers**
*   **Penetration Testers**
*   **SOC Analysts**
*   **Network Administrators**
*   **System Administrators**
*   **Security Auditors**

### Let us understand with a simple example:

Suppose a company has a web server. They think only the website should be accessible. So ideally, only these ports should be open:
*   **80** for **HTTP**
*   **443** for **HTTPS**

But when they run **Nmap**, they find:
*   **22** open
*   **80** open
*   **443** open
*   **3306** open

#### This means:
*   **SSH** is open
*   The **website** is open
*   The **secure website** is open
*   The **database port** is also open

> [!WARNING]
> This may be dangerous because the database should usually not be open to everyone.

Nmap helps security teams check whether the system is showing more than it should. In simple words, Nmap helps answer this question:

> **“What can this machine be accessed for from the network?”**


## 5. What is a Port?

To understand **Nmap**, you must understand ports first.

A **port** is like a numbered communication point on a computer. Think of a computer like a building and ports like **doors**:

*   Each door has a **number**.
*   Different **services** use different doors.
*   If a door is **open**, communication can happen through it.

### Some Common Ports:


| Port Number | Service |
| :--- | :--- |
| **21** | FTP |
| **22** | SSH |
| **23** | Telnet |
| **25** | SMTP |
| **53** | DNS |
| **80** | HTTP |
| **110** | POP3 |
| **143** | IMAP |
| **443** | HTTPS |
| **3306** | MySQL |

> [!NOTE]
> When **Nmap** scans a machine, it checks these ports and sees which ones are open.

---

### Why Ports Matter

If a port is open, it usually means a service is running there. That service may be:

*   **Useful** or **Normal**
*   **Unnecessary** or **Old**
*   **Badly configured** or **Vulnerable**

> [!IMPORTANT]
> This is why open ports are very important in cybersecurity.


## 6. Port States in Nmap

When **Nmap** scans ports, it does not always say only “yes” or “no”. It shows the specific **state** of each port to provide better context.

---

### The Main Port States:

#### 1. Open
This means the port is open and a service is **listening** there.
> **Example:** Port `80 open` means a web service may be running.

#### 2. Closed
This means the port is **reachable**, but no service is currently running on it.

#### 3. Filtered
This means Nmap **cannot clearly see** the port because a firewall or filter is blocking the scan.

#### 4. Open|Filtered
This means Nmap is **not fully sure** whether the port is open or filtered.

#### 5. Closed|Filtered
This means Nmap **cannot fully decide** whether the port is closed or filtered.

---

### 💡 Easy Understanding

*   **Open** = Something is there.
*   **Closed** = Nothing is there right now.
*   **Filtered** = Something is blocking Nmap from checking properly.

> [!TIP]
> This helps us understand not only the target machine but also the **firewall behavior**.


## 7. Installing Nmap

Before using **Nmap**, you need to install it. 

On many cybersecurity systems like **Kali Linux**, Nmap is already pre-installed. However, if it is not, you can install it manually.

---

### On Ubuntu / Debian / Kali:
```bash
sudo apt install nmap
```

### Check version:
```bash
nmap --version
```

### 📝 Explanation

*   **`sudo`** — Run as administrator
*   **`apt install`** — Install a package
*   **`nmap`** — The tool name
*   **`--version`** — Show installed version

> [!TIP]
> If the version appears, that means **Nmap** is installed correctly.

## 8. First Basic Nmap Command

The most basic scan is:

```bash
nmap 192.168.1.10
```

This means **Nmap** will scan the target IP address `192.168.1.10`.

---

### What this does
This command checks:
*   **Whether the host is alive**
*   **Which common ports are open**
*   **What services may be running**

---

### 🟢 Beginner Understanding
This is usually the first step when you are given a target machine in a lab. You may not know anything about that machine, so the first question is:

> **“What is open on it?”**

This command helps answer that.


## 9. Understanding Basic Output

Suppose the output is:

```text
Starting Nmap 7.94
Nmap scan report for 192.168.1.10
Host is up.

PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
443/tcp  open  https
```

### Now let us understand this simply:

#### **Host is up**
This means the machine is active and responding.

#### **22/tcp open ssh**
This means:
*   **Port 22** is open
*   It uses **TCP**
*   **SSH service** is probably running

#### **80/tcp open http**
This means a **website** may be running.

#### **443/tcp open https**
This means a **secure website** may be running.

---

### 💡 What we learn from this
From just one scan, we now know:
*   The machine is **alive**
*   **Remote login** may be possible through SSH
*   A **website** is running
*   A **secure website** is also running

> [!TIP]
> That is why **Nmap** is so powerful.


## 10. Scanning a Website Name Instead of IP

**Nmap** can also scan a hostname or domain name.

### Example:
```bash
nmap example.com
```


This is useful when you know the website name, but not the IP address.

---

### 🔍 What happens
**Nmap** first finds the IP address of that domain, then scans it.

---

### 🟢 Beginner Example
Instead of typing an IP like:
```bash
nmap 93.184.216.34
```

You can simply type:

```bash
nmap example.com
```

This is easier for beginners.


## 11. Scanning More Than One Host

You can scan multiple systems together.

### Example:
```bash
nmap 192.168.1.10 192.168.1.20 192.168.1.30
```

This scans all three targets.

---

### ⏱️ Why this is useful

Suppose in your lab you have:
*   **One web server**
*   **One database server**
*   **One file server**

Instead of scanning them one by one, you can scan them all together. 

> [!TIP]
> This saves time.


## 12. Scanning a Range of IP Addresses

If you want to scan many nearby IPs, you can use a range.

### Example:
```bash
nmap 192.168.1.1-50
```

This means **Nmap** will scan:
*   `192.168.1.1`
*   `192.168.1.2`
*   `192.168.1.3`
*   ...
*   `192.168.1.50`

---

### 📡 Why this is useful

This helps when you do not know which systems are active in a network.

> [!TIP]
> For example, in a lab network, some machines may be **on** and some may be **off**. This command helps you check many systems quickly.


## 13. Scanning a Full Subnet

Sometimes you may want to scan a whole subnet.

### Example:
```bash
nmap 192.168.1.0/24
```

### ❓ What does /24 mean?
It means a full group of IP addresses in that network. Usually, this covers addresses like:
*   `192.168.1.1`
*   `192.168.1.2`
*   ...
*   `192.168.1.254`

---

### 📡 Why this is useful
This is useful for finding:
*   **Laptops** & **Desktops**
*   **Servers**
*   **Printers**
*   **IoT devices**
*   **Routers**

> [!TIP]
> Subnet scanning is essential for **network discovery**.


## 14. Host Discovery Only

Sometimes you do not want a full port scan. You only want to know which machines are alive.

For that, use:
```bash
nmap -sn 192.168.1.0/24
```

### 📝 Explanation

*   **`-sn`** — means only check which hosts are up.
*   It **does not** do a normal port scan.

---

### 🚀 Why this is useful

This is faster and cleaner when you first want to find active devices.

### 🟢 Beginner Understanding

This command answers:
> **“Which devices are alive in this network?”**

rather than:
> *“Which ports are open?”*


## 15. Scanning Specific Ports

Sometimes you only care about a few ports.

### Example:
```bash
nmap -p 22,80,443 192.168.1.10
```

### 📝 Explanation

*   **`-p`** — means port.
*   **`22,80,443`** — are the specific ports to scan.

This scans **only**:
*   Port **22**
*   Port **80**
*   Port **443**

---

### 🎯 Why this is useful
This is helpful when you want to quickly check known important services.

**For example:**
*   **22** for SSH
*   **80** for website
*   **443** for secure website


## 16. Scanning a Port Range

You can also scan a continuous range of ports.

### Example:
```bash
nmap -p 1-1000 192.168.1.10
``` 

This scans ports from **1 to 1000**.

---

### 🎯 Why this is useful

This gives more detail than a very small scan. It helps you find services running on lower-numbered common ports.


## 17. Scanning All Ports

By default, **Nmap** does not scan all 65,535 ports. If you want to scan every single port, use:

```bash
nmap -p- 192.168.1.10
```

### 📝 Explanation

*   **`-p-`** — means scan **all** 65,535 ports.

---

### 🎯 Why this matters

Sometimes a service may be running on an **unusual port**. A normal scan may miss it. A full port scan helps find **hidden** or **uncommon** services.

> [!NOTE]
> **Beginner note:** This scan is more complete, but it can take significantly more time to finish.


## 18. SYN Scan

A very common **Nmap** scan is the **SYN scan**.

### Example:
```bash
sudo nmap -sS 192.168.1.10
```


### 📝 Explanation

*   **`sudo`** — Administrator rights
*   **`-sS`** — SYN scan

---

### 💡 Simple Understanding

This scan is faster and commonly used by security professionals. It checks ports in a smart way without fully opening every connection.

> [!NOTE]  
> **Beginner note:** You do not need to deeply understand packet details right now. Just remember that **`-sS`** is one of the most popular Nmap scan types.


## 19. TCP Connect Scan

Another scan type is:

```bash
nmap -sT 192.168.1.10
```

### 📝 Explanation

*   **`-sT`** — TCP connect scan

---

### 🔍 What it does

This scan completes the **full TCP connection** (the three-way handshake).

---

### ⚖️ Difference from SYN scan

*   **SYN scan (`-sS`)** is more efficient and "stealthy."
*   **TCP connect scan (`-sT`)** is simpler.
*   **TCP connect scan** is often used when raw packet permissions (like root/sudo) are not available.

> [!NOTE]  
> **Beginner note:** For starting, just remember:  
> *   **`-sS`** = SYN scan  
> *   **`-sT`** = full TCP connect scan





