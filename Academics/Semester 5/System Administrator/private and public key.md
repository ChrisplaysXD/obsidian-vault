**1. How SSL/TLS Works: The Handshake Process**

When a client (browser, mobile app, etc.) connects to a server over HTTPS, an **SSL/TLS handshake** happens before any data is exchanged. Here's the step-by-step breakdown:

### [](https://dev.to/prathvihan108/understanding-ssltls-encryption-how-session-keys-secure-your-communication-2n35#step-1-client-hello)**Step 1: Client Hello**

- The client sends a request to the server, indicating it wants a **secure connection**.
- It includes a list of supported **TLS versions** and **encryption algorithms**.

### [](https://dev.to/prathvihan108/understanding-ssltls-encryption-how-session-keys-secure-your-communication-2n35#step-2-server-hello-amp-certificate-exchange)**Step 2: Server Hello & Certificate Exchange**

- The server responds with a **digital certificate** (`cert.pem`) that proves its authenticity.
- This certificate contains the server’s **public key** and is signed by a trusted Certificate Authority (CA).
- The client verifies this certificate to confirm it's talking to the right server.

### [](https://dev.to/prathvihan108/understanding-ssltls-encryption-how-session-keys-secure-your-communication-2n35#step-3-session-key-generation)**Step 3: Session Key Generation**

- The client generates a **random session key**.
- It encrypts this session key using the server’s **public key** (from the certificate) and sends it to the server.
- The server decrypts it using its **private key** (`key.pem`).

### [](https://dev.to/prathvihan108/understanding-ssltls-encryption-how-session-keys-secure-your-communication-2n35#step-4-secure-communication-begins)**Step 4: Secure Communication Begins**

- Both the client and server now use the **same session key** for encrypting and decrypting messages.
- This session key is used with **symmetric encryption algorithms** like **AES (Advanced Encryption Standard)** to ensure **fast and secure** data exchange.

**Why Use a Session Key Instead of Public/Private Keys for Every Request?**  
✔ **Performance** – Asymmetric encryption (public/private key) is slow, but symmetric encryption (session key) is much faster.  
✔ **Efficiency** – The session key allows secure communication without needing to re-encrypt every request with the server’s public key.  
✔ **Security** – Even if the session key is compromised, it only affects one session (not all future communications).
