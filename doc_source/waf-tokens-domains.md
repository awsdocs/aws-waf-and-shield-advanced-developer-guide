# Token domains and domain lists<a name="waf-tokens-domains"></a>

When AWS WAF creates a token for a client, it configures it with a token domain\. When AWS WAF inspects a token in a web request, it rejects the token as invalid if its domain doesn't match any of the domains that are considered valid for the web ACL\. 

By default, AWS WAF only accepts tokens whose domain setting exactly matches the host domain of the resource that's associated with the web ACL\. This is the value of the `Host` header in the web request\. In a browser, you can find this domain in the JavaScript `window.location.hostname` property and in the address that your user sees in their address bar\. 

You can specify token domains for AWS WAF to use when setting the domain and when evaluating a token in a web ACL\. The domains that you specify can't be public suffixes such as `usa.gov`\. 

## Configuring the web ACL token domain list<a name="waf-tokens-domain-lists"></a>

You can configure a web ACL to share tokens across multiple protected resources by providing a token domain list with the additional domains that you want AWS WAF to accept\. With a token domain list, AWS WAF still accepts the resource's host domain\. Additionally, it accepts all domains in the token domain list, including their prefixed subdomains\. 

For example, a domain specification `example.com` in your token domain list matches `example.com` \(from `http://example.com/`\), `api.example.com`, \(from `http://api.example.com/`\), and `www.example.com` \(from `http://www.example.com/`\)\. It doesn't match `example.api.com`, \(from `http://example.api.com/`\), or `apiexample.com` \(from `http://apiexample.com/`\)\.

You can configure the token domain list in your web ACL when you create or edit it\. For general information about managing a web ACL, see [Working with web ACLs](web-acl-working-with.md)\.

## Controlling the domain setting inside the token<a name="waf-tokens-domain-in-token"></a>

AWS WAF creates tokens at the request of the challenge scripts, which are run by the application integration SDKs and the Challenge and CAPTCHA rule actions\. 

The domain that AWS WAF sets in a token is determined by the type of challenge script that's requesting it and any additional token domain configuration that you provide\. AWS WAF sets the domain in the token to the shortest, most general setting that it can find in the configuration\.
+ **JavaScript SDK** – You can configure the JavaScript SDK with a token domain specification, which can include one or more domains\. The domains that you configure must be domains that AWS WAF will accept, based on the protected host domain and the web ACL's token domain list\. 

  AWS WAF sets the token domain to one that matches the host domain and is the shortest, from among the host domain and the domains in the list\. For example, if the host domain is `api.example.com` and the token domain list has `example.com`, AWS WAF uses `example.com` in the token, because it matches the host domain and is shorter\. If you don't provide a token domain list in the JavaScript SDK configuration, AWS WAF sets the domain to the host domain of the protected resource\.

  For more information, see [Providing domains for use in the tokens](waf-javascript-sdk-set-token-domain.md)\. 
+ **Mobile SDK** – You must configure the mobile SDK with a token domain for AWS WAF to use in the token\. The domain that you configure must be a domain that AWS WAF will accept, based on the protected host domain and the web ACL's token domain list\. AWS WAF doesn't consider the host domain in the token domain setting for the mobile SDK\. 

  For more information, see the `WAFConfiguration` `domainName` setting at [The AWS WAF mobile SDK specification](waf-mobile-sdk-specification.md)\. 
+ **Challenge action** – If you specify a token domain list in the web ACL, AWS WAF sets the token domain to one that matches the host domain and is the shortest, from among the host domain and the domains in the list\. For example, if the host domain is `api.example.com` and the token domain list has `example.com`, AWS WAF uses `example.com` in the token, because it matches the host domain and is shorter\. If you don't provide a token domain list in the web ACL, AWS WAF sets the domain to the host domain of the protected resource\. 