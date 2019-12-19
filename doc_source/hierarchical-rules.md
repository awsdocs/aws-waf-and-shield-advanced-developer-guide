# Tutorial: Creating a Policy with Hierarchical Rules<a name="hierarchical-rules"></a>

With AWS Firewall Manager, you can create and apply protection policies that contain hierarchical rules\. That is, you can create and enforce certain rules centrally, but delegate the creation and maintenance of account\-specific rules to other individuals\. You can monitor the centrally applied \(common\) rules for any accidental removal or mishandling, thereby ensuring that they are applied consistently\. The account\-specific rules add further protection customized for the needs of individual teams\.

The following tutorial describes how to create a hierarchical set of protection rules\. 

**Topics**
+ [Step 1: Designate a Firewall Manager Administrator Account](#hierarchical-rules-set-firewall-administrator)
+ [Step 2: Create a Rule Group Using the Firewall Manager Administrator Account](#hierarchical-rules-create-a-rule-group)
+ [Step 3: Create a Firewall Manager Policy and Attach the Common Rule Group](#hierarchical-rules-create-policy)
+ [Step 4: Add Account\-Specific Rules](#hierarchical-rules-add-account-specific-rules)
+ [Conclusion](#hierarchical-rules-conclusion)

## Step 1: Designate a Firewall Manager Administrator Account<a name="hierarchical-rules-set-firewall-administrator"></a>

To use AWS Firewall Manager, you must designate an account in your organization as the Firewall Manager administrator account\. This account can be either the master account or a member account in the organization\. 

You can use the Firewall Manager administrator account to create a set of common rules that you apply to other accounts in the organization\. Other accounts in the organization can't change these centrally applied rules\.

To designate an account as a Firewall Manager administrator account and complete other prerequisites for using Firewall Manager, see the instructions in [AWS Firewall Manager Prerequisites](fms-prereq.md)\. If you've already completed the prerequisites, you can skip to step 2 of this tutorial\. 

In this tutorial, we refer to the administrator account as **Firewall\-Administrator\-Account**\.

## Step 2: Create a Rule Group Using the Firewall Manager Administrator Account<a name="hierarchical-rules-create-a-rule-group"></a>

Next, create a rule group using **Firewall\-Administrator\-Account**\. This rule group contains the common rules that you will apply to all member accounts governed by the policy that you create in the next step\. Only **Firewall\-Administrator\-Account** can make changes to these rules and the container rule group\.

In this tutorial, we refer to this container rule group as **Common\-Rule\-Group**\.

To create a rule group, see the instructions in [Creating a Rule Group](create-rule-group.md)\. Remember to sign in to the console using your Firewall Manager administrator account \(**Firewall\-Administrator\-Account**\) when following these instructions\.

## Step 3: Create a Firewall Manager Policy and Attach the Common Rule Group<a name="hierarchical-rules-create-policy"></a>

Using **Firewall\-Administrator\-Account**, create a Firewall Manager policy\. When you create this policy, you must do the following:
+ Add **Common\-Rule\-Group** to the new policy\.
+ Include all accounts in the organization that you want **Common\-Rule\-Group** applied to\.
+ Add all resources that you want **Common\-Rule\-Group** applied to\.

For instructions on creating a policy, see [Creating an AWS Firewall Manager Policy](create-policy.md)\.

This creates a web ACL in each specified account and adds **Common\-Rule\-Group** to each of those web ACLs\. After you create the policy, this web ACL and the common rules are deployed to all specified accounts\.

In this tutorial, we refer to this web ACL as **Administrator\-Created\-ACL**\. A unique **Administrator\-Created\-ACL** now exists in each specified member account of the organization\. 

## Step 4: Add Account\-Specific Rules<a name="hierarchical-rules-add-account-specific-rules"></a>

Each member account in the organization can now add their own account\-specific rules to the **Administrator\-Created\-ACL** that exists in their account\. The common rules already in **Administrator\-Created\-ACL** continue to apply, along with the new, account\-specific rules\. AWS WAF inspects web requests based on the order in which rules appear in the web ACL\. This applies to both **Administrator\-Created\-ACL** and account\-specific rules\.

To add rules to **Administrator\-Created\-ACL**, see [Editing a Web ACL](web-acl-editing.md)\.

## Conclusion<a name="hierarchical-rules-conclusion"></a>

You now have a web ACL that contains common rules administered by the Firewall Manager administrator account as well as account\-specific rules maintained by each member account\.

The **Administrator\-Created\-ACL** in each account references the single **Common\-Rule\-Group**\. Therefore, future changes by the Firewall Manager administrator account to **Common\-Rule\-Group** will immediately take effect in each member account\.

Member accounts can't change or remove the common rules in **Common\-Rule\-Group**\.

Account\-specific rules don't affect other accounts\.