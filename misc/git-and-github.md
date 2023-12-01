# Git and GitHub

## Git

* Version Control

#### Initialisation

```
git init
```

#### To connect local repository to github

```
git config --global user.name {username}
```

```
git config --global user.email {github email}
```

#### .gitignore

* File that defines folders/files that you don't want inside repository

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### Check current status of project

```
git status
```

#### Add files to staging area

* \-A: all files

```
git add -A
```

#### Moving files in staging area to repository

```
git commit -m '{message}'
```

#### Go back to latest commit

```
git reset --hard HEAD
```

#### Go back to previous commit

```
git log
```

```
git add reset --hard {log_id}
```

### Branching

#### Creating new branch

```
git branch {branch_name}
```

#### Switching to new branch

```
git checkout {branch_name}
```

#### Combining branches

* switch to master branch first

```
git merge {branch_name}
```



## GitHub

#### Connecting a github repository to an already created local repository

```
git remote add origin {github_repo_url}
```

#### Pushing to remote repository

* master branch if you want to send everything

```
git push origin {branch_name}
```

Normal steps:

* Add
* Commit
* Push

#### Pulling from remote repository

* conventionally used for subsequent updates

```
git pull origin {branch_name}
```

#### Cloning remote repository

* Used for initial update

```
git clone {github_repo_url}
```
