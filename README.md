# Autompg panel dashboard on Saturn Cloud

![](https://app.community.saturnenterprise.io/favicon.svg)[Click to Deploy Dashboard in Saturn Cloud](https://app.community.saturnenterprise.io/dash/resources?recipeUrl=https://raw.githubusercontent.com/albertdefusco/autompg-deployment/main/.saturn/deployment.json)

![](https://app.community.saturnenterprise.io/favicon.svg)[Click to Launch in Jupyter on Saturn Cloud](https://app.community.saturnenterprise.io/dash/resources?recipeUrl=https://raw.githubusercontent.com/albertdefusco/autompg-deployment/main/.saturn/jupyter.json)

This project demonstrates how to use [Anaconda Project](https://anaconda-project.readthedocs.io/) and
[Saturn Cloud Resource Recipes](https://saturncloud.io/docs/using-saturn-cloud/recipes/) to deploy a
[Panel](https://panel.holoviz.org/) dashboard.

## Details

The `anaconda-project.yml` file in this repository defines the reproducible elements of this project
* The required dependencies to develop and execute the project
* Runtime environment variables
* Runable commands for development and deployment

You will see in the `.saturn/` directory two Saturn Cloud recipe files that Saturn Cloud will install `anaconda-project`
on startup. When `anaconda-project run <command-name>` is executed during the Saturn Cloud deployment
initialization all dependencies defined in the `anaconda-project.yml` will be automatically installed.

This means that the Saturn Cloud recipes here can be used for any project using anaconda-project. The only items that
would need to be changed are `working_directory`, `git_repositories.url`, and `git_repositories.path` to the correct
values for your own repo.

### Dependencies

The dependencies are specified in two files `anaconda-project.yml` records the top-level requirements determined
by the developer and any essential version constraints.

```yaml
packages:
  - python=3.8
  - notebook
  - pandas
  - lxml
  - panel
  - hvplot
```

The `anaconda-project-lock.yml` contains fully solved versions of all transitive dependencies of the above packages
for the requested platforms, in this case osx-64, osx-arm64, win-64, and linux-64.

### Commands

This project defines two commands. Commands are executed by running `anaconda project run <command-name>`. This will
1) install a local Conda environment from the locked dependencies for the current platform 2) set any defined `variables`
and 3) execute the command script.

* `notebook`: To launch Jupyter Notebook with the project directory as the working directory
* `default`: The default command to serve the Panel dashboard
