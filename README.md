# Secure-static-website-hosting-on-AWS
Developed and deployed a static portfolio website on AWS using secure and scalable architecture without exposing the S3 bucket to public access.

Goals:

1. Create a responsive static website using HTML, CSS, and JavaScript.
2. Host static content on a private S3 bucket, with CloudFront as a secure content delivery layer using Origin Access Control (OAC).
3. Configur Amazon Route 53 for custom domain routing and DNS management.
4. Enable HTTPS and SSL certificate via AWS Certificate Manager for secure website access.

 <img width="692" height="117" alt="Screenshot 2025-07-28 at 10 49 12 AM" src="https://github.com/user-attachments/assets/f800a186-6039-4e12-9bc6-971d873851a9" />

Steps:

1. Create a Private S3 Bucket and keep this checked "Block all public access" (i.e., bucket remains private) and Upload the website files (e.g., index.html, style.css)

2. Request SSL Certificate with ACM
   
Go to ACM (Certificate Manager)

Request a public certificate

Add domain name: manikandanr.info

Choose DNS validation

Copy DNS validation CNAME and add it in Route 53

Wait until status becomes Issued.

4. Create CloudFront Distribution
   
Origin domain: my S3 bucket name (selected from dropdown)

Origin access: Created OAC (Origin Access Control)

Viewer protocol policy: Redirect HTTP to HTTPS

Alternate domain name (CNAME): manikandar.info

Custom SSL certificate: Selected the ACM cert

Default root object: index.html

Click Create distribution

5. Attached OAC Permissions to Bucket
   
After distribution is created, got the OAC settings

Go to your S3 bucket > Permissions > Bucket Policy

Past the policy.

6. Set Up Route 53
   
Go to Route 53 > Hosted zones > my domain

Creat a new A Record:

Type: A

Alias: Yes

Alias target: Selected my CloudFront distribution

7. Test my Website
   
Visit https://www.manikandanr.info — the site should loads securely over HTTPS using CloudFront.

