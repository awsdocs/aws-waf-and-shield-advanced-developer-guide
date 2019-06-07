# Getting Started with AWS WAF<a name="getting-started"></a>

This tutorial shows how to use AWS WAF to perform the following tasks:
+ Set up AWS WAF\.
+ Create a web access control list \(web ACL\) using the AWS WAF console, and specify the conditions that you want to use to filter web requests\. For example, you can specify the IP addresses that the requests originate from and values in the request that are used only by attackers\.
+ Add the conditions to a rule\. Rules let you target the web requests that you want to block or allow\. A web request must match all the conditions in a rule before AWS WAF blocks or allows requests based on the conditions that you specify\.
+ Add the rules to your web ACL\. This is where you specify whether you want to block web requests or allow them based on the conditions that you add to each rule\.
+ Specify a default action, either block or allow\. This is the action that AWS WAF takes when a web request doesn't match any of your rules\.
+ Choose the Amazon CloudFront distribution that you want AWS WAF to inspect web requests for\. This tutorial covers the steps only for CloudFront, but the process for an Application Load Balancer and Amazon API Gateway APIs essentially is the same\. AWS WAF for CloudFront is available for all regions\. AWS WAF for use with API Gateway or an Application Load Balancer is available in the regions listed at [AWS Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#waf_region)\.

**Note**  
AWS typically bills you less than US $0\.25 per day for the resources that you create during this tutorial\. When you're finished with the tutorial, we recommend that you delete the resources to prevent incurring unnecessary charges\. 

**Topics**
+ [Step 1: Set Up AWS WAF](#getting-started-aws-account)
+ [Step 2: Create a Web ACL](#getting-started-wizard-create-web-acl)
+ [Step 3: Create an IP Match Condition](#getting-started-wizard-create-ip-condition)
+ [Step 4: Create a Geo Match Condition](#getting-started-wizard-create-geo-condition)
+ [Step 5: Create a String Match Condition](#getting-started-wizard-create-string-condition)
+ [Step 5A: Create a Regex Condition \(Optional\)](#getting-started-wizard-create-regex-condition)
+ [Step 6: Create a SQL Injection Match Condition](#getting-started-wizard-create-sql-condition)
+ [Step 7: \(Optional\) Create Additional Conditions](#getting-started-wizard-create-optional-conditions)
+ [Step 8: Create a Rule and Add Conditions](#getting-started-wizard-create-rule)
+ [Step 9: Add the Rule to a Web ACL](#getting-started-wizard-add-rule)
+ [Step 10: Clean Up Your Resources](#getting-started-wizard-clean-up)

## Step 1: Set Up AWS WAF<a name="getting-started-aws-account"></a>

If you already signed up for an AWS account and created an IAM user as described in [Setting Up](setting-up-waf.md), go to [Step 2: Create a Web ACL](#getting-started-wizard-create-web-acl)\.

If not, go to [Setting Up](setting-up-waf.md) and perform at least the first two steps\. \(You can skip downloading tools for now because this Getting Started topic focuses on using the AWS WAF console\.\)

## Step 2: Create a Web ACL<a name="getting-started-wizard-create-web-acl"></a>

The AWS WAF console guides you through the process of configuring AWS WAF to block or allow web requests based on conditions that you specify, such as the IP addresses that the requests originate from or values in the requests\. In this step, you create a web ACL\.<a name="getting-started-wizard-create-web-acl-procedure"></a>

**To create a web ACL**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. If this is your first time using AWS WAF, choose **Go to AWS WAF**, and then choose **Configure web ACL**\. 

   If you've used AWS WAF before, choose **Web ACLs** in the navigation pane, and then choose **Create web ACL**\.

1. On the **Name web ACL** page, for **Web ACL name**, type a name\. 
**Note**  
You can't change the name after you create the web ACL\.

1. For **CloudWatch metric name**, type a name\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\)\. It can't contain whitespace\.
**Note**  
You can't change the name after you create the web ACL\.

1. For **Region**, choose a region\. If you will associate this web ACL with a CloudFront distribution, choose **Global \(CloudFront\)**\. 

1. For **AWS resource to associate**, choose the resource that you want to associate with your web ACL, and then choose **Next**\.

## Step 3: Create an IP Match Condition<a name="getting-started-wizard-create-ip-condition"></a>

An IP match condition specifies the IP addresses or IP address ranges that requests originate from\. In this step, you create an IP match condition\. In a later step, you specify whether you want to allow requests or block requests that originate from the specified IP addresses\.

**Note**  
For more information about IP match conditions, see [Working with IP Match Conditions](web-acl-ip-conditions.md)\.<a name="getting-started-wizard-create-ip-condition-procedure"></a>

**To create an IP match condition**

1. On the **Create conditions** page, for **IP match conditions**, choose **Create condition**\.

1. In the **Create IP match condition** dialog box, for **Name**, type a name\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./ \.

1. For **Address**, type **192\.0\.2\.0/24**\. This IP address range, specified in CIDR notation, includes the IP addresses from 192\.0\.2\.0 to 192\.0\.2\.255\. \(The 192\.0\.2\.0/24 IP address range is reserved for examples, so no web requests will originate from these IP addresses\.\)

   AWS WAF supports IPv4 address ranges: /8 and any range between /16 through /32\. AWS WAF supports IPv6 address ranges: /24, /32, /48, /56, /64, and /128\. \(To specify a single IP address, such as 192\.0\.2\.44, type **192\.0\.2\.44/32**\.\) Other ranges aren't supported\.

   For more information about CIDR notation, see the Wikipedia article [Classless Inter\-Domain Routing](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)\.

1. Choose **Create**\.

## Step 4: Create a Geo Match Condition<a name="getting-started-wizard-create-geo-condition"></a>

A geo match condition specifies the country or countries that requests originate from\. In this step, you create a geo match condition\. In a later step, you specify whether you want to allow requests or block requests that originate from the specified countries\.

**Note**  
For more information about geo match conditions, see [Working with Geographic Match Conditions](web-acl-geo-conditions.md)\.<a name="getting-started-wizard-create-geo-condition-procedure"></a>

**To create a geo match condition**

1. On the **Create conditions** page, for **Geo match conditions**, choose **Create condition**\.

1. In the **Create geo match condition** dialog box, for **Name**, type a name\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./ \. 

1. Choose a **Location type** and a country\. **Location type** is currently limited to **Country**\.

1. Choose **Add location**\.

1. Choose **Create**\.

## Step 5: Create a String Match Condition<a name="getting-started-wizard-create-string-condition"></a>

A string match condition identifies the strings that you want AWS WAF to search for in a request, such as a specified value in a header or in a query string\. Usually, a string consists of printable ASCII characters, but you can specify any character from hexadecimal 0x00 to 0xFF \(decimal 0 to 255\)\. In this step, you create a string match condition\. In a later step, you specify whether you want to allow or block requests that contain the specified strings\.

**Note**  
For more information about string match conditions, see [Working with String Match Conditions](web-acl-string-conditions.md)\.<a name="getting-started-wizard-create-string-condition-procedure"></a>

**To create a string match condition**

1. On the **Create conditions** page, for **String match conditions**, choose **Create condition**\.

1. In the **Create string match condition** dialog box, type the following values:  
**Name**  
Type a name\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./ \.  
**Type**  
Choose **String match**\.  
**Part of the request to filter on**  
Choose the part of the web request that you want AWS WAF to inspect for a specified string\.   
For this example, choose **Header**\.  
If you choose **Body** for the value of **Part of the request to filter on**, AWS WAF inspects only the first 8192 bytes \(8 KB\) because CloudFront forwards only the first 8192 bytes for inspection\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. \(AWS WAF gets the length of the body from the request headers\.\) For more information, see [Working with Size Constraint Conditions](web-acl-size-conditions.md)\.  
**Header \(Required if "Part of the request to filter on" is "Header"\)**  
Because you chose **Header** for **Part of the request to filter on**, you must specify which header you want AWS WAF to inspect\. Type **User\-Agent**\. \(This value is not case sensitive\.\)  
**Match type**  
Choose where the specified string must appear in the **User\-Agent** header, for example, at the beginning, at the end, or anywhere in the string\.   
For this example, choose **Exactly matches**, which indicates that AWS WAF inspects web requests for a header value that is identical to the value that you specify\.  
**Transformation**  
In an effort to bypass AWS WAF, attackers use unusual formatting in web requests, for example, by adding whitespace or by URL\-encoding some or all of the request\. Transformations convert the web request to a more standard format by removing whitespace, by URL\-decoding the request, or by performing other operations that eliminate much of the unusual formatting that attackers commonly use\.  
You can only specify a single type of text transformation\.  
For this example, choose **None**\.  
**Value is base64 encoded**  
When the value that you type in **Value to match** is already base64\-encoded, select this check box\.   
For this example, don't select the check box\.  
**Value to match**  
Specify the value that you want AWS WAF to search for in the part of web requests that you indicated in **Part of the request to filter on**\.  
For this example, type **BadBot**\. AWS WAF will inspect the `User-Agent` header in web requests for the value **BadBot**\.  
The maximum length of **Value to match** is 50 characters\. If you want to specify a base64\-encoded value, the limit is 50 characters before encoding\.

1. If you want AWS WAF to inspect web requests for multiple values, such as a `User-Agent` header that contains `BadBot` and a query string that contains `BadParameter`, you have two choices:
   + If you want to allow or block web requests only when they contain both values \(`AND`\), you create one string match condition for each value\. 
   + If you want to allow or block web requests when they contain either value or both \(`OR`\), you add both values to the same string match condition\. 

   For this example, choose **Create**\.

## Step 5A: Create a Regex Condition \(Optional\)<a name="getting-started-wizard-create-regex-condition"></a>

A regular expression condition is a type of string match condition and similar in that it identifies the strings that you want AWS WAF to search for in a request, such as a specified value in a header or in a query string\. The primary difference is that you use a regular expression \(regex\) to specify the string pattern that you want AWS WAF to search for\. In this step, you create a regex match condition\. In a later step, you specify whether you want to allow or block requests that contain the specified strings\.

**Note**  
For more information about regex match conditions, see [Working with Regex Match Conditions](web-acl-regex-conditions.md)\.<a name="getting-started-wizard-create-regex-condition-procedure"></a>

**To create a regex match condition**

1. On the **Create conditions** page, for **String match conditions**, choose **Create condition**\.

1. In the **Create string match condition** dialog box, type the following values:  
**Name**  
Type a name\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\) or the following special characters: \_\-\!"\#`\+\*\},\./ \.  
**Type**  
Choose **Regex match**\.  
**Part of the request to filter on**  
Choose the part of the web request that you want AWS WAF to inspect for a specified string\.   
For this example, choose **Body**\.  
If you choose **Body** for the value of **Part of the request to filter on**, AWS WAF inspects only the first 8192 bytes \(8 KB\) because CloudFront forwards only the first 8192 bytes for inspection\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. \(AWS WAF gets the length of the body from the request headers\.\) For more information, see [Working with Size Constraint Conditions](web-acl-size-conditions.md)\.  
**Transformation**  
In an effort to bypass AWS WAF, attackers use unusual formatting in web requests, for example, by adding whitespace or by URL\-encoding some or all of the request\. Transformations convert the web request to a more standard format by removing whitespace, by URL\-decoding the request, or by performing other operations that eliminate much of the unusual formatting that attackers commonly use\.  
You can only specify a single type of text transformation\.  
For this example, choose **None**\.  
**Regex patterns to match to request**  
Choose **Create regex pattern set**\.  
**New pattern set name**  
Type a name and then specify the regex pattern that you want AWS WAF to search for\.   
Next, type the regular expression **I\[a@\]mAB\[a@\]dRequest**\. AWS WAF will inspect the `User-Agent` header in web requests for the values:  
   + **IamABadRequest**
   + **IamAB@dRequest**
   + **I@mABadRequest**
   + **I@mAB@dRequest**

1. Choose **Create pattern set and add filter**\.

1. Choose **Create**\.

## Step 6: Create a SQL Injection Match Condition<a name="getting-started-wizard-create-sql-condition"></a>

A SQL injection match condition identifies the part of web requests, such as a header or a query string, that you want AWS WAF to inspect for malicious SQL code\. Attackers use SQL queries to extract data from your database\. In this step, you create a SQL injection match condition\. In a later step, you specify whether you want to allow requests or block requests that appear to contain malicious SQL code\.

**Note**  
For more information about string match conditions, see [Working with SQL Injection Match Conditions](web-acl-sql-conditions.md)\.<a name="getting-started-wizard-create-sql-condition-procedure"></a>

**To create a SQL injection match condition**

1. On the **Create conditions** page, for **SQL injection match conditions**, choose **Create condition**\.

1. In the **Create SQL injection match condition** dialog box, type the following values:  
**Name**  
Type a name\.  
**Part of the request to filter on**  
Choose the part of web requests that you want AWS WAF to inspect for malicious SQL code\.   
For this example, choose **Query string**\.  
If you choose **Body** for the value of **Part of the request to filter on**, AWS WAF inspects only the first 8192 bytes \(8 KB\) because CloudFront forwards only the first 8192 bytes for inspection\. To allow or block requests for which the body is longer than 8192 bytes, you can create a size constraint condition\. \(AWS WAF gets the length of the body from the request headers\.\) For more information, see [Working with Size Constraint Conditions](web-acl-size-conditions.md)\.  
**Transformation**  
For this example, choose **URL decode**\.  
Attackers use unusual formatting, such as URL encoding, in an effort to bypass AWS WAF\. The **URL decode** option eliminates some of that formatting in the web request before AWS WAF inspects the request\.  
You can only specify a single type of text transformation\.

1. Choose **Create**\.

1. Choose **Next**\. 

## Step 7: \(Optional\) Create Additional Conditions<a name="getting-started-wizard-create-optional-conditions"></a>

AWS WAF includes other conditions, including the following:
+ **Size constraint conditions** – Identifies the part of web requests, such as a header or a query string, that you want AWS WAF to check for length\. For more information, see [Working with Size Constraint Conditions](web-acl-size-conditions.md)\.
+ **Cross\-site scripting match conditions** – Identifies the part of web requests, such as a header or a query string, that you want AWS WAF to inspect for malicious scripts\. For more information, see [Working with Cross\-site Scripting Match Conditions](web-acl-xss-conditions.md)\.

You can optionally create these conditions now, or you can skip to [Step 8: Create a Rule and Add Conditions](#getting-started-wizard-create-rule)\.

## Step 8: Create a Rule and Add Conditions<a name="getting-started-wizard-create-rule"></a>

You create a rule to specify the conditions that you want AWS WAF to search for in web requests\. If you add more than one condition to a rule, a web request must match all the conditions in the rule for AWS WAF to allow or block requests based on that rule\.

**Note**  
For more information about rules, see [Working with Rules](web-acl-rules.md)\.<a name="getting-started-wizard-create-rule-procedure"></a>

**To create a rule and add conditions**

1. On the **Create rules** page, choose **Create rule**\.

1. In the **Create rule** dialog box, type the following values:  
**Name**  
Type a name\.   
**CloudWatch metric name**  
Type a name for the CloudWatch metric that AWS WAF will create and will associate with the rule\. The name can contain only alphanumeric characters \(A\-Z, a\-z, 0\-9\)\. It can't contain whitespace\.  
**Rule type**  
Choose either `Regular rule` or `Rate based rule`\. Rate based rules are identical to regular rules but also take into account how many requests arrive from the identified IP address every five minutes\. For more information on these rule types, see [How AWS WAF Works](how-aws-waf-works.md)\. For this example, choose `Regular rule`\.  
**Rate limit**  
If you are creating a rate\-based rule, enter the maximum number of requests from a single IP address allowed in a five\-minute period\.

1. For the first condition that you want to add to the rule, specify the following settings:
   + Choose whether you want AWS WAF to allow or block requests based on whether a web request does or does not match the settings in the condition\.

     For this example, choose **does**\.
   + Choose the type of condition that you want to add to the rule: an IP match set condition, a string match set condition, or a SQL injection match set condition\.

     For this example, choose **originate from IP addresses in**\.
   + Choose the condition that you want to add to the rule\.

     For this example, choose the IP match condition that you created in previous tasks\.

1. Choose **Add condition**\.

1. Add the geo match condition that you created earlier\. Specify the following values:
   + **When a request does**
   + **originate from a geographic location in**
   + Choose your geo match condition\.

1. Choose **Add another condition**\.

1. Add the string match condition that you created earlier\. Specify the following values:
   + **When a request does**
   + **match at least one of the filters in the string match condition**
   + Choose your string match condition\.

1. Choose **Add condition**\.

1. Add the SQL injection match condition that you created earlier\. Specify the following values:
   + **When a request does**
   + **match at least one of the filters in the SQL injection match condition**
   + Choose your SQL injection match condition\.

1. Choose **Add condition**\.

1. Add the size constraint condition that you created earlier\. Specify the following values:
   + **When a request does**
   + **match at least one of the filters in the size constraint condition**
   + Choose your size constraint condition\.

1. If you created any other conditions, such as a regex condition, add those in a similar manner\.

1. Choose **Create**\. 

1. For the **Default action**, choose **Allow all requests that don't match any rules**\. 

1. Choose **Review and create**\. 

## Step 9: Add the Rule to a Web ACL<a name="getting-started-wizard-add-rule"></a>

When you add the rule to a web ACL, you specify the following settings:
+ The action that you want AWS WAF to take on web requests that match all the conditions in the rule: allow, block, or count the requests\.
+ The default action for the web ACL\. This is the action that you want AWS WAF to take on web requests that *do not* match all the conditions in the rule: allow or block the requests\.

AWS WAF starts blocking CloudFront web requests that match all the following conditions \(and any others you might have added\):
+ The value of the `User-Agent` header is `BadBot`
+ \(If you created and added the regex condition\) The value of the `Body` is any of the four strings that matches the pattern `I[a@]mAB[a@]dRequest`
+ The requests originate from IP addresses in the range 192\.0\.2\.0\-192\.0\.2\.255
+ The requests originate from country you selected in your geo match condition
+ The requests appear to include malicious SQL code in the query string

AWS WAF allows CloudFront to respond to any requests that don't meet all three of these conditions\. 

## Step 10: Clean Up Your Resources<a name="getting-started-wizard-clean-up"></a>

You've now successfully completed the tutorial\. To prevent your account from accruing additional AWS WAF charges, you should clean up the AWS WAF objects that you created\. Alternatively, you can change the configuration to match the web requests that you really want to allow, block, and count\.

**Note**  
AWS typically bills you less than US $0\.25 per day for the resources that you create during this tutorial\. When you're finished, we recommend that you delete the resources to prevent incurring unnecessary charges\. <a name="getting-started-wizard-clean-up-procedure"></a>

**To delete the objects that AWS WAF charges for**

1. Disassociate your web ACL from your CloudFront distribution:

   1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

   1. Choose the web ACL that you want to delete\.

   1. In the right pane, on the **Rules** tab, go to the **AWS resources using this web ACL** section\. For the CloudFront distribution that you associated the web ACL with, choose the **x** in the **Type** column\. 

1. Remove the conditions from your rule:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the rule that you created during the tutorial\.

   1. Choose **Edit rule**\. 

   1. Choose the **x** at the right of each condition heading\.

   1. Choose **Update**\.

1. Remove the rule from your web ACL, and delete the web ACL:

   1. In the navigation pane, choose **Web ACLs**\.

   1. Choose the web ACL that you created during the tutorial\.

   1. On the **Rules** tab, choose **Edit web ACL**\. 

   1. Choose the **x** at the right of the rule heading\.

   1. Choose **Actions**, and then choose **Delete web ACL**\.

1. Delete your rule:

   1. In the navigation pane, choose **Rules**\.

   1. Choose the rule that you created during the tutorial\.

   1. Choose **Delete**\.

   1. In the **Delete** dialog box, choose **Delete** again to confirm\.

AWS WAF doesn't charge for conditions, but if you want to complete the cleanup, perform the following procedure to remove filters from conditions and delete the conditions\.<a name="getting-started-wizard-clean-up-conditions-procedure"></a>

**To delete filters and conditions**

1. Delete the IP address range in your IP match condition, and delete the IP match condition:

   1. In the navigation pane of the AWS WAF console, choose **IP addresses**\.

   1. Choose the IP match condition that you created during the tutorial\.

   1. Select the check box for the IP address range that you added\. 

   1. Choose **Delete IP address or range**\.

   1. In the **IP match conditions** pane, choose **Delete**\.

   1. In the **Delete** dialog box, choose **Delete** again to confirm\.

1. Delete the filter in your SQL injection match condition, and delete the SQL injection match condition:

   1. In the navigation pane, choose **SQL injection**\.

   1. Choose the SQL injection match condition that you created during the tutorial\.

   1. Select the check box for the filter that you added\. 

   1. Choose **Delete filter**\.

   1. In the **SQL injection match conditions** pane, choose **Delete**\.

   1. In the **Delete** dialog box, choose **Delete** again to confirm\.

1. Delete the filter in your string match condition, and delete the string match condition:

   1. In the navigation pane, choose **String and regex matching**\.

   1. Choose the string match condition that you created during the tutorial\.

   1. Select the check box for the filter that you added\. 

   1. Choose **Delete filter**\.

   1. In the **String match conditions** pane, choose **Delete**\.

   1. In the **Delete** dialog box, choose **Delete** again to confirm\.

1. If you created one, delete the filter in your regex match condition, and delete the regex match condition:

   1. In the navigation pane, choose **String and regex matching**\.

   1. Choose the regex match condition that you created during the tutorial\.

   1. Select the check box for the filter that you added\. 

   1. Choose **Delete filter**\.

   1. In the **Regex match conditions** pane, choose **Delete**\.

   1. In the **Delete** dialog box, choose **Delete** again to confirm\.

1. Delete the filter in your size constraint condition, and delete the size constraint condition:

   1. In the navigation pane, choose **Size constraints**\.

   1. Choose the size constraint condition that you created during the tutorial\.

   1. Select the check box for the filter that you added\. 

   1. Choose **Delete filter**\.

   1. In the **Size constraint conditions** pane, choose **Delete**\.

   1. In the **Delete** dialog box, choose **Delete** again to confirm\.