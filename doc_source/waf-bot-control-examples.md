# AWS WAF Bot Control examples<a name="waf-bot-control-examples"></a>

This section shows example configurations that satisfy a variety of common use cases for AWS WAF Bot Control implementations\. 

Each example provides a description of the use case and then shows the solution in JSON listings for the custom configured rules\. 

**Note**  
The JSON listings shown in these examples were created in the console by configuring the rule and then editing it using the **Rule JSON editor**\. You can also retrieve the JSON for the rules in an entire rule group or web ACL using `get` commands through the APIs or the command line interface\. 

**Topics**
+ [AWS WAF Bot Control example: Simple configuration](waf-bot-control-example-basic.md)
+ [AWS WAF Bot Control example: Explicitly allow verified bots](waf-bot-control-example-allow-verified-bots.md)
+ [AWS WAF Bot Control example: Block verified bots](waf-bot-control-example-block-verified-bots.md)
+ [AWS WAF Bot Control example: Allow a specific blocked bot](waf-bot-control-example-allow-blocked-bot.md)
+ [AWS WAF Bot Control example: Create an exception for a blocked user agent](waf-bot-control-example-user-agent-exception.md)
+ [AWS WAF Bot Control example: Use Bot Control only for login page](waf-bot-control-example-scope-down-login.md)
+ [AWS WAF Bot Control example: Use Bot Control only for dynamic content](waf-bot-control-example-scope-down-dynamic-content.md)
+ [AWS WAF Bot Control example: Exclude IP range from bot management](waf-bot-control-example-scope-down-ip.md)
+ [AWS WAF Bot Control example: Allow traffic from a bot that you control](waf-bot-control-example-scope-down-your-bot.md)