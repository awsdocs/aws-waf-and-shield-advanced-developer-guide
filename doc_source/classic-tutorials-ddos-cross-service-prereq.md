# Prerequisites<a name="classic-tutorials-ddos-cross-service-prereq"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

The following tasks are not specifically related to DDoS protection, but are necessary to complete the tutorial\.

**Topics**
+ [Sign up for AWS](#classic-tutorials-ddos-cross-service-prereq-aws)
+ [Create an IAM user](#classic-tutorials-ddos-cross-service-prereq-iam)
+ [Create a key pair](#classic-tutorials-ddos-cross-service-prereq-pair)
+ [Create a virtual private cloud \(VPC\) with two subnets](#classic-tutorials-ddos-cross-service-prereq-vpc)
+ [Create a security group](#classic-tutorials-ddos-cross-service-prereq-security-group)

## Sign up for AWS<a name="classic-tutorials-ddos-cross-service-prereq-aws"></a>

When you sign up for Amazon Web Services \(AWS\), your AWS account is automatically signed up for all services in AWS\. You are charged only for the services that you use\.

If you have an AWS account already, skip to the next task\. If you don't have an AWS account, use the following procedure to create one\.

**To create an AWS account**

1. Open [https://portal\.aws\.amazon\.com/billing/signup](https://portal.aws.amazon.com/billing/signup)\.

1. Follow the online instructions\.

   Part of the sign\-up procedure involves receiving a phone call and entering a verification code on the phone keypad\.

Note your AWS account number, because you'll need it for the next task\.

## Create an IAM user<a name="classic-tutorials-ddos-cross-service-prereq-iam"></a>

To access AWS services and resources, you must provide credentials\. Although it’s possible to sign in with the user name and password that you created when you first opened your AWS account, for security purposes we strongly recommend that you create new credentials through the AWS Identity and Access Management \(IAM\) service, and that you use those credentials to sign in\. 

If you signed up for AWS but have not created an IAM user for yourself, you can create one using the following procedure\.

**To create an IAM user for yourself and add the user to an administrators group**

1. Sign in to the AWS Management Console and open the IAM console at [https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\.

1. In the navigation pane, choose **Users**, and then choose **Add user**\.

1. For **User name**, type a user name, such as **Administrator**\. The name can consist of letters, digits, and the following characters: plus \(\+\), equal \(=\), comma \(,\), period \(\.\), at \(@\), underscore \(\_\), and hyphen \(\-\)\. The name is not case sensitive and can be up to 64 characters in length\.

1. Select the check box next to **AWS Management Console access**, select **Custom password**, and then type the new user's password in the text box\. 

1. Choose **Next: Permissions**\.

1. On the **Set permissions for user** page, choose **Add user to group**\.

1. Choose **Create group**\.

1. In the **Create group** dialog box, type the name for the new group\. The name can consist of letters, digits, and the following characters: plus \(\+\), equal \(=\), comma \(,\), period \(\.\), at \(@\), underscore \(\_\), and hyphen \(\-\)\. The name is not case sensitive and can be up to 128 characters in length\.

1. For **Filter**, choose **Job function**\.

1. In the policy list, select the check box for ** AdministratorAccess**\. Then choose **Create group**\.

1. Back in the list of groups, select the check box for your new group\. Choose **Refresh** if necessary to see the group in the list\.

1. Choose **Next: Review** to see the list of group memberships to be added to the new user\. When you are ready to proceed, choose **Create user**\.

To sign in as this new IAM user, sign out of the AWS console, then use the following URL, where *your\_aws\_account\_id* is your AWS account number without the hyphens \(for example, if your AWS account number is `1234-5678-9012`, your AWS account ID is `123456789012`\):

```
https://your_aws_account_id.signin.aws.amazon.com/console/
```

Enter the IAM user name \(not your email address\) and password that you just created\. When you're signed in, the navigation bar displays "*your\_user\_name* @ *your\_aws\_account\_id*"\.

To verify the sign\-in link for IAM users for your account, open the IAM console and check under **IAM users sign\-in link** on the dashboard\.

For more information about IAM, see the [IAM User Guide](https://docs.aws.amazon.com/IAM/latest/UserGuide/)\.

## Create a key pair<a name="classic-tutorials-ddos-cross-service-prereq-pair"></a>

A *key pair* is a set of security credentials that you use to prove your identity\. A key pair consists of a private key and a public key that you create\. You use your key pair to log in to your Amazon EC2 instance, which is a virtual server in the AWS Cloud\. You specify the name of the key pair when you initially launch the instance\.

**To create a key pair**

1. Sign in to AWS using the URL that you created in the previous section\.

1. From the AWS dashboard, choose **EC2** to open the Amazon EC2 console\.

1. From the navigation bar, select a region for the key pair\. You can select any region that's available to you, regardless of your location\. However, key pairs are specific to a region; for example, if you plan to launch an instance in the US West \(Oregon\) Region, you must create a key pair for the instance in the US West \(Oregon\) Region\. For this tutorial, consider choosing the US West \(Oregon\) Region\.
**Note**  
Later in this tutorial, we use AWS Lambda and Amazon API Gateway, which currently are available only in specific AWS Regions\. Therefore, ensure that you select an AWS Region where both Lambda and Amazon API Gateway are available\. US West \(Oregon\), suggested above, supports all the services that are used in this tutorial\. For the most current service availability information, see [AWS service offerings by region](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)\. 

1. In the navigation pane, under **NETWORK & SECURITY**, choose **Key Pairs**\.
**Tip**  
The navigation pane is on the left side of the console\. If you do not see the pane, it might be minimized; choose the arrow to expand the pane\. You might have to scroll down to see the **Key Pairs** link\.

1. Choose **Create Key Pair**\.

1. Type a name for the new key pair in the **Key pair name** field of the **Create Key Pair** dialog box, and then choose **Create**\. Use a name that is easy for you to remember, such as your IAM user name, followed by `-key-pair`, plus the region name\. For example, *me*\-key\-pair\-*uswest2*\.

1. The private key file is automatically downloaded by your browser\. The base file name is the name that you specified as the name of your key pair, and the file name extension is `.pem`\. Save the private key file in a safe place\.
**Important**  
This is the only chance for you to save the private key file\. You must provide the name of your key pair when you launch an instance and the corresponding private key each time you connect to the instance\.

For more information, see [Amazon EC2 Key Pairs](https://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/ec2-key-pairs.html)\. 

## Create a virtual private cloud \(VPC\) with two subnets<a name="classic-tutorials-ddos-cross-service-prereq-vpc"></a>

Amazon VPC enables you to launch AWS resources into a virtual network that you've defined\. In this tutorial your VPC will contain the two Amazon EC2 instances that host your website along with two subnets connected to those instances\. 

For more information about Amazon VPC, see [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/) in the *Amazon VPC User Guide*\.

**To create a nondefault VPC**

1. Open the Amazon VPC console at [https://console\.aws\.amazon\.com/vpc/](https://console.aws.amazon.com/vpc/)\.

1. From the navigation bar, select a region for the VPC\. VPCs are specific to a region, so you should select the same region in which you created your key pair\. For this tutorial, we use the US West \(Oregon\) Region\.

1. On the VPC dashboard, choose **Start VPC Wizard**\.

1. On the **Step 1: Select a VPC Configuration** page, ensure that **VPC with a Single Public Subnet** is selected, and then choose **Select**\.

1. On the **Step 2: VPC with a Single Public Subnet** page, specify the following details:
   + For **VPC name**, type a friendly name for your VPC\.
   + For **Availability Zone**, choose **us\-west\-2a**\. 
   + For **Subnet name**, type `subnet-1`\.
   + Keep the other default configuration settings\.

1. Choose **Create VPC**\. On the confirmation page, choose **OK**\.

### Add a second subnet to your VPC<a name="classic-tutorials-ddos-cross-service-vpc-subnet"></a>

For increased availability, later in this tutorial you configure a load balancer to use different subnets in two different Availability Zones\. When you created your Amazon VPC in the previous step, you created the first subnet in an Availability Zone\. You now must add a second subnet in a different Availability Zone\. Both Availability Zones must be in the same AWS Region\.

**To add a second subnet to your Amazon VPC**

1. Open the Amazon VPC console at https://console\.aws\.amazon\.com/vpc/\.

1. In the navigation pane, choose **Subnets, Create Subnet**\. 

1. Specify the following subnet details: 
   + For **Name tag**, provide a name for your subnet\. For example, type `subnet-2`\. Doing so creates a tag with a key of Name and the value that you specify\. 
   + For **VPC**, choose the VPC that you just created in the previous steps\.
   + For **Availability Zone**, choose an Availability Zone that your subnet will reside in\. This should be different than the Availability Zone that you created with your VPC earlier in this tutorial\. The tutorial used `us-west-2a` as an example\. So this time, choose something other than `us-west-2a`, such as `us-west-2b`\. 
   + For **IPv4 CIDR block**, specify an IPv4 CIDR block for this second subnet\. You must specify an IPv4 CIDR block for the subnet from the range of your VPC\. The IP addresses for your two subnets cannot overlap\. Assuming you used the defaults when setting up your VPC, your first subnet used CIDR block 10\.0\.0\.0/24\. So for this second CIDR block, you can use 10\.0\.1\.0/24\. For more information, see [VPC and Subnet Sizing for IPv4](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Subnets.html#vpc-sizing-ipv4)\. 

1. Choose **Yes, create**\.

1. On the subnets page, choose the *first* subnet you created, `subnet-1`\.

1. In the details pane, on the **Route Table** tab, note the **Route Table** ID\. It starts with **rtb\-**\.

1. On the subnets page, choose the *second* subnet that you created, `subnet-2`\.

1. On the details pane, choose **Edit**\.

1. Your second subnet must use the same route table as your first subnet\. For **Change to**, select the name of the route table that you noted earlier\.

1. Choose **Save**\.

## Create a security group<a name="classic-tutorials-ddos-cross-service-prereq-security-group"></a>

Security groups act as a firewall for associated instances, controlling both inbound and outbound traffic at the instance level\. You must add rules to a security group that enable you to connect to your instance from your IP address using RDP\. You can also add rules that allow inbound and outbound HTTP and HTTPS access from anywhere\.

**Prerequisites**  
You need the public IPv4 address of your local computer\. The security group editor in the Amazon EC2 console can automatically detect the public IPv4 address for you\. Alternatively, you can use the search phrase "what is my IP address" in an internet browser\. If you are connecting through an internet service provider \(ISP\) or from behind a firewall without a static IP address, you must find out the range of IP addresses used by client computers\.

**To create a security group with least privilege**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. From the navigation bar, select a region for the security group\. Security groups are specific to a region, so you should select the same region in which you created your key pair, US West \(Oregon\)\.

1. In the navigation pane, choose **Security Groups** \.

1. Choose **Create Security Group**\.

1. Type a name for the new security group and a description\. Use a name that is easy for you to remember, such as your IAM user name, followed by \_SG\_, plus the region name\. For example, *me*\_SG\_*uswest2*\.

1. In the **VPC** list, select the VPC that you created earlier in this tutorial\.

1. On the **Inbound** tab, create the following rules \(choose **Add Rule** for each new rule\): 
   + Choose **HTTP** from the **Type** list, and make sure that **Source** is set to **Anywhere** \(`0.0.0.0/0`\)\.
   + Choose **HTTPS** from the **Type** list, and make sure that **Source** is set to **Anywhere** \(`0.0.0.0/0`\)\.
   + Choose **RDP** from the **Type** list\. In the **Source** box, choose **MyIP** to automatically populate the field with the public IPv4 address of your local computer\. Alternatively, choose **Custom** and specify the public IPv4 address of your computer or network in CIDR notation\. To specify an individual IP address in CIDR notation, add the routing suffix `/32`, for example, `203.0.113.25/32`\. If your company allocates addresses from a range, specify the entire range, such as `203.0.113.0/24`\.
**Warning**  
For security reasons, we don't recommend that you allow RDP access from all IPv4 addresses \(`0.0.0.0/0`\) to your instance, except for testing purposes and only for a short time\.

1. After you have added all of the rules, choose **Create**\.

Next: [Step 1: Launch a virtual server using Amazon EC2](classic-tutorials-ddos-cross-service-EC2.md)\.