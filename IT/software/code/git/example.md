# 案例

## 简单流程

- clone repository

  ```bash
  git clone <url_address>
  ```

- edit
- check status

  ```bash
  git status
  git log
  ```

- track file

  ```bash
  git add <file_name>
  ```

- commit

  ```bash
  git commit -m "a simple description"
  ```

- push

  ```bash
  git push
  ```

## 取消文件跟踪

失误 commit 了, 需要取消跟踪, 但是不想从本地删掉

- 从 index 中删除

  ```bash
  git rm --cached <file_name>
  ```

- 添加到 .gitignore

  ```bash
  echo <file_name> >> .gitignore
  ```

## 保留当前工作拉取远程

- 暂时保存

  ```bash
  git stash
  ```

- 拿出来

  ```bash
  git stash pop
  ```

## 添加上游仓库

- add remote

  `git remote add upstream <url>`

- fetch

  `git fetch upstream`

- merge

  `git merge upstream/master`
