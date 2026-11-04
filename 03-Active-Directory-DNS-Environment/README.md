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

In a company, the domain controller is the central place where all user accounts and computers are managed, so people can sign in to any work computer with the same account.

<p align="center">
  <img width="49%" alt="Server roles installed" src="screenshots/03-server-roles.png" />
  <img width="49%" alt="Domain verified with whoami and systeminfo" src="screenshots/04-domain-verified.png" />
</p>

## Users, Groups, and OUs

I created Organizational Units (OUs) to organize accounts, then added users and security groups.

Companies use OUs to organize accounts by department, and groups to control access. For example, giving everyone in a Managers group access to the same files instead of setting it up one person at a time.

<p align="center">
  <img width="49%" alt="OU structure in Active Directory Users and Computers" src="screenshots/05-ou-structure.png" />
  <img width="49%" alt="User group membership" src="screenshots/06-group-membership.png" />
</p>

## DNS

DNS was set up along with the domain controller.

DNS turns names into IP addresses. In a domain, computers use it to find the domain controller, which is why each computer's DNS needs to point to it.

<p align="center">
  <img width="60%" alt="DNS forward lookup zone" src="screenshots/07-dns-forward-zone.png" />
</p>

## Joining a Computer to the Domain

I pointed the Windows 11 VM's DNS to the domain controller, tested it with `nslookup`, joined it to `kojo.lab`, and signed in as a domain user.

This is what IT does when setting up a new work computer, so the employee can sign in with their company account.

<p align="center">
  <img width="49%" alt="nslookup resolving kojo.lab" src="screenshots/09-nslookup-working.png" />
  <img width="49%" alt="Signed in as a domain user" src="screenshots/10-domain-user-login.png" />
</p>

## Basic Account Management

I practiced resetting passwords and enabling and disabling user accounts in Active Directory.

These are some of the most common help desk tasks, like when someone forgets their password, a new employee starts, or someone leaves the company.

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

Active Directory, DNS, users and groups, OUs, password resets, static IP addressing, Hyper-V, `nslookup`, `whoami`

---

[← Back to portfolio](../README.md)
