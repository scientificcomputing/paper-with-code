(environment-main)=
# Reproducible environments

Being able to create a reproducible environment is probably one of the biggest challenges when it comes to reproducibility.

When reproducing the results of a research paper you would like to use the same environment as was used when writing the paper. This can be achieved by publishing a Docker image.

We recommend that you publish a docker image every time you create a new version of your code (see [](versioning-main) for more info about how to create a version).

You can read more about how to publish a docker image [here](https://scientificcomputing.github.io/reproducibility/part4/docker.html) and you can see an example `Dockerfile` in the [example-paper repo](https://github.com/scientificcomputing/example-paper/blob/main/Dockerfile).

Additional resources on reproducible environments can be found at [Simula Tools meetup: Reproducible Environments](https://github.com/ComputationalPhysiology/simula-tools-meetup/tree/master/2022-09-05-reproducible-envs)/

## Language specific dependencies
You should also list the language specific packages you used to generate the results for your paper. In Python these are typically listed in a `requirements.txt` file.

To export the exact dependencies in Python you use the following command
```bash
pip freeze > requirements.txt
```


## conda
Many people use [conda](https://www.anaconda.com/) for their applications.
In this section, we assume that you are familiar with how to set up a conda [environment file](https://conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html#creating-an-environment-from-an-environment-yml-file).
We will use a simple `environment.yml` file, whose environment only needs [DOLFIN](https://bitbucket.org/fenics-project/dolfin)

```yaml
name: test-env
channels:
  - conda-forge
dependencies:
  - fenics-dolfin
```

We create the following `Dockerfile` to install the conda environment
```docker
FROM condaforge/mambaforge

ENV DEBIAN_FRONTEND=noninteractive

# Install ssh (missing dependency to run conda envs)
RUN apt-get update && \
    apt-get install -y ssh build-essential

# Upgrade mamba
RUN mamba upgrade -y mamba

# Copy environment and requirements files into docker env
COPY environment.yml .

# Update environment file with new environment name
RUN mamba env update --file environment.yml --name dockerenv
SHELL ["mamba", "run", "-n", "dockerenv", "/bin/bash", "-c"]
```
