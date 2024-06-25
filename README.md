# global-repository-rules
Global workflows for the organization

# Branch Protection Workflow

This GitHub Actions workflow automates the process of setting up branch protection rules and creating essential elements for newly created repositories in your organization.

## Workflow Overview

The `Branch-protect-workflow` is triggered by two events:
1. A `repository_dispatch` event of type `repo-created`
2. Manual trigger via `workflow_dispatch`

## Features

This workflow performs the following actions on the target repository:

1. **README Creation**: Checks if a README.md file exists. If not, it creates one with a welcome message.
2. **Branch Protection**: Enables branch protection rules on the default branch.
3. **Issue Creation**: Creates an issue in the repository to notify about the automated setup.

## Workflow Steps

### 1. Ensure README.md Exists

- Checks if README.md exists in the target repository
- If not present, creates a basic README.md with a welcome message

### 2. Enable Branch Protection

Applies the following branch protection rules to the default branch:
- Enforces restrictions for administrators
- Requires pull request reviews before merging
- Dismisses stale pull request approvals when new commits are pushed
- Requires review from code owners
- Requires at least one approving review

### 3. Create Notification Issue

Creates an issue in the target repository to notify about the automated setup.

## Usage

### Automatic Trigger

This workflow is designed to be triggered automatically when a new repository is created in your organization. It requires a separate system to listen for repository creation events and dispatch the `repo-created` event to this workflow.

A sample event look like 

{
  "event_type": "repo-created",
  "client_payload": {
    "owner": "siddjos",
    "repo": "notfy6"
  }
}

## Requirements

- A Personal Access Token (PAT) with appropriate permissions stored as a secret named `PAT_GITHUB`
- The workflow must be stored in a central repository in your organization
- Proper webhook setup to trigger the workflow on repository creation (for automatic triggering)

## Customization

You can customize the branch protection rules, README content, and issue notification by modifying the respective sections in the workflow YAML file.

## Troubleshooting

- Ensure that the PAT has the necessary permissions to modify repository settings and create issues
- Check the workflow run logs for any error messages if the workflow fails

## Contributing

Feel free to open issues or submit pull requests to improve this workflow.
