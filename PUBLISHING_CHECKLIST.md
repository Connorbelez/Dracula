# 📋 Publishing Checklist - Dracula Enhanced

Use this checklist before publishing to ensure everything is ready.

## Pre-Publication Checklist

### ✅ Code Quality
- [ ] Theme builds without errors: `npm run build`
- [ ] Package creates successfully: `npm run package`
- [ ] No linting errors: `npm run lint` (if applicable)
- [ ] All JSON files are valid (checked by build)

### ✅ Testing
- [ ] Installed locally and tested: `code --install-extension bin/dracula.vsix`
- [ ] Tested in TypeScript files
- [ ] Tested in JavaScript files
- [ ] Tested in React/JSX/TSX files
- [ ] Tested in Python files
- [ ] Tested in your primary languages
- [ ] Parameters are orange in declarations
- [ ] Parameters are orange in function bodies
- [ ] Properties are purple
- [ ] Variables are default white
- [ ] UI colors look good (sidebar, tabs, etc.)

### ✅ Documentation
- [ ] README.md updated with screenshots
- [ ] CHANGELOG.md has version entry
- [ ] Version number updated in package.json
- [ ] All URLs in package.json are correct
- [ ] Publisher name is correct in package.json

### ✅ Repository
- [ ] All changes committed to git
- [ ] Repository pushed to GitHub
- [ ] Repository is public (or accessible to CI/CD)
- [ ] .gitignore is properly configured
- [ ] No sensitive data in repository

### ✅ Marketplace Setup
- [ ] VSCode Marketplace publisher created
- [ ] Publisher ID matches package.json
- [ ] Personal Access Token (PAT) generated
- [ ] PAT has Marketplace: Acquire and Manage permissions
- [ ] PAT hasn't expired

### ✅ GitHub Setup
- [ ] Repository created on GitHub
- [ ] Secret `VSCE_PAT` added to GitHub repository
- [ ] GitHub Actions are enabled
- [ ] CI workflow passes on main branch

### ✅ Visual Assets
- [ ] icon.png is present and looks good
- [ ] screenshot.png is updated (if applicable)
- [ ] Images are properly sized for marketplace

## Publishing Methods

### Method 1: Automated (Recommended)

```bash
# 1. Ensure you're on main branch
git checkout main
git pull

# 2. Bump version (choose one)
npm version patch  # 1.0.0 → 1.0.1
npm version minor  # 1.0.0 → 1.1.0
npm version major  # 1.0.0 → 2.0.0

# 3. Push with tags
git push --follow-tags

# 4. Watch GitHub Actions
# Go to: https://github.com/YOUR_USERNAME/dracula-enhanced/actions
```

### Method 2: Manual

```bash
# 1. Build
npm run build

# 2. Package
npm run package

# 3. Publish
npx vsce publish -p YOUR_PERSONAL_ACCESS_TOKEN

# Or using npm script
npm run vsce-publish
```

## Post-Publication Checklist

### ✅ Immediate Verification (5-10 minutes after publish)
- [ ] Theme appears in VSCode Marketplace
- [ ] Marketplace URL works: `https://marketplace.visualstudio.com/items?itemName=YOUR_PUBLISHER.dracula-enhanced`
- [ ] Install button works in marketplace
- [ ] Theme installs successfully from VSCode Extensions
- [ ] Version number is correct in marketplace

### ✅ Quality Check
- [ ] Description displays correctly
- [ ] Icon shows properly
- [ ] Keywords are appropriate
- [ ] Categories are correct
- [ ] License is displayed

### ✅ GitHub
- [ ] GitHub Release was created (if using automated workflow)
- [ ] Release notes are accurate
- [ ] .vsix artifact is attached to release
- [ ] Tag is on correct commit

### ✅ Documentation
- [ ] CHANGELOG.md updated with release date
- [ ] README.md reflects current version
- [ ] Any "unreleased" sections moved to version sections

## Version Numbering Guide

Follow Semantic Versioning (SemVer):

### Patch (x.x.X) - Bug fixes
```bash
npm version patch  # 1.0.0 → 1.0.1
```
Examples:
- Fix parameter color in edge case
- Correct property highlighting in specific language
- Fix typo in description

### Minor (x.X.0) - New features
```bash
npm version minor  # 1.0.0 → 1.1.0
```
Examples:
- Add support for new language
- Improve color for specific scope
- Add new UI theme colors

### Major (X.0.0) - Breaking changes
```bash
npm version major  # 1.0.0 → 2.0.0
```
Examples:
- Complete color scheme overhaul
- Remove/change default behaviors
- Incompatible with previous versions

## Troubleshooting

### ❌ "Publisher not found"
- Verify publisher ID in package.json
- Check you created publisher at marketplace.visualstudio.com
- Ensure publisher ID exactly matches (case-sensitive)

### ❌ "Authentication failed"
- Check VSCE_PAT secret is set correctly in GitHub
- Verify PAT hasn't expired
- Ensure PAT has correct permissions
- Try regenerating PAT

### ❌ "Version already exists"
- You can't republish same version
- Bump version: `npm version patch`
- Commit and push again

### ❌ GitHub Action fails
- Check Actions tab for detailed logs
- Verify all secrets are set
- Ensure package.json is valid
- Check build completes locally

### ❌ Theme not appearing in VSCode
- Wait 10-15 minutes (propagation time)
- Clear VSCode cache: Reload Window
- Check directly on marketplace website
- Try searching by exact name

## Quick Commands Reference

```bash
# Development
npm install                    # Install dependencies
npm run build                  # Build theme
npm run package                # Create .vsix
npm run lint                   # Run linter

# Testing
code --install-extension bin/dracula.vsix        # Install locally
code --install-extension bin/dracula.vsix --force # Force reinstall

# Publishing
npm version patch              # Bump patch version
npm version minor              # Bump minor version
npm version major              # Bump major version
git push --follow-tags         # Push with tags (triggers CI/CD)
npm run vsce-publish           # Manual publish

# Git
git status                     # Check changes
git add .                      # Stage all changes
git commit -m "message"        # Commit changes
git push                       # Push to GitHub
git tag v1.0.0                 # Create version tag
git push --tags                # Push tags
```

## Support Resources

- **Marketplace**: https://marketplace.visualstudio.com/manage
- **Azure DevOps**: https://dev.azure.com
- **VSCode Publishing Docs**: https://code.visualstudio.com/api/working-with-extensions/publishing-extension
- **GitHub Actions Logs**: https://github.com/YOUR_USERNAME/dracula-enhanced/actions

## First Release Checklist

Special checklist for v1.0.0:

- [ ] README has compelling description
- [ ] Screenshots showcase key features
- [ ] CHANGELOG documents all features
- [ ] Testing across 5+ languages
- [ ] Documentation is complete
- [ ] GitHub repository looks professional
- [ ] License file is present
- [ ] Contributing guidelines exist
- [ ] Issue templates set up (optional)
- [ ] You're excited to share it! 🎉

---

## 🎯 Ready to Publish?

If all checkboxes are marked:

1. **Take a deep breath** 😌
2. **Run the automated publish**:
   ```bash
   npm version minor
   git push --follow-tags
   ```
3. **Watch it deploy**: Check GitHub Actions
4. **Celebrate** 🎉: You've published a VSCode theme!

Good luck! 🦇✨