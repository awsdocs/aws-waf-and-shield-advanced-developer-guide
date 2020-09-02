# Managed lists<a name="working-with-managed-lists"></a>

Managed application and protocol lists streamline your configuration and management of AWS Firewall Manager content audit security group policies\. You use managed lists to define the protocols and applications that your policy allows and disallows\. For information about content audit security group policies, see [Content audit security group policies](security-group-policies.md#security-group-policies-audit)\. 

You can use the following types of managed lists in a security group content audit policy:
+ **Firewall Manager application lists and protocol lists** – Firewall Manager manages these lists\. The application lists include `FMS-Default-Public-Access-Apps-Allowed` and `FMS-Default-Public-Access-Apps-Denied`, which describe commonly used applications that should be allowed or denied to the general public\. The protocol lists include `FMS-Default-Protocols-Allowed`, a list of commonly used protocols that should be allowed to the general public\. You can use any list that Firewall Manager manages, but you can't edit or delete it\.
+ **Custom application lists and protocol lists** – You manage these lists\. You can create lists of either type with the settings that you need\. You have full control over your own custom managed lists, and you can create, edit, and delete them as needed\.
**Note**  
Currently, Firewall Manager doesn’t check references to a custom managed list when you delete it\. This means that you can delete a custom managed application list or protocol list even when it is in use by an active policy\. This can cause the policy to stop functioning\. Delete an application list or protocol list only after you have verified that it isn't referenced by any active polices\.

Managed lists are AWS resources\. You can tag a custom managed list\. You can't tag a Firewall Manager managed list\.

## Managed list versioning<a name="versioning-managed-lists"></a>

Custom managed lists don't have versions\. When you edit a custom list, policies that reference the list automatically use the updated list\. 

Firewall Manager managed lists are versioned\. The Firewall Manager service team publishes new versions as needed, in order to apply the best security practices to the lists\. 

When you use a Firewall Manager managed list in a policy, you choose your versioning strategy as follows: 
+ **Latest available version** – If you don't specify an explicit version setting for the list, then your policy automatically uses the latest version\. This is the only option available through the console\.
+ **Explicit version** – If you specify a version for the list, then your policy uses that version\. Your policy remains locked to the version that you specified until you modify the version setting\. To specify the version, you must define the policy outside of the console, for example through the CLI or one of the SDKs\. 

For more information about choosing the version setting for a list, see [Using managed lists in your content audit security group policies](#using-managed-lists)\.

## Using managed lists in your content audit security group policies<a name="using-managed-lists"></a>

When you create a content audit security group policy, you can choose to use managed audit policy rules\. Some of the settings for this option require a managed application list or protocol list\. Examples of these settings include protocols that are allowed in security group rules and applications can access the internet\.

The following restrictions apply for each policy setting that uses a managed list: 
+ You can specify at most one Firewall Manager managed list for any setting\. By default, you can specify at most one custom list\. The custom list limit is a soft quota, so you can request an increase to it\. For more information, see [AWS Firewall Manager quotas](fms-limits.md)\.
+ In the console, if you select a Firewall Manager managed list, you can't specify the version\. The policy will alway use the latest version of the list\. To specify the version, you must define the policy outside of the console, for example through the CLI or one of the SDKs\. For information about versioning for Firewall Manager managed lists, see [Managed list versioning](#versioning-managed-lists)\.

For information about creating a content audit security group policy through the console, see [Creating a content audit security group policy](create-policy.md#creating-firewall-manager-policy-audit-security-group)\.

## Creating a custom managed application list<a name="creating-custom-managed-application-list"></a>

**To create a custom managed application list**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Application lists**\.

1. In the **Application lists** page, choose **Create application list**\. 

1. In the **Create application list** page, give your list a name\. Don't use the prefix `fms-` as this is reserved for Firewall Manager\. 

1. Specify an application either by providing the protocol and port number or by selecting an application from the **Type** drop down\. Give your application specification a name\. 

1. Choose **Add another** as needed and fill in the application information until you have completed your list\. 

1. \(Optional\) Apply tags to your list\. 

1. Choose **Save** to save your list and return to the **Application lists** page\. 

## Creating a custom managed protocol list<a name="creating-custom-managed-protocol-list"></a>

**To create a custom managed protocol list**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Protocol lists**\.

1. In the **Protocol lists** page, choose **Create protocol list**\. 

1. In the protocol list creation page, give your list a name\. Don't use the prefix `fms-` as this is reserved for Firewall Manager\. 

1. Specify a protocol\. 

1. Choose **Add another** as needed and fill in the protocol information until you have completed your list\. 

1. \(Optional\) Apply tags to your list\. 

1. Choose **Save** to save your list and return to the **Protocol lists** page\. 

## Viewing a managed list<a name="viewing-managed-list"></a>

**To view an application list or protocol list**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. In the navigation pane, choose **Application lists** or **Protocol lists**\.

   The page displays all of the lists of the selected type that are available for your use\. The lists that Firewall Manager manages have a **Y** in the **ManagedList** column\. 

1. To see the details of a list, choose its name\. The detail page displays the list's content and any tags\.

   For Firewall Manager managed lists, you can also see the available versions by selecting the **Version** drop down\. 

## Deleting a custom managed list<a name="deleting-custom-managed-list"></a>

You can delete custom managed lists\. You can't edit or delete lists that Firewall Manager manages\. 

**Note**  
Currently, Firewall Manager doesn’t check references to a custom managed list when you delete it\. This means that you can delete a custom managed application list or protocol list even when it is in use by an active policy\. This can cause the policy to stop functioning\. Only delete an application list or protocol list after you have verified that it isn't referenced by any active polices\.

**To delete a custom managed application or protocol list**

1. Sign in to the AWS Management Console using the Firewall Manager administrator account that you set up in the prerequisites \([AWS Firewall Manager prerequisites](fms-prereq.md)\), and then open the Firewall Manager console at [https://console.aws.amazon.com/wafv2/fms](https://console.aws.amazon.com/wafv2/fms)\. 
**Note**  
For information about setting up a Firewall Manager administrator account, see [Step 2: Set the AWS Firewall Manager administrator account](enable-integration.md)\.

1. Make sure that the list that you want to delete isn't in use in any of your audit security group policies by doing the following: 

   1. In the navigation pane, choose **Security policies**\.

   1. In the **AWS Firewall Manager policies** page, select and edit your audit security groups, and remove any references to the custom list that you want to delete\. 

      If you delete a custom managed list that's in use in an audit security group policy, the policy that's using it can stop functioning\. 

1. In the navigation pane, choose **Application lists** or **Protocol lists**, depending on the type of list you want to delete\.

1. In the list page, select the custom list that you want to delete and choose **Delete**\.