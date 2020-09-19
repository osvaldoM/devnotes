

# playing with commits

## Rebase explanation

[git rebase](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html)

[another one](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

[yet, another one](https://github.com/edx/edx-platform/wiki/How-to-Rebase-a-Pull-Request)

## reset last commit 

[answer form sof](https://stackoverflow.com/questions/927358/how-to-undo-the-last-commits-in-git)


### get list of conflicting files
    git diff --name-only --diff-filter=U

### get their changes during merge
     git pull -X theirs

### force remote changes into local repo(discard all local commits)
 _fetch from the default remote, origin_
    
    git fetch
 _reset your current branch (master) to origin's master_

    git reset --hard origin/master

### after git pull 

    git checkout --theirs path/to/file

### get a single file from git stash

[answer from sof](https://stackoverflow.com/questions/1105253/how-would-i-extract-a-single-file-or-changes-to-a-file-from-a-git-stash)

### checkout file from branch

    git checkout branch --path

### show history of file with diff

    git log -p -- path/to/file

### merge branch without commiting

    git merge branch-name --no-commit --no-ff


### find parent of branch
[answer from so](https://stackoverflow.com/a/42562318)

`git show-branch | grep '*' | grep -v "$(git rev-parse --abbrev-ref HEAD)" | head -n1 | sed 's/.*\[\(.*\)\].*/\1/' | sed 's/[\^~].*//'`

checkout file from branch
        git checkout <branch_name> -- <paths>

### delete branches already merged into master

        git checkout master
        git branch --merged | egrep -v "(^\*|master)" | xargs git branch -d 

### Set author of commit
        git commit --author="John Doe <john@doe.org>"
