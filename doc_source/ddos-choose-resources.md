# Add resources to protect and configure protections<a name="ddos-choose-resources"></a>

Shield Advanced only protects the resources that you specify, either through Shield Advanced or in a Firewall Manager Shield Advanced policy\. It doesn't automatically protect the resources of a subscribed account\. 

If you use an AWS Firewall Manager Shield Advanced policy for your protections, you don't need to do this step\. You configure the policy with the types of resource to protect, and Firewall Manager automatically adds protections to resources that are within scope of the policy\. 

If you don't use Firewall Manager, go through the following procedures for each account that has resources to protect\.

**To choose the resources to protect using Shield Advanced**

1. Choose **Add resources to protect** from the subscription confirmation page of the prior procedure, or from the **Protected resources** or **Overview** page\. 

1. In the **Choose resources to protect with Shield Advanced** page, in **Specify the Region and resource types**, provide the Region and resource type specifications for the resources that you want to protect\. You can protect resources in multiple Regions by selecting **All Regions** and you can narrow the selection to global resources by selecting **Global**\. You can deselect any resource types that you do not want to protect\. For information about protections for your resource types, see [AWS Shield Advanced protections by resource type](ddos-protections-by-resource-type.md)\.

1. Choose **Load resources**\. Shield Advanced populates the **Select Resources** section with the AWS resources that match your criteria\. 

1. In the **Select Resources** section, you can filter the list of resources by entering a string to search for in the resource listings\. 

   Select the resources that you want to protect\.

1. In the **Tags** section, if you want to add tags to the Shield Advanced protections that you are creating, specify those\. For information about tagging AWS resources, see [Working with Tag Editor](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/tag-editor.html)\. 

1. Choose **Protect with Shield Advanced**\. This adds Shield Advanced protections to the resources\.

Continue through the console wizard screens to complete the configuration of your resource protections\. 

**Topics**
+ [Configure application layer \(layer 7\) DDoS protections with AWS WAF](ddos-get-started-web-acl-rbr.md)
+ [Configure health\-based detection for your protections](ddos-get-started-health-checks.md)
+ [Configure alarms and notifications](ddos-get-started-create-alarms.md)
+ [Review and finish your protection configuration](ddos-get-started-review-and-configure.md)