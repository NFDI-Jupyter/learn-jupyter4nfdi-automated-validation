## Configuring repo2docker

Automated Notebook Validation leverages repo2docker to build the image with the environment needed to run the notebooks.
Relevant configuration files have to be in included in the repository.

Depending on the project, this may include files such as:

- `requirements.txt`
- `install.R`


The exact files depend on the software used by the project.


## Checking for common mistakes

Look through the notebooks and check for assumptions such as:

- absolute paths from your own computer;
- files stored outside the repository;
- environment variables that only exist locally;
- a kernel name that is not available in the built environment;
- cells that need to be run in a particular undocumented order.

