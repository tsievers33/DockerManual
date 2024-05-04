# Local Testing of GitHub Actions with `act`

Testing GitHub Actions locally before pushing changes can save time and reduce unnecessary commits.
`act` is a tool that allows you to run GitHub Actions on your local machine.
Below is a simple guide on how to set up and use `act` for testing your GitHub Actions pipelines locally.

## Step 1: Installation

`act` can be installed on your Ubuntu WSL instance:

- **Install [brew](https://brew.sh/) in WSL**:
  ```bash
  /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
  - ```

- **Install [Act]('https://nektosact.com/') using brew**:
    ```bash
        brew install act
    ```

## Step 2: Secret management

If your project does not contain a `.env` or any other secret file, create one.
Act will be using this secret file to grab the required secrets for your workflows.

fill in the secrets required for your pipeline and tell act to use that secret file for workflows:
```.env
GITHUB_TOKEN='' # Github classic PAT

# Add any other workflow secrets
# EXAMPLE docker registry login:
REGISTRY=''
REG_USERNAME=''
REG_PASSWORD=''
REG_TAG=''
```


You're also able to pass secrets to Act via the commandline with:
```bash
act -s MY_SECRET=value # This is a security risk
```
## Step 3: Run your workflow locally
```bash
act -P ubuntu-latest=nektos/act-environments-ubuntu:20.04 push --secret-file .secrets
```

This command will simulute a ```git push``` event on your branch.
It will spin up the same Docker containers that your workflows would when running on GitHub.


