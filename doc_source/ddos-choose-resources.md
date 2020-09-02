# Step 2: Add resources to protect<a name="ddos-choose-resources"></a>

After you subscribe to AWS Shield Advanced, as described in [Step 1: Subscribe to AWS Shield Advanced](enable-ddos-prem.md), you specify the resources that you want to protect\. 

If you are using AWS Firewall Manager to create a Firewall Manager Shield Advanced policy, you don't need to do this step\. You already specified your resources in the Firewall Manager policy\.

If you aren't using a Firewall Manager Shield Advanced policy, you can also specify resources later if you want, using the procedure at [Adding AWS Shield Advanced protection to AWS resources](configure-new-protection.md)\. 

**Note**  
Shield Advanced protects only resources that you have specified either in Shield Advanced or through a Firewall Manager Shield Advanced policy\. It doesn't automatically protect your resources\.

**Note**  
The console guidance provided here is for the latest version of the AWS Shield console, released in 2020\. In the console, you can switch between versions\. <a name="ddos-choose-resources-procedure"></a>

**To choose the resources to protect with Shield Advanced**

1. Do one of the following, depending on your starting point: 
   + From the subscription confirmation page at the end of the procedure [Step 1: Subscribe to AWS Shield Advanced](enable-ddos-prem.md), choose **Add resources to protect**\. 
   + From the console navigation bar, choose **Protected Resources** and then choose **Add resources to protect**\. 

1. In the **Choose resources to protect with Shield Advanced** page, select the Regions and resource types that you want to protect, then choose **Load resources**\. 
**Note**  
If you want to protect an Amazon EC2 instance, you first must associate an Elastic IP address to the instance, and then choose the Elastic IP address as the resource to protect\.
If you choose an Elastic IP address as the resource to protect, Shield Advanced protects whatever resource is associated with that Elastic IP address, either an Amazon EC2 instance or an Elastic Load Balancing load balancer\. Shield Advanced automatically identifies the type of resource that is associated with the Elastic IP address and applies the appropriate mitigations for that resource\. This includes configuring network ACLs that are specific to that Elastic IP address\. For more information about using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\.
Shield Advanced does not support EC2\-Classic\.

1. Select the resources that you want to protect, then choose **Protect with Shield Advanced**\.

You can now go to [Step 3: Configure layer 7 DDoS mitigation](ddos-get-started-rate-based-rules.md)\.