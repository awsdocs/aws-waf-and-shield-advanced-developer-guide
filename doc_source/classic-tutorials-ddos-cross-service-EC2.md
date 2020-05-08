# Step 1: Launch a virtual server using Amazon EC2<a name="classic-tutorials-ddos-cross-service-EC2"></a>

**Note**  
This is **AWS WAF Classic** documentation\. You should only use this version if you created AWS WAF resources, like rules and web ACLs, in AWS WAF prior to November 2019, and you have not migrated them over to the latest version yet\. To migrate your resources, see [Migrating your AWS WAF Classic resources to AWS WAF ](waf-migrating-from-classic.md)\.  
**For the latest version of AWS WAF**, see [AWS WAF](waf-chapter.md)\. 

You can mitigate infrastructure \(layer 3 and layer 4\) DDoS attacks by using techniques like overprovisioning capacity\. That is, you can scale your website to absorb larger volumes of traffic without capital\-intensive investments or unnecessary complexity\. You can use Amazon EC2 to launch virtual servers \(known as *instances*\) and quickly scale up or down as your requirements change\. You can scale horizontally by adding instances to your website as needed\. You can also choose to scale vertically by using larger instances\. In this step of the tutorial, you create a `c4.8xlarge` Amazon EC2 Windows instance, which includes a 10 GB network interface and enhanced networking, in the US West \(Oregon\) Region\. 

**Important**  
You are responsible for the cost of the AWS services implemented in this tutorial\. For full details about EC2 costs, see the [Amazon EC2 pricing page](https://aws.amazon.com/ec2/pricing)\. 

**Topics**
+ [Create an Amazon EC2 instance](#classic-tutorials-ddos-cross-service-EC2-launch)
+ [Connect to your instance](#classic-tutorials-ddos-cross-service-EC2-connect)
+ [Install a web server and host your site](#classic-tutorials-ddos-cross-service-EC2-install-web-server)
+ [Launch a second EC2 instance](#classic-tutorials-ddos-cross-service-EC2-second)
+ [Test your website](#classic-tutorials-ddos-cross-service-EC2-test)

## Create an Amazon EC2 instance<a name="classic-tutorials-ddos-cross-service-EC2-launch"></a>

The Amazon EC2 instances you create here will host your website\.

**To launch an instance**

1. Open the Amazon EC2 console at [https://console\.aws\.amazon\.com/ec2/](https://console.aws.amazon.com/ec2/)\.

1. In the navigation pane, choose the US West \(Oregon\) Region \(or whatever region you chose for your VPC\)\.

1. From the Amazon EC2 dashboard, choose **Launch Instance**\.

1. The **Choose an Amazon Machine Image \(AMI\)** page displays a list of basic configurations, called *Amazon Machine Images \(AMIs\)*, that serve as templates for your instance\. Choose the AMI for **Windows Server 2016 R2 Base**\.

1. On the **Choose an Instance Type** page, choose the `c4.8xlarge` type\. This type provides a 10 GB network interface and support for enhanced networking\.

1. Choose **Review and Launch**\.

1. Choose **Edit Instance Details**\.

1. For **Network**, choose the VPC that you created in the prerequisites step, [Create a virtual private cloud \(VPC\) with two subnets](classic-tutorials-ddos-cross-service-prereq.md#classic-tutorials-ddos-cross-service-prereq-vpc)\.

1. For **Subnet**, choose **subnet\-1**, which you created and named when creating the VPC\.

1. For **Auto\-assign Public IP**, choose **Enable**\.

1. Choose **Review and Launch**\.

1. On the **Review Instance Launch** page, under **Security Groups**, use the following steps to choose the security group that you created in the prerequisites step, [Create a security group](classic-tutorials-ddos-cross-service-prereq.md#classic-tutorials-ddos-cross-service-prereq-security-group)\.

   1. Choose **Edit security groups**\.

   1. On the **Configure Security Group** page, ensure that **Select an existing security group** is selected\.

   1. Choose the security group that you created earlier from the list of existing security groups, and then choose **Review and Launch**\.

1. On the **Review Instance Launch** page, choose **Launch**\.

1. When prompted for a key pair, select **Choose an existing key pair**, and then select the key pair that you created in the prerequisites step, [Create a key pair](classic-tutorials-ddos-cross-service-prereq.md#classic-tutorials-ddos-cross-service-prereq-pair)\.
**Warning**  
Don't select the **Proceed without a key pair** option\. If you launch your instance without a key pair, you can't connect to it\.

   Select the acknowledgement check box, and then choose **Launch Instances**\. 

1. A confirmation page lets you know that your instance is launching\. Choose **View Instances** to close the confirmation page and return to the console\.

1. On the **Instances** page, you can view the status of the launch\. It takes a short time for an instance to launch\. When you launch an instance, its initial state is `pending`\. After the instance starts, its state changes to `running` and it receives a public DNS name\. \(If the **Public DNS \(IPv4\)** column is hidden, choose the Show/Hide icon in the top\-right corner of the page, and then select **Public DNS \(IPv4\)**\.\) Take note of your public IPv4 address\. You need this value later in this tutorial\. 

1. It can take a few minutes for the instance to be ready so that you can connect to it\. Check that your instance has passed its status checks; you can view this information in the **Status Checks** column\.

## Connect to your instance<a name="classic-tutorials-ddos-cross-service-EC2-connect"></a>

You will use Microsoft Remote Desktop to connect to your instances\. If you are connecting from a Microsoft Windows computer, Remote Desktop is already installed\. If you are using another operating system, you might need to install Remote Desktop before performing the following procedure\. 

**To connect to your Windows instance using an RDP client**

1. In the Amazon EC2 console, select the instance, and then choose **Connect**\.

1. In the **Connect To Your Instance** dialog box, choose **Get Password** \(it will take a few minutes after the instance is launched before the password is available\)\.

1. Choose **Browse** and navigate to the private key file that you created when you launched the instance\. Select the file and choose **Open** to copy the entire contents of the file into the **Contents** field\.

1. Choose **Decrypt Password**\. The console displays the default administrator password for the instance in the **Connect To Your Instance** dialog box, replacing the link to **Get Password** shown previously with the actual password\.

1. Record the default administrator password, or copy it to the clipboard\. You need this password to connect to the instance\.

1. Choose **Download Remote Desktop File**\. Your browser prompts you to either open or save the \.rdp file\. Either option is fine\. When you have finished, you can choose **Close** to dismiss the **Connect To Your Instance** dialog box\. 
   + If you opened the \.rdp file, you see the **Remote Desktop Connection** dialog box\.
   + If you saved the \.rdp file, navigate to your downloads directory, and then open the \.rdp file to display the dialog box\.

1. You might get a warning that the publisher of the remote connection is unknown\. You can continue to connect to your instance\.

1. When prompted, connect to and log in to the instance, using the administrator account for the operating system and the password that you recorded or copied previously\.
**Note**  
Sometimes copying and pasting content can corrupt data\. If you encounter a "Password Failed" error when you log in, try typing in the password manually\.

1. Due to the nature of self\-signed certificates, you might get a warning that the security certificate could not be authenticated\. Use the following steps to verify the identity of the remote computer, or simply choose **Yes** or **Continue** to continue if you trust the certificate\.

   1. If you are using **Remote Desktop Connection** from a Windows PC, choose **View certificate**\. If you are using **Microsoft Remote Desktop** on a Mac, choose **Show Certificate**\.

   1. Choose the **Details** tab, and scroll down to the **Thumbest\-practicesrint** entry on a Windows PC, or the **SHA1 Fingerprints** entry on a Mac\. This is the unique identifier for the remote computer's security certificate\.

   1. In the Amazon EC2 console, select the instance, choose **Actions**, and then choose **Get System Log**\.

   1. In the system log output, look for an entry labeled `RDPCERTIFICATE-THUMbest-practicesRINT`\. If this value matches the thumbest\-practicesrint or fingerprint of the certificate, you have verified the identity of the remote computer\.

   1. If you are using **Remote Desktop Connection** from a Windows PC, return to the **Certificate** dialog box and choose **OK**\. If you are using **Microsoft Remote Desktop** on a Mac, return to the **Verify Certificate** and choose **Continue**\.

   1. \[Windows\] Choose **Yes** in the **Remote Desktop Connection** window to connect to your instance\.

      \[Mac OS\] Log in as prompted, using the default administrator account and the default administrator password that you recorded or copied previously\. You might need to switch spaces to see the login screen\. For more information about spaces, see the Apple website\.

   1. If you receive an error while attempting to connect to your instance, see [Remote Desktop can't connect to the remote computer](http://docs.aws.amazon.com/AWSEC2/latest/WindowsGuide/troubleshooting-windows-instances.html#rdp-issues)\.

## Install a web server and host your site<a name="classic-tutorials-ddos-cross-service-EC2-install-web-server"></a>

The next step is to install a web hosting service on your Amazon EC2 instance and build your website\. You have several options for a web server, such as Microsoft Internet Information Server \(IIS\), which is already part of your instance, Apache HTTP Server for Windows, and others\.

Installing a web server and configuring your website is outside the scope of this tutorial\. Refer to the proper product documentation to implement a web server on your instance\. However, as an example, at a general level, the steps for installing IIS are the following:
+ Connect to your instance as described earlier\.
+ Using Windows Server Manager, choose **Add roles and features**\.
+ Choose **Role\-based or feature\-based installation**\.
+ Choose **Web Server \(IIS\)** and begin the installation process\.
+ After the installation is complete, build your website\.

## Launch a second EC2 instance<a name="classic-tutorials-ddos-cross-service-EC2-second"></a>

You now must repeat this process \(launch another EC2 instance and build your website\) to create a duplicate of your first EC2 instance\. This is necessary to enable load balancing later in the tutorial\.

Follow all the same steps just described to launch an instance\. Be sure to edit the second instance details and security group as per the previous steps\. When editing the instance details, note the following:
+ Choose the same VPC as your first instance, the VPC that you created in the prerequisites\. 
+ For **Subnet**, choose **subnet\-2**\. This is the *second* subnet that you created in the prerequisites step\. This is *not* the same subnet that you used for your first instance\.
+ For **Auto\-assign Public IP**, choose **Enable**\.

After launching your second Amazon EC2 instance, install the same web hosting service and files as your first EC2 instance\.

## Test your website<a name="classic-tutorials-ddos-cross-service-EC2-test"></a>

You should now be able to view your website using the public address of each instance\.

**To test your Amazon EC2 instances and website**

1. In the Amazon EC2 console, select the check box next to your first instance\.

1. In the details pane, note the **Public DNS address**\.

1. Enter this address in a web browser\. You should be directed to your website\.

1. Repeat these steps for the second instance\.

Next: [Step 2: Scale your traffic using Elastic Load Balancing](classic-tutorials-ddos-cross-service-ELB.md)\.