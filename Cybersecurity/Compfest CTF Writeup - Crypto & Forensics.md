---
title: "Compfest CTF Writeup: Cryptography & Network Forensics"
created: 2026-09-09
tags:
  - cybersecurity
  - ctf
  - cryptography
  - rsa
  - forensics
  - pcap
  - python
aliases:
  - Compfest Writeup
  - RSA Wiener Attack Writeup
type: writeup
status: complete
---

# Compfest CTF Writeup: Cryptography & Network Forensics

Complete analysis and solution walkthrough for two advanced competition challenges: custom modulus inflation in RSA and chronological time-series packet steganography.

---

## 1. Cryptography Challenge: Wiener's Attack on Inflated Totient

### Vulnerability Analysis
The target challenge file `chall.py` implemented a non-standard Euler totient formulation:
- Standard Euler totient: $\phi(N) = (p-1)(q-1)$
- Target implementation: $\phi_{custom} = (p^2 - 1)(q^2 - 1)$

This algebraic modification inflates $\phi$ to the order of $\approx N^2$, yielding an 8192-bit modulus space rather than the standard 4096-bit dimension.

Furthermore, the private exponent was bounded:
$$d = \phi - k, \quad k < 2^{2048}$$

Given the fundamental congruence $e \cdot d \equiv 1 \pmod{\phi}$, substituting $d$ produces:
$$e(\phi - k) \equiv 1 \pmod{\phi} \implies e \cdot (-k) \equiv 1 \pmod{\phi}$$
$$e \cdot k + 1 = c \cdot \phi$$

Because $\phi \approx N^2$ (8192 bits) while $k < 2^{2048}$, the ratio satisfies Wiener's condition:
$$k < \frac{1}{3}\phi^{1/4}$$

Using continued fraction expansion of $\frac{e}{(N-1)^2}$, the rational convergents $\frac{c}{k}$ reveal candidate values for $k$ and the inflated totient $\phi$.

### Solver Implementation (`solve.py`)

```python
from Crypto.Util.number import inverse, long_to_bytes
import math

def get_convergents(e, n):
    convergents, q = [], []
    a, b = e, n
    while b != 0:
        q.append(a // b)
        a, b = b, a % b
        
    n0, n1 = 0, 1
    d0, d1 = 1, 0
    for qi in q:
        n2 = qi * n1 + n0
        d2 = qi * d1 + d0
        convergents.append((n2, d2))
        n0, n1 = n1, n2
        d0, d1 = d1, d2
    return convergents

def is_perfect_square(n):
    if n < 0: return False
    x = math.isqrt(n)
    return x * x == n

def solve(N, e, ct):
    approx_phi = (N - 1) ** 2
    for c, k in get_convergents(e, approx_phi):
        if c == 0 or k == 0 or (e * k + 1) % c != 0:
            continue
        phi = (e * k + 1) // c
        S = N**2 + 1 - phi
        D = S**2 - 4 * (N**2)
        if D >= 0 and is_perfect_square(D):
            sqD = math.isqrt(D)
            if (S + sqD) % 2 == 0:
                p2 = (S + sqD) // 2
                q2 = (S - sqD) // 2
                if is_perfect_square(p2) and is_perfect_square(q2):
                    p, q = math.isqrt(p2), math.isqrt(q2)
                    if p * q == N:
                        d = inverse(e, phi)
                        m = pow(ct, d, N)
                        print("RECOVERED FLAG:", long_to_bytes(m))
                        return
```

> [!success] Cryptography Result
> **Flag:** `COMPFEST18{some_good_ol_wienner_attack_on_too_large_d}`

---

## 2. Forensics Challenge: Chronological TCP Port Steganography

### Traffic Analysis
Inspection of `network_log.pcap` revealed no HTTP transactions, DNS queries, or conventional application layer streams. Instead, a large sequence of bare TCP packets targeted varying high ports.

> [!important] Encoding Mechanism
> The 16-bit destination port values directly encoded ASCII characters via 2-byte packing:
> $$\text{char}_1 = \text{port} \gg 8, \quad \text{char}_2 = \text{port} \ \& \ 0\text{xFF}$$

Due to packet capture jitter and multi-threading, arrival times were out of sequence. Packets had to be sorted by absolute arrival timestamp (`frame.time_relative`) and partitioned by source IP (`192.168.1.100` vs `192.168.1.101`).

### Extraction Pipeline

```bash
python3 -c "
import subprocess
out = subprocess.check_output(['tshark', '-r', 'network_log.pcap', '-T', 'fields', '-e', 'frame.number', '-e', 'frame.time_relative', '-e', 'ip.src', '-e', 'tcp.dstport']).decode()
lines = [l.split('\t') for l in out.splitlines() if l]
parsed = [(float(p[1]), p[2], int(p[3])) for p in lines if len(p) >= 4 and p[3]]
parsed.sort(key=lambda x: x[0])

stream_100 = ''.join(chr(p[2] >> 8) + chr(p[2] & 0xff) for p in parsed if p[1] == '192.168.1.100')
stream_101 = ''.join(chr(p[2] >> 8) + chr(p[2] & 0xff) for p in parsed if p[1] == '192.168.1.101')
print('Password string:', stream_101)
"
```

1. **Stream from `.101`**: Base64 decoded to `The password of zipfile is 89874223acfe6272eeaca8ffbaed6f1d`.
2. **Stream from `.100`**: Encoded a ZIP container header (`PK\x03\x04`).

```bash
python3 -c "
import base64
with open('flag.zip', 'wb') as f:
    f.write(base64.b64decode('UEsDBAoACQAAAHuG...'))
" && unzip -P 89874223acfe6272eeaca8ffbaed6f1d flag.zip && cat flag.txt
```

> [!success] Forensics Result
> **Flag:** `COMPFEST18{mess4ge_0ver_filt3red_port_sc4n_ad841e}`

---

## Related Notes
- [[Cybersecurity MOC]]
- [[Data Structures & Algorithms - Fundamentals]]
- [[CompTIA Network+ Exam Tips#Protocols & Monitoring]]
