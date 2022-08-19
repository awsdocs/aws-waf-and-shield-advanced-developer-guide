# Step 3: \(Optional\) authorize the Shield Response Team \(SRT\)<a name="get-started-fms-shield-authorize-srt"></a>

One of the benefits of AWS Shield Advanced is support from the Shield Response Team \(SRT\)\. When you experience a potential DDoS attack, you can contact the [AWS Support Center](https://console.aws.amazon.com/support/home#/)\. If necessary, the Support Center escalates your issue to the SRT\. The SRT helps you analyze the suspicious activity and assists you in mitigating the issue\. This mitigation often involves creating or updating AWS WAF rules and web ACLs in your account\. The SRT can inspect your AWS WAF configuration and create or update AWS WAF rules and web ACLs for you, but the team needs your authorization to do so\. We recommend that as part of setting up AWS Shield Advanced, you proactively provide the SRT with the needed authorization\. Providing authorization ahead of time helps prevent mitigation delays in the event of an actual attack\. 

You authorize and contact the SRT at the account level\. That is, the account owner, not the Firewall Manager administrator, must perform the following steps to authorize the SRT to mitigate potential attacks\. The Firewall Manager administrator can authorize the SRT only for accounts that they own\. Likewise, only the account owner can contact the SRT for support\.

**Note**  
To use the services of the SRT, you must be subscribed to the [Business Support plan](https://aws.amazon.com/premiumsupport/business-support/) or the [Enterprise Support plan](https://aws.amazon.com/premiumsupport/enterprise-support/)\.

To authorize the SRT to mitigate potential attacks on your behalf, follow the instructions in [Shield Response Team \(SRT\) support](ddos-srt-support.md)\. You can change SRT access and permissions at any time by using the same steps\.

Continue to [Step 4: Configure Amazon SNS notifications and Amazon CloudWatch alarms](get-started-fms-shield-cloudwatch.md)\.