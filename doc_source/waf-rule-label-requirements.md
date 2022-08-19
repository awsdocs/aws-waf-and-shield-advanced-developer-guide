# Label syntax and naming requirements<a name="waf-rule-label-requirements"></a>

A label is a string made up of a prefix, optional namespaces, and a name\. The components of a label are delimited with a colon\. Labels have the following requirements and characteristics:
+ Labels are case\-sensitive\. 
+ Each label namespace or label name can have up to 128 characters\. 
+ You can specify up to five namespaces in a label\. 
+ Components of a label are separated by colon \(`:`\)\.
+ You can't use the following reserved strings in the namespaces or name that you specify for a label: `awswaf`, `aws`, `waf`, `rulegroup`, `webacl`, `regexpatternset`, `ipset`, and `managed`\.

**Label syntax**  
A fully qualified label has a prefix, optional namespaces, and label name\. The prefix identifies the rule group or web ACL context of the rule that added the label\. Namespaces might be used to add more context for the label\. The label name provides the lowest level of detail for a label\. It often indicates the specific rule that added the label to the request\. 

The label prefix varies depending on its origin\. 
+ **Your labels** – The following shows the full label syntax for labels that you create in your web ACL and rule group rules\. The entity types are `rulegroup` and `webacl`\.

  ```
  awswaf:<entity owner account id>:<entity type>:<entity name>:<custom namespace>:...:<label name>
  ```
  + Label namespace prefix: `awswaf:<entity owner account id>:<entity type>:<entity name>:`
  + Custom namespace additions: `<custom namespace>:…:`

  When you define a label for a rule in a rule group or web ACL, you control the custom namespace strings and the label name\. The rest is generated for you by AWS WAF\. AWS WAF automatically prefixes all labels with `awswaf` and the account and web ACL or rule group entity settings\.
+ **Managed rule group labels** – The following shows the full label syntax for labels that are created by rules in managed rule groups\. 

  ```
  awswaf:managed:<vendor>:<rule group name>:<custom namespace>:...:<label name>
  ```
  + Label namespace prefix: `awswaf:managed:<vendor>:<rule group name>:`
  + Custom namespace additions: `<custom namespace>:…:`

  All AWS Managed Rules rule groups add labels\. For information about managed rule groups, see [Managed rule groups](waf-managed-rule-groups.md)\. 
+ **Labels from other AWS processes** – These processes are used by AWS Managed Rules rule groups, so you see them added to web requests that you evaluate using managed rule groups\. The following shows the full label syntax for labels that are created by processes that are called by managed rule groups\. 

  ```
  awswaf:managed:<process>:<custom namespace>:...:<label name>
  ```
  + Label namespace prefix: `awswaf:managed:<process>:`
  + Custom namespace additions: `<custom namespace>:…:`

  Labels of this type are listed for the managed rule groups that call the AWS process\. For information about managed rule groups, see [Managed rule groups](waf-managed-rule-groups.md)\. 

**Label examples for your rules**  
The following example labels are defined by rules in a rule group named `testRules` that belongs to the account, 111122223333\. 

```
awswaf:111122223333:rulegroup:testRules:testNS1:testNS2:LabelNameA
```

```
awswaf:111122223333:rulegroup:testRules:testNS1:LabelNameQ
```

```
awswaf:111122223333:rulegroup:testRules:LabelNameZ
```

The following listing shows an example label specification in JSON\. These label names include custom namespace strings before the ending label name\. 

```
Rule: {
    Name: "label_rule",
    Statement: {...}
    RuleLabels: [
        Name: "header:encoding:utf8",
        Name: "header:user_agent:firefox"
    ],
    Action: { Count: {} }
}
```

**Note**  
You can access this type of listing in the console through the rule JSON editor\. 

If you run the preceding rule in the same rule group and account as the preceding label examples, the resulting, fully qualified labels would be the following: 

```
awswaf:111122223333:rulegroup:testRules:header:encoding:utf8
```

```
awswaf:111122223333:rulegroup:testRules:header:user_agent:firefox
```

**Label examples for managed rule groups**  
The following show example labels from AWS Managed Rules rule groups and processes that they invoke\.

```
awswaf:managed:aws:core-rule-set:NoUserAgent_Header
```

```
awswaf:managed:aws:sql-database:SQLiExtendedPatterns_QueryArguments
```

```
awswaf:managed:aws:atp:aggregate:attribute:compromised_credentials
```

```
awswaf:managed:token:accepted
```