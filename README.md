# GithubRepoGuide

```git init  # Initializes a new Git repository```
```git remote add origin https://github.com/Username/RepoName.git # Remember the .git is important to add!```
**To add changes and push them**
```git add . # The dot represents everything change the dot with the file name you want to add if you want to add a specific file!```
```git commit -m "Replace this text with the message you want for the commit!"```
```git branch -M main  # Ensure you are on the main branch. (Makes everything easier tbh)```
```git push -u origin main  # Push your code to GitHub or you can do it without the -u if it is easier to remember!```
**To get the latest changes or like to get back the current code**
```git pull origin main```
```git reset --hard origin/main # ONLY IF YOU WANT TO RESTORE THE GITHUB REPO'S FILES THIS WILL REWRITE EVERYTHING```
 **Handling .env files correctly or any enviroment variable with secrets in them like tokens API keys etc.**
 First Create a .gitignore file in the directory of your project in my case I am using Ubuntu so to create the .gitignore file I would do
 ```echo ".env" >> .gitignore``` echo creates a new text file with the ".env" .env representing the text you want to create the file with and .gitignore representing the text file name!
 Then commit the .gitignore file and push!
 ```git filter-branch --force --index-filter "git rm --cached --ignore-unmatch .env" --prune-empty --tag-name-filter cat -- --all``` 
 **ONLY DO THIS IF YOU WANT TO REMOVE A ACCIDENTALLY ADDED PRIVATE FILE FROM THE HISTORY SO IT CANNOT BE RETRIEVED**

