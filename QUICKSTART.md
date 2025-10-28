# Quick Start Guide

Get your Admize OpenRTB documentation up and running in minutes!

## What's Included

This documentation package includes:

- ✅ Complete OpenRTB 2.3-2.5 specification for Admize
- ✅ SSP Integration guide (Supply-Side Platforms)
- ✅ DSP Integration guide (Demand-Side Platforms)
- ✅ Native Ads specification (OpenRTB Native 1.2)
- ✅ Real-world request/response examples
- ✅ Ready for GitHub and Gitbook

## File Structure

```
admize-openrtb-docs/
├── README.md              # Main introduction
├── SUMMARY.md            # Table of contents (Gitbook navigation)
├── GITHUB_SETUP.md       # Detailed GitHub setup instructions
├── QUICKSTART.md         # This file
├── .gitbook.yaml         # Gitbook configuration
├── .gitignore           # Git ignore rules
│
├── ssp/                 # SSP Integration Documentation
│   ├── README.md        # SSP overview
│   ├── bid-request.md   # Bid request specification
│   ├── bid-response.md  # Bid response specification
│   ├── native-spec.md   # Native ads specification
│   └── examples.md      # Request/response examples
│
└── dsp/                 # DSP Integration Documentation
    ├── README.md        # DSP overview
    ├── bid-request.md   # Bid request specification
    ├── bid-response.md  # Bid response specification
    ├── native-spec.md   # Native ads specification
    └── examples.md      # Request/response examples
```

## Option 1: Publish to GitHub (Recommended)

### Step 1: Create GitHub Repository

```bash
# Navigate to your documentation folder
cd /path/to/admize-openrtb-docs

# Initialize Git
git init

# Add all files
git add .

# Make first commit
git commit -m "Initial commit: Admize OpenRTB documentation"
```

### Step 2: Push to GitHub

```bash
# Create a new repository on GitHub first, then:
git remote add origin https://github.com/YOUR_USERNAME/admize-openrtb-docs.git
git branch -M main
git push -u origin main
```

### Step 3: Connect to Gitbook (Optional)

1. Sign in to [Gitbook.com](https://www.gitbook.com)
2. Create new space → Import from GitHub
3. Select your repository
4. Your docs will be live at `your-space.gitbook.io`

✨ Done! Your documentation is now live and will auto-update on every push.

## Option 2: Local Preview

### Using Gitbook CLI

```bash
# Install Gitbook CLI
npm install -g gitbook-cli

# Navigate to docs folder
cd admize-openrtb-docs

# Install plugins
gitbook install

# Serve locally
gitbook serve
```

Open `http://localhost:4000` in your browser.

### Using a Markdown Viewer

Simply open the `.md` files in any markdown viewer:
- VS Code (with Markdown Preview)
- Typora
- MacDown (Mac)
- MarkdownPad (Windows)

## Option 3: GitHub Pages

1. Push to GitHub (see Option 1)
2. Go to repository Settings → Pages
3. Select source branch (`main`) and folder (`/ root`)
4. Your docs will be at: `https://YOUR_USERNAME.github.io/admize-openrtb-docs/`

## Customization

### Change the Title
Edit `README.md` and update the main heading.

### Modify Navigation
Edit `SUMMARY.md` to add, remove, or reorder pages.

### Add New Pages
1. Create a new `.md` file
2. Add it to `SUMMARY.md`
3. Commit and push

### Change Theme (Gitbook)
Add to `.gitbook.yaml`:
```yaml
theme:
  primary: "#ff6b6b"
  secondary: "#4ecdc4"
```

## Maintaining the Documentation

### Update Content

```bash
# Edit markdown files
# Then:
git add .
git commit -m "Update: describe your changes"
git push
```

### Add New Sections

1. Create new markdown file(s)
2. Add to `SUMMARY.md`
3. Commit and push

### Review Changes

```bash
# See what changed
git status
git diff

# Review commit history
git log --oneline
```

## Tips for Success

1. **Keep it updated**: Regular updates keep documentation valuable
2. **Use examples**: Real examples are worth 1000 words
3. **Link liberally**: Cross-reference related sections
4. **Version control**: Use branches for major updates
5. **Get feedback**: Share with your team and iterate

## Common Issues

### Can't push to GitHub?
- Check your authentication (use Personal Access Token)
- Verify remote URL: `git remote -v`

### Gitbook not updating?
- Check GitHub integration in Gitbook settings
- Manually trigger sync in Gitbook dashboard

### Formatting looks wrong?
- Validate markdown syntax
- Check relative links in `SUMMARY.md`
- Ensure consistent heading levels

## Next Steps

1. ✅ Push to GitHub
2. ✅ Connect to Gitbook
3. 📚 Share with your team
4. 🔄 Set up automatic updates
5. 📊 Monitor usage and gather feedback

## Resources

- [Gitbook Documentation](https://docs.gitbook.com)
- [GitHub Guides](https://guides.github.com)
- [Markdown Cheatsheet](https://www.markdownguide.org/cheat-sheet/)
- [OpenRTB Specification](https://www.iab.com/guidelines/openrtb/)

## Need Help?

Refer to:
- `GITHUB_SETUP.md` for detailed GitHub instructions
- `README.md` for documentation overview
- Individual section READMEs for specific topics

---

Happy documenting! 🚀
