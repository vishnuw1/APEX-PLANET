Cryptography Basics

Symmetric vs. Asymmetric Encryption

Symmetric Encryption: Uses the same key for both encrypting and decrypting data. It's like a single secret code that both the sender and receiver know.
Pros: Fast and efficient.
Cons: The key must be securely shared between parties, which can be a risk.

Asymmetric Encryption: Uses a pair of keys: a public key and a private key. Data encrypted with the public key can only be decrypted with the corresponding private key.
Pros: Highly secure for key exchange; you don't need to share the private key.
Cons: Slower than symmetric encryption.

Hashing (MD5, SHA256)

Hashing is a one-way process that takes data and turns it into a fixed-size string of characters called a "hash" or "digest."

MD5: Stands for Message Digest 5. It's an older hashing algorithm. While it was once popular, it's now considered insecure because it is easy to find collisions (two different pieces of data that produce the same hash).

SHA256: Stands for Secure Hash Algorithm 256-bit. It's a more modern and secure hashing algorithm. It's widely used today to ensure data integrity, because even a tiny change in the original data will produce a completely different hash.

The main use of hashing is to verify data integrity. If the hash of a file matches the original hash, you can be sure the file hasn't been changed.

Digital Certificates & SSL/TLS

These are crucial for securing communication on the internet.

SSL/TLS: Stands for Secure Sockets Layer / Transport Layer Security. These are cryptographic protocols that provide secure communication over a computer network. They are used to encrypt the traffic between your web browser and a website.

Digital Certificates: These verify the identity of a website or server. A certificate links a public key to an organization's identity and is signed by a trusted third party, called a Certificate Authority (CA). When your browser connects to a website, it checks the website's digital certificate to ensure it's legitimate and that the connection is secure. This is why you see a padlock icon in your browser's address bar.

Hands-on: OpenSSL
OpenSSL is a powerful command-line tool for encryption and decryption. Here are some basic commands you can use to complete the hands-on task:

To Encrypt:
openssl enc -aes-256-cbc -in [input_file.txt] -out [encrypted_file.enc]

To Decrypt:
openssl enc -d -aes-256-cbc -in [encrypted_file.enc] -out [decrypted_file.txt]



The CIA Triad 

The CIA Triad is a fundamental model for security. Think of it as the three main goals you're trying to achieve to keep information safe.

Confidentiality: This means keeping data secret and accessible only to authorized people. An example is using a strong password to protect your email.

Integrity: This ensures that data is accurate and has not been tampered with or corrupted. For instance, a bank's record of your balance must be correct and unchanged.

Availability: This means that authorized users can access the information and systems whenever they need to. A good example is a website that is always online and doesn't crash.

Threat Types

These are the different kinds of malicious activities or attacks we might face.

Phishing: Tricking someone into revealing sensitive information (like passwords or credit card numbers) through fake emails or websites.

Malware: Malicious software designed to disrupt or damage computer systems. This includes viruses, worms, and Trojans.

DDoS (Distributed Denial-of-Service): Flooding a server with so much traffic that it overwhelms the system and becomes unavailable to legitimate users.

SQL Injection: Exploiting a vulnerability in a web application's database to access, modify, or delete data.

Brute Force: Trying to guess a password or key by attempting a massive number of possible combinations.

Ransomware: A type of malware that locks down a user's files and demands a ransom payment to unlock them.

Attack Vectors

These are the methods or paths that attackers use to gain access to a system or network.

Social Engineering: Manipulating people to get them to give up confidential information. This often involves psychological tricks rather than technical hacking.

Wireless Attacks: Exploiting vulnerabilities in a Wi-Fi network to gain unauthorized access. This can include cracking the password or setting up a fake Wi-Fi access point.

Insider Threats: When an authorized person, like an employee or former employee, uses their access to steal data or damage a system.

