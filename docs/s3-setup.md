# S3 Setup - AutoSync Portfolio

## Bucket Details

**Bucket Name:** autosync-portfolio-yourname
**Region:** us-east-1
**Website Endpoint:** http://autosync-portfolio-yourname.s3-website-us-east-1.amazonaws.com

## Configuration

### Static Website Hosting
- **Status:** Enabled
- **Index document:** index.html
- **Error document:** index.html

### Public Access
- **Block Public Access:** Disabled
- **Bucket Policy:** Allows public read access (s3:GetObject)

### Versioning
- **Status:** Enabled
- **Why:** Allows recovery of previous file versions

## Bucket Policy
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "PublicReadGetObject",
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::autosync-portfolio-yourname/*"
    }
  ]
}
```

## Deployment Methods

### Method 1: AWS Console Upload
1. S3 Console → Bucket → Upload
2. Select files
3. Upload

### Method 2: AWS CLI
```bash
aws s3 cp index.html s3://autosync-portfolio-yourname/
```

### Method 3: Sync Entire Folder (Future)
```bash
aws s3 sync ./frontend/public s3://autosync-portfolio-yourname/ --delete
```

## Cost Estimation

**Current usage:**
- Storage: ~5KB (index.html)
- Requests: ~100/month (testing)

**Estimated cost:** $0.01/month (effectively free)

**Free tier includes:**
- 5GB storage
- 20,000 GET requests
- 2,000 PUT requests

## Design Decisions

**Why S3 for hosting?**
- Serverless (no server management)
- Highly available (99.99% uptime SLA)
- Scalable (handles traffic spikes automatically)
- Cost-effective ($0.50-2/month for small sites)
- Integrates with CloudFront for global CDN

**Why versioning enabled?**
- Accidental file deletions can be recovered
- Can rollback to previous versions
- Minimal cost impact (~$0.01/month extra)

## Next Steps

- [ ] Add CloudFront distribution (Week 2)
- [ ] Set up custom domain (Week 3)
- [ ] Implement CI/CD pipeline (Week 4)
- [ ] Deploy React application (Week 2)
