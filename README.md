# AWS Secrets GitHub Actions Integration

This repository demonstrates how to securely access AWS Secrets Manager and Systems Manager Parameter Store from GitHub Actions workflows using OIDC authentication.

## Workflow Overview

The GitHub Actions workflow (`test.yml`) includes the following features:

- **Triggers**: Runs automatically on pushes to the main branch, or can be triggered manually
- **OIDC Authentication**: Uses AWS OIDC provider for secure, token-based authentication without storing long-lived AWS credentials
- **Secrets Manager Integration**: Retrieves and parses JSON secrets from AWS Secrets Manager
- **Parameter Store Integration**: Accesses multiple SSM parameters for configuration values

## Workflow Steps

1. **Checkout**: Checks out the repository code
2. **AWS Credentials**: Configures AWS credentials using OIDC token-based authentication
3. **SSM Parameters**: Retrieves three MuleSoft-related configuration parameters:
   - `/mulesoft/anypoint-cli/ruleset-validation`
   - `/mulesoft/anypoint-cli/mule-rulesets`
   - `/mulesoft/anypoint-cli/ruleset-validation-command`
4. **Secrets Manager**: Gets a JSON-formatted secret named `example-secret` and extracts username and password
5. **Output**: Displays the retrieved parameters and secrets (for demonstration purposes)

## Prerequisites

To use this workflow, you need:

1. AWS IAM Role configured for GitHub OIDC authentication
2. The following AWS resources:
   - Secret in AWS Secrets Manager named `example-secret`
   - SSM Parameters under the `/mulesoft/anypoint-cli/` path
3. GitHub repository secret:
   - `AWS_ROLE_ARN`: ARN of the IAM role to assume

## Security Notes

- The workflow is configured with minimal permissions (`id-token: write`, `contents: read`)
- Secrets are stored as environment variables using GitHub's secure environment
- The example includes code to output secrets for demonstration purposes only - this should be removed in production

## Usage

To use this workflow in your repository:

1. Configure AWS resources (IAM roles, secrets, parameters) as required
2. Set up the repository secret `AWS_ROLE_ARN`
3. Push code to the main branch or manually trigger the workflow

For more information about AWS OIDC integration with GitHub Actions, refer to the [AWS documentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles_providers_create_oidc_github-actions.html).
