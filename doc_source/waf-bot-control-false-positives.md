# False positives with AWS WAF Bot Control<a name="waf-bot-control-false-positives"></a>

We have carefully selected the rules in the AWS WAF Bot Control managed rule group to minimize false positives\. We test the rules against global traffic and monitor their impact on test web ACLs\. However, it's still possible to get false positives occasionally\. 

Examples of situations where you might encounter false positives include the following: 
+ A rule that has a historically low false positive rate might have increased false positives for valid traffic\. This might be due to new traffic patterns or request attributes that emerge with valid traffic, causing it to match the rule where it didn't before\. These changes might be due to situations like the following:
  + Traffic details that are altered as traffic flows through network appliances, such as load balancers or content distribution networks \(CDN\)\.
  + Emerging changes in traffic data, for example new browsers or new versions for existing browsers\.
+ A rule with a low global false positive rate might heavily impact specific devices or applications\. For example, in testing and validation, we might not have observed requests from applications with low traffic volumes or from less common browsers or devices\. 
+ You might rely on some specific bot traffic for things like uptime monitoring, integration testing, or marketing tools\. If Bot Control identifies and blocks the bot traffic that you want to allow, you need to alter the handling by adding your own rules\. While this isn't a false positive scenario for all customers, if it is for you, the handling is the same as for a false positive\. 
+ The Bot Control managed rule group verifies bots using the IP addresses from AWS WAF\. If you use Bot Control and you have verified bots that route through a proxy or load balancer, you might need to explicitly allow them using a custom rule\. For information about how to create a custom rule of this type, see [Forwarded IP address](waf-rule-statement-forwarded-ip-address.md)\. 

For information about how to handle false positives that you might get from the AWS WAF Bot Control managed rule group, see the guidance in the prior section, [Testing and deploying AWS WAF Bot Control](waf-bot-control-deploying.md)\.