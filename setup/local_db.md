# Building a Local Database

Building a local database is relatively simple. By utilizing Django's management commands we can generate
a local database all from the terminal.

---

## Shortcuts

- [Building a Local Database](#building-a-local-database)
  - [Shortcuts](#shortcuts)
  - [Requirements](#requirements)
  - [Data Scrapping](#data-scrapping)
  - [Initialize Database](#initialize-database)
  - [Populate Database](#populate-database)
  - [Optional Set Up Administration App](#optional-set-up-administration-app)
  
---

## Requirements

Part of this process requires selenium, a python package that allows
automated browser processes to take place. Currently our methodology requires a chrome browser installed on
the local machine. If you do not have chrome installed run the follow command in your base directory.

    ```shell
        # terminal
        wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
        sudo apt install ./google-chrome-stable_current_amd64.deb
    ```

We also require a chromedriver. Follow instructions on [chromedriver download link](https://chromedriver.chromium.org/downloads)
to identify the driver suited for the local machine. Once downloaded place the chromedriver
in the ~./meps/mep_dev directory. Now we can begin.

## Data Scrapping

First open the terminal and swap to the meps_dev alias.

    ```shell
        # terminal
        meps_dev
    ```

Next we will call the `scrap_meps` command to download meps files to your local machine. By default this
command will pull meps file from 2005-2018 (2018 is the most recent available data as of 2021-03). In
all the resulting database will be ~9GB, however you can decrease that by specifiying which years you would like
and or which data types you would like. The `scrap_meps` command should be run in the terminal as follows.

    Example: All years, all data types
    ```shell
        # terminal
        python manage.py scrap_meps
    ```

    Example: Specific years, all data types
    ```shell
        # terminal
        python manage.py scrap_meps --years 2012 2013 2014
    ```

    Example: All years, specific data types
    ```shell
        # terminal
        python manage.py scrap_meps --model "PrescribedMedicines" "EmergencyRoomVisits"
    ```

    Example: Specific years, specific data types
    ```shell
        # terminal
        python manage.py scrap_meps --years 2012 2013 2014 --model "PrescribedMedicines" "EmergencyRoomVisits"
    ```

This command will open up chrome, and download zipped data files and associated data dictionaries to your meps_data
folder. If you have a slow internet download speed and the webdriver navigates to new pages before files have
completed downloading you can add the following argument to enforce a fixed waiting time, in seconds.

    ```shell
        # terminal
        python manage.py scrap_meps --sleep 30
    ```

## Initialize Database

Next we need to set the parameters of the database. This can be done with the following command.

    ```shell
        # terminal
        python manage.py migrate
    ```

This will generate an empty SQLite3 database for all years 2005-2018 for all data types.

## Populate Database

Populate the database with the following command. This command will unpack the zipped data files, process the
contents and populate the database with the data. When doing all years and all data types these can take
several hours. Years and data types can be specified decrease this processing time. Ensure that these
arguments are consistent with the ones use with the "scrap_meps" command.

    Example: All years, all data types
    ```shell
        # terminal
        python manage.py populate_models
    ```

    Example: Specific years, all data types
    ```shell
        # terminal
        python manage.py populate_models --years 2012 2013 2014
    ```

    Example: All years, specific data types
    ```shell
        # terminal
        python manage.py populate_models --model "PrescribedMedicines" "EmergencyRoomVisits"
    ```

    Example: Specific years, specific data types
    ```shell
        # terminal
        python manage.py populate_models --years 2012 2013 2014 --model "PrescribedMedicines" "EmergencyRoomVisits"
    ```

## Optional Set Up Administration App

If you are interested you can set yourself up as an adminstrator to your local database and interact with it, through
the django admin application. This can be useful to better understand the layout of the database or to explore
specific entries without writing any code. To do this run the following:

    ```shell
        # terminal
        python manage.py createsuperuser
        # follow the prompts to create a login username and password
        # the email address is not shared with anyone, you can enter
        # a dummy email if you wish
        python manage.py runserver
    ```

This will spool up a local instance of the database. After the runserver command there should be an output that looks
like this:

    ```
        Django version 3.0.7, using settings 'meps_db.settings'
        Starting development server at http://127.0.0.1:8000/
        Quit the server with CONTROL-C.
    ```

The address "http://127.0.0.1:8000/" may differ on your machine. Copy your address, open a browser and paste the address.
This will take you to the frontend of the django app, which we currently do not support. To access the administration
part of the app add /admin/ to your address, ex: "http://127.0.0.1:8000/admin/". From here you can use your credentials
from the createsuperuser command to login in. Now you can navigate around the database.
