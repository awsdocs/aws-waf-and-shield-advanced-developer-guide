# Configuring health\-based detection using health checks<a name="ddos-advanced-health-checks"></a>

You can configure Shield Advanced to use health\-based detection for improved responsiveness and accuracy in attack detection and mitigation\. You can use this option with any resource type except for Route 53 hosted zones\. 

To configure health\-based detection, you define a health check for your resource in Route 53, verify that it's reporting healthy, and then associate it with your Shield Advanced protection\. For information about Route 53 health checks, see [How Amazon Route 53 checks the health of your resources](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-health-checks.html) and [Creating, updating, and deleting health checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating-deleting.html) in the Amazon Route 53 Developer Guide\. 

**Note**  
Health checks are required for Shield Response Team \(SRT\) proactive engagement support\. For information about proactive engagement, see [Configuring proactive engagement](ddos-srt-proactive-engagement.md)\.

Health checks measure the health of your resources based on the requirements that you define\. The health check status provides input to the Shield Advanced detection mechanisms, allowing them to be more sensitive to the current state of your specific applications\. 

You can enable health\-based detection for any resource type except for Route 53 hosted zones\.
+ **Network and transport layer \(layer 3/layer 4\) resources** – Health\-based detection improves the accuracy of network\-layer and transport\-layer event detection and mitigation for Network Load Balancers, Elastic IP addresses, and Global Accelerator standard accelerators\. When you protect these resource types with Shield Advanced, Shield Advanced can provide mitigations for smaller attacks and faster mitigation for attacks, even when traffic is within the application’s capacity\.

  When you add health\-based detection, during periods when the associated health check is unhealthy, Shield Advanced can place mitigations even more quickly and at even lower thresholds\.
+ **Application layer \(layer 7\) resources** – Health\-based detection improves the accuracy of web request flood detection for CloudFront distributions and Application Load Balancers\. When you protect these resource types with Shield Advanced, you receive web request flood detection alerts when there's a statistically significant deviation in traffic volume that's combined with significant changes in traffic patterns, based on request characteristics\. 

  With health\-based detection, when the associated Route 53 health check is unhealthy, Shield Advanced requires smaller deviations to alert and it reports events more quickly\. Conversely, when the associated Route 53 health check is healthy, Shield Advanced requires larger deviations to alert\. 

**Contents**
+ [Best practices for using health checks with Shield Advanced](health-checks-best-practices.md)
+ [Metrics commonly used for health checks](health-checks-metrics.md)
  + [Metrics used to monitor application health](health-checks-metrics.md#health-checks-metrics-common)
  + [Amazon CloudWatch metrics for each resource type](health-checks-metrics.md#health-checks-protected-resource-metrics)
+ [Managing health check associations](manage-health-check-associations.md)
  + [Associating a health check with your resource](manage-health-check-associations.md#associate-health-check)
  + [Disassociating a health check from your resource](manage-health-check-associations.md#disassociate-health-check)
  + [The health check association status](manage-health-check-associations.md#health-check-association-status)
+ [Health check examples](health-checks-examples.md)
  + [Amazon CloudFront distributions](health-checks-examples.md#health-checks-example-cloudfront)
  + [Load balancers](health-checks-examples.md#health-checks-example-load-balancer)
  + [Amazon EC2 elastic IP address \(EIP\)](health-checks-examples.md#health-checks-example-elastic-ip)