# Label syntax and naming requirements<a name="waf-rule-label-requirements"></a>

A label is a string made up of a prefix, optional namespaces, and a name\. The components of a label are delimited with a colon\. Labels have the following requirements and characteristics:
+ Labels are case\-sensitive\. 
+ Each label namespace or label name can have up to 128 characters\. 
+ You can specify up to five namespaces in a label\. 
+ Components of a label are separated by colon \(`:`\)\.
+ You can't use the following reserved strings in the namespaces or name that you specify for a label: `awswaf`, `aws`, `waf`, `rulegroup`, `webacl`, `regexpatternset`, `ipset`, and `managed`\.

**Label syntax**  
The label prefix varies between the labels that you define in your rules and the ones that are defined in managed rule groups\. For information about these rule group types, see [Rule groups](waf-rule-groups.md)\. 
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

**Label examples**  
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

If you run the rule above in the same rule group and account as the preceding label examples, the resulting, fully qualified labels would be the following: 

```
awswaf:111122223333:rulegroup:testRules:header:encoding:utf8
```

```
awswaf:111122223333:rulegroup:testRules:header:user_agent:firefox
```