# Jenkins1
Jenkins Assignment 1
Here's the README file for your Jenkins setup:  

---

# **Jenkins Pipeline for Git Operations and File Publishing**  

## **Overview**  
This project automates Git operations and file creation using Jenkins. It includes Slack and Email notifications for failure and success scenarios.  

## **Technologies Used**  
- Jenkins  
- Shell Scripting  
- Git  
- Slack & Email Notifications  
- Web Server (Apache/Nginx)  

---

## **Part 1: Git Operations Job**  
### **Steps Performed:**  
1. Clone the Git repository  
2. Create a new branch  
3. List all branches  
4. Merge one branch into another  
5. Rebase one branch with another  
6. Delete the created branch  

### **Jenkins Job Configuration:**  
1. **Create a Freestyle Job** named `Git_Operations_Job`  
2. **Add "Execute Shell" Step:**  
   ```bash
   REPO_URL="git@github.com:[Shivikh0505.git](https://github.com/Shivikh0505)"
   BRANCH_NAME="new-feature-branch"
   BASE_BRANCH="main"
   REBASE_BRANCH="develop"

   git clone $REPO_URL repo_dir
   cd repo_dir
   
   git checkout -b $BRANCH_NAME || { echo "Branch Creation Failed"; exit 1; }
   git branch -a || { echo "Branch Listing Failed"; exit 1; }
   git checkout $BASE_BRANCH
   git merge $BRANCH_NAME || { echo "Merge Failed"; exit 1; }
   git checkout $REBASE_BRANCH
   git rebase $BASE_BRANCH || { echo "Rebase Failed"; exit 1; }
   git branch -d $BRANCH_NAME || { echo "Branch Deletion Failed"; exit 1; }
   ```

3. **Configure Slack & Email Notifications:**  
   - Go to **Post-build Actions** → Add **Slack Notification** and configure the workspace  
   - Add **Email Notification** with recipient details  

---

## **Part 2: File Creation and Publishing**  
### **Job 1: Create File (`Create_File_Job`)**  
1. **Create a Parameterized Job** → Add String Parameter `Ninja_Name`  
2. **Add "Execute Shell" Step:**  
   ```bash
   echo "${Ninja_Name} from DevOps Ninja" > /var/www/html/ninja_file.txt
   ```  
3. **Configure Notifications for Failure/Success**  

### **Job 2: Publish File (`Publish_File_Job`)**  
1. **Set as Downstream of `Create_File_Job`**  
   - Go to **"Build Triggers"** → Select **"Build after other projects are built"**  
   - Mention `Create_File_Job` as upstream  
2. **Add "Execute Shell" Step to Serve File:**  
   ```bash
   cat /var/www/html/ninja_file.txt
   ```  
3. **Enable Notifications for Success/Failure**  

---

## **Final Setup**  
- Ensure Jenkins jobs run in sequence  
- Verify Slack and Email alerts  
- Test with different `Ninja_Name` values  

---

## **Expected Outcomes**  
✔️ Automated Git operations  
✔️ File creation & publishing  
✔️ Error handling & notifications  

This setup ensures a smooth DevOps workflow using Jenkins. 🚀
