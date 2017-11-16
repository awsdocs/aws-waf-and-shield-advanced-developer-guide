# Deleting a Web ACL<a name="web-acl-deleting"></a>

To delete a web ACL, you must remove the rules that are included in the web ACL and disassociate all CloudFront distributions and Application Load Balancers from the web ACL\. Perform the following procedure\.

**To delete a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to delete\.

1. On the **Rules** tab in the right pane, choose **Edit web ACL**\.

1. To remove all rules from the web ACL, choose the **x** at the right of the row for each rule\. This doesn't delete the rules from AWS WAF, it just removes the rules from this web ACL\.

1. Choose **Update**\.

1. Disassociate the web ACL from all CloudFront distributions and Application Load Balancers\. On the **Rules** tab, under **AWS resources using this web ACL**, choose the **x** for each CloudFront distribution or Application Load Balancer\.

1. On the **Web ACLs** page, confirm that the web ACL that you want to delete is selected, and then choose **Delete**\.