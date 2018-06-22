# Step 2: Specify Your Resources to Protect<a name="ddos-choose-resources"></a>

After you activate your AWS Shield Advanced subscription, as described in [Step 1: Activate AWS Shield Advanced](enable-ddos-prem.md), you specify the resources you want to protect\. <a name="ddos-choose-resources-procedure"></a>

**To select the resources to protect with Shield Advanced**

1. Choose the resources to protect\. For load balancers or Elastic IP addresses, you also must choose a region\. 

   You can choose from the drop\-down list, or you can type the Amazon Resource Name \(ARN\) of specific resources to protect\. You can choose or type any combination of resource types and resources\. If you enter an ARN, the ARN must be in the same account that you are working from\. 

   Shield Advanced lists a maximum of 100 resources at one time\. If you have more than 100 resources, choose **Next** to see the next set\.

   If you want to protect an Amazon EC2 instance, you must first associate an Elastic IP address to the instance, and then choose the Elastic IP address as the resource to protect\.

   If you choose an Elastic IP address as the resource to protect, Shield Advanced protects whatever resource is associated with that Elastic IP address, either an Amazon EC2 instance or an Elastic Load Balancing load balancer\. Shield Advanced automatically identifies the type of resource that is associated with the Elastic IP address and applies the appropriate mitigations for that resource, including configuring network ACLs that are specific to that Elastic IP address\. For more information about using Elastic IP addresses with your AWS resources, see the appropriate guide: [Amazon Elastic Compute Cloud Documentation](https://aws.amazon.com/documentation/ec2/) or [Elastic Load Balancing Documentation](https://aws.amazon.com/documentation/elastic-load-balancing/)\.

   Shield Advanced does not support EC2\-Classic\.
**Important**  
You can continue from this step without choosing any resources\. However, if you do so, you must add resources later as described in [Add AWS Shield Advanced Protection to more AWS Resources](configure-new-protection.md)\. Shield Advanced doesn't protect resources automatically; you must specify the resources that you want to protect\.

1. Choose **Next**\.

You can now go to [Step 3: \(Optional\) Authorize the DDoS Response Team](authorize-DRT.md)