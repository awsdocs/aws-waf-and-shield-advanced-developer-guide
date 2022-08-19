# Deployments for versioned AWS Managed Rules rule groups<a name="waf-managed-rule-groups-deployments"></a>

AWS deploys changes to its versioned AWS Managed Rules rule groups in three standard deployments: release candidate, static version, and default version\. Additionally, AWS might sometimes need to release an exception deployment or roll back a default version deployment\. 

**Note**  
This section applies only to AWS Managed Rules rule groups that are versioned\. The rule groups that are not versioned are IP reputation, Bot Control, and ATP rule groups\. 

**Sign up for deployment notifications**  
For every deployment of a versioned rule group, AWS provides at least one SNS notification\. In some cases, we also update the managed rule group description in this guide, the changelog for the AWS Managed Rules rule groups, and the document history page\. To sign up for notifications, see [Getting notified of new versions and updates to a managed rule group](waf-using-managed-rule-groups-sns-topic.md)\.

**Topics**
+ [Overview of the standard deployments for AWS Managed Rules](waf-managed-rule-groups-deployments-standard.md)
+ [Typical version states for AWS Managed Rules](waf-managed-rule-groups-typical-version-states.md)
+ [Release candidate deployments for AWS Managed Rules](waf-managed-rule-groups-deployments-release-candidate.md)
+ [Static version deployments for AWS Managed Rules](waf-managed-rule-groups-deployments-static-version.md)
+ [Default version deployments for AWS Managed Rules](waf-managed-rule-groups-deployments-default-version.md)
+ [Exception deployments for AWS Managed Rules](waf-managed-rule-groups-deployments-exceptions.md)
+ [Default deployment rollbacks for AWS Managed Rules](waf-managed-rule-groups-deployments-default-rollbacks.md)