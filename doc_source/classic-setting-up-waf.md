# Setting up AWS WAF Classic<a name="classic-setting-up-waf"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

This topic describes preliminary steps, such as creating a user account, to prepare you to use AWS WAF Classic\. You aren't charged for these\. You are charged only for AWS services that you use\. 

**Note**  
If you're a new user to AWS WAF, don't follow these setup steps for AWS WAF Classic\. Instead, follow the steps for the latest version of AWS WAF, at [Setting up](setting-up-waf.md)\. 

After you complete these steps, see [Getting started with AWS WAF Classic](classic-getting-started.md) to continue getting started with AWS WAF Classic\.

**Note**  
AWS Shield Standard is included with AWS WAF Classic and does not require additional setup\. For more information, see [How AWS Shield works](ddos-overview.md)\.

Before you use AWS WAF Classic or AWS Shield Advanced for the first time, complete the steps in this section\. 

**Topics**
+ [Sign up for an AWS account](#sign-up-for-aws)
+ [Create an administrative user](#create-an-admin)
+ [Download tools](#classic-setting-up-waf-tools)

## Sign up for an AWS account<a name="sign-up-for-aws"></a>

If you do not have an AWS account, complete the following steps to create one\.

**To sign up for an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

   When you sign up for an AWS account, an *AWS account root user* is created\. The root user has access to all AWS services and resources in the account\. As a security best practice, [assign administrative access to an administrative user](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html), and use only the root user to perform [tasks that require root user access](https://docs.aws.amazon.com/accounts/latest/reference/root-user-tasks.html)\.

AWS sends you a confirmation email after the sign\-up process is complete\. At any time, you can view your current account activity and manage your account by going to [https://aws\.amazon\.com/](https://aws.amazon.com/) and choosing **My Account**\.

## Create an administrative user<a name="create-an-admin"></a>

After you sign up for an AWS account, create an administrative user so that you don't use the root user for everyday tasks\.

**Secure your AWS account root user**

1.  Sign in to the [AWS Management Console](https://console.aws.amazon.com/) as the account owner by choosing **Root user** and entering your AWS account email address\. On the next page, enter your password\.

   For help signing in by using root user, see [Signing in as the root user](https://docs.aws.amazon.com/signin/latest/userguide/console-sign-in-tutorials.html#introduction-to-root-user-sign-in-tutorial) in the *AWS Sign\-In User Guide*\.

1. Turn on multi\-factor authentication \(MFA\) for your root user\.

   For instructions, see [Enable a virtual MFA device for your AWS account root user \(console\)](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa_enable_virtual.html#enable-virt-mfa-for-root) in the *IAM User Guide*\.

**Create an administrative user**
+ For your daily administrative tasks, grant administrative access to an administrative user in AWS IAM Identity Center \(successor to AWS Single Sign\-On\)\.

  For instructions, see [Getting started](https://docs.aws.amazon.com/singlesignon/latest/userguide/getting-started.html) in the *AWS IAM Identity Center \(successor to AWS Single Sign\-On\) User Guide*\.

**Sign in as the administrative user**
+ To sign in with your IAM Identity Center user, use the sign\-in URL that was sent to your email address when you created the IAM Identity Center user\.

  For help signing in using an IAM Identity Center user, see [Signing in to the AWS access portal](https://docs.aws.amazon.com/signin/latest/userguide/iam-id-center-sign-in-tutorial.html) in the *AWS Sign\-In User Guide*\.

## Download tools<a name="classic-setting-up-waf-tools"></a>

The AWS Management Console includes a console for AWS WAF Classic, but if you want to access AWS WAF Classic programmatically, see the following:
+ If you want to call the AWS WAF Classic API without having to handle low\-level details like assembling raw HTTP requests, you can use an AWS SDK\. The AWS SDKs provide functions and data types that encapsulate the functionality of AWS WAF Classic and other AWS services\. To download an AWS SDK, see the applicable page, which also includes prerequisites and installation instructions:
  + [Java](https://aws.amazon.com/sdk-for-java/)
  + [JavaScript](http://aws.amazon.com/sdkforbrowser/)
  + [\.NET](https://aws.amazon.com/sdk-for-net/)
  + [Node\.js](https://aws.amazon.com/sdk-for-node-js/)
  + [PHP](https://aws.amazon.com/sdk-for-php/)
  + [Python](https://github.com/boto/boto)
  + [Ruby](https://aws.amazon.com/sdk-for-ruby/)

  For a complete list of AWS SDKs, see [Tools for Amazon Web Services](http://aws.amazon.com/tools/)\.
+ If you're using a programming language for which AWS doesn't provide an SDK, the [AWS WAF API Reference](https://docs.aws.amazon.com/waf/latest/APIReference/) documents the operations that AWS WAF Classic supports\. 
+ The AWS Command Line Interface \(AWS CLI\) supports AWS WAF Classic\. The AWS CLI lets you control multiple AWS services from the command line and automate them through scripts\. For more information, see [AWS Command Line Interface](https://aws.amazon.com/cli/)\.
+ AWS Tools for Windows PowerShell supports AWS WAF Classic\. For more information, see [AWS Tools for PowerShell Cmdlet Reference](http://aws.amazon.com/documentation/powershell/)\.