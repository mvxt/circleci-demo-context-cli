# CircleCI Contexts CLI Demo [![CircleCI](https://circleci.com/gh/mvxt/circleci-demo-context-cli.svg?style=shield&circle-token=5a49c2c32b4bf0e25f4c911dd0477c280b2e72a1)](https://circleci.com/gh/mvxt/circleci-demo-context-cli)

Repository showcasing usage of CircleCI's new context CLI functionality.

## Prerequisites for this example project
- Need to have the following env variables set, either project-level or context-level:

Variable             | Description
---------------------|------------------------------------------------------------------------------
`VCS`                | Either "github" or "bitbucket"
`CIRCLECI_CLI_TOKEN` | A personal API token for CircleCI. User must have org-level/admin permissions

## What's happening in this example config?
1. We use the [CircleCI CLI Orb](https://circleci.com/orbs/registry/orb/circleci/circleci-cli) to install the client-side CLI and setup auth with the `CIRCLECI_CLI_TOKEN` variable.

```yaml
orbs:
  circleci-cli: circleci/circleci-cli@0.1.7

# ...
jobs:
  context-cli-test:
    # ...
    steps:
      - circleci-cli/install
      - circleci-cli/setup
```

2. Then we demonstrate the Context CLI functionality in multiple steps. The commands generally follow this format:

```
circleci context FUNCTION $VCS $CIRCLE_PROJECT_USERNAME [FUNCTION-SPECIFIC_ARGS...]
```

The current functions available include create/delete of context, and create/delete of variables inside the context. `$VCS` you should have set as a prerequisite, and `$CIRCLE_PROJECT_USERNAME` refers to the org name owning the current project.

Run `circleci context` or `circleci context -h` for more help and information on available commands.
