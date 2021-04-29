# Label match examples<a name="waf-rule-label-match-examples"></a>

This section provides examples of match specifications, for the label match rule statement\. 

**Note**  
These JSON listings were created in the console by adding a rule to a web ACL with the label match specifications and then editing the rule and switching to the **Rule JSON editor**\. You can also get the JSON for a rule group or web ACL through the APIs or the command line interface\. 

**Topics**
+ [Match against a local label](#waf-rule-label-match-examples-local-label)
+ [Match against a label from anther context](#waf-rule-label-match-examples-label)
+ [Match against a managed rule group label](#waf-rule-label-match-examples-mgd-rg-label)
+ [Match against a local namespace](#waf-rule-label-match-examples-local-namespace)
+ [Match against a managed rule group namespace](#waf-rule-label-match-examples-mgd-rg-namespace)

## Match against a local label<a name="waf-rule-label-match-examples-local-label"></a>

The following JSON listing shows a label match statement for a label that's been added to the web request locally, in the same context as this rule\.

```
Rule: {
    Name: "match_rule",
    Statement: {
        LabelMatchStatement: {
            Scope: "LABEL",
            Key: "header:encoding:utf8"
        }
    },
    RuleLabels: [
        ...generate_more_labels...
    ],
    Action: { Block: {} }
}
```

If you use this match statement in account 111122223333, in a rule that you define for web ACL `testWebACL`, it would match the following labels\. 

```
awswaf:111122223333:webacl:testWebACL:header:encoding:utf8
```

```
awswaf:111122223333:webacl:testWebACL:testNS1:testNS2:header:encoding:utf8
```

It wouldn't match the following label, because the label string isn't an exact match\.

```
awswaf:111122223333:webacl:testWebACL:header:encoding2:utf8
```

It wouldn't match the following label, because the context isn't the same, so the prefix doesn't match\. This is true even if you added the rule group `productionRules` to the web ACL `testWebACL`, where the rule is defined\. 

```
awswaf:111122223333:rulegroup:productionRules:header:encoding:utf8
```

## Match against a label from anther context<a name="waf-rule-label-match-examples-label"></a>

The following JSON listing shows a label match rule that matches against a label from a rule inside a user\-created rule group\. The prefix is required in the specification for all rules running in the web ACL that aren't part of the named rule group\. This example label specification matches only the exact label\. 

```
Rule: {
    Name: "match_rule",
    Statement: {
        LabelMatchStatement: {
            Scope: "LABEL",
            Key: "awswaf:111122223333:rulegroup:testRules:header:encoding:utf8"
        }
    },
    RuleLabels: [
        ...generate_more_labels...
    ],
    Action: { Block: {} }
}
```

## Match against a managed rule group label<a name="waf-rule-label-match-examples-mgd-rg-label"></a>

This is a special case of matching against a label that's from another context than that of the match rule\. The following JSON listing shows a label match statement for a managed rule group label\. This matches only the exact label that's specified in the label match statement's key setting\.

```
Rule: {
    Name: "match_rule",
    Statement: {
        LabelMatchStatement: {
            Scope: "LABEL",
            Key: "awswaf:managed:aws:managed-rule-set:header:encoding:utf8"
        }
    },
    RuleLabels: [
        ...generate_more_labels...
    ],
    Action: { Block: {} }
}
```

## Match against a local namespace<a name="waf-rule-label-match-examples-local-namespace"></a>

The following JSON listing shows a label match statement for a local namespace\.

```
Rule: {
    Name: "match_rule",
    Statement: {
        LabelMatchStatement: {
            Scope: "NAMESPACE",
            Key: "header:encoding:"
        }
    },
    Labels: [
        ...generate_more_labels...
    ],
    Action: { Block: {} }
}
```

Similar to the local `Label` match, if you use this statement in account 111122223333, in a rule that you define for web ACL `testWebACL`, it would match the following label\. 

```
awswaf:111122223333:webacl:testWebACL:header:encoding:utf8
```

It wouldn't match the following label, because the account isn't the same, so the prefix doesn't match\. 

```
awswaf:444455556666:webacl:testWebACL:header:encoding:utf8
```

The prefix also doesn't match any labels applied by managed rule groups, like the following\. 

```
awswaf:managed:aws:managed-rule-set:header:encoding:utf8
```

## Match against a managed rule group namespace<a name="waf-rule-label-match-examples-mgd-rg-namespace"></a>

The following JSON listing shows a label match statement for a managed rule group namespace\. For a rule group that you own, you'd also need to provide the prefix in order to match for a namespace that's outside of the rule's context\. 

```
Rule: {
    Name: "match_rule",
    Statement: {
        LabelMatchStatement: {
            Scope: "NAMESPACE",
            Key: "awswaf:managed:aws:managed-rule-set:header:"
        }
    },
    RuleLabels: [
        ...generate_more_labels...
    ],
    Action: { Block: {} }
}
```

This specification matches against the following example labels\. 

```
awswaf:managed:aws:managed-rule-set:header:encoding:utf8
```

```
awswaf:managed:aws:managed-rule-set:header:encoding:unicode
```

It doesn't match the following label\.

```
awswaf:managed:aws:managed-rule-set:query:badstring
```