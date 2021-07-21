# AWS Shield Advanced policies<a name="policy-scope-changes"></a>

This topic covers the ways in which changes to an AWS Firewall Manager\-Shield Advanced policy and to related accounts and resources affect your protections and associated charges on your account\. 

When you create a Shield policy with auto remediation enabled, for each in scope resource that's not already associated with an AWS WAF web ACL, Firewall Manager associates an empty AWS WAF Classic web ACL\. The empty web ACL is used only for Shield monitoring purposes\. If you then associate any other web ACL to the resource, Firewall Manager removes the empty web ACL association\.

If you modify an AWS Firewall Manager\-Shield Advanced policy in a way that causes an account or resource to go out of scope of the policy, Firewall Manager no longer monitors the account or resource\. However, the account continues to be subscribed to Shield Advanced\. The resources continue to be protected by Shield Advanced and they continue to incur the Shield Advanced data transfer charges\.

If the tags assigned to a resource change in a way that causes the resource to go out of scope of a Firewall Manager Shield Advanced policy, Firewall Manager no longer monitors the resource\. However, the resource continues to be protected by Shield Advanced and it continues to incur Shield Advanced data transfer charges\.

If an account that was part of a Firewall Manager Shield Advanced policy leaves the organization, it no longer falls under the scope of the policy and no longer is monitored by Firewall Manager\. However, the account remains subscribed to Shield Advanced\. Because the account is no longer part of the consolidated billing family, the account will incur a prorated Shield Advanced subscription fee\.