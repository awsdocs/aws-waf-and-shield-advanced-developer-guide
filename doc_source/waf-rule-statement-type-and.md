# AND rule statement<a name="waf-rule-statement-type-and"></a>

The AND rule statement combines nested statements with a logical AND operation, so all nested statements must match for the AND statement to match\. This requires at least one nested statement\. 

**Nestable** – You can nest this statement type\. 

**WCUs** – Depends on the nested statements\.

**Where to find this**
+ **Rule builder** on the console – For **If a request**, choose **matches all the statements \(AND\)**, and then fill in the nested statements\. 
+ **API statement** – `AndStatement`