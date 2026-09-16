---
title: Linux System Administration & Automation
created: 2026-09-04
tags:
  - academic
  - semester-5
  - sysadmin
  - linux
  - systemd
  - automation
  - security
aliases:
  - System Administrator Day 1
  - Linux SysAdmin Fundamentals
type: lecture-note
status: active
---

# Linux System Administration & Automation

Core competencies for enterprise Linux system administration, process supervision, storage provisioning, security authentication stacks, and administrative automation.

> [!abstract] Administrative Mandate
> System administrators guarantee the operational availability, performance, and security posture of multi-user operating systems through deterministic configuration management, automated telemetry, and principle of least privilege.

---

## 1. Systemd Service Lifecycle & Process Management

`systemd` acts as PID 1, handling parallelized boot sequences, socket activation, and service dependency graphs.

```bash
# Service lifecycle management
sudo systemctl start <unit>.service
sudo systemctl enable --now <unit>.service
sudo systemctl status <unit>.service

# Inspect systemd journal logs
journalctl -u <unit>.service -f --since "1 hour ago"
```

### Writing a Custom Systemd Service Unit
```ini
[Unit]#
Description=Custom Background Task Daemon
After=network.target

[Service]
Type=simple
User=chrisplaysxd
ExecStart=/usr/local/bin/my-daemon
Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```


---

## 2. Pluggable Authentication Modules (PAM) & Access Control

Authentication logic in Linux is decoupled from application code via the PAM framework located in `/etc/pam.d/`.

- **`auth`**: Validates credentials (passwords, biometrics, hardware tokens).
- **`account`**: Verifies account validity (expiration, access windows, group policies).
- **`password`**: Enforces passphrase complexity and updates authentication tokens.
- **`session`**: Configures environment variables, mount points, and auditing wrappers upon login.

> [!tip] Hardware Authentication Hooks
> PAM allows seamless integration of physical hardware tokens via `pam_u2f.so` to enforce MFA on `sudo` and graphical display managers. See [[Hardware Security Keys - FIDO2 & WebAuthn#4. Linux PAM Integration (pam_u2f)|PAM U2F Integration]].

---

## 3. Storage & Filesystem Administration
- **POSIX Permission Architecture**: Standard `rwx` bits for User, Group, and Others, alongside SUID (`4000`), SGID (`2000`), and Sticky Bit (`1000`).
- **Modern Copy-on-Write (CoW) Filesystems**: Managing Btrfs/ZFS subvolumes, instantaneous snapshots, and transparent zstd compression.
- **LVM (Logical Volume Management)**: Dynamic pooling of Physical Volumes (PVs) into Volume Groups (VGs) and dynamically resizable Logical Volumes (LVs).

---

## Related Notes
- [[Academic MOC]]
- [[Hardware Security Keys - FIDO2 & WebAuthn]]
- [[CompTIA Network+ Exam Tips#Network Security & Access Control]]
- [[Cybersecurity MOC]]
