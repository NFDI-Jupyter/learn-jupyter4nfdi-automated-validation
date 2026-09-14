# Run the validation and read the results

Once the workflow has been committed, run it manually before relying on the schedule.

Open the repository on GitHub and select:

**Actions → Runs on Jupyter4NFDI → Run workflow**

A new workflow run should appear. It can take a few minutes. Open the run and then open the `notebooks` job.
What happens behind the scenes? The GitHub Action sends the repository information to Jupyter4NFDI.

The output may contain a job URL and status updates such as:

```text
Job URL: https://hub.nfdi-jupyter.de/hub/api/job/...
Job status: running
Job status: stopped
```

After the job has finished, the workflow prints the Papermill results.

A successful run may look like:

```text
========== PAPERMILL LOGS ==========
{
  "exitCode": 0,
  "results": [
    {
      "notebook": "/home/jovyan/notebooks/notebook.ipynb",
      "exitCode": 0,
      "stdout": "..."
    }
  ]
}
===================================
Papermill job completed successfully
```



### Analysing the results

* An exit code of `0` means that the job completed successfully. The job means: building the image and running the code in all notebooks.

```json
"exitCode": 0
```

* A non-zero exit code means that something failed.


Apart for the exit code for the job, each notebook also has its own exit code:

```json
{
  "notebook": "/home/jovyan/notebooks/notebook.ipynb",
  "exitCode": 0
}
```

If a repository contains several notebooks, use this part of the output to identify which notebook failed.

The `stdout` field contains output from Papermill.

For example:

```text
Executing notebook with kernel: python3
Executing: 100%|██████████| ...
```

The kernel name can be useful when debugging a failure.


