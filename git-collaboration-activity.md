## **Git & GitHub Activity Guide: “Collaborative Recipe Creation”**

**Objective**: By the end of this activity, you’ll understand basic Git and GitHub workflows, including creating a repository, forking, making commits, collaborating, and handling merge conflicts.

### **Overview**

You and your partner will work together to create a shared "Recipe" repository. Each of you will add an ingredient and step to the recipe to practice making commits, pushing changes, creating a pull request, and resolving merge conflicts.

### **Duration**: 30–45 minutes

---

### **Prerequisites**

- Both learners should have Git installed and a GitHub account.
- Basic understanding of the command line is helpful but not required.

---

### **Activity Steps**

### **Part 1: Repository Creation & Setup**

1. **Create a New Repository** (5 minutes)
   - Decide which partner will be the “Owner” (A) and who will be the “Contributor” (B).
   - Partner A:
     - Go to GitHub, click on **New repository**.
     - Name the repository (e.g., `collaborative-recipe`) and set it to **Public**.
     - Add a README file by checking the option "Add a README file".
     - Click **Create repository**.
   - Partner B:
     - Navigate to Partner A’s GitHub profile, find the `collaborative-recipe` repository, and **fork** it to your own account.

2. **Clone the Repository Locally** (5 minutes)
   - Both Partner A and Partner B should open a terminal and clone their respective repositories:
     ```bash
     git clone <YOUR_REPOSITORY_URL>
     ```
   - After cloning, navigate into the project directory:
     ```bash
     cd collaborative-recipe
     ```

---

### **Part 2: Adding Initial Content**

3. **Create an Initial Recipe File** (5 minutes)
   - Partner A:
     - In the cloned repo, create a new file named `recipe.txt`:
       ```bash
       touch recipe.txt
       ```
     - Add a title to the file (e.g., "Best Chocolate Chip Cookies").
     - Save and **stage** the change:
       ```bash
       git add recipe.txt
       ```
     - Commit the change with a descriptive message:
       ```bash
       git commit -m "Add initial recipe title"
       ```
     - Push the change to GitHub:
       ```bash
       git push origin main
       ```

4. **Partner B Adds Ingredients** (5 minutes)
   - Partner B:
     - Pull the latest changes from GitHub to your local fork:
       ```bash
       git pull upstream main
       ```
     - Open `recipe.txt` and add the ingredients section:
       ```
       Ingredients:
       - 1 cup butter
       - 1 cup sugar
       ```
     - Save, stage, and commit the changes:
       ```bash
       git add recipe.txt
       git commit -m "Add ingredients section"
       ```
     - Push changes to your GitHub fork:
       ```bash
       git push origin main
       ```

5. **Create a Pull Request (PR)** (5 minutes)
   - Partner B:
     - On your GitHub fork page, click on **New pull request**.
     - Write a short description, then submit the pull request.
   - Partner A:
     - Review and **merge** the pull request into the main branch.

---

### **Part 3: Creating a Merge Conflict**

6. **Simultaneous Edits to Create a Conflict** (10 minutes)
   - Both Partner A and Partner B will add a "Preparation" section to `recipe.txt`.
   - **Partner A**:
     - Add the following to `recipe.txt`:
       ```
       Preparation:
       - Step 1: Preheat the oven to 350°F.
       ```
     - Save, stage, and commit:
       ```bash
       git add recipe.txt
       git commit -m "Add oven preheating step"
       ```
     - Push to GitHub:
       ```bash
       git push origin main
       ```
   - **Partner B**:
     - Add a different step to `recipe.txt`:
       ```
       Preparation:
       - Step 1: Mix butter and sugar until smooth.
       ```
     - Save, stage, and commit:
       ```bash
       git add recipe.txt
       git commit -m "Add mixing step"
       ```
     - Push changes to your fork on GitHub:
       ```bash
       git push origin main
       ```
     - On GitHub, create a **pull request** for this change.

7. **Resolve the Merge Conflict** (10 minutes)
   - Partner A:
     - Review the pull request from Partner B, where GitHub will show a **merge conflict** message.
     - Click on **Resolve conflicts** to open GitHub’s conflict editor.
     - Decide on a resolution together:
       ```
       Preparation:
       - Step 1: Preheat the oven to 350°F.
       - Step 2: Mix butter and sugar until smooth.
       ```
     - After editing, click **Mark as resolved** and then **Commit merge**.
     - Complete the pull request by clicking **Merge**.

---

### **Reflection and Discussion**

Take 5 minutes to discuss these questions with your partner:

- What steps in this process felt clear, and which were challenging?
- Why is it important to resolve merge conflicts carefully?
- How do you see Git and GitHub being useful in larger projects?
