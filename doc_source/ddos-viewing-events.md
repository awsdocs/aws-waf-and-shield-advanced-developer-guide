# Visibility into DDoS events<a name="ddos-viewing-events"></a>

AWS Shield provides visibility into the following categories of events and event activities: 
+ **Global** – All customers can access an aggregated view of global threat activity over the last two weeks\. You can see this information under the **Getting Started** and **Global threat dashboard** pages of the AWS Shield console\. For more information, see [AWS Shield global and account activity](ddos-standard-event-visibility.md)\.
+ **Account** – All customers can access a summary of the events for their account over the prior year\. You can see this information under the **Getting Started** page of the AWS Shield console\. For more information, see [AWS Shield global and account activity](ddos-standard-event-visibility.md)\.

When you subscribe to Shield Advanced and add protections to your resources, you gain access to additional information about the events and DDoS attacks on the protected resources:
+ **Events on protected resources** – Shield Advanced provides detailed information for each event through the **Events** page of the AWS Shield console\. For more information, see [AWS Shield Advanced events](ddos-events.md)\.
+ **Event metrics for protected resources** – Shield Advanced publishes Amazon CloudWatch metrics for all resources that it protects that you can use to configure CloudWatch dashboards and alarms\. For more information, see [AWS Shield Advanced Amazon CloudWatch metrics](ddos-cloudwatch-metrics.md)\.
+ **Cross\-account event visibility for protected resources** – If you use AWS Firewall Manager to manage your Shield Advanced protections, you can enable visibility into protections across multiple accounts by using Firewall Manager combined with AWS Security Hub\. For more information, see [Event visibility across accounts](ddos-viewing-multiple-accounts.md)\.

