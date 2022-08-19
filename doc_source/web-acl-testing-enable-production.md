# Enabling your protections in production<a name="web-acl-testing-enable-production"></a>

When you've finished the final stage of testing and tuning in your production environment, enable your protections in production mode\.

**Production traffic risk**  
Before you deploy your web ACL implementation for production traffic, test and tune it in a test environment until you are comfortable with the potential impact to your traffic\. Also test and tune it in count mode with your production traffic before enabling your protections for production traffic\. 

**Note**  
To follow the guidance in this section, you need to understand generally how to create and manage AWS WAF protections like web ACLs, rules, and rule groups\. That information is covered in earlier sections of this guide\.

Perform these steps first in your test environment, then in production\.

**Enable your AWS WAF protections in production**

1. 

**Switch to your production protections**

   Update your web ACL and switch your settings for production\. 

   1. 

**Remove any test rules that you don't need**

      If you added test rules that you don't need in production, remove them\. If you're using any label matching rules to filter the results of managed rule group rules, be sure to leave those in place\. 

   1. 

**Switch to production actions**

      Change the action settings for your new rules to their intended production settings\. 
      + **Rule defined in the web ACL** – Edit the rules in the web ACL and change their actions from `Count` to their production actions\. 
      + **Rule group** – In your web ACL configuration of the rule group, switch rules to use their own actions or leave them with the `Count` action override, according to the results of your testing and tuning activities\. If you're using a label matching rule to filter the results of a rule group rule, be sure to leave the override for that rule in place\. 

        To switch to using a rule's action, in your web ACL configuration, edit the rule statement for the rule group and remove the `Count` override for the rule\. If you manage the web ACL in JSON, remove the rule from the `ExcludedRules` list in the rule group reference statement\. 
      + **Web ACL** – If you changed the web ACL default action for your tests, switch it to its production setting\. 

      With these settings, your new protections will be managing web traffic as you intend\. 

   When you save your web ACL, the resources that it's associated with will be using your production settings\. 

1. 

**Monitor and tune**

   To be sure that web requests are being handled as you want, closely monitor your traffic after you enable the new functionality\. You'll be monitoring metrics and logs for your production rule actions, instead of the count actions that you were monitoring for in your tuning work\. Keep monitoring and adjust the behavior as needed to adapt to changes in your web traffic\. 