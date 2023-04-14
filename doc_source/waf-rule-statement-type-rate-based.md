# Rate\-based rule statement<a name="waf-rule-statement-type-rate-based"></a>

A rate\-based rule tracks the rate of requests for each originating IP address, and triggers the rule action on IPs with rates that go over the limit that you set\. You can use this type of rule to put a temporary block on requests from an IP address that's sending excessive requests\. By default, this rule uses the IP address from the web request origin, but you can configure a different IP address source\. 

You can add a scope\-down statement to the rule, to only track and rate limit requests that match the scope\-down statement\. 

When the rule action triggers for an IP address, AWS WAF applies the action to requests from the IP address that match the rule's scope\-down statement, until the rate of these requests falls below the limit\. It can take a minute or two for an action change to go into effect\. 

**Note**  
You can also get rate limiting with the targeted level of the AWS WAF Bot Control rule group\. For a comparison, see [Rate limiting options in rate\-based rules and targeted Bot Control rules](waf-managed-protections-comparison-table-rbr-bot.md)\. 

The minimum rate that you can set is 100\. AWS WAF checks the rate of requests every 30 seconds, and counts requests for the prior 5 minutes each time\. Because of this, it's possible for an IP address to send requests at too high a rate for 30 seconds before AWS WAF detects and blocks it\. 

AWS WAF tracks and manages web requests separately for each instance of a rate\-based rule that you use\. For example, if you provide the same rate\-based rule settings in two web ACLs, each of the two rule statements represents a separate instance of the rate\-based rule and gets its own tracking and management by AWS WAF\. If you define a rate\-based rule inside a rule group, and then use that rule group in multiple places, each use creates a separate instance of the rate\-based rule that gets its own tracking and management by AWS WAF\.

Each rate\-based rule instance can rate limit up to 10,000 IP addresses\. If a rule instance identifies more than 10,000 IP addresses to rate limit, it only limits the 10,000 highest senders\. 

You can retrieve the list of IP addresses that a rate\-based rule is currently rate limiting\. The requests that are rate limited for any IP address are those that match the scope\-down statement in the limiting rate\-based rule\. For information, see [Listing IP addresses that are being rate limited by rate\-based rulesListing rate\-limited IP addresses](listing-managed-ips.md)\.

**Narrowing the scope of a rate\-based rule**  
You can narrow the scope of the requests that AWS WAF tracks and manages in a rate\-based rule\. To do this, you nest a scope\-down statement inside the rate\-based statement\. 
+ Without a scope\-down statement, a rate\-based rule aggregates requests by IP address and takes action on all requests from IP addresses that go over the limit\.
+ With a scope\-down statement, the rule only counts requests that match the scope down statement, and it aggregates those by IP address\. If a request count for an IP address goes over the limit, the rate\-based rule only takes action on requests from that IP address that also match the scope\-down statement\. The rule doesn't inspect or take action on any other requests from the IP address\.

For information about scope\-down statements, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

**Not nestable** – You can't nest this statement type inside other statements\. You can include it directly in a web ACL and in a rule group\. 

**\(Optional\) Scope\-down statement** – This rule type takes an optional scope\-down statement, to narrow the scope of the requests that the rate\-based statement tracks\. For more information, see [Scope\-down statements](waf-rule-scope-down-statements.md)\.

**WCUs** – 2 plus any additional WCUs for a nested statement\.

This statement uses the following optional setting: 
+ **\(Optional\) Forwarded IP configuration** – By default, AWS WAF aggregates on the IP address in the web request origin, but you can instead configure the rule to use a forwarded IP address in an HTTP header like `X-Forwarded-For`\. AWS WAF uses the first IP address in the header\. With this configuration, you also specify a fallback behavior to apply to a web request with a malformed IP address in the specified header\. The fallback behavior sets the matching result for the request, to match or no match\. For more information, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. 

**Where to find this rule statement**
+ **Rule builder** in your web ACL, on the console – Under **Rule**, for **Type**, choose **Rate\-based rule**\.
+ **API** – [RateBasedStatement](https://docs.aws.amazon.com/waf/latest/APIReference/API_RateBasedStatement.html)

**Examples**  
If you wanted to limit the number of requests to the login page on your website without affecting traffic to the rest of your site, you could create a rate\-based rule with a scope\-down statement that matches requests to your login page\. For example, the scope\-down statement might be a string match statement that inspects the URI path and matches on strings that start with `/login`\. 

As another example, to counter a recent flood of requests from an attacker in the United States, you might create a rate\-based rule with the following scope\-down statement: 
+ AND rule statement that contains the following, second level of nested statements: 
  + A geo match statement that specifies requests originating in the United States\.
  + A string match statement that searches in the `User-Agent` header for the string `BadBot`\.