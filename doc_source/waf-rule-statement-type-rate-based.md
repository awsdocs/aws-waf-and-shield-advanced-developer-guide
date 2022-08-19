# Rate\-based rule statement<a name="waf-rule-statement-type-rate-based"></a>

A rate\-based rule tracks the rate of requests for each originating IP address, and triggers the rule action on IPs with rates that go over a limit\. You set the limit as the number of requests per 5\-minute time span\. You can use this type of rule to put a temporary block on requests from an IP address that's sending excessive requests\. By default, AWS WAF aggregates requests based on the IP address from the web request origin, but you can configure the rule to use an IP address from an HTTP header, like `X-Forwarded-For`, instead\. 

AWS WAF tracks and manages web requests separately for each instance of a rate\-based rule that you use\. For example, if you provide the same rate\-based rule settings in two web ACLs, each of the two rule statements represents a separate instance of the rate\-based rule and gets its own tracking and management by AWS WAF\. If you define a rate\-based rule inside a rule group, and then use that rule group in multiple places, each use creates a separate instance of the rate\-based rule that gets its own tracking and management by AWS WAF\.

When the rule action triggers, AWS WAF applies the action to additional requests from the IP address until the request rate falls below the limit\. It can take a minute or two for the action change to go into effect\. 

You can retrieve the list of IP addresses that are currently blocked due to rate limiting\. For information, see [Listing IP addresses blocked by rate\-based rules](listing-managed-ips.md)\.

The following caveats apply to AWS WAF rate\-based rules: 
+ The minimum rate that you can set is 100\.
+ AWS WAF checks the rate of requests every 30 seconds, and counts requests for the prior five minutes each time\. Because of this, it's possible for an IP address to send requests at too high a rate for 30 seconds before AWS WAF detects and blocks it\. 
+ AWS WAF can block up to 10,000 IP addresses\. If more than 10,000 IP addresses send high rates of requests at the same time, AWS WAF will only block 10,000 of them\. 

You can narrow the scope of the requests that AWS WAF tracks and counts\. To do this, you nest another, scope\-down statement inside the rate\-based statement\. Then, AWS WAF only counts requests that match the scope\-down statement\. For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

For example, based on recent requests that you've seen from an attacker in the United States, you might create a rate\-based rule with the following scope\-down statement: 
+ AND rule statement that contains the following, second level of nested statements: 
  + A geo\-match match statement that specifies requests originating in the United States\.
  + A string match statement that searches in the `User-Agent` header for the string `BadBot`\.

Let's say that you also set a rate limit of 1,000\. For each IP address, AWS WAF counts requests that meet the criteria for both of the nested statements\. Requests that don't meet both aren't counted\. If the count for an IP address exceeds 1,000 requests in any 5\-minute time span, the rule's action triggers against that IP address\. 

As another example, you might want to limit requests to the login page on your website\. To do this, you could create a rate\-based rule with the following nested string match statement: 
+ The **Inspect** **Request component** is `URI path`\.
+ The **Match type** is `Starts with string`\. 
+ The **String to match** is `/login`\. 

By adding this rate\-based rule to a web ACL, you could limit requests to your login page without affecting the rest of your site\.

**Not nestable** – You can't nest this statement type inside other statements\. You can include it directly in a web ACL and in a rule group\. 

**\(Optional\) Scope\-down statement** – This rule type takes an optional scope\-down statement, to narrow the scope of the requests that the rate\-based statement tracks\. For more information, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

**WCUs** – 2 plus any additional WCUs for a nested statement\.

This statement uses the following optional setting: 
+ **\(Optional\) Forwarded IP configuration** – By default, AWS WAF aggregates on the IP address in the web request origin, but you can instead configure the rule to use a forwarded IP address in an HTTP header like `X-Forwarded-For`\. AWS WAF uses the first IP address in the header\. With this configuration, you also specify a fallback behavior to apply to a web request with a malformed IP address in the specified header\. The fallback behavior sets the matching result for the request, to match or no match\. For more information, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. 

**Where to find this**
+ **Rule builder** in your web ACL, on the console – Under **Rule**, for **Type**, choose **Rate\-based rule**\.
+ **API statement** – `RateBasedStatement`