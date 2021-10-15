# Git

## git workflow

![git-workflow3](https://github.com/miseon119/whylearn.github.io/blob/master/test/images/git-workflow-diagram3.png)

```console
# workspace -> staging
$ git add <file/dir>

# staging -> local repo
$ git commit -m "some info"

# local repo -> remote repo, local master to remote origin
$ git push origin master
```

```console
# workspace <- staging
$ git checkout -- <file>

# staging <- local repo
$ git reset HEAD <file>

# local repo <- remote repo
$ git clone <git_url>  
$ git fetch upstream master # 拉取远程代码到本地但不应用在当前分支
$ git pull upstream master   # 拉取远程代码到本地但应用在当前分支
$ git pull --rebase upstream master  # 如果平时使用rebase合并代码则加上
```

```console
# workspace <- local repo
$ git reset <commit>          # 本地仓库覆盖到工作区(保存回退文件内容修改)
$ git reset --mixed <commit>  # 本地仓库覆盖到工作区(保存回退文件内容修改)
$ git reset --soft <commit>   # 本地仓库覆盖到工作区(保留修改并加到暂存区)
$ git reset --hard <commit>   # 本地仓库覆盖到工作区(不保留修改直接删除掉)
```

### git user info

```console
$ git config --global user.name "your_name"
$ git config --global user.email "your_email"
$ git config --list
```


##  Git Basic Commands

**Commit**
```console
$ git commit -m "your note"
```

**Modify Commit Message**
```console
$ git commit -m “new message” - -amend
```

**Add Remote Repository**
```console
$ git remote add origin {remote repository Address}
```

**Add**
```console
$ git add .
```

**Push**
```console
$ git push origin {branch name}
```
eg. branch name is master or main.

**Initialize repo**
```console
$ git init
```

**fetch**

The **git fetch** command is used to download the contents from a remote repository. **git pull** directly changes your local working copy of a repository.

git서버에서 최신 코드 받아오기

```console
$ git fetch 
```

### branch

Check remote repo branch:
```console
$ git branch -r
```

create branch:
```console
$ git branch dev
```

move to branch:
```console
$ git checkout dev
```

create and move to branch:
```console
$ git checkout -b dev
```

delete branch:
```console
$ git branch -d dev
```

push branch:
```console
git push -u origin test
```
[reference](https://pks2974.medium.com/%EC%9E%90%EC%A3%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EA%B8%B0%EC%B4%88-git-%EB%AA%85%EB%A0%B9%EC%96%B4-%EC%A0%95%EB%A6%AC%ED%95%98%EA%B8%B0-533b3689db81)

### Diff

Compare two branch file
```console
$ git diff mybranch2 master -- myfile.py
```
or 
```console
$ git diff branch1:path/to/file branch2:path/to/file
```
Compare local/remote branches:
```console
$ git diff <local branch> <remote>/<remote branch>
```
e.g.
```console
$ git diff myfile.py origin/myfile.py
```

### Clone

Clone branch
```console
$ git clone -b <branch> <remote_repo>
```
