# Updating to the latest version
WARNING: If you are updating from pre-0.7.0, this update will erase all your existing recordings. We do apologize! We will do our best to avoid this in the future.

1. In your local codesee-alpha directory, `git pull` the latest changes from this repo
2. Restart your docker compose by shutting down the docker container (Ctrl-C), and then running `docker-compose up` again.
3. From the root of your app, install the latest codesee packages:
   - If you are using npm, run: `npm install --save-dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
   - If you are using yarn, run: `yarn add --dev @codesee/tracker@0.10.1 @codesee/babel-plugin-instrument@0.10.1`
4. Rebuild and restart your application

TROUBLESHOOTING ADVICE: If it appears that nothing has changed, your application may be cacheing its babel artifacts. If you can do a clean build, try that. Or, if not, try removing your `node_modules/.cache` directory, or even remove your entire `node_modules` directory.
