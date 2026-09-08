# What is Automated Notebook Validation?

Automated Notebook Validation (ANV) is a tool which with one click checks if the code in Jupyter Notebooks runs correctly on Juptyter4NFDI. You don't need to manually log in, upload the Notebooks and then run the code cells. ANV does it all for you in predfeinded steps. All you need to do is to complete some configuration steps (which this training material will guide you through). It is possible to set up the ANV to run on regular basis witout you having to trigger it manually.

At the moment ANV is possible for Jupyter Notebooks sitting within the repositories in GitHub as Automated Notebook Validation uses GitHub Actions. 

## Learning objectives

After completing this course, you should be able to:

- prepare a repository for automated notebook validation;
- create a GitHub Action that runs notebooks on Jupyter4NFDI;
- run the workflow manually and on a schedule;
- read the validation logs;
- add a Jupyter4NFDI badge to a repository.


### Why use Automated Notebook Validation?

Even if the code in the Notebooks hasn't changed, it may still break. It is due to, for example:

- dependency changes;
- a dependency is not pinned and a new incompatible version is installed;
- service changes;
- a notebook expects a file that is no longer present;
- a kernel or package is missing from the environment.


The workflow does not reuse your local environment. Instead, Jupyter4NFDI creates the repository environment using Repo2Docker. The notebooks are then executed with Papermill.
