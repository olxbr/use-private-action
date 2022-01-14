[![Security Workflow](https://github.com/olxbr/use-private-action/actions/workflows/security-workflow.yml/badge.svg)](https://github.com/olxbr/use-private-action/actions/workflows/security-workflow.yml)

# use-private-action
This action allows you to use private actions.

## Usage

```yaml
# .github/workflows/my-workflow.yml
jobs:
    my_job:
        ...
        steps:
            - uses: olxbr/use-private-action@v0.0.1
              with:
                  private-action: Private action to execute, ex. hello-world-docker-action
                  private-action-token: ${{ secrets.PERSONAL_ACCESS_TOKEN }}
                  private-action-ref: Version, branch, hash or tag ex. v1

            # Use your private action
            - name: Hello World action step
              id: hello
              #using the action like private repo action
              uses: ./.github/actions/hello-world-docker-action
              with:
                  who-to-greet: 'Olx Brasil'
            - ... other steps
```

**Note:** all fields are required.

## Prerequisites

### Access Token

To access private repositories, you need to create an access token. To create a new access token:
1. Access your Developer Settings on this [page](https://github.com/settings/tokens) 
2. Click on `Generate new token` button
3. Enter your password to confirm your identity
4. Assign a name to this token (i.e. `Github actions private repository`)
5. Select `repo` (this allows this access token to access your repositories)
6. Copy the generated token (once you leave this page the value will not be accessible anymore, so take care of pasting somewhere)

### Secrets

We need to create a Secret, in th repository where you will use this action. To do that:
1. Go to your repository `Settings > Secrets`
2. Click on `Add ay new secret` link
3. Choose a name for this secret (i.e. `PERSONAL_ACCESS_TOKEN`), and add the previously copied value of the token in the `Value` box
