# 🌐 Web & Email Server Hardening (Apache, Postfix, & Dovecot)

## 🛡️ Project Overview
This project involved the end-to-end setup and security hardening of a robust mail and web server environment on **Rocky Linux 9.4**. The primary goal was to ensure all communications were secured using **SSL/TLS (Self-Signed Certificates)** and to verify the encryption's effectiveness using network analysis tools.

### Key Objectives
* **Mail Server Setup:** Install and configure Postfix (MTA) and Dovecot (IMAP/POP3) to handle secure email transmission and retrieval.
* **Web Server Setup:** Install and configure Apache HTTPD to serve web content.
* **Encryption Implementation:** Apply a self-signed SSL/TLS certificate to both Postfix/Dovecot and Apache to enable secure protocols (SMTPS, IMAPS, HTTPS).
* **Verification:** Use **Wireshark** to confirm that sensitive data (like login credentials and message bodies) was successfully encrypted during transmission, particularly after implementing **STARTTLS**.

---

## 🛠️ Technical Stack & Tools

| Category | Component / Tool | Purpose in Project |
| :--- | :--- | :--- |
| **Operating System** | Rocky Linux 9.4 | Server host operating system (`mugserver.techsys.com`). |
| **Mail Transport Agent** | Postfix | Responsible for sending and routing mail (SMTP/SMTPS). |
| **Mail Retrieval Agent** | Dovecot | Responsible for mail retrieval (IMAP/IMAPS). |
| **Web Server** | Apache HTTPD (`httpd`) | Serving web content (HTTP/HTTPS). |
| **Security & Crypto** | OpenSSL | Used to generate the 2048-bit RSA self-signed SSL/TLS certificate. |
| **Network Analysis** | Wireshark | Used on the client to capture packets and verify encryption. |
| **Mail Client** | Mozilla Thunderbird | Used on the Ubuntu client (`mugclient.techsys.com`) for email testing. |

---

## 🔒 Hardening Highlights & Results

### Postfix & Dovecot Security
* Configured **Postfix** to use **Dovecot** for SMTP-Auth (SASL), ensuring only authenticated users can send mail.
* Implemented **anti-spam measures** by enforcing client, sender, and HELO restrictions to reject improperly configured hosts and potential spoofing attempts.
* Enabled both **SMTPS (Port 465)** and **STARTTLS (Port 587/25)** encryption methods to secure mail transfer.

### Apache HTTPD Security
* Configured Apache to **permanently redirect all HTTP (Port 80) traffic to HTTPS (Port 443)**, enforcing secure communication for web access.
* Used the `ServerTokens Prod` directive to minimize version disclosure in HTTP headers, reducing information leakage.
* Removed the `Indexes` option from the `DocumentRoot` to prevent unauthorized directory listing.

### Encryption Verification
Analysis with **Wireshark** confirmed that after configuring SSL/TLS, the data transmission in both Mail and Web services was encrypted, successfully preventing credentials and message content from being read in cleartext.

**Key Takeaway:** The project successfully established secure Mail and Web services, validating strong encryption controls against network sniffing.
