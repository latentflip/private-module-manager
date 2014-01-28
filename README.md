## Why?

Sometimes you want to install modules from private github repos, but you don't want to have to setup your own npm registry. In development you can just install with a git url, but that won't work in a deployment environment if you need to setup deploy keys for each private repo.

## What?

This is a module that provides a script that you can run as a postinstall step in the requiring modules' package.json. You can then add a section to your package.json called privateDependencies. When you run npm install, this module will ensure those extra private scripts get cloned and installed. You can provide your own cloning script (as detailed below) where you will want to setup ssh keys etc in your deployment environment, but for development it should just work.

## How?

* Install

    ```sh
    npm install private-module-manager --save
    ```

* Add a postinstall step to your package.json

    ```javascript
    "scripts": {
        "postinstall": "private-module-manager install"
    }

* add `privateDependencies` to your package.json

    ```javascript
    "privateDependencies": {
        "my-module": "git@github.com:foo-bar/my-module#ace-branch"
    }
    ```

* You can set the script used to clone the github repo with the `PMM_CLONE_SCRIPT` environment variable. The script will be called like:

    `/path/to/script.sh <reponame> <repo-url> <directory to clone to> <branch/tag/sha to checkout>`

    It is the responsibility of your script to clone the module into the directory, and ensure the correct branch/tag is checked out. A basic script is included as a default, but you'll need yourown if you need to monkey around with ssh deploy keys etc.
