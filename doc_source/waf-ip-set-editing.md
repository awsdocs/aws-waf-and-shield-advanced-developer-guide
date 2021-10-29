# Editing an IP set<a name="waf-ip-set-editing"></a>

To add or remove IP addresses or IP address ranges from an IP set or change its description, perform the following procedure\. <a name="web-acl-editing-procedure"></a>

**To edit an IP set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **IP sets**\.

1. Select the IP set that you want to edit and choose **Edit**\.

1. Modify the IP version and addresses as needed\. In the **IP addresses** text box, you must have one IP address or IP address range per line, in CIDR notation\. AWS WAF supports all IPv4 and IPv6 CIDR ranges except for `/0`\. For more information about CIDR notation, see the Wikipedia article [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\. For addresses, enter one IP address or IP address range per line, in CIDR notation\.

   Here are some examples:
   + To specify the IPv4 address 192\.0\.2\.44, type **192\.0\.2\.44/32**\.
   + To specify the IPv6 address 0:0:0:0:0:ffff:c000:22c, type **0:0:0:0:0:ffff:c000:22c/128**\.
   + To specify the range of IPv4 addresses from 192\.0\.2\.0 to 192\.0\.2\.255, type **192\.0\.2\.0/24**\.
   + To specify the range of IPv6 addresses from 2620:0:2d0:200:0:0:0:0 to 2620:0:2d0:200:ffff:ffff:ffff:ffff, enter **2620:0:2d0:200::/64**\.

1. Choose **Save changes**\.