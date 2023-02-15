# Final Test Tools Cheat Sheet

## Vulnerable and Outdated Components

`A06:2021-Vulnerable and Outdated Components` was previously titled Using `Components with Known Vulnerabilities` and is `#2` in the Top 10 community survey, but also had enough data to make the Top 10 via data analysis. This category moves up from `#9` in `2017` and is a known issue that we struggle to test and assess risk. 

### Vulnerable and Outdated Components Description

You are likely vulnerable::
-	If you do not know the versions of all components you use (both client-side and server-side). This includes components you directly use as well as nested dependencies.
-	If the software is vulnerable, unsupported, or out of date. This includes the OS, web/application server, database management system (DBMS), applications, APIs and all components, runtime environments, and libraries.
-	If you do not scan for vulnerabilities regularly and subscribe to security bulletins related to the components you use.
-	If you do not fix or upgrade the underlying platform, frameworks, and dependencies in a risk-based, timely fashion. This commonly happens in environments when patching is a monthly or quarterly task under change control, leaving organizations open to days or months of unnecessary exposure to fixed vulnerabilities.
-	If software developers do not test the compatibility of updated, upgraded, or patched libraries.
-	If you do not secure the components’ configurations (see A05:2021-Security Misconfiguration).

### Vulnerable and Outdated Components Example Attack Scenarios

Components typically run with the same privileges as the application itself, so flaws in any component can result in serious impact. Such flaws can be accidental (e.g., coding error) or intentional (e.g., a backdoor in a component). 

Some example exploitable component vulnerabilities discovered are:

        -	`CVE-2017-5638`, a Struts 2 remote code execution vulnerability that enables the execution of arbitrary code on the server, has been blamed for significant breaches.
        -	While the `internet of things (IoT)` is frequently difficult or impossible to patch, the importance of patching them can be great (e.g., biomedical devices).
        -   There are automated tools to help attackers find unpatched or misconfigured systems. For example, the `Shodan IoT search engine` can help you find devices that still suffer from Heartbleed vulnerability patched in `April 2014`.

### Heartbleed Vulnerability

- improper input validation 
- a buffer over-read
    - more data can be read than should be allowed
- exploited by sending a malformed heartbeat request with a `small payload` and `large length field` to the vulnerable party
- read up to 64 kilobytes of the victim's memory 
- attacker has some control over the disclosed memory block's size
- no control over its location

### Heartbleed Attack on bwapp from Kali

1. Browse to BWAPP Website on Kali
2. Choose Heartbleed Vulnerability
3. Click on attack script to download the script
4. Perform a nmap scan with

        sudo nmap -sV -Pn -T4 -p- bWAPP_IP 
        sudo nmap --script ssl-heartbleed -sV -p 443,8443,9443 bWAPP_IP

5. Use sslyze

        sslyze bWAPP_IP:<port vulnerable to heartbleed attack>

6. Browse to BWAPP Website on Kali

        https://192.168.93.132:8443/bWAPP/heartbleed.php

7. Using Terminal run the following commands

        cd Downloads
        python2 heartbleed.py -p <port vulnerable to heartbleed attack> bWAPP_IP

8. Get results

## Cryptographic Failures

`A02:2021-Cryptographic Failures` shifts up one position to #2, previously known as `A3:2017-Sensitive Data Exposure`, which was `broad symptom` rather than a `root cause`. The renewed name focuses on `failures related to cryptography` as it has been implicitly before. This category often `leads to sensitive data exposure` or `system compromise`. Notable Common Weakness Enumerations (CWEs) included are `CWE-259`: Use of Hard-coded Password, `CWE-327`: Broken or Risky Crypto Algorithm, and `CWE-331` Insufficient Entropy.

### Cryptographic Failures Description

- First determine the protection needs of data in transit and at rest

- Ask Questions

    -	Is any data transmitted in clear text? This concerns protocols such as HTTP, SMTP, FTP also using TLS upgrades like STARTTLS. External internet traffic is hazardous. Verify all internal traffic, e.g., between load balancers, web servers, or back-end systems.
    -	Are any old or weak cryptographic algorithms or protocols used either by default or in older code?
    -	Are default crypto keys in use, weak crypto keys generated or re-used, or is proper key management or rotation missing? Are crypto keys checked into source code repositories?
    -	Is encryption not enforced, e.g., are any HTTP headers (browser) security directives or headers missing?
    -	Is the received server certificate and the trust chain properly validated?
    -	Are initialization vectors ignored, reused, or not generated sufficiently secure for the cryptographic mode of operation? Is an insecure mode of operation such as ECB in use? Is encryption used when authenticated encryption is more appropriate?
    -	Are passwords being used as cryptographic keys in absence of a password base key derivation function?
    -	Is randomness used for cryptographic purposes that was not designed to meet cryptographic requirements? Even if the correct function is chosen, does it need to be seeded by the developer, and if not, has the developer over-written the strong seeding functionality built into it with a seed that lacks sufficient entropy/unpredictability?
    -	Are deprecated hash functions such as MD5 or SHA1 in use, or are non-cryptographic hash functions used when cryptographic hash functions are needed?
    -	Are deprecated cryptographic padding methods such as PKCS number 1 v1.5 in use?
    -	Are cryptographic error messages or side channel information exploitable, for example in the form of padding oracle attacks?

### Cryptographic Failures Example Attack Scenarios

1. An application encrypts credit card numbers in a database using automatic database encryption. However, this data is automatically decrypted when retrieved, allowing a SQL injection flaw to retrieve credit card numbers in clear text.

2. A site doesn't use or enforce TLS for all pages or supports weak encryption. An attacker monitors network traffic (e.g., at an insecure wireless network), downgrades connections from HTTPS to HTTP, intercepts requests, and steals the user's session cookie. The attacker then replays this cookie and hijacks the user's (authenticated) session, accessing or modifying the user's private data. Instead of the above they could alter all transported data, e.g., the recipient of a money transfer.

3. The password database uses unsalted or simple hashes to store everyone's passwords. A file upload flaw allows an attacker to retrieve the password database. All the unsalted hashes can be exposed with a rainbow table of pre-calculated hashes. Hashes generated by simple or fast hash functions may be cracked by GPUs, even if they were salted.

## Software and Data Integrity Failures

A new category for 2021 focuses on `making assumptions` related to `software updates`, `critical data`, and `CI/CD pipelines without verifying integrity`. One of the `highest weighted impacts` from Common Vulnerability and Exposures/Common Vulnerability Scoring System (CVE/CVSS) data. Notable Common Weakness Enumerations (CWEs) include `CWE-829`: Inclusion of Functionality from Untrusted Control Sphere, `CWE-494`: Download of Code Without Integrity Check, and `CWE-502`: Deserialization of Untrusted Data.

### Software and Data Integrity Failures Description

- code and infrastructure that does not protect against integrity violations
- application relies upon plugins, libraries, or modules from untrusted sources, repositories, and content delivery networks (CDNs)
- An insecure CI/CD pipeline can introduce the potential for unauthorized access, malicious code, or system compromise
- auto-update functionality, where updates are downloaded without sufficient integrity verification and applied to the previously trusted application
- potentially upload their own updates to be distributed and run on all installations
- objects or data are encoded or serialized into a structure that an attacker can see and modify is vulnerable to insecure deserialization

### Software and Data Integrity Failures Example Attack Scenarios

1. Update without signing: Many home routers, set-top boxes, device firmware, and others do not verify updates via signed firmware. Unsigned firmware is a growing target for attackers and is expected to only get worse. This is a major concern as many times there is no mechanism to remediate other than to fix in a future version and wait for previous versions to age out.

2. SolarWinds malicious update: Nation-states have been known to attack update mechanisms, with a recent notable attack being the SolarWinds Orion attack. The company that develops the software had secure build and update integrity processes. Still, these were able to be subverted, and for several months, the firm distributed a highly targeted malicious update to more than 18,000 organizations, of which around 100 or so were affected. This is one of the most far-reaching and most significant breaches of this nature in history.

3. A React application calls a set of Spring Boot microservices. Being functional programmers, they tried to ensure that their code is immutable. The solution they came up with is serializing the user state and passing it back and forth with each request. An attacker notices the "rO0" Java object signature (in base64) and uses the Java Serial Killer tool to gain remote code execution on the application server.
