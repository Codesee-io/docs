CodeSee is offered as a hosted service, but you can also run it locally on your machine as a Docker container (please [get in touch with us](mailto:support@codesee.io?subject=CodeSee Local Access) for access).

## Account setup
1. Get access to docker codeseeio/app_node, make sure to have Docker installed, and that you are logged in.
1. Get access to github.com/codesee-io/codesee-alpha, and git clone it locally. We recommend putting this repo *outside* of your app directory. For example:

- src/
  - my-app/
  - codesee-alpha/

```
git clone git@github.com:Codesee-io/codesee-alpha.git --depth=1
```

## CodeSee Local setup
1. From the local, cloned codesee-alpha directory, run docker compose:
   `docker-compose up`
1. Wait for postgres to report it's ready to receive requests, then hit Control C to stop the server
1. When you're ready, run `docker-compose up` and your CodeSee server should be good to go. You'll know everything is working when you see the message: `server started at http://localhost:5198`

From now on, you can run `docker-compose up` in the codesee-alpha directory anytime to start up the CodeSee server, and \<ctrl\>+c to bring the server back down.

## Setting up CodeSee on your codebase

Please follow our instructions on [installing CodeSee](/install/installation), with the added
instruction of setting `hosted` to `false`, or removing the option entirely.
