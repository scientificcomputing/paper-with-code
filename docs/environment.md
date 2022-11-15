(environment-main)=
# Reproducible environments

Being able to create a reproducible environment is probably one of the biggest challenges when it comes to reproducibility.

When reproducing the results of a research paper you would like to use the same environment as was used when writing the paper. This can be achieved by publishing a Docker image.

We recommend that you publish a docker image every time you create a new version of your code (see [](versioning-main) for more info about how to create a version).

You can read more about how to publish a docker image [here](https://scientificcomputing.github.io/reproducibility/part4/docker.html) and you can see an example `Dockerfile` in the [example-paper repo](https://github.com/scientificcomputing/example-paper/blob/main/Dockerfile)
