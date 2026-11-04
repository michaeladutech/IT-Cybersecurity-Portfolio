# Project 3: Virtualization Environment — Active Directory & DNS Lab

For this project, I built a small Windows domain on my own PC using Hyper-V. I wanted hands-on practice with Active Directory and DNS, since they're used in almost every company and show up constantly in help desk work.

## Lab Setup

| Component | Details |
|---|---|
| Hypervisor | Hyper-V on my Windows 11 Pro PC |
| Domain Controller | `DC01` — Windows Server 2025 |
| Client | `WIN11-01` — Windows 11 Pro |
| Domain | `kojo.lab` |
| Network | Private virtual switch, separate from my home network |

| Machine | IP Address | DNS Server |
|---|---|---|
| DC01 | 192.168.1.5 | Itself (127.0.0.1) |
| WIN11-01 | 192.168.1.101 | DC01 (192.168.1.5) |

## Building the Lab

### Setting Up the Network

I created a private virtual switch in Hyper-V so the lab VMs could talk to each other but stay isolated from my home network.

<p align="center">
  <img width="60%" alt="Private virtual switch in Hyper-V" src="screenshots/01-private-switch.png" />
</p>

After moving the server onto the private switch, it showed a `169.254.x.x` address. That happens when a computer is set to get an IP automatically but there's no DHCP server to give it one. Since a domain controller needs an address that never changes, I gave it a static IP of `192.168.1.5`.

<p align="center">
  <img width="60%" alt="DC01 with a 169.254 APIPA address" src="screenshots/02-dc01-apipa-address.png" />
</p>

### Creating the Domain

I installed the Active Directory Domain Services and DNS roles on the server, then promoted it to a domain controller for a new domain called `kojo.lab`. I confirmed it worked with `whoami` and `systeminfo`.

<p align="center">
  <img width="49%" alt="Server roles installed" src="screenshots/03-server-roles.png" />
  <img width="49%" alt="Domain verified with whoami and systeminfo" src="screenshots/04-domain-verified.png" />
</p>

### Users, Groups, and OUs

I set up Organizational Units (OUs) to organize accounts like a small company would: **Employees**, **Management**, **IT Staff**, and **Groups**. Then I created user accounts and security groups, and added users to the groups that matched their roles.

<p align="center">
  <img width="49%" alt="OU structure in Active Directory Users and Computers" src="screenshots/05-ou-structure.png" />
  <img width="49%" alt="User group membership" src="screenshots/06-group-membership.png" />
</p>

### DNS

DNS was set up automatically when the server became a domain controller. I looked through the records to see how computers on the domain are listed by name and IP address. I also created a reverse lookup zone so DNS works both ways (name to IP and IP to name).

<p align="center">
  <img width="49%" alt="DNS forward lookup zone" src="screenshots/07-dns-forward-zone.png" />
  <img width="49%" alt="DNS reverse lookup zone" src="screenshots/08-dns-reverse-zone.png" />
</p>

### Joining the Client to the Domain

On the Windows 11 VM, I set a static IP and pointed its DNS to the domain controller. I tested it with `nslookup`, joined the computer to `kojo.lab`, and signed in as a domain user.

<p align="center">
  <img width="49%" alt="nslookup resolving kojo.lab" src="screenshots/09-nslookup-working.png" />
  <img width="49%" alt="Signed in as a domain user" src="screenshots/10-domain-user-login.png" />
</p>

## Help Desk Practice

Once the domain was working, I practiced common help desk tickets:

- **Locked out / disabled accounts:** Unlocked and re-enabled user accounts in Active Directory.
- **Forgot password:** Reset a user's password from Active Directory.
- **New hire:** Created an account that stayed disabled until the user's start date, then enabled it.
- **User changed roles:** Moved the user to the correct OU and removed group access they no longer needed.
- **Computer renamed / DNS record missing:** Confirmed DNS updated after renaming the PC, and used `ipconfig /registerdns` to bring back a deleted record.

<p align="center">
  <img width="49%" alt="Disabled account message at login" src="screenshots/11-account-disabled.png" />
  <img width="49%" alt="Password reset in Active Directory" src="screenshots/12-password-reset.png" />
</p>

### Troubleshooting a DNS Problem

I changed the client's DNS to `8.8.8.8` to see what would break. The user could still sign in, but Group Policy failed with name resolution errors because the client couldn't find the domain controller. After pointing DNS back to `192.168.1.5`, everything worked again.

<p align="center">
  <img width="49%" alt="gpupdate failing with wrong DNS" src="screenshots/13-gpupdate-dns-failure.png" />
  <img width="49%" alt="gpupdate working after fixing DNS" src="screenshots/14-gpupdate-fixed.png" />
</p>

### Delegating Password Resets

I created a **Help Desk** group and gave it permission to reset passwords for users in the Employees OU only, without making them full admins.

<p align="center">
  <img width="60%" alt="Delegation of Control Wizard" src="screenshots/15-delegation-wizard.png" />
</p>

## What I Learned

- A domain controller needs a static IP, and a `169.254` address means DHCP isn't working.
- Domain computers need to use the domain controller for DNS, or a lot of things quietly stop working.
- OUs organize accounts, while groups control what people can access.
- When someone changes roles, their old access needs to be removed too.
- It's better to give permissions to groups instead of individual users.

## Skills Practiced

Active Directory, DNS, OUs, users and groups, password resets, account management, static IP addressing, Hyper-V, `ipconfig`, `nslookup`, `ping`, `gpupdate`, `whoami`

## Next Steps

- Group Policy and shared folder permissions
- DHCP
- A help desk ticketing system connected to the domain

---

[← Back to portfolio](../README.md)
