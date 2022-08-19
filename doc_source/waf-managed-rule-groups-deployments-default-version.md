# Default version deployments for AWS Managed Rules<a name="waf-managed-rule-groups-deployments-default-version"></a>

When AWS determines that a new static version provides improved protections for the rule group compared to the current default, AWS updates the default version to the new static version\. AWS might release multiple static versions before promoting one to the rule group's default version\. 

The following diagram shows the state of the example rule group versions after AWS moves the default version setting to the new static version\. 

![\[This is similar to the typical version states figure, but with Version_1.5 on the top of the stack and the default indicator pointing to it.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

Before deploying this change to the default version, AWS provides notifications so that you can test and prepare for the upcoming changes\. If you use the default version, you can take no action and remain on it through the update\. If instead you want to delay switching to the new version, before the planned start of the default version deployment, you can explicitly configure your rule group to use the static version that the default is set to\. 

**Timing and notifications**  
AWS updates the default version when it recommends a different static version for the rule group than the one that's currently in use\. 

AWS sends an SNS notification at least one week prior to the targeted deployment day and then another on the deployment day, at the start of the deployment\. Each notification includes the rule group name, the static version that the default version is being updated to, and the deployment date\. The notification sent on the deployment day also provides the scheduled timing of the deployment for each AWS Region where the update is being performed\. 