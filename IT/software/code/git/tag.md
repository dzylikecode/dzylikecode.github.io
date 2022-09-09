# 标签

## list

- `git tag`

  view all tags

- `git show <tag_name>`

  view the detail about specified name

## create

- `git tag <tag_name>`

  current head will be tagged

- `git tag <tag_name> <hash_id>`

- `git tag -a <tag_name> -m "explanation" <hash_id>`

## delete

- `git tag -d <tag_name>`

  delete local tag

- `git push origin --delete <tag_name>`

  delete remote tag

## push

- `git push origin <tag_name>`

- `git push origin --tag`

  push all tag
