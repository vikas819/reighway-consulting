# GitHub Actions Deployment Setup

## Quick Setup (Password Authentication)

### Step 1: Add GitHub Secret

1. Go to your GitHub repository
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret**
4. Add the following:

   **Name:** `SSH_PASSWORD`  
   **Value:** `cNbc^5,XrJr6`

5. Click **Add secret**

### Step 2: Push Your Code

The workflow will automatically run when you push to the `production` branch.

```bash
git add .
git commit -m "Update deployment workflow"
git push origin production
```

### Step 3: Monitor Deployment

1. Go to your GitHub repository
2. Click the **Actions** tab
3. You'll see the deployment workflow running
4. Click on it to see the deployment progress

## Server Details

- **Host:** 145.79.212.148
- **Port:** 65002
- **Username:** u152908012
- **Deployment Path:** domains/reighway.com/public_html/

## What Gets Deployed

All files except:
- `.git/` folder
- `.github/` folder
- `node_modules/`
- `.DS_Store` files
- `*.md` files
- `old/` folder

## Manual Deployment (if needed)

If you need to deploy manually:

```bash
# Install sshpass first
brew install sshpass  # macOS
# or
sudo apt-get install sshpass  # Linux

# Deploy
sshpass -p "cNbc^5,XrJr6" rsync -avz --delete \
  -e "ssh -p 65002" \
  --exclude='.git' \
  --exclude='.github' \
  --exclude='node_modules' \
  --exclude='old' \
  ./ u152908012@145.79.212.148:domains/reighway.com/public_html/
```

## Troubleshooting

- **Permission denied:** Check that the SSH_PASSWORD secret is set correctly
- **Connection timeout:** Verify server IP and port are correct
- **Deployment fails:** Check the Actions tab logs for detailed error messages

