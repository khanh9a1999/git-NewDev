# xử lí conflict:

- git rebase

  - git pull origin develop
  - git checkout <branch đang làm việc>
  - git rebase develop
  - xử lí conflict
  - git add .
  - git rebase --continue
  - git push origin <branch đang làm việc> -f
    ====> trong trường hợp đang làm việc với code cũ ở nhánh hiện tại

  - git stash
  - thực hiện các bước trên
  - git stash apply

- git merge
  - git pull origin develop
  - git checkout <branch đang làm việc>
  - git merge origin/develop
  - git add .
  - git merge --continue
  - git push origin <branch đang làm việc> -f

# gộp commit

-
