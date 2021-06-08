CodeSee is offered as a hosted service, but you can also run it locally on your machine as a Docker container (please [get in touch with us](mailto:support@codesee.io?subject=CodeSee Local Access) for access).

## Account setup

1. Get access to our Docker image, codeseeio/app_node, make sure you have Docker installed, and that you are logged in.
2. Get access to `github.com/codesee-io/codesee-alpha`, and clone it locally. We recommend putting this repo *outside* of your app directory. For example:
  ```
  - src/
    - my-app/
    - codesee-alpha/
  ```
  ```
  git clone git@github.com:Codesee-io/codesee-alpha.git --depth=1
  ```

## CodeSee Local setup

1. From the local, cloned codesee-alpha directory, run Docker Compose: `docker-compose up`.
2. Wait for Postgres to report that it's ready to receive requests, then hit `Ctrl + c` to stop the server.
3. Run `docker-compose up` again, and your CodeSee server should be good to go. You'll know everything is working when you see the message: `server started at http://localhost:5198`.

From now on, you can run `docker-compose up` in the `codesee-alpha` directory to start up the CodeSee server, and `Ctrl + c` to bring the server back down.

## Setting up CodeSee on your codebase

Please follow our instructions on [installing CodeSee](../../install/installation). 

!!! note
    You must set `hosted` to `false` during setup. For example:
    ```
    babelLoaderConfig.options.plugins.push(["@codesee/instrument", { hosted: false }]);
    ```
