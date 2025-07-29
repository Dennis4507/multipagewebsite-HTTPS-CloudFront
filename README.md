# multipagewebsite-HTTPS-CloudFront
 Serve The S3 Website via HTTPS with CloudFront

1. I created distribution” and in the origin settings we
set the origin domain as the S3 website endpoint.

![alt text](<Bilder/Screenshot (244).png>)

2. then i set the Default cache behavior and Viewer Protocol Policy: Redirect HTTP to HTTPS, Allowed HTTP methods: GET, HEAD and choose Choose “CachingOptimized” for 
Cache Policy

![alt text](<Bilder/Screenshot (245).png>)

3. Settings
 I set the price Class use to only North America and Europe” for cheaper/free-tier eligibility
 
 Left the Alternate domain empty and we will add ou own domain later on once we purchase the domain.

4. Click “Create distribution”
It takes a couple of minutes to deploy and we can access our website through HTTPS once deployed using our CloudFront distribution´

![alt text](<Bilder/Screenshot (247).png>)


5. would like to use my own Domain and purchased a domain on go daddy.com 

(denisriungu.de) 

next step is to request an SSL certificate from AWS Certificate Manager (ACM)

![alt text](<Bilder/Screenshot (249).png>)


Add your domain to CloudFront

Point your domain’s DNS (e.g. via Route 53 or your registrar) to CloudFront


6. Create a Hosted Zone in Route 53

On AWS Route 53 we created a Hosted Zone Domain name: denisriungu.de and enter Public Hosted Zone

![alt text](<Bilder/Screenshot (250).png>)

7. then get the Name Servers from Route 53 after creating the zone and copy the 4 NS records

![alt text](<Bilder/Screenshot (251).png>)

8. then paste them onto go daddy.

![alt text](<Bilder/Screenshot (252).png>)

Wait for DNS propagation which can take 5 minutes to several hours.

9. Add DNS Records in Route 53 + CloudFront distribution using Alias Records for denisriungu.de

![alt text](<Bilder/Screenshot (253).png>)

10. Included Name record for www which is optional but included it either way as it's using the same CloudFront distribution. 

![alt text](<Bilder/Screenshot (254).png>)



11. Updated CloudFront Alternate Domain Names (CNAMEs)and Alternate domain names (CNAMES)
I addded both

denisriungu.de

www.denisriungu.de

Chose a valid ACM certificate for both domains (must be in us-east-1)

![alt text](<Bilder/Screenshot (255).png>)

12. Redirected HTTP and HTTPS in Cloudfront under behaviours

![alt text](<Bilder/Screenshot (257).png>)

13. We also Enabled Logging on CloudFront console. Chose an S3 bucket to store logs. Saved the changes.

![alt text](<Bilder/Screenshot (258).png>)


14. This gives Me access logs in the S3 bucket like:

![alt text](<Bilder/Screenshot (261).png>)

![alt text](<Bilder/Screenshot (259).png>)

15. To ensure Cloudfront can write logs on my S3 bucket i had to provide S3 Bucket Permissions and add a Bucket Policy.

![alt text](<Bilder/Screenshot (262).png>)

16. For Safety purposes i turned off or blocked S3 Public Access and
fully rely on CloudFront and avoid the public s3 access.

![alt text](<Bilder/Screenshot (263).png>)

17: Delete on the Bucket Policy

{
  "Effect": "Allow",
  "Principal": "*",
  "Action": "s3:GetObject",
  "Resource": "arn:aws:s3:::denisriungu.de/*"
}

17. I also ensured my CloudFront distribution had an Origin Access Control (OAC) set up to read from S3 securely.

![alt text](<Bilder/Screenshot (264).png>)

 . First ensure OAC Origin Access Control is set up 

 ![alt text](<Bilder/Screenshot (288).png>)

18. Ensured that Origin access control (OAC) is enabled and attached to my Cloud front distribution”

![alt text](<Bilder/Screenshot (266).png>)

19.  Ensure S3 Bucket Policy Grants CloudFront Access Only and write the OAC Policy that allows CloudFront only to access the S3 Bucket.

![alt text](<Bilder/Screenshot (267).png>)

20. Tested to see if the security works, open the browser your S3 Bucket Link. 
and it should return Access denied.

![alt text](<Bilder/Screenshot (268).png>)

and my website links will be working just fine

Now go to https://denisriungu.de or https://www.denisriungu.de

That's all 

Thank you  

