# Add resources to protect and configure protections<a name="ddos-choose-resources"></a>

After you subscribe to AWS Shield Advanced, as described in [Subscribe to AWS Shield Advanced](enable-ddos-prem.md), you specify the resources that you want to protect\. 

If you are using an AWS Firewall Manager Shield Advanced policy for your Shield Advanced protections, you don't need to do this step\. You specify the resources to protect in the Firewall Manager policy, and Firewall Manager manages adding resource protections according to your policy configuration\.

If you aren't using a Firewall Manager Shield Advanced policy, you can add resources here or after your initial configuration, using the procedure at [Adding AWS Shield Advanced protection to AWS resources](ddos-manage-protected-resources.md#configure-new-protection)\. 

**Note**  
Shield Advanced doesn't automatically protect your resources\. It protects only resources that you have specified either in Shield Advanced or in a Firewall Manager Shield Advanced policy\. 

**To choose the resources to protect using Shield Advanced**

1. Do one of the following, depending on your starting point: 
   + From the subscription confirmation page at the end of the procedure [Subscribe to AWS Shield Advanced](enable-ddos-prem.md), choose **Add resources to protect**\. 
   + In the **AWS Shield** navigation bar, choose **Protected Resources** and then choose **Add resources to protect**\. 

1. In the **Choose resources to protect with Shield Advanced** page, do the following: 

   1. Select the Region where your resources are located or, if you want to protect resources in multiple Regions, select **All Regions**\. 

   1. Select the resource types that you want to protect\. 

      For information about protections for your resource type, see [AWS Shield Advanced protections by resource type](ddos-protections-by-resource-type.md)\.

   1. Choose **Load resources**\.

   Shield Advanced populates the **Select Resources** section with the AWS resources that match your criteria\. 

1. In the **Select Resources** section, select the resources that you want to protect\.

1. In the **Tags** section, if you want to add tags to the Shield Advanced protections that you are creating, specify those\. For information about tagging AWS resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

1. Choose **Protect with Shield Advanced**\. This choice adds Shield Advanced protections to the resources\. Proceed through the additional screens provided by the console wizard to further configure your protections, with options like health checks and alarm notifications\. 