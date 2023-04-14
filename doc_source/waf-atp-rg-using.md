# Adding the ATP managed rule group to your web ACL<a name="waf-atp-rg-using"></a>

To configure the ATP managed rule group to recognize account takeover activities in your web traffic, you provide information about how clients send login requests to your application\. For protected Amazon CloudFront distributions, you also provide information about how your application responds to login requests\. This configuration is in addition to the normal configuration for a managed rule group\. 

For the rule group description and rules listing, see [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\.

**Note**  
The ATP stolen credentials database only contains usernames in email format\.

This guidance is intended for users who know generally how to create and manage AWS WAF web ACLs, rules, and rule groups\. Those topics are covered in prior sections of this guide\. 

**Follow best practices**  
Use the ATP rule group in accordance with the best practices at [Best practices for intelligent threat mitigation](waf-managed-protections-best-practices.md)\. 

**To use the `AWSManagedRulesATPRuleSet` rule group in your web ACL**

1. Add the AWS managed rule group, `AWSManagedRulesATPRuleSet` to your web ACL, and **Edit** the rule group settings before saving\. 
**Note**  
You are charged additional fees when you use this managed rule group\. For more information, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.
**Note**  
For basic information about how to add a managed rule group to your web ACL, see [Adding a managed rule group to a web ACL through the console](waf-using-managed-rule-group.md)\.

1. In the **Rule group configuration** pane, provide the information that the ATP rule group uses to inspect login requests\. 

   1. For **Login path**, provide the path of the login endpoint for your application\. For example, for the URL `https://example.com/web/login`, you would provide the path `/web/login`\. Login paths that start with the path that you provide are considered a match\. For example `/web/login` matches the login paths `/web/login`, `/web/login/`, `/web/loginPage`, and `/web/login/thisPage`, but doesn't match the login path `/home/web/login` or `/website/login`\. 

      The rule group inspects only HTTP `POST` requests to your specified login endpoint\.

   1. For **Request inspection**, specify how your application accepts login attempts by providing the request payload type and the names of the fields within the request body where the username and password are provided\. Your specification of the field names depends on the payload type\.
      + **JSON payload type** – Specify the field names in JSON pointer syntax\. For information about the JSON Pointer syntax, see the Internet Engineering Task Force \(IETF\) documentation [JavaScript Object Notation \(JSON\) Pointer](https://tools.ietf.org/html/rfc6901)\. 

        For example, for the following example JSON payload, the username field specification is `/login/username` and the password field specification is `/login/password`\.

        ```
        {
            "login": {
                "username": "THE_USERNAME",
                "password": "THE_PASSWORD"
            }
        }
        ```
      + **FORM\_ENCODED payload type** – Use the HTML form names\.

        For example, for an HTML form with input elements named `username1` and `password1`, the username field specification is `username1` and the password field specification is `password1`\.

   1. If you're protecting Amazon CloudFront distributions, then under **Response inspection**, specify how your application indicates success or failure in its responses to login attempts\. 
**Note**  
ATP response inspection is available only in web ACLs that protect CloudFront distributions\.

      Specify a single component in the login response that you want ATP to inspect\. For the **Body** and **JSON** component types, AWS WAF can inspect the first 65,536 bytes \(64 KB\) of the component\. 

      Provide your inspection criteria for the component type, as indicated by the interface\. You must provide both success and failure criteria to inspect for in the component\. 

      For example, say your application indicates the status of a login attempt in the status code of the response, and uses `200 OK` for success and `401 Unauthorized` or `403 Forbidden` for failure\. You would set the response inspection **Component type** to **Status code**, then in the **Success** text box enter `200` and in the **Failure** text box, enter `401` on the first line and `403` on the second\.

      The ATP rule group only counts responses that match your success or failure inspection criteria\. The rule group rules act on clients while they have too high a failure rate among the responses that are counted\. For accurate behavior by the rule group rules, be sure to provide complete information for both successful and failed login attempts\. 

      To see the rules that inspect login responses, look for `VolumetricIpFailedLoginResponseHigh` and `VolumetricSessionFailedLoginResponseHigh` in the rules listing at [AWS WAF Fraud Control account takeover prevention \(ATP\) rule group](aws-managed-rule-groups-atp.md)\. 

1. Provide any additional configuration that you want for the rule group\. 

   You can further limit the scope of requests that the rule group inspects by adding a scope\-down statement to the managed rule group statement\. For example, you can inspect only requests with a specific query argument or cookie\. The rule group will inspect only HTTP `POST` requests to your specified login endpoint that match the criteria in your scope\-down statement\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

1. Save your changes to the web ACL\. 

Before you deploy your ATP implementation for production traffic, test and tune it in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune the rules in count mode with your production traffic before enabling them\. See the section that follows for guidance\. 