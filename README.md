# Windows Server DNS Configuration & Troubleshooting Lab

## Project Overview

In this lab, I configured a **DNS server using Windows Server 2022** and connected a **Windows 10 Enterprise client** to it in Microsoft Azure.

I created a custom DNS zone, added DNS records, tested name resolution, and simulated a DNS issue to practice troubleshooting.

## Technologies Used

- Microsoft Azure
- Windows Server 2022 Datacenter: Azure Edition
- Windows 10 Enterprise
- DNS Manager
- Command Prompt
- TCP/IP & DNS

---

## Lab Environment

```text
Windows 10 Enterprise
      CLIENT01
          |
          | DNS Request
          v
Windows Server 2022
      SERVER01
          |
          v
    davidlab.local
```

---

## Step 1: Server Network Configuration

I used `ipconfig` to identify the private IPv4 address of my Windows Server.


```cmd
ipconfig
```


<img width="1470" height="956" alt="Screenshot 2026-10-05 at 8 08 08 PM" src="https://github.com/user-attachments/assets/7bc8248b-f39f-442b-a515-2698f6bfa090" />

---

## Step 2: Install DNS Server

Using **Server Manager**, I installed the DNS Server role on Windows Server 2022.

```text
Server Manager
→ Manage
→ Add Roles and Features
→ DNS Server
→ Install
```

I then opened **DNS Manager** to begin configuring the server.

### Screenshot
<!-- Drag your DNS Manager screenshot below this line -->


---

## Step 3: Create a Forward Lookup Zone

I created a new **Primary Forward Lookup Zone** named:

```text
davidlab.local
```

This zone allows my DNS server to resolve hostnames within my lab environment.

### Screenshot
<!-- Drag your Forward Lookup Zone screenshot below this line -->


---

## Step 4: Create DNS A Records

I created two DNS A records:

```text
server01.davidlab.local
fileserver.davidlab.local
```

Both records point to the private IPv4 address of my Windows Server.

### Screenshot
<!-- Drag your DNS records screenshot below this line -->


---

## Step 5: Configure the Windows 10 Client

I configured the Windows 10 VM to use the **Windows Server's private IP address as its Preferred DNS Server**.

I verified the configuration using:

```cmd
ipconfig /all
```

### Screenshot
<!-- Drag your Windows 10 DNS configuration screenshot below this line -->


---

## Step 6: Test DNS Resolution

I cleared the Windows DNS cache:

```cmd
ipconfig /flushdns
```

Then I tested both DNS records:

```cmd
nslookup server01.davidlab.local
```

```cmd
nslookup fileserver.davidlab.local
```

I also tested hostname resolution with:

```cmd
ping server01.davidlab.local
```

The client successfully resolved the hostname to the correct server IP address.

### Screenshot
<!-- Drag your successful nslookup screenshot below this line -->


---

## Step 7: DNS Troubleshooting

To practice troubleshooting, I intentionally configured the Windows 10 client with an incorrect DNS server.

I then used:

```cmd
ipconfig /all
```

and:

```cmd
nslookup server01.davidlab.local
```

to identify the DNS issue.

After finding the incorrect DNS configuration, I restored the correct DNS server and cleared the DNS cache:

```cmd
ipconfig /flushdns
```

I tested the DNS record again:

```cmd
nslookup server01.davidlab.local
```

The hostname successfully resolved after correcting the DNS configuration.

### Screenshot
<!-- Drag your troubleshooting screenshot below this line -->


---

## Skills Demonstrated

- Windows Server Administration
- DNS Server Configuration
- DNS A Records
- Forward Lookup Zones
- Microsoft Azure
- TCP/IP Networking
- Windows Client Configuration
- `nslookup`
- `ipconfig`
- DNS Troubleshooting
- Network Troubleshooting

---

## What I Learned

This lab helped me understand how DNS translates hostnames into IP addresses and how Windows clients communicate with DNS servers.

I also gained hands-on experience using tools such as `nslookup` and `ipconfig` to identify and resolve DNS configuration issues.

---


