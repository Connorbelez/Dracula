# Deployment Guide for Dracula Enhanced

This guide walks you through publishing your theme to the VSCode Marketplace and setting up automated CI/CD with GitHub Actions.

## Prerequisites

- A GitHub account
- A Microsoft/Azure account for VSCode Marketplace
- Node.js 16+ installed
- Git installed

## Step 1: Create a Visual Studio Marketplace Publisher

1. **Create a Microsoft Account** (if you don't have one)
   - Go to https://login.live.com and create an account

2. **Create a Publisher**
   - Navigate to https://marketplace.visualstudio.com/manage
   - Sign in with your Microsoft account
   - Click **"Create publisher"**
   - Fill in the required information:
     - **Name**: Your name or organization (e.g., "connor")
     - **ID**: A unique identifier (must match `publisher` in `package.json`)
     - **Display name**: What users will see
     - **Email**: Your contact email

3. **Save your Publisher ID**
   - Note down the Publisher ID - it should match the `publisher` field in `package.json`
   - Current value in package.json: `connor`

## Step 2: Generate a Personal Access Token (PAT)

1. Go to https://dev.azure.com
2. Click on your profile icon → **"Personal access tokens"**
3. Click **"+ New Token"**
4. Configure the token:
   - **Name**: `vscode-marketplace-publish`
   - **Organization**: Select **"All accessible organizations"**
   - **Expiration**: Choose your preferred duration (90 days, 1 year, or custom)
   - **Scopes**: Select **"Custom defined"**
   - Under **Marketplace**, check:
     - ✅ **Acquire** (to publish extensions)
     - ✅ **Manage** (to update/delete extensions)
5. Click **"Create"**
6. **IMPORTANT**: Copy the token immediately - you won't be able to see it again!

## Step 3: Test Local Publishing

Before setting up CI/CD, test publishing manually:

```bash
# Install dependencies
npm install

# Build the theme
npm run build

# Package the extension
npm run package

# Test publishing (replace YOUR_TOKEN with your actual PAT)
npx vsce publish -p YOUR_TOKEN
```

If this succeeds, you're ready for automated deployment!

## Step 4: Set Up GitHub Secrets

1. Go to your GitHub repository
2. Navigate to **Settings** → **Secrets and variables** → **Actions**
3. Click **"New repository secret"**
4. Add the following secret:
   - **Name**: `VSCE_PAT`
   - **Value**: Your Personal Access Token from Step 2

The `GITHUB_TOKEN` is automatically provided by GitHub Actions, so you don't need to create it.

## Step 5: Update package.json Publisher Name

Make sure the `publisher` field in `package.json` matches your Publisher ID from Step 1:

```json
{
  "publisher": "your-publisher-id"
}
```

## Step 6: Create Initial Git Repository (if not done)

```bash
# Initialize git repository
git init

# Add all files
git add .

# Initial commit
git commit -m "Initial commit: Dracula Enhanced theme"

# Create GitHub repository and push
# (Follow GitHub instructions for creating a new repo)
git remote add origin https://github.com/YOUR_USERNAME/dracula-enhanced.git
git branch -M main
git push -u origin main
```

## Step 7: Publishing Workflow

### Automated Publishing (Recommended)

The theme will automatically publish when you push a version tag:

```bash
# Update version in package.json (or use npm version)
npm version patch  # 1.0.0 → 1.0.1
# or
npm version minor  # 1.0.0 → 1.1.0
# or
npm version major  # 1.0.0 → 2.0.0

# Push the tag
git push --follow-tags
```

This will trigger the GitHub Action to:
1. ✅ Build the theme
2. ✅ Run linting
3. ✅ Package the extension
4. ✅ Publish to VSCode Marketplace
5. ✅ Create a GitHub Release with the .vsix file

### Manual Publishing

If you prefer to publish manually:

```bash
# Build and package
npm run build
npm run package

# Publish
npm run vsce-publish
```

## Step 8: Verify Publication

1. Wait 5-10 minutes after publishing
2. Visit https://marketplace.visualstudio.com/items?itemName=YOUR_PUBLISHER.dracula-enhanced
3. Or search in VSCode: Open Extensions → Search "Dracula Enhanced"

## CI/CD Workflows Explained

### 1. `publish.yml` - Automated Publishing
**Triggers**: 
- When you push a tag matching `v*.*.*` (e.g., `v1.0.0`)
- Manual workflow dispatch

**What it does**:
- Builds and validates the theme
- Publishes to VSCode Marketplace
- Creates a GitHub Release
- Uploads .vsix artifact

### 2. `ci.yml` - Continuous Integration
**Triggers**: 
- Push to `main` or `develop` branches
- Pull requests to `main` or `develop`

**What it does**:
- Tests build on Node.js 16, 18, 20
- Validates JSON structure
- Packages extension
- Uploads artifacts for review

## Versioning Strategy

Follow [Semantic Versioning](https://semver.org/):

- **MAJOR** (x.0.0): Breaking changes or major redesigns
- **MINOR** (1.x.0): New features, color adjustments
- **PATCH** (1.0.x): Bug fixes, typos, small tweaks

Example workflow:
```bash
# Bug fix
npm version patch
git push --follow-tags

# New color for a language
npm version minor
git push --follow-tags

# Complete redesign
npm version major
git push --follow-tags
```

## Troubleshooting

### Error: "Publisher not found"
- Verify the `publisher` field in `package.json` matches your Publisher ID
- Check that you've created a publisher at https://marketplace.visualstudio.com/manage

### Error: "Authentication failed"
- Verify your PAT is correct and hasn't expired
- Ensure the PAT has **Marketplace: Acquire** and **Manage** permissions
- Check the `VSCE_PAT` secret is correctly set in GitHub

### Error: "Version already exists"
- You can't republish the same version
- Increment the version in `package.json`
- Use `npm version patch/minor/major` to bump version

### Build fails in GitHub Actions
- Check the Actions tab for detailed logs
- Ensure all dependencies are in `package.json`
- Test locally with `npm ci && npm run build`

### Theme not appearing in VSCode
- Wait 10-15 minutes after publishing
- Clear VSCode extension cache: Reload Window
- Check marketplace URL directly

## Updating the Theme

To release an update:

1. Make your changes to `src/dracula.yml`
2. Test locally:
   ```bash
   npm run build
   code --install-extension bin/*.vsix
   ```
3. Commit your changes:
   ```bash
   git add .
   git commit -m "feat: improve property colors"
   ```
4. Bump version and publish:
   ```bash
   npm version minor
   git push --follow-tags
   ```

## Best Practices

1. **Test before publishing**: Always install the .vsix locally first
2. **Write clear commit messages**: Users will see these in release notes
3. **Update CHANGELOG.md**: Document all changes
4. **Monitor feedback**: Check marketplace reviews and GitHub issues
5. **Keep dependencies updated**: Run `npm audit` regularly

## Marketplace Metrics

After publishing, monitor your theme's performance:
- Visit https://marketplace.visualstudio.com/manage/publishers/YOUR_PUBLISHER
- Track: Installs, Ratings, Q&A

## Security Notes

- ⚠️ **NEVER commit your PAT** to the repository
- 🔒 Store tokens only in GitHub Secrets
- 🔄 Rotate PATs every 90 days for security
- 🔐 Use minimal required permissions

## Additional Resources

- [VSCode Extension API](https://code.visualstudio.com/api)
- [Publishing Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
- [Theme Color Reference](https://code.visualstudio.com/api/references/theme-color)
- [Semantic Versioning](https://semver.org/)

## Support

If you encounter issues:
1. Check the [GitHub Actions logs](https://github.com/YOUR_USERNAME/dracula-enhanced/actions)
2. Review [VSCode Publishing docs](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
3. Open an issue on GitHub

---

Happy theme publishing! 🎨🦇