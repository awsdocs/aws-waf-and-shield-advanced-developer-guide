# Deleting an AWS Firewall Manager policy<a name="policy-deleting"></a>

You can delete a Firewall Manager policy by performing the following steps\.<a name="policy-deleting-procedure"></a>

**To delete a policy \(console\)**

1. In the navigation pane, choose **Security policies**\.

1. Choose the option next to the policy that you want to delete\. 

1. Choose **Delete**\.

**Note**  
When you delete a Firewall Manager common security group policy, to remove the policy's replica security groups, choose the option to clean up the resources created by the policy\. Otherwise, after the primary is deleted, the replicas remain and require manual management in each Amazon VPC instance\. 

**Important**  
When you delete a Firewall Manager Shield Advanced policy, the policy is deleted, but your accounts remain subscribed to Shield Advanced\.