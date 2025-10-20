# Deployment Instructions for v1.2.0

## Step 1: Push to Docker Hub (anbrme) ✅

```bash
cd /Users/alessandronurnberg/standalone_rag/local-rag/document-lake

# Login to anbrme account
docker logout
docker login -u anbrme

# Tag images
docker tag anbrme/document-lake-api:latest anbrme/document-lake-api:1.2.0

# Push to Docker Hub
docker push anbrme/document-lake-api:1.2.0
docker push anbrme/document-lake-api:latest
```

## Step 2: Update Public Releases Repository

Navigate to your public releases repo and copy these files:

```bash
# Clone your public repo (if not already)
cd ~/repos
git clone https://github.com/anbrme/document-lake-releases.git
cd document-lake-releases

# Copy the prepared files
cp /Users/alessandronurnberg/standalone_rag/local-rag/document-lake/releases-repo-files/VERSION .
cp /Users/alessandronurnberg/standalone_rag/local-rag/document-lake/releases-repo-files/README.md .
cp /Users/alessandronurnberg/standalone_rag/local-rag/document-lake/releases-repo-files/CHANGELOG.md .
cp /Users/alessandronurnberg/standalone_rag/local-rag/document-lake/docker-compose.prod.yml docker-compose.yml

# Commit and push
git add VERSION README.md CHANGELOG.md docker-compose.yml
git commit -m "Release v1.2.0 - Fix critical multi-tenancy query bug"
git push origin main
```

## Step 3: Verify Deployment

### Check Docker Hub
Visit: https://hub.docker.com/r/anbrme/document-lake-api/tags

You should see:
- ✅ `1.2.0` tag
- ✅ `latest` tag

### Check Releases Repo
Visit: https://github.com/anbrme/document-lake-releases

You should see:
- ✅ VERSION file showing `1.2.0`
- ✅ README.md
- ✅ CHANGELOG.md
- ✅ docker-compose.yml

### Test Auto-Update Detection
```bash
# Check that your API can see the new version
curl "http://localhost:5001/check-update?user_id=test"
```

Should return:
```json
{
  "current_version": "1.1.0",
  "latest_version": "1.2.0",
  "update_available": true
}
```

## Step 4: Update Your Local Installation (Optional)

To use the Docker Hub version locally:

```bash
cd /Users/alessandronurnberg/standalone_rag/local-rag/document-lake

# Use production compose file
docker compose -f docker-compose.prod.yml pull
docker compose -f docker-compose.prod.yml up -d
```

Or keep using the development version with build.

## What Your Users Will See

1. **Automatic notification** in Document Lake UI: "Update available: v1.2.0"
2. They click **"Update Now"**
3. System automatically pulls `anbrme/document-lake-api:1.2.0` and restarts
4. Fixed bug: Documents now appear in the UI!

## Migration from ncdatadocker (Optional)

If you want to maintain backward compatibility:

```bash
# Also push to old registry
docker logout
docker login -u ncdatadocker
docker tag anbrme/document-lake-api:1.2.0 ncdatadocker/document-lake-api:1.2.0
docker tag anbrme/document-lake-api:latest ncdatadocker/document-lake-api:latest
docker push ncdatadocker/document-lake-api:1.2.0
docker push ncdatadocker/document-lake-api:latest
```

Add note in CHANGELOG about migration.

## Troubleshooting

### Docker Push Permission Denied
- Ensure logged into correct account: `docker login -u anbrme`
- Check repository exists on Docker Hub
- Verify you have write access

### Update Not Detected
- Check UPDATE_CHECK_URL in docker-compose.yml points to correct repo
- Verify VERSION file is accessible: `curl https://raw.githubusercontent.com/anbrme/document-lake-releases/main/VERSION`
- Check API logs: `docker compose logs api | grep update`

## Next Release Checklist

For future releases:

1. ✅ Update `api/VERSION` file
2. ✅ Build and test locally
3. ✅ Tag with new version: `docker tag anbrme/document-lake-api:latest anbrme/document-lake-api:X.Y.Z`
4. ✅ Push to Docker Hub
5. ✅ Update public releases repo VERSION file
6. ✅ Update CHANGELOG.md
7. ✅ Users get automatic notification

---

**Current Status:** Ready to deploy v1.2.0 🚀
