# Failed Automated Notebook Validation

A failed Automated Notebook Validation shows that the repository cannot  be reproduced. There may be multiple reasons for that. The logs are a good source of finding out what went wrong.


### Missing dependency

A failed run may include:

```text
ModuleNotFoundError: No module named 'matplotlib'
```

This tells you that the notebook imports `matplotlib`, but the environment created from the repository does not provide it.
To fix it, update the repository's environment definition. For a repository using `requirements.txt`, you add:

```text
matplotlib
```

Commit the change and run the validation again. Of course, there may be other solution included in the repository which specifies dependencies. If that is the case, consult the relevant documentation how to add missing dependencies


### Missing Python or R package

Typical output:

```text
ModuleNotFoundError
```

or an R error stating that a package is not installed.

**Check:** Is the dependency included in the repository environment definition?

### Missing file

Typical output:

```text
FileNotFoundError
```

There may be several reasons why this error occurred:

- Is the file committed to the repository?
- Is the path relative to the repository?
- Is the filename case correct?
- Is the notebook assuming a local directory structure?

### Wrong kernel

Papermill may report that the notebook kernel cannot be found or cannot start.

Check if:
- Does the Repo2Docker environment provide that kernel?
- Is a custom kernel required?

### Internet or service dependency

A notebook may depend on:

- a URL;
- an API;
- a database;
- cloud storage;
- a service requiring authentication.

An automated environment may not have the same network access or credentials as your normal environment.
Make sure that any external dependency is can be accessed automatically, without any additional manual steps. If you need to access any data sources and that requires authentication, consider if a sample of the data can be stored in the repository instead.


## Step-by-step debugging


1. Find the notebook with a non-zero exit code.
2. Read the last part of its Papermill output.
3. Identify the first meaningful Python, R, Julia, or shell error.
4. Decide whether the problem is in:
   - the notebook;
   - the repository environment;
   - a file path;
   - an external dependency;
   - the workflow configuration.
5. Fix the repository rather than the temporary validation environment.
6. Commit the change.
7. run the workflow again.

