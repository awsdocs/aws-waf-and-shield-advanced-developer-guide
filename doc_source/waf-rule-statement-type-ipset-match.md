# IP Set Match Rule Statement<a name="waf-rule-statement-type-ipset-match"></a>

The IP set match statement inspects the IP address of a web request's origin against a set of IP addresses and address ranges\. Use this to allow or block web requests based on the IP addresses that the requests originate from\. AWS WAF supports all IPv4 and IPv6 address ranges\. For more information about CIDR notation, see the Wikipedia entry [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\. An IP set can hold up to 10,000 IP addresses or IP address ranges to check\.

**Note**  
Each IP set match rule references an IP set, which you create and maintain independent of your rules\. This allows you to use the single set in multiple rules\. When you update the referenced IP set, AWS WAF automatically updates all rules that reference it\.   
For information about creating and managing an IPSet, see [Creating and Managing an IP Set](waf-ip-set-managing.md)\.

When you add or update the rules in your rule group or web ACL, choose the option **IP set** and select the name of the IP set that you want to use\. 

**Nestable** – You can nest this statement type inside logical rule statements and rate\-based statements\. 

**WCUs** – 1 WCU\. 

This statement requires the following settings: 
+ IP set specification – Choose the IP set that you want to use from the list or create a new one\. 

**Where to find this**
+ **Rule builder** on the console – For **Request option**, choose **Originates from an IP address in**\.
+ **Add my own rules and rule groups** page on the console – Choose the **IP set** option\.
+ **API statement** – `IPSetReferenceStatement`