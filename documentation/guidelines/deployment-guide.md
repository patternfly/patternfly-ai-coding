# Quick Deployment Guide for Prototypes

This guide provides simple, fast methods for building and deploying your React application so you can share a live prototype with others.

## Introduction

Once you have a working prototype on your local machine, the next step is to host it on a public URL. The services listed below are excellent for this purpose, offering generous free tiers and simple command-line interfaces (CLIs) that make deployment a breeze.

## 1. Build Your Application

Before you can deploy, you need to create a production-ready build of your application. This process compiles your React code into a set of static HTML, CSS, and JavaScript files that can be served by any web server.

From your project's root directory, run the following command:

```bash
# Using npm
npm run build

# Or using yarn
yarn build
```

This command will create a new directory named `dist` (or sometimes `build`) in your project. This is the folder you will deploy.

## 2. Choose a Deployment Service

Here are four popular options for hosting your static site, ranked from simplest to most involved. For the absolute fastest deployment with no prior setup, Surge is the best choice.

### Option A: Deploying with Surge

Surge is famous for its simplicity and speed, making it an excellent choice for instant deployments. You can create an account directly from the command line on your first use.

1.  **Install the Surge CLI**:
    ```bash
    npm install -g surge
    ```

2.  **Deploy your app**:
    From your project's root directory, run the `surge` command and point it to your build folder.
    ```bash
    surge dist
    ```
    The first time you use it, Surge will prompt you to create a free account. It will then ask you to confirm the publish directory and will suggest a random domain name, which you can edit on the fly before deploying.

    Your site will be live moments after you hit Enter.

### Option B: Deploying with Vercel

Vercel is a zero-configuration deployment platform that is also incredibly easy to use.

1.  **Install the Vercel CLI**:
    ```bash
    npm install -g vercel
    ```

2.  **Log in to your Vercel account**:
    ```bash
    vercel login
    ```
    *(This will open a browser window for you to log in or sign up.)*

3.  **Deploy your app**:
    From your project's root directory, run the `vercel` command.
    ```bash
    vercel
    ```
    Vercel's CLI will guide you through a few simple questions. In most cases, you can accept the default answers. It will automatically detect that you have a Vite-based React app and deploy the `dist` directory.

    Once finished, it will give you a public URL for your prototype.

### Option C: Deploying with Netlify

Netlify is another excellent platform for deploying static sites, with a very similar workflow to Vercel.

1.  **Install the Netlify CLI**:
    ```bash
    npm install -g netlify-cli
    ```

2.  **Log in to your Netlify account**:
    ```bash
    netlify login
    ```

3.  **Deploy your app**:
    From your project's root directory, run the `netlify deploy` command.
    ```bash
    netlify deploy --prod
    ```
    The CLI will ask you for the "Publish directory". Enter `dist` (or the name of your build output folder). It will then deploy your site and provide you with a live URL.

### Option D: Deploying with GitHub Pages

If your project is already a GitHub repository, GitHub Pages is a convenient, free option, though it requires more setup than the other services.

1.  **Install the `gh-pages` package**:
    ```bash
    npm install --save-dev gh-pages
    ```

2.  **Update your `package.json`**:
    Add a `homepage` field and a `deploy` script. The `homepage` URL should follow this format: `https://<YOUR-USERNAME>.github.io/<YOUR-REPO-NAME>`.

    ```json
    {
      "name": "my-react-app",
      "homepage": "https://my-username.github.io/my-react-app",
      "scripts": {
        "dev": "vite",
        "build": "vite build",
        "deploy": "gh-pages -d dist",
        "preview": "vite preview"
      },
      // ... other package.json contents
    }
    ```

3.  **Deploy**:
    First, build your application, then run the new `deploy` script.
    ```bash
    # 1. Build the app
    npm run build

    # 2. Deploy to GitHub Pages
    npm run deploy
    ```
    This will create a new `gh-pages` branch in your repository and publish the contents of your `dist` folder to it. After a minute or two, your prototype will be live at the URL you specified in the `homepage` field. 