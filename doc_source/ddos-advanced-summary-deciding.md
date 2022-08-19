# Deciding whether to subscribe to AWS Shield Advanced and apply additional protections<a name="ddos-advanced-summary-deciding"></a>

Review the scenarios in this section for help deciding which accounts to subscribe to AWS Shield Advanced and where to apply additional protections\. With Shield Advanced, you pay one monthly subscription fee for all accounts created under a consolidated billing account, plus usage fees based on GB of data transferred out\. For information about Shield Advanced pricing, see [AWS Shield Advanced Pricing](http://aws.amazon.com/shield/pricing/)\.

**Note**  
For accounts that are members of an AWS Organizations organization, Shield Advanced subscriptions are billed against the organization's payer account, regardless of whether the payer account itself is subscribed\. 

To protect an application and its resources with Shield Advanced, you subscribe the accounts that manage the application to Shield Advanced and then you add protections to the application's resources\. For information about subscribing accounts and protecting resources, see [Getting started with AWS Shield Advanced](getting-started-ddos.md)\.

**Identifying the applications to protect**  
Consider implementing Shield Advanced protections for applications where you need any of the following: 
+ Guaranteed availability for the users of the application\. 
+ Rapid access to DDoS mitigation experts if the application is affected by a DDoS attack\.
+ Awareness by AWS that the application might be affected by a DDoS attack and notification of attacks from AWS and escalation to your security or operations teams\.
+ Predictability in your cloud costs, including when a DDoS attack affects your use of AWS services\.

If an application or its resources require any of the above, consider creating subscriptions for the related accounts\. 

**Identifying the resources to protect**  
For each subscribed account, consider adding a Shield Advanced protection to each resource that has any of the following characteristics:
+ The resource serves external users on the internet\. 
+ The resource is exposed to the internet and is also part of a critical application\. Consider every exposed resource, regardless of whether you intend it to be accessed by users on the internet\. 
+ The resource is protected by an AWS WAF web ACL\.

To learn more about creating and managing protections for your resources, see [Resource protections in AWS Shield Advanced](ddos-resource-protections.md)\. 

Additionally, follow the recommendations in this guide to help ensure that you architect your application for DDoS resiliency and that you have properly configured the features of Shield Advanced for optimal protections\. 