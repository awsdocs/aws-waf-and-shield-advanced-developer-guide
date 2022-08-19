# Static version deployments for AWS Managed Rules<a name="waf-managed-rule-groups-deployments-static-version"></a>

When AWS determines that a release candidate provides valuable changes to the rule group, AWS deploys a new static version for the rule group based on the release candidate\. This deployment doesn't change the default version of the rule group\. 

The new static version contains the following rules from the release candidate: 
+ Rules from the prior static version that don't have a replacement candidate among the release candidate rules\. 
+ Release candidate rules, with the following changes: 
  + AWS changes the rule name by removing the release candidate suffix `_RC_COUNT`\.
  + AWS changes the rule actions from `COUNT` to their production rule actions\. 

   For release candidate rules that are replacements of prior existing rules, this replaces the functionality of the prior rules in the new static version\. 

The following diagram depicts the creation of the new static version from the release candidate\. 

![\[At the top of the figure is the release candidate version Version_1.4_PLUS_RC_COUNT, with the same rules as in the prior release candidate deployment figure. The version contains the rules from Version_1.4 and it also contains release candidate rules RuleB_RC_COUNT and RuleZ_RC_COUNT, both with count action. Below this, at the bottom of the figure is a static version Version_1.5, which contains rules RuleA, RuleB, and RuleZ, all with production action. Arrows point from the RC version to Version_1.5 to indicate that RuleA is copied from the Version_1.4 rules and RuleB and RuleZ are copied from the release candidate rules. All rules in Version_1.5 have production actions.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

After deployment, the new static version is available for you to test and to use in your protections if you want to\. You can review new and updated rule actions and descriptions in the rule group's rule listings at [AWS Managed Rules rule groups list](aws-managed-rule-groups-list.md)\. 

A static version is immutable after deployment, and only changes when AWS expires it\. For information about version lifecycles, see [Version management with managed rule groups](waf-managed-rule-groups-versioning.md)\.

**Timing and notifications**  
AWS deploys a new static version as needed, in order to deploy improvements to rule group functionality\. The deployment of a static version doesn't impact the default version setting\.

AWS sends an SNS notification at the start of the deployment\.

After the deployment is complete everywhere that AWS WAF is available, AWS announces the release in this guide, in the AWS Managed Rules rule group change log and in the documentation history page\. 