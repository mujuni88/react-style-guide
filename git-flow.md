# Git Flow

This is our guide for contributing to SchoolStatus projects. These steps are based on the following [article](https://akrabat.com/the-beginners-guide-to-contributing-to-a-github-project/).

## Step 1: Setup a local copy on your computer

1. Fork project  
   ![](/assets/schoolstatus_sasha__super_secret_project_sasha_that_everyone_knows_about.png)

2. Clone forked project to your local machine. Use [ssh](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/) link. `$ git clone git@github.com:mujuni88/sasha.git`  
   ![](/assets/mujuni88_sasha__super_secret_project_sasha_that_everyone_knows_about.png)

3. `cd sasha`

4. Setup remote so that you can point to the original project to retrieve any new changes to your local copy.   
   `git remote add upstream git@github.com:schoolstatus/sasha.git`

## Step 2: Working on a feature

#### General rule of thumb:
> Fix the thing you are working on.

* Working on a bug in production?

  create a branch from master

```
$ git checkout master
$ git pull upstream master && git push origin master
$ git checkout -b hotfix/readme-update
```

* Working on a new feature?

  create a branch from dev

```
$ git checkout dev
$ git pull upstream dev && git push origin dev
$ git checkout -b feature/new-content
```
1. Make sure you are on the correct branch
`git checkout branch`
2. Sync `git pull` your local copy with upstream copy. Then `git push` syncs it to our forked copy. 
3. Create our new branch. prefix branch with `hotfix/` or `feature/`


