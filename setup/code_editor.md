# Code Editors

The codebase is designed around Visual Studio Code (VScode), however it is not a requirement. The following document outlines how to configure VScode

---

## Shortcuts

- [Code Editors](#code-editors)
  - [Shortcuts](#shortcuts)
  - [Installation](#installation)
  - [General Configuration](#general-configuration)
  - [Extensions](#extensions)
  - [Recommended Settings](#recommended-settings)

---

## Installation

Ubuntu based distributions
The easiest way to install Visual Studio Code for Ubuntu based distributions is to download and install the [.deb package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868), either through the graphical software center if it's available, or through the command line with:

    ```shell
        # terminal
        sudo apt install ./<file>.deb
    ```

If you're on an older Linux distribution, you will need to run this instead:
    ```shell
        # terminal
        sudo dpkg -i .deb
        sudo apt-get install -f# Install dependencies

    ```

Note that other binaries are also available on the VS Code download page.
Installing the .deb package will automatically install the apt repository and signing key to enable auto-updating using the system's package manager.

## General Configuration

- Python
  - Linter: pylint, pyflakes, pycodestyle
  - Formatter: black
  - Line Width: 119
    -Markdown
  - Formatter: prettier
- JSON
  - Formatter: prettier

## Extensions

Install the following extensions:

    - Python: python code support
    - Prettier: code formatter
    - Jupyter: Jupyter notebook support
    - Markdown All in One: Markdown advanced support
    - Markdown Lint: Markdown tinting
    - Material Icon Theme: Icons for folder and file types

## Recommended Settings

Add the following to your user settings.json file: [Shift]-[Ctrl]-[P], select "Preferences: Open Settings (JSON)".

    ```javascript
        {
            "breadcrumbs.enabled": true,
            "editor.fontSize": 15,
            "editor.fontFamily": "Courier New",
            "editor.minimap.enabled": true,
            "editor.multiCursorModifier": "ctrlCmd",
            "editor.snippetSuggestions": "top",
            "editor.wordWrap": "off",
            "editor.tabSize": 4,
            "editor.wordWrapColumn": 119,
            "explorer.confirmDelete": false,
            "explorer.confirmDragAndDrop": false,
            "json.format.enable": true,
            "[json]": {
                "editor.rulers": [119],
                "editor.defaultFormatter": "esbenp.prettier-vscode",
                "editor.formatOnSave": false
            },
            "[markdown]": {
                "editor.rulers": [119],
                "editor.defaultFormatter": "esbenp.prettier-vscode",
                "editor.formatOnSave": true
            },
            "markdownlint.run": "onSave",
            "[python]":{
                "editor.rulers": [119],
                "editor.formatOnPaste": false,
                "editor.formatOnSave": false,
            },
            "python.formatting.blackArgs": [
                "--line-length", "119", 
                "--target-version", "py38", 
                "--formatOnSave", "false",
                "--indent-size=4"
            ],
            "python.formatting.provider": "black",
            "python.linting.enabled": true,
            "python.linting.pylintEnabled": true,
            "telemetry.enableCrashReporter": false,
            "telemetry.enableTelemetry": false,
            "window.zoomLevel": 0,
            "workbench.iconTheme": "material-icon-theme",
            "workbench.sideBar.location": "left",
            "workbench.tree.indent": 20,
            "workbench.statusBar.visible": true,
            "files.exclude": {
                "**/.git": true,
                "**/.svn": true,
                "**/.hg": true,
                "**/CVS": true,
                "**/.DS_Store": true,
                "**/.pyc": true,
                "**/__pycache__": true,
                "**.sqlite3": false,
                "**.github": true,
            },
            "python.pythonPath": "/home/mike/.virtualenvs/product/bin/python",
        }
    ```
