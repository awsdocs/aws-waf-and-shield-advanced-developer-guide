# Tutorial: Quickly setting up AWS WAF Classic protection against common attacks<a name="classic-tutorials-common-attacks"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

This tutorial shows you how to use [AWS CloudFormation](https://aws.amazon.com/cloudformation/) to quickly configure AWS WAF Classic to protect against the following common attacks:
+ **Cross\-site scripting attacks** – Attackers sometimes insert scripts into web requests in an effort to exploit vulnerabilities in web applications\. Cross\-site scripting match conditions identify the parts of web requests, such as the URI or the query string, that you want AWS WAF Classic to inspect for possible malicious scripts\.
+ **SQL injection attacks** – Attackers sometimes insert malicious SQL code into web requests in an effort to extract data from your database\. SQL injection match conditions identify the part of web requests that you want AWS WAF Classic to inspect for possible malicious SQL code\.
+ **Attacks from known bad IP addresses** – You can use IP match conditions to allow, block, or count web requests based on the IP addresses that the requests originate from\. An IP match condition lists up to 1,000 IP addresses or IP address ranges that you specify\.

**Note**  
This tutorial assumes that you have a CloudFront distribution that you use to deliver content for your web application\. If you don't have a CloudFront distribution, see [Creating or Updating a Web Distribution Using the CloudFront Console](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html) in the *Amazon CloudFront Developer Guide*\. 

**Topics**
+ [Solution overview](#classic-tutorials-common-attacks-overview)
+ [Step 1: Create an AWS CloudFormation stack that sets up AWS WAF Classic protection against common attacks](#classic-tutorials-common-attacks-cloudformation)
+ [Step 2: Associate a Web ACL with a CloudFront distribution](#classic-tutorials-common-attacks-cloudfront)
+ [Step 3: \(Optional\) add IP addresses to the IP Match Condition](#classic-tutorials-common-attacks-add-ips)
+ [Step 4: \(Optional\) update the Web ACL to block large bodies](#classic-tutorials-common-attacks-block-large-bodies)
+ [Step 5: \(Optional\) delete your AWS CloudFormation stack](#classic-tutorials-common-attacks-delete-stack)
+ [Related resources](#classic-relatedresources)

## Solution overview<a name="classic-tutorials-common-attacks-overview"></a>

AWS CloudFormation uses a template to set up the following AWS WAF Classic conditions, rules, and a web ACL\.

### Conditions<a name="classic-tutorials-common-attacks-overview-conditions"></a>

AWS CloudFormation creates the following conditions\.

**IP Match Condition**  
Filters requests that come from known bad IP addresses\. This lets you easily add IPs to a list to block access to your website\. You might want to do this if you're receiving a lot of bad requests from one or more IP addresses\. If you want to allow, block, or count requests based on the IP addresses that the requests come from, see [Step 3: \(Optional\) add IP addresses to the IP Match Condition](#classic-tutorials-common-attacks-add-ips) later in this tutorial\.  
The name of the condition is *prefix***ManualBlockSet** where *prefix* is the name that you specify for the web ACL when you create the AWS CloudFormation stack\.

**Size Constraint Condition**  
Filters requests for which the body is longer than 8,192 bytes\. AWS WAF Classic evaluates only the first 8,192 bytes of the request part that you specify in a filter\. If valid request bodies never exceed 8,192 bytes, you can use a size constraint condition to catch malicious requests that might otherwise slip through\.  
For this tutorial, AWS CloudFormation configures AWS WAF Classic only to count, not block, requests that have a body longer than 8,192 bytes\. If the body in your requests never exceeds that length, you can change the configuration to block requests that have longer bodies\. For information about how to view the count of requests that exceed 8,192 bytes and how to change the web ACL to block requests that contain bodies larger than 8,192 bytes, see [Step 4: \(Optional\) update the Web ACL to block large bodies](#classic-tutorials-common-attacks-block-large-bodies)\.  
The name of the condition is *prefix***LargeBodyMatch** where *prefix* is the name that you specify for the web ACL when you create the AWS CloudFormation stack\.

**SQL Injection Condition**  
Filters requests that contain possible malicious SQL code\. The condition includes filters that evaluate the following parts of requests:  
+ Query string \(URL decode transformation\)
+ URI \(URL decode transformation\)
+ Body \(URL decode transformation\)
+ Body \(HTML decode transformation\)
The name of the condition is *prefix***SqliMatch** where *prefix* is the name that you specify for the web ACL when you create the AWS CloudFormation stack\.

**Cross\-site Scripting Condition**  
Filters requests that contain possible malicious scripts\. The condition includes filters that evaluate the following parts of requests:  
+ Query string \(URL decode transformation\)
+ URI \(URL decode transformation\)
+ Body \(URL decode transformation\)
+ Body \(HTML decode transformation\)
The name of the condition is *prefix***XssMatch** where *prefix* is the name that you specify for the web ACL when you create the AWS CloudFormation stack\.

### Rules<a name="classic-tutorials-common-attacks-overview-rules"></a>

When you create the AWS CloudFormation stack, AWS CloudFormation creates the following rules and adds the corresponding condition to each rule:

***prefix*ManualIPBlockRule**  
AWS CloudFormation adds the *prefix***ManualBlockSet** condition to this rule\. 

***prefix*SizeMatchRule**  
AWS CloudFormation adds the *prefix***LargeBodyMatch** condition to this rule\.

***prefix*SqliRule**  
AWS CloudFormation adds the *prefix***SqliMatch** condition to this rule\.

***prefix*XssRule**  
AWS CloudFormation adds the *prefix***XssMatch** condition to this rule\.

### Web ACL<a name="classic-tutorials-common-attacks-overview-web-acls"></a>

AWS CloudFormation creates a web ACL that has the name that you specify when you create the AWS CloudFormation stack\. The web ACL contains the following rules with the specified settings: 

***prefix*ManualIPBlockRule**  
By default, the condition in this rule doesn't contain any IP addresses\. If you want to allow, block, or count requests based on the IP addresses that the requests come from, see [Step 3: \(Optional\) add IP addresses to the IP Match Condition](#classic-tutorials-common-attacks-add-ips) later in this tutorial\. 

***prefix*SizeMatchRule**  
By default, AWS WAF Classic counts requests for which the body is longer than 8,192 bytes\.

***prefix*SqliRule**  
AWS WAF Classic blocks requests based on the settings in this rule\.

***prefix*XssRule**  
AWS WAF Classic blocks requests based on the settings in this rule\.

### Requirements<a name="classic-tutorials-common-attacks-overview-requirements"></a>

This tutorial assumes that you have a CloudFront distribution that you use to deliver content for your web application\. If you don't have a CloudFront distribution, see [Creating or Updating a Web Distribution Using the CloudFront Console](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html) in the *Amazon CloudFront Developer Guide*\. This tutorial also uses AWS CloudFormation to simplify the provisioning process\. For more information, see the [AWS CloudFormation User Guide](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/)\.

### Estimated time<a name="classic-tutorials-common-attacks-overview-time"></a>

The estimated time to complete this tutorial is 15 minutes if you already have a CloudFront distribution, or 30 minutes if you need to create a CloudFront distribution\.

### Costs<a name="classic-tutorials-common-attacks-overview-cost"></a>

There is a cost associated with the resources that you create during this tutorial\. You can delete the resources after you finish the tutorial to stop incurring charges\. For more information, see [AWS WAF Classic Pricing](https://aws.amazon.com/waf/pricing/) and [Amazon CloudFront Pricing](http://aws.amazon.com/cloudfront/pricing/)\.

## Step 1: Create an AWS CloudFormation stack that sets up AWS WAF Classic protection against common attacks<a name="classic-tutorials-common-attacks-cloudformation"></a>

In the following procedure, you use an AWS CloudFormation template to create a stack that sets up AWS WAF Classic protection against common attacks\.

**Important**  
You begin to incur charges for the different services when you create the AWS CloudFormation stack that deploys this solution\. Charges continue to accrue until you delete the AWS CloudFormation stack\. For more information, see [Step 5: \(Optional\) delete your AWS CloudFormation stack](#classic-tutorials-common-attacks-delete-stack)\. <a name="classic-tutorials-common-attacks-cloudformation-procedure"></a>

**To create an AWS CloudFormation stack for blocking IP addresses that submit bad requests**

1. To start the process that creates an AWS CloudFormation stack, choose the link for the region in which you want to create AWS resources:
   + [Create a stack in US East \(N\. Virginia\)](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/new)
   + [Create a stack in US West \(Oregon\)](https://us-west-2.console.aws.amazon.com/cloudformation/home?region=us-west-2#/stacks/new)
   + [Create a stack in Europe \(Ireland\)](https://eu-west-1.console.aws.amazon.com/cloudformation/home?region=eu-west-1#/stacks/new)
   + [Create a stack in Asia Pacific \(Tokyo\)](https://ap-northeast-1.console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#/stacks/new)

1. If you are not already signed in to the AWS Management Console, sign in when prompted\. 

1. On the **Specify template** page, choose **Amazon S3 URL**\. For the template URL, type **https://s3\.amazonaws\.com/cloudformation\-examples/community/common\-attacks\.json**\.

1. Choose **Next**\.

1. On the **Specify stack details** page, specify the following values:  
**Stack Name**  
You can use the default name \(**CommonAttackProtection**\), or you can change the name\. The stack name must not contain spaces and must be unique within your AWS account\.   
**Name**  
Specify a name for the web ACL that AWS CloudFormation will create\. The name that you specify is also used as a prefix for the conditions and rules that AWS CloudFormation will create, so you can easily find all the related objects\.

1. Choose **Next**\.

1. \(Optional\) On the **Configure stack options** page, enter tags and advanced settings or leave the boxes blank\.

1. Choose **Next**\.

1. On the **Review** page, review the configuration, and then choose **Create stack**\.

   After you choose **Create stack**, AWS CloudFormation creates the AWS WAF Classic resources that are identified in [Solution overview](#classic-tutorials-common-attacks-overview)\.

## Step 2: Associate a Web ACL with a CloudFront distribution<a name="classic-tutorials-common-attacks-cloudfront"></a>

After AWS CloudFormation creates the stack, you must associate your CloudFront distribution to activate AWS WAF Classic\. 

**Note**  
You can associate a web ACL with as many distributions as you want, but you can associate only one web ACL with a given distribution\.

**To associate a web ACL with a CloudFront distribution**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Go to AWS WAF Classic**\.

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to associate with a CloudFront distribution\.

1. On the **Rules** tab, under **AWS resources using this web ACL**, choose **Add association**\.

1. When prompted, use the **Resource** list to choose the distribution that you want to associate this web ACL with\.

1. Choose **Add**\.

1. To associate this web ACL with additional CloudFront distributions, repeat steps 4 through 6\.

## Step 3: \(Optional\) add IP addresses to the IP Match Condition<a name="classic-tutorials-common-attacks-add-ips"></a>

When you created the AWS CloudFormation stack, AWS CloudFormation created an IP match condition for you, added it to a rule, added the rule to a web ACL, and configured the web ACL to block requests based on IP addresses\. The IP match condition doesn't include any IP addresses, though\. If you want to block requests based on IP addresses, perform the following procedure\. <a name="classic-tutorials-common-attacks-cloudformation-parameters-procedure"></a>

**To edit AWS CloudFormation parameter values**

1. Open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **IP addresses**\.

1. In the **IP match conditions** pane, choose the IP match condition that you want to edit\.

1. To add an IP address range:

   1. In the right pane, choose **Add IP address or range**\.

   1. Type an IP address or range by using CIDR notation\. Here are two examples:
      + To specify the IP address 192\.0\.2\.44, type **192\.0\.2\.44/32**\.
      + To specify the range of IP addresses from 192\.0\.2\.0 to 192\.0\.2\.255, type **192\.0\.2\.0/24**\.

      AWS WAF Classic supports IPv4 address ranges: /8 and any range between /16 through /32\. AWS WAF Classic supports IPv6 address ranges: /24, /32, /48, /56, /64, and /128\. For more information about CIDR notation, see the Wikipedia entry [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\.
**Note**  
AWS WAF Classic supports both IPv4 and IPv6 IP addresses\.

   1. To add more IP addresses, choose **Add another IP address**, and then type the value\.

   1. Choose **Add**\.

## Step 4: \(Optional\) update the Web ACL to block large bodies<a name="classic-tutorials-common-attacks-block-large-bodies"></a>

When you created the AWS CloudFormation stack, AWS CloudFormation created a size constraint condition that filters requests that have request bodies longer than 8,192 bytes\. It also added the condition to a rule, and added the rule to the web ACL\. In this example, AWS CloudFormation configured the web ACL to count requests, not to block requests\. This is useful when you want to confirm you are not blocking valid requests inadvertently\. 

If you want to block requests that are longer than 8,192 bytes, perform the following procedure\.<a name="classic-tutorials-common-attacks-block-large-bodies-procedure"></a>

**To change the action for a rule in a web ACL**

1. Open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to edit\.

1. In the right pane, choose the **Rules** tab\.

1. Choose **Edit Web ACL**\.

1. To change the action for the *prefix***LargeBodyMatchRule**, choose the preferred option\. \(*prefix* is the value that you specified for the name of the web ACL\.\)

1. Choose **Save changes**\.

## Step 5: \(Optional\) delete your AWS CloudFormation stack<a name="classic-tutorials-common-attacks-delete-stack"></a>

If you want to stop protecting from common attacks as described in [Solution overview](#classic-tutorials-common-attacks-overview), delete the AWS CloudFormation stack that you created in [Step 1: Create an AWS CloudFormation stack that sets up AWS WAF Classic protection against common attacks](#classic-tutorials-common-attacks-cloudformation)\. This deletes the AWS WAF Classic resources that AWS CloudFormation created and stops the AWS charges for those resources\. 

**To delete an AWS CloudFormation stack**

1. Sign in to the AWS Management Console and open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. Select the check box for the stack\. The default name is **CommonAttackProtection**\.

1. Choose **Delete Stack**\.

1. Choose **Yes, Delete** to confirm\.

1. To track the progress of the stack deletion, select the check box for the stack, and choose the **Events** tab in the bottom pane\.

## Related resources<a name="classic-relatedresources"></a>

For AWS WAF Classic samples, including Lambda functions, AWS CloudFormation templates, and SDK usage examples, go to GitHub at [https://github.com/awslabs/aws-waf-sample](https://github.com/awslabs/aws-waf-sample)\. 