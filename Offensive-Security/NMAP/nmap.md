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









