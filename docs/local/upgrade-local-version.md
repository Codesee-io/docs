# Upgrading CodeSee Local to the latest version

1. In your local `codesee-alpha` directory, `git pull` the latest changes.
2. Restart your Docker Compose:
    a. Shut down the Docker container with `Ctrl + c`.
    b. Run `docker-compose up` again.
3. From the root of your app, install the latest CodeSee packages:

    === "npm"

        ```shell
        npm install --save-dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
        ```

    === "yarn"

        ```shell
        yarn add --dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
        ```

4. Rebuild and restart your application.


!!! help
    If it appears that nothing has changed, your application may be cacheing its Babel artifacts. If you can do a clean build, try that. Or, if not, try deleting your `node_modules/.cache` directory, or even delete your entire `node_modules` directory.
