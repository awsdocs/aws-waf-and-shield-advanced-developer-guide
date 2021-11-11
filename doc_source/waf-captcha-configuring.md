# Configuring the CAPTCHA immunity time<a name="waf-captcha-configuring"></a>

You can configure the CAPTCHA immunity time setting for the web ACL and for any rule that uses the CAPTCHA action\. The default web ACL setting is 300 seconds\. The rule inherits its default setting from the web ACL\. Valid values range from 60 to 259,200 seconds, or three days\. 

**To configure the immunity time for a web ACL**
+ **Console** – On the **Web ACLs** page, choose the web ACL that you want to configure\. This takes you to the web ACL page\. In the console, you can configure the web ACL CAPTCHA immunity time only after you've created the web ACL\.
  + Choose the **Rules** tab\. 
  + In the **Web ACL CAPTCHA configuration** section, choose **Edit**, make your changes, and choose **Save**\.
+ **Outside of the console** – The web ACL data type has a CAPTCHA configuration parameter, which you can configure for create or update operations on the web ACL\. If you don't configure this parameter, the web ACL inherits the default AWS WAF CAPTCHA configuration\.

**To configure the immunity time for a rule**
+ **Console** – When you create or edit a rule and specify the CAPTCHA action, the console displays the rule's current immunity time setting and allows you to modify it\. If you don't use the CAPTCHA action, this setting is unavailable\.
+ **Outside of the console** – The rule data type has a CAPTCHA configuration parameter, which you can configure when you define the rule\. If you don't configure the rule's parameter, the rule inherits the CAPTCHA configuration from the web ACL where you use the rule\.