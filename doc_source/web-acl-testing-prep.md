# Preparing for testing<a name="web-acl-testing-prep"></a>

This section describes how to get set up to test and tune your AWS WAF protections\. 

**Note**  
To follow the guidance in this section, you need to understand generally how to create and manage AWS WAF protections like web ACLs, rules, and rule groups\. That information is covered in earlier sections of this guide\.

**To prepare for testing**

1. 

**Enable web ACL logging, Amazon CloudWatch metrics, and web request sampling for the web ACL**

   Use logging, metrics, and sampling to monitor the interaction of the web ACL rules with your web traffic\. 
   + **Logging** – You can configure AWS WAF to log the web requests that a web ACL evaluates\. You can send logs to CloudWatch logs, an Amazon S3 bucket, or an Amazon Kinesis Data Firehose\. You can redact fields and apply filtering\. For more information, see [Logging web ACL traffic](logging.md)\. 
   + **Amazon CloudWatch metrics** – In your web ACL configuration, provide metric specifications for everything that you want to monitor\. You can view metrics through the AWS WAF and CloudWatch consoles\. For more information, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\. 
   + **Web request sampling** – You can view a sample of all web requests that your web ACL evaluates\. For information about web request sampling, see [Viewing a sample of web requests](web-acl-testing-view-sample.md)\. 

1. 

**Set your protections to `Count` mode**

   In your web ACL configuration, switch anything that you want to test to count mode\. This causes the test protections to record matches against web requests without altering how the requests are handled\. You'll be able to see the matches in your metrics, logs, and sampled requests, to verify the match criteria and to understand what the effects might be on your web traffic\. Rules that add labels to matching requests will add labels regardless of the rule action\. 
   + **Rule defined in the web ACL** – Edit the rules in the web ACL and set their actions to `Count`\. 
   + **Rule group** – In your web ACL configuration, edit the rule statement for the rule group and set the rule actions to `Count`\. If you manage the web ACL in JSON, add the rule to the `ExcludedRules` list in the rule group reference statement\. For more information, see [Setting rule actions to count in a rule group](web-acl-rule-group-settings.md#web-acl-rule-group-rule-to-count)\.

     For your own rule group, don't modify the rule actions in the rule group itself\. Rule group rules with `Count` action don't generate the metrics or other artifacts that you need for your testing\. Also, changing a rule group affects all web ACLs that use it, while the changes inside the web ACL configuration only affect the single web ACL\. 
   + **Web ACL** – If you're testing a new web ACL, set the default action for the web ACL to allow requests\. This lets you try out the web ACL without affecting traffic in any way\. 

   In general, count mode reports more matches than production\. This is because a rule that counts requests doesn't stop the evaluation of the request by the web ACL, so rules that run later in the web ACL might also match the request\. When you change your rule actions to their production settings, rules that allow or block requests will terminate the evaluation of requests that they match\. As a result, matching requests will generally be inspected by fewer rules in the web ACL\. For more information about the effects of rule actions on the overall evaluation of a web request, see [AWS WAF rule action](waf-rule-action.md)\. 

   With these settings, your new protections won't alter web traffic, but will generate match information in metrics, web ACL logs, and request samples\. 

1. 

**Associate the web ACL with a resource**

   If the web ACL isn't already associated with the resource, associate it\. 

   See [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

You're now ready to monitor and tune your web ACL\. 