# AWS WAF web ACL capacity units \(WCUs\)<a name="aws-waf-capacity-units"></a>

AWS WAF uses web ACL capacity units \(WCU\) to calculate and control the operating resources that are required to run your rules, rule groups, and web ACLs\. AWS WAF enforces WCU limits when you configure your rule groups and web ACLs\. WCUs don't affect how AWS WAF inspects web traffic\. 

AWS WAF manages capacity for rules, rule groups, and web ACLs\. 

**Rule WCUs**  
AWS WAF calculates rule capacity when you create or update a rule\. AWS WAF calculates capacity differently for each rule type, to reflect each rule's relative cost\. Simple rules that cost little to run use fewer WCUs than more complex rules that use more processing power\. For example, a size constraint rule statement uses fewer WCUs than a statement that inspects requests using a regex pattern set\. 

Rule capacity requirements generally start at a base cost for the rule type and increase with complexity, for example, when you add text transformations before inspection or if you inspect the JSON body\. For information about rule capacity requirements, see the listings for the rule statements at [AWS WAF rule statements](waf-rule-statements.md)\. 

**Rule group WCUs**  
The WCU requirements for a rule group are determined by the rules that you define inside the rule group\. The maximum capacity for a rule group is 1,500 WCUs\. 

Each rule group has an immutable capacity setting, which the owner assigns at creation\. This is true for managed rule groups and rule groups that you create through AWS WAF\. When you modify a rule group, your changes must keep the rule group's WCUs within its capacity\. This ensures that web ACLs that are using the rule group remain within their capacity requirements\. 

When you create a rule group, take care to set the capacity high enough to accommodate the rules that you'll want to use throughout the rule group's lifetime\. 

**Web ACL WCUs**  
The WCU requirements for a web ACL are determined by the rules that you use inside the web ACL\. The cost of using a rule group in a web ACL is the rule group's capacity setting\. The cost of using a rule is the rule's calculated WCUs\. 

The basic price for a web ACL includes up to 1,500 WCUs\. Using more than 1,500 WCUs incurs additional fees, according to a tiered pricing model\. AWS WAF automatically adjusts your web ACL pricing as your web ACL WCU usage changes\. For pricing details, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\. 

The maximum capacity for a web ACL is 5,000 WCUs\. If you need more capacity than this, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. 

**Determining WCU usage**  
In the AWS WAF console, you can see the capacity consumed when you add rules to your web ACL or rule group\. The console displays the current capacity units used as you add the rules\. 

Through the API, you can check the capacity requirements for the rules that you want to use in a web ACL or rule group\. To do this, provide the JSON listing of the rules to the check capacity call\. For more information, see [CheckCapacity](https://docs.aws.amazon.com/waf/latest/APIReference/API_CheckCapacity.html) in the *AWS WAFV2 API Reference*\.