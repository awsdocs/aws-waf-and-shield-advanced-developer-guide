# Which should I choose?<a name="waf-which-to-choose"></a>

## <a name="waf-choosing"></a>

You can use [AWS WAF](waf-chapter.md), [AWS Firewall Manager](fms-chapter.md), and [AWS Shield](shield-chapter.md) together to create a comprehensive security solution\.

It all starts with AWS WAF\. You can automate and then simplify AWS WAF management using AWS Firewall Manager\. Shield Advanced adds additional features on top of AWS WAF, such as dedicated support from the DDoS Response Team \(DRT\) and advanced reporting\.

If you want granular control over the protection that is added to your resources, AWS WAF alone is the right choice\. If you want to use AWS WAF across accounts, accelerate your AWS WAF configuration, or automate protection of new resources, use Firewall Manager with AWS WAF\.

Finally, if you own high visibility websites or are otherwise prone to frequent DDoS attacks, you should consider purchasing the additional features that Shield Advanced provides\. 

**Note**  
To use the services of the DRT, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.