# Set up the spaceflights project

In this section, we discuss the project set-up phase, which is the first part of the [standard development workflow](./spaceflights_tutorial.md#kedro-project-development-workflow). The set-up steps are as follows:


* Create a new project
* Install dependencies
* Configure the project


## Create a new project

Navigate to your chosen working directory and run the following to [create a new empty Kedro project](../get_started/new_project.md#create-a-new-project-interactively) using the default interactive prompts:

```bash
kedro new
```

When prompted for a project name, enter `Kedro Tutorial`. Subsequently, accept the default suggestions for `repo_name` and `python_package` by pressing enter.

## Install project dependencies

To install the project-specific dependencies, navigate to the root directory of the project and run:

```bash
pip install -r src/requirements.txt
```

### More about project dependencies

Up to this point, we haven't discussed project dependencies, so now is a good time to examine them. We use Kedro to specify a project's dependencies and make it easier for others to run your project. It avoids version conflicts because Kedro ensures that you use same Python packages and versions.

The generic project template bundles some typical dependencies, in `src/requirements.txt`. Here's a typical example, although you may find that the version numbers are slightly different depending on the version of Kedro that you are using:

```text
black==21.5b1 # Used for formatting code with `kedro lint`
flake8>=3.7.9, <4.0 # Used for linting code with `kedro lint`
ipython==7.0 # Used for an IPython session with `kedro ipython`
isort~=5.0 # Used for linting code with `kedro lint`
jupyter~=1.0 # Used to open a Kedro-session in Jupyter Notebook & Lab
jupyter_client>=5.1.0, <7.0 # Used to open a Kedro-session in Jupyter Notebook & Lab
jupyterlab~=3.0 # Used to open a Kedro-session in Jupyter Lab
kedro==0.17.6
nbstripout~=0.4 # Strips the output of a Jupyter Notebook and writes the outputless version to the original file
pytest-cov~=3.0 # Produces test coverage reports
pytest-mock>=1.7.1, <2.0 # Wrapper around the mock package for easier use with pytest
pytest~=6.2 # Testing framework for Python code
wheel>=0.35, <0.37 # The reference implementation of the Python wheel packaging standard
```

```eval_rst
.. note::  If your project has ``conda`` dependencies, you can create a ``src/environment.yml`` file and list them there.
```


### Add and remove project-specific dependencies

The dependencies above may be sufficient for some projects, but for the spaceflights project, you need to add a requirement for the `pandas` project because you are working with CSV and Excel files. You can add the necessary dependencies for these files types as follows:

```bash
pip install "kedro[pandas.CSVDataSet,pandas.ExcelDataSet]"
```

Alternatively, if you need to, you can edit `src/requirements.txt` directly to modify your list of dependencies by replacing the requirement `kedro==0.17.6` with the following (your version of Kedro may be different):

```text
kedro[pandas.CSVDataSet,pandas.ExcelDataSet]==0.17.6
```

Then run the following:

```bash
kedro build-reqs
```

You can find out more about [how to work with project dependencies](../kedro_project_setup/dependencies.md) in the Kedro project documentation. In a [later step of this tutorial](./create_pipelines.md#update-dependencies), we will modify project's dependencies to illustrate how, once you have installed project-specific dependencies, you can update them.


## Configure the project

You may optionally add in any credentials to `conf/local/credentials.yml` that you would need to load specific data sources like usernames and passwords. Some examples are given within the file to illustrate how you store credentials. Additional information can be found in the [advanced documentation on configuration](../kedro_project_setup/configuration.md).

At this stage of the workflow, you may also want to [set up logging](../logging/logging.md), but we do not use it in this tutorial.