# Shield Advanced proactive engagement<a name="ddos-advanced-proactive-engagement"></a>

With proactive engagement, the Shield Response Team \(SRT\) engages with you directly if the Amazon Route 53 health check associated with your protected resource becomes unhealthy during an event that's detected by Shield Advanced\. This allows you to engage with experts more quickly when the availability of your application might be affected by a suspected attack\. 

**Note**  
To use proactive engagement for a protected resource, you must associate an Amazon Route 53 health check with the resource, as described in [Shield Advanced health\-based detection](ddos-advanced-health-check-option.md)\. 

Proactive engagement is available for network\-layer and transport\-layer events on Elastic IP addresses and AWS Global Accelerator accelerators, and for web request floods on Amazon CloudFront distributions and Application Load Balancers\.

To use proactive engagement, you configure Shield Advanced health\-based detection for a resource that you want the SRT to monitor\. You then specify 1\-10 contacts for proactive engagement\. The SRT uses the information to contact you during a detected event that correlates with an unhealthy protected resource\. After you provide your contact information, you can enable proactive engagement\. 

**Note**  
To use proactive engagement, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.