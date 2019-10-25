# Removing AWS Shield Advanced from an AWS Resource<a name="remove-protection"></a>

You can remove AWS Shield Advanced protection from any of your resources at any time\. 

**Important**  
Deleting a resource will not remove the resource from AWS Shield Advanced\. You must also remove the resource from AWS Shield Advanced, as described in this procedure\.<a name="remove-protection-procedure"></a>

**Remove AWS Shield Advanced protection from an AWS resource**

1. Sign in to the AWS Management Console and open the AWS WAF console at [https://console\.aws\.amazon\.com/wafv2/](https://console.aws.amazon.com/wafv2/)\. 

1. Choose **Protected resources**\.

1. Choose the radio button next to the resource\.

1. Choose **Delete protection**\.
**Note**  
If you have an Amazon CloudWatch alarm configured for this protection, you will be give the option to delete this alarm along with the protection\. If you choose not to delete the alarm at this point, you can instead delete it later using the CloudWatch console\.

These steps remove AWS Shield Advanced protection from a specific resource\. They do not cancel your AWS Shield Advanced subscription\. You will continue to be charged for the service\. For more information about your AWS Shield Advanced subscription, contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\.