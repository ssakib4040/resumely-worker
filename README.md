## Getting Started

This repository is wired for DigitalOcean App Platform and GitHub Actions. The app runs as a Node.js service and can be deployed automatically from the `main` branch.

**Note: Following these steps may result in charges for the use of DigitalOcean services.**

### Requirements

- You need a DigitalOcean account. If you don't already have one, you can sign up at https://cloud.digitalocean.com/registrations/new.

## Deploying the App

To create or recreate the App Platform app:

1. Open https://cloud.digitalocean.com/apps and click **Create App**.
1. Choose **GitHub** as the source and connect the `ssakib4040/resumely-worker` repository.
1. Select the `main` branch.
1. Let App Platform detect the Node.js service, then keep the generated service settings unless you need custom ports or environment variables.
1. Review the app name and region, then launch the app.

App Platform will build and deploy on pushes to `main` when the repository is connected and auto-deploy is enabled.

## GitHub Actions CI/CD

The workflow in [`.github/workflows/ci-cd.yml`](.github/workflows/ci-cd.yml) does two things:

1. Runs CI on every pull request and push by installing dependencies and smoke-testing the app.
1. Triggers a DigitalOcean deployment on pushes to `main` when the required secrets exist.

To make the deploy job work, add these GitHub repository secrets in **Settings > Secrets and variables > Actions**:

1. `DO_API_TOKEN` - create this in DigitalOcean under **My Account > API > Tokens/Keys**.
1. `DO_APP_ID` - copy this from your DigitalOcean App Platform app details or from the app URL in the DigitalOcean dashboard.

If you only want CI and do not want GitHub to trigger deployments, you can leave those secrets unset.

## Where GitHub Is Connected

GitHub is used in two places:

1. DigitalOcean App Platform connects directly to this repository and watches the `main` branch.
1. GitHub Actions reads the workflow file in this repo and uses repository secrets to talk to DigitalOcean.

That means you do not paste GitHub into the app itself anywhere else. You connect the repo in DigitalOcean, then add the secrets inside GitHub.

### Making Changes to Your App

If you connect your own copy of this repo, you can push changes to `main` and see App Platform automatically re-deploy the update to your app. During these automatic deployments, your application will never pause or stop serving request because App Platform offers zero-downtime deployments.

Here's an example code change you can make for this app:

1. Edit code within the repository
1. Commit the change to the `main` branch. Normally it's a better practice to create a new branch for your change and then merge that branch to `main` after review, but for this demo you can commit to the `main` branch directly.
1. Visit https://cloud.digitalocean.com/apps and navigate to your app.
1. You should see a "Building..." progress indicator, just like when you first created the app.
1. Once the build completes successfully, click the **Live App** link in the header and you should see your updated application running. You may need to force refresh the page in your browser (e.g. using **Shift+Reload**).

### Learn More

You can learn more about the App Platform and how to manage and update your application at https://www.digitalocean.com/docs/app-platform/.

## Deleting the App

When you no longer need this sample application running live, you can delete it by following these steps:

1. Visit the Apps control panel at https://cloud.digitalocean.com/apps.
2. Navigate to the app.
3. In the **Settings** tab, click **Destroy**.

**Note: If you do not delete your app, charges for using DigitalOcean services will continue to accrue.**
