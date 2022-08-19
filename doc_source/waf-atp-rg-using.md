# Using the ATP managed rule group<a name="waf-atp-rg-using"></a>

The ATP managed rule group `AWSManagedRulesATPRuleSet` requires additional configuration that allows it to recognize and handle account takeover activities in your web traffic\. This configuration information is specific to your web request handling\. 

This guidance is intended for users who know generally how to create and manage AWS WAF web ACLs, rules, and rule groups\. Those topics are covered in prior sections of this guide\. 

**To use the `AWSManagedRulesATPRuleSet` rule group in your web ACL**

1. Add the AWS managed rule group, `AWSManagedRulesATPRuleSet` to your web ACL, and edit the rule group settings when you add it\. 
**Note**  
For basic information about how to add a managed rule group to your web ACL, see [Adding a managed rule group to a web ACL through the console](waf-using-managed-rule-group.md)\.

1. The ATP managed rule group requires information about your application's login page that allows it to monitor, label, and handle login attempts to your application\. You provide this configuration in addition to any of the standard managed rule group configuration settings that you might want to apply\. 

   In the **Rule group configuration** pane, provide the following information about your application's login page\. 
   + For **Login path**, provide the path of the login endpoint for your application\. For example, for the URL `https://example.com/web/login`, you would provide the path `/web/login`\.

     The rule group inspects only HTTP `POST` requests to your specified login endpoint\.
   + For **Payload type**, select either JSON or form encoded\. 
   + For **Username field** and **Password field**, enter the field names within the request body where the username and password are provided\. 

     Your specification of these field names depends on the payload type that you've selected:
     + For JSON payloads, specify the field names in JSON pointer syntax\. For information about the JSON Pointer syntax, see the Internet Engineering Task Force \(IETF\) documentation [JavaScript Object Notation \(JSON\) Pointer](https://tools.ietf.org/html/rfc6901)\. 

       For example, for the following example JSON payload, the username field specification is `/login/username` and the password field specification is `/login/password`\.

       ```
       {
           "login": {
               "username": "THE_USERNAME",
               "password": "THE_PASSWORD"
           }
       }
       ```
     + For form encoded payloads, use the HTML form names\.

       For example, for an HTML form with input elements named `username1` and `password1`, the username field specification is `username1` and the password field specification is `password1`\.

1. Provide any additional configuration that you want for the rule group\. 

   You can further limit the scope of requests that the rule group inspects by adding a scope\-down statement to the managed rule group statement\. For example, you can inspect only requests with a specific query argument or cookie\. The rule group will inspect only HTTP `POST` requests that match the criteria in your scope\-down statement\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

1. Save your changes to the web ACL\. 

You can use the ATP managed rule group as you would any other AWS Managed Rules rule group\. 

For enhanced detection capabilities, we recommend that you integrate the AWS WAF ATP JavaScript SDK into your browser login page\. AWS WAF also provides mobile SDKs to integrate iOS and Android devices\. For more information about the integration SDKs, see [AWS WAF client application integration](waf-application-integration.md)\. 