# Practical Session: Finding Hidden Pages Using `dirb`

## Aim

To understand how hidden website pages can be discovered using the `dirb` tool and how such pages may expose sensitive functionality.

---

## Basic Idea

To outsmart a hacker, you need to think like one.

This is the core idea of **Offensive Security**. In this approach, we simulate the actions of an attacker in order to find weaknesses in systems, websites, and applications. The purpose is not to harm the system, but to understand how attacks happen and then improve security defenses.

In a safe lab environment, we can practice these techniques legally and learn how ethical hackers identify hidden features that normal users are not supposed to access.

---

## Objective of This Practical

In this practical, the goal is to examine a sample banking website and identify hidden pages that are not visible through normal navigation.

Sometimes, web applications contain secret or unlinked URLs that provide sensitive functions. If such URLs are discovered, they may allow unauthorized actions. One common way to find these hidden paths is by using a brute-force content discovery tool such as `dirb`.

---

## Tool Used

### `dirb`

`dirb` is a web content scanner used to discover hidden directories and pages on a website.

It works by:
- taking a target website URL
- using a predefined wordlist
- testing many possible page names one by one
- checking which pages actually exist

This is possible because developers often use predictable names for web pages and folders.

---

## Requirement

- A running lab website target
- Terminal access
- `dirb` installed
- Browser access to open discovered pages

---

# Installation on Kali Linux

### Step 1: Update package list

Open the Kali terminal and run:
`sudo apt update`  
This refreshes the package index before installation.

### Step 2: Install dirb

Run:
`sudo apt install dirb`  
Kali’s official tools page lists this as the installation command for dirb.

### Step 3: Verify installation
Run:
`dirb`  
If installed correctly, the tool will display its banner and usage information.

# Practical Setup on Kali Linux

### Step 4: Open the lab website in your browser

Open the target website in Firefox or another browser on Kali.

**Example target:**  
`http://fakebank.thm`

If the page opens correctly in the browser, your lab target is reachable.

If it does not open, the issue is usually one of these:
* The lab machine is not started
* Your VPN is not connected
* The target hostname is not resolving
* Kali cannot reach the lab network

### Step 5: Check Whether the Target Hostname Resolves Properly

Before using dirb, you must confirm that your Kali machine can actually identify and reach the target website name.

Here the target name is:

`fakebank.thm`

When you type this in browser or terminal, Kali must know which IP address belongs to this name.

Run this command:
```bash
ping -c 4 fakebank.thm
```

**What this command does:**

*   **ping** checks network connectivity
*   **-c 4** means send only 4 packets
*   **fakebank.thm** is the hostname we want to test

### If everything is working correctly:

You will get output similar to this:

```text
PING fakebank.thm (10.10.10.10) 56(84) bytes of data.
64 bytes from fakebank.thm (10.10.10.10): icmp_seq=1 ttl=64 time=10.2 ms
64 bytes from fakebank.thm (10.10.10.10): icmp_seq=2 ttl=64 time=11.1 ms
64 bytes from fakebank.thm (10.10.10.10): icmp_seq=3 ttl=64 time=10.5 ms
64 bytes from fakebank.thm (10.10.10.10): icmp_seq=4 ttl=64 time=9.8 ms
```

**This means:**

* The hostname is resolving properly
* The target machine is reachable
* You can move to the next step

### If it does not work:

You may see errors like:

`ping: fakebank.thm: Name or service not known`

or

`Temporary failure in name resolution`

**This means:**
Kali cannot convert `fakebank.thm` into an IP address.

Then you need to manually add the hostname in `/etc/hosts`.


### Step 6: Manually Add the Target in /etc/hosts If Needed

If `fakebank.thm` is not resolving, you need to map it manually.

**Why this step is needed:**

* Sometimes lab websites do not exist on public DNS.
* So Kali does not know where `fakebank.thm` points unless you tell it manually.