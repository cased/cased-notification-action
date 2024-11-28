# Cased Notification Action

This GitHub Action sends a notification to Cased when a deployment of your
project occurs. Cased will then send further notifications to Slack, SMS, and
email.

## Inputs

- `cased_token`: **Required** The token used for authentication with the Cased API.
- `branch_name`: The name of the branch to deploy. Defaults to 'main'.
- `target`: The target environment for the deployment. Defaults to 'prod'.

The action automatically sends the repository name (*project name* in Cased)
and will automatically send the pull request number if available.

## Environment Variables

No additional environment variables are required. All necessary information is passed through inputs.

## Example Usage

```yaml
name: Notify Cased of Deployment
on:
  pull_request:
    types: [closed]

jobs:
  notify-cased:
    if: github.event.pull_request.merged == true
    runs-on: ubuntu-latest
    steps:
      - name: Send notification to Cased
        uses: cased/cased-notification-action@v1
        with:
          branch_name: ${{ github.event.pull_request.base.ref }}
          target: 'feat/我的新分支'
          cased_token: ${{ secrets.CASED_TOKEN }}
