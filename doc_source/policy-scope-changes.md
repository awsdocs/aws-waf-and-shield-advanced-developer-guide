# AWS Shield Advanced policy scope changes<a name="policy-scope-changes"></a>

If you modify a Firewall Manager\-Shield Advanced policy which causes an account or resource to go out of scope of the policy, Firewall Manager no longer monitors the account or resource\. However, the account continues to be subscribed to Shield Advanced\. The resources continue to be protected by Shield Advanced and will incur the Shield Advanced data transfer charges\.

If the tags assigned to a resource change, causing the resource to fall out of scope of a Firewall Manager\-Shield Advanced policy, Firewall Manager no longer monitors the resource\. However, the resource continues to be protected by Shield Advanced and will incur the Shield Advanced data transfer charges\.

If an account that was part of a Firewall Manager\-Shield Advanced policy leaves the organization, it no longer falls under the scope of the policy and no longer is monitored by Firewall Manager\. However, the account remains subscribed to Shield Advanced\. Because the account is no longer part of the consolidated billing family, the account will incur a prorated Shield Advanced subscription fee\.