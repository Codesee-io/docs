---
hide:
  - toc
---
# Upgrading local to the latest version

1. In your local codesee-alpha directory, ```git pull``` the latest changes from this repo
2. Restart your docker compose by shutting down the docker container (Ctrl-C), and then running ```docker-compose up``` again.
3. From the root of your app, install the latest codesee packages:

    === "npm"

        ```
        npm install --save-dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
        ```

    === "yarn"

        ```
        yarn add --dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
        ```

4. Rebuild and restart your application
TROUBLESHOOTING ADVICE: If it appears that nothing has changed, your application may be cacheing its babel artifacts. If you can do a clean build, try that. Or, if not, try removing your ```node_modules/.cache``` directory, or even remove your entire ```node_modules``` directory.
