# Shield Advanced health\-based detection<a name="ddos-advanced-health-check-option"></a>

Shield Advanced health\-based detection uses the health of your AWS resource to improve responsiveness and accuracy in attack detection and mitigation\. To use health\-based detection, you define the health check for your resource in Route 53 and then associate it with your Shield Advanced protection\. For information about Route 53 health checks, see [How Amazon Route 53 Checks the Health of Your Resources](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/welcome-health-checks.html) and [Creating and Updating Health Checks](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/health-checks-creating.html)\. 

**Note**  
Do not use health checks with Route 53 hosted zones\.

You can enable health\-based detection for the following resource types:
+ **Elastic IP addresses and Global Accelerator accelerators** – Health\-based detection improves the accuracy of network\-layer and transport\-layer event detection and mitigation\. 

  When you protect an Elastic IP address or Global Accelerator accelerator with Shield Advanced, you reduce the threshold required to place a mitigation\. Shield Advanced helps to provide quicker mitigation for attacks and mitigations for smaller attacks, even when traffic is within the application’s capacity\.

  When you add health\-based detection, during periods when the associated Route 53 health check is unhealthy, Shield Advanced can place mitigations even more quickly and at lower thresholds\. 
+ **CloudFront distributions and Application Load Balancers** – Health\-based detection improves the accuracy of web request flood detection\. 

  When you protect a CloudFront distribution or Application Load Balancer with Shield Advanced, you receive web request flood detection alerts when there is a statistically significant deviation in traffic volume combined with significant changes in traffic self\-similarity\. Self\-similarity is determined based on attributes like user agent, referrer, and URI\. 

  When you add health\-based detection, you increase the likelihood that the alerts you receive are timely and actionable\. With health\-based detection, during periods when the associated Route 53 health check is unhealthy, Shield Advanced requires smaller deviations to alert and it reports events more quickly\. When the associated Route 53 health check is healthy, Shield Advanced requires larger deviations to alert\. 