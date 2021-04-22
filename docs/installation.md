---
hide:
  - toc
---
# Installing CodeSee in your project

Following the instructions below, you will:

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

- [**Create React App**](../setup-cra)
- [**Typescript, but without Babel**](../setup-typescript-without-babel)
- [**Next**](../setup-next)
- [**Nuxt**](../setup-nuxt)
- [**Storybook**](../setup-storybook)
- [**Gatsby**](../setup-gatsby)
- [**Ember**](../setup-ember)

Or, select generic setup if you use Typescript with Babel, or another framework not listed above:

- [**Generic setup**](../setup-generic)

## Step 3: Rebuild and run your app locally
Rebuild your app, wait a few seconds, and you should see the CodeSee button towards the top right of your screen. Congrats, you're ready to start using CodeSee!


## [Next step: Using CodeSee](../quick-start)

## [Troubleshooting](../troubleshooting)


&nbsp;
