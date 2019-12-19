# AWS Firewall Manager Findings<a name="fms-findings"></a>

AWS Firewall Manager creates findings for resources that are out of compliance and for attacks that it detects and sends them to AWS Security Hub\. For information about Security Hub findings, see [Findings in AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings.html)\.

When you use Security Hub and Firewall Manager, Firewall Manager automatically sends your findings to Security Hub\. For information about getting started with Security Hub, see [Setting Up AWS Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-settingup.html) in the [AWS Security Hub User Guide](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)\.

**How do I view my Firewall Manager findings?**  
To view your Firewall Manager findings in Security Hub, follow the guidance at [Working with Findings in Security Hub](https://docs.aws.amazon.com/securityhub/latest/userguide/securityhub-findings.html#securityhub-managing-findings) and create a filter using the following settings: 
+ Attribute set to **Product Name**\.
+ Operator set to **EQUALS**\.
+ Value set to `Firewall Manager`\. This setting is case sensitive\.

**Can I disable this?**  
You can disable the integration of AWS Firewall Manager findings with Security Hub through the Security Hub console\. Choose **Integrations** in the navigation bar, then in the Firewall Manager pane, choose **Disable Integration**\. For more information, see the [AWS Security Hub User Guide](https://docs.aws.amazon.com/securityhub/latest/userguide/what-is-securityhub.html)\.

**Topics**
+ [AWS WAF Policy Findings](waf-policy-findings.md)
+ [AWS Shield Advanced Policy Findings](shield-policy-findings.md)
+ [Security Group Common Policy Findings](security-group-common-policy-findings.md)
+ [Security Group Content Audit Policy Findings](security-group-content-audit-policy-findings.md)
+ [Security Group Usage Audit Policy Findings](security-group-usage-audit-policy-findings.md)