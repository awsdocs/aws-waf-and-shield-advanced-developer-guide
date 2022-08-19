# AWS Shield mitigation logic for CloudFront and Route 53<a name="ddos-event-mitigation-logic-continuous-inspection"></a>

Shield DDoS mitigation continually inspects traffic for CloudFront and Route 53\. These services operate from a globally distributed network of AWS edge locations that provide you with broad access to Shield’s DDoS mitigation capacity and deliver your application from infrastructure that's closer to your end users\. 
+ **CloudFront** – Shield DDoS mitigations only allow traffic that's valid for web applications to pass through to the service\. This provides automatic protection against many common DDoS vectors, like UDP reflection attacks\. 

  CloudFront maintains persistent connections to your application origin, TCP SYN floods are automatically mitigated through integration with the Shield TCP SYN proxy feature, and Transport Layer Security \(TLS\) is terminated at the edge\. These combined features ensure that your application origin only receives well\-formed web requests and that it's protected against lower\-layer DDoS attacks, connection floods, and TLS abuse\.

  CloudFront uses a combination of DNS traffic direction and anycast routing\. These techniques improve the resilience of your application by mitigating attacks close to the source, providing fault isolation, and ensuring access to capacity to mitigate the largest known attacks\. 
+ **Route 53** – Shield mitigations only allow valid DNS requests to reach the service\. Shield mitigates DNS query floods using suspicion scoring that prioritizes known good queries and deprioritizes queries that contain suspicious or known DDoS attack attributes\. 

  Route 53 uses shuffle sharding to provide a unique set of four resolver IP addresses to every hosted zone, for both IPv4 and IPv6\. Each IP address corresponds to a different subset of Route 53 locations\. Each location subset consists of authoritative DNS servers that only partially overlap with infrastructure in any other subset\. This ensures that if a user query fails for any reason, it will be successfully served on retry\.

  Route 53 uses anycast routing to direct DNS queries to the nearest edge location, based on network proximity\. Anycast also fans out DDoS traffic to many edge locations, which prevents attacks from focusing on a single location\. 

In addition to the speed of mitigation, CloudFront and Route 53 provide broad access to the globally distributed capacity of Shield\. To take advantage of these capabilities, use these services as the entry point of your dynamic or static web applications\. 

To learn more about using CloudFront and Route 53 to protect web applications, see [How to Help Protect Dynamic Web Applications Against DDoS Attacks by Using Amazon CloudFront and Amazon Route 53](http://aws.amazon.com/blogs/security/how-to-protect-dynamic-web-applications-against-ddos-attacks-by-using-amazon-cloudfront-and-amazon-route-53/)\. To learn more about fault isolation on Route 53, see [A Case Study in Global Fault Isolation](http://aws.amazon.com/blogs/architecture/a-case-study-in-global-fault-isolation/)\.