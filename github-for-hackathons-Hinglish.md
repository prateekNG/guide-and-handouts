## **Beginner's Guide to Collaborative Git/GitHub Workflow for Small Teams (Hinglish Edition)**

### **1. Apna Repository Set Up Karna**

- **Shared Repository Banaye**: Ek team member GitHub pe repository banata hai aur baaki sab ko collaborators mein add kar deta hai.
- **Main Branch (`main`)**: Yeh branch hamesha stable aur production-ready code rakhti hai.
- **Feature Branches**: Har team member apna kaam alag-alag branches mein karta hai, jise feature ya fix ke naam se banaya jaata hai (e.g., `feature/login-system`).

### **2. Branching Strategy**

- **Main Branch**: Hamesha stable aur deployable rakhni chahiye.
- **Feature Branches**: Har nayi feature, bug fix, ya enhancement ke liye ek branch banao.

**Example**:
```bash
git checkout -b feature/your-feature-name
```

### **3. Har Team Member ke liye Workflow**

1. **Repository Clone Karo**:
   ```bash
   git clone https://github.com/your-team/your-repo.git
   cd your-repo
   ```

2. **Feature Branch Banao**:
   ```bash
   git checkout -b feature/your-feature-name
   ```

3. **Apni Feature Pe Kaam Karo**:
   - Changes karo, stage karo, aur commit karo:
     ```bash
     git add .
     git commit -m "Implemented feature X"
     ```

4. **Apni Branch Ko Updated Rakho**:
   - Latest `main` ko apni feature branch mein merge karte raho taaki sab updated rahe:
     ```bash
     git checkout main
     git pull origin main
     git checkout feature/your-feature-name
     git merge main
     ```
   - Conflicts resolve karo, locally test karo, aur phir resolved changes ko commit karo.

5. **Apni Branch GitHub Pe Push Karo**:
   ```bash
   git push origin feature/your-feature-name
   ```

### **4. Code Review Aur Collaboration**

1. **Pull Request (PR) Open Karo**:
   - GitHub pe apni feature branch se `main` branch mein PR open karo.
   - Ek clear description do aur apne teammates se review ke liye request karo.

2. **PRs Review Aur Approve Karo**:
   - Ek dusre ke PRs review karo, feedback do, aur sab thik lage to approve karo.

3. **Final Testing**:
   - Ensure karo ki sab tests pass ho rahe hain aur feature expected tarike se kaam kar rahi hai.

4. **PR Merge Karo**:
   - "Squash and Merge" ya "Rebase and Merge" options use karke history clean rakho.
   - Merge ke baad feature branch delete kar do.

### **5. Synchronization aur Communication**

1. **Daily Sync**:
   - Regularly `main` branch se latest changes pull karo:
     ```bash
     git pull origin main
     ```

2. **Team Communication**:
   - Discord, GitHub Issues, ya Trello jaise tools use karke progress track karo aur issues discuss karo.

3. **Conflicts Jaldi Resolve Karo**:
   - Merge conflicts aate hi unhe jaldi resolve karo aur team se help maango agar zaroorat pade.

### **6. Galti se Push Hone Se Kaise Bache**

1. **Branch Protection Enable Karo**:
   - `main` branch ko protect karo taaki koi directly push na kar sake.
   - Pull request reviews aur passing checks ko enforce karo.

2. **Pull Request Workflow Implement Karo**:
   - `main` branch mein changes merge karne ke liye hamesha PRs use karo.
   - Ensure karo ki sab changes review aur test hone ke baad hi merge ho.

3. **Roles Aur Permissions Use Karo**:
   - Team members ko appropriate roles assign karo taaki direct push karne ka access control mein rahe.

### **7. Quick Reference Commands**

- **Nayi Branch Banao**:
  ```bash
  git checkout -b feature/your-feature-name
  ```
- **Main Ko Feature Branch Mein Merge Karo**:
  ```bash
  git checkout main
  git pull origin main
  git checkout feature/your-feature-name
  git merge main
  ```
- **Apni Branch Push Karo**:
  ```bash
  git push origin feature/your-feature-name
  ```
- **GitHub Pe PR Open Karo**: 
  - Apne repository pe jao GitHub pe, **Pull Requests** pe click karo, phir **New Pull Request** pe.

### **Conclusion**

Iss structured workflow ko follow karke, tumhari team efficiently GitHub pe collaborate kar sakti hai, `main` branch ko stable rakhte hue aur nayi features ko properly review aur test karne ke baad hi merge karti hai. Communication, regular synchronization, aur GitHub features jaise branch protection aur pull requests ka use key hain smooth collaboration ke liye.

*** 

### **Technical Keywords (Simple Words Mein)**

1. **Repository**: Project ke files aur unki version history ko store karne ki jagah.
2. **Branch**: Repository mein alag-alag development lines jahan tum different features ya fixes pe kaam kar sakte ho.
3. **Main Branch (`main`)**: Primary branch jo stable aur deployable version rakhti hai project ka.
4. **Feature Branch**: Ek nayi feature ya bug fix karne ke liye alag branch, jo `main` branch se alag hoti hai.
5. **Commit**: Changes ko repository mein save karna aur ek descriptive message likhna jo bataye ki kya kiya gaya.
6. **Push**: Apni local branch ke commits ko GitHub pe remote repository mein upload karna.
7. **Pull**: Remote repository se latest changes ko apne local machine pe download karna.
8. **Merge**: Ek branch se doosri branch mein changes ko combine karna, usually feature branch se `main` mein.
9. **Conflict**: Jab do alag changes clash karte hain, jise manually resolve karna padta hai merge se pehle.
10. **Pull Request (PR)**: Request karna ki ek branch ke changes doosri branch mein merge ho jaye, jo aksar dusre team members review karte hain.
11. **Branch Protection**: Settings jo certain branches pe direct changes ko rokta hai, ensuring ki sab changes review process se guzrein.
12. **Roles aur Permissions**: Team members ko diye gaye access levels, jo control karte hain ki woh repository mein kya actions perform kar sakte hain.
