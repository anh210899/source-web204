- kiểm tra danh sách commit của nhánh đang đứng 
    git log --oneline // xem log, mỗi commit trên 1 dòng

- Thực hiện tách nhánh: Nhánh đc tách sẽ chứa toàn bộ commit của nhánh cha (toàn bộ code)
    git checkout tên nhánh (nếu nhánh đó đã đc tạo)
    git checkout -b tên nhánh (nếu nhánh chưa đc tạo) -> chỉ tạo ở local

Giả sử nhanh develope đang có chức năng -> người khác muốn thức hiện trên nhánh này
    git push web204 develope
    - develope -> tạo nhánh add_user
        <- (khi thực hiện xong chức năng, commit và push lên )

        Hoàn thiện code ở nhanh add_user -> git add "tên file" -> git commit -m "ND" -> git push 

        Sau khi hoàn thiện -> gộp code vào nhanh làm việc gôc (develope) : tạo pull request 
            so sánh nhánh mới với nhánh gốc (develope <- add_user) thấy ko có vấn đề gì -> Merge

git checkout -b "name"
git add .
git commit -m "name"
git push
git checkout develope - quay về nhánh develope

Sau khi hoàn thiện -> gộp code vào nhánh làm việc gốc (develop): tạo pull request
                So sánh nhánh mới với nhánh gốc (develop <- add_user) thấy k có vấn đề gì -> Merge

- Luôn để nhánh làm việc chính (develop) được update mới nhất so với develop trên github
    Quay về nhánh develop ở local (Không được làm việc trực tiếp ở trên nhánh này)
    git pull web204 develop

----------- tên nhánh đang đứng: công việc
1. master: tách nhánh làm việc chính develop (git checkout -b develop)
2. develop: tách nhánh add_user  (git checkout -b add_user)
3. add_user: thực hiện code chức năng (tạo file add_user.php và thay đổi nội dung)
4. add_user: commit -> push lên nhánh add_user trên github (git add . -> git commit -m "Add user" ->
        git push web204 add_user )
5. github: Tạo pull request so sánh develop <- add_user, merge code nhánh add_user trên github vào
    nhánh develop trên github (Bấm vào nút Compare & pull request -> Create -> Merge)
6. add_user: quay về nhánh develop (git checkout develop)
7. develop: pull code mới nhất trên nhánh develop của github về nhánh develop local
    (git pull web204 develop)
kiểm tra remote đang sử dụng đc đặt tên là gì
    " git remote -v " | tên bên trái là đùng để lưu code về hay đẩy lên

Vẫn ở nhánh develop nhưng lại lỡ làm việc (có sự thay đổi của file)
    Cách 1: Vẫn checkout sang nhánh mới bình thường
        git checkout -b 31_07_add_admin
        Vẫn add -> commit -> push như bình thường
    Cách 2: Chưa có gì

- Vừa commit xong, sau đó push code lên, tuy nhiên lại muốn sửa tiếp code ở nhánh đó
    Thực hiện thay đổi file
        "git add ."
    Git commit (commit để những phần thay đổi được đóng gói lại và đặt tên, thì mới push được lên)
    (Tuy nhiên phần code thêm này vẫn thuộc chức năng có tên là Add admin,
    không commit 1 lần nữa với tên giống hệt.
    Cần đưa phần code vừa thay đổi vào chung commit lúc nãy
        "git commit --amend --no-edit"
        Giải thích: --amend: đưa phần code mới vào chung commit cũ
                    --no-edit: không thay đổi tên commit trước đó
    )
    Sau khi đã push lên lần đầu, thì những lần sau sẽ cần push -f (--force ghi đè)
    *** Chú ý nếu thực hiện push -f thì bắt buộc cần git add . -> git commit --amend --n-edit
    (Nếu không thì phần code mới thêm sẽ đè bỏ phần code trước đó)
        "git push web204 HEAD -f" 
- Luôn cập nhật nhánh làm viêc chính (develope) mới nhất só với develop trên github
- git pull origin/web204 develop 
- bắt buộc phải đứng ở nhánh develop