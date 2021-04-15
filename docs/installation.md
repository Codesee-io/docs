# Installing CodeSee in your project

Following the instructions below, you will:

1. Install two npm packages.
2. Configure Babel so that CodeSee instruments your code when running in development.
3. Rebuild and run your app locally.


## Step 1: Install the CodeSee package in your JavaScript or TypeScript app
In the terminal, run the install command for your package manager:

<details><summary>npm</summary>

```
npm install --save-dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
```

</details>
<details><summary>yarn</summary>

```
yarn add --dev @codesee/tracker@latest @codesee/babel-plugin-instrument@latest
```
</details>

## Step 2: Configure your project for CodeSee
Follow the links below to set up CodeSee for your specific project environment:

- [**Create React App**](../setup-cra)
- [**Typescript, but without Babel**](../setup-typescript-without-babel)
- [**Nuxt**](../setup-nuxt)
- [**Storybook**](../setup-storybook)
- [**Gatsby**](../setup-gatsby)
- [**Ember**](../setup-ember)

Or, select generic setup if you use Next.js, Typescript with Babel, or another framework not listed above:

- [**Generic setup**](../setup-generic)

## Step 3: Rebuild and run your app locally
Rebuild your app, wait a few seconds, and you should see the CodeSee eye icon towards the top right of your screen. Then you can celebrate!

A few thoughts to help you on your CodeSee journey:

- If the CodeSee icon is in a red circle then you're not logged in. Click it to log into CodeSee.
- If the CodeSee icon is in a purple circle, you're ready to go! Click it to start recording, interact with your app, then click it again to stop recording.
- Keep recordings as short as possible -- focus on the one thing you want to understand better.
- When you finish recording, CodeSee will open a new tab with your recording in it as soon as all the data has been transmitted. For larger recordings or on slower networks, there can be some buffering, so please give it a few seconds or more to finish sending the recording to our servers.
    - If it delays for long enough, your pop-up blocker may decide to block it. Keep an eye out for that if the codesee site isn't coming up. If in doubt, you can always go to [app.codesee.io/library](app.codesee.io/library) to see all your latest recordings.
- The CodeSee UI can be a little sluggish with larger recordings! Sorry about that! For the moment, we ask that you give our UI a second to process now and then. But fear not, we take performance very seriously and we're actively working on performance improvements.

## Compatibility and troubleshooting
### We're here to help
If there's anything you need, or you just want to tell us what you think, please don't hesitate to reach out to us at: <a href="mailto:support@codesee.io">support@codesee.io</a>.

### Browsers
Currently, for CodeSee to work properly, you'll need to be running your application in Chrome.

### Third-Party Cookies
Unfortunately, if third-party cookies are blocked, our authentication process does not work.

If you have disabled cross-site cookies, you'll need to add the following to the "allow these sites to always use cookies" list in Chrome settings to get CodeSee to work:

```
app.codesee.io
[*.]okta.com
```

&nbsp;  