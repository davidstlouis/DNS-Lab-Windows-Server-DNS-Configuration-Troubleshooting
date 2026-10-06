# Windows Server DNS Configuration & Troubleshooting Lab

## Project Overview

In this lab, I configured a **DNS environment using Windows Server 2022** and a **Windows 10 Enterprise client** in Microsoft Azure.

I created a DNS zone, added DNS records, configured the Windows client to use my DNS server, tested name resolution, and practiced basic DNS troubleshooting.

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

## Step 1: Verify Server Network Configuration

I used `ipconfig` to identify the private IPv4 address of my Windows Server.

```cmd
ipconfig
```

<img width="1470" height="956" alt="Screenshot 2026-10-05 at 8 08 08 PM" src="https://github.com/user-attachments/assets/7bc8248b-f39f-442b-a515-2698f6bfa090" />
---

## Step 2: Verify DNS Server

The DNS Server role was already installed on my Windows Server 2022 VM.

I opened **DNS Manager** through:

```text
Server Manager
→ Tools
→ DNS
```

I verified that the DNS service was available before beginning the DNS configuration.

### Screenshot
<!-- Drag your DNS Manager screenshot here -->

---

## Step 3: Create a Forward Lookup Zone

In DNS Manager, I created a new **Primary Forward Lookup Zone** named:

```text
davidlab.local
```

This zone allows my DNS server to manage DNS records for the lab environment.

### Screenshot
<!-- Drag your Forward Lookup Zone screenshot here -->

---

## Step 4: Create DNS A Records

I created two DNS A records:

```text
server01.davidlab.local
fileserver.davidlab.local
```

Both records point to the private IPv4 address of my Windows Server.

### Screenshot
<!-- Drag your DNS records screenshot here -->

---

## Step 5: Configure the Windows 10 Client

I configured my Windows 10 Enterprise VM to use the **Windows Server's private IP address as its Preferred DNS Server**.

I verified the configuration with:

```cmd
ipconfig /all
```

### Screenshot
<!-- Drag your Windows 10 DNS configuration screenshot here -->

---

## Step 6: Test DNS Resolution

I cleared the client's DNS cache:

```cmd
ipconfig /flushdns
```

I then tested both DNS records:

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

The Windows 10 client successfully resolved the hostname to the correct server IP address.

### Screenshot
<!-- Drag your successful nslookup screenshot here -->

---

## Step 7: DNS Troubleshooting

To simulate a DNS issue, I temporarily configured the Windows 10 client with an incorrect DNS server.

I checked the client's configuration with:

```cmd
ipconfig /all
```

I then tested DNS resolution:

```cmd
nslookup server01.davidlab.local
```

After identifying the incorrect DNS server configuration, I restored the correct DNS server and cleared the DNS cache:

```cmd
ipconfig /flushdns
```

I tested the DNS record again:

```cmd
nslookup server01.davidlab.local
```

The hostname successfully resolved after correcting the DNS configuration.

### Screenshot
<!-- Drag your troubleshooting screenshot here -->

---

## Skills Demonstrated

- Windows Server Administration
- DNS Configuration
- Forward Lookup Zones
- DNS A Records
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

I also gained hands-on experience using `nslookup` and `ipconfig` to identify and resolve DNS configuration issues.

---

