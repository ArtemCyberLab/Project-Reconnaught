Project Goal
This project was created to demonstrate the practical use of initial reconnaissance techniques, authentication into a remote system, and extraction of a target artifact (a flag), based on credentials leaked through open services. All steps were performed on a CTF-style training environment.

Tools & Technologies Used
Nmap 7.80 – Port scanning with default scripts and service/version detection (-sC -sV)

OpenSSH 8.2p1 – Target SSH service on standard and non-standard ports

Ubuntu 20.04 – Target operating system

Linux CLI – Shell-based interaction and navigation for artifact retrieval

Steps Taken
1. Host Scanning
I started by running an active scan on the target IP 10.10.16.71 using nmap with built-in scripts and version detection:

nmap -sC -sV 10.10.16.71
The scan results revealed:

Ports 22 and 2222: Running OpenSSH

Port 31337: Unidentified service returning plaintext credentials

In case I forget - user:pass
ubuntu:Dafdas!!/str0ng
2. SSH Authentication
Using the leaked credentials, I successfully connected to the system via SSH:

ssh ubuntu@10.10.16.71
Password: Dafdas!!/str0ng

3. Flag Extraction
After logging in, I explored the filesystem and discovered a separate user directory:

cd /home/user
ls -al
Inside, I found a file named flag.txt:

cat flag.txt
The flag was successfully retrieved:

flag{251f309497a18888dde5222761ea88e4}

Conclusion
This challenge turned out to be relatively easy due to a clear misconfiguration: a sensitive service on a high-numbered port (31337) was exposing plaintext credentials — a textbook example of why security through obscurity is not enough.

The exercise reinforced the importance of:

Performing thorough service enumeration

Validating the content of unidentified ports

Avoiding credential leakage in service banners or debug responses

Final Thoughts
Although the challenge was on the lighter side, it served as a fun and practical refresher on reconnaissance fundamentals. In real-world scenarios, even “small” mistakes like this can have serious consequences — which makes exercises like this invaluable.
