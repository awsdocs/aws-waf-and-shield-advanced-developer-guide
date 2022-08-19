# Examples of DDoS attacks<a name="types-of-ddos-attacks"></a>

AWS Shield Advanced provides expanded protection against many types of attacks\. 

The following list describes some common attack types:



**User Datagram Protocol \(UDP\) reflection attacks**  
In UDP reflection attacks, an attacker can spoof the source of a request and use UDP to elicit a large response from the server\. The extra network traffic directed towards the spoofed, attacked IP address can slow the targeted server and prevent legitimate end users from accessing needed resources\.

**TCP SYN flood**  
The intent of an TCP SYN flood attack is to exhaust the available resources of a system by leaving connections in a half\-open state\. When a user connects to a TCP service like a web server, the client sends a TCP SYN packet\. The server returns an acknowledgment, and the client returns its own acknowledgement, completing the three\-way handshake\. In a TCP SYN flood, the third acknowledgment is never returned, and the server is left waiting for a response\. This can prevent other users from connecting to the server\. 

**DNS query flood**  
In a DNS query flood, an attacker uses multiple DNS queries to exhaust the resources of a DNS server\. AWS Shield Advanced can help provide protection against DNS query flood attacks on Route 53 DNS servers\.

**HTTP flood/cache\-busting \(layer 7\) attacks**  
With an HTTP flood, including `GET` and `POST` floods, an attacker sends multiple HTTP requests that appear to be from a real user of the web application\. Cache\-busting attacks are a type of HTTP flood that uses variations in the HTTP request's query string that prevent use of edge\-located cached content and forces the content to be served from the origin web server, causing additional and potentially damaging strain on the origin web server\. 