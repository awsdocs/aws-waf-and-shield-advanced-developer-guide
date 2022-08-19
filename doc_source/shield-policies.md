# AWS Shield Advanced policies<a name="shield-policies"></a>

When you apply a Firewall Manager Shield Advanced policy with auto remediation enabled, for each in\-scope resource that's not already associated with an AWS WAF web ACL, Firewall Manager associates an empty AWS WAF web ACL\. The empty web ACL is used only for Shield monitoring purposes\. If you then associate any other web ACL to the resource, Firewall Manager removes the empty web ACL association\.

## How AWS Firewall Manager manages scope changes in Shield policies<a name="shield-policies-changes-in-scope"></a>

Accounts and resources can go out of scope of an AWS Firewall Manager Shield Advanced policy due to a number of changes, such as changes to policy scope settings, changes to the tags on a resource, and the removal of an account from an organization\. For general information about policy scope settings, see [AWS Firewall Manager policy scope](policy-scope.md)\.

With an AWS Firewall Manager Shield Advanced policy, if an account or resource goes out of scope, Firewall Manager stops monitoring the account or resource\. 

If an account goes out of scope by being removed from the organization, it will continue to be subscribed to Shield Advanced\. Because the account is no longer part of the consolidated billing family, the account will incur a prorated Shield Advanced subscription fee\. On the other hand, an account that goes out of scope but remains in the organization doesn't incur additional fees\. 

If a resource goes out of scope, it continues to be protected by Shield Advanced and continues to incur Shield Advanced data transfer charges\.

## Automatic application layer DDoS mitigation for Amazon CloudFront distributions<a name="shield-policies-auto-app-layer-mitigation"></a>

When you apply a Shield Advanced policy to Amazon CloudFront distributions, you have the option of configuring Shield Advanced automatic application layer DDoS mitigation in the policy\. 

For information about Shield Advanced automatic mitigation, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.

Shield Advanced automatic application layer DDoS mitigation has the following requirements: 
+ Automatic application layer DDoS mitigation works only with Amazon CloudFront resources\.

  Because of this, you can only choose this option for Shield Advanced policies that you create for the **Global** Region, for use with Amazon CloudFront distributions\.
+ Automatic application layer DDoS mitigation works only with web ACLs that were created using the latest version of AWS WAF \(v2\)\. You cannot use automatic mitigation with AWS WAF Classic web ACLs\. 

  Because of this, if you have a policy that uses AWS WAF Classic web ACLs, you need to either replace the policy with a new policy, which will automatically use the latest version of AWS WAF, or have Firewall Manager create new version web ACLs for your existing policy and switch over to using them\. For more information about the options, see [Replace AWS WAF Classic web ACLs with latest version web ACLs](#shield-policies-auto-app-layer-update-waf-version)\.

### Automatic mitigation configuration<a name="shield-policies-auto-app-layer-mitigation-config"></a>

The automatic application layer DDoS mitigation option for Firewall Manager Shield Advanced policies applies Shield Advanced automatic mitigation functionality to your policy's in\-scope accounts and resources\. For detailed information about this Shield Advanced feature, see [Shield Advanced automatic application layer DDoS mitigation](ddos-automatic-app-layer-response.md)\.

You can choose to have Firewall Manager enable or disable automatic mitigation for the CloudFront distributions that are in scope of the policy, or you can choose to have the policy ignore Shield Advanced automatic mitigation settings: 
+ **Enable** – If you choose to enable automatic mitigation, you also specify whether mitigating Shield Advanced rules should count or block matching web requests\. Firewall Manager will mark in\-scope resources as noncompliant if they either don't have automatic mitigation enabled, or are using a rule action that doesn't match the one you specify for the policy\. If you configure the policy for automatic remediation, Firewall Manager updates noncompliant resources as needed\. 
+ **Disable** – If you choose to disable automatic mitigation, Firewall Manager will mark in\-scope resources as noncompliant if they have automatic mitigation enabled\. If you configure the policy for automatic remediation, Firewall Manager updates noncompliant resources as needed\. 
+ **Ignore** – If you choose to ignore automatic mitigation, Firewall Manager won't consider any automatic mitigation settings when it performs remediation activities for the policy\. This setting allows you to enable or disable automatic mitigation at the resource level, through Shield Advanced, without having those settings overwritten by Firewall Manager\. 

### Replace AWS WAF Classic web ACLs with latest version web ACLs<a name="shield-policies-auto-app-layer-update-waf-version"></a>

Automatic application layer DDoS mitigation works only with web ACLs that were created using the latest version of AWS WAF \(v2\)\. You cannot use automatic mitigation with AWS WAF Classic web ACLs\.

To determine the web ACL version for your Shield Advanced policy, see [Determining the version of AWS WAF that's used by a Shield Advanced policy](#shield-policies-identify-waf-version)\. 

If you want to use automatic mitigation in your Shield Advanced policy, and your policy currently uses AWS WAF Classic web ACLs, you can either create a new Shield Advanced policy to replace your current one, or you can use the options described in this section to replace earlier version web ACLs with new \(v2\) web ACLs inside your current Shield Advanced policy\. New policies always create web ACLs using the latest version of AWS WAF\. If you replace the entire policy, when you delete it, you can have Firewall Manager delete all of the earlier version web ACLs as well\. The rest of this section describes your options for replacing the web ACLs inside your existing policy\.

When you modify an existing Shield Advanced policy for Amazon CloudFront resources, Firewall Manager can automatically create a new empty AWS WAF \(v2\) web ACL for the policy, in any in\-scope account that doesn't already have a v2 web ACL\. When Firewall Manager creates a new web ACL, if the policy already has an AWS WAF Classic web ACL in the same account, Firewall Manager configures the new version web ACL with the same default action setting as the existing web ACL\. If there is no existing AWS WAF Classic web ACL, Firewall Manager sets the default action to `Allow` in the new web ACL\. After Firewall Manager creates a new web ACL, you can customize it as needed through the AWS WAF console\. 

When you choose any of the following policy configuration options, Firewall Manager creates new \(v2\) web ACLs for in\-scope accounts that don't already have them: 
+ When you enable or disable automatic application layer DDoS mitigation\. This choice alone only causes Firewall Manager to create the new web ACLs, and not to replace any existing AWS WAF Classic web ACL associations on the policy's in\-scope resources\. 
+ When you choose the policy action of automatic remediation and you choose the option to replace AWS WAF Classic web ACLs with AWS WAF \(v2\) web ACLs\. You can choose to replace earlier version web ACLs regardless of your configuration choices for automatic application layer DDoS mitigation\. 

  When you choose the replacement option, Firewall Manager creates the new version web ACLs as needed and then does the following for the policy's in\-scope resources: 
  + If a resource is associated with a web ACL from any other active Firewall Manager policy, Firewall Manager leaves the association alone\. 
  + For any other case, Firewall Manager removes any association with an AWS WAF Classic web ACL and associates the resource with the policy's AWS WAF \(v2\) web ACL\. 

You can choose to have Firewall Manager replace the earlier version web ACLs with the new version web ACLs when you want to\. If you've previously customized the policy's AWS WAF Classic web ACLs, you can update new version web ACLs to comparable settings before you choose to have Firewall Manager perform the replacement step\. 

You can access either version of web ACL for a policy through the same\-version console for AWS WAF or AWS WAF Classic\. 

Firewall Manager doesn't delete any replaced AWS WAF Classic web ACLs until you delete the policy itself\. After the AWS WAF Classic web ACLs are no longer used by the policy, you can delete them if you want to\.

## Determining the version of AWS WAF that's used by a Shield Advanced policy<a name="shield-policies-identify-waf-version"></a>

You can determine which version of AWS WAF your Firewall Manager Shield Advanced policy uses by looking at the parameter keys in the policy's AWS Config service\-linked rule\. If the AWS WAF version that's in use is the latest, the parameter keys include `policyId` and `webAclArn`\. If it's the earlier version, AWS WAF Classic, the parameter keys include `webAclId` and `resourceTypes`\. 

The AWS Config rule only lists keys for the web ACLs that the policy is currently using with in\-scope resources\. 

**To determine which version of AWS WAF your Firewall Manager Shield Advanced policy uses**

1. Retrieve the policy ID for the Shield Advanced policy: 

   1. Sign in to the AWS Management Console using your Firewall Manager administrator account, and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fmsv2](https://console.aws.amazon.com/wafv2/fmsv2)\. 

   1. In the navigation pane, choose **Security Policies**\.

   1. Choose the Region for the policy\. For CloudFront distributions, this is `Global`\.

   1. Find the policy that you want and copy the value of its **Policy ID**\. 

      Example policy ID: `1111111-2222-3333-4444-a55aa5aaa555`\.

1. Create the policy's AWS Config rule name by appending the policy ID to the string `FMManagedShieldConfigRule`\. 

   Example AWS Config rule name: `FMManagedShieldConfigRule1111111-2222-3333-4444-a55aa5aaa555`\.

1. Search the parameters for the associated AWS Config rule for keys named `policyId` and `webAclArn`: 

   1. Open the AWS Config console at [https://console\.aws\.amazon\.com/config/](https://console.aws.amazon.com/config/)\.

   1. In the navigation pane, choose **Rules**\.

   1. Find your Firewall Manager policy's AWS Config rule name in the list and select it\. The rule's page opens\. 

   1. Under **Rule details**, in the **Parameters** section, look at the keys\. If you find keys named `policyId` and `webAclArn`, the policy uses web ACLs that were created using the latest version of AWS WAF\. If you find keys named `webAclId` and `resourceTypes`, the policy uses web ACLs that were created using the earlier version, AWS WAF Classic\. 