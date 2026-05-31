# Lab 1 OSD - Giải thích các lệnh, tùy chọn và ví dụ

---

## 0. Quy ước đọc lệnh

- `FILE`: tên file.
- `DIR`: tên thư mục.
- `SOURCE`: nguồn cần copy/move/link.
- `DEST`: đích.
- Nếu thao tác trong thư mục hệ thống như `/`, `/etc`, `/usr`, thường cần thêm `sudo`.

Ví dụ:

```bash
sudo mkdir -p /grandfather/father/son
```

# 1. Các cơ chế shell xuất hiện trong lab

## 1.1. Pipe `|`

**Công dụng:** Chuyển stdout của lệnh bên trái thành stdin của lệnh bên phải.


**Cú pháp:**

```bash
command1 | command2
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| Không có tùy chọn riêng | Đây là cơ chế của shell, không phải một chương trình độc lập. |


**Ví dụ:**

```bash
ls /etc | wc -l
```

**Giải thích ví dụ:** `ls /etc` liệt kê nội dung `/etc`, pipe chuyển kết quả sang `wc -l` để đếm số dòng.

---

## 1.2. Redirect stdout `>` và `>>`

**Công dụng:** Chuyển output bình thường của lệnh vào file.


**Cú pháp:**

```bash
command > file
command >> file
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| `>` | Ghi đè stdout vào file. |
| `>>` | Ghi thêm stdout vào cuối file. |


**Ví dụ:**

```bash
echo "line1" > abc.txt
echo "line2" >> abc.txt
```

**Giải thích ví dụ:** Dòng đầu tạo/ghi đè `abc.txt`; dòng sau ghi thêm vào cuối file.

---

## 1.3. Redirect stderr `2>`, `2>>`, `2>&1`

**Công dụng:** Điều hướng luồng lỗi stderr.


**Cú pháp:**

```bash
command 2> error.txt
command >> log.txt 2>&1
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| `2>` | Ghi đè stderr vào file. |
| `2>>` | Ghi thêm stderr vào file. |
| `2>&1` | Gộp stderr vào stdout. |


**Ví dụ:**

```bash
cat taptinkhongco 2> error.txt
```

**Giải thích ví dụ:** Vì file không tồn tại, lỗi của `cat` được ghi vào `error.txt` thay vì hiện trên màn hình.

---

## 1.4. Toán tử `&&`

**Công dụng:** Chỉ chạy lệnh sau nếu lệnh trước thành công, tức exit code bằng `0`.


**Cú pháp:**

```bash
command1 && command2
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| Không có tùy chọn riêng | Đây là toán tử điều khiển của shell. |


**Ví dụ:**

```bash
mkdir -p testdir && cd testdir
```

**Giải thích ví dụ:** Chỉ `cd testdir` nếu `mkdir -p testdir` thành công.

---

## 1.5. Dấu `;`

**Công dụng:** Ngăn cách nhiều lệnh trên cùng dòng; lệnh sau vẫn chạy dù lệnh trước lỗi.


**Cú pháp:**

```bash
command1 ; command2
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| Không có tùy chọn riêng | Đây là dấu phân tách lệnh của shell. |


**Ví dụ:**

```bash
cat taptinkhongco ; echo "Lenh echo van chay"
```

**Giải thích ví dụ:** `cat` lỗi nhưng `echo` vẫn chạy vì `;` không phụ thuộc kết quả lệnh trước.

---

## 1.6. Heredoc `<<EOF`

**Công dụng:** Truyền nhiều dòng nội dung vào stdin của một lệnh.


**Cú pháp:**

```bash
command <<'EOF'
noi dung
EOF
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| `<<EOF` | Mở khối heredoc. |
| `<<'EOF'` | Không mở rộng biến/ký tự đặc biệt trong nội dung heredoc. |


**Ví dụ:**

```bash
cat > demo.txt <<'EOF'
Dong 1
Dong 2
EOF
```

**Giải thích ví dụ:** Ghi hai dòng `Dong 1`, `Dong 2` vào file `demo.txt`.

---

## 1.7. Command substitution `$()`

**Công dụng:** Lấy output của một lệnh và chèn vào lệnh khác.


**Cú pháp:**

```bash
command "$(other_command)"
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| Không có tùy chọn riêng | Đây là cú pháp shell. |


**Ví dụ:**

```bash
echo "Hom nay la $(date +%F)"
```

**Giải thích ví dụ:** `date +%F` trả về ngày dạng `YYYY-MM-DD`, sau đó được chèn vào chuỗi của `echo`.

---

## 1.8. Biến shell

**Công dụng:** Lưu giá trị tạm thời để dùng lại trong terminal hoặc script.


**Cú pháp:**

```bash
NAME="value"
echo "$NAME"
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| Dấu nháy kép `"$VAR"` | Giữ nguyên giá trị có khoảng trắng/ký tự đặc biệt. |


**Ví dụ:**

```bash
SOURCE="/home/student/athena/class2/thegioimang.txt"
echo "$SOURCE"
```

**Giải thích ví dụ:** Gán đường dẫn vào biến `SOURCE`, sau đó in giá trị biến.

---

## 1.9. Vòng lặp `for`

**Công dụng:** Lặp qua danh sách giá trị trong shell script hoặc terminal.


**Cú pháp:**

```bash
for item in list; do
  command "$item"
done
```

**Tùy chọn/ký hiệu liên quan:**

| Mục | Ý nghĩa |
|---|---|
| `in list` | Danh sách giá trị cần lặp. |
| `do ... done` | Khối lệnh chạy cho từng giá trị. |


**Ví dụ:**

```bash
for d in athena/class1 athena/class2; do
  cp thegioimang.txt "$d/"
done
```

**Giải thích ví dụ:** Copy `thegioimang.txt` lần lượt vào `class1` và `class2`.

---

# 2. Các lệnh được dùng trong lab

## 2.1. `sudo`

**Công dụng:** Chạy lệnh với quyền của user khác, thường là `root`.


**Cú pháp:**

```bash
sudo [OPTION] COMMAND
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -u USER | Chạy lệnh dưới quyền user chỉ định. |
| -i | Mở login shell của root. |
| -s | Mở shell với quyền root. |
| -k | Xóa cache xác thực sudo hiện tại. |


**Ví dụ:**

```bash
sudo mkdir -p /grandfather/father/son
```

**Giải thích ví dụ:** Tạo thư mục dưới `/`, nơi tài khoản thường thường không có quyền ghi.

---

## 2.2. `su`

**Công dụng:** Chuyển sang user khác. Nếu không ghi user, mặc định chuyển sang `root`.


**Cú pháp:**

```bash
su [OPTION] [USER]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| - hoặc -l | Mở login shell của user đích. |
| -c COMMAND | Chạy một lệnh với user đích rồi thoát. |


**Ví dụ:**

```bash
su -
```

**Giải thích ví dụ:** Chuyển sang phiên đăng nhập của `root`, thường cần nhập mật khẩu root.

---

## 2.3. `whoami`

**Công dụng:** Hiển thị tên user hiện tại đang chạy lệnh.


**Cú pháp:**

```bash
whoami
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| --help | Xem trợ giúp. |
| --version | Xem phiên bản. |


**Ví dụ:**

```bash
whoami
```

**Giải thích ví dụ:** Cho biết bạn đang thao tác với user nào.

---

## 2.4. `who`

**Công dụng:** Hiển thị các user đang đăng nhập vào hệ thống.


**Cú pháp:**

```bash
who [OPTION]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -a | Hiển thị nhiều thông tin hơn. |
| -b | Hiển thị thời điểm boot hệ thống. |
| -q | Chỉ hiện tên user và số lượng user. |


**Ví dụ:**

```bash
who
```

**Giải thích ví dụ:** Kiểm tra các phiên đăng nhập hiện tại.

---

## 2.5. `date`

**Công dụng:** Hiển thị hoặc định dạng ngày giờ hệ thống.


**Cú pháp:**

```bash
date [OPTION] [+FORMAT]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| +%F | Ngày dạng `YYYY-MM-DD`. |
| +%T | Giờ dạng `HH:MM:SS`. |
| +%Y | Năm 4 chữ số. |
| +%m | Tháng. |
| +%d | Ngày. |
| -u | Hiển thị giờ UTC. |
| -d STRING | Hiển thị ngày giờ theo chuỗi mô tả. |


**Ví dụ:**

```bash
date +%F
```

**Giải thích ví dụ:** In ngày hiện tại theo dạng `YYYY-MM-DD`.

---

## 2.6. `cal`

**Công dụng:** Hiển thị lịch trong terminal.


**Cú pháp:**

```bash
cal [OPTION] [MONTH] [YEAR]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -y | Hiển thị lịch cả năm. |
| -3 | Hiển thị tháng trước, tháng hiện tại, tháng sau. |
| -m | Đặt thứ Hai là ngày đầu tuần, tùy bản Linux. |


**Ví dụ:**

```bash
cal 5 2026
```

**Giải thích ví dụ:** Hiển thị lịch tháng 5 năm 2026.

---

## 2.7. `pwd`

**Công dụng:** Hiển thị đường dẫn thư mục hiện tại.


**Cú pháp:**

```bash
pwd [OPTION]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -L | In đường dẫn logic, có thể giữ symlink trong path. |
| -P | In đường dẫn vật lý, resolve symlink. |


**Ví dụ:**

```bash
pwd -P
```

**Giải thích ví dụ:** In đường dẫn thật sau khi xử lý symbolic link.

---

## 2.8. `cd`

**Công dụng:** Chuyển thư mục làm việc hiện tại. Đây là shell builtin.


**Cú pháp:**

```bash
cd [OPTION] [DIR]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| không tham số | Về home directory. |
| ~ | Home directory. |
| .. | Thư mục cha. |
| - | Quay lại thư mục trước đó. |
| -P | Đi theo đường dẫn vật lý, resolve symlink. |
| -L | Đi theo đường dẫn logic. |


**Ví dụ:**

```bash
cd /etc/init.d
```

**Giải thích ví dụ:** Chuyển thư mục hiện tại sang `/etc/init.d`.

---

## 2.9. `timedatectl`

**Công dụng:** Xem và cấu hình ngày giờ, timezone trên hệ thống dùng systemd.


**Cú pháp:**

```bash
timedatectl [COMMAND]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| status | Xem trạng thái thời gian hiện tại. |
| list-timezones | Liệt kê timezone. |
| set-timezone TIMEZONE | Đặt timezone. |
| set-ntp true/false | Bật/tắt đồng bộ NTP. |


**Ví dụ:**

```bash
timedatectl
```

**Giải thích ví dụ:** Hiển thị giờ, timezone và trạng thái đồng bộ thời gian.

---

## 2.10. `ls`

**Công dụng:** Liệt kê file và thư mục.


**Cú pháp:**

```bash
ls [OPTION] [FILE_OR_DIR]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -l | Hiển thị dạng dài: quyền, owner, group, size, thời gian. |
| -a | Hiển thị cả file ẩn bắt đầu bằng `.`. |
| -i | Hiển thị inode number. |
| -h | Hiển thị size dễ đọc, thường dùng với `-l`. |
| -R | Liệt kê đệ quy thư mục con. |
| -F | Thêm ký hiệu phân loại như `/`, `*`, `@`. |
| -1 | Mỗi file một dòng. |
| -d | Hiển thị chính thư mục, không liệt kê bên trong. |


**Ví dụ:**

```bash
ls -ila /etc
```

**Giải thích ví dụ:** Hiển thị inode, thông tin chi tiết và cả file ẩn trong `/etc`.

---

## 2.11. `stat`

**Công dụng:** Hiển thị metadata chi tiết của file/thư mục.


**Cú pháp:**

```bash
stat [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -c FORMAT | Tự định dạng output. |
| -L | Theo symlink đến file đích thay vì xem chính symlink. |
| %n | Tên file khi dùng `-c`. |
| %i | Inode khi dùng `-c`. |
| %h | Link count khi dùng `-c`. |
| %A | Permission dạng chữ khi dùng `-c`. |
| %U | Owner khi dùng `-c`. |
| %G | Group khi dùng `-c`. |
| %F | Loại file khi dùng `-c`. |


**Ví dụ:**

```bash
stat -c '%n %i %h %A %U %G %F' rootfile.txt
```

**Giải thích ví dụ:** In tên file, inode, số link, quyền, owner, group và loại file.

---

## 2.12. `file`

**Công dụng:** Nhận diện kiểu file dựa trên nội dung và metadata.


**Cú pháp:**

```bash
file [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -b | Không in tên file ở đầu output. |
| -i | In MIME type. |
| -L | Theo symlink đến file đích. |


**Ví dụ:**

```bash
file /etc/passwd
```

**Giải thích ví dụ:** Cho biết `/etc/passwd` là file text hay kiểu khác.

---

## 2.13. `dircolors`

**Công dụng:** Hiển thị hoặc tạo cấu hình màu cho `ls`.


**Cú pháp:**

```bash
dircolors [OPTION]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -p | In cấu hình màu mặc định. |
| -b | Sinh lệnh cấu hình cho Bash. |
| -c | Sinh lệnh cấu hình cho C shell. |


**Ví dụ:**

```bash
dircolors -p | less
```

**Giải thích ví dụ:** Xem bảng cấu hình màu mặc định của `ls` theo từng trang.

---

## 2.14. `tree`

**Công dụng:** Hiển thị cây thư mục dạng trực quan.


**Cú pháp:**

```bash
tree [OPTION] [DIR]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -a | Hiển thị cả file ẩn. |
| -L N | Chỉ hiển thị đến độ sâu N. |
| -d | Chỉ hiển thị thư mục. |
| -f | Hiển thị đường dẫn đầy đủ. |


**Ví dụ:**

```bash
tree athena
```

**Giải thích ví dụ:** Hiển thị cấu trúc cây thư mục `athena`.

---

## 2.15. `mkdir`

**Công dụng:** Tạo thư mục.


**Cú pháp:**

```bash
mkdir [OPTION] DIR
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -p | Tạo cả thư mục cha nếu chưa tồn tại; không lỗi nếu đã tồn tại. |
| -v | Hiển thị thư mục được tạo. |
| -m MODE | Tạo thư mục với quyền chỉ định. |


**Ví dụ:**

```bash
mkdir -p athena/class2/basic_network
```

**Giải thích ví dụ:** Tạo toàn bộ đường dẫn nhiều cấp nếu chưa có.

---

## 2.16. `touch`

**Công dụng:** Tạo file rỗng hoặc cập nhật timestamp của file.


**Cú pháp:**

```bash
touch [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -a | Chỉ cập nhật access time. |
| -m | Chỉ cập nhật modification time. |
| -t TIME | Đặt thời gian theo dạng `[[CC]YY]MMDDhhmm[.ss]`. |
| -c | Không tạo file nếu file chưa tồn tại. |


**Ví dụ:**

```bash
touch empty1.txt empty2.txt
```

**Giải thích ví dụ:** Tạo hai file rỗng nếu chúng chưa tồn tại.

---

## 2.17. `cp`

**Công dụng:** Copy file hoặc thư mục.


**Cú pháp:**

```bash
cp [OPTION] SOURCE DEST
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -r hoặc -R | Copy thư mục đệ quy. |
| -a | Archive mode: giữ quyền, timestamp, symlink tốt hơn. |
| -i | Hỏi trước khi ghi đè. |
| -v | Hiển thị quá trình copy. |
| -p | Giữ permission, ownership, timestamp nếu có thể. |


**Ví dụ:**

```bash
cp thegioimang.txt athena/class1/
```

**Giải thích ví dụ:** Copy file `thegioimang.txt` vào thư mục `athena/class1/`.

---

## 2.18. `mv`

**Công dụng:** Di chuyển hoặc đổi tên file/thư mục.


**Cú pháp:**

```bash
mv [OPTION] SOURCE DEST
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -i | Hỏi trước khi ghi đè. |
| -n | Không ghi đè file đã tồn tại. |
| -v | Hiển thị thao tác đang thực hiện. |
| -f | Ghi đè không hỏi. |


**Ví dụ:**

```bash
mv athena/class4/ccna athena/class5/ccnp/
```

**Giải thích ví dụ:** Di chuyển thư mục `ccna` vào trong thư mục `ccnp`.

---

## 2.19. `rm`

**Công dụng:** Xóa file hoặc thư mục.


**Cú pháp:**

```bash
rm [OPTION] FILE_OR_DIR
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -r hoặc -R | Xóa thư mục và nội dung bên trong theo kiểu đệ quy. |
| -f | Ép xóa, không hỏi, bỏ qua lỗi file không tồn tại. |
| -i | Hỏi xác nhận trước khi xóa từng file. |
| -v | Hiển thị file đang bị xóa. |


**Ví dụ:**

```bash
rm athena/class1/thegioimang.txt
```

**Giải thích ví dụ:** Xóa file `thegioimang.txt` trong `athena/class1`.

---

## 2.20. `nano`

**Công dụng:** Trình soạn thảo văn bản trong terminal.


**Cú pháp:**

```bash
nano [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -l | Hiển thị số dòng. |
| -m | Bật hỗ trợ chuột, tùy bản nano. |
| -B | Tạo file backup trước khi lưu. |
| -w | Không tự động xuống dòng kiểu cũ, tùy bản nano. |


**Ví dụ:**

```bash
nano /home/student/backup-athena.sh
```

**Giải thích ví dụ:** Mở hoặc tạo file script `backup-athena.sh` để chỉnh sửa.

---

## 2.21. `chmod`

**Công dụng:** Thay đổi quyền truy cập file/thư mục.


**Cú pháp:**

```bash
chmod [OPTION] MODE FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| +x | Thêm quyền thực thi. |
| u+x | Thêm quyền thực thi cho owner. |
| 755 | Owner `rwx`, group `rx`, others `rx`. |
| 644 | Owner `rw`, group `r`, others `r`. |
| -R | Áp dụng đệ quy. |
| -v | Hiển thị thay đổi quyền. |


**Ví dụ:**

```bash
chmod +x /home/student/backup-athena.sh
```

**Giải thích ví dụ:** Cấp quyền thực thi cho script để cron có thể chạy.

---

## 2.22. `echo`

**Công dụng:** In chuỗi ra stdout.


**Cú pháp:**

```bash
echo [OPTION] STRING
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -n | Không tự thêm ký tự xuống dòng cuối output. |
| -e | Bật xử lý escape như `\n`, `\t`. |
| -E | Tắt xử lý escape, thường là mặc định. |


**Ví dụ:**

```bash
echo "Noi dung ban dau cua rootfile"
```

**Giải thích ví dụ:** In chuỗi ra màn hình; có thể kết hợp pipe/redirect để ghi file.

---

## 2.23. `tee`

**Công dụng:** Đọc từ stdin, ghi ra file và đồng thời in ra stdout.


**Cú pháp:**

```bash
tee [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -a | Append, ghi thêm vào cuối file. |
| -i | Bỏ qua tín hiệu interrupt. |


**Ví dụ:**

```bash
echo "Dong them" | tee -a demo.txt
```

**Giải thích ví dụ:** Ghi thêm `Dong them` vào cuối `demo.txt` và vẫn in ra màn hình.

---

## 2.24. `cat`

**Công dụng:** Xem, tạo, nối và xuất nội dung file.


**Cú pháp:**

```bash
cat [OPTION] [FILE]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -n | Đánh số tất cả dòng. |
| -b | Đánh số dòng không rỗng. |
| -s | Gộp nhiều dòng rỗng liên tiếp. |
| -A | Hiển thị ký tự đặc biệt như `$`, tab. |


**Ví dụ:**

```bash
cat /etc/passwd
```

**Giải thích ví dụ:** In toàn bộ nội dung `/etc/passwd` ra màn hình.

---

## 2.25. `more`

**Công dụng:** Xem nội dung file/output theo từng trang.


**Cú pháp:**

```bash
more [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -d | Hiển thị hướng dẫn phím bấm thân thiện hơn. |
| -s | Gộp nhiều dòng trắng liên tiếp. |
| -NUM | Hiển thị mỗi trang NUM dòng, ví dụ `-20`. |


**Ví dụ:**

```bash
more /etc/passwd
```

**Giải thích ví dụ:** Xem file `/etc/passwd` theo từng trang; bấm `q` để thoát.

---

## 2.26. `less`

**Công dụng:** Xem file/output theo trang, linh hoạt hơn `more`.


**Cú pháp:**

```bash
less [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -N | Hiển thị số dòng. |
| -S | Không tự wrap dòng dài. |
| -F | Tự thoát nếu nội dung ngắn hơn một màn hình. |
| +G | Mở file và nhảy đến cuối file. |


**Ví dụ:**

```bash
ls -la /usr/bin | less
```

**Giải thích ví dụ:** Xem output dài của `ls` theo trang; bấm `q` để thoát.

---

## 2.27. `head`

**Công dụng:** In phần đầu của file.


**Cú pháp:**

```bash
head [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -n N | In N dòng đầu. |
| -N | Dạng viết tắt, ví dụ `head -3 file`. |
| -c N | In N byte đầu. |


**Ví dụ:**

```bash
head -n 3 /mydir/mypasswords.txt
```

**Giải thích ví dụ:** In 3 dòng đầu của `mypasswords.txt`.

---

## 2.28. `tail`

**Công dụng:** In phần cuối của file.


**Cú pháp:**

```bash
tail [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -n N | In N dòng cuối. |
| -N | Dạng viết tắt, ví dụ `tail -3 file`. |
| -n +N | In từ dòng N đến hết file. |
| -c N | In N byte cuối. |
| -f | Theo dõi file đang được ghi thêm, hay dùng xem log. |


**Ví dụ:**

```bash
tail -n +4 /mydir/mypasswords.txt
```

**Giải thích ví dụ:** In từ dòng số 4 đến hết file.

---

## 2.29. `sed`

**Công dụng:** Stream editor: lọc, in, thay thế hoặc chỉnh sửa text theo dòng.


**Cú pháp:**

```bash
sed [OPTION] 'SCRIPT' FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -n | Không tự in toàn bộ dòng; chỉ in khi script yêu cầu. |
| '4,15p' | In dòng 4 đến dòng 15. |
| s/old/new/ | Thay chuỗi đầu tiên trên mỗi dòng. |
| s/old/new/g | Thay toàn bộ chuỗi khớp trên mỗi dòng. |
| -i | Sửa trực tiếp file, cần cẩn thận. |


**Ví dụ:**

```bash
sed -n '4,15p' /mydir/mypasswords.txt
```

**Giải thích ví dụ:** Chỉ in dòng 4 đến dòng 15 của file.

---

## 2.30. `wc`

**Công dụng:** Đếm dòng, từ, ký tự hoặc byte.


**Cú pháp:**

```bash
wc [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -l | Đếm số dòng. |
| -w | Đếm số từ. |
| -m | Đếm số ký tự. |
| -c | Đếm số byte. |
| -L | In độ dài dòng dài nhất. |


**Ví dụ:**

```bash
wc -l /mydir/mypasswords.txt
```

**Giải thích ví dụ:** Đếm số dòng trong file; với `/etc/passwd`, số dòng thường tương ứng số account.

---

## 2.31. `sort`

**Công dụng:** Sắp xếp các dòng text.


**Cú pháp:**

```bash
sort [OPTION] [FILE]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -r | Sắp xếp giảm dần. |
| -n | Sắp xếp theo số. |
| -f | Không phân biệt hoa thường. |
| -u | Loại dòng trùng sau khi sort. |
| -k FIELD | Sắp xếp theo cột/trường. |


**Ví dụ:**

```bash
ls /usr/bin | sort -r
```

**Giải thích ví dụ:** Liệt kê `/usr/bin` rồi sắp xếp giảm dần.

---

## 2.32. `grep`

**Công dụng:** Tìm dòng khớp với mẫu trong text.


**Cú pháp:**

```bash
grep [OPTION] PATTERN [FILE]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -i | Không phân biệt hoa thường. |
| -n | Hiển thị số dòng. |
| -r hoặc -R | Tìm đệ quy trong thư mục. |
| -v | In các dòng không khớp. |
| -E | Dùng extended regular expression. |
| -w | Khớp nguyên từ. |


**Ví dụ:**

```bash
ls / | grep a2
```

**Giải thích ví dụ:** Lọc output của `ls /`, chỉ in dòng có chứa `a2`.

---

## 2.33. `diff`

**Công dụng:** So sánh nội dung hai file.


**Cú pháp:**

```bash
diff [OPTION] FILE1 FILE2
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -s | Báo rõ nếu hai file giống nhau. |
| -u | Hiển thị unified diff. |
| -q | Chỉ báo có khác hay không. |
| -i | Không phân biệt hoa thường. |


**Ví dụ:**

```bash
diff -s rootfile.txt softfile.txt
```

**Giải thích ví dụ:** So sánh hai file và báo rõ nếu chúng giống nhau.

---

## 2.34. `find`

**Công dụng:** Tìm file/thư mục theo điều kiện.


**Cú pháp:**

```bash
find PATH [CONDITION] [ACTION]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -maxdepth N | Giới hạn độ sâu tìm kiếm. |
| -type f | Chỉ tìm file thường. |
| -type d | Chỉ tìm thư mục. |
| -type l | Chỉ tìm symbolic link. |
| -name PATTERN | Tìm theo tên. |
| -printf FORMAT | In output theo format. |
| -exec COMMAND {} \; | Chạy lệnh trên từng kết quả. |


**Ví dụ:**

```bash
find /etc -maxdepth 1 -type f | wc -l
```

**Giải thích ví dụ:** Tìm file thường ngay trong `/etc`, rồi đếm số lượng.

---

## 2.35. `which`

**Công dụng:** Cho biết đường dẫn đầy đủ của một lệnh trong `PATH`.


**Cú pháp:**

```bash
which [OPTION] COMMAND
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -a | Hiển thị tất cả đường dẫn khớp trong `PATH`. |


**Ví dụ:**

```bash
which tar
```

**Giải thích ví dụ:** Cho biết `tar` nằm ở đâu, ví dụ `/usr/bin/tar`; hữu ích khi viết cron.

---

## 2.36. `ln`

**Công dụng:** Tạo hard link hoặc symbolic link.


**Cú pháp:**

```bash
ln [OPTION] SOURCE LINK_NAME
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -s | Tạo symbolic link/soft link. |
| -f | Ghi đè link đích nếu đã tồn tại. |
| -n | Xử lý symlink tới thư mục như một file link. |
| -v | Hiển thị thao tác đang thực hiện. |


**Ví dụ:**

```bash
ln -s /grandfather/father/son/rootfile.txt /grandmother/mother/daughter/softfile.txt
```

**Giải thích ví dụ:** Tạo soft link `softfile.txt` trỏ tới `rootfile.txt`.

---

## 2.37. `readlink`

**Công dụng:** In đường dẫn mà symlink trỏ tới hoặc resolve đường dẫn tuyệt đối.


**Cú pháp:**

```bash
readlink [OPTION] FILE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -f | Resolve thành đường dẫn tuyệt đối, kể cả qua symlink. |
| -e | Resolve tuyệt đối nhưng yêu cầu mọi thành phần phải tồn tại. |
| -m | Resolve đường dẫn, cho phép một số thành phần chưa tồn tại. |


**Ví dụ:**

```bash
readlink -f athena/class2/thegioimang.txt
```

**Giải thích ví dụ:** In đường dẫn tuyệt đối của file.

---

## 2.38. `apt`

**Công dụng:** Công cụ quản lý package trên Debian/Ubuntu.


**Cú pháp:**

```bash
sudo apt COMMAND [PACKAGE]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| update | Cập nhật danh sách package. |
| install PACKAGE | Cài package. |
| remove PACKAGE | Gỡ package. |
| search KEYWORD | Tìm package. |
| show PACKAGE | Xem thông tin package. |
| -y | Tự động trả lời yes, cần cẩn thận. |


**Ví dụ:**

```bash
sudo apt install tree
```

**Giải thích ví dụ:** Cài package `tree` nếu hệ thống chưa có.

---

## 2.39. `systemctl`

**Công dụng:** Quản lý service trên hệ thống dùng systemd.


**Cú pháp:**

```bash
systemctl COMMAND SERVICE
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| status SERVICE | Xem trạng thái service. |
| start SERVICE | Khởi động service. |
| stop SERVICE | Dừng service. |
| restart SERVICE | Khởi động lại service. |
| enable SERVICE | Cho service tự chạy khi boot. |
| disable SERVICE | Tắt tự chạy khi boot. |
| is-active SERVICE | Kiểm tra service có active không. |


**Ví dụ:**

```bash
systemctl status cron
```

**Giải thích ví dụ:** Kiểm tra service `cron` có đang chạy không.

---

## 2.40. `tar`

**Công dụng:** Đóng gói nhiều file/thư mục thành archive; có thể kết hợp nén gzip/bzip2/xz.


**Cú pháp:**

```bash
tar [OPTION] -f ARCHIVE FILE_OR_DIR
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -c | Create: tạo archive mới. |
| -x | Extract: giải nén/giải đóng gói archive. |
| -t | List: xem nội dung archive. |
| -v | Verbose: hiển thị chi tiết. |
| -f FILE | Chỉ định tên archive; thường phải có. |
| -z | Dùng gzip, thường tạo `.tar.gz`. |
| -j | Dùng bzip2, thường tạo `.tar.bz2`. |
| -J | Dùng xz, thường tạo `.tar.xz`. |
| -C DIR | Đổi thư mục trước khi extract hoặc đóng gói. |
| -p | Giữ permission khi extract. |
| -r | Append file vào archive `.tar` chưa nén. |
| -u | Update file mới hơn vào archive `.tar` chưa nén. |
| --delete | Xóa file khỏi archive `.tar` chưa nén. |
| --exclude=PATTERN | Loại trừ file/thư mục. |
| --strip-components=N | Bỏ N cấp thư mục đầu khi extract. |
| -P | Giữ đường dẫn tuyệt đối; cần cẩn thận. |


**Ví dụ:**

```bash
tar -czvf athena.tar.gz athena/
```

**Giải thích ví dụ:** Tạo file `athena.tar.gz` từ thư mục `athena/` bằng gzip, có hiển thị chi tiết.

---

## 2.41. `crontab`

**Công dụng:** Xem, sửa, cài đặt hoặc xóa lịch cron của user.


**Cú pháp:**

```bash
crontab [OPTION]
```

**Tùy chọn/lệnh con/format thường dùng:**

| Mục | Ý nghĩa |
|---|---|
| -e | Mở crontab để chỉnh sửa. |
| -l | Liệt kê cron job hiện tại. |
| -r | Xóa toàn bộ crontab; nguy hiểm. |
| -i | Hỏi xác nhận khi dùng `-r`. |
| -u USER | Quản lý crontab của user khác, thường cần root. |


**Ví dụ:**

```bash
crontab -e
```

**Giải thích ví dụ:** Mở file crontab để thêm/sửa cron job.

---


# 4. Cú pháp cron job

Một dòng cron cơ bản có dạng:

```cron
* * * * * command
| | | | |
| | | | +--- thứ trong tuần, 0-7; 0 hoặc 7 là Chủ nhật
| | | +----- tháng, 1-12
| | +------- ngày trong tháng, 1-31
| +--------- giờ, 0-23
+----------- phút, 0-59
```

Ký hiệu thường dùng trong cron:

| Ký hiệu | Ý nghĩa | Ví dụ |
|---|---|---|
| `*` | Mọi giá trị | `* * * * *` = mỗi phút |
| `,` | Liệt kê nhiều giá trị | `0 8,13 * * *` = 8h và 13h |
| `-` | Khoảng giá trị | `0 8 * * 1-5` = 8h từ thứ Hai đến thứ Sáu |
| `/` | Bước nhảy | `*/10 * * * *` = mỗi 10 phút |

Shortcut cron:

| Shortcut | Ý nghĩa |
|---|---|
| `@reboot` | Chạy khi hệ thống khởi động |
| `@yearly` hoặc `@annually` | Mỗi năm một lần |
| `@monthly` | Mỗi tháng một lần |
| `@weekly` | Mỗi tuần một lần |
| `@daily` hoặc `@midnight` | Mỗi ngày một lần |
| `@hourly` | Mỗi giờ một lần |

Ví dụ cron job:

```cron
0 2 * * * /home/student/backup-athena.sh >> /home/student/backups/backup.log 2>&1
```

Giải thích:

- `0 2 * * *`: chạy lúc 02:00 mỗi ngày.
- `/home/student/backup-athena.sh`: script cần chạy.
- `>> backup.log`: ghi thêm output vào log.
- `2>&1`: gộp stderr vào stdout để lỗi cũng vào log.

Lưu ý khi viết cron:

- Nên dùng đường dẫn tuyệt đối, ví dụ `/usr/bin/tar` thay vì chỉ viết `tar`.
- Cron có môi trường tối giản, không giống terminal tương tác.
- Nên ghi log để dễ debug.
- Script cần quyền thực thi, ví dụ `chmod +x script.sh`.
- Nếu dùng `%` trực tiếp trong crontab, cần escape thành `\%`, ví dụ `date +\%F`.

