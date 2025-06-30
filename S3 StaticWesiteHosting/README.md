# AWS S3 Static Website Hosting

## What are S3 Buckets?

**Amazon S3 (Simple Storage Service)** buckets are containers that hold your files in the cloud. Think of them as folders on the internet where you can store websites, images, documents, and any other files. S3 buckets are:

- **Globally accessible** - Anyone can access your files (if you allow it)
- **Highly durable** - Your files are safely stored across multiple locations
- **Cost-effective** - Pay only for what you store and transfer
- **Scalable** - Store unlimited amounts of data

## Bucket Versioning

**Versioning** keeps multiple versions of the same file in your bucket. When you upload a new version of `index.html`, S3 keeps the old version too.

**Benefits:**
- **Backup protection** - Accidentally deleted files can be recovered
- **Change tracking** - See all versions of your files
- **Rollback capability** - Easily restore previous versions

---

## Static Website Hosting Setup (UI Steps)

### Step 1: Create S3 Bucket
1. Go to **AWS Console** → **S3**
2. Click **"Create bucket"**
3. Enter unique bucket name (e.g., `my-website-2025-unique`)
4. Choose your region
5. Click **"Create bucket"**

### Step 2: Upload Website Files
1. Open your new bucket
2. Click **"Upload"**
3. Drag and drop your `index.html` file
4. Click **"Upload"**

### Step 3: Enable Static Website Hosting
1. Go to your bucket → **"Properties"** tab
2. Scroll down to **"Static website hosting"**
3. Click **"Edit"**
4. Select **"Enable"**
5. Index document: `index.html`
6. Click **"Save changes"**
7. **Copy the generated URL** (you'll need this)

### Step 4: Test (Will Show 403 Error)
1. Click the generated website URL
2. You'll see **"403 Forbidden"** error
3. This is normal! We need to fix permissions next

### Step 5: Fix Public Access
1. Go to **"Permissions"** tab
2. Find **"Block public access"**
3. Click **"Edit"**
4. **Uncheck all boxes** (disable blocking)
5. Click **"Save changes"**
6. Type `confirm` when prompted

### Step 6: Add Bucket Policy
1. Still in **"Permissions"** tab
2. Scroll to **"Bucket policy"**
3. Click **"Edit"**
4. Paste this JSON (replace `YOUR-BUCKET-NAME`):

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
        }
    ]
}
```

5. Replace `YOUR-BUCKET-NAME` with your actual bucket name
6. Click **"Save changes"**

### Step 7: Success! 🎉
1. Go back to the website URL from Step 3
2. **Boom!** Your website is now live on AWS S3
3. Share the URL with anyone

---

## Quick Checklist ✅

- [ ] Created S3 bucket with unique name
- [ ] Uploaded index.html file
- [ ] Enabled static website hosting
- [ ] Disabled block public access
- [ ] Added bucket policy with correct bucket name
- [ ] Website loads successfully

## Troubleshooting

**Still getting 403 error?**
- Double-check bucket policy has your exact bucket name
- Ensure all public access blocks are disabled
- Wait 5-10 minutes for changes to take effect

**Website not updating?**
- Clear your browser cache
- Upload new files to replace old ones
- Check file names match exactly

---

## File Structure
```
S3 Bucket/
├── index.html          # Your main website file
├── style.css           # CSS files (optional)
├── script.js           # JavaScript files (optional)
└── images/             # Images folder (optional)
```

## Benefits of S3 Static Hosting

✅ **Fast** - Global content delivery  
✅ **Cheap** - Pay only for storage and bandwidth  
✅ **Reliable** - 99.999999999% durability  
✅ **Easy** - No server management required  
✅ **Secure** - AWS enterprise-grade security  

---

**Your website is now live on the internet using AWS S3! 🚀**