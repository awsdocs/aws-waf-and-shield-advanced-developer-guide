# Using your rule group in a web ACL<a name="waf-rule-group-using"></a>

To use a rule group in a web ACL, you add it to the web ACL in a rule group reference statement\. 

**Production traffic risk**  
Before you deploy changes in your web ACL for production traffic, test and tune them in a staging or testing environment until you are comfortable with the potential impact to your traffic\. Then test and tune your updated rules in count mode with your production traffic before enabling them\. For guidance, see [Testing and tuning your AWS WAF protections](web-acl-testing.md)\.

**Note**  
Using more than 1,500 WCUs in a web ACL incurs costs beyond the basic web ACL price\. For more information, see [AWS WAF web ACL capacity units \(WCUs\)](aws-waf-capacity-units.md) and [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

On the console, when you add or update the rules in your web ACL, on the **Add rules and rule groups** page, choose **Add rules**, and then choose **Add my own rules and rule groups**\. Then choose **Rule group** and select your rule group from the list\. 

In your web ACL, you can alter the behavior of a rule group and its rules by setting the individual rule actions to count or any other action and by overriding the resulting rule group action to count\. This can help you do things like test a rule group, identify false positives from rules in a rule group, and customize how a managed rule group handles your requests\. For more information about these options, see [Action overrides in rule groups](web-acl-rule-group-override-options.md)\. 

If your rule group contains a rate\-based statement, each web ACL where you use the rule group has its own separate rate tracking and management for the rate\-based rule, independent of any other web ACL where you use the rule group\. For more information, see [Rate\-based rule statement](waf-rule-statement-type-rate-based.md)\.

**Temporary inconsistencies during updates**  
When you create or change a web ACL or other AWS WAF resources, the changes take a small amount of time to propagate to all areas where the resources are stored\. The propagation time can be from a few seconds to a number of minutes\. 

The following are examples of the temporary inconsistencies that you might notice during change propagation: 
+ After you create a web ACL, if you try to associate it with a resource, you might get an exception indicating that the web ACL is unavailable\. 
+ After you add a rule group to a web ACL, the new rule group rules might be in effect in one area where the web ACL is used and not in another\.
+ After you change a rule action setting, you might see the old action in some places and the new action in others\. 
+ After you add an IP address to an IP set that is in use in a blocking rule, the new address might be blocked in one area while still allowed in another\.