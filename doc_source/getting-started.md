# Getting started with AWS WAF<a name="getting-started"></a>

This tutorial shows how to use AWS WAF to perform the following tasks:
+ Set up AWS WAF\.
+ Create a web access control list \(web ACL\) using the wizard in the AWS WAF console\. 
+ Choose the AWS resources that you want AWS WAF to inspect web requests for\. This tutorial covers the steps for Amazon CloudFront\. The process is essentially the same for an Application Load Balancer or Amazon API Gateway REST API\. 
+ Add the rules and rule groups that you want to use to filter web requests\. For example, you can specify the IP addresses that the requests originate from and values in the request that are used only by attackers\. For each rule, you specify whether you want to block matching web requests or allow them\. The rules that are defined inside a rule group have their actions defined inside the rule group\.
+ Specify a default action for the web ACL, either block or allow\. This is the action that AWS WAF takes when a web request doesn't match any of the rules\.

**Note**  
AWS typically bills you less than US $0\.25 per day for the resources that you create during this tutorial\. When you're finished with the tutorial, we recommend that you delete the resources to prevent incurring unnecessary charges\. 

**Topics**
+ [Step 1: Set up AWS WAF](#getting-started-aws-account)
+ [Step 2: Create a Web ACL](#getting-started-wizard-create-web-acl)
+ [Step 3: Add a string match rule](#getting-started-wizard-create-string-condition)
+ [Step 4: Add an AWS Managed Rules rule group](#getting-started-wizard-add-rule-group)
+ [Step 5: Finish your Web ACL configuration](#getting-started-wizard-finish-webacl-options)
+ [Step 6: Clean up your resources](#getting-started-wizard-clean-up)

## Step 1: Set up AWS WAF<a name="getting-started-aws-account"></a>

If you already signed up for an AWS account and created an IAM user as described in [Setting up](setting-up-waf.md), go to [Step 2: Create a Web ACL](#getting-started-wizard-create-web-acl)\.

If not, go to [Setting up](setting-up-waf.md) and perform at least the first two steps\. \(You can skip downloading tools for now because this Getting Started topic focuses on using the AWS WAF console\.\)

## Step 2: Create a Web ACL<a name="getting-started-wizard-create-web-acl"></a>

The AWS WAF console guides you through the process of configuring AWS WAF to block or allow web requests based on conditions that you specify, such as the IP addresses that the requests originate from or values in the requests\. In this step, you create a web ACL\.<a name="getting-started-wizard-create-web-acl-procedure"></a>

**To create a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. If this is your first time using AWS WAF, choose **Go to AWS WAF**, and then choose **Create web ACL**\. 

   If you've used AWS WAF before, choose **Web ACLs** in the navigation pane, and then choose **Create web ACL**\.

1. For **Name**, enter the name that you want to use to identify this web ACL\. 
**Note**  
You can't change the name after you create the web ACL\.

1. \(Optional\) For **Description \- optional**, enter a longer description for the web ACL if you want to\. 

1. For **CloudWatch metric name**, change the default name if applicable\. Follow the guidance on the console for valid characters\. The name can't contain special characters, white space, or metric names reserved for AWS WAF, including "All" and "Default\_Action\."
**Note**  
You can't change the CloudWatch metric name after you create the web ACL\.

1. For **Resource type**, choose **CloudFront distributions**\. The **Region** automatically populates to **Global \(CloudFront\)** for CloudFront distributions\.

1. \(Optional\) For **Associated AWS resources \- optional**, choose **Add AWS resources**\. In the dialog box, choose the resources that you want to associate, and then choose **Add**\. AWS WAF returns you to the **Describe web ACL and associated AWS resources** page\. 

1. Choose **Next**\.

## Step 3: Add a string match rule<a name="getting-started-wizard-create-string-condition"></a>

A string match rule statement identifies strings that you want AWS WAF to search for in a request, such as a specified value in a header or in a query string\. Usually, a string consists of printable ASCII characters, but you can specify any character from hexadecimal 0x00 to 0xFF \(decimal 0 to 255\)\. In this step, you create a rule with a string match statement and indicate what to do with matching requests\. 

**Note**  
For more information about string match rule statements, see [String match rule statement](waf-rule-statement-type-string-match.md)\.<a name="getting-started-wizard-create-string-condition-procedure"></a>

**To create a string match rule statement**

1. On the **Add rules and rule groups** page, choose **Add rules**, **Add my own rules and rule groups**, **Rule builder**, then **Rule visual editor**\. 
**Note**  
The console provides the **Rule visual editor** and also a **Rule JSON editor**\. The JSON editor makes it easy for you to copy configurations between web ACLs and is required for more complex rule sets, like those with multiple levels of nesting\.   
This procedure uses the **Rule visual editor**\. 

1. For **Name**, enter the name that you want to use to identify this rule\. 

1. For **Type** choose **Regular rule**\.

1. For **If a request** choose **matches the statement**\. 

   The other options use the logical statement types for rules, which allow you to combine or negate rule statement results\. 

1. On **Statement**, for **Inspect**, open the dropdown and choose the web request component that you want AWS WAF to look for your string in\. For this example, choose **Header**\.

   When you choose **Header**, you also specify which header you want AWS WAF to inspect\. Enter **User\-Agent**\. \(This value isn't case sensitive\.\)
**Note**  
If you choose to inspect the web request **Body**, AWS WAF inspects only the first 8192 bytes \(8 KB\), because the underlying host service forwards only the first 8192 bytes for inspection\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. AWS WAF gets the length of the body from the request headers\. For more information, see [Size constraint rule statement](waf-rule-statement-type-size-constraint-match.md)\.

1. For **Match type**, choose where the specified string must appear in the `User-Agent` header\. 

   For this example, choose **Exactly matches string**\. This indicates that AWS WAF inspects the user\-agent header in each web request for a string that is identical to the string that you specify\.

1. For **String to match**, specify a string that you want AWS WAF to search for\. The maximum length of **String to match** is 200 characters\. If you want to specify a base64\-encoded value, you can specify up to 200 characters before encoding\.

   For this example, enter **BadBot**\. AWS WAF will inspect the `User-Agent` header in web requests for the value `BadBot`\.

1. Leave **Text transformation** set to **None**\. 

   In an effort to bypass AWS WAF, attackers use unusual formatting in web requests, for example, by adding white space or by URL\-encoding some or all of the request\. Transformations convert the web request to a more standard format by removing white space, by URL\-decoding the request, or by performing other operations that eliminate much of the unusual formatting that attackers commonly use\. You can specify multiple transformations\. AWS WAF processes them all in order before inspecting the web request component\. 

1. For **Action**, select the action you want the rule to take when it matches a web request\. For this example, choose **Count**\. This creates metrics for web requests that match the rule, but doesn't affect whether the rule is allowed or blocked\. For information on your choices, see [AWS WAF rule action](waf-rule-action.md) and [How AWS WAF processes a web ACL](web-acl-processing.md)\.

1. Choose **Add rule**\.

## Step 4: Add an AWS Managed Rules rule group<a name="getting-started-wizard-add-rule-group"></a>

AWS Managed Rules offers a set of managed rule groups for your use, free of charge to AWS WAF customers\. For more information about rule groups, see [Rule groups](waf-rule-groups.md)\. We'll add an AWS Managed Rules rule group to this web ACL\. <a name="getting-started-wizard-add-rule-group-procedure"></a>

**To add an AWS Managed Rules rule group**

1. On the **Add rules and rule groups** page, choose **Add rules**, and then choose **Add managed rule groups**\. 

1. On the **Add managed rule groups** page, expand the listing for the **AWS managed rule groups**\. \(You'll also see listings offered for AWS Marketplace sellers\. You can subscribe to their offerings and then use them in the same way as for AWS Managed Rules rule groups\.\)

1. For the rule group that you want to add, turn on the **Add to web ACL** toggle in the **Action** column\. Also turn on the **Set rules action to count** toggle\. This sets the action for all rules in the rule group to count only\. This allows you to see how the rule group behaves with your web requests before you put it to use\.

1. Choose **Add rules**

1. Choose **Next**\.

## Step 5: Finish your Web ACL configuration<a name="getting-started-wizard-finish-webacl-options"></a>

When you're done adding rules and rule groups to your web ACL configuration, finish up by managing the priority of the rules in the web ACL and configuring settings like metrics, tagging, and logging\. 

**To finish your web ACL configuration**

1. On the **Add rules and rule groups** page, choose **Next**\. 

1. On the **Set rule priority** page, you can see the processing order for the rules and rule groups in the web ACL\. AWS WAF processes them starting from the top\. You can change the processing order by moving them up and down\. To do this, select one in the list and choose **Move up** or **Move down**\.

1. Choose **Next**\.

1. On the **Configure metrics** page, for **Amazon CloudWatch metrics**, you can see the planned metrics for your rules and rule groups\. Deselect any you don't want metrics for\. As needed, change the names of the ones you want metrics for\. For more information about Amazon CloudWatch metrics, see [Monitoring with Amazon CloudWatch](monitoring-cloudwatch.md)\.

1. Choose **Next**\.

1. On the **Review and create web ACL** page, review your settings, then choose **Create web ACL**\. 

The wizard returns you to the **Web ACL** page, where your new web ACL is listed\.

## Step 6: Clean up your resources<a name="getting-started-wizard-clean-up"></a>

You've now successfully completed the tutorial\. To prevent your account from accruing additional AWS WAF charges, clean up the AWS WAF objects that you created\. Alternatively, you can change the configuration to match the web requests that you really want to allow, block, and count\.

**Note**  
AWS typically bills you less than US $0\.25 per day for the resources that you create during this tutorial\. When you're finished, we recommend that you delete the resources to prevent incurring unnecessary charges\. <a name="getting-started-wizard-clean-up-procedure"></a>

**To delete the objects that AWS WAF charges for**

1. In the **Web ACL** page, select your web ACL from the list and choose **Edit**\. 

1. On **Associated AWS resources \- optional**, select all associated resources, and then choose **Remove**\. This disassociates the web ACL from your AWS resources\. 

1. In each of the following screens, choose **Next** until you return to the **Web ACL** page\.

   In the **Web ACL** page, select your web ACL from the list and choose **Delete**\. 

Rules and rule statements don't exist outside of rule group and web ACL definitions\. If you delete a web ACL, this deletes all individual rules that you've defined in the web ACL\. When you remove a rule group from a web ACL, you just remove the reference to it\. 