# Event visibility across accounts<a name="ddos-viewing-multiple-accounts"></a>

You can use AWS Firewall Manager and AWS Security Hub to manage and monitor AWS Shield Advanced protected resources across multiple accounts\. 

With Firewall Manager, you can create a Shield Advanced security policy that reports and enforces DDoS protection compliance across all of your accounts\. Firewall Manager monitors your protected resources, including adding protections to new resources that come into scope of the Shield Advanced policy\. 

You can integrate Firewall Manager with AWS Security Hub to get a single dashboard that reports DDoS events that are detected by Shield Advanced and Firewall Manager compliance findings, when Firewall Manager identifies a resource that's out of compliance with your Shield Advanced security policy\. 

The following figure depicts a typical architecture for monitoring Shield Advanced protected resources with Firewall Manager and Security Hub\. 

![\[At the top of the figure is an AWS Organizations icon. It has an arrow pointing down that splits to point to two icons that are side by side. The left icon has the title Production OU and the right icon has the title Security OU. Below these icons sit three icons, titled from left to right: AWS Shield Advanced, AWS Firewall Manager, and AWS Security Hub. The production OU icon has an arrow pointing down to the Shield Advanced icon. The security OU icon has an arrow pointing down that splits to point to the Firewall Manager and Security Hub icons. The Shield Advanced icon has an arrow pointing down to a rectangle with the title Shield Advanced protected resources. Inside the rectangle are icons for Application Load Balancer, CloudFront distribution, and Elastic IP address. The Firewall Manager icon also has an arrow pointing down to the Shield Advanced protected resources rectangle, and it's labeled Enforces compliance of protected resources. The Shield Advanced icon has a horizontal arrow pointing to the Firewall Manager icon that's labeled DDoS alarm. The Firewall Manager icon has a horizontal arrow pointing to its right, to the Security Hub icon that's labeled DDoS alarm and compliance findings.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

When you integrate Firewall Manager with Security Hub, you can view security findings in a single place, alongside other alerts and compliance status information for the applications that you run on AWS\. 

The following screenshot highlights the information that you can see for a Shield Advanced event inside the Security Hub console when you have an integration of this type\. 

![\[The screenshot shows the Security Hub console Findings page, subtitled A finding is a security issue or a failed security check.. The section has red outlines highlighting the strings: Title EQUALS Shield Advanced detected attack against monitored resource and Product name EQUAL Firewall Manager. The screen shows a set of details about the specific attack and its status.\]](http://docs.aws.amazon.com/waf/latest/developerguide/)

To learn how to integrate Firewall Manager and Security Hub with Shield Advanced to centralize event and compliance monitoring across your protected accounts, see the AWS security blog [Set up centralized monitoring for DDoS events and auto\-remediate noncompliant resources](http://aws.amazon.com/blogs/security/set-up-centralized-monitoring-for-ddos-events-and-auto-remediate-noncompliant-resources/)\. 