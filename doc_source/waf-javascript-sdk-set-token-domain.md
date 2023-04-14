# Providing domains for use in the tokens<a name="waf-javascript-sdk-set-token-domain"></a>

You can provide a domain configuration for the tokens that AWS WAF creates for the SDK\. To do this, configure the global variable `window.awsWafCookieDomainList` with one or more token domains\. 

Example settings: 

```
window.awsWafCookieDomainList = ['.aws.amazon.com']
```

```
window.awsWafCookieDomainList = ['.aws.amazon.com', 'abc.aws.amazon.com']
```

Public suffixes aren't allowed\. For example, you can't use `usa.gov` or `co.uk` as token domains\.

The domains that you specify must be ones that AWS WAF will accept, based on the protected host domain and the token domain list that's configured for the web ACL\. For more information, see [Configuring the web ACL token domain list](waf-tokens-domains.md#waf-tokens-domain-lists)\.

When AWS WAF creates a token, it uses the most appropriate, shortest domain from the combination of domains from the `window.awsWafCookieDomainList` configuration and the host domain of the resource that’s associated with the web ACL\. 

For the `AWSManagedRulesATPRuleSet` managed rule group, this will usually be a single domain that matches the domain in the login path that you provided to the rule group configuration\. 