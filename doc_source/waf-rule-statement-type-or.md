# OR rule statement<a name="waf-rule-statement-type-or"></a>

The OR rule statement combines nested statements with OR logic, so one of the nested statements must match for the OR statement to match\. This requires at least one nested statement\. 

For example, if you want to block requests that come from a specific country or that contain a specific query string, you could create an OR statement and nest in it a geographic match statement for the country and a string match statement for the query string\. 

If instead you want to block requests that *don't* come from a specific country or that contain a specific query string, you would modify the previous OR statement to nest the geographics match statement one level lower, inside a NOT statement\. This level of nesting requires you to use the JSON formatting, as the console supports only one level of nesting\.

**Nestable** – You can nest this statement type\. 

**WCUs** – Depends on the nested statements\.

**Where to find this**
+ **Rule builder** on the console – For **If a request**, choose **matches at least one of the statements \(OR\)**, and then fill in the nested statements\. 
+ **API statement** – `OrStatement`