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

    /path/to/script.sh <reponame> <repo-url> <directory to clone to>
