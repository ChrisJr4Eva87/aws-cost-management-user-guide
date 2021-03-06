# Getting Started<a name="billing-getting-started"></a>

The following steps discuss a few of the most common tasks you're likely to perform when using the Billing and Cost Management console\. 


+ [Step 1: Review Your Usage](#billing-gs-review)
+ [Step 2: Turn on Reports](#step-2)
+ [Step 3: Download or Print Your Bill](#billing-gs-download)
+ [Step 4: Set Up Alerts to Monitor Charges to Your Account](#billing-gs-alerts)
+ [Step 5: Get Answers to Questions About Your Bill](#billing-gs-answer)
+ [Where Do I Go from Here?](#whereto)

## Step 1: Review Your Usage<a name="billing-gs-review"></a>

Billing and Cost Management offers you a number of different ways to view and monitor your AWS usage\. Here's how to quickly check to see what you've used so far in the current month\.

**To open the Billing and Cost Management console and review your usage and charges**

1.  Sign in to the AWS Management Console and open the Billing and Cost Management console at [https://console\.aws\.amazon\.com/billing/](https://console.aws.amazon.com/billing/)\. The console opens to the **Dashboard**, where you can see your current month\-to\-date usage graphs\. 

1. On the navigation pane, choose the applicable option:  
**Cost Explorer**  
 Choose [https://console.aws.amazon.com/cost-reports/home?#/custom](https://console.aws.amazon.com/cost-reports/home?#/custom) to track and analyze your AWS usage\. Cost Explorer is free for all accounts\. For more information about Cost Explorer, see [Analyzing Your Costs with Cost Explorer](cost-explorer-what-is.md)\.   
**Budgets**  
 Choose [https://console.aws.amazon.com/billing/home?region=us-east-1#/budgets](https://console.aws.amazon.com/billing/home?region=us-east-1#/budgets) to view, create, or delete budgets for your account\. For more information about budgets, see [Monitoring Your Usage and Costs](monitoring-costs.md)\.   
You can also check the status of your free tier usage using the provided AWS Free Tier usage alerts using AWS Budgets\. For more information about AWS Free Tier usage alerts, see [AWS Free Tier Usage Alerts Using AWS Budgets](tracking-free-tier-usage.md#free-budget)\.   
**Bills**  
 Choose [https://console.aws.amazon.com/billing/home?region=us-east-1#/bill](https://console.aws.amazon.com/billing/home?region=us-east-1#/bill) to see details about your current charges\.   
**Payment History**  
 Choose [https://console.aws.amazon.com/billing/home?region=us-east-1#/paymenthistory/history?redirected](https://console.aws.amazon.com/billing/home?region=us-east-1#/paymenthistory/history?redirected) to see your past payment transactions\. 

## Step 2: Turn on Reports<a name="step-2"></a>

 In addition to the features described in step 1, AWS Billing and Cost Management offers a set of billing reports about your AWS usage\. The reports show you which AWS services that you used, the amount of time that you used them, the amount of data that you transferred in and out of storage, the average storage space that you use, and more\. 

 Billing and Cost Management can deliver your reports to an Amazon S3 bucket that you create\. Amazon S3 is the AWS Cloud storage offering\. The Amazon S3 bucket must be owned by the payer account\. Reports cannot be delivered to a bucket owned by a linked account\. 

**Create an Amazon S3 bucket for your reports**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose **Create Bucket**\.

1. In the dialog box, for **Bucket Name**, enter the name for your bucket\.
**Note**  
Your bucket name must be all lowercase, from 3 to 63 characters long, and cannot contain spaces\. You can use lowercase letters, numbers, hyphens \(\-\), and periods \(\.\) in your bucket name\.

1. Choose the region that you want your Amazon S3 bucket to be in\.

1.  \(Optional\) If you choose **Set Up Logging**, you can enable access logs that track who accesses your Amazon S3 bucket\. Choose the bucket that you want the access logs to be delivered to, and the name of a folder that you want the logs to be stored in\. 

1. Choose **Create**\.

**Grant Billing and Cost Management permission to deliver reports to your Amazon S3 bucket**

1. Open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Choose the bucket in which you want to receive reports\.

1. Choose **Permissions**\.

1. Choose **Bucket Policy**\.

1. Paste the following text into the bucket policy editor\.

   ```
   {
     "Version": "2012-10-17",
     "Statement": [
     {
       "Effect": "Allow",
       "Principal": {
         "AWS": "386209384616"
       },
       "Action": [
         "s3:GetBucketAcl",
         "s3:GetBucketPolicy"
       ],
       "Resource": "arn:aws:s3:::bucketname"
     },
     {
       "Effect": "Allow",
       "Principal": {
         "AWS": "386209384616"
       },
       "Action": "s3:PutObject",
       "Resource": "arn:aws:s3:::bucketname/*"
     }
     ]
   }
   ```

1. Replace *bucketname* with the name of your bucket\. Don't replace the **Principal** number `386209384616`\. AWS uses that account to deliver reports to the S3 bucket\.

1. Choose **Save**\.

**Create an AWS Cost and Usage report**

1. Sign into the AWS Management Console and open the Billing and Cost Management console at [https://console\.aws\.amazon\.com/billing/](https://console.aws.amazon.com/billing/)

1. On the navigation pane, choose **Reports**\.

1. Choose **Create report**\.

1. For **Report name**, type a name for your report\.

1.  For **Time unit**, choose **Hourly** if you want the line items in the report to be aggregated by the hour\. Choose **Daily** if you want the line items in the report to be aggregated by the day\. 

1.  For **Include**, to include the IDs of each individual resource in the report, select Resource IDs\. To include manifests that enable you to upload the report to Amazon Redshift or Amazon QuickSight, select **Redshift Manifest** or **QuickSight Manifest**\. If you select a manifest, your report is stored with `.gz` compression\. 

1.  For **Enable support for\.\.\.**, select whether you want to upload your AWS Cost and Usage report to Amazon Redshift or Amazon QuickSight\. 

1. Choose **Next**\.

1.  For **S3 bucket**, type the name of the **S3 bucket** where you want the reports to be delivered, and choose **Verify**\. The bucket must have appropriate permissions to be valid\. For more information on adding permissions to the bucket, see [Setting Bucket and Object Access Permissions](http://docs.aws.amazon.com/AmazonS3/latest/user-guide/set-permissions.html)\. 

1.  For **Report path prefix**, type the prefix that you want to prepend to the name of your report\. 

1. Choose **Next**\.

1.  After you have reviewed the settings for your report, choose **Review and Complete**\. 

## Step 3: Download or Print Your Bill<a name="billing-gs-download"></a>

 AWS Billing and Cost Management closes the billing period at midnight on the last day of each month, and then calculates your bill\. Most bills are ready for you to download by the seventh accounting day of the month\. 

**To download your bill**

1.  Sign into the AWS Management Console and open the Billing and Cost Management at [https://console\.aws\.amazon\.com/billing/](https://console.aws.amazon.com/billing/)\. 

1. On the navigation pane, choose **Bills**\.

1. For **Date**, choose the month of the bill you want to work with\.

1. Choose **Download CSV** to download a comma\-separated variable file, or choose **Print**\.

## Step 4: Set Up Alerts to Monitor Charges to Your Account<a name="billing-gs-alerts"></a>

If you use the AWS Free Tier, Billing and Cost Management automatically provides AWS Free Tier usage alerts via AWS Budgets to track your free tier usage and notify you when you go over the free tier limits or are forecasted to go over the free tier limits\. AWS sends these notifications to the email that you used to create your AWS account\.

In addition to the free tier usage alerts, you can use budgets or Amazon CloudWatch to create and email alerts to you when your monthly charges for using an AWS product exceed a threshold that you set\. These alerts can be set only for exceeding a threshold\. If you want to be alerted before a certain threshold is reached, create an alert for a threshold that is lower than the one that you don't want to exceed\. Alerts are emails that AWS sends when a CloudWatch alarm triggers\. CloudWatch alarms are alarms that monitor your services\. To create alarms that notify you, you must first enable alerts and then create the alarm\. You need to enable alerts only once\.

**Important**  
Turning on billing alerts enables the creation of billing alarms, but does not create any alarms for you\. For best results, wait at least 15 minutes after enabling alerts before you create a CloudWatch alarm\.

 By default, IAM users don't have access to billing information, and therefore do not have access to billing alerts or alarms\. If you are logged in to AWS as an IAM user, verify that the AWS account owner has granted IAM users access to the billing information\. For more information about IAM restrictions, see [Granting Access to Your Billing Information and Tools](grantaccess.md)\. 

**Note**  
If your account is linked to a reseller account, billing alerts are not available for your account\. 

**To enable billing alerts**

Before you create a billing alarm, you must enable billing alerts\. You need to do this only once\. After you enable billing alerts, you can't turn them off\.

1. Sign in to the AWS Management Console and open the Billing and Cost Management console at [https://console\.aws\.amazon\.com/billing/home\#/](https://console.aws.amazon.com/billing/home)\.

1. On the navigation pane, choose **Preferences**\.

1. Select the **Receive Billing Alerts** check box\.

1. Choose **Save preferences**\.

**To create a billing alarm**

1.  \(Optional\) If you want to send your alert to an AWS\-managed distribution list instead of a single email address, follow these steps to set up an Amazon Simple Notification Service \(Amazon SNS\) notification list\. If you want to send your alert to a single email address, go to step 2\. 

   To create an Amazon SNS notification list:

   1. Open the Amazon SNS console at [https://console\.aws\.amazon\.com/sns/v2/home](https://console.aws.amazon.com/sns/v2/home)\.

   1. On the navigation pane, choose **SNS Home**\.

   1. In the **Common actions** section, choose **Create topic**\.

   1. In the dialog box, for **Topic name**, enter the name for your notification list\.

   1. \(Optional\) If you want to use this notification list to send SMS messages, for **Display name**, enter the name you want to appear on your SMS messages\.

   1. Choose **Create topic**\.

1. Open the CloudWatch console at [https://console\.aws\.amazon\.com/cloudwatch/](https://console.aws.amazon.com/cloudwatch/)\.

1.  If necessary, change the region on the navigation bar to US East \(N\. Virginia\)\. The billing metric data is stored in this region, even for resources in other regions\. 

1. On the navigation pane, under **Metrics**, choose **Billing**\.

1.  In the list of billing metrics, select the check box next to **Currency** `USD`, for the metric named **EstimatedCharges**\. 

1. Choose **Create Alarm**\.

1. Define the alarm as follows\.

   1. If you want the alarm to trigger as soon as you go over the free tier, set **When my total AWS charges for the month exceed** to $\.01\. This means that you receive a notification as soon as you incur a charge\. Otherwise, set it to the amount you want to trigger the alarm, and you will be notified when you go over that amount\. 

   1. Choose the **New list** link next to the **send a notification to** box\. 

   1.  When prompted, enter your email address or choose your Amazon SNS notification from the dropdown list\. 

   1. Choose **Create Alarm**\.

1. In the **Confirm new email addresses** dialog box, confirm the email address or choose **I will do it later**\. If you don't confirm the email address now, the alarm remains in the `Pending confirmation` status until you do so, and does not send an alert\. To view the status of your alarm, choose **Alarms** in the navigation pane\. 

 For more information about CloudWatch alarms, see [Monitor Your Estimated Charges Using Amazon CloudWatch](http://docs.aws.amazon.com/AmazonCloudWatch/latest/DeveloperGuide/monitor_estimated_charges_with_cloudwatch.html) in the *Amazon CloudWatch User Guide*\. 

## Step 5: Get Answers to Questions About Your Bill<a name="billing-gs-answer"></a>

If you have questions about your bill, see the [AWS Knowledge Center](http://aws.amazon.com/premiumsupport/knowledge-center/)\. If you don't find the answer you're looking for in the Knowledge Center, you can access account and billing support free of charge\. For more information about AWS Support, see [Contacting Customer Support About Your Bill](billing-get-answers.md)\. For information about closing your account, see [Closing an Account](close-account.md)\.

## Where Do I Go from Here?<a name="whereto"></a>

 Explore some of the features designed to help you dig a little deeper and streamline your accounting practices\. 

+ [Tracking Your AWS Free Tier Usage](tracking-free-tier-usage.md)

+ [Understanding Your Usage with Billing Reports](billing-reports.md)

+ [Analyzing Your Costs with Cost Explorer](cost-explorer-what-is.md)

+ [Managing Your Costs with Budgets](budgets-managing-costs.md)

+ [Consolidated Billing for Organizations](consolidated-billing.md)