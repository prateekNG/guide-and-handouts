## Handout: Introduction to GitHub

### 1. **Introduction to GitHub**

**What is GitHub?**
- GitHub is a web-based platform for version control and collaboration using Git.
- It allows developers to share code, work together on projects, and track changes.

**Analogy**: Think of GitHub as a social networking site for developers, where they can share code, collaborate on projects, and keep track of changes.

### 2. **Creating a GitHub Account**

**Steps to Create an Account:**
1. Go to [GitHub](https://github.com) and click "Sign up".
2. Follow the instructions to create an account.
3. Verify your email address.

### 3. **Setting Up GitHub Authentication**

**Generating a Personal Access Token (PAT):**
1. Log in to GitHub.
2. Navigate to **Settings** > **Developer settings** > **Personal access tokens**.
3. Click **Generate new token**.
4. Select the required scopes (permissions), such as `repo` for full control of private repositories.
5. Click **Generate token** and copy the token.

**Configuring Git to Use the Token:**
```sh
git config --global credential.helper cache
```
- When prompted for your username and password while pushing changes, use your GitHub username and the personal access token.

### 4. **Creating a Repository**

**Steps to Create a Repository:**
1. Log in to GitHub and click on the "+" icon at the top right.
2. Select "New repository".
3. Name the repository (e.g., "my-first-repo") and add a description.
4. Initialize the repository with a README file.
5. Click "Create repository".

### 5. **Forking a Repository**

**What is Forking?**
- Forking is making a personal copy of someone else’s repository to propose changes or use it as a starting point for your own project.

**Steps to Fork a Repository:**
1. Find a public repository on GitHub.
2. Click the "Fork" button at the top right of the repository page.
3. This creates a copy of the repository under your GitHub account.

### 6. **Cloning a Repository**

**What is Cloning?**
- Cloning is downloading a copy of a repository from GitHub to your local machine.

**Steps to Clone a Repository:**
1. Copy the repository URL from GitHub.
2. Use the following Git command to clone the repository:
   ```sh
   git clone https://github.com/yourusername/my-first-repo.git
   ```

### 7. **Making Changes and Pushing to GitHub**

**Steps to Make Changes and Push to GitHub:**
1. Navigate to the cloned repository:
   ```sh
   cd my-first-repo
   ```
2. Create a new file and add some content:
   ```sh
   echo "Hello, GitHub!" > hello.txt
   ```
3. Stage and commit the changes:
   ```sh
   git add hello.txt
   git commit -m "Add hello.txt"
   ```
4. Push the changes to GitHub:
   ```sh
   git push origin main
   ```

**Note**: If prompted for authentication, use your GitHub username and the personal access token.

### 8. **Creating and Merging Pull Requests**

**What is a Pull Request?**
- A pull request allows you to propose changes to a repository and have them reviewed before they are merged into the main project.

**Steps to Create and Merge a Pull Request:**
1. Create a new branch:
   ```sh
   git checkout -b feature-branch
   ```
2. Make changes, commit, and push the branch:
   ```sh
   echo "Some new features" > feature.txt
   git add feature.txt
   git commit -m "Add feature.txt"
   git push origin feature-branch
   ```
3. Go to the repository on GitHub and create a pull request from `feature-branch` to `main`.
4. Review and discuss the changes.
5. Merge the pull request.

---

## Quick Reference / Cheat Sheet

### GitHub Basics

**Create a Repository:**
1. GitHub: "+" icon > "New repository" > Fill details > "Create repository"

**Fork a Repository:**
1. GitHub: Navigate to repository > "Fork" button

**Clone a Repository:**
```sh
git clone https://github.com/username/repo.git
```

**Create and Push Changes:**
1. Create a new file and add content:
   ```sh
   echo "Hello, GitHub!" > hello.txt
   ```
2. Stage and commit the changes:
   ```sh
   git add hello.txt
   git commit -m "Add hello.txt"
   ```
3. Push the changes:
   ```sh
   git push origin main
   ```

**Create a Branch and Push Changes:**
1. Create a new branch:
   ```sh
   git checkout -b feature-branch
   ```
2. Make changes, commit, and push the branch:
   ```sh
   echo "New feature" > feature.txt
   git add feature.txt
   git commit -m "Add feature.txt"
   git push origin feature-branch
   ```

**Create a Pull Request:**
1. GitHub: Navigate to repository > "Pull requests" tab > "New pull request" > Select branches > "Create pull request"

### Authentication

**Generate Personal Access Token (PAT):**
1. GitHub: Settings > Developer settings > Personal access tokens > Generate new token

**Configure Git to Use Token:**
```sh
git config --global credential.helper cache
```

### Common Commands

**Check Git Status:**
```sh
git status
```

**View Git Log:**
```sh
git log
```

**Fetch and Merge Changes:**
```sh
git fetch origin
git merge origin/main
```
