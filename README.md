# Cryptography-TLS1.3-Lab
A study and documentation of TLS 1.3 protocol mechanics, handshake, cipher suites, and security improvements.
1) TLS 1.3 ( Transport Layer Security 1.3 ) is a security protocol that allows a client and a server to communicate securely online . It provides three major security features:
    Confidentiality prevents third parties from reading the data that are being sent.
    Integrity: protects against covert data alteration.
    Authentication: it is used to verify the identity of the communicating server.
    TLS 1.2 was bumped to TLS 1.3 It speeds up the process of establishing a secure connection and enhances security.
    
2) Explaining the TLS 1.3 handshake
 The TLS handshake is the method by which a client and server agree on a secure connection.In a typical TLS 1.3 connection,   the handshake is done in 1 round trip (1-RTT).
 In the shakes.The client sends a ClientHello message with its crypto options and a key share.The server responds with a      ServerHello message that will include its chosen options and key share.The server sends the authentication information (certificate and digital signature)Both parties compute the common encryption keys.Client and server exchange Finished       messages.The application data can then be sent encrypted.TLS 1.3 also supports early data in 0-RTT resumption of a previous connection with a pre-shared key. This may reduce latency, but 0-RTT data has other security considerations regarding replay.

3) TLS 1.3 Handshake Flow Diagram
         The simplified handshake can be represented as:
       CLIENT                                  SERVER

          |                                       |
          |-------- ClientHello + Key Share ----->|
          |                                       |
          |<------- ServerHello + Key Share -----|
          |<------- Encrypted Extensions --------|
          |<------- Certificate ------------------|
          |<------- CertificateVerify ------------|
          |<------- Finished ---------------------|
          |                                       |
          |---------- Finished ------------------>|
          |                                       |
          |<==== Encrypted Application Data =====>|
          |                                       |

          Simple Flow
          
ClientHello
     ↓
ServerHello + Key Exchange
     ↓
Server Authentication
     ↓
Finished Messages
     ↓
Encrypted Communication

The key improvement is that TLS 1.3 reduces the normal handshake to 1-RTT, making secure connections faster than TLS 1.2.

4)TLS 1.2 vs TLS 1.3
   Normal Handshake: TLS 1.2 — Usually 2-RTT | TLS 1.3 — 1-RTT

   0-RTT: TLS 1.2 — Not available as TLS 1.3 early data | TLS 1.3 — Supported for resumption

   Key Exchange: TLS 1.2 — Several older methods available | TLS 1.3 — Modern ephemeral key exchange such as ECDHE

   Forward Secrecy: TLS 1.2 — Not always required | TLS 1.3 — Provided by normal ephemeral key exchange

   Cipher Suites: TLS 1.2 — More complex and includes legacy choices | TLS 1.3 — Simpler and modern

   RSA Key Exchange: TLS 1.2 — Supported | TLS 1.3 — Removed

   RC4: TLS 1.2 — Legacy/obsolete | TLS 1.3 — Removed

   MD5: TLS 1.2 — Legacy/obsolete | TLS 1.3 — Removed

   Security: TLS 1.2 — Older design | TLS 1.3 — Stronger modern design

   Performance: TLS 1.2 — More handshake overhead | TLS 1.3 — Lower handshake latency

5)TLS 1.3 Cipher Suites
    A cipher suite defines the algorithms used to protect encrypted communication.
    TLS 1.3 supports modern authenticated encryption cipher suites such as:
    TLS_AES_128_GCM_SHA256
     Uses:
       AES-128 for encryption
       GCM for authenticated encryption
       SHA-256 for hashing
   TLS_AES_256_GCM_SHA384
    Uses:
      AES-256 for encryption
      GCM for authenticated encryption
      SHA-384 for hashing
  TLS_CHACHA20_POLY1305_SHA256
   Uses:
      ChaCha20 for encryption
      Poly1305 for authentication
      SHA-256 for hashing
TLS 1.3 simplifies cipher-suite selection and removes obsolete mechanisms. For example, RSA is no longer used for key exchange, and older algorithms such as RC4 and MD5 are not part of TLS 1.3.

6) ECDHE and Forward Secrecy
   ECDHE stands for Elliptic Curve Diffie-Hellman Ephemeral.
   It is a key-exchange mechanism that allows the client and server to establish a shared secret without directly sending that secret over the network.
The simplified process is:

Client                                Server

Private temporary key                Private temporary key
        ↓                                    ↓
   Key Exchange  -------------------->  Key Exchange
        ↓                                    ↓
        └────── Shared Secret ──────────────┘
                       ↓
                Session Encryption Key

The word ephemeral means that temporary keys are used for the session.Forward secrecy means that if a server's long-term private key is compromised in the future,previously recorded TLS sessions should not be able to be decrypted.
TLS 1.3 normally uses ephemeral key exchange such as ECDHE to provide this protection.






