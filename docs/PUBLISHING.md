# Publishing Guide

This guide explains how to build and publish the Makinda Dark theme to the VS Code Marketplace.

## Prerequisites

### 1. Install vsce (VS Code Extension Manager)

```bash
npm install -g @vscode/vsce
```

### 2. Create a Publisher Account

1. Go to [Visual Studio Marketplace](https://marketplace.visualstudio.com/manage)
2. Sign in with your Microsoft account
3. Create a publisher if you don't have one
   - Publisher ID: `makindajack`
   - Display Name: `Jackson Makinda`

### 3. Generate Personal Access Token (PAT)

1. Go to [Azure DevOps](https://dev.azure.com/)
2. Sign in with the same Microsoft account
3. Click your profile icon → **Personal Access Tokens**
4. Click **+ New Token**
5. Configure:
   - **Name**: `vsce-publish` (or any name)
   - **Organization**: `All accessible organizations`
   - **Expiration**: Set as needed (max 1 year)
   - **Scopes**: Select **Custom defined**, then:
     - **Marketplace** → Check **Manage**
6. Click **Create** and copy the token immediately (you won't see it again)

## Building the Extension

### Package the Extension

```bash
# Navigate to project directory
cd /path/to/makinda-dark

# Create the .vsix package
vsce package

# This creates: makinda-dark-1.0.0.vsix
```

### Verify the Package

```bash
# List package contents
vsce ls

# Test install locally
code --install-extension makinda-dark-1.0.0.vsix
```

## Publishing

### Method 1: Command Line (Recommended)

```bash
# Login with your PAT
vsce login makindajack
# Paste your Personal Access Token when prompted

# Publish
vsce publish

# Or publish with version bump
vsce publish minor  # 1.0.0 → 1.1.0
vsce publish patch  # 1.0.0 → 1.0.1
vsce publish major  # 1.0.0 → 2.0.0
```

### Method 2: Using PAT Directly

```bash
vsce publish -p YOUR_PERSONAL_ACCESS_TOKEN
```

### Method 3: Manual Upload

1. Build the `.vsix` file: `vsce package`
2. Go to [VS Marketplace Management](https://marketplace.visualstudio.com/manage)
3. Click your publisher
4. Click **+ New Extension** → **VS Code**
5. Upload the `.vsix` file

## Pre-Publish Checklist

Before publishing, verify:

- [ ] **package.json**
  - [ ] Version number is updated
  - [ ] Description is clear and accurate
  - [ ] Keywords are relevant
  - [ ] Icon exists at specified path
  - [ ] Repository URL is correct
  - [ ] License is specified

- [ ] **README.md**
  - [ ] Features are documented
  - [ ] Screenshots are included
  - [ ] Installation instructions are clear
  - [ ] Links work correctly

- [ ] **CHANGELOG.md**
  - [ ] New version is documented
  - [ ] Changes are listed

- [ ] **Theme Files**
  - [ ] JSON is valid (no syntax errors)
  - [ ] Theme loads without errors
  - [ ] Colors are tested

- [ ] **Assets**
  - [ ] Icon is 128x128 PNG
  - [ ] Screenshots are high quality
  - [ ] Images are optimized

## Version Management

### Semantic Versioning

Follow [SemVer](https://semver.org/):

- **MAJOR (X.0.0)**: Breaking changes
- **MINOR (0.X.0)**: New features, backward compatible
- **PATCH (0.0.X)**: Bug fixes, minor adjustments

### Updating Version

```bash
# Edit package.json manually, or:

# Automatic version bump
npm version patch  # 1.0.0 → 1.0.1
npm version minor  # 1.0.0 → 1.1.0
npm version major  # 1.0.0 → 2.0.0
```

## Post-Publish

### Verify Publication

1. Visit your extension page:
   ```
   https://marketplace.visualstudio.com/items?itemName=makindajack.makinda-dark
   ```
2. Verify:
   - Version is correct
   - README displays properly
   - Images load correctly
   - Extension installs successfully

### Announce the Release

1. Create a GitHub Release
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```
2. Upload the `.vsix` file to the release
3. Share on social media if desired

## Unpublishing

If needed, you can unpublish:

```bash
# Unpublish specific version
vsce unpublish makindajack.makinda-dark version

# Unpublish entire extension (use with caution!)
vsce unpublish makindajack.makinda-dark
```

## Troubleshooting

### "Invalid Publisher"

- Verify publisher name in package.json matches your Marketplace publisher ID
- Check case sensitivity

### "Token Expired"

- Generate a new PAT in Azure DevOps
- Run `vsce login makindajack` again

### "Missing Repository"

- Ensure `repository` field in package.json is complete

### "Icon Not Found"

- Verify icon path is relative to package.json
- Check file exists and is a valid PNG

### "README Not Displaying"

- Check markdown syntax
- Ensure image URLs are absolute or hosted publicly
- Verify no broken links

## Continuous Integration (Optional)

For automated publishing with GitHub Actions:

```yaml
# .github/workflows/publish.yml
name: Publish Extension

on:
  release:
    types: [created]

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: 18
      - run: npm install -g @vscode/vsce
      - run: vsce publish -p ${{ secrets.VSCE_PAT }}
```

Store your PAT as a GitHub Secret named `VSCE_PAT`.

## Resources

- [Publishing Extensions](https://code.visualstudio.com/api/working-with-extensions/publishing-extension)
- [Marketplace Publisher Management](https://marketplace.visualstudio.com/manage)
- [vsce Documentation](https://github.com/microsoft/vscode-vsce)
- [Azure DevOps PAT](https://docs.microsoft.com/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate)
