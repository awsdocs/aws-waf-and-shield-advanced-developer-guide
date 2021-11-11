# Creating a web ACL<a name="web-acl-creating"></a><a name="web-acl-creating-procedure"></a>

**To create a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Web ACLs** in the navigation pane, and then choose **Create web ACL**\.

1. For **Name**, enter the name that you want to use to identify this web ACL\. 
**Note**  
You can't change the name after you create the web ACL\.

1. \(Optional\) For **Description \- optional**, enter a longer description for the web ACL if you want to\. 

1. For **CloudWatch metric name**, change the default name if applicable\. Follow the guidance on the console for valid characters\. The name can't contain special characters, white space, or metric names reserved for AWS WAF, including "All" and "Default\_Action\."
**Note**  
You can't change the CloudWatch metric name after you create the web ACL\.

1. For **Resource type**, choose the category of AWS resource that you want to associate with this web ACL\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. For **Region**, if you've chosen a Regional resource type, choose the Region where you want AWS WAF to store the web ACL\. 

   You only need to choose this option for Regional resource types\. For CloudFront distributions, the Region is hard\-coded to the US East \(N\. Virginia\) Region, `us-east-1`, for Global \(CloudFront\) applications\.

1. \(Optional\) For **Associated AWS resources \- optional**, choose **Add AWS resources**\. In the dialog box, choose the resources that you want to associate, and then choose **Add**\. AWS WAF returns you to the **Describe web ACL and associated AWS resources** page\. 

1. Choose **Next**\.

1. \(Optional\) If you want to add managed rule groups, on the **Add rules and rule groups** page, choose **Add rules**, and then choose **Add managed rule groups**\. Do the following for each managed rule group that you want to add:

   1. On the **Add managed rule groups** page, expand the listing for AWS managed rule groups or for the AWS Marketplace seller of your choice\.

   1. For the rule group that you want to add, turn on the **Add to web ACL** toggle in the **Action** column\. 

      If you want to set the actions for any rules in the rule group to count only, choose **Edit**, then either turn on the **Count** toggle for individual rules or turn on the **Set all rules actions to count** toggle\. Choose **Save rule**\. For information about this option, see [Overriding the actions of a rule group or its rules](web-acl-rule-group-override-options.md)\. 

   Choose **Add rules** to finish adding managed rules and return to the **Add rules and rule groups** page\.

1. \(Optional\) If you want to add your own rule group, on the **Add rules and rule groups** page, choose **Add rules**, and then choose **Add my own rules and rule groups**\. Do the following for each rule group that you want to add:

   1. On the **Add my own rules and rule groups** page, choose **Rule group**\.

   1. For **Name**, enter the name that you want to use for the rule group rule in this web ACL\. 

   1. Choose your rule group from the list, and then choose **Add rule**\.

1. \(Optional\) If you want to add your own rule, on the **Add rules and rule groups** page, choose **Add rules**, **Add my own rules and rule groups**, **Rule builder**, then **Rule visual editor**\. 
**Note**  
The console **Rule visual editor** supports one level of nesting\. For example, you can use a single logical `AND` or `OR` statement and nest one level of other statements inside it, but you can't nest logical statements within logical statements\. To manage more complex rule statements, use the **Rule JSON editor**\. For information about all options for rules, see [AWS WAF rules](waf-rules.md)\.   
This procedure covers the **Rule visual editor**\. 

   1. For **Name**, enter the name that you want to use to identify this rule\. 

   1. Enter your rule definition, according to your needs\. You can combine rules inside logical `AND` and `OR` rule statements\. The wizard guides you through the options for each rule, according to context\. For information about your rules options, see [AWS WAF rules](waf-rules.md)\. 

   1. For **Action**, select the action you want the rule to take when it matches a web request\. For information on your choices, see [AWS WAF rule action](waf-rule-action.md) and [Web ACL rule and rule group evaluation](web-acl-processing.md)\.

      If you are using the **CAPTCHA** action, adjust the **Immunity time** configuration as needed for this rule\. For more information, see [CAPTCHA tokens and token expiration](waf-captcha-how-it-works.md#waf-captcha-tokens)\.

      If you want to customize the request or response, choose the options for that and fill in the details of your customization\. For more information, see [Customizing web requests and responses in AWS WAF](waf-custom-request-response.md)\.

      If you want to have your rule add labels to matching web requests, choose the options for that and fill in your label details\. For more information, see [AWS WAF labels on web requests](waf-rule-labels.md)\.

   1. Choose **Add rule**\.

1. Choose the default action for the web ACL\. This is the action that AWS WAF takes when a web request doesn't match any of the rules in the web ACL\. For more information, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\.

   If you want to customize the default action, choose the options for that and fill in the details of your customization\. For more information, see [Customizing web requests and responses in AWS WAF](waf-custom-request-response.md)\.

1. Choose **Next**\.

1. In the **Set rule priority** page, select and move your rules and rule groups to the order that you want AWS WAF to process them\. For more information, see [Web ACL rule and rule group evaluation](web-acl-processing.md)\. 

1. Choose **Next**\.

1. In the **Configure metrics** page, review the options and apply any updates that you need\. You can combine metrics from multiple sources by providing the same **CloudWatch metric name** for them\. 

1. Choose **Next**\.

1. In the **Review and create web ACL** page, check over your definitions\. If you want to change any area, choose **Edit** for the area\. This returns you to the page in the web ACL wizard\. Make any changes, then choose **Next** through the pages until you come back to the **Review and create web ACL** page\.

1. Choose **Create web ACL**\. Your new web ACL is listed in the **Web ACLs** page\.