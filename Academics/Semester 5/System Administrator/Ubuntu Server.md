---
title: Ubuntu Server
tags:
  - sysadmin
  - academic
  - semester-5
  - linux
  - subject-tag
type: lecture-note
status: active
created: 2026-09-04
aliases: []
---

# Ubuntu Server

> [!abstract] Lecture Summary
> setting up ubuntu server, changing the ip address to the lab ip,and connecting via ssh.

---

## 1. Core Principles
when it comes to linux theres usually 2 type of them a desktop and server version. a desktop version is mainly gui based while server is mainly console based.a desktop version usually get an update ranging from rolling update or every couple month while a server version is made around stability meaning it get update but not as often as desktop version 

---

## 2. Practical Implementation / Code
# Initial Setup
- setup a usb preferably with ventoy(or just burn the iso into the flashdisk via rufus or other iso burner)
	  - download [ventoy] from https://www.ventoy.net/en/download.html ([rufus]= https://rufus.ie/en/ )
- install ubuntu server(or other distro)
	  - suggested version 24 but the latest version 26 is fine (https://ubuntu.com/download/server)
- follow the on screen setup wizard and hit yes until we got to the partition setup
- in partion setup we need to choose the manual option not auto 
- then we move to the user setup where we can make our username and root username with password
- finally once were in do a repo update via sudo apt update & sudo apt upgrade
# Network Setup
- install NetworkManager: `sudo apt install network-manager`
- hand over interface management from systemd-networkd to NetworkManager in Netplan:
  - open the configuration file: `sudo nano /etc/netplan/*.yaml`
  - set `renderer: NetworkManager` under `network:`
  - apply configuration: `sudo netplan apply`
  - restart daemon: `sudo systemctl restart NetworkManager`
- verify interface state is managed: `nmcli device status`
- assign the static lab IP:
  - `sudo nmcli connection add type ethernet ifname <interface> con-name static-eth ipv4.method manual ipv4.addresses 192.168.24.16/24 ipv4.gateway 192.168.24.100 ipv4.dns "8.8.8.8 1.1.1.1"`
  - activate profile: `sudo nmcli connection up static-eth`
  - verify IP assignment: `ip a`

# SSH Access
- install OpenSSH server: `sudo apt install openssh-server -y`
- verify service is active: `sudo systemctl status ssh`
- connect from client machine: `ssh <username>@192.168.24.16`

---

## 3. Personal Key Takeaways & Notes for Next
- the ui is teribble.
- wonder how the other server distro would look.
- task for next: 
	- [ ] ⏫ configure antigravity cli
	- [ ] 🔼 install other server distro(RHEL(centOS),almalinux,etc)
	- [ ] 🔽 return the original partition(optional)

---

## Related Notes
- [[Academic MOC]]
