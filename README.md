# Deploy-a-static-website-



Step 1: Creating a S3 bucket
The first step you need to take is to create an S3 bucket to put your website’s files and folders.

1.	Sign in to the AWS Management Console.
2.	Open the Amazon S3 console

This should display the S3 dashboard.





3.	Click on Create bucket.

4.	Choose a Region that is geographically close to you to minimize latency and costs, or to address regulatory requirements. The Region that you choose determines your Amazon S3 website endpoint.

 





5.	Under “Block Public Access settings for this bucket” section, uncheck the “Block all public access” checkbox and accept the acknowledgement.

 



6.	Select “Disable” for Bucket Versioning.

 





7.	Under “Default encryption” section, click on disable for Server-side encryption.

 



8.	Click on “Create bucket”.




 
Step 2: Enabling static website hosting
1.	In the Buckets list, choose the name of the bucket that you want to enable static website hosting

2.	Click on the “Properties” tab.






3.	Scroll down to the “Static website hosting” section and click on its Edit
button.






4.	Under Static website hosting, choose Enable (1). Also, select Host a static website (2) for the Hosting type. In Index document, enter the file name of the index document, typically index.html (3).
 



5.	Click on “Save Changes”. You should see the following next.

 



Under Static website hosting, note the Endpoint which is the Amazon S3 website endpoint for your bucket.
Step 3: Securing my S3 bucket through IAM policies
To allow users to access your website and to secure your S3 bucket and block uploads and/or deletions, you will need to add a bucket policy.

1.	Under Buckets, click on the name of your website bucket.


2.	Click on the “Permissions” tab.

3.	Under Bucket Policy, choose Edit.





4.	To grant public read access for your website, copy the following bucket policy, and paste it in the Bucket policy editor. Make sure to replace bucket- name with the name of your bucket.






5.	Scroll down and click on “Save changes”. You should see the following next.

Step 4: Uploading web files to my S3 bucket
After completing all the previous steps, you need to upload your website’s files and folders to your website S3 bucket.

1.	Under Buckets, click on the name of your website bucket.

2.	On the Objects tab, you can see that the bucket is currently empty, click on the Upload button.
3.	This should take you to the Upload page. Click Add files to add the website files and use Add folder to add the website folders.



Step 5: Testing my website endpoint
1.	Under Buckets, click on the name of your website bucket.



2.	Click on the “Properties” tab.


3.	scroll down to the “Static website hosting” section and click on your endpoint URL.


 



  
Registering a new domain using Route 53


1.	Sign in to the AWS Management Console and open the Route 53 console
2.	In the navigation pane, choose Domains and then Registered domains.


 

Click on “Select” to select your domain.



Routing traffic to our website on Amazon S3 with Route 53
1.	Sign in to the AWS Management Console and open the Route 53 console at https://console.aws.amazon.com/route53/
2.	In the navigation pane, choose Hosted zones.




3.Choose the name of the hosted zone that has the domain name that you want to use to route traffic to your S3 bucket
 


4.Choose Create record.
 

On the Create record page, you will create an alias record for your Apex/root domain so that it will redirect to your S3 Bucket website. You will accomplish
 
this by entering the following information: Alias: toggle the switch to “on”
Route traffic to: Alias to S3 endpoint

Region: Choose the Region for your S3 endpoint Enter S3 endpoint: Select your S3 Bucket from the list Routing Policy: Simple Routing


 

Following this, you’ll receive confirmation verifying the successful creation of the DNS record for your domain.

The certificate is created, but not yet validated; let's check its configuration:
select the two FQDNs and finally Create records:


 


All you have to do now is wait a few minutes until you see the Success status:
 

create and configure CloudFront distributions

By using CloudFront, you will be able to deploy your website in HTTPS, and get other benefits as using Edge locations to provide faster access to the website for the users.
CloudFront will act as a stepping stone between Route 53 and S3. In other words, the traffic from the website will be routed to a CloudFront distribution that will deliver it to the corresponding S3 Bucket. You will create a CloudFront distribution for each of your S3 Bucket, two in total.


Now, create your CloudFront distribution:
 
Paste the s3 endpoint url in the origin domain
 

The Default cache behavior section should look like this:

 

In the custom SSL certificate field, select the newly created certificate:
 

Once all the necessary information are filled, you can now validate the creation of your main CloudFront distribution, and move on to creating the redirect CloudFront distribution


B.
select the checkbox next to your A record for your domain. Once selected, an Edit pane will open on the right. Modify the “Route traffic to” field so that the chosen option is now “Alias to CloudFront distribution,” then proceed by clicking “Save.”

 



The website is accessible, and in HTTPS this time

 

You’ve successfully completed all the necessary steps for deploying a secure static website on AWS, utilizing Route 53 and CloudFront.
