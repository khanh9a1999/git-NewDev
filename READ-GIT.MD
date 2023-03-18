- remote respo -> index -> tree local repo
- HEAD đại diện con trỏ đang trỏ đến 1 branch nào đó, nếu đang có 1 commit cụ thể thì nó trỏ đến commit đó
  + kiểm tra HEAD đang trỏ branch nào: git rev-parse --abbrev-ref HEAD
  + trỏ commit: git log -n 1 HEAD


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

- git merge: tạo ra một commit mới trên branch hiện tại bao gồm sư thay đổi của cả 2 branch, commit mới sẽ có 2 commit cha là branch hiện tại và branch khác.điều này tạo ra lịch sử commit tương đối dễ đọc, nhưng đổi lại có thể tạo ra nhiều commit k cần thiết đặc biệt là khi phải thao tác liên tục việc tích hợp thường xuyên các thay đổi.
  - git pull origin develop
  - git checkout <branch đang làm việc>
  - git merge origin/develop
  - git add .
  - git merge --continue
  - git push origin <branch đang làm việc> -f

# gộp commit

-
