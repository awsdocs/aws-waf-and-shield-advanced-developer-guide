# Setting the token immunity times<a name="waf-tokens-immunity-times-setting"></a>

You can set the immunity times in your web ACL and in your rules that use the Challenge and CAPTCHA rule actions\. 

For general information about managing a web ACL and its rules, see [Working with web ACLs](web-acl-working-with.md)\.

**Where to set the immunity time for a web ACL**
+ **Console** – When you edit the web ACL, in the **Rules** tab, edit and change the settings in the **Web ACL CAPTCHA configuration** and **Web ACL Challenge configuration** panes\. In the console, you can configure the web ACL CAPTCHA and challenge immunity times only after you've created the web ACL\.
+ **Outside of the console** – The web ACL data type has CAPTCHA and challenge configuration parameters, which you can configure and provide to your create and update operations on the web ACL\. 

**Where to set the immunity time for a rule**
+ **Console** – When you create or edit a rule and specify the CAPTCHA or Challenge action, you can modify the rule's immunity time setting\. 
+ **Outside of the console** – The rule data type has CAPTCHA and challenge configuration parameters, which you can configure when you define the rule\. 