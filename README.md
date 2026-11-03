# Terraform and DevSecOps Learning

A beginner practice project for learning Terraform and secure infrastructure development.
Terraform describes infrastructure in text files. DevSecOps means including security checks
throughout development, rather than waiting until the end.

## Current status

This repository is a starting point, not a working AWS deployment:

- `main.tf` contains the placeholder text `new line`, which is not valid Terraform configuration.
- `provider.tf` is empty; no provider or AWS region is configured.
- `variables.tf` is empty; no input variables are defined.
- No infrastructure resources are defined in the current files.

## Files in this project

| File | Purpose |
| --- | --- |
| `main.tf` | Usually holds the infrastructure resources you want Terraform to manage. |
| `provider.tf` | Usually configures providers, such as the provider used to communicate with AWS. |
| `variables.tf` | Usually declares inputs so configuration can be reused with different values. |
| `learning-notes.md` | Your notes about Terraform, Git, and GitHub. |
| `.gitignore` | Tells Git which local files to leave out of future commits. |

Terraform reads all `.tf` files in a directory together. These filenames help people organize
the project; they do not control the order Terraform runs things.

## Safe learning workflow

1. Learn the basic configuration structure and replace the placeholder when you are ready.
2. Choose a Terraform version and provider version before adding working configuration.
3. Keep AWS credentials out of source files and Git. Use a local AWS profile or temporary credentials.
4. Once the configuration is ready, check formatting and validate it. Initialization may
   download providers and access a configured backend; review that configuration first.
5. Review a plan before deciding whether to create resources. A plan may contact AWS and
   may contain private information. Applying changes can create billable resources.

No Terraform commands or AWS deployment were run while preparing this documentation.

## What belongs in Git?

Commit your `.tf` source files, documentation, and `.terraform.lock.hcl` when it is generated.
The lock file records selected provider versions and checksums so future installations
can use the same provider selections.

Keep these local:

- `.terraform/`: downloaded providers, modules, and local backend information.
- State files: Terraform's record of managed resources; they can contain secrets.
- Variable value files (`*.tfvars` and `*.tfvars.json`): local settings that may contain secrets.
  Sanitized example files such as `terraform.tfvars.example` can be committed.
- Saved plans, crash logs, credentials, private keys, and local environment files.

Save any future plan files with a `.tfplan` extension or the name `tfplan` so the ignore
rules cover them. Other plan filenames need their own ignore rule.

`.gitignore` is a convenience, not a security check. It does not remove files already tracked
by Git or erase secrets from commit history. Review changes before committing; if a real
credential is exposed, revoke or rotate it.
