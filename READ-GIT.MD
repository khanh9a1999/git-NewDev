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

# push cần làm sao để fast-forward tức là k có xung đột

# amend 
  - ghi đè nội dung commit , còn k muốn thêm commit mà sử dụng commit trc thì --no-edit
  - thêm nội dung commit vào cuooiss commit trước 
  - ko tạo ra thêm commit mới tránh nhiều commit or chỉnh sửa bình luận commit ngay trước đó.

#revert commit <> git revert --abort, muốn đảo ngc lại thì revert lại thì sẽ về như ban đầu
- xóa commit đã công khai tức đã merge 1 cách an toàn
- hoàn tác lại tất cả các commit của 1 nhánh tính tử commit bạn điền đến commit mới nhất
- tạo ra 1 commit mới.
- undo 1 merge commit và có lịch sử hoàn tác

#reset
  - loại bỏ commit : HEAD - index - tree
  - git reset --soft HEAD~ (git reset 'HEAD@{1}'): thay đổi HEAd ko thay đổi index và tree thích hợp cho việc ta commit lại từ đầu or đổi tên commit, tiếp tục code thêm. vì sao lại ko thay đổi index và work tree, tức file vẫn được lưu trong index nếu thay đổi thì 1 phần file vẫn ở ngoài index, và trong tree thì k còn commit tức HEAD trở veeff commit trước đó và trong tree bao gồm commit trc đó và branch hiện tại. và ở trên HEAD hiện tại sẽ là 1 commit là local change đứng thay thế commit trước khi reset. đổi tên commit
  - git reset --fixed or git reset (default): nó tương tự nhu soft nhưng sẽ bỏ file change ra khỏi index tuwcss vùng trước khi commit, hữu ichs trong việc chúng ta muốn sửa đối trước khi chạy lại commit.
  - git reset --hard: coi như xóa cả commit khỏi HEAD index và tree, xóa cả nội dung đã thay đổi

#chery pick commit : trích xuất commit
  - sao chép commit ở branch  chỉ đinh sang branch hiện tại

#rebase -i HEAD~
  - khi sử dụng -i trong rebase có thể thực hienj thay đổi, kết hợp, xóa commit, thay thế
  - thêm file khi commit thiếu
  - gộp thành 1 commit cùng nghĩa
  - sửa lại nội dung commit
