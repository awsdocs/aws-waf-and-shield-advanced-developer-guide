# Body inspection size limits for CloudFront web ACLs<a name="web-acl-setting-body-inspection-limit"></a>

The body inspection size limit is the maximum request body size that a protected resource can forward to AWS WAF for inspection\. 

The default body inspection size limit for web ACLs that protect CloudFront distributions is 16 KB\. You can increase the limit in your web ACL configuration by increments of 16 KB, up to 64 KB\. The setting options are 16 KB, 32 KB, 48 KB, and 64 KB\.

**Oversize body handling**  
Whether you use the default AWS WAF limit or set a higher limit for your web ACL, if your web traffic includes bodies that are larger than the limit, your configured oversize handling will apply\. For information about your options for oversize handling, see [Handling oversize web request components](waf-oversize-request-components.md)\. 

**Pricing considerations**  
AWS WAF charges a base rate for inspecting traffic for CloudFront distributions using the default limit of 16 KB\. When you increase the limit for a web ACL, the traffic that AWS WAF can inspect for its associated CloudFront distributions includes body sizes up to your new limit\. You're only charged extra for the inspection of requests that have body sizes larger than the default 16 KB\. For more information about pricing, see [AWS WAF Pricing](http://aws.amazon.com/waf/pricing/)\.

**How to modify the body inspection size limit**  
You can configure the body inspection size limit in any web ACL that protects CloudFront distributions\. When you create or edit a CloudFront web ACL, you set the body inspection size limit in the resource association configurations\. In the API, the association configuration is part of the web ACL data type\. In the console, the configuration is on the page where you specify the web ACL's associated resources\. For guidance on the console configuration, see [Working with web ACLs](web-acl-working-with.md)\. 