

# playing with commits

## Rebase explanation

[git rebase](http://gitready.com/advanced/2009/02/10/squashing-commits-with-rebase.html)

[another one](https://www.atlassian.com/git/tutorials/merging-vs-rebasing)

## reset last commit 

[answer form sof](https://stackoverflow.com/questions/927358/how-to-undo-the-last-commits-in-git)


### get list of conflicting files
`git diff --name-only --diff-filter=U`

### get their changes during merge
 `git pull -X theirs`

after git pull 
`git checkout --theirs path/to/file`

### get a single file from git stash

[answer from sof](https://stackoverflow.com/questions/1105253/how-would-i-extract-a-single-file-or-changes-to-a-file-from-a-git-stash)

### merge branch without commiting
git merge branch-name --no-commit --no-ff

