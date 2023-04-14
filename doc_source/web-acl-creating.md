# Creating a web ACL<a name="web-acl-creating"></a>

To create a new web ACL, use the web ACL creation wizard following the procedure on this page\. 

**Production traffic risk**  
Before you deploy changes in your web ACL for production traffic, test and tune them in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune your updated rules in count mode with your production traffic before enabling them\. For guidance, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**Note**  
Using more than 1,500 WCUs in a web ACL incurs costs beyond the basic web ACL price\. For more information, see [AWS WAF web ACL capacity units \(WCUs\)](aws-waf-capacity-units.md) and [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

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

1. Under **Resource type**, choose the category of AWS resource that you want to associate with this web ACL, either Amazon CloudFront distributions or Regional resources\. For more information, see [Associating or disassociating a web ACL with an AWS resource](web-acl-associating-aws-resource.md)\.

1. For **Region**, if you've chosen a Regional resource type, choose the Region where you want AWS WAF to store the web ACL\. 

   You only need to choose this option for Regional resource types\. For CloudFront distributions, the Region is hard\-coded to the US East \(N\. Virginia\) Region, `us-east-1`, for Global \(CloudFront\) applications\.

1. \(CloudFront distributions only\) For **Web request inspection size limit \- optional**, if you want to specify a different body inspection size limit, select the limit\. Inspecting body sizes over the CloudFront default of 16 KB can incur additional costs\. For information about this option, see [Body inspection size limits for CloudFront web ACLs](web-acl-setting-body-inspection-limit.md)\. 

1. \(Optional\) For **Associated AWS resources \- optional**, if you want to specify your resources now, choose **Add AWS resources**\. In the dialog box, choose the resources that you want to associate, and then choose **Add**\. AWS WAF returns you to the **Describe web ACL and associated AWS resources** page\.

1. Choose **Next**\.

1. \(Optional\) If you want to add managed rule groups, on the **Add rules and rule groups** page, choose **Add rules**, and then choose **Add managed rule groups**\. Do the following for each managed rule group that you want to add:

   1. On the **Add managed rule groups** page, expand the listing for AWS managed rule groups or for the AWS Marketplace seller of your choice\.

   1. For the rule group that you want to add, in the **Action** column, turn on the **Add to web ACL** toggle\. 

      To customize how your web ACL uses the rule group, choose **Edit**\. The following are common customization settings: 
      + Override the rule actions for some or all rules\. If you don't define an override action for a rule, the evaluation uses the rule action that's defined inside the rule group\. For information about this option, see [Action overrides in rule groups](web-acl-rule-group-override-options.md)\. 
      + Reduce the scope of the web requests that the rule group inspects by adding a scope\-down statement\. For information about this option, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.
      + Some managed rule groups require you to provide additional configuration\. See the documentation from your managed rule group provider\. For information specific to the AWS Managed Rules rule groups, see [AWS Managed Rules for AWS WAF](aws-managed-rule-groups.md)\. 

      When you're finished with your settings, choose **Save rule**\.

   Choose **Add rules** to finish adding managed rules and return to the **Add rules and rule groups** page\.

1. \(Optional\) If you want to add your own rule group, on the **Add rules and rule groups** page, choose **Add rules**, and then choose **Add my own rules and rule groups**\. Do the following for each rule group that you want to add:

   1. On the **Add my own rules and rule groups** page, choose **Rule group**\.

   1. For **Name**, enter the name that you want to use for the rule group rule in this web ACL\. 

   1. Choose your rule group from the list, and then choose **Add rule**\.

1. \(Optional\) If you want to add your own rule, on the **Add rules and rule groups** page, choose **Add rules**, **Add my own rules and rule groups**, **Rule builder**, then **Rule visual editor**\. 
**Note**  
The console **Rule visual editor** supports one level of nesting\. For example, you can use a single logical `AND` or `OR` statement and nest one level of other statements inside it, but you can't nest logical statements within logical statements\. To manage more complex rule statements, use the **Rule JSON editor**\. For information about all options for rules, see [Rules](waf-rules.md)\.   
This procedure covers the **Rule visual editor**\. 

   1. For **Name**, enter the name that you want to use to identify this rule\. 

   1. Enter your rule definition, according to your needs\. You can combine rules inside logical `AND` and `OR` rule statements\. The wizard guides you through the options for each rule, according to context\. For information about your rules options, see [Rules](waf-rules.md)\. 

   1. For **Action**, select the action you want the rule to take when it matches a web request\. For information on your choices, see [AWS WAF rule action](waf-rule-action.md) and [Web ACL rule and rule group evaluation](web-acl-processing.md)\.

      If you are using the **CAPTCHA** or **Challenge** action, adjust the **Immunity time** configuration as needed for the rule\. If you don't specify the setting, the rule inherits it from the web ACL\. To modify the web ACL immunity time settings, edit the web ACL after you create it\. For more information about immunity times, see [Timestamp expiration: token immunity times](waf-tokens-immunity-times.md)\.
**Note**  
You are charged additional fees when you use the CAPTCHA or Challenge rule action in one of your rules or as a rule action override in a rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

      If you want to customize the request or response, choose the options for that and fill in the details of your customization\. For more information, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

      If you want to have your rule add labels to matching web requests, choose the options for that and fill in your label details\. For more information, see [Labels on web requests](waf-labels.md)\.

   1. Choose **Add rule**\.

1. Choose the default action for the web ACL, either `Block` or `Allow`\. This is the action that AWS WAF takes on a request when the rules in the web ACL don't explicitly allow or block it\. For more information, see [Deciding on the default action for a web ACL](web-acl-default-action.md)\.

   If you want to customize the default action, choose the options for that and fill in the details of your customization\. For more information, see [Customized web requests and responses in AWS WAF](waf-custom-request-response.md)\.

1. You can define a **Token domain list** to enable token sharing between protected applications\. Tokens are used by the CAPTCHA and Challenge actions and by the application integration SDKs that you implement when you use the AWS Managed Rules rule groups for AWS WAF Fraud Control account takeover prevention \(ATP\) and AWS WAF Bot Control\. 

   Public suffixes aren't allowed\. For example, you can't use `usa.gov` or `co.uk` as a token domain\.

   By default, AWS WAF accepts tokens only for the domain of the protected resource\. If you add token domains in this list, AWS WAF accepts tokens for all domains in the list and for the domain of the associated resource\. For more information, see [Configuring the web ACL token domain list](waf-tokens-domains.md#waf-tokens-domain-lists)\.

1. Choose **Next**\.

1. In the **Set rule priority** page, select and move your rules and rule groups to the order that you want AWS WAF to process them\. AWS WAF processes rules starting from the top of the list\. When you save the web ACL AWS WAF assigns numeric priority settings to the rules, in the order that you have them listed\. For more information, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\. 

1. Choose **Next**\.

1. In the **Configure metrics** page, review the options and apply any updates that you need\. You can combine metrics from multiple sources by providing the same **CloudWatch metric name** for them\. 

1. Choose **Next**\.

1. In the **Review and create web ACL** page, check over your definitions\. If you want to change any area, choose **Edit** for the area\. This returns you to the page in the web ACL wizard\. Make any changes, then choose **Next** through the pages until you come back to the **Review and create web ACL** page\.

1. Choose **Create web ACL**\. Your new web ACL is listed in the **Web ACLs** page\.