# Activity 1.1

When a pen-tester point the URL of his Firefox browser to https://www.ibm.com

The communications between his browser and the IBM servers were captured and given in the next five slides, separate them as `REQUEST` or `RESPONSE` message. 

Using the `ZAP Proxy Tool`, show the intercepted HTTP Request and Response Header

---

## OWASP ZAP Proxy

1. Ensure Kali VM is in `NAT`

![](activity1.1_images/VM-NAT-Config.png)  

2. Start an OWASP ZAP Proxy Session

![](activity1.1_images/OWASPZAP-Start-Session.png)  

3. Start a `Manual Exploration`

![](activity1.1_images/Manual-Exploration.png)  

4. Key in the website to manually explore

![](activity1.1_images/Manual-Explore-IBM.png)  

5. Notice the browser information is captured by the server in the `REQUEST` and the `RESPONSE` is a redirect status code

#### HTTP Request

![](activity1.1_images/OWASPZAP-Browser-Information-Capture-Request.png)  

#### HTTP Response

![](activity1.1_images/OWASPZAP-Browser-Information-Capture-Response.png) 

6. Notice that within the packet of the Redirect status code there is another redirect status code in the `RESPONSE`

![](activity1.1_images/OWASPZAP-Redirect-Status-Code-1.png)  

7. Notice that within the packet of the Redirect status code there is another redirect status code in the `RESPONSE`

![](activity1.1_images/OWASPZAP-Redirect-Status-Code-2.png)  

8. Notice that within the packet of the Redirect status code there is another redirect status code in the `RESPONSE`

![](activity1.1_images/OWASPZAP-Redirect-Status-Code-3.png)  

9. Notice on recieving a `200 OK` status code, the server type, link and the html code is returned

![](activity1.1_images/OWASPZAP-OK-Status-Code.png)  

---

# Additional Resources
1. [Types of VM Network connections](https://docs.vmware.com/en/VMware-Workstation-Pro/16.0/com.vmware.ws.using.doc/GUID-3B504F2F-7A0B-415F-AE01-62363A95D052.html)
2. [HTTPS Status Codes and their meanings](https://www.webfx.com/web-development/glossary/http-status-codes/)
3. [HTTPS Server Redirection - How it works](https://developer.mozilla.org/en-US/docs/Web/HTTP/Redirections)