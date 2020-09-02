# IP set match rule statement<a name="waf-rule-statement-type-ipset-match"></a>

The IP set match statement inspects the IP address of a web request against a set of IP addresses and address ranges\. Use this to allow or block web requests based on the IP addresses that the requests originate from\. By default, AWS WAF uses the IP address from the web request origin, but you can configure the rule to use an HTTP header like `X-Forwarded-For` instead\. 

AWS WAF supports all IPv4 and IPv6 CIDR ranges except for `/0`\. For more information about CIDR notation, see the Wikipedia entry [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\. An IP set can hold up to 10,000 IP addresses or IP address ranges to check\.

**Note**  
Each IP set match rule references an IP set, which you create and maintain independent of your rules\. This allows you to use the single set in multiple rules\. When you update the referenced IP set, AWS WAF automatically updates all rules that reference it\.   
For information about creating and managing an IP set, see [Creating and managing an IP set](waf-ip-set-managing.md)\.

When you add or update the rules in your rule group or web ACL, choose the option **IP set** and select the name of the IP set that you want to use\. 

**Nestable** – You can nest this statement type inside logical rule statements and rate\-based statements\. 

**WCUs** – 1 WCU for most\. If you configure the statement to use forwarded IP addresses and specify a position of `ANY`, the WCU usage is 5\.

This statement uses the following settings: 
+ **IP set specification** – Choose the IP set that you want to use from the list or create a new one\. 
+ **\(Optional\) Forwarded IP configuration** – An alternate forwarded IP header name to use in place of the request origin\. You specify whether to match against the first, last, or any address in the header\. You also specify a fallback behavior to apply to a web request with a malformed IP address in the specified header\. The fallback behavior sets the matching result for the request, to match or no match\. For more information, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. 

**Where to find this**
+ **Rule builder** on the console – For **Request option**, choose **Originates from an IP address in**\.
+ **Add my own rules and rule groups** page on the console – Choose the **IP set** option\.
+ **API statement** – `IPSetReferenceStatement`