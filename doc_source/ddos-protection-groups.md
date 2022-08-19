# AWS Shield Advanced protection groups<a name="ddos-protection-groups"></a>

Use protection groups to create logical collections of your protected resources and manage their protections as a group\. For information about managing resource protections, see [Configuring AWS Shield Advanced protections](ddos-manage-protected-resources.md#manage-protection)\. 

**Note**  
Automatic application layer DDoS mitigation does not interact with protection groups\. You can enable automatic mitigation for resources that are in protection groups, but Shield Advanced does not automatically apply attack mitigations based on protection group findings\. Shield Advanced applies automatic attack mitigations for individual resources\.

AWS Shield Advanced protection groups give you a self\-service way to customize the scope of detection and mitigation by treating multiple protected resources as a single unit\. Resource grouping can provide a number of benefits\. 
+ Improve accuracy of detection\. 
+ Reduce unactionable event notifications\. 
+ Increase coverage of mitigation actions to include protected resources that also might be affected during an event\. 
+ Accelerate time to mitigation of attacks with multiple similar targets\. 
+ Facilitate automatic protection of newly created protected resources\. 

Protection groups can help reduce false positives in situations such as blue/green swap, where resources alternate between being near zero load and fully loaded\. Another example is when you create and delete resources frequently while maintaining a load level that's shared among the members of the group\. For situations such as these, monitoring individual resources can lead to false positives, while monitoring the health of the group of resources does not\. 

You can configure protection groups to include all protected resources, all resources of specific resource types, or individually specified resources\. Newly protected resources that satisfy your protection group criteria are automatically included in your protection group\. A protected resource can belong to multiple protection groups\. 