# GitHub Setup Guide

This guide will help you publish this Gitbook documentation to GitHub and integrate it with Gitbook.

## Prerequisites

- A GitHub account
- Git installed on your computer
- A Gitbook account (optional, for automatic publishing)

## Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and log in
2. Click the "+" icon in the top right and select "New repository"
3. Enter repository details:
   - Repository name: `admize-openrtb-docs` (or your preferred name)
   - Description: "Admize OpenRTB Integration Documentation"
   - Choose Public or Private
   - Do NOT initialize with README (we already have one)
4. Click "Create repository"

## Step 2: Push to GitHub

Open your terminal and navigate to the documentation folder, then run:

```bash
cd /path/to/admize-openrtb-docs

# Initialize git repository
git init

# Add all files
git add .

# Commit files
git commit -m "Initial commit: Admize OpenRTB documentation"

# Add remote repository (replace with your repository URL)
git remote add origin https://github.com/YOUR_USERNAME/admize-openrtb-docs.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 3: Connect to Gitbook (Optional)

If you want to use Gitbook's hosting and features:

1. Go to [Gitbook.com](https://www.gitbook.com) and sign in
2. Click "New Space"
3. Select "Import from GitHub"
4. Authorize Gitbook to access your GitHub account
5. Select your `admize-openrtb-docs` repository
6. Choose the branch (usually `main`)
7. Click "Import"

Gitbook will automatically:
- Build your documentation
- Provide a public URL
- Auto-update when you push changes to GitHub

## Step 4: Configure GitHub Pages (Alternative)

If you prefer GitHub Pages instead of Gitbook:

1. In your GitHub repository, go to "Settings"
2. Scroll down to "Pages" section
3. Under "Source", select the branch (usually `main`)
4. Select the folder: `/ (root)`
5. Click "Save"

Your documentation will be available at:
`https://YOUR_USERNAME.github.io/admize-openrtb-docs/`

Note: GitHub Pages displays markdown files, but may not render as nicely as Gitbook.

## Directory Structure

```
admize-openrtb-docs/
├── README.md                 # Main introduction
├── SUMMARY.md               # Table of contents
├── .gitbook.yaml           # Gitbook configuration
├── .gitignore              # Git ignore rules
├── ssp/                    # SSP integration docs
│   ├── README.md
│   ├── bid-request.md
│   ├── bid-response.md
│   ├── native-spec.md
│   └── examples.md
└── dsp/                    # DSP integration docs
    ├── README.md
    ├── bid-request.md
    ├── bid-response.md
    ├── native-spec.md
    └── examples.md
```

## Updating Documentation

To update the documentation:

```bash
# Make your changes to the markdown files

# Stage changes
git add .

# Commit changes
git commit -m "Update: description of changes"

# Push to GitHub
git push origin main
```

If connected to Gitbook, it will automatically rebuild and deploy the changes.

## Tips

1. **Keep commits small**: Make frequent, focused commits
2. **Write clear commit messages**: Describe what changed and why
3. **Use branches**: For major changes, create a branch and merge via pull request
4. **Review changes**: Before committing, review your changes with `git diff`

## Troubleshooting

### Authentication Issues
If you have trouble pushing to GitHub:
- Use a Personal Access Token instead of password
- Or set up SSH keys

### Gitbook Not Updating
If Gitbook doesn't auto-update:
- Check the GitHub integration settings in Gitbook
- Manually trigger a sync from Gitbook dashboard
- Ensure `.gitbook.yaml` is in the root directory

### Formatting Issues
If markdown doesn't render correctly:
- Validate your markdown syntax
- Check that all links are correct
- Ensure SUMMARY.md structure matches your file structure

## Need Help?

- [Gitbook Documentation](https://docs.gitbook.com)
- [GitHub Docs](https://docs.github.com)
- [Markdown Guide](https://www.markdownguide.org)
