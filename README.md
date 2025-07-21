🕵️ Packet Sniffing and Credential Capture in a Controlled Lab

📘 Project Overview

This project demonstrates **packet sniffing** and **plaintext credential capture** in a safe, isolated lab environment as part of a cybersecurity assignment. I have created two virtual machines one is attacker and one is victim. The goal is to highlight the security risks of transmitting unencrypted credentials using tools like **Wireshark**.

🎯 Objective

To perform packet sniffing in a virtual lab using appropriate tools and extract usernames and passwords transmitted in plaintext via **HTTP** and **FTP** protocols.

🧰 Tools & Technologies Used

- Operating Systems: Kali Linux (Attacker), Windows 10 (Victim)
- Sniffing Tool: Wireshark
- Virtualization Platform: VMware
- Network Type: Bridged
- Target Websites: **using systems in Virtual Machines on same network**
  - [`certifiedhacker.com`](http://certifiedhacker.com)
  - [`testphp.vulnweb.com`](http://testphp.vulnweb.com)

🧪 Lab Setup

- Kali Linux with Wireshark installed as the attacker machine.
- Windows 10 virtual machine acting as the victim.
- Both machines connected to the same bridged network interface.
- Communication tested via:
  - **FTP login** using Windows CMD.
  - **HTTP POST login** via web browser.

🛠️ Methodology

🔹 5.1 FTP Credential Sniffing (`certifiedhacker.com`)
1. Started Wireshark on Kali, interface `eth0`.
2. Victim logged into FTP server using CMD on Windows (`ftp certifiedhacker.com`).
3. Applied filter: `tcp.port == 21`.
4. Located packet containing FTP credentials.
5. Extracted:
   - **Username:** `test`
   - **Password:** `testqwerty`

🔹 5.2 HTTP Credential Sniffing (`testphp.vulnweb.com`)
1. Started Wireshark on Kali, interface `eth0`.
2. Victim logged into `testphp.vulnweb.com` via browser.
3. Applied filter: `http`.
4. Identified HTTP `POST` request containing form data.
5. Extracted:
   - **Username:** `test`
   - **Password:** `test`

🔍 Observations

| Target Site using Same System              | Protocol | Credentials Captured         | Security Risk         |
|--------------------------------------------|----------|-------------------------------|------------------------|
| certifiedhacker.com                        | FTP      | `test:testqwerty`             | No encryption on FTP   |
| testphp.vulnweb.com                        | HTTP     | `test:test`                   | No SSL/TLS on POST     |

Screenshots are available in the [`screenshots/`](./Screenshots) directory.

## ⚠️ Analysis

- Sensitive data such as usernames and passwords were transmitted in **plaintext**.
- **Wireshark** easily intercepted this data with no need for advanced techniques.
- This demonstrates the danger of using **unencrypted protocols** like HTTP and FTP.

🛡️ Security Implications

- Attackers with access to the network can easily sniff login credentials.
- **Recommendations:**
  - Always use **HTTPS** and **SFTP** for secure communication.
  - Employ **SSL/TLS** encryption.
  - Monitor network traffic using IDS/IPS.
  - Use strong password policies and hashing mechanisms.

✅ Conclusion

This project proves that transmitting login credentials over unencrypted channels can be easily exploited using packet sniffing tools like Wireshark. It highlights the importance of secure transmission protocols and adherence to cybersecurity best practices.

⚠️ Disclaimer

> This experiment was conducted in a **controlled lab environment** strictly for educational purposes. I have caputured the packets only of my network for credential.  
> **Do NOT use packet sniffing techniques on unauthorized or live production networks.**

📧 Author

Shubham Shah  
CEH | CCT Student | [LinkedIn] (https://www.linkedin.com/in/shubhamshah11/)
