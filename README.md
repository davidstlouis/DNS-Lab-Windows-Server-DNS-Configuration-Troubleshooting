# Windows Server DNS Lab

## Project Overview

In this lab, I configured a basic **DNS environment** using Windows Server 2022 and Windows 10 Enterprise virtual machines in Microsoft Azure.

The goal was to configure a DNS server, create DNS records, connect a Windows client to the DNS server, and troubleshoot DNS resolution.

## Technologies Used

- Microsoft Azure
- Windows Server 2022
- Windows 10 Enterprise
- DNS Manager
- Command Prompt

## Lab Setup

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

## 1. Install DNS Server

On Windows Server 2022, I installed the **DNS Server** role using Server Manager.

```text
Server Manager
→ Manage
→ Add Roles and Features
→ DNS Server
→ Install
```

## 2. Create DNS Zone

Using DNS Manager, I created a new Primary Forward Lookup Zone:

```text
davidlab.local
```

I then created DNS A records:

```text
server01.davidlab.local → Server IP Address
fileserver.davidlab.local → Server IP Address
```

## 3. Configure Windows 10

I configured the Windows 10 VM to use the private IP address of my Windows Server as its **Preferred DNS Server**.

I verified the configuration with:

```cmd
ipconfig /all
```

## 4. Test DNS

I cleared the DNS cache:

```cmd
ipconfig /flushdns
```

Then tested name resolution:

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

## Troubleshooting

I simulated a DNS problem by configuring the client with an incorrect DNS server.

I used:

```cmd
ipconfig /all
nslookup server01.davidlab.local
```

After identifying the incorrect DNS configuration, I changed the client back to the correct DNS server and ran:

```cmd
ipconfig /flushdns
nslookup server01.davidlab.local
```

The hostname successfully resolved to the correct IP address.

## Skills Demonstrated

- Windows Server Administration
- DNS Configuration
- DNS A Records
- TCP/IP Networking
- Microsoft Azure
- `nslookup`
- `ipconfig`
- Network Troubleshooting
