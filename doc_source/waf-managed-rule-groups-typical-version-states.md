# Typical version states for AWS Managed Rules<a name="waf-managed-rule-groups-typical-version-states"></a>

Normally, a versioned managed rule group has a number of unexpired static versions, and the default version points to the static version that AWS recommends\. The following figure shows an example of the typical set of static versions and default version setting\. 

![\[Three static versions Version_1.2, Version_1.3, and Version_1.4 are stacked, with Version_1.4 on the top. Version_1.4 has two rules, RuleA and RuleB, both with production action. A default version indicator points to Version_1.4.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

The production action for most rules in a static version is Block, but it might be set to something different\. For detailed information about rule action settings, see the rule listings for each rule group at [AWS Managed Rules rule groups list](aws-managed-rule-groups-list.md)\. 