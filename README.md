
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

<img width="1470" height="956" alt="Screenshot 2026-10-05 at 8 21 05 PM" src="https://github.com/user-attachments/assets/ea79aedb-bf66-466b-9aa6-e2483f4416e3" />
---

## Step 3: Create a Forward Lookup Zone

In DNS Manager, I created a new **Primary Forward Lookup Zone** named:

```text
davidlab.local
```

This zone allows my DNS server to manage DNS records for the lab environment.

<img width="1470" height="956" alt="Screenshot 2026-10-05 at 8 20 21 PM" src="https://github.com/user-attachments/assets/8ed9c02d-9918-498c-920e-f653f4e264a5" />


---

## Step 4: Create DNS A Records

I created two DNS A records:

```text
server01.davidlab.local
fileserver.davidlab.local
```

Both records point to the private IPv4 address of my Windows Server.

<img width="1470" height="956" alt="Screenshot 2026-10-06 at 4 26 50 PM" src="https://github.com/user-attachments/assets/a6bb3635-4dac-4a8c-86cd-4e26841e38a5" />


---

## Step 5: Configure the Windows 10 Client

I configured my Windows 10 Enterprise VM to use the **Windows Server's private IP address as its Preferred DNS Server**.

I verified the configuration with:

```cmd
ipconfig /all
```

<img width="1470" height="956" alt="Screenshot 2026-10-06 at 4 30 40 PM" src="https://github.com/user-attachments/assets/49f6365f-83c6-4190-96ed-3f05b8cf5f04" />

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

<img width="1470" height="956" alt="Screenshot 2026-10-06 at 4 34 12 PM" src="https://github.com/user-attachments/assets/365a7adc-4a83-4b11-a5e3-852851b08f08" />
---

## Step 7: DNS Troubleshooting

To simulate a DNS issue, I temporarily configured the Windows 10 client with an incorrect DNS server.

<img width="1470" height="956" alt="Screenshot 2026-10-06 at 4 43 13 PM" src="https://github.com/user-attachments/assets/bb1003d5-e698-4f06-8a9e-d0fca74f1354" />


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

<img width="1470" height="956" alt="Screenshot 2026-10-06 at 4 39 42 PM" src="https://github.com/user-attachments/assets/d0f071b6-0a89-48a7-b502-6be4c5631809" />

---


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

