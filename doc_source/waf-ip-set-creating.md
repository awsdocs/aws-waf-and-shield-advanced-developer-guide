# Creating an IP set<a name="waf-ip-set-creating"></a>

Follow the procedure in this section to create a new IP set\.

**Note**  
In addition to the procedure in this section, you have the option to add a new IP set when you add an IP match rule to your web ACL or rule group\. Choosing that option requires you to provide the same settings as those required by this procedure\. 

**To create an IP set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **IP sets** and then **Create IP set**\. 

1. Enter a name and description for the IP set\. You'll use these to identify the set when you want to use it\. 
**Note**  
You can't change the name after you create the IP set\.

1. For **Region**, choose the Region where you want to store the IP set\. To use an IP set in web ACLs that protect Amazon CloudFront distributions, you must use Global \(CloudFront\)\. 

1. For **IP version**, select the version you want to use\.

1. In the **IP addresses** text box, enter one IP address or IP address range per line, in CIDR notation\. AWS WAF supports all IPv4 and IPv6 CIDR ranges except for `/0`\. For more information about CIDR notation, see the Wikipedia article [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\.

   Here are some examples:
   + To specify the IPv4 address 192\.0\.2\.44, type **192\.0\.2\.44/32**\.
   + To specify the IPv6 address 0:0:0:0:0:ffff:c000:22c, type **0:0:0:0:0:ffff:c000:22c/128**\.
   + To specify the range of IPv4 addresses from 192\.0\.2\.0 to 192\.0\.2\.255, type **192\.0\.2\.0/24**\.
   + To specify the range of IPv6 addresses from 2620:0:2d0:200:0:0:0:0 to 2620:0:2d0:200:ffff:ffff:ffff:ffff, enter **2620:0:2d0:200::/64**\.

1. Review the settings for the IP set, and choose **Create IP set**\.