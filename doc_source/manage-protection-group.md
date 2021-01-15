# Managing AWS Shield Advanced protection groups<a name="manage-protection-group"></a>

Use protection groups to create logical collections of your protected resources and manage their protections as a group\. For information about managing resource protections, see [Configuring AWS Shield Advanced protections](manage-protection.md)\. For information about protection groups, see [Shield Advanced protection groups](ddos-overview.md#ddos-advanced-protection-groups)\.

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. 

## Creating a Shield Advanced protection group<a name="protection-group-creating"></a>

**To create a protection group**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. Choose the **Protection groups** tab, then choose **Create protection group**\. 

1. In the **Create protection group** page, provide a name for your group\. You'll use this name to identify the group in your list of protected resources\. You can't change the name of a protection group after you create it\. 

1. For **Protection grouping criteria**, select the criteria that you want Shield Advanced to use to identify the protected resources to include in the group\. Make your additional selections based on the criteria that you've chosen\.

1. For **Aggregation**, select how you want Shield Advanced to combine resource data for the group in order to detect, mitigate, and report events\.
   + **Sum** – Use the total traffic across the group\. This is a good choice for most cases\. Examples include Elastic IP addresses for Amazon EC2 instances that scale manually or automatically\. 
   + **Mean** – Use the average of the traffic across the group\. This is a good choice for resources that share traffic uniformly\. Examples include accelerators and load balancers\. 
   + **Max** – Use the highest traffic from each resource\. This is useful for resources that don't share traffic, and for resources that share traffic in a non\-uniform way\. Examples include Amazon CloudFront distributions and origin resources for CloudFront distributions\. 

1. Choose **Save** to save your protection group and return to the **Protected resources** page\.

In the **Shield** **Events** page, you can view events for your protection group and drill down to see additional information for the protected resources that are in the group\. 

## Updating a Shield Advanced protection group<a name="protection-group-updating"></a>

**To update a protection group**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. In the **Protection groups** tab, select the check box next to the protection group that you want to modify\. 

1. In the protection group's page, choose **Edit**\. Make your changes to the protection group settings\. 

1. Choose **Save** to save your changes\.

## Deleting a Shield Advanced protection group<a name="protection-group-deleting"></a>

**To delete a protection group**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. In the **Protection groups** tab, select the check box next to the protection group that you want to remove\. 

1. In the protection group's page, choose **Delete** and confirm the action\. 