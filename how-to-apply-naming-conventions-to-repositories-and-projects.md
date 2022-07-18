# Summary
**`ALERT` For *Student Developers doing the mass project move*: Please use [this](Naming-Conventions#Repository) instead!**

Because of **[this](Naming-Conventions#Repository)** policy we have these steps to help guide you on how to make this change to a repository. 

Follow the steps top to bottom, starting with **Email the Web Dev Team** and ending with **Uploading Changes**.

# Email the Web Dev Team
1. Email all the web developers to let them know the current Repo you are changing, 
    > Subject: CMich.PersonnelTransaction Rename Starting

    > We are updating the naming conventions https://code.cmich.edu/App-Custom/CMich.PersonnelTransaction  **Tomorrow or the Day After** and it is highly recommended that you commit any uncommited changes and merge them into master IMMEDIATELY. If not they will later need to rebase onto master, and do some very messy local merges. Email us *right away* if you have any concerns. 
2. Wait until the next day you are in the office and reply to any emails about concerns, or needs to hold off on renaming.

# Steps to Change Repo Name and Location
1. Go the The Repo( e.g., https://code.cmich.edu/App-Custom/CMich.PersonnelTransaction)
2. Click :gear: **Settings** (this should link to something like https://code.cmich.edu/App-Custom/CMich.PersonnelTransaction/edit)
3. **Expand** *Advanced settings*
4. Correct Project Name and Path (e.g.,CMich.PersonnelTransaction → PersonnelTransactions), and Click **Rename project**
5. With *Advanced settings* **Expand** still open, under **Transfer project** Move repo to its new rightful home (e.g., **/App-Custom** → **/IT-AppDevelopment/CustomApplications**)
6. Click **Transfer project** `red` button.
7. Enter the Repo name to continue transfer on **Confirmation required** modal

# Steps to change the Solution and Project Directory names
1. From the command line in your desired directory enter `git clone https://code.cmich.edu/App-Custom/PersonnelTransactions.git`
2. Enter 'cd repoName' (e.g., `cd PersonnelTransactions`)
3. Enter `git checkout -b renameRepoAndProjects` to create a new branch where all your changes will happen **(Don't forget this or you will be stuck with changes in `master`)**
4. From the command line in your desired repo enter `git mv OriginalSolutionName.sln NewSolutionName.sln` (e.g.,  `git mv CMich.PersonnelTransaction.sln PersonnelTransactions.sln`)
  - Using `git mv` instead of renaming in Visual Studio is better because git won't do a delete and add, but just a rename, keeping more history on that file
5. Enter `dir` to get a list of the directories, aka Projects, you will later rename
6. Now to rename the first Project enter `git mv OriginalBaseProject Base` (e.g.,  `git mv CMich.PersonnelTransaction\ Base`)
7. Repeat the renaming process for each Project (e.g., CMich.PersonnelTransaction.Web → Web, etc.)
8. Enter 'git status', and you should see nearly every file in the solution has been renamed

# Updating **.Sln** Project Paths
1. Open `MySolution.sln` in VSCode Or Notpad++ (e.g., `code PersonnelTransactions.sln`)
2. Near the top, notice The Project lines, and update the `oldProjectDirectory` to the new shortened name
  - Pattern: (`Project("{hash}") = "projectLabel", "oldProjectDirectory/projectLabel.csproj"`)
  - Before: (e.g., `Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "CMich.PersonnelTransaction.Web", "CMich.PersonnelTransaction.Web\CMich.PersonnelTransaction.Web.csproj"`)
  - After: (e.g., `Project("{FAE04EC0-301F-11D3-BF4B-00C04F79EFBC}") = "CMich.PersonnelTransaction.Web", "Web\CMich.PersonnelTransaction.Web.csproj"`)
3. Repeat this for each project, and when done save the file  

# Steps to Change Project Names in Visual Studio
1. Open your solution in Visual Studio 2017, and have the **Solution Explorer** open (e.g., `start PersonnelTransactions.sln`)
  - If the Projects look empty, carefully repeat the above steps in [Updating **.Sln** Project Paths](https://code.cmich.edu/IT-AppDevelopment/Documentation/wiki/wikis/how-to-apply-naming-conventions-to-repositories-and-projects#updating-sln-project-paths)
2. Right-click on the first project name and pick *Rename* (e.g., CMich.PersonnelTransaction → Base)
3. Repeat for each project (e.g., CMich.PersonnelTransaction.Web → Web, etc.)
4. Right-click on your Solution and pick *Rename*  (e.g., CMich.PersonnelTransaction → PersonnelTransactions)
5. Go into the **.gitlab-ci.yml** and change the "Solution" variable to match the new solution name (e.g., CMich.PersonnelTransaction.sln → PersonnelTransactions.sln)
  - You *may* also need to rename the the Testing, or other paths, so pay attention to this. Examples below.
      - `'msbuild.exe "%BaseSolution%".UnitTests\\"%BaseSolution%".UnitTests.csproj'` → `'msbuild.exe Web.Tests\Web.Tests.csproj'`
      - `mstest.exe /testcontainer:"%BaseSolution%".UnitTests\bin\Debug\\"%BaseSolution%".UnitTests.dll` → `mstest.exe /testcontainer:Web.Tests\bin\Debug\CMich.SearchRegister.UnitTests.dll`
      -  `"CMich.SearchRegister.Web\tsconfig.json" --listEmittedFiles'` → `"Web\tsconfig.json" --listEmittedFiles'`
6. If the project uses TypeScript:
  - Update the tsconfig.json to generate js and map.js files in the correct places.
  - Update the .gitignore to not add the generated js, map.js, and css files.
7. Finally, ***make sure the solution still runs*** by launching it in debug mode by clicking the &#10148; **Google Chrome** button
  - This should build the project, pull in NuGet dependencies, and launch it in a new browser window
  
# Uploading Changes
1. From the command line in your desired directory enter `git add .`
2. Enter `git commit -m "applied new naming conventions for repo and projects"`
3. Enter `git push -u origin renameRepoAndProjects`
4. Create a merge request for **renameRepoAndProjects** → **master**
5. Have another web developer do the actual merge.
6. Wait for the merge to be placed in master

# Email Out to the Web Developers that This Repo is Now Renamed
1. Send out a Reply All on your previous email to all developers saying
    > PersonnelTransactions Rename Complete

    > You should *delete* your local copy and do a fresh `git clone https://code.cmich.edu/IT-AppDevelopment/CustomApplications/PersonnelTransactions.git` since the naming to master for this repo is complete.
2. Pat yourself on the back, you've done it!

## Tags
[[Conventions]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=ConventionsTag)
[[Git]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=GitTag)
[[Policy]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=PolicyTag)
[[VisualStudio]](https://code.cmich.edu/search?project_id=365&repository_ref=master&scope=wiki_blobs&search=VisualStudioTag)