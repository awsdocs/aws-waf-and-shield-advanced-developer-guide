# Step 4: Register your Domain name and implement DNS service using Route 53<a name="classic-tutorials-ddos-cross-service-R53"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

You can use Route 53 to register the domain name for your website, route internet traffic to the resources for your domain, and check the health of your web server to verify that it's reachable, available, and functional\. Route 53 helps to protect against DDoS attacks by providing redundancy and load balancing across multiple DNS servers\. Route 53 can also detect anomalies in DNS queries and prioritize requests from users that are known to be reliable and, by extension, deprioritize requests that are from potentially less reliable sources\.

**Important**  
You are responsible for the cost of the AWS services implemented in this tutorial\. For full details about Route 53 costs, see the [Route 53 pricing page](https://aws.amazon.com/route53/pricing/)\. 

**Topics**
+ [Register your Domain with Route 53](#classic-tutorials-ddos-cross-service-r53-register)
+ [Create records](#classic-tutorials-ddos-cross-service-r53-records)

## Register your Domain with Route 53<a name="classic-tutorials-ddos-cross-service-r53-register"></a>

If you are new to hosting a website, your next step in this tutorial is to register a domain using Route 53\. Following are the steps to do this\.

**Important**  
If your domain is already registered with another registrar, you must migrate your existing domain from the other registrar's DNS service to instead use Route 53 as the DNS service\. This tutorial does not cover that transfer process\. Instead of following the Route 53 procedures described in this tutorial, you must perform four steps to transfer an existing domain:  
Create a hosted zone
Get your current DNS configuration from your DNS service provider
Create resource records sets
Update your registrar's name servers 
For more information about transferring an existing domain registration from another registrar, see [Transferring Domains](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-transfer.html)\. 

**To register a new domain using Route 53**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. Under **Domain Registration**, choose **Get Started Now**\.

1. Choose **Register Domain**\.

1. Type the domain name that you want to register, and choose **Check** to find out whether the domain name is available\. As an example, this tutorial assumes that you register the domain name `example.com`\.

   For information about how to specify characters other than a\-z, 0\-9, and \- \(hyphen\) and how to specify internationalized domain names, see [DNS Domain Name Format](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/DomainNameFormat.html)\.

1. If the domain is available, choose **Add to cart**\. The domain name appears in your shopping cart\. 

1. In the shopping cart, choose the number of years that you want to register the domain for\.

1. To register more domains, repeat steps 4 through 6\.

1. Choose **Continue**\.

1. On the **Contact Details for Your** *n* **Domains** page, enter contact information for the domain registrant, administrator, and technical contacts\. The values that you enter here are applied to all the domains that you're registering\. 

1. For some top\-level domains \(TLDs\), we're required to collect additional information\. For these TLDs, enter the applicable values after the **Postal/Zip Code** field\.

1. Choose whether you want to hide your contact information from WHOIS queries\. For more information, see the following topics:
   + [Enabling or Disabling Privacy Protection for Contact Information for a Domain](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-privacy-protection.html)
   + [Domains That You Can Register with Route 53](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html)

1. Choose **Continue**\.

1. Review the information that you entered, read the terms of service, and select the check box to confirm that you've read the terms of service\. 

1. Choose **Complete Purchase**\.

   For [generic TLDs](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html#registrar-tld-list-generic), we typically send an email to the registrant for the domain to verify that the registrant contact can be reached at the email address that you specified\. \(We don't send an email if we already have confirmation that the email address is valid\.\) The email comes from one of the following email addresses: 
   + **noreply@registrar\.amazon\.com** – for TLDs registered by Amazon Registrar\.
   + **noreply@domainnameverification\.net** – for TLDs registered by our registrar associate, Gandi\. To determine who the registrar is for your TLD, see [Domains That You Can Register with Route 53](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/registrar-tld-list.html)\.
**Important**  
The registrant contact must follow the instructions in the email to verify that the email was received, or we must suspend the domain as required by ICANN\. When a domain is suspended, it's not accessible on the internet\.

   For all TLDs, you receive an email when your domain registration has been approved\. To determine the current status of your request, see [Viewing the Status of a Domain Registration](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/domain-view-status.html)\.

## Create records<a name="classic-tutorials-ddos-cross-service-r53-records"></a>

Your next step is to create records that tell Route 53 how you want to route traffic for the domain and subdomain\.

**To create records**

1. Sign in to the AWS Management Console and open the Route 53 console at [https://console\.aws\.amazon\.com/route53/](https://console.aws.amazon.com/route53/)\.

1. In the navigation pane, choose **Hosted zones**\.

1. Because you registered your domain using Route 53, Route 53 automatically creates a hosted zone for you\. Choose this hosted zone\.

1. Choose **Create Record Set**\. 

1. Enter the applicable values: 
   + For **Name**, leave as is \(it should already be example\.com\)\.
   + For **Type**, choose **A – IPv4 address**\.
   + For **Alias**, choose **Yes**\.
   + For **Alias Target**, type the domain name of your CloudFront distribution that you created earlier in this tutorial\.

1. Choose **Create**\.

**Note**  
Your new record takes time to propagate to the Route 53 DNS servers\. Changes generally propagate to all Route 53 name servers within 60 seconds\. 

**To test your Route 53 records**

1. Open the domain name you added to the record, such as example\.com, in a browser\.

1. You should see your website\.

Next: [Step 5: Detect and filter malicious web requests using AWS WAF Classic](classic-tutorials-ddos-cross-service-WAF.md)\.