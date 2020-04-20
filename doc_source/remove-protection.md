# Removing AWS Shield Advanced protection from an AWS resource<a name="remove-protection"></a>

You can remove AWS Shield Advanced protection from any of your AWS resources at any time\. 

**Important**  
Deleting an AWS resource doesn't remove the resource from AWS Shield Advanced\. You must also remove the protection on the resource from AWS Shield Advanced, as described in this procedure\.<a name="remove-protection-procedure"></a>

**Remove AWS Shield Advanced protection from an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Protected resources**\.

1. Choose the radio button next to the resource\.

1. Choose **Delete protection**\.

   1. If you have an Amazon CloudWatch alarm configured for this protection, you are given the option to delete the alarm along with the protection\. If you choose not to delete the alarm at this point, you can instead delete it later using the CloudWatch console\.
**Note**  
For protections that have an Amazon Route 53 health check configured, if you add the protection again later, the protection still includes the health check\. 

The preceding steps remove AWS Shield Advanced protection from a specific AWS resource\. They don't cancel your AWS Shield Advanced subscription\. You will continue to be charged for the service\. For information about your AWS Shield Advanced subscription, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.

## Removing a CloudWatch alarm from your Shield Advanced protections<a name="remove-cloudwatch-ddos"></a>

To remove a CloudWatch alarm from your Shield Advanced protections, you have two options:
+ Delete the protection as described in [Removing AWS Shield Advanced protection from an AWS resource](#remove-protection)\. Be sure to select the check box next to **Also delete related DDoSDetection alarm**\.
+ Delete the alarm using the CloudWatch console\. The name of the alarm to delete will start with **DDoSDetectedAlarmForProtection**\.