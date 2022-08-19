# Best practices for using health checks with Shield Advanced<a name="health-checks-best-practices"></a>

Follow the best practices in this section when you create and use health checks with Shield Advanced\.
+ Plan your health checks by identifying the components of your infrastructure that you want to monitor\. Consider the following resource types for health checks: 
  + Critical resources\.
  + Any resources where you want higher sensitivity in Shield Advanced detection and mitigation\.
  + Resources for which you want Shield Advanced to proactively reach out to you\. Proactive engagement is informed by the status of your health checks\.

  Examples of resources that you might want to monitor include Amazon CloudFront distributions, internet\-facing load balancers, and Amazon EC2 instances\. 
+ Define health checks that accurately reflect the health of your application origin with as few notifications as possible\. 
  + Write health checks so that they're only unhealthy when your application is unavailable or isn't performing within acceptable parameters\. You are responsible for defining and maintaining health checks based on your application's specific requirements\. 
  + Use as few health checks as possible while still accurately reporting on the health of your application\. For example, multiple alarms from multiple areas of your application that all report the same problem might add overhead to your response activities without adding informational value\. 
  + Use calculated health checks to monitor application health using a combination of Amazon CloudWatch metrics\. For example, you can calculate combined health based on the latency of your application servers and their 5xx error rates, which indicate that the origin server didn't fulfill the request\. 
  + Create and publish your own application health indicators to CloudWatch custom metrics as needed and use them in a calculated health check\.
+ Implement and manage your health checks to improve detection and reduce unnecessary maintenance activities\.
  + Before you associate a health check with a Shield Advanced protection, make sure that it's in a healthy state\. Associating a health check that's reporting unhealthy can skew the Shield Advanced detection mechanisms for your protected resources\.
  + Keep your health checks available for use by Shield Advanced\. Don't delete a health check in Route 53 that you're using for a Shield Advanced protection\.
  + Use staging and test environments only to test your health checks\. Only maintain health check associations for environments that require production\-level performance and availability\. Don't maintain health check association in Shield Advanced for staging and test environments\. 