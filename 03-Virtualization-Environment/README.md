# Project 3: Virtualization Environment — Active Directory & DNS Lab

For this project, I built a small Windows domain on my own PC using Hyper-V. I wanted hands-on practice with Active Directory and DNS, since they're used in almost every company and show up constantly in help desk work.

## Lab Goals

- Set up a Windows Server domain controller with Active Directory and DNS
- Organize users and computers the way a small company might
- Join a Windows 11 computer to the domain and sign in with domain accounts
- Practice everyday help desk tasks like password resets and account changes

## Lab Setup

| Component | Details |
|---|---|
| Hypervisor | Hyper-V on my Windows 11 Pro PC |
| Domain Controller | `DC01` — Windows Server 2025 Standard (Desktop Experience), 4 GB RAM |
| Client | `WIN11-01` — Windows 11 Pro |
| Domain | `kojo.lab` (short name: `KOJO`) |
| Network | Private virtual switch (`192.168.1.0/24`), separate from my home network |

| Machine | IP Address | Subnet Mask | DNS Server |
|---|---|---|---|
| DC01 | 192.168.1.5 (static) | 255.255.255.0 | Itself (127.0.0.1) |
| WIN11-01 | 192.168.1.101 (static) | 255.255.255.0 | DC01 (192.168.1.5) |

## Building the Lab

### 1. Setting Up the Network

I created a **private virtual switch** in Hyper-V. With a private switch, the lab VMs can talk to each other, but they can't reach my home network or the internet. That keeps the lab separate from the other devices in my house.

<p align="center">
  <img width="60%" alt="Private virtual switch in Hyper-V" src="screenshots/01-private-switch.png" />
</p>

On the private switch, the server first got a `169.254.x.x` address. Windows gives itself this kind of address (called APIPA) when it's set to get an IP automatically but there's no DHCP server to give it one. Domain controllers should have an address that doesn't change, since every computer on the domain points to it, so I gave it a static IP of `192.168.1.5` and set its DNS to itself.

<p align="center">
  <img width="60%" alt="DC01 with a 169.254 APIPA address" src="screenshots/02-dc01-apipa-address.png" />
</p>

### 2. Creating the Domain

1. Installed Windows Server 2025 with the Desktop Experience (the version with a GUI).
2. Renamed the server to `DC01` and set its static IP.
3. Used **Add Roles and Features** in Server Manager to install **Active Directory Domain Services (AD DS)** and **DNS**. I also installed the DHCP role to set up in a later lab.
4. Promoted the server to a **domain controller**, creating a new forest with the domain `kojo.lab`.
5. After the restart, signed in as `KOJO\Administrator` and confirmed the domain with `whoami` and `systeminfo`.

<p align="center">
  <img width="49%" alt="Server roles installed" src="screenshots/03-server-roles.png" />
  <img width="49%" alt="Domain verified with whoami and systeminfo" src="screenshots/04-domain-verified.png" />
</p>

### 3. Users, Groups, and OUs

In **Active Directory Users and Computers**, I set up Organizational Units (OUs) to organize accounts like a small company would:

| OU | What's in it |
|---|---|
| **Employees** | Regular staff user accounts |
| **Management** | Manager accounts |
| **IT Staff** | Help desk technician accounts |
| **Groups** | Security groups like `Managers` and `Help Desk` |

The difference I learned between the two:
- **OUs** are like folders. They organize accounts and are where Group Policy gets applied.
- **Security groups** control what people can access. Permissions are given to the group, and users get access by being added to it.

I created user accounts in each OU and added users to the groups that matched their roles.

<p align="center">
  <img width="49%" alt="OU structure in Active Directory Users and Computers" src="screenshots/05-ou-structure.png" />
  <img width="49%" alt="User group membership" src="screenshots/06-group-membership.png" />
</p>

### 4. DNS

DNS was set up automatically when the server became a domain controller. Active Directory depends on DNS, because computers use it to find the domain controller.

In **DNS Manager**, I looked at:
- **Forward lookup zone (`kojo.lab`):** turns names into IP addresses. It has **A records** for `DC01` and `WIN11-01`. The client added its own record automatically when it joined the domain.
- **Reverse lookup zone (`1.168.192.in-addr.arpa`):** turns IP addresses back into names using **PTR records**. This one wasn't created automatically, so I added it myself. Afterward, `nslookup` showed the DNS server's name (`dc01.kojo.lab`) instead of "UnKnown."

<p align="center">
  <img width="49%" alt="DNS forward lookup zone" src="screenshots/07-dns-forward-zone.png" />
  <img width="49%" alt="DNS reverse lookup zone" src="screenshots/08-dns-reverse-zone.png" />
</p>

### 5. Joining the Client to the Domain

1. Connected the Windows 11 VM to the private switch.
2. Set a static IP of `192.168.1.101` and pointed its DNS to the domain controller (`192.168.1.5`).
3. Tested with `ping` and `nslookup kojo.lab` to make sure the client could reach the server and find the domain.
4. Joined the computer to `kojo.lab` using the domain administrator account, then restarted.
5. Signed in as a domain user and confirmed it with `whoami`.

<p align="center">
  <img width="49%" alt="nslookup resolving kojo.lab" src="screenshots/09-nslookup-working.png" />
  <img width="49%" alt="Signed in as a domain user" src="screenshots/10-domain-user-login.png" />
</p>

## Help Desk Practice

Once the domain was working, I practiced some common help desk tasks:

| Task | What I Did |
|---|---|
| **Locked out / disabled account** | Unlocked and re-enabled user accounts in Active Directory Users and Computers. |
| **Forgot password** | Reset a user's password and checked **User must change password at next logon**, so the user picks their own password after signing in. |
| **New hire** | Created an account that was disabled until the user's start date, confirmed they couldn't sign in, then enabled it. |
| **User changed roles** | Moved the user to the correct OU and removed them from the group they no longer needed, so they didn't keep their old access. |
| **Renaming a computer** | Renamed the domain-joined PC to `WIN11-01` and checked that the new name showed up in Active Directory and DNS. |

<p align="center">
  <img width="49%" alt="Disabled account message at login" src="screenshots/11-account-disabled.png" />
  <img width="49%" alt="Password reset in Active Directory" src="screenshots/12-password-reset.png" />
</p>

### Why the DNS Setting Matters

To understand why domain computers need to use the domain controller for DNS, I tried changing the client's DNS to `8.8.8.8` (Google's public DNS). Google's DNS doesn't know anything about `kojo.lab`, so `nslookup` couldn't find the domain and `gpupdate /force` failed because the client couldn't find the domain controller. Setting DNS back to `192.168.1.5` got everything working again.

<p align="center">
  <img width="49%" alt="gpupdate failing with wrong DNS" src="screenshots/13-gpupdate-dns-failure.png" />
  <img width="49%" alt="gpupdate working after fixing DNS" src="screenshots/14-gpupdate-fixed.png" />
</p>

### Delegating Password Resets

Help desk staff usually aren't full admins. They only get the permissions they need for their job. To practice this, I:

1. Created a **Help Desk** security group and added the IT Staff users to it.
2. Ran the **Delegation of Control Wizard** on the **Employees** OU.
3. Gave the Help Desk group only one task: **Reset user passwords and force password change at next logon**.

Help Desk members can reset passwords for regular employees, but not for managers or other IT staff, and they don't have admin rights. I checked this with the **Effective Access** tab in Active Directory.

<p align="center">
  <img width="60%" alt="Delegation of Control Wizard" src="screenshots/15-delegation-wizard.png" />
</p>

## What I Learned

- A domain controller should have a static IP, and a `169.254` address means the computer didn't get an address from DHCP.
- Domain computers need to use the domain controller for DNS, since that's how they find it.
- Forward lookup zones turn names into IPs, and reverse lookup zones turn IPs into names.
- OUs organize accounts, while groups control what people can access.
- When someone changes roles, their old access needs to be removed too.
- It's better to give permissions to groups instead of individual users, and only give people the access they need.

## Skills Practiced

Active Directory Domain Services, DNS (forward and reverse lookup zones), Organizational Units, users and security groups, password resets, account management, delegation of control, static IP addressing, Hyper-V, `ipconfig`, `nslookup`, `ping`, `gpupdate`, `whoami`

## Next Steps

- Group Policy and shared folder permissions
- DHCP
- A help desk ticketing system connected to the domain

---

[← Back to portfolio](../README.md)
