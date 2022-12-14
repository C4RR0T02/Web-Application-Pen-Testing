# Hacker's view of the web

## Types of Web Server
1. Web Servers
2. Dynamic Servers
3. Application Servers
4. Proxy Servers

### Web Servers
- Very rare for `pure web servers`
- Static Content only
- Used for information discovery
- Usually safe from active web application attacks
- Daemon service listening for service request
- Example of Commonly used Web Services
    - IIS (Internet Information Server)
    - Apache Web Server 
- Possess different vulnerabilities that can be exploited
- Pen-tester needs to first map out the type of Web Server is being used to host the web application

### Dynamic Servers
- Serves both `static` and `active` content
- `active content` drawn from `back-end data store`
    - relational database
    - file servers / application servers
- Simple and inexpensive to set up
- more difficult to harden
    - code is executed in the same server as the display

### Application Server Architecture
- Application is executed within an application server
    - Usually located behind a proxy server 
- rarely communicate with the client
- website that provides both static and dynamically generated content runs web servers
- software process that resides on the server-side and provides business logic behind any application
- Application servers needs to be patched to prevent attacks that make use of the known vulnerabilities.

### Proxy Server Architecture
- Front end for one or more applications
    - called reverse proxy to differentiate from proxy used by clients
- Passes request through application and caches the result
- Targeted as it contains cache data which may be confidential (cache poisoning)
- Inbound and outbound proxies
- Provides content caching

---

## Why is it important to know the Website Server Architecture?
- Makes attacking easier
    - has features that can be targeted
- `Application` and the `data` are targets
- Attacks on website can be used to gain access into the company's network
- Website Server Architect may open more attack vector's
    - Cache Poisoning against proxies (defacement of site)
    - Source code disclosure attack against application servers

---

### HTTP Protocol
- Hypertext Transfer Protocol (HTTP)
- `Request` and `Response` protocol using TCP
- Has many versions
    - HTTP/1 - 1996
    - HTTP/1.1 - 1997
    - HTTP/2 - 2015
    - HTTP/3 - 2022

## HTTP Request
- Request contains a number of header fields
- usually are optional or added by client / application
- Modifies logic based user agent string
    - Example when using Windows user agent, it shows a different UI / screen size compared to a Android user agent

### User Agent
- Web clients are considered a User-Agent
    - Usually a browser but not always
- Can be spoofed

## HTTP Response
Contains the following
1. Status code
2. Server Token
3. Server Time
4. Content Length

### Status Code
- Result from the request
- Often mistaken as error code

### Server Token
- String returned to the web server identifying itself
- can be spoofed or changed by administrator

### Server Time
- Time stamp based on server's time and date

### Content Length
- Length of the response

**`Header always ends with a blank line`**

---

## [Activity 1.1](activity1.1.md)

---

## What is HTTPS?
Uses the TCP/IP structure to implement TLS/SSL encryption to protect the data in transit

### HTTPS Status codes
100s: `Informational codes` indicating request initiated by the browser

200s: `Success codes` returned when browser request is received, understood and processed by the server

300s: `Redirection codes` returned when a new resource has been substituted for the requested resource

400s: Client error codes indicating that there was a `problem with the request`

500s: Server error codes indicating that the request was accepted, but that `an error on the server` prevented the fulfillment of the request

---

## Web Application Architecture

### What is a Web Application Architecture?
- `Complete setup` platform / virtual environment that can be used to `deliver services of a web application`
- `Basic components` of an actual production environment
    - Hardware Server / VM with Server Operating system
    - Web Server
    - Database Server
    - Application Server
    - Browser Client
- Components and make should be known by pen-testers for `effectivity` and `efficiency`

### What is a Server Operating System?
- `Operating System (OS)` used in server hardware / VM that `host the Web Application`
- Examples of Server OS
    - Windows Server 2019
    - Windows Server 2016
    - Ubuntu Server 21.04
    - Fedora 34 Server
    - etc.
- Operating System requires to be `hardened` to prevent attacks from known vulnerabilities
- Web applications and resources are `compromised` if the server OS is `exploited`

## Popular Database Servers
- MS SQL Server
- MySQL
- Oracle RDBMS
- SAP Sybase ASE
- IBM DB2
- PostgreSQL

### Database Errors
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

## HTTP Methods
- Browser use REQUEST methods to get server to act
    - OPTIONS
        - find out the HTTP methods and options supported by the web server

                OPTIONS * HTTP/1.1
                User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
        
        - Server respond with current configuration of server

                Allow: GET, HEAD, POST, OPTIONS, TRACE

    - `GET`
        - Retrieve data from web server
        - Specify parameters in URL portion of request
        - Used for file retrieval
    - PUT
        - Used to create resources
    - `POST`
        - Update / Modify Resources
    - DELETE
        - Delete files
    - HEAD
        - Retrieve headers
    - TRACE
        - Echo request as seen by server
        - Used for diagnostics
    - CONNECT
        - Establish network connection to web server over HTTP

### Difference Between POST request and PUT request
- `PUT` request is no matter how many times you execute the command, the same result is achieved (idempotent)
- `POST` request result in side effects in terms of duplicated copies of resources


## Software available in Kali Linux and its uses
- Nmap 
    - Server OS Mapping

            nmap -O -

- whatweb 
    - Web Server Mapping

            whatweb -v <http://Website_ip_address>

- Curl Tool
    - Mapping of methods supported by web server

            (Bee Box)
            curl -X OPTIONS <http://Website_ip_address> -i

            (BWAPP)
            curl -X GET <http://Website_ip_address> -i

            (BWAPP)
            curl -d "<document file path>" -X PUT <http://Website_ip_address> -v

            (BWAPP)
            curl -d "<document file path>" -X POST <http://Website_ip_address> -v

            (BWAPP)
            curl -X DELETE <http://Website_ip_address> -v

            curl -X HEAD <http://Website_ip_address> -v

## Web Based Tools
- Netcraft
- urlscan.io

---

## Additional Resources
1. [How to spoof your User Agent](https://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)
2. [HTTPS Status Codes and their meanings](https://www.webfx.com/web-development/glossary/http-status-codes/)