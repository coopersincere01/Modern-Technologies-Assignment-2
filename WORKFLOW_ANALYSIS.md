# GitHub Actions Workflow Analysis

## 1. What triggers this workflow to run?

This workflow runs when code is pushed to the `main` branch or when a pull request is opened or updated that's going into `main`. The `on:` section in the `deploy.yml` file controls that. The build and test part can run for both pushes and pull requests, but the website only gets deployed when there is an actual push to `main`.

## 2. What are the four main steps this workflow performs?

The four main steps in the `build-and-test` job are

1. **Checkout code** – Gets the repository files so the workflow can use them.
2. **Validate HTML** – Checks the HTML files for errors.
3. **Check links** – Looks for broken links in the project.
4. **Upload artifact** – Uploads the website files so they can be used for deployment.

After those steps are finished there's also a separate deployment job called **Deploy to GitHub Pages**. That part publishes the website if the workflow was triggered by a push to `main`.

## 3. What does the "Checkout code" step do and why is it necessary?

The `Checkout code` step gets the files from the repository and places them on the GitHub Actions runner. The workflow runs on its own machine so it needs this step before it can actually see and work with the project files. Without checking out the code first the later steps wouldn't have anything to validate, test, or deploy.

## 4. What is the purpose of the environment configuration?

The environment configuration tells GitHub that this deployment is using the `github-pages` environment. It also connects the deployment to the URL of the live site after the deployment finishes. This helps keep the deployment part organized and lets GitHub show where the website was deployed.

## 5. How does this automated deployment improve reliability compared to manual deployment?

This makes deployment more reliable because the same steps happen each time instead of depending on someone remembering everything manually. The workflow checks the HTML and links before deployment so problems have a better chance of being caught first. It also lowers the chance of mistakes like forgetting a step, uploading the wrong files, or deploying something that was not checked. Overall the process is more consistent because GitHub handles it the same way each time. Another benefit is that the workflow creates a clear record in GitHub Actions showing whether each deployment passed or failed, which makes problems easier to track. 

## 6. What would happen if you pushed code to a different branch instead of `main`?

If I pushed code directly to a branch other than `main`, this workflow wouldn't run because the push trigger is only set for `main`. If I made a pull request from another branch into `main` the build and test job would still run because pull requests targeting `main` are included. The deployment job would be skipped though, because it only deploys when the event is a push to `main`. This lets changes be tested before they are actually added to the live website.