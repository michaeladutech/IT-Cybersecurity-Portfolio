# Project 3: Virtualization Environment — Active Directory & DNS Lab

A hands-on Windows domain environment built in Hyper-V to practice the identity, DNS, and help desk work done in real IT support and IAM roles.

## Overview

I built an isolated Active Directory domain (`kojo.lab`) on my own PC using Hyper-V. The lab includes a Windows Server 2025 domain controller with integrated DNS, a domain-joined Windows 11 Pro client, and an organized structure of OUs, users, and security groups. After building it, I worked through a set of help desk–style tickets to practice common support and access-management tasks, including delegating password resets with least privilege.

## Environment

| Component | Details |
|---|---|
| Hypervisor | Microsoft Hyper-V (Windows 11 Pro host) |
| Domain controller | `DC01`, Windows Server 2025 Standard (Desktop Experience) |
| Client | `WIN11-01`, Windows 11 Pro, domain-joined |
| Domain | `kojo.lab` (NetBIOS: `KOJO`) |
| Network | Private virtual switch `VM-LAN`, isolated from my home network |

## Network Plan

| Host | IP Address | Subnet Mask | DNS Server |
|---|---|---|---|
| DC01 | 192.168.1.5 (static) | 255.255.255.0 | 127.0.0.1 (itself) |
| WIN11-01 | 192.168.1.101 (static) | 255.255.255.0 | 192.168.1.5 (DC01) |

## What I Built

### Domain Controller
- Installed Windows Server 2025 and configured a static IP after diagnosing an APIPA (169.254.x.x) address on the private switch
- Installed the AD DS and DNS roles and promoted the server to a domain controller in a new forest (`kojo.lab`)
- Verified the domain with `whoami` and `systeminfo`

### DNS
- Reviewed the AD-integrated forward lookup zone, including A, NS, and SOA records
- Explored the SRV records clients use to find the domain controller (`_ldap` 389, `_kerberos` 88, `_kpasswd` 464, `_gc` 3268)
- Created a reverse lookup zone (`1.168.192.in-addr.arpa`) and PTR records, which fixed the nslookup "Server: UnKnown" message

### Users, Groups, and OUs
- Created OUs: `Employees`, `Management`, `IT Staff`, `Groups`
- Created domain users and security groups (`Managers`, `Help Desk`)
- Applied group-based access instead of assigning permissions to individual users

### Client
- Joined the Windows 11 client to the domain after verifying connectivity (`ping`) and name resolution (`nslookup`)
- Signed in as domain users and confirmed with `whoami`
- Renamed the domain-joined computer and confirmed the change in AD and in both DNS zones

## Help Desk Scenarios

| # | Ticket | What I Did |
|---|---|---|
| 1 | Account locked out | Unlocked the account in AD Users and Computers |
| 2 | Forgot password | Reset the password and set it to change at next logon |
| 3 | New hire starting Monday | Created the account disabled, confirmed login was blocked, then enabled it on the start date |
| 4 | User changed roles | Moved the user to the correct OU and removed old group access to prevent privilege creep |
| 5 | Group Policy not applying | Found the client's DNS pointed to 8.8.8.8; `gpupdate /force` showed name resolution errors; set DNS back to the DC |
| 6 | Computer renamed | Renamed the domain-joined PC; verified AD, forward, and reverse DNS updated automatically |
| 7 | DNS record deleted | Removed the client's A and PTR records, confirmed the failure, then restored both with `ipconfig /registerdns` |
| 8 | Help Desk delegation | Delegated "Reset password" on the Employees OU to the Help Desk group only; verified with Effective Access that resets are allowed for Employees and denied for Management and IT Staff |

## Troubleshooting & Lessons Learned

- **APIPA (169.254.x.x):** means a machine is set to DHCP but no DHCP server answered. Domain controllers need static IPs.
- **Clients must use the DC for DNS:** with DNS set to 8.8.8.8, the client couldn't locate the domain, and Group Policy failed with name resolution errors.
- **Cached credentials and broadcast fallbacks can hide DNS problems:** users could still sign in with bad DNS (cached credentials or NetBIOS on a single subnet), and `ping` found hosts through mDNS. Using the full name (`WIN11-01.kojo.lab`) and `ipconfig /flushdns` showed the real DNS failure.
- **Moving a user's OU doesn't change their access:** group memberships have to be cleaned up separately when someone changes roles.
- **"Access is denied" doesn't always mean the permission is missing:** `net user /domain` was denied for the Help Desk technician, but Effective Access confirmed the delegated right was in place. The tool used a different path than LDAP-based tools like AD Users and Computers.
- **Grant access to groups, not individual users:** I removed a direct permission I'd added for one technician so all access flows through the Help Desk group.

## Skills Practiced

Active Directory Domain Services, DNS (forward/reverse zones, A/PTR/SRV records), Organizational Units, security groups, user lifecycle (joiner-mover-leaver), password resets and account lockouts, delegation of control, least privilege, Effective Access, static IP addressing, Hyper-V virtual networking, `ipconfig`, `nslookup`, `ping`, `gpupdate`, `whoami`

## Screenshots

> Screenshots are in the [`screenshots`](screenshots/) folder. *(Coming soon)*

| Screenshot | Shows |
|---|---|
| `01-vm-lan-switch.png` | Private virtual switch in Hyper-V |
| `02-dc01-apipa.png` | DC01 with an APIPA address before configuration |
| `03-dc01-static-ip.png` | DC01 static IP and DNS settings |
| `04-domain-verified.png` | `whoami` and `systeminfo` showing KOJO.LAB |
| `05-forward-zone.png` | Forward lookup zone with A records |
| `06-srv-records.png` | SRV records for LDAP and Kerberos |
| `07-reverse-zone.png` | Reverse lookup zone with PTR records |
| `08-nslookup-before-after.png` | nslookup before and after the reverse zone |
| `09-ous-users-groups.png` | OU structure in AD Users and Computers |
| `10-domain-join.png` | Client joined to kojo.lab |
| `11-gpupdate-dns-failure.png` | Group Policy failing with bad DNS |
| `12-delegation-effective-access.png` | Effective Access showing Reset password allowed |

## Next Steps

- Install RSAT on the client and perform delegated password resets as a Help Desk user
- Group Policy and file share permissions labs
- Configure a DHCP scope
- Build a self-hosted ticketing system (osTicket) connected to the domain

---

[← Back to portfolio](../README.md)
