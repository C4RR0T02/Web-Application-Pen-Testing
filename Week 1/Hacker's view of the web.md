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

200s: `Success codes` returned when browser request is recieved, understood and processed by the server

300s: `Redirection codes` returned when a new resource has been substituted for the requested resource

400s: Client eroor codes indicating that there was a `problem with the request`

500s: Server error codes indicating that the request was accepted, but that `an error on the server` prevented the fulfillment of the request

---

## Additional Resources
1. [How to spoof your User Agent](https://www.howtogeek.com/113439/how-to-change-your-browsers-user-agent-without-installing-any-extensions/)
2. [HTTPS Status Codes and their meanings](https://www.webfx.com/web-development/glossary/http-status-codes/)