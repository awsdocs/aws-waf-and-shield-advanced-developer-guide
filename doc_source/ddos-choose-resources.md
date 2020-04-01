# Step 2: Specify your resources to protect<a name="ddos-choose-resources"></a>

After you activate your AWS Shield Advanced subscription, as described in [Step 1: Activate AWS Shield Advanced](enable-ddos-prem.md), you specify the resources that you want to protect\. 

If you are using AWS Firewall Manager to create a Firewall Manager\-Shield Advanced policy, you don't need to do this step\. You have already specified your resources in the policy\.

If you aren't using a Firewall Manager\-Shield Advanced policy, you can also specify resources later if you want, using the procedure at [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\. 

**Note**  
Shield Advanced only protects resources that you have specified in Shield Advanced or through a Firewall Manager\-Shield Advanced policy\. It doesn't automatically protect your resources\.<a name="ddos-choose-resources-procedure"></a>

**To choose the resources to protect with Shield Advanced**

1. Choose the resources to protect\. For load balancers or Elastic IP addresses, you also must choose a Region\. 

   You can choose from the dropdown list, or you can enter the Amazon Resource Name \(ARN\) of specific resources\. You can choose or enter any combination of resource types and resources\. If you enter an ARN, the ARN must be in the account that you're using\. 

   Shield Advanced lists a maximum of 100 resources at one time\. If you have more than 100 resources, choose **Next** to see the next set\.
**Note**  
If you want to protect an Amazon EC2 instance, you first must associate an Elastic IP address to the instance, and then choose the Elastic IP address as the resource to protect\.
If you choose an Elastic IP address as the resource to protect, Shield Advanced protects whatever resource is associated with that Elastic IP address, either an Amazon EC2 instance or an Elastic Load Balancing load balancer\. Shield Advanced automatically identifies the type of resource that is associated with the Elastic IP address and applies the appropriate mitigations for that resource\. This includes configuring network ACLs that are specific to that Elastic IP address\. For more information about using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\.
Shield Advanced does not support EC2\-Classic\.

1. Choose **Protect selected resources**\.

You can now go to [Step 3: Add rate\-based rules](ddos-get-started-rate-based-rules.md)\.