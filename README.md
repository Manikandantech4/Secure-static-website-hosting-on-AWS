# Secure-static-website-hosting-on-AWS
Developed and deployed a static portfolio website on AWS using secure and scalable architecture without exposing the S3 bucket to public access.

Key Highlights:

1. Created a responsive static website using HTML, CSS, and JavaScript.
2. Hosted static content on a private S3 bucket, with CloudFront as a secure content delivery layer using Origin Access Control (OAC).
3. Configured Amazon Route 53 for custom domain routing and DNS management.
4. Enabled HTTPS and SSL certificate via AWS Certificate Manager for secure website access.

   <img width="692" height="117" alt="Screenshot 2025-07-28 at 10 41 25 AM" src="https://github.com/user-attachments/assets/ba0c0520-adc3-4d5f-9635-3f26fe3ec89d" />


✅ Step-by-Step Deployment

1. Created a Private S3 Bucket

Went to AWS Console > S3 > Create bucket

Bucket name: manikandanr.info

Kept this checked "Block all public access" (i.e., bucket remains private)

Created the bucket

Uploaded your website files (e.g., index.html, style.css)

2. Request SSL Certificate with ACM

Went to ACM (Certificate Manager)

Requested a public certificate

Added domain name: manikandanr.info

Chose DNS validation

Copied DNS validation CNAME and added it in Route 53

Waited until status becomes Issued

3. Create CloudFront Distribution

Went to CloudFront > Create distribution

Origin:

Origin domain: my S3 bucket name (selected from dropdown)

Origin access: Created OAC (Origin Access Control)

Viewer protocol policy: Redirect HTTP to HTTPS

Alternate domain name (CNAME): manikandar.info

Custom SSL certificate: Selected the ACM cert

Default root object: index.html

Clicked Create distribution

4. Attached OAC Permissions to Bucket

After distribution is created, got the OAC settings

Went to your S3 bucket > Permissions > Bucket Policy

Pasted the policy.

5. Set Up Route 53

Went to Route 53 > Hosted zones > my domain

Created a new A Record:

Type: A

Alias: Yes

Alias target: Selected my CloudFront distribution

6. Test my Website

Visit https://www.manikandanr.info — the site should loads securely over HTTPS using CloudFront.

