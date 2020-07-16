# Setting up<a name="setting-up-waf"></a>

This topic describes preliminary steps, such as creating an AWS account, to prepare you to use AWS WAF, AWS Firewall Manager, and AWS Shield Advanced\. You are not charged to set up this account and other preliminary items\. You are charged only for AWS services that you use\. 

After you complete these steps, see [Getting started with AWS WAF](getting-started.md) to continue getting started with AWS WAF\.

**Note**  
AWS Shield Standard is included with AWS WAF and does not require additional setup\. For more information, see [How AWS Shield works](ddos-overview.md)\.

Before you use AWS WAF or AWS Shield Advanced for the first time, complete the following tasks:
+ [Step 1: Sign up for an AWS account](#setting-up-waf-aws-account)
+ [Step 2: Create an IAM user](#setting-up-waf-iam)
+ [Step 3: Download tools](#setting-up-waf-tools)

## Step 1: Sign up for an AWS account<a name="setting-up-waf-aws-account"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS, including AWS WAF\. You are charged only for the services that you use\.

If you have an AWS account already, skip to the next task\. If you don't have an AWS account, use the following procedure to create one\.

**To sign up for AWS**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Note your AWS account number, because you'll need it for the next task\.

## Step 2: Create an IAM user<a name="setting-up-waf-iam"></a>

To use the AWS WAF console, you must sign in to confirm that you have permission to perform AWS WAF operations\. You can use the root credentials for your AWS account, but we don't recommend it\. For greater security and control of your account, we recommend that you use AWS Identity and Access Management \(IAM\) to do the following:
+ Create an IAM user account for yourself or your business\.
+ Either add the IAM user account to an IAM group that has administrative permissions, or grant administrative permissions directly to the IAM user account\.
+ Verify that the account has full access to AWS WAF and related services, for general use and for console access\. For information, see [AWS managed \(predefined\) policies for AWS WAF](access-control-identity-based.md#access-policy-examples-aws-managed)\.

You then can sign in to the AWS WAF console \(and other service consoles\) by using a special URL and the credentials for the IAM user\. You also can add other users to the IAM user account, and control their level of access to AWS services and to your resources\.

**Note**  
For information about creating access keys to access AWS WAF by using the [AWS Command Line Interface](http://aws.amazon.com/cli/) \(AWS CLI\), [Tools for Windows PowerShell](http://aws.amazon.com/documentation/powershell), the [AWS SDKs](http://aws.amazon.com/tools/), or the AWS WAF API, see [Managing Access Keys for IAM Users](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html)\.

If you signed up for AWS but have not created an IAM user for yourself, you can create one using the IAM console\. If you aren't familiar with using the console, see [Working with the AWS Management Console](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/getting-started.html) for an overview\. 

**To create an administrator user for yourself and add the user to an administrators group \(console\)**

1. Sign in to the [IAM console](https://console.aws.amazon.com/iam/) as the account owner by choosing **Root user** and entering your AWS account email address\. On the next page, enter your password\.
**Note**  
We strongly recommend that you adhere to the best practice of using the **Administrator** IAM user below and securely lock away the root user credentials\. Sign in as the root user only to perform a few [account and service management tasks](https://docs.aws.amazon.com/general/latest/gr/aws_tasks-that-require-root.html)\.

1. In the navigation pane, choose **Users** and then choose **Add user**\.

1. For **User name**, enter **Administrator**\.

1. Select the check box next to **AWS Management Console access**\. Then select **Custom password**, and then enter your new password in the text box\.

1. \(Optional\) By default, AWS requires the new user to create a new password when first signing in\. You can clear the check box next to **User must create a new password at next sign\-in** to allow the new user to reset their password after they sign in\.

1. Choose **Next: Permissions**\.

1. Under **Set permissions**, choose **Add user to group**\.

1. Choose **Create group**\.

1. In the **Create group** dialog box, for **Group name** enter **Administrators**\.

1. Choose **Filter policies**, and then select **AWS managed \-job function** to filter the table contents\.

1. In the policy list, select the check box for **AdministratorAccess**\. Then choose **Create group**\.
**Note**  
You must activate IAM user and role access to Billing before you can use the `AdministratorAccess` permissions to access the AWS Billing and Cost Management console\. To do this, follow the instructions in [step 1 of the tutorial about delegating access to the billing console](https://docs.aws.amazon.com/IAM/latest/UserGuide/tutorial_billing.html)\.

1. Back in the list of groups, select the check box for your new group\. Choose **Refresh** if necessary to see the group in the list\.

1. Choose **Next: Tags**\.

1. \(Optional\) Add metadata to the user by attaching tags as key\-value pairs\. For more information about using tags in IAM, see [Tagging IAM Entities](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_tags.html) in the *IAM User Guide*\.

1. Choose **Next: Review** to see the list of group memberships to be added to the new user\. When you are ready to proceed, choose **Create user**\.

You can use this same process to create more groups and users and to give your users access to your AWS account resources\. To learn about using policies that restrict user permissions to specific AWS resources, see [Access Management](https://docs.aws.amazon.com/IAM/latest/UserGuide/access.html) and [Example Policies](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies_examples.html)\.

To sign in as this new IAM user, first sign out of the AWS console\. Then use the following URL, where *your\_aws\_account\_id* is your AWS account number without the hyphens\. For example, if your AWS account number is `1234-5678-9012`, your AWS account ID is `123456789012`:

```
https://your_aws_account_id.signin.aws.amazon.com/console/
```

Enter the IAM user name and password that you just created\. When you're signed in, the navigation bar displays "*your\_user\_name* @ *your\_aws\_account\_id*"\.

If you don't want the URL for your sign\-in page to contain your AWS account ID, you can create an account alias\. From the IAM dashboard, choose **Customize** and enter an alias, such as your company name\. To sign in after you create an account alias, use the following URL:

```
https://your_account_alias.signin.aws.amazon.com/console/
```

To verify the sign\-in link for IAM users for your account, open the IAM console and check under the **IAM users sign\-in link** on the dashboard\. 

After you complete these steps, you can stop here and go to [Getting started with AWS WAF](getting-started.md) to continue getting started with AWS WAF using the console\. If you want to access AWS WAF programmatically using the AWS WAF API, continue on to the next step, [Step 3: Download tools](#setting-up-waf-tools)\.

## Step 3: Download tools<a name="setting-up-waf-tools"></a>

The AWS Management Console includes a console for AWS WAF, but if you want to access AWS WAF programmatically, the following documentation and tools will help you:
+ If you want to call the AWS WAF API without having to handle low\-level details like assembling raw HTTP requests, you can use an AWS SDK\. The AWS SDKs provide functions and data types that encapsulate the functionality of AWS WAF and other AWS services\. To download an AWS SDK, see the applicable page, which also includes prerequisites and installation instructions:
  + [Java](https://aws.amazon.com/sdk-for-java/)
  + [JavaScript](http://aws.amazon.com/sdkforbrowser/)
  + [\.NET](https://aws.amazon.com/sdk-for-net/)
  + [Node\.js](https://aws.amazon.com/sdk-for-node-js/)
  + [PHP](https://aws.amazon.com/sdk-for-php/)
  + [Python](https://github.com/boto/boto)
  + [Ruby](https://aws.amazon.com/sdk-for-ruby/)

  For a complete list of AWS SDKs, see [Tools for Amazon Web Services](http://aws.amazon.com/tools/)\.
+ If you're using a programming language for which AWS doesn't provide an SDK, the [AWS WAF API Reference](https://docs.aws.amazon.com/waf/latest/APIReference/) documents the operations that AWS WAF supports\. 
+ The AWS Command Line Interface \(AWS CLI\) supports AWS WAF\. The AWS CLI lets you control multiple AWS services from the command line and automate them through scripts\. For more information, see [AWS Command Line Interface](https://aws.amazon.com/cli/)\.
+ AWS Tools for Windows PowerShell supports AWS WAF\. For more information, see [AWS Tools for PowerShell Cmdlet Reference](http://aws.amazon.com/documentation/powershell/)\.