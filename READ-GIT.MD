- remote respo -> index -> tree local repo
- HEAD đại diện con trỏ đang trỏ đến 1 branch nào đó, nếu đang có 1 commit cụ thể thì nó trỏ đến commit đó
  + kiểm tra HEAD đang trỏ branch nào: git rev-parse --abbrev-ref HEAD
  + trỏ commit: git log -n 1 HEAD


# xử lí conflict:

- git rebase: nó không tạo ra commit mơi mà sẽ move các commit ở branch hiện tại lên trên nhánh khác và sau đó kết hợp lại sự thay đổi ở nhánh khác sang nhánh hiện tại, keesst quả là lịch sử commit sẽ được sắp xếp theo thứ tự mới. các commit của nhánh hiện tại sẽ được đặt lên trên các nhánh khác. giảm commit k cần thiết, tuy nhiên việc tái cấu trucs lịch sử commit sẽ gây ra nhiều xung đột và cần cẩn thận. Git rebase do việc mang sang nhánh đich nên HEAD nằm ở nhánh ddichss tức là main.

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

- git merge: tạo ra một commit mới trên branch hiện tại bao gồm sư thay đổi của cả 2 branch, commit mới sẽ có 2 commit cha là branch hiện tại và branch khác.điều này tạo ra lịch sử commit tương đối dễ đọc, nhưng đổi lại có thể tạo ra nhiều commit k cần thiết đặc biệt là khi phải thao tác liên tục việc tích hợp thường xuyên các thay đổi. điều này tạo ra 1 cây commit đa nhánh
  + khi thực hiện merge nếu commit trên nhánh đích không có sự thay đổi nào mà không co trên nhánh hiện tại thì sẽ thực hiện fast forward mà k tạo ra commit, tuy nhiên nếu co sự thay đổi thì sẽ thực hiện non-fast forward và tạo ra commit mới -> vậy khi nào lựa chọn thì tùy thuộc vaof mục đích
  + cách tạo ff thì ta đã biết r: trong trường hợp file thay đổi k ảnh hưởng branch đích thì sẽ là ff, còn có thay đổi xảy ra conflict thì ta fix bằng merge thì sẽ là non-ff , còn fix = rebase xong về main merge thì sẽ là ff
  + tạo 1 commit mới từ nhánh hiện tại nên HEAD sẽ là branch hiện tại.

  - git pull origin develop
  - git checkout <branch đang làm việc>
  - git merge origin/develop
  - git add .
  - git merge --continue
  - git push origin <branch đang làm việc> -f

# gộp commit

- git rebase -i HEAD~n

# pull kéo về và merge còn fetch kéo về và k merge, Branch này có thể checkout bằng tên là FETCH_HEAD.
