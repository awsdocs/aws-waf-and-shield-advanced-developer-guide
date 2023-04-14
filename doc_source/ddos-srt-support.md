# Shield Response Team \(SRT\) support<a name="ddos-srt-support"></a>

The Shield Response Team \(SRT\) provides added support for Shield Advanced customers\. The SRT are security engineers who specialize in DDoS event response\. As an additional layer of support to your AWS Support plan, you can work directly with the SRT, leveraging their expertise as part of your event response workflow\. For information about the options and for configuration guidance, see the topics that follow\.

**Note**  
To use the services of the Shield Response Team \(SRT\), you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\. 

**SRT support activities**  
The primary goal in an engagement with the SRT is to protect the availability and performance of your application\. Depending on the type of DDoS event and the architecture of your application, the SRT may take one or more of the following actions: 
+ **AWS WAF log analysis and rules** – For resources that use an AWS WAF web ACL, the SRT can analyze your AWS WAF logs to identify attack characteristics in your application web requests\. With your approval during engagement, the SRT can apply changes to your web ACL to block the attacks that they've identified\. 
+ **Build custom network mitigations** – The SRT can write custom mitigations for you for infrastructure layer attacks\. The SRT can work with you to understand traffic that's expected for your application, to block unexpected traffic, and to optimize packet per second rate limits\. For more information, see [Configuring custom mitigations with the Shield Response Team \(SRT\)](ddos-srt-custom-mitigations.md)\.
+ **Network traffic engineering** – The SRT works closely with AWS networking teams to protect Shield Advanced customers\. When required, AWS can change how internet traffic arrives on the AWS network in order to allocate more mitigation capacity to your application\. 
+ **Architectural recommendations** – The SRT may determine that the best mitigation for an attack requires architectural changes to better align with the AWS best practices, and they will help support your implementation of these practices\. For information, see [AWS Best Practices for DDoS Resiliency](https://docs.aws.amazon.com/whitepapers/latest/aws-best-practices-ddos-resiliency)\. 

**Topics**
+ [Configuring access for the Shield Response Team \(SRT\)](ddos-srt-access.md)
+ [Configuring proactive engagement](ddos-srt-proactive-engagement.md)
+ [Contacting the Shield Response Team \(SRT\)](ddos-srt-contacting.md)
+ [Configuring custom mitigations with the Shield Response Team \(SRT\)](ddos-srt-custom-mitigations.md)