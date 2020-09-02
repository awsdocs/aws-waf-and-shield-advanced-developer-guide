# Editing an IP set<a name="waf-ip-set-editing"></a>

To add or remove IP addresses or IP address ranges from an IP set or change its description, perform the following procedure\. <a name="web-acl-editing-procedure"></a>

**To edit an IP set**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **IP sets**\.

1. Select the IP set that you want to edit and choose **Edit**\.

1. Modify the IP version and addresses as needed\. In the **IP addresses** text box, you must have one IP address or IP address range per line, in CIDR notation\. AWS WAF supports all IPv4 and IPv6 CIDR ranges except for `/0`\. For more information about CIDR notation, see the Wikipedia article [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\. For addresses, enter one IP address or IP address range per line, in CIDR notation\.

1. Choose **Save changes**\.