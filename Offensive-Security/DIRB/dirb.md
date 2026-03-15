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