<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Website Delivery with CloudFront

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-cloudfront)

**Author:** Łukasz Brodziak  
**Email:** lukasz.brodziak@gmail.com

---

## Website Delivery with CloudFront

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-networks-cloudfront_1dddddwe)

---

## Introducing Today's Project!

In this project, I will host a static website on S3 bucket and make it globally available using AWS CloudFront. I am doing this project to learn about ways of ensuring efficient and scalable content delivery. Also this project serves as an introduction to Three-Tier application architecture, by introducing the first tier which is presentation layer.

### Tools and concepts

Services I used were S3 and CloudFront. Key concepts I learnt include content delivery network (CDN), and static website hosting on S3.

### Project reflection

This project took me approximately 60 minutes. The most challenging part was setting up proper permissions.

I chose to do this project today because I wanted to learn about Three-tier architecture and website hosting with CloudFront.

---

## Set Up S3 and Website Files

I started the project by creating an S3 bucket to store the project website files in it. I can't use CloudFront for this task because CloudFront is a Content Delivery Network(CDN) which hosts content that is stored elsewhere, like in the S3 bucket.

The three files that make up my website are index.html, which. is the main file that organizes content of the page, style.css, which defines styles for website's elements, and script.js, which holds code responsible for page interactions.

I validated that my website files work by viewing the downloaded index.html file in my browser.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-networks-cloudfront_qgo7wcd3)

---

## Exploring Amazon CloudFront

Amazon CloudFront is is a Content Delivery Network (CDN), which means it speeds up the distribution of your static and dynamic web content, such as .html, .css, .js, and image files. Businesses and developers use CloudFront because it helps with optimizing the content delivery process.

To use Amazon CloudFront, you set up distributions,.A CloudFront distribution is a set of instructions that tells CloudFront how to deliver your content.
It specifies where your website's files are stored (called the origin), how they should be cached, and other delivery settings like security standards. I set up a distribution for the single web app. The origin is set to S3 bucket created in previous steps.

My CloudFront distribution's default root object is index.html file. This means that when user navigates to root of the website the file delivered will be index.html

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-networks-cloudfront_qgo7wcdt)

---

## Handling Access Issues

When I tried visiting my distributed website, I ran into an access denied error because of the permissions set to objects in S3 bucket. By default all objects stored in S3 are private. I need change their permissions in order to make them accessible.

My distribution's origin access settings were "Origin access control settings (recommended)". This caused the access denied error because by default all objects in S3 are private and not accessible.

To resolve the error, I set up origin access control (OAC). OAC is a special user for CloudFront that prevents this. An OAC lets you keep your S3 bucket and objects not publicly accessible, while still making sure they can be accessed through CloudFront. OAC also gives you granular control over how CloudFront accesses the content. For example, you can add other authentication or security settings to make sure only legitimate users can access your content.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-networks-cloudfront_egrhntyu)

---

## Updating S3 Permissions

Once I set up my OAC, I still needed to update my bucket policy because objescts are still private.

Creating an OAC automatically gives me a policy I could copy, which grants access to S3 bucket objects.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-networks-cloudfront_eg98ntyu)

---

## S3 vs CloudFront for Hosting

For my project extension, I'm comparing hosting website on S3 vs CloudFront. I initially had an error with static website hosting because public access is blocked by default.

I tried resolving this by allowing all public access. I still ran into an error because there is no policy explicitly granting access to these files.

I could finally see my S3 hosted website when I updated the bucket policy. This worked because the policy gratns explicitly access to anyone on the internet.

Compared to the permission settings for my CloudFront distribution, using S3 meant that anyone would have direct access to my S3 bucket's objects. I preferred the CloudFront approach as it introduces another layer between content and user making access more secure.

---

## S3 vs CloudFront Load Times

Load time means how much time it takes to access the site. The load times for the CloudFront site were faster than the S3 site because CloudFront caches content closer to users globally, while S3 static website hosting serves files directly from a single region.
This means data travels a much shorter distance from an edge location to the end user.

A business would prefer CloudFront when they want to ensure efficiency and low latency. S3 static website hosting might be sufficient when we have a simple websites with no high performance/low latency requirements.

![Image](http://learn.nextwork.org/surprised_maroon_fierce_chinese_gooseberry/uploads/aws-networks-cloudfront_12verpuh)

---

---
