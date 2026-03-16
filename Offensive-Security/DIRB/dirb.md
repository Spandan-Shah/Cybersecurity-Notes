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

### Open the hosts file:

```bash
sudo nano /etc/hosts
```

**What this file is:**

`/etc/hosts` is a local file in Linux used to connect hostnames with IP addresses.


### Add a new line like this at the bottom:
`10.10.10.10 fakebank.thm`

**Important:**

* Replace `10.10.10.10` with the actual IP address of your target machine
* Keep one space between IP and hostname
* Do not add extra symbols

markdown
**Example:**
```text
127.0.0.1       localhost
127.0.1.1       kali

10.10.10.10     fakebank.thm
```

**Save the file in nano:**

* Press **Ctrl + O**
* Press **Enter**
* Press **Ctrl + X**

**Test again:**
```bash
ping -c 4 fakebank.thm
```

If ping now works, hostname resolution is fixed.


### Step 7: Open the Website in Kali Browser

Now open Firefox in Kali Linux.

In the address bar type:
`http://fakebank.thm`

**What you should see:**
* The banking website home page
* Login page or account page
* The target website should load normally

**If the page opens:**
Good. That means:
* Browser can reach the target
* Hostname mapping is correct
* You are ready to scan

**If the page does not open:**
Check these things:
* Target machine is running
* VPN or lab network is connected
* `/etc/hosts` entry is correct
* Hostname spelling is correct
* IP address is correct

### Step 8: Log In to the Website Normally First

Before doing the hidden page discovery, log in as a normal user if credentials are provided.

**Why this matters:**

You should understand what pages are visible to a regular user before searching for hidden ones.

**Look for:**

* Account number
* Current balance
* Menu options
* What pages are available normally

**Important:**

Note down your bank account number.

**Example:**

`8881`

You will need it later when using the hidden deposit page.


### Step 9: Open Kali Terminal for Scanning

Now open Terminal in Kali Linux.

**You can do this by:**

* Clicking terminal icon
* Or pressing **Ctrl + Alt + T**

This terminal is where you will run `dirb`.


### Step 10: Run the Basic dirb Scan

Now type:

```bash
dirb http://fakebank.thm
```

**What this command means:**

* **dirb** = the tool
* **http://fakebank.thm** = the target website

Since no wordlist is manually given here, dirb will use its default wordlist.


### Step 11: Wait for the Scan to Complete

After running the command, `dirb` will start testing many common directory and page names one by one.

**Examples of names it may test:**

* `/admin`
* `/images`
* `/login`
* `/config`
* `/backup`
* `/deposit`

**What dirb is doing internally:**

It is sending HTTP requests to many possible paths and checking which ones give meaningful responses.

### Step 12: Read the Output Carefully

You may see output like this:

```text
-----------------
DIRB v2.22
By The Dark Raver
-----------------

START_TIME: Thu Apr 17 16:29:52 2025
URL_BASE: http://fakebank.thm/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt

-----------------

GENERATED WORDS: 4610

---- Scanning URL: http://fakebank.thm/ ----
+ http://fakebank.thm/bank-deposit (CODE:200|SIZE:4663)
+ http://fakebank.thm/images (CODE:301|SIZE:179)

-----------------
END_TIME: Thu Apr 17 16:29:59 2025
DOWNLOADED: 4610 - FOUND: 2
```

### Step 13: Understand Each Part of the Output

#### 1. Tool version
`DIRB v2.22`

This is simply the installed version of dirb.

#### 2. Start time
`START_TIME: Thu Apr 17 16:29:52 2025`

This shows when the scan started.

#### 3. URL base
`URL_BASE: http://fakebank.thm/`

This tells you which target website is being scanned.

#### 4. Wordlist file
`WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt`

This tells you which wordlist is being used.

A wordlist is simply a file containing many common file and directory names.

#### 5. Generated words
`GENERATED WORDS: 4610`

This means dirb will try 4610 possible names.

#### 6. Scanning results
`+ http://fakebank.thm/bank-deposit (CODE:200|SIZE:4663)`  
`+ http://fakebank.thm/images (CODE:301|SIZE:179)`

These are the important findings.

### Step 14: Understand the Meaning of Result Codes

**CODE:200**

This means:

* The page exists
* It is accessible
* You can open it directly

**Example:**

`http://fakebank.thm/bank-deposit`
This is a strong result.

**CODE:301**

This means:

* The path exists
* It redirects to another location

**Example:**

`http://fakebank.thm/images`

This still means the page or folder is real.

**SIZE**
This tells the size of the response body.

*   **Example:** `SIZE:4663`
*   **Purpose:** This can help compare pages and identify false positives.


### Step 15: Identify the Hidden URLs Properly

From the output, two hidden URLs were found:

* http://fakebank.thm
* http://fakebank.thm

Now for the practical, the important page is:

**http://fakebank.thm**

Because this page gives access to a hidden function.

### Step 16: Open the Hidden Page in the Browser

Now go back to Firefox in Kali.

In the address bar type:

`http://fakebank.thm/bank-deposit`

and press Enter.


### What you should see:

A page that allows money to be deposited into a bank account.

This page was hidden from normal navigation, but **dirb** found it.

**This is the main concept of the practical:**
Hidden URLs may expose sensitive functionality.


### Step 17: Enter the Account Number

On the deposit page, you will usually see fields like:

* Account number
* Deposit amount

Now enter your account number.

**Example:**
`8881`

Make sure you type the correct account number that belongs to your login.


### Step 18: Enter the Deposit Amount

In the amount field, enter:

`2000`

You can enter the required amount according to the practical.

Then click the **deposit** or **submit** button.


### Step 19: Read the Deposit Receipt

After submission, a receipt or confirmation page may appear.

This usually confirms:

* Account number
* Amount added
* Whether the transaction succeeded

Read the details carefully.

### Step 20: Return to the Account Page

On the receipt page, click:

**Return to Your Account**

This will take you back to your account overview page.

### Step 21: Confirm Whether Balance Has Changed

Now check the account balance.

If the hidden deposit page worked, the balance should have increased.

**For example:**

* Old balance may have been negative.
* After adding `2000`, the balance may become positive.

This proves the hidden page performed a sensitive action.
















