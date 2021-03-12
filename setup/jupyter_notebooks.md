# Developer Environment Jupyter Notebook Setup

This guide will walk you through how to set up your machine to use Jupyter Notebooks. Jupyter Notebook is an
open-source web application that allows you to create and share documents that contain live code, equations,
visualizations and explanatory text. Uses include: data cleaning and transformation, numerical simulation,
statistical modeling, machine learning and much more. These instructions are designed to be executed in order, and
assume you have already walked through the
[Developer Environment Setup Instructions for Linux](https://github.com/rossids/wiki/blob/master/software_development/dev_environment_setup.md#python-virtual-environment).

## Starting a Notebook

The expectation is that all notebooks will be kept in the **analytics** repository. Begin by nativigating to the
analytics virtual environment and creating a new branch. From there you can launch the notebook app.

        ```shell
            an
            git checkout master
            git pull
            git checkout -b {name-of-new-branch}
            jn
        ```

This will launch a jupyter notebook server which will display the analytics repository. Most projects involving
jupyter notebooks will be **research spikes**. A research spike is an experimental area where problems can be explored
without the expectation of fully productized code. Navigate to the research spike folder and create a new folder with
the following format {year}_{month}_{short description of project}. Within that folder create your first notebook by
clicking on the "New" button in the upper right corner of the screen and selecting "Python 3". This will open a new
window where your analysis can begin.

## Notebook Format

The goal of notebooks is to allow for free form data exporation and rapid experimentation so the structure is much
looser than fully productized code. Often research spikes will answer a self contained question and lead to new ones,
or code in these notebooks will eventually become implemented in the product repository. Therefore a general structure
is followed. Build a header using markdown in the first cell of your notebook by selecting it and pressing ESC. This
will convert the cell from interpreting python to interpreting markdown. Header cells should be formatted as follows:

        ```markdown
        # Notebook Intentions

        {Text describe the question this notebook seeks to answer, or the expiriments this notebook is going to do}

        ## Structure

        {Text describing the layout of the notebook}

        ## Conclusions

        {Text describing the conclusions reached by this notebook}
        ```

Another person should be able to open this notebook and gather of the significant details from this header alone. The
only other strict rule is that the second cell should include all imports.

## Django and Jupyter

Often we will want to import data from our django models for analysis. In order to do this we need to set up a few
things in our notebook. All of this can be done in the imports cell. If you want to pull data from our models place
the following code in you imports:

    ```python
    # allows imports from the product repor
    import sys
    sys.path.append('/home/mike/code/product/')

    # points to the project setting file
    import os
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "nba_project.settings")
    os.environ["DJANGO_ALLOW_ASYNC_UNSAFE"] = "true"

    import django
    django.setup();
    ```

Now that we have that we can import classes and methods from the product repo, but more importantly we can import
Models from our database as simply as:

    ```python
    from nba.models import Game
    ```
