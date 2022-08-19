# Installing the AWS WAF mobile SDK<a name="waf-mobile-sdk-installing"></a>

Implement the mobile SDK first in a test environment, then in production\.

**To install the AWS WAF mobile SDK**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Application integration**\. This takes you to the **Application integration SDKs** page\.

1. In the **Application integration SDKs** page, do the following: 

   1. In the pane **Web ACLs that are enabled for application integration**, locate the web ACL that you're integrating with\. Copy and save the web ACL integration URL for use in your implementation\. You can also obtain this URL through the API call `GetWebACL`\.

   1. Choose the mobile device type and version, then choose **Download**\. You can choose any version you like, but we recommend using the latest version\. AWS WAF downloads the `zip` file for your device to your standard download location\.

1. In your app development environment, unzip the file to a work location of your choice\. In the top\-level directory of the zip file, locate and open the `README`\. Follow the instructions in the `README` file to install the AWS WAF mobile SDK for use in your mobile app code\. 

1. Program your app according to the guidance in the following sections\.