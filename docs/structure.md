# Repository structure

In this document we describe which files you need to have in your repository and where we recommend to put them. For easy reference, we have made a template-repo () that you can use as template. Note however that it is difficult to make a guideline that will work in all cases and therefore you might need to adust this guideline to your specific use case.


## Files that you absolutely need

### `README.md`

One thing you absolutely need is a README file. We also recommend you to write this in [markdown](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet) since this is a relatively simple format to learn, it is simple to read in raw format, it renders nicely on github and since it is pure text it also works great with source control. A README file should contain the following information

```markdown
# Suitable title, e.g Supplementary code for the paper: Title of paper

## Abstract
A short paragraph about the paper

## Install
How to install the code or link to docker image

## Reproducing result
Instructions on how to reproduce the results

## Citation
How to cite the code
```

You can also check out <https://readme.so/editor> than contains an interactive editor with pre-made templates for different sections that you can include in you README file.

### `code`
This is the folder containing the actual scripts for running simulations and creating figures and tables. How you organize this folder will depend on the project

### `data`
This is the folder containing the data you are using in your paper. This folder should also contain a `README.md` file with information about what files are expected to be present in this folder. You might be in a situation where you cannot put the data in the repository, either because the data is too large, or the data is not shareable. In this case the README file should contain information about this. You can read more about data at [](data-main)

### `LICENSE`
A LICENSE contains information about what people can do with the code in your repository. Without a license, no one are allowed to do anything to the code. You can read more about licensing [here](docs-license), and hoe to add a license to your repository [here](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/adding-a-license-to-a-repository)



## Files we recommend you to have

### `docs`
The `docs` folder contains files for building the documentation. See [](docs-main) for more info.

### `.github`
The `.github` folder is a special folder that contains GitHub specific files such as workflows and issue templates.

An [issue template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/configuring-issue-templates-for-your-repository) is useful if you want user to submit issues and feedback in a structured manner. For example, you want the user submitting an issue to provide information such as which operating system was used, how was the dependencies installed, what was the expected and actual behavior.

[GitHub workflows](https://docs.github.com/en/actions/using-workflows) are webhooks that will trigger when certain actions occur in your repository. For example you could set up a workflow to run your tests every time someone pushes to your repository. If you want to host documentation, then we recommend to set up a workflow to build and deploy the documentation on every push to the main branch (see [](docs-main) for more info). If you provide a `Dockerfile`, then we recommend to deploy a docker image on every new version of your code (see [](versioning-main) for more info).

The [example-paper](https://github.com/scientificcomputing/example-paper) contains both of these workflows as well as an issue template.


### `.gitignore`
Whenever you work with `git` it is good practice to add a `.gitignore` file containing a list of files you would like to exclude. Check out <https://gitignore.io> if you want to autogenerate a `.gitignore` file based on the tools and programming languages you are using.


### `CITATION.cff`
A citation file is nice to have in your repo so that people easily can see how to cite the repository. You can read more about citation files [here](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-citation-files)


### `Dockerfile`
A [`Dockerfile`](https://docs.docker.com/engine/reference/builder/docker ) is a file containing commands for recreating the environment for running the code. Here you first need to define a base image and then list the commands for installing all the necessary dependencies. If you don't know which base image to use, then [ubuntu](https://hub.docker.com/_/ubuntu) is a good choice. See [](environment-main) for more information about how to specify a reproducible environment.

### `requirements.txt`
In addition to the `Dockerfile` that contains instructions on how to reproduce the environment, it is good practice to provide the list of dependencies in a language specific file. For Python this can be done using a `requirements.txt` file. Other languages have other types of configuration files (`Cargo.toml` in Rust, `Project.toml` for Julia, `CmakeLists.txt` for C/C++ and so on).


## Files you don't need but is nice to have

### `.dockerignore`
A [`.dockerignore`](https://docs.docker.com/engine/reference/builder/#dockerignore-file) is a file containing a list of files that you want Docker to ignore. This is useful if you want to copy everything from the repository into the image but you would like to exclude some files (e.g sensitive data).

### `.pre-commit-config.yaml`
This files contains a set of [pre-commit hooks](https://pre-commit.com) that can run every time you commit to the repository.


## Summary of structure

We recommend that you

```
├── .github
│   ├── ISSUE_TEMPLATE
│   │   └── bug_report.yml
│   └── workflows
│       ├── build_docs.yml
│       └── docker-image.yml
├── .gitignore
├── .dockerignore
├── .pre-commit-config.yaml
├── CITATION.cff
├── Dockerfile
├── LICENSE
├── README.md
├── code
│   ├── postprocess.py
│   ├── pre_processing.py
│   ├── results
│   ├── run_all.py
│   └── run_simulation.py
├── data
│   ├── README.md
├── docs
│   ├── _config.yml
│   ├── _toc.yml
│   ├── abstract.md
│   ├── citation.md
│   ├── demo.ipynb
│   ├── index.md
│   ├── logo.png
│   ├── refs.bib
│   └── reproducing.md
├── requirements-dev.txt
├── requirements-docs.txt
└── requirements.txt
```
