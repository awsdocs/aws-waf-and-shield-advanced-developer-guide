# Deleting a web ACL<a name="web-acl-deleting"></a>

To delete a web ACL, you first disassociate all AWS resources from the web ACL\. Perform the following procedure\.

**To delete a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Select the name of the web ACL that you want to delete\. The console takes you to the web ACL's description, where you can edit it\.

1. On the **Associated AWS resources** tab, for each associated resource, select the radio button next to the resource name and then choose **Disassociate**\. This disassociates the web ACL from your AWS resources\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Select the radio button next to the web ACL that you are deleting, and then choose **Delete**\.