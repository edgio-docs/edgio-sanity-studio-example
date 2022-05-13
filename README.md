# Deploying Sanity Studio with Layer0

## By [Rishi Raj Jain](https://rishi.app)

Sanity Studio is a single page app (SPA) written in React, where you can configure the document types and input fields, with simple JavaScript objects. This guide will walk you through how to deploy Sanity Studio with Layer0 in four simple steps.

![Deploying Sanity Studio with Layer0](https://cdn.sanity.io/images/81pocpw8/production/a430c6c7d8de38357ddb99a38876ca955a16c9ee-1200x630.png?w=800&h=420&fit=clip&auto=format)

## Step 1: Setting Up your Sanity Studio Project

**NOTE:** You can skip this step if you already have a project set up.

First, install the [Sanity CLI](https://www.npmjs.com/package/@sanity/cli):

`npm i -g @sanity/cli`

To initiate a new project and download the Studio code to your computer, run the following in the command line:

`sanity init`

The Sanity CLI will walk you through the necessary steps to set up a project, letting you choose a schema template. When you're done with these steps, the CLI will download the source code and configuration to get you started. To start a local development server, `cd` into the project folder and run the following command:

`sanity start`

## Step 2: Preparing for Deployment

First, install the [Layer0 CLI](https://www.npmjs.com/package/@layer0/cli):

`npm i -g @layer0/cli`

To add Layer0 to an existing app, run the following:

`layer0 init`

The above command creates routes.ts and layer0.config.js. Replace the content in routes.ts by the following:

```bash
import { Router } from '@layer0/core/router'
export default new Router()
    .static('dist')
    .fallback(({ appShell }) => {
        appShell('dist/index.html')
    })
```

After saving your `routes.ts` file you will be ready to deploy your project.

## Step 3: Preview Production Locally With Layer0

To preview production app locally run:

1\. `sanity build && layer0 build`

2\. Set default port number for the app to run on 3333:

`set PORT=3333 // windows`

OR

`export PORT=3333 // ubuntu`

3\. `layer0 run --production`

## Step 4: Deploy With Layer0

To deploy run:

`sanity build && layer0 deploy`

Once Sanity Studio is deployed, you will need to add it's URL to Sanity’s [CORS origins](https://www.sanity.io/docs/front-ends/cors) settings. You can do this from the command line:

`sanity cors add https://your-url.layer0-limelight.link --credentials`

Alternatively, you can navigate to [manage.sanity.io](https://manage.sanity.io/), find your project and under Settings > API, add the Studio URL to the CORS origins list. You should allow credentials as the Studio requires authentication for added security.
