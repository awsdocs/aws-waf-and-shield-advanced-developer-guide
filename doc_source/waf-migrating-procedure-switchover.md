# Migrating a web ACL: switchover<a name="waf-migrating-procedure-switchover"></a>

After you've verified your new web ACL settings, you can start to use it in place of your AWS WAF Classic web ACL\. 

**Note**  
You might encounter a brief disruption as you change the resource association to the new web ACL\.

**To begin using your new AWS WAF web ACL**

1. Associate the AWS WAF web ACL with the resources that you want to protect, following the guidance at [Associating or disassociating a Web ACL with an AWS resource](web-acl-associating-aws-resource.md)\. This automatically disassociates the resources from the old web ACL\. 

1. Configure logging for the new web ACL, following the guidance at [Logging Web ACL traffic information](logging.md)\. 

1. \(Optional\) If your AWS WAF Classic web ACL is no longer associated with any resources, consider removing it entirely from AWS WAF Classic\. For information, see [Deleting a Web ACL](classic-web-acl-deleting.md)\.