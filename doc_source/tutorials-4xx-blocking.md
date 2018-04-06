# Tutorial: Blocking IP Addresses That Submit Bad Requests<a name="tutorials-4xx-blocking"></a>

Using [AWS Lambda](https://aws.amazon.com/lambda/), you can set a threshold of how many bad requests per minute your web application will tolerate from a given IP address\. A bad request is one for which your CloudFront origin returns one of the following HTTP 40x status codes:
+ 400, Bad Request
+ 403, Forbidden
+ 404, Not Found
+ 405, Method Not Allowed

If users \(based on IP addresses\) exceed this error code threshold, Lambda automatically updates your AWS WAF rules to block IP addresses and specify for how long requests from those IP addresses should be blocked\.

This tutorial shows you how to use an [AWS CloudFormation](https://aws.amazon.com/cloudformation/) template to specify the request threshold and time to block requests\. The tutorial also uses CloudFront [access logs](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/AccessLogs.html) \(stored in [Amazon S3](https://aws.amazon.com/s3/)\) to count requests as they are served by [CloudFront](https://aws.amazon.com/cloudfront/) and by [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) metrics\.

**Topics**
+ [Solution Overview](#tutorials-4xx-blocking-overview)
+ [Step 1: Create an AWS CloudFormation Stack for Blocking IP Addresses That Submit Bad Requests](#tutorials-4xx-blocking-cloudformation)
+ [Step 2: Associate a Web ACL with a CloudFront Distribution](#tutorials-4xx-blocking-cloudfront)
+ [Step 3: \(Optional\) Edit AWS CloudFormation Parameter Values](#tutorials-4xx-blocking-cloudformation-parameters)
+ [Step 4: \(Optional\) Test Your Thresholds and IP Rules](#tutorials-4xx-blocking-test)
+ [Step 5: \(Optional\) Delete Your AWS CloudFormation Stack](#tutorials-4xx-blocking-delete-stack)
+ [Related Resources](#relatedresources_1)

## Solution Overview<a name="tutorials-4xx-blocking-overview"></a>

The following illustration shows how you can use AWS WAF with AWS Lambda to block requests from specific IP addresses\.

![\[Solution Overview: Blocking IP Addresses that Submit Bad Requests\]](http://docs.aws.amazon.com/waf/latest/developerguide/images/tutorial-4xx-blacklist.png)

1. As CloudFront receives requests on behalf of your web application, it sends access logs to an Amazon S3 bucket that contains detailed information about the requests\.

1. For every new access log stored in the Amazon S3 bucket, a Lambda function is triggered\. The Lambda function parses the log files and looks for requests that resulted in error codes 400, 403, 404, and 405\. The function then counts the number of bad requests and temporarily stores results in `current_outstanding_requesters.json` in the Amazon S3 bucket that you're using for access logs\.

1. The Lambda function updates AWS WAF rules to block the IP addresses that are listed in `current_outstanding_requesters.json` for a period of time that you specify\. After this blocking period has expired, AWS WAF allows those IP addresses to access your application again, but continues to monitor the requests from those IP addresses\.

1. The Lambda function publishes execution metrics in CloudWatch, such as the number of requests analyzed and IP addresses blocked\.

The AWS CloudFormation template creates a web access control list \(web ACL\) and two separate rules in AWS WAF that block and monitor requests from IP addresses, depending on the settings that you configure during the tutorial\. The two rules are defined here: 
+ **Auto Block** – This rule adds IP addresses that exceed the request\-per\-minute limit\. New requests from those IP addresses are blocked until Lambda removes the IP addresses from the block list after the specified expiration period\. The default is four hours\.
+ **Manual Block** – This rule adds IP addresses manually to the auto\-block list\. The IP addresses are permanently blocked; they can access the web application only if you remove them from the block list\. You can use this list to block known bad IP addresses or IP addresses that frequently are added to the auto\-block rule\.

**Requirements:** This tutorial assumes that you already have a CloudFront distribution that you use to deliver content for your web application\. If you don't have a CloudFront distribution, see [Creating or Updating a Web Distribution Using the CloudFront Console](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-creating-console.html) in the *Amazon CloudFront Developer Guide*\. This tutorial also uses AWS CloudFormation to simplify the provisioning process\. For more information, see the [AWS CloudFormation User Guide](http://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/)\.

**Estimated time:** 15 minutes if you already have a CloudFront distribution, or 30 minutes if you need to create a CloudFront distribution\.

**Estimated cost:**
+ **AWS WAF**
  + $5\.00 per month per web ACL \(the tutorial creates one web ACL\)
  + $1\.00 per month per rule \(x2 for the two rules that AWS CloudFormation creates for this tutorial\)
  + $0\.60 per million requests
+ **AWS Lambda** – Each new CloudFront access log represents a new request and triggers the Lambda function that is created by this tutorial\. Lambda charges include the following:
  + **Requests** – The first million requests are free, and then Lambda charges $0\.20 per million requests\. CloudFront delivers access logs for a distribution up to several times an hour\. 
  + **Memory used per second** – $0\.00001667 per GB of memory used per second\.
+ **Amazon S3** – Amazon S3 charges for storing CloudFront access logs\. The size of the logs and, therefore, the charge for storage depends on the number of requests that CloudFront receives for your objects\. For more information, see [Amazon S3 Pricing](https://aws.amazon.com/s3/pricing/)\.
+ **CloudFront** – You don't incur any additional CloudFront charges for this solution\. For more information, see [Amazon CloudFront Pricing](http://aws.amazon.com/cloudfront/pricing/)\.

## Step 1: Create an AWS CloudFormation Stack for Blocking IP Addresses That Submit Bad Requests<a name="tutorials-4xx-blocking-cloudformation"></a>

In the following procedure, you use an AWS CloudFormation template to create a stack that launches the AWS resources required by Lambda, CloudFront, Amazon S3, AWS WAF, and CloudWatch\.

**Important**  
You begin to incur charges for the different services when you create the AWS CloudFormation stack that deploys this solution\. Charges continue to accrue until you delete the AWS CloudFormation stack\. For more information, see [Step 5: \(Optional\) Delete Your AWS CloudFormation Stack](#tutorials-4xx-blocking-delete-stack)\. <a name="tutorials-4xx-blocking-cloudformation-procedure"></a>

**To create an AWS CloudFormation stack for blocking IP addresses that submit bad requests**

1. To start the process that creates an AWS CloudFormation stack, choose the link for the region in which you want to create AWS resources:
   + [Create a stack in US East \(N\. Virginia\)](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#cstack=sn%7eBadBehavingIP%7cturl%7ehttps:%2f%2fs3.amazonaws.com/awswaf.us-east-1/block-bad-behaving-ips/block-bad-behaving-ips_template.json)
   + [Create a stack in US West \(Oregon\)](https://console.aws.amazon.com/cloudformation/home?region=us-west-2#cstack=sn%7eBadBehavingIP%7cturl%7ehttps:%2f%2fs3.amazonaws.com/awswaf.us-west-2/block-bad-behaving-ips/block-bad-behaving-ips_template.json)
   + [Create a stack in EU \(Ireland\)](https://console.aws.amazon.com/cloudformation/home?region=eu-west-1#cstack=sn%7eBadBehavingIP%7cturl%7ehttps:%2f%2fs3.amazonaws.com/awswaf.eu-west-1/block-bad-behaving-ips/block-bad-behaving-ips_template.json)
   + [Create a stack in Asia Pacific \(Tokyo\)](https://console.aws.amazon.com/cloudformation/home?region=ap-northeast-1#cstack=sn%7eBadBehavingIP%7cturl%7ehttps:%2f%2fs3.amazonaws.com/awswaf.ap-northeast-1/block-bad-behaving-ips/block-bad-behaving-ips_template.json)

1. If you are not already signed in to the AWS Management Console, sign in when prompted\. 

1. On the **Select Template** page, the selected URL automatically appears under **Specify an Amazon S3 template URL**\. Choose **Next**\.

1. On the **Specify Details** page, specify the following values:  
**Stack Name**  
You can use the default name \(**BadBehavingIP**\), or you can change the name\. The stack name must not contain spaces and must be unique within your AWS account\.   
**Create CloudFront Access Log Bucket**  
Select **yes** to create a new Amazon S3 bucket for CloudFront access logs, or select **no** if you already have an Amazon S3 bucket for CloudFront access logs\.  
**CloudFront Access Log Bucket Name**  
Type the name of the Amazon S3 bucket where you want CloudFront to put access logs\. Leave this box empty if you selected **no** for **Create CloudFront Access Log Bucket**\.  
**Request Threshold**  
Type the maximum number of requests that can be made from an IP address per minute without being blocked\. The default is 400\.  
**WAF Block Period**  
Specify how long \(in minutes\) an IP address should be blocked after crossing the threshold\. The default is 240 minutes \(four hours\)\.

1. Choose **Next**\.

1. \(Optional\) On the **Options** page, enter tags and advanced settings or leave the boxes blank\.

1. Choose **Next**\.

1. On the **Review** page, select the **I acknowledge** check box, and then choose **Create**\.

   After you choose **Create**, AWS CloudFormation creates the AWS resources that are necessary to run the solution:
   + Lambda function
   + AWS WAF web ACL \(named **Malicious Requesters**\) with the necessary rules configured
   + CloudWatch custom metric
   + Amazon S3 bucket with the name that you specified in the **CloudFront Access Log Bucket Name** field in step 6, if you selected **yes** for **Create CloudFront Access Log Bucket**

## Step 2: Associate a Web ACL with a CloudFront Distribution<a name="tutorials-4xx-blocking-cloudfront"></a>

After AWS CloudFormation creates the stack, you must associate the CloudFront distribution to activate AWS WAF and update your Amazon S3 bucket to enable event notification\. 

**Note**  
If you're already using AWS WAF to monitor CloudFront requests and if logging is already enabled for the distribution that you're monitoring, you can skip the first procedure\.

**Note**  
You can associate a web ACL with as many distributions as you want, but you can associate only one web ACL with a given distribution\.

**To associate a web ACL with a CloudFront distribution**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Web ACLs**\.

1. Choose the web ACL that you want to associate with a CloudFront distribution\.

1. On the **Rules** tab, under **AWS resources using this web ACL**, choose **Add association**\.

1. When prompted, use the **Resource** list to choose the distribution that you want to associate this web ACL with\.

1. Choose **Add**\.

1. To associate this web ACL with additional CloudFront distributions, repeat steps 4 through 6\.

If you already have an Amazon S3 bucket for CloudFront access logs \(if you selected **no** for **Create CloudFront Access Log Bucket** in the preceding procedure\), enable Amazon S3 event notification to trigger the Lambda function when a new log file is added to the bucket\. For more information, see [Enabling Event Notifications](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/SettingBucketNotifications.html) in the *Amazon Simple Storage Service Console User Guide*\.

**Note**  
If you chose to have AWS CloudFormation create the bucket for you, AWS CloudFormation also enabled event notifications for the bucket\. 

**To enable Amazon S3 event notification**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket that you want to use for CloudFront access logs\.

1. Choose **Properties**, and expand **Events**\.

1. Specify the following values:  
**Name**  
Type a name for the event, such as **LambdaNotificationsForWAFBadRequests**\. The name cannot contain spaces\.  
**Events**  
Select **ObjectCreated \(All\)**\.  
**Prefix**  
Leave the field empty\.  
**Suffix**  
Type **gz**\.  
**Send To**  
Select **Lambda function**\.  
**Lambda function**  
Choose **BadBehavingIP** or the name that you specified for your AWS CloudFormation stack\.

1. Choose **Save**\.

## Step 3: \(Optional\) Edit AWS CloudFormation Parameter Values<a name="tutorials-4xx-blocking-cloudformation-parameters"></a>

If you want to change the parameters after you create the AWS CloudFormation stack—for example, if you want to change the threshold value or how long IPs are blocked—you can update the AWS CloudFormation stack\.<a name="tutorials-4xx-blocking-cloudformation-parameters-procedure"></a>

**To edit AWS CloudFormation parameter values**

1. Open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. In the list of stacks, choose the running stack that you want to update, which is **BadBehavingIP** if you accepted the default value when you created the stack\.

1. Choose **Actions**, and then choose **Update Stack**\.

1. On the **Select Template** page, select **Use current template**, and then choose **Next**\.

1. On the **Specify Details** page, change the values of **Error Code Blacklisting Parameters** as applicable:  
**Request Threshold**  
Type the new maximum number of requests that can be made per minute without being blocked\.  
**WAF Block Period**  
Specify the new value of how long \(in minutes\) that you want AWS WAF to block the IP address after the number of requests from that IP address exceed the value of **Request Threshold**\.

1. On the **Options** page, choose **Next**\.

1. On the **Review** page, select the **I acknowledge** check box, and then choose **Update**\.

   AWS CloudFormation updates the stack to reflect the new values of the parameters\.

## Step 4: \(Optional\) Test Your Thresholds and IP Rules<a name="tutorials-4xx-blocking-test"></a>

To test your solution, you can wait until CloudFront generates a new access log file, or you can simulate this process by uploading a sample access log into the Amazon S3 bucket that you specified for receiving log files\.<a name="tutorials-4xx-blocking-test-thresholds-procedure"></a>

**To test your thresholds and IP rules**

1. Download the sample CloudFront [access log file](https://s3.amazonaws.com/awswaf.us-east-1/block-bad-behaving-ips/access_log_sample.gz) from the AWS website\.

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the Amazon S3 bucket that you're using for CloudFront access logs for this tutorial\.

1. Choose **Upload**\.

1. Choose **Add Files**, choose the sample access log file, and then choose **Start Upload**\.

After the upload finishes, perform the following procedure to confirm that the IP addresses were populated automatically in the AWS WAF **Auto Block** rule\. Lambda takes a few seconds to process the log file and update the rule\.<a name="tutorials-4xx-blocking-test-review-ip-addresses-procedure"></a>

**To review IP addresses in the **Auto Block** rule**

1. Open the AWS WAF console at [https://console\.aws\.amazon\.com/waf/](https://console.aws.amazon.com/waf/)\. 

1. In the navigation pane, choose **Rules**\.

1. Choose the **Auto Block** rule\.

1. Confirm that the **Auto Block** rule includes an IP match condition that contains IP addresses\.

## Step 5: \(Optional\) Delete Your AWS CloudFormation Stack<a name="tutorials-4xx-blocking-delete-stack"></a>

If you want to stop blocking IP addresses that submit bad requests, delete the AWS CloudFormation stack that you created in [Step 1: Create an AWS CloudFormation Stack for Blocking IP Addresses That Submit Bad Requests](#tutorials-4xx-blocking-cloudformation)\. This deletes the AWS resources that AWS CloudFormation created and stops the AWS charges for those resources\. 

**To delete an AWS CloudFormation stack**

1. Sign in to the AWS Management Console and open the AWS CloudFormation console at [https://console\.aws\.amazon\.com/cloudformation](https://console.aws.amazon.com/cloudformation/)\.

1. Select the check box for the stack\. The default name is **BadBehavingIP**\.

1. Choose **Delete Stack**\.

1. Choose **Yes, Delete** to confirm\.

1. To track the progress of the stack deletion, select the check box for the stack, and then choose the **Events** tab in the bottom pane\.

## Related Resources<a name="relatedresources_1"></a>

For AWS WAF samples, including Lambda functions, AWS CloudFormation templates, and SDK usage examples, go to GitHub at [https://github.com/awslabs/aws-waf-sample](https://github.com/awslabs/aws-waf-sample)\.