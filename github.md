# GithubRepoGuide

```bash
git init  # Initializes a new Git repository
```

```bash
git remote add origin https://github.com/Username/RepoName.git # Remember the .git is important to add!
```

**To add changes and push them:**

```bash
git add . # The dot represents everything. Change the dot with the file name you want to add if you want to add a specific file!
```

```bash
git commit -m "Replace this text with the message you want for the commit!"
```

```bash
git branch -M main  # Ensure you are on the main branch. (Makes everything easier tbh)
```

```bash
git push -u origin main  # Push your code to GitHub, or you can do it without the -u if it is easier to remember!
```

**To get the latest changes or revert to the current code:**

```bash
git pull origin main
```

```bash
git reset --hard origin/main # ONLY IF YOU WANT TO RESTORE THE GITHUB REPO'S FILES. THIS WILL REWRITE EVERYTHING
```

**Handling .env files correctly or any environment variable with secrets in them like tokens, API keys, etc.:**

First, create a .gitignore file in the directory of your project. In this example, I am using Ubuntu:

```bash
echo ".env" >> .gitignore  # echo creates a new text file with the ".env" content. .env represents the text you want to create the file with and .gitignore represents the text file name!
```

Then commit the .gitignore file and push:

```bash
git filter-branch --force --index-filter "git rm --cached --ignore-unmatch SECRETSFILENAME" --prune-empty --tag-name-filter cat -- --all
```

**ONLY DO THIS IF YOU WANT TO REMOVE AN ACCIDENTALLY ADDED PRIVATE FILE FROM THE HISTORY SO IT CANNOT BE RETRIEVED**
