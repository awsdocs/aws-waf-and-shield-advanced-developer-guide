# Default deployment rollbacks for AWS Managed Rules<a name="waf-managed-rule-groups-deployments-default-rollbacks"></a>

Under certain conditions, AWS might roll back the default version to its prior setting\. A rollback usually takes less than ten minutes for all AWS Regions\.

AWS performs a rollback only to mitigate a significant issue in a static version, such as an unacceptably high level of false positives\. 

After the rollback of the default version setting, AWS expedites both the expiration of the static version that has the issue and the release of a new static version to address the issue\. 

**Timing and notifications**  
AWS performs default version rollbacks only when required\. 
+ **SNS** – AWS sends a single SNS notification at the time of the rollback\. The notification includes the rule group name, the version that the default version is being set to, and the deployment date\. This deployment type is very quick, so the notification doesn't provide timing information for Regions\. 
+ **Change log** – AWS doesn't update the change log or other parts of this guide for this type of deployment\.