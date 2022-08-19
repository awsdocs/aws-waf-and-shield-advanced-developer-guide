# Installing the AWS WAF JavaScript SDK<a name="waf-javascript-sdk-installing"></a>

Implement the JavaScript SDK first in a test environment, then in production\.

**To begin using the JavaScript SDK**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the navigation pane, choose **Application integration**\. This takes you to the **Application integration SDKs** page\.

1. In the **Application integration SDKs** page, in the pane **Web ACLs that are enabled for application integration**, locate the web ACL that you're integrating with\. Copy and save the web ACL integration URL for use in your implementation\. You can also obtain this URL through the API call `GetWebACL`\.

1. In your application page code, in the `<head>` section, insert the following `<script>` tag, and populate it with your web ACL's integration URL\. This inclusion causes your client application to automatically retrieve a token in the background on page load\. 

   ```
   <script type="text/javascript" src="Web ACL integration URL/challenge.js” defer></script>
   ```

   This `<script>` listing is configured with the `defer` attribute, but you can change the setting to `async` if you want a different behavior for your page\. 

1. Complete coding your integration to ensure that token retrieval completes before the client's login request is sent\. If you are already using the `fetch` API to make your call, you can substitute the AWS WAF integration `fetch` wrapper\. If you don't use the `fetch` API, you can use the AWS WAF integration `getToken` operation instead\. 

   For coding guidance, see the following sections\. 