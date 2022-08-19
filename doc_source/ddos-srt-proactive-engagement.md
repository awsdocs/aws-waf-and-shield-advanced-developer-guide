# Configuring proactive engagement<a name="ddos-srt-proactive-engagement"></a>

With proactive engagement, the Shield Response Team \(SRT\) contacts you directly when the availability or performance of your application is affected because of a possible attack\. We recommend this engagement model because it provides the quickest SRT response and it allows the SRT to begin troubleshooting even before they've established contact with you\. 

Proactive engagement is available for network\-layer and transport\-layer events on Elastic IP addresses and AWS Global Accelerator standard accelerators, and for web request floods on Amazon CloudFront distributions and Application Load Balancers\. Proactive engagement is available only for Shield Advanced resource protections that have an associated Amazon Route 53 health check\. For information about managing and using health checks, see [Configuring health\-based detection using health checks](ddos-advanced-health-checks.md)\.

During an event that's detected by Shield Advanced, the SRT uses the state of your health checks to determine whether the event qualifies for proactive engagement\. If so, the SRT will contact you within 15 minutes, according to the contact guidance that you provide in your proactive engagement configuration\. 

You can configure up to ten contacts for proactive engagement, and you can provide notes to guide the SRT in reaching out to you\. Your proactive engagement contacts should be available to engage with the SRT within 15 minutes of contact, as you might provide in a 24/7 operations center\. If you don't have a 24/7 operations center, you can provide a pager contact and indicate this contact preference in your contact notes\.

Proactive engagement requires you to do the following: 
+ You must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.
+ You must associate an Amazon Route 53 health check with any resource that you want to protect with proactive engagement\. The SRT uses the status of your health checks to help determine whether an event requires proactive engagement, so it's important that your health checks accurately reflect the state of your protected resources\. For more information and guidance, see [Configuring health\-based detection using health checks](ddos-advanced-health-checks.md)\.
+ For a resource that has an AWS WAF web ACL associated, you must create the web ACL using AWS WAF \(v2\), which is the latest version of AWS WAF\. 
+ You must provide at least one contact for the SRT to use for proactive engagement during an event\. Keep your contact information complete and up to date\. 

**To enable SRT proactive engagement**

1. In the AWS Shield console **Overview** page, under **Proactive engagement and contacts**, in the contacts area, choose **Edit**\.

   In the **Edit contacts** page, provide the contact information for the people that you want the SRT to contact for proactive engagement\. 

   If you provide more than one contact, in the **Notes**, indicate the circumstances under which each contact should be used\. Include primary and secondary contact designations, and provide the hours of availability and time zones for each contact\. 

   Example contact notes: 
   + This is a hotline that's staffed 24x7x365\. Please work with the responding analyst and they will get the appropriate person on the call\. 
   + Please contact me if the hotline doesn't respond within 5 minutes\.

1. Choose **Save**\. 

   The **Overview** page reflects the updated contact information\.

1. Choose **Edit proactive engagement feature**, choose **Enable**, and then choose **Save**\.