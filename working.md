# Task 1 — Static Portfolio Hosting on AWS

---

## Phase 1: Local Development

- **Created the Web Asset:** Authored a local HTML file named `zafar.portfolio.html` containing the portfolio content.

---

## Phase 2: Object Storage Deployment (Amazon S3)

- **Provisioned a Bucket:** Created a globally unique Amazon S3 bucket (`zafaralichatha.portfolio`) to host the website without provisioning a traditional server.
- **Modified Account Perimeter:** Unchecked *Block all public access* and acknowledged the security warning to allow the bucket to serve public internet traffic.
- **Uploaded Assets:** Uploaded `zafar.portfolio.html` directly into the S3 bucket.

---

## Phase 3: Infrastructure Configuration

- **Enabled Static Website Hosting:** Navigated to the bucket properties and activated the static website hosting feature.
- **Configured Index Document:** Initially encountered a `404 NoSuchKey` error because the system defaulted to searching for `index.html`. Corrected the configuration by explicitly setting the Index document to `zafar.portfolio.html`.
- **Applied Resource Policy:** Authored and applied a custom JSON Bucket Policy using the `s3:GetObject` action and the `*` (global) principal, granting public read permissions strictly to objects inside the bucket.
- **Initial Live URL:**
  ```
  http://zafaralichatha.portfolio.s3-website.eu-north-1.amazonaws.com/
  ```

---

## Phase 4: Global Content Delivery & Security Upgrade (Amazon CloudFront)

- **Diagnosed Mobile Access Failure:** Identified that modern mobile browsers reset the connection because the raw S3 endpoint only supported unencrypted HTTP traffic.
- **Deployed an Edge CDN:** Created a new Amazon CloudFront distribution (`my-portfolio-cdn`) to act as a secure, globally distributed edge layer.
- **Configured Origin:** Set the origin to the exact S3 website endpoint rather than the standard bucket endpoint.
- **Optimized for Cost:** Explicitly disabled the Web Application Firewall (WAF) to avoid a $14/month charge, keeping the architecture entirely within the free tier.
- **Final Secure Deployment:** CloudFront provisioned a free SSL/TLS certificate and distributed the cached website globally.
- **Final HTTPS Endpoint:**
  ```
  https://d2ngehk3h2inf3.cloudfront.net
  ```