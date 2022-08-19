# Managing health check associations<a name="manage-health-check-associations"></a>

You'll benefit the most from using a health check with Shield Advanced if the health check only reports healthy when your application is running within acceptable parameters and only reports unhealthy when it's not\. Use the guidance in this section to manage your health check associations in Shield Advanced\. 

**Note**  
Shield Advanced doesn't automatically manage your health checks\. 

The following are required to use a health check with Shield Advanced: 
+ The health check must report healthy when you associate it with your Shield Advanced protection\. 
+ The health check must be relevant to the health of your protected resource\. You are responsible for defining and maintaining health checks that accurately report the health of your application, based on your application's specific requirements\. 
+ The health check must remain available for use by the Shield Advanced protection\. Don't delete a health check in Route 53 that you're using for a Shield Advanced protection\.

**Topics**
+ [Associating a health check with your resource](#associate-health-check)
+ [Disassociating a health check from your resource](#disassociate-health-check)
+ [The health check association status](#health-check-association-status)

## Associating a health check with your resource<a name="associate-health-check"></a>

The following procedure shows how to associate an Amazon Route 53 health check with a protected resource\. 

**Note**  
Before you associate a health check with a Shield Advanced protection, make sure that it's in a healthy state\. For information, see [Monitoring health check status and getting notifications](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-monitor-view-status.html) in the Amazon Route 53 Developer Guide\. 

**To associate a health check**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. On the **Protections** tab, select the resource that you want to associate with a health check\. 

1. Choose **Configure protections**\.

1. Choose **Next** until you get to the page **Configure health check based DDoS detection \- *optional***\.

1. Under **Associated Health Check**, choose the ID of the health check that you want to associate with the protection\. 
**Note**  
If you do not see the health check you need, go to the Route 53 console and verify the health check and its ID\. For information, see [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\.

1. Walk through the rest of the pages until you finish the configuration\. On the **Protections** page, your updated health check association is listed for the resource\.

1. On the **Protections** page, check that your newly associated health check is reporting healthy\. 

   You can't successfully begin using a health check in Shield Advanced while the health check is reporting unhealthy\. Doing so causes Shield Advanced to detect false positives at very low thresholds and can also negatively impact the ability of the Shield Response Team \(SRT\) to provide proactive engagement for the resource\. 

   If the newly associated health check is reporting unhealthy, do the following: 

   1. Disassociate the health check from your protection in Shield Advanced\.

   1. Revisit your health check specifications in Amazon Route 53 and verify your overall application performance and availability\. 

   1. When your application is performing within your parameters for good health and your health check is reporting healthy, try again to associate the health check in Shield Advanced\.

The health check association procedure is complete when you've established your new health check association and it reports healthy in Shield Advanced\.

## Disassociating a health check from your resource<a name="disassociate-health-check"></a>

The following procedure shows how to disassociate an Amazon Route 53 health check from a protected resource\. 

**To disassociate a health check**

1. Sign in to the AWS Management Console and open the AWS WAF & Shield console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. In the AWS Shield navigation pane, choose **Protected resources**\.

1. On the **Protections** tab, select the resource that you want to disassociate from a health check\. 

1. Choose **Configure protections**\.

1. Choose **Next** until you get to the page **Configure health check based DDoS detection \- *optional***\.

1. Under **Associated Health Check**, choose the empty option, listed as **\-**\. 

1. Walk through the rest of the pages until you finish the configuration\. 

On the **Protections** page, the health check field for your resource is set to **\-**, indicating no health check association\.

## The health check association status<a name="health-check-association-status"></a>

You can see the status of the health check that's associated with a protection on the AWS WAF & Shield console **Protected resources** page and on the details page of each resource\. 
+ **Healthy** – The health check is available and is reporting healthy\.
+ **Unhealthy** – The health check is available and is reporting unhealthy\.
+ **Unavailable** – The health check is not available for use by Shield Advanced\. 

**To resolve an **Unavailable** health check**

Create and use a new health check\. Don't try to associate a health check again after it has had a status of unavailable in Shield Advanced\. 

For detailed guidance on following these steps, see the preceding topics\. 

1. In Shield Advanced, disassociate the health check from the resource\. 

1. In Route 53, create a new health check for the resource and note its ID\. For information, see [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html) in the Amazon Route 53 Developer Guide\.

1. In Shield Advanced, associate the new health check with the resource\. 