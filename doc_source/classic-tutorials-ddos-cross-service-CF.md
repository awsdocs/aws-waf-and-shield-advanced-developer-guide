# Step 3: Improve performance and absorb attacks using Amazon CloudFront<a name="classic-tutorials-ddos-cross-service-CF"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

Highly scaled, diverse internet connections can significantly improve the response time of your website, better absorb DDoS attacks, and isolate faults\. Amazon CloudFront edge servers along with Route 53 provide the additional layer of network infrastructure that you need to achieve these benefits\. Your content is served and DNS queries are resolved from locations that typically are closer to your users than your EC2 origin servers\. This reduces the load on your origin EC2 servers\.

**Important**  
You are responsible for the cost of the AWS services implemented in this tutorial\. For full details about CloudFront costs, see the [CloudFront pricing page](https://aws.amazon.com/cloudfront/pricing/)\. 

**Topics**
+ [Deliver Your Content using Amazon CloudFront](#classic-tutorials-ddos-cross-service-CF-implement)

## Deliver Your Content using Amazon CloudFront<a name="classic-tutorials-ddos-cross-service-CF-implement"></a>

Amazon CloudFront is a content delivery network \(CDN\) service that you can use to deliver your entire website, including static, dynamic, streaming, and interactive content\. You can use persistent TCP connections and variable time\-to\-live \(TTL\) to accelerate the delivery of your content, even if it can’t be cached at an edge location\. This allows you to use CloudFront to protect your web application, even if you are not serving static content\.

CloudFront accepts only well\-formed connections to prevent many common DDoS attacks, like [SYN floods](https://en.wikipedia.org/wiki/SYN_flood) and UDP reflection attacks, from reaching your origin\. CloudFront can automatically close connections that are unusually slow, which can indicate a potential DDoS attack\. 

Further, DDoS attacks are geographically isolated close to the source, which prevents the traffic from affecting other locations\. You can also use the CloudFront geo restriction feature to prevent users in specific geographic locations from accessing your content\. This can be useful in case you want to block attacks that are originating from geographic locations where you do not expect to serve users\. 

All of these capabilities can greatly improve your ability to continue serving traffic to users during large DDoS attacks\.

**To implement Amazon CloudFront**

1. Open the CloudFront console at [ https://console\.aws\.amazon\.com/cloudfront/](https://console.aws.amazon.com/cloudfront/)\.

1. Choose **Create Distribution**\.

1. On the **Select a delivery method for your content** page, in the **Web** section, choose **Get Started**\.

1. On the **Create Distribution** page, for **Origin name**, type the name of the load balancer that you created earlier in the tutorial\. To find the name, go to the Amazon EC2 dashboard and choose **Load Balancers** in the navigation pane\. Choose the load balancer that you created earlier\.

1. Accept all the default values for the remainder of the **Origin Settings** fields\.

1. Under **Default Cache Behavior Settings**, accept the default values, and CloudFront will do the following:
   + Forward all requests that use the CloudFront URL for your distribution \(for example, `http://d111111abcdef8.cloudfront.net/image.jpg`\) to the load balancer that you specified earlier
   + Allow users to use either HTTP or HTTPS to access your objects
   + Respond to requests for your objects
   + Cache your objects at CloudFront edge locations for 24 hours
   + Forward only the default request headers to your origin and not cache your objects based on the values in the headers
   + Allow everyone to view your content
   + Not automatically compress your content

   For more information, see [Cache Behavior Settings](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/distribution-web-values-specify.html#DownloadDistValuesCacheBehavior)\.

1. Under **Distribution Settings**, accept the defaults, other than the following:  
**Price Class**  
Select the price class that corresponds with the maximum price that you want to pay for CloudFront service\. By default, CloudFront serves your objects from edge locations in all CloudFront regions\.   
For more information about price classes and about how your choice of price class affects CloudFront performance for your distribution, see [Choosing the Price Class for a CloudFront Distribution](http://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/PriceClass.html)\. For information about CloudFront pricing, including how price classes map to CloudFront regions, see [Amazon CloudFront Pricing](http://aws.amazon.com/cloudfront/pricing/)\.  
**AWS WAF Classic Web ACL**  
Choose **None**\. You configure AWS WAF Classic later in this tutorial\.  
**Alternate Domain Names \(CNAMEs\) \(Optional\)**  
Specify a domain name that you want to use for your website's URLs\. For example, you could enter `example.com`\.   
**Default Root Object \(Optional\)**  
The object that you want CloudFront to request from your origin \(for example, `index.html`\) when a viewer requests the root URL of your distribution \(`http://example.com/`\) instead of an object in your distribution \(`http://example.com/product-description.html`\)\. Specifying a default root object avoids exposing the contents of your distribution\.   
**Comment \(Optional\)**  
Enter any comments that you want to save with the distribution\.

1. Choose **Create Distribution**\.

1. After CloudFront creates your distribution, the value of the **Status** column for your distribution changes from **InProgress** to **Deployed**\. If you chose to enable the distribution, it will then be ready to process requests\. This should take less than 15 minutes\.

   The domain name that CloudFront assigns to your distribution appears in the list of distributions\. \(It also appears on the **General** tab for a selected distribution\.\) Note both this name and the Distribution ID because you need these later in the tutorial\.

1. On the CloudFront console, note the ID of the distribution that you just created\. You need this ID later in the tutorial\.

**To test your CloudFront distribution**

1. On the CloudFront console, select the ID of the distribution that you just created\. This opens the details page for this distribution\. Note the domain name\.

1. Open that domain name in a browser\. You should see your website\. It might take about 15 minutes or so for the distribution to be active\. If you get an error that indicates that your origin closed the connection, give it some more time and try again\. You might also have to refresh the page in your browser\.

Next: [Step 4: Register your Domain name and implement DNS service using Route 53](classic-tutorials-ddos-cross-service-R53.md)\.