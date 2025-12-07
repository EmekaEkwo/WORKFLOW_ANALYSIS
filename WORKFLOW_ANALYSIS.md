# GitHub Actions Workflow Analysis

This document explains how the `deploy.yml` GitHub Actions workflow in this project operates and why it is useful for maintaining a reliable deployment process.

---

### 1. What triggers this workflow to run?

The workflow is triggered automatically whenever changes are pushed to the `main` branch. In the `on:` section of the `deploy.yml` file, the workflow listens for a `push` event targeting `main`. This means any commit that reaches the main branch—either through a pull request or a direct push—will start a new deployment run.

---

### 2. What are the four main steps this workflow performs?

Based on the job steps listed in the workflow, it performs the following actions:

1. **Checkout code** – Pulls the repository files into the GitHub Actions environment.
2. **Set up the environment** – Installs the tools needed (such as Node or HTML validation dependencies) so the workflow can run consistently.
3. **Run validation/tests** – Checks the HTML for issues and ensures there are no broken links or structural errors.
4. **Deploy to GitHub Pages** – Publishes the updated website to GitHub Pages if all previous steps complete successfully.

---

### 3. What does the "Checkout code" step do and why is it necessary?

The checkout step uses the `actions/checkout` action to download the repository’s content into the virtual machine that GitHub provides for the workflow run. Without this step, the workflow would have no access to the project’s files and therefore could not validate the HTML, run any checks, or deploy the website. It essentially prepares the workspace so all following steps can operate on the actual code.

---

### 4. What is the purpose of the environment configuration?

The environment configuration ensures that every workflow run uses the same versions of tools and dependencies. This removes inconsistency between different machines or development setups. By defining the environment explicitly, the workflow becomes predictable and reproducible—two important qualities in professional software development.

---

### 5. How does this automated deployment improve reliability compared to manual deployment?

Manual deployment leaves room for errors such as forgetting to upload a file, skipping a test, or deploying code that hasn't been reviewed. Automated deployment reduces these risks because it always follows the same steps, never forgets validations, and only deploys when the code passes all checks. This consistency helps prevent broken pages and ensures that the live site always reflects a clean and tested version of the project.

---

### 6. What would happen if you pushed code to a different branch (not `main`)?

If code is pushed to another branch—such as a feature branch—the workflow will not run. The deployment process only starts when updates reach the `main` branch. This prevents unfinished or experimental code from being deployed and encourages developers to use pull requests to review changes before they go live.

---
