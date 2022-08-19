# How AWS Shield works<a name="ddos-overview"></a>

AWS Shield Standard and AWS Shield Advanced provide protections against Distributed Denial of Service \(DDoS\) attacks for AWS resources at the network and transport layers \(layer 3 and 4\) and the application layer \(layer 7\)\. A DDoS attack is an attack in which multiple compromised systems try to flood a target with traffic\. A DDoS attack can prevent legitimate end users from accessing the target services and can cause the target to crash due to overwhelming traffic volume\. 

AWS Shield provides protection against a wide range of known DDoS attack vectors and zero\-day attack vectors\. Shield detection and mitigation is designed to provide coverage against threats even if they are not explicitly known to the service at the time of detection\. 

Classes of attacks that Shield detects include the following:
+ **Network volumetric attacks \(layer 3\)** – This is a sub category of infrastructure layer attack vectors\. These vectors attempt to saturate the capacity of the targeted network or resource, to deny service to legitimate users\.
+ **Network protocol attacks \(layer 4\)** – This is a sub category of infrastructure layer attack vectors\. These vectors abuse a protocol to deny service to the targeted resource\. A common example of a network protocol attack is a TCP SYN flood, which can exhaust connection state on resources like servers, load balancers, or firewalls\. A network protocol attack can also be volumetric\. For example, a larger TCP SYN flood may intend to saturate the capacity of a network while also exhausting the state of the targeted resource or intermediate resources\.
+ **Application layer attacks \(layer 7\)** – This category of attack vector attempts to deny service to legitimate users by flooding an application with queries that are valid for the target, such as web request floods\.

**Contents**
+ [AWS Shield Standard overview](ddos-standard-summary.md)
+ [AWS Shield Advanced overview](ddos-advanced-summary.md)
  + [AWS Shield Advanced protected resources](ddos-advanced-summary-protected-resources.md)
  + [AWS Shield Advanced capabilities and options](ddos-advanced-summary-capabilities.md)
  + [Deciding whether to subscribe to AWS Shield Advanced and apply additional protections](ddos-advanced-summary-deciding.md)
+ [Examples of DDoS attacks](types-of-ddos-attacks.md)
+ [How AWS Shield detects events](ddos-event-detection.md)
  + [Detection logic for infrastructure layer threats](ddos-event-detection-infrastructure.md)
  + [Detection logic for application layer threats](ddos-event-detection-application.md)
  + [Detection logic for multiple resources in an application](ddos-event-detection-multiple-resources.md)
+ [How AWS Shield mitigates events](ddos-event-mitigation.md)
  + [Mitigation features](ddos-event-mitigation-features.md)
  + [AWS Shield mitigation logic for CloudFront and Route 53](ddos-event-mitigation-logic-continuous-inspection.md)
  + [AWS Shield mitigation logic for AWS Regions](ddos-event-mitigation-logic-regions.md)
  + [AWS Shield mitigation logic for AWS Global Accelerator standard accelerators](ddos-event-mitigation-logic-gax.md)
  + [AWS Shield Advanced mitigation logic for Elastic IPs](ddos-event-mitigation-logic-adv-eip.md)
  + [AWS Shield Advanced mitigation logic for web applications](ddos-event-mitigation-logic-adv-web-app.md)