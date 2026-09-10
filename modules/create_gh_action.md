# Create the GitHub Action

Automated Notebook Validation uses GitHub Actions. The workflow will send a job to Jupyter4NFDI, where the repository is built and the notebooks are executed.

**1. Create a Jupyter4NFDI API token**

Open:

[https://hub.nfdi-jupyter.de/hub/token](https://hub.nfdi-jupyter.de/hub/token)

Log in and request a new API token.

Give the token a useful note, for example:

`my-repository GitHub Action`

Copy the token.

**Note**
Treat the API token like a password. Do not add it directly to the workflow file or commit it to the repository.

**2. Add the token to a GitHub environment**

Open your GitHub repository and go to:

Settings  : Environments : New environment

Create an environment called:

`jupyter4nfdi`

Open the environment and add an environment secret.

Use:

**Name**

```text
JUPYTERHUB_API_TOKEN
```

**Value**

Paste the Jupyter4NFDI API token.

The environment name used by the workflow must match the environment you created in GitHub.

**3. Create the workflow**

Open:

Actions : set up a workflow yourself

Replace the example workflow with:

```yaml
name: Runs on Jupyter4NFDI

on:
  workflow_dispatch:
  schedule:
    - cron: "0 7 * * 1"

jobs:
  notebooks:
    runs-on: ubuntu-latest
    environment: jupyter4nfdi
    steps:
      - name: Run notebooks via papermill on Jupyter4NFDI
        uses: NFDI-Jupyter/ghactions/.github/actions/notebooks@main
        with:
          repo: ${{ github.repository }}
          ref: ${{ github.ref_name }}
          # notebook_dirs: '["notebooks", "examples"]'
          token: ${{ secrets.JUPYTERHUB_API_TOKEN }}
```

Save the file in `.github/workflows/`, for example as:

```text
.github/workflows/notebooks.yml
```

Commit the change.

### What does the workflow do?

**`workflow_dispatch`**

```yaml
workflow_dispatch:
```

This allows you to start the workflow manually from the GitHub Actions page.

**`schedule`**

```yaml
schedule:
  - cron: "0 7 * * 1"
```

This schedules a regular validation.

**`environment`**

```yaml
environment: jupyter4nfdi
```

This tells GitHub which environment contains the secret used by the job.

**`uses`**

```yaml
uses: NFDI-Jupyter/ghactions/.github/actions/notebooks@main
```

This runs the notebook-validation action provided by Jupyter4NFDI.

**Repository and branch**

```yaml
repo: ${{ github.repository }}
ref: ${{ github.ref_name }}
```

These values tell the action which repository and Git reference should be tested.

**Token**

```yaml
token: ${{ secrets.JUPYTERHUB_API_TOKEN }}
```

GitHub supplies the secret to the action without storing the token directly in the workflow file.

**Checking only selected folders**

By default the action can check notebooks in the repository.

If you only want to validate selected folders, uncomment `notebook_dirs`:

```yaml
notebook_dirs: '["notebooks", "examples"]'
```

This is useful if the repository contains notebooks that are not intended to be executed automatically.
