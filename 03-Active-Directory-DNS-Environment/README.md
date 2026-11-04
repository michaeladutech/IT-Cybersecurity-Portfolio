# Project 3: Active Directory & DNS Environment

For this project, I built a small Windows domain on my own PC using Hyper-V to learn the fundamentals of Active Directory and DNS, and how companies use them to manage users and computers.

## Lab Setup

| Component | Details |
|---|---|
| Hypervisor | Hyper-V |
| Domain Controller | `DC01` — Windows Server 2025 (192.168.1.5) |
| Client | `WIN11-01` — Windows 11 Pro (192.168.1.101) |
| Domain | `kojo.lab` |
| Network | Private virtual switch, separate from my home network |

<p align="center">
  <img width="60%" alt="Private virtual switch in Hyper-V" src="screenshots/01-private-switch.png" />
</p>

## Setting Up the Domain

I gave the server a static IP, installed the Active Directory Domain Services and DNS roles, and promoted it to a domain controller for `kojo.lab`.

In a company, the domain controller is the central place where all user accounts and computers are managed. Instead of creating a separate account on every computer, IT creates one account in Active Directory, and the employee can use it to sign in to any computer on the domain. The domain controller checks the username and password each time someone signs in. That's also why it needs a static IP: every computer on the network needs to be able to find it at the same address.

<p align="center">
  <img width="49%" alt="Server roles installed" src="screenshots/03-server-roles.png" />
  <img width="49%" alt="Domain verified with whoami and systeminfo" src="screenshots/04-domain-verified.png" />
</p>

## Users, Groups, and OUs

I created Organizational Units (OUs) to organize accounts, then added users and security groups.

OUs work like folders. Companies use them to organize accounts, for example by department, which makes accounts easier to find and manage.

Groups are used to control access. Instead of giving permissions to each person one at a time, IT gives permissions to a group, like Managers, and adds people to it. When someone joins or leaves a team, IT just adds them to or removes them from the group.

<p align="center">
  <img width="49%" alt="OU structure in Active Directory Users and Computers" src="screenshots/05-ou-structure.png" />
  <img width="49%" alt="User group membership" src="screenshots/06-group-membership.png" />
</p>

## DNS

DNS was set up along with the domain controller.

DNS turns names into IP addresses. When a computer wants to reach `kojo.lab`, it asks DNS for the IP address and then connects to it.

That's why domain computers need to use the domain controller for DNS. It's the DNS server that knows where `kojo.lab` is. The screenshot shows each computer's name matched to its IP address.

<p align="center">
  <img width="60%" alt="DNS forward lookup zone" src="screenshots/07-dns-forward-zone.png" />
</p>

## Joining a Computer to the Domain

I pointed the Windows 11 VM's DNS to the domain controller, tested it with `nslookup`, joined it to `kojo.lab`, and signed in as a domain user.

Joining a computer to the domain connects it to Active Directory, so IT can manage it and employees can sign in with their company account instead of a local one. Before joining, the computer needs to be able to find the domain controller, which is why I checked DNS with `nslookup` first. This is part of what IT does when setting up a new work computer.

<p align="center">
  <img width="49%" alt="nslookup resolving kojo.lab" src="screenshots/09-nslookup-working.png" />
  <img width="49%" alt="Signed in as a domain user" src="screenshots/10-domain-user-login.png" />
</p>

## Basic Account Management

I practiced resetting passwords and enabling and disabling user accounts in Active Directory.

These are some of the most common help desk tasks. Password resets happen when someone forgets their password or gets locked out. Accounts are disabled when an employee leaves, so they can no longer sign in, and new employees' accounts are enabled when they start.

<p align="center">
  <img width="49%" alt="Disabled account message at login" src="screenshots/11-account-disabled.png" />
  <img width="49%" alt="Password reset in Active Directory" src="screenshots/12-password-reset.png" />
</p>

## What I Learned

- How a domain controller, DNS, and domain-joined computers work together
- Why a domain controller needs a static IP
- Why domain computers need to use the domain controller for DNS
- How OUs, users, and groups are used to organize accounts

## Skills Practiced

Active Directory, DNS, domain controllers, users and groups, security groups, Organizational Units (OUs), account management, password resets, domain join, static IP addressing, Windows Server 2025, Windows 11, Hyper-V, virtual machines, virtual networking

---

[← Back to portfolio](../README.md)
