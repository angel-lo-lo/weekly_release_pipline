# Weekly Release Pipeline

Automated weekly release pipeline for open-source projects using GitHub Actions.

## Overview

This repository contains a production-ready GitHub Actions workflow that automates weekly releases with intelligent change detection, auto-generated changelogs, and comprehensive release management.

## Features

- ✅ **Automated Weekly Releases** - Runs every Monday at 9:00 AM UTC
- ✅ **Smart Change Detection** - Skips releases when there are no new commits
- ✅ **Auto-Generated Changelogs** - Categorizes commits by type (features, fixes, docs, etc.)
- ✅ **GitHub Releases** - Creates full releases with notes, not just tags
- ✅ **Manual Triggers** - On-demand releases with configurable options
- ✅ **Variant Support** - Create alpha, beta, or test releases
- ✅ **Semantic Versioning** - Compatible with `v<major>.<minor>.<patch>` scheme

## Quick Start

### 1. Copy to Your Repository

```bash
# Copy the workflow file
cp .github/workflows/weekly-release.yml YOUR_REPO/.github/workflows/

# Optionally copy the usage guide
cp RELEASE_PIPELINE_GUIDE.md YOUR_REPO/docs/
```

### 2. Configure Your Branch

The workflow expects branches named in the format `v<major>.<minor>` (e.g., `v1.2`).

### 3. Test with a Variant Release

1. Go to **Actions** → **Weekly Release** in your GitHub repository
2. Click **Run workflow**
3. Set `variant: test`
4. Click "Run workflow"
5. Verify the test release is created successfully

### 4. Wait for Automated Release

The workflow will automatically run every Monday at 9:00 AM UTC and create a release if there are new commits.

## Documentation

📚 **[Complete Usage Guide](RELEASE_PIPELINE_GUIDE.md)** - Comprehensive documentation covering:
- How the pipeline works
- Manual trigger instructions
- Versioning strategy
- Changelog generation
- Schedule configuration
- Troubleshooting

## Workflow Configuration

### Schedule

Default: **Monday at 9:00 AM UTC**

To change the schedule, edit the cron expression:
```yaml
schedule:
  - cron: '0 9 * * 1'  # Modify this line
```

### Manual Trigger Options

| Option | Description | Default |
|--------|-------------|---------|
| `branch` | Target branch | Current branch |
| `variant` | Release type (alpha/beta/test) | (production) |
| `skip_if_no_changes` | Skip if no commits | `true` |

## Changelog Format

The workflow automatically categorizes commits:

- **✨ Features** - Commits starting with `feat:` or `feature:`
- **🐛 Bug Fixes** - Commits starting with `fix:`
- **📚 Documentation** - Commits starting with `docs:`
- **🔧 Other Changes** - All other commits

### Recommended: Use Conventional Commits

For best results, use conventional commit format:
```bash
feat: add new authentication method
fix: resolve login timeout issue
docs: update API documentation
chore: update dependencies
```

## Example Release

```markdown
## What's Changed

### ✨ Features
- feat: add user authentication (a1b2c3d)
- feat: implement dark mode (e4f5g6h)

### 🐛 Bug Fixes
- fix: resolve memory leak (i7j8k9l)
- fix: correct timezone handling (m0n1o2p)

### 📚 Documentation
- docs: update API reference (q3r4s5t)

---

**Full Changelog**: https://github.com/user/repo/compare/v1.2.5...v1.2.6
```

## Requirements

- GitHub Actions enabled
- `contents: write` permission (already configured in workflow)
- Branch naming: `v<major>.<minor>` format

## Validation

The workflow has been validated with:
- ✅ **actionlint** - GitHub Actions workflow linter
- ✅ **shellcheck** - Shell script static analysis
- ✅ No errors or warnings

## Customization

### Change Detection

To force releases even without changes:
```yaml
skip_if_no_changes:
  default: 'false'  # Change from 'true'
```

### Versioning

The workflow supports:
- **Production**: `v1.2.3`
- **Variants**: `v1.2.3-alpha1`, `v1.2.3-beta2`, `v1.2.3-test1`

## Troubleshooting

### Workflow doesn't run on schedule
- Ensure workflow is on your default branch
- Check repository has recent activity
- Verify GitHub Actions is enabled

### No release created
- Check logs for "No changes detected"
- Verify commits exist since last release
- Ensure branch name matches `v<major>.<minor>`

### Changelog is empty
- Commits may not follow conventional format
- All commits appear in "Other Changes"
- Consider adopting conventional commits

## License

This workflow is provided as-is for use in open-source projects.

## Contributing

Feel free to customize this workflow for your needs. Suggestions and improvements are welcome!

## Related

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Semantic Versioning](https://semver.org/)
