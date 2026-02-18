# Creating GitHub Issues Guide

This guide provides information on creating GitHub issues for the Vittual-Arena project.

## Using Issue Templates

When creating a new issue, GitHub will present you with several templates to choose from:

### 1. Bug Report Template

Use this template when you encounter a bug or unexpected behavior.

**When to use:**
- Something isn't working as expected
- You've found an error or crash
- A feature is behaving incorrectly

**What to include:**
- Clear description of the bug
- Steps to reproduce
- Expected vs actual behavior
- Environment details
- Screenshots (if applicable)

### 2. Feature Request Template

Use this template to suggest new features or enhancements.

**When to use:**
- You have an idea for a new feature
- You want to suggest an improvement
- You need functionality that doesn't exist

**What to include:**
- Feature description
- Problem it solves
- Proposed solution
- Alternative approaches
- Priority level

### 3. Documentation Template

Use this template for documentation-related issues.

**When to use:**
- Documentation is missing
- Documentation is incorrect or outdated
- Documentation is unclear
- You want to improve documentation

**What to include:**
- Documentation location
- Type of issue (missing, incorrect, unclear, etc.)
- Description of the problem
- Suggested improvements

## Creating Issues via Web Interface

1. Go to https://github.com/amaechiu-del/Vittual-Arena/issues
2. Click "New Issue"
3. Select the appropriate template
4. Fill in the required fields
5. Click "Submit new issue"

## Creating Issues via GitHub CLI

You can also create issues using the GitHub CLI (`gh`):

### Install GitHub CLI

```bash
# macOS
brew install gh

# Windows
winget install GitHub.cli

# Linux
sudo apt install gh
```

### Authenticate

```bash
gh auth login
```

### Create a Bug Report

```bash
gh issue create \
  --repo amaechiu-del/Vittual-Arena \
  --title "[Bug]: Brief description" \
  --body "Bug description here" \
  --label "bug"
```

### Create a Feature Request

```bash
gh issue create \
  --repo amaechiu-del/Vittual-Arena \
  --title "[Feature]: Brief description" \
  --body "Feature description here" \
  --label "enhancement"
```

### Create a Documentation Issue

```bash
gh issue create \
  --repo amaechiu-del/Vittual-Arena \
  --title "[Docs]: Brief description" \
  --body "Documentation issue here" \
  --label "documentation"
```

## Creating Issues via GitHub API

You can create issues programmatically using the GitHub REST API:

### Using curl

```bash
# Set your GitHub token as an environment variable first:
# export GITHUB_TOKEN="your_token_here"

curl -X POST \
  -H "Accept: application/vnd.github+json" \
  -H "Authorization: Bearer $GITHUB_TOKEN" \
  https://api.github.com/repos/amaechiu-del/Vittual-Arena/issues \
  -d '{
    "title": "[Bug]: Issue title",
    "body": "Issue description",
    "labels": ["bug"]
  }'
```

### Using Python

```python
import os
import requests

def create_github_issue(title, body, labels):
    # Get token from environment variable
    token = os.environ.get('GITHUB_TOKEN')
    if not token:
        raise ValueError("GITHUB_TOKEN environment variable not set")
    
    url = "https://api.github.com/repos/amaechiu-del/Vittual-Arena/issues"
    headers = {
        "Accept": "application/vnd.github+json",
        "Authorization": f"Bearer {token}"
    }
    data = {
        "title": title,
        "body": body,
        "labels": labels
    }
    response = requests.post(url, headers=headers, json=data)
    return response.json()

# Example usage (set GITHUB_TOKEN environment variable first)
create_github_issue(
    title="[Bug]: Example bug",
    body="This is an example bug report",
    labels=["bug"]
)
```

### Using Node.js (Octokit)

```javascript
const { Octokit } = require("@octokit/rest");

// Get token from environment variable
const token = process.env.GITHUB_TOKEN;
if (!token) {
  throw new Error("GITHUB_TOKEN environment variable not set");
}

const octokit = new Octokit({
  auth: token
});

async function createIssue(title, body, labels) {
  const response = await octokit.rest.issues.create({
    owner: "amaechiu-del",
    repo: "Vittual-Arena",
    title: title,
    body: body,
    labels: labels
  });
  return response.data;
}

// Example usage (set GITHUB_TOKEN environment variable first)
createIssue(
  "[Feature]: Example feature",
  "This is an example feature request",
  ["enhancement"]
);
```

## Issue Labels

The following labels are available:

- `bug` - Something isn't working
- `enhancement` - New feature or request
- `documentation` - Documentation improvements
- `good first issue` - Good for newcomers
- `help wanted` - Extra attention needed
- `question` - Further information requested
- `wontfix` - This will not be worked on
- `duplicate` - This issue already exists

## Best Practices

1. **Search first**: Check if a similar issue already exists
2. **Be specific**: Provide clear, detailed descriptions
3. **One issue per topic**: Don't combine multiple unrelated issues
4. **Use templates**: They help ensure you include all necessary information
5. **Be respectful**: Maintain a professional and courteous tone
6. **Follow up**: Respond to questions and provide updates
7. **Reference related issues**: Use `#issue_number` to link related issues

## Issue Lifecycle

1. **Open**: Issue is created and awaiting review
2. **Triaged**: Issue has been reviewed and labeled
3. **In Progress**: Someone is actively working on the issue
4. **Review**: Changes are under review
5. **Closed**: Issue has been resolved or won't be fixed

## Need Help?

If you need help creating an issue:

- Review the CONTRIBUTING.md guide
- Check existing issues for examples
- Ask in GitHub Discussions
- Reach out to the maintainers

## Additional Resources

- [GitHub Issues Documentation](https://docs.github.com/en/issues)
- [GitHub CLI Documentation](https://cli.github.com/manual/)
- [GitHub REST API](https://docs.github.com/en/rest/issues/issues)
- [Octokit.js](https://github.com/octokit/octokit.js)
