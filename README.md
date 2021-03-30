# Explore-MEPS

This repository is intended for researchers who would like to explore the [Medical Expenditure Panel Survey](https://www.meps.ahrq.gov/mepsweb/index.jsp) (MEPS) using Python.

## Why?

Until now access to this MEPS has been limited to researchers who are skilled with SAS or STATA. In the 90s and early
00's these were the programming languages best suited for this type of data. However the academic research community,
particularly surrounding data analysis, data science and machine learning, is much more reliant on languages such as
Python, R and Julia. The core purpose of this repository extracts MEPS data intended for use with SAS and populates
a SQLite3 database with it. Researchers can now use Django into interact with this data. This sidesteps the
dependency on SAS or STATA and allows reseachers who are more comfortable with Python to work with MEPS data.

## About MEPS

MEPS is a set of large-scale surveys of families and individuals, their medical providers, and employers across
the United States. MEPS is the most complete source of data on the cost and use of health care and health insurance
coverage. MEPS collects data on the specific health services that Americans use, how frequently they use them, the
cost of these services, and how they are paid for, as well as data on the cost, scope, and breadth of health insurance
held by and available to U.S. workers.

## Setup

Below is a guide intended for a researcher with minimal knowledge of Python and Django. Following this guide will allow
you to have local access to the data in MEPS. More advanced researchers/developers can likely skip sections of this guide
to integrate everything into their local enviroment.

- Setup Guide
  - [Environment Setup](setup/environment_setup.md)
  - [Code Editors](setup/code_editor.md)
  - [Coding Standards](setup/coding_standards.md)
  - [Building a Local Database](setup/local_db.md)
