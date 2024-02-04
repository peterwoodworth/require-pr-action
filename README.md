# require-pr-action

> [!WARNING]  
> Using this action can result in destroying hard work. Please be careful when using this action

Are you unable to use branch protection because you're working on a private repository? Is there someone on your team who keeps pushing commits without PRs despite being asked not to? This action is for you! Simply use this action in your repo, and any commits pushed by certain users (or all) will automatically be hard reset to the state before push (`git reset --hard HEAD~1`) if they did not submit a PR. 

## Usage

This action has one input: `users`. Specify the list of github usernames separated by commas, and this action will apply to all of those users when committing. If this prop is not specified, this action will apply to *all* users.

Trigger this action on push events on the branches you want to require PRs for, and be sure to give permissions to read PRs and write to the repository.

## Examples

```yaml
name: "Enforce PR Requirement on main for all users"

on:
  push:
    branches:
      - "main"

jobs:
  revert:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: read
    steps:
      - uses: peterwoodworth/require-pr-action@v1
```

```yaml
name: "Enforce PR Requirement on main for Peter and Sean"

on:
  push:
    branches:
      - "main"

jobs:
  revert:
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: read
    steps:
      - uses: peterwoodworth/require-pr-action@v1
        with:
          users: peter,sean
```