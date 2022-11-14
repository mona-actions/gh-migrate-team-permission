# Migrate Team Permission

**GitHub CLI** extensions are repositories that provide additional `gh` commands, and this **GitHub CLI** extension can help to migrate GitHub Team repository permissions from one organization to another organization.

## GHES Compatibility
The **gh-migrate-team-permission** extension supports the following versions of GitHub Enterpise Server (GHES):

- Supported: >= 2.20
- Not Supported: <= v2.19

*It should be noted that support for versions < 3.1 is limited.*

## Prerequisites

- Operating system that can run shell scripts (*bash/sh*)
- **GitHub CLI** installed by following this documentation: <https://github.com/cli/cli#installation>
- **jq** command-line JSON parser: <https://stedolan.github.io/jq/>
- Your destination organization have all Team names identical to teams in source organization
- Your destination organization have all repository names identical to repositories in source organization
- You have ownership/admin permissions in the destination GitHub GHES/GHEC where you want to migrate to
- You have ownership/admin permission in the source GitHub GHEC/EMU where you can migrate from
- You need to create a GitHub **Personal Access Token** with all `repo` permission `admin:org` permission in your source URL and authenticate for the source organization if the org is behind SAML/SSO
- You need to create a GitHub **Personal Access Token** with all `repo` permission `admin:org` permission in your destination URL and authenticate for the destionation organization if the org is behind SAML/SSO

You need to either export these environment variables.

| Environment Variable name | Value                                                                                       |
| ------------------------- | ------------------------------------------------------------------------------------------- |
| SOURCE_URL | GitHub URL or GHES URL where you want to migrate. Defaults to `https://github.com` |
| DEST_URL | GitHub URL or GHES URL where you want to migrate. Defaults to `https://github.com` |
| GH_TOKEN_SOURCE | GitHub Personal Access Token (PAT) for your source organization with all `repo` permission `admin:org` permission  |
| GH_TOKEN_DEST | GitHub Personal Access Token (PAT) for your destination organization with all `repo` permission `admin:org` permission  |
| SOURCE_ORG | Source organization name where you want to migrate from  |
| DEST_ORG | Destination organization name where you want to migrate to  |

Or the script will prompt you to put in the relevant information.

## CLI options

```text
Usage: gh-migrate-team-permission [options]
Options:
    -h, --help                    : Show script help
    -su, --source-url             : Set source GitHub URL (e.g. https://github.example.com) Looks for SOURCE_URL environment
                                    variable if omitted or defaults to https://github.com
    -du, --destination-url        : Set destination GitHub URL (e.g. https://github.example.com) Looks for DEST_URL environment
                                    variable if omitted or defaults to https://github.com                                 
    -st, --source-token           : Set Personal Access Token for source organization with repo scope - Looks for GH_TOKEN_SOURCE environment
                                    variable if omitted
    -dt, --destination-token      : Set Personal Access Token for destination organization with repo scope - Looks for GH_TOKEN_DEST environment
                                    variable if omitted
    -so, --source-org             : Set source organization to migrate from - Looks for SOURCE_ORG environment
                                    variable if omitted
    -do, --destination-org        : Set destination organization to migrate to - Looks for DEST_ORG environment
                                    variable if omitted
Description:
gh-migrate-team-permission migrates the team repository permissions from one organzation to another organization, assuming that the Teams and repositories are properly mapped
Example:
  gh migrate-team-permission -su https://ghes-url.com -st ABCDEFG1234567 -so source-org -do final-destination-org -dt ABCDEFG1234567
```
## How to run

Make sure you followed prerequisites and then follow these instructions.

### Step 1: Install GitHub extension

```sh
gh extension install mona-actions/gh-migrate-team-permission
```

### Step 2: Run gh migrate-team-permission

```sh
  gh migrate-team-permission -su https://ghes-url.com -st ABCDEFG1234567 -so source-org -do final-destination-org -dt ABCDEFG1234567
```