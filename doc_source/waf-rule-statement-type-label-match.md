# Label match rule statement<a name="waf-rule-statement-type-label-match"></a>

The label match statement inspects the labels that are on the web request against a string specification\. The labels that are available to a rule for inspection are those that have already been added to the web request by other rules in the same web ACL evaluation\. Labels don't persist outside of the web ACL evaluation\. 

**Note**  
A label match statement can only see labels from rules that are evaluated earlier in the web ACL\. For information about how AWS WAF evaluates the rules and rule groups in web ACL processing, see [Processing order of rules and rule groups in a web ACL](web-acl-processing-order.md)\.

For more information about labels, see [AWS WAF labels on web requests](waf-rule-labels.md)\.

**Nestable** – You can nest this statement type\. 

**WCUs** – 1 WCU

This statement uses the following settings: 
+ **Match scope** – Set this to **Label** to match against the label name and, optionally, the preceding namespaces and prefix\. Set this to **Namespace** to match against some or all of the namespace specifications and, optionally, the preceding prefix\. 
+ **Key** – The string that you want to match against\. If you specify a namespace match scope, this should only specify namespaces and optionally the prefix, with an ending colon\. If you specify a label match scope, this must include the label name and can optionally include preceding namespaces and prefix\. 

For more information about these settings, see [Matching against a label](waf-rule-label-match.md) and [Label match examples](waf-rule-label-match-examples.md)\.

**Where to find this**
+ **Rule builder** on the console – For **Request option**, choose **Has label**\.
+ **API statement** – `LabelMatchStatement`