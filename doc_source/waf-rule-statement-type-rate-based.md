# Rate\-based rule statement<a name="waf-rule-statement-type-rate-based"></a>

A rate\-based rule tracks the rate of requests for each originating IP address, and triggers the rule action on IPs with rates that go over a limit\. You set the limit as the number of requests per 5\-minutes time span\. You can use this type of rule to put a temporary block on requests from an IP address that's sending excessive requests\. 

When the rule action triggers, AWS WAF blocks additional requests from the IP address until the request rate falls below the limit\.

You can optionally nest another statement inside the rate\-based statement, to narrow the scope so that AWS WAF only counts requests that match the nested statement\. For example, based on recent requests that you've seen from an attacker in the United States, you might create a rate\-based rule with a nested AND rule statement that contains the following, second level of nested statements: 
+ A geo\-match match statement that specifies requests originating in the United States\.
+ A string match statement that searches in the `User-Agent` header for the string `BadBot`\.

Let's say that you also set a rate limit of 1,000\. For each IP address, AWS WAF counts requests that meet both of the conditions\. Requests that don't meet both conditions aren't counted\. If the count for an IP address exceeds 1,000 requests in any 5\-minute time span, the rule's action triggers against that IP address\. 

As another example, you might want to limit requests to the login page on your website\. To do this, you could create a rate\-based rule with the following nested string match statement: 
+ The **Request option** is `URI`\.
+ The **Match Type** is `Starts with`\. 
+ A **Strings to match** is `login`\. 

By adding this rate\-based rule to a web ACL, you could limit requests to your login page without affecting the rest of your site\.

**Not nestable** – You can't nest this statement type inside other statements\. You can include it directly in a web ACL\. You cannot include it in a rule group\. 

**WCUs** – Depends on the nested statement\.

**Where to find this**
+ **Rule builder** on the console – For **Request option**, choose **Rate**\.
+ **API statement** – `RateBasedStatement`