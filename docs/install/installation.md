# Installing CodeSee in your project

This section describes how to install CodeSee into your project.

Following these instructions, you will:

1. Install two npm packages.
2. Configure Babel so that CodeSee instruments your code when running in development.
3. Rebuild and run your app locally.


## Step 1: Install the CodeSee package in your JavaScript or TypeScript app
In the terminal, run the install command for your package manager:

=== "npm"

    ```
    npm install --save-dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
    ```

=== "yarn"

    ```
    yarn add --dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
    ```

## Step 2: Configure your project for CodeSee

Follow the links below to set up CodeSee for your specific project environment:

- [Create React App](/install/setup-cra)
- [Typescript, but without Babel](/install/setup-typescript-without-babel)
- [Next](/install/setup-next)
- [Nuxt](/install/setup-nuxt)
- [Storybook](/install/setup-storybook)
- [Gatsby](/install/setup-gatsby)
- [Ember](/install/setup-ember)

Or, select generic setup if you use Typescript with Babel, or another framework not listed above:

- [Generic setup](/install/setup-generic)

## Step 3: Rebuild and run your app locally

Rebuild your app, wait a few seconds, and you should see the CodeSee button towards the top right of your screen. Congrats, you're ready to start using CodeSee!


## Next steps

* [Using CodeSee](/use/quick-start)
* [Troubleshooting](/troubleshooting)