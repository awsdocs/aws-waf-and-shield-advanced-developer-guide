# Exception deployments for AWS Managed Rules<a name="waf-managed-rule-groups-deployments-exceptions"></a>

AWS might bypass the standard deployment stages in order to quickly deploy updates that address critical security risks\. An exception deployment might involve any of the standard deployment types, and it might be rolled out quickly across the AWS Regions\. 

AWS provides as much advance notification as possible for exception deployments\. 

**Timing and notifications**  
AWS performs exception deployments only when required\. 
+ **SNS** – AWS sends an SNS notification as far ahead of the targeted deployment day as possible and then another one at the start of the deployment\. Each notification includes the rule group name, the change that's being made, and the deployment date\. 
+ **Change log** – If the deployment is for a static version, after the deployment is complete everywhere that AWS WAF is available, AWS updates the rule group definition in this guide as needed, and then announces the release in the AWS Managed Rules rule group change log and in the documentation history page\. 