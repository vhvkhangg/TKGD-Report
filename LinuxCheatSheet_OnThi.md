# Linux Cheat Sheet - Ôn Thi

  

## Mục tiêu ôn tập

  

Tài liệu này tóm tắt các lệnh Linux thường gặp trong đề thi, gồm:

  

- Tìm kiếm và lọc dữ liệu

- Xử lý văn bản

- Quản lý tiến trình

- File, permission, inode, hard link, soft link

- Nén, backup, kiểm tra dung lượng

- Cron job

- Service và log

- Pipeline thực tế

- Git cơ bản

- Bảo mật và giám sát hệ thống

  

---

  

# 1. Tìm kiếm và lọc

  

## `find`

  

**Chức năng:**  

Tìm file hoặc thư mục theo tên, loại, kích thước, thời gian chỉnh sửa,...

  

**Cú pháp cơ bản:**

  

```bash

find <đường_dẫn> <điều_kiện>

```

  

**Ví dụ:**

  

Tìm tất cả file `.py` trong thư mục hiện tại:

  

```bash

find . -name "*.py"

```

  

Tìm không phân biệt hoa thường:

  

```bash

find . -iname "*.PY"

```

  

Tìm file thường:

  

```bash

find . -type f

```

  

Tìm thư mục:

  

```bash

find . -type d

```

  

Tìm file lớn hơn 100MB:

  

```bash

find . -size +100M

```

  

Tìm file được sửa trong 7 ngày gần đây:

  

```bash

find . -mtime -7

```

  

Tìm file `.log` rồi xóa:

  

```bash

find . -name "*.log" -delete

```

  

---

  

## `grep`

  

**Chức năng:**  

Tìm dòng chứa chuỗi hoặc pattern trong file hoặc output của lệnh khác.

  

**Ví dụ:**

  

Tìm chữ `error` trong file log:

  

```bash

grep "error" app.log

```

  

Không phân biệt hoa thường:

  

```bash

grep -i "error" app.log

```

  

Hiển thị số dòng:

  

```bash

grep -n "error" app.log

```

  

Đếm số dòng khớp:

  

```bash

grep -c "error" app.log

```

  

Tìm ngược, loại bỏ dòng chứa `INFO`:

  

```bash

grep -v "INFO" app.log

```

  

Tìm đệ quy trong thư mục hiện tại:

  

```bash

grep -r "database" .

```

  

Tìm process nginx:

  

```bash

ps aux | grep nginx

```

  

---

  

## `egrep`

  

**Chức năng:**  

Tìm kiếm bằng regular expression mở rộng. Tương đương gần giống `grep -E`.

  

**Ví dụ:**

  

Tìm dòng chứa `error` hoặc `warning`:

  

```bash

egrep "error|warning" app.log

```

  

Hoặc:

  

```bash

grep -E "error|warning" app.log

```

  

---

  

## `wc`

  

**Chức năng:**  

Đếm số dòng, số từ, số byte/ký tự.

  

**Ví dụ:**

  

Đếm số dòng:

  

```bash

wc -l file.txt

```

  

Đếm số từ:

  

```bash

wc -w file.txt

```

  

Đếm số byte:

  

```bash

wc -c file.txt

```

  

Đếm số file Python tìm được:

  

```bash

find . -name "*.py" | wc -l

```

  

---

  

## `xargs`

  

**Chức năng:**  

Nhận output từ lệnh trước và biến nó thành tham số cho lệnh sau.

  

**Ví dụ:**

  

Tìm file `.log` rồi xóa:

  

```bash

find . -name "*.log" | xargs rm

```

  

Tìm file `.txt` rồi hiển thị nội dung:

  

```bash

find . -name "*.txt" | xargs cat

```

  

Tìm file `.py` rồi grep chữ `def`:

  

```bash

find . -name "*.py" | xargs grep "def "

```

  

---

  

# 2. Xử lý văn bản

  

## `sort`

  

**Chức năng:**  

Sắp xếp các dòng văn bản.

  

**Ví dụ:**

  

Sắp xếp alphabet:

  

```bash

sort names.txt

```

  

Sắp xếp số tăng dần:

  

```bash

sort -n numbers.txt

```

  

Sắp xếp số giảm dần:

  

```bash

sort -nr numbers.txt

```

  

Sắp xếp theo cột thứ 3:

  

```bash

sort -k3 file.txt

```

  

Sắp xếp process theo CPU giảm dần:

  

```bash

ps aux | sort -k3 -nr

```

  

---

  

## `uniq`

  

**Chức năng:**  

Loại bỏ các dòng trùng nhau liên tiếp.

  

**Lưu ý:**  

Thường dùng cùng `sort`.

  

**Ví dụ:**

  

```bash

sort file.txt | uniq

```

  

Đếm số lần xuất hiện:

  

```bash

sort file.txt | uniq -c

```

  

---

  

## `cut`

  

**Chức năng:**  

Cắt/lấy một phần dữ liệu theo cột hoặc ký tự.

  

**Ví dụ:**

  

Lấy username trong `/etc/passwd`:

  

```bash

cut -d ":" -f1 /etc/passwd

```

  

Lấy UID:

  

```bash

cut -d ":" -f3 /etc/passwd

```

  

Trong đó:

  

- `-d ":"`: dùng dấu `:` làm dấu phân cách

- `-f1`: lấy cột 1

  

---

  

## `awk`

  

**Chức năng:**  

Xử lý text theo cột, mạnh hơn `cut`.

  

**Ví dụ:**

  

In cột 1:

  

```bash

awk '{print $1}' file.txt

```

  

In cột 1 và cột 2:

  

```bash

awk '{print $1, $2}' file.txt

```

  

In user và CPU từ `ps aux`:

  

```bash

ps aux | awk '{print $1, $3, $11}'

```

  

Tính tổng cột 1:

  

```bash

awk '{sum += $1} END {print sum}' numbers.txt

```

  

---

  

## `sed`

  

**Chức năng:**  

Xử lý và thay thế văn bản theo dòng.

  

**Ví dụ:**

  

Thay `error` thành `warning`:

  

```bash

sed 's/error/warning/g' log.txt

```

  

Thay lần đầu tiên trong mỗi dòng:

  

```bash

sed 's/error/warning/' log.txt

```

  

Xóa dòng chứa `DEBUG`:

  

```bash

sed '/DEBUG/d' log.txt

```

  

In dòng 1 đến dòng 5:

  

```bash

sed -n '1,5p' file.txt

```

  

---

  

# 3. Tiến trình - Process

  

## `ps`

  

**Chức năng:**  

Hiển thị các process đang chạy.

  

**Ví dụ:**

  

Xem tất cả process:

  

```bash

ps aux

```

  

Ý nghĩa một số cột:

  

- `USER`: user chạy process

- `PID`: mã tiến trình

- `%CPU`: CPU đang dùng

- `%MEM`: RAM đang dùng

- `COMMAND`: lệnh/process

  

Tìm process nginx:

  

```bash

ps aux | grep nginx

```

  

Top 5 process dùng CPU cao nhất:

  

```bash

ps aux | sort -k3 -nr | head -5

```

  

Top 5 process dùng RAM cao nhất:

  

```bash

ps aux | sort -k4 -nr | head -5

```

  

---

  

## `top`

  

**Chức năng:**  

Xem CPU, RAM và process theo thời gian thực.

  

```bash

top

```

  

Thường dùng để kiểm tra máy có bị quá tải CPU/RAM không.

  

---

  

## `htop`

  

**Chức năng:**  

Giống `top` nhưng giao diện dễ nhìn hơn.

  

```bash

htop

```

  

---

  

## `kill`

  

**Chức năng:**  

Gửi tín hiệu để dừng process.

  

Dừng process bình thường:

  

```bash

kill PID

```

  

Ép buộc dừng process:

  

```bash

kill -9 PID

```

  

Ví dụ:

  

```bash

kill -9 1234

```

  

---

  

## `nohup`

  

**Chức năng:**  

Chạy chương trình tiếp tục ngay cả khi logout SSH.

  

**Ví dụ:**

  

```bash

nohup python app.py &

```

  

Trong đó:

  

- `nohup`: không bị tắt khi logout

- `&`: chạy nền

  

---

  

## `jobs`

  

**Chức năng:**  

Xem các job đang chạy nền trong shell hiện tại.

  

```bash

jobs

```

  

---

  

## `bg`

  

**Chức năng:**  

Đưa job đang tạm dừng chạy tiếp ở background.

  

```bash

bg

```

  

---

  

## `fg`

  

**Chức năng:**  

Đưa job từ background về foreground.

  

```bash

fg

```

  

---

  

# 4. File, quyền, inode, link

  

## `ls -li`

  

**Chức năng:**  

Hiển thị inode number của file.

  

```bash

ls -li

```

  

Ví dụ output:

  

```text

123456 -rw-r--r-- 1 user user 100 file.txt

```

  

Trong đó `123456` là inode number.

  

---

  

## `ln`

  

**Chức năng:**  

Tạo hard link.

  

```bash

ln file_goc hard_link

```

  

Ví dụ:

  

```bash

ln a.txt b.txt

```

  

`a.txt` và `b.txt` cùng trỏ đến một inode.

  

---

  

## `ln -s`

  

**Chức năng:**  

Tạo symbolic link, còn gọi là soft link.

  

```bash

ln -s file_goc soft_link

```

  

Ví dụ:

  

```bash

ln -s a.txt shortcut.txt

```

  

`shortcut.txt` là file riêng, trỏ đến đường dẫn `a.txt`.

  

---

  

## Hard link vs Soft link

  

| Tiêu chí | Hard link | Soft link |

|---|---|---|

| Inode | Cùng inode với file gốc | Có inode riêng |

| Filesystem | Thường chỉ trong cùng filesystem | Có thể trỏ sang filesystem khác |

| Khi xóa file gốc | Dữ liệu vẫn còn nếu còn hard link | Link bị gãy |

| Bản chất | Tên khác của cùng file | Shortcut chứa đường dẫn |

  

---

  

## `chmod`

  

**Chức năng:**  

Thay đổi quyền truy cập file/thư mục.

  

**Ví dụ:**

  

Cho phép file được thực thi:

  

```bash

chmod +x script.sh

```

  

Cấp quyền `755`:

  

```bash

chmod 755 script.sh

```

  

Ý nghĩa:

  

```text

7 = rwx

5 = r-x

5 = r-x

```

  

Tức là:

  

- Owner: đọc, ghi, chạy

- Group: đọc, chạy

- Others: đọc, chạy

  

Quyền `644`:

  

```bash

chmod 644 file.txt

```

  

Ý nghĩa:

  

- Owner: đọc, ghi

- Group: đọc

- Others: đọc

  

---

  

## `chown`

  

**Chức năng:**  

Đổi chủ sở hữu file/thư mục.

  

Đổi owner:

  

```bash

chown ubuntu file.txt

```

  

Đổi owner và group:

  

```bash

chown ubuntu:www-data file.txt

```

  

Đổi đệ quy cả thư mục:

  

```bash

chown -R ubuntu:www-data /var/www/html

```

  

---

  

## `umask`

  

**Chức năng:**  

Quy định quyền mặc định khi tạo file/thư mục mới.

  

Xem umask hiện tại:

  

```bash

umask

```

  

Ví dụ:

  

```bash

umask 022

```

  

Thường dẫn đến:

  

- File mới: `644`

- Thư mục mới: `755`

  

---

  

# 5. Nén và dung lượng

  

## `tar`

  

**Chức năng:**  

Đóng gói nhiều file/thư mục thành một file, thường kết hợp nén gzip.

  

Nén thư mục:

  

```bash

tar -czf backup.tar.gz project/

```

  

Giải nén:

  

```bash

tar -xzf backup.tar.gz

```

  

Xem nội dung file nén:

  

```bash

tar -tzf backup.tar.gz

```

  

Ý nghĩa option:

  

- `c`: create, tạo file nén

- `x`: extract, giải nén

- `z`: gzip

- `f`: file

- `t`: list nội dung

  

---

  

## `gzip`

  

**Chức năng:**  

Nén một file bằng gzip.

  

```bash

gzip file.txt

```

  

Kết quả:

  

```text

file.txt.gz

```

  

---

  

## `gunzip`

  

**Chức năng:**  

Giải nén file `.gz`.

  

```bash

gunzip file.txt.gz

```

  

---

  

## `du`

  

**Chức năng:**  

Xem dung lượng file/thư mục.

  

Dung lượng thư mục hiện tại:

  

```bash

du -sh .

```

  

Dung lượng từng thư mục/file con:

  

```bash

du -sh *

```

  

Sắp xếp thư mục theo dung lượng:

  

```bash

du -sh * | sort -h

```

  

---

  

## `df`

  

**Chức năng:**  

Xem dung lượng ổ đĩa/filesystem.

  

```bash

df -h

```

  

Ý nghĩa:

  

- `Size`: tổng dung lượng

- `Used`: đã dùng

- `Avail`: còn trống

- `Use%`: phần trăm đã dùng

  

---

  

# 6. Cron

  

## `crontab`

  

**Chức năng:**  

Lập lịch chạy lệnh/script tự động.

  

Mở file cron:

  

```bash

crontab -e

```

  

Xem cron hiện tại:

  

```bash

crontab -l

```

  

Xóa cron hiện tại:

  

```bash

crontab -r

```

  

Cấu trúc cron:

  

```text

* * * * * command

| | | | |

| | | | +-- thứ trong tuần

| | | +---- tháng

| | +------ ngày trong tháng

| +-------- giờ

+---------- phút

```

  

Ví dụ chạy backup mỗi ngày lúc 2h sáng:

  

```bash

0 2 * * * /home/user/backup.sh

```

  

Chạy mỗi 5 phút:

  

```bash

*/5 * * * * /home/user/check.sh

```

  

---

  

# 7. Service và log

  

## `systemctl`

  

**Chức năng:**  

Quản lý service trên Linux dùng systemd.

  

Xem trạng thái:

  

```bash

systemctl status nginx

```

  

Khởi động service:

  

```bash

systemctl start nginx

```

  

Dừng service:

  

```bash

systemctl stop nginx

```

  

Khởi động lại:

  

```bash

systemctl restart nginx

```

  

Cho service tự chạy khi boot:

  

```bash

systemctl enable nginx

```

  

Tắt tự chạy khi boot:

  

```bash

systemctl disable nginx

```

  

---

  

## `journalctl`

  

**Chức năng:**  

Xem log của hệ thống hoặc service.

  

Xem log nginx:

  

```bash

journalctl -u nginx

```

  

Xem log realtime:

  

```bash

journalctl -u nginx -f

```

  

Xem log hôm nay:

  

```bash

journalctl --since today

```

  

Xem 50 dòng cuối:

  

```bash

journalctl -u nginx -n 50

```

  

---

  

## `tail`

  

**Chức năng:**  

Xem các dòng cuối của file.

  

Xem 10 dòng cuối:

  

```bash

tail error.log

```

  

Xem 100 dòng cuối:

  

```bash

tail -n 100 error.log

```

  

Theo dõi realtime:

  

```bash

tail -f error.log

```

  

Ví dụ debug nginx:

  

```bash

tail -f /var/log/nginx/error.log

```

  

---

  

# 8. Network và monitoring

  

## `ss`

  

**Chức năng:**  

Xem socket, port, kết nối mạng.

  

Xem port đang listen:

  

```bash

ss -tulpn

```

  

Trong đó:

  

- `t`: TCP

- `u`: UDP

- `l`: listening

- `p`: process

- `n`: hiển thị số, không resolve tên

  

Tìm port 80:

  

```bash

ss -tulpn | grep 80

```

  

---

  

## `netstat`

  

**Chức năng:**  

Xem kết nối mạng và port. Cũ hơn `ss` nhưng vẫn hay gặp.

  

```bash

netstat -tulpn

```

  

---

  

# 9. Pipeline

  

## Pipeline là gì?

  

Pipeline `|` là cơ chế lấy output của lệnh bên trái làm input cho lệnh bên phải.

  

Ví dụ:

  

```bash

ps aux | grep nginx

```

  

Nghĩa là:

  

```text

ps aux tạo danh sách process

grep nginx lọc dòng chứa nginx

```

  

---

  

## Ví dụ pipeline hay ra thi

  

Tìm process nginx:

  

```bash

ps aux | grep nginx

```

  

Top 5 process dùng CPU cao nhất:

  

```bash

ps aux | sort -k3 -nr | head -5

```

  

Top 5 process dùng RAM cao nhất:

  

```bash

ps aux | sort -k4 -nr | head -5

```

  

Tìm file `.py`, lọc dòng định nghĩa hàm:

  

```bash

find . -name "*.py" | xargs grep "^def "

```

  

Đếm số hàm Python:

  

```bash

find . -name "*.py" | xargs grep "^def " | wc -l

```

  

Lọc log lỗi không phân biệt hoa thường:

  

```bash

grep -i "error" app.log

```

  

Lọc log lỗi realtime:

  

```bash

tail -f app.log | grep -i "error"

```

  

---

  

# 10. Git cơ bản

  

## `git clone`

  

**Chức năng:**  

Tải repository từ remote về máy.

  

```bash

git clone <url>

```

  

---

  

## `git fetch`

  

**Chức năng:**  

Tải thay đổi từ remote về nhưng chưa merge vào nhánh hiện tại.

  

```bash

git fetch origin

```

  

---

  

## `git pull`

  

**Chức năng:**  

Tải thay đổi từ remote và merge/rebase vào nhánh hiện tại.

  

```bash

git pull

```

  

Ghi nhớ:

  

```text

git pull = git fetch + git merge

```

  

---

  

## Branch feature

  

Tạo nhánh mới:

  

```bash

git checkout -b feature/login

```

  

Chuyển nhánh:

  

```bash

git checkout main

```

  

---

  

## Merge

  

**Chức năng:**  

Gộp commit từ nhánh khác vào nhánh hiện tại.

  

```bash

git merge feature/login

```

  

---

  

## Rebase

  

**Chức năng:**  

Đưa commit của nhánh hiện tại lên trên commit mới của nhánh khác, giúp lịch sử tuyến tính hơn.

  

```bash

git rebase main

```

  

**Lưu ý:**  

Không nên rebase nhánh đã push và nhiều người dùng chung vì rebase viết lại lịch sử commit.

  

---

  

# 11. Tình huống thực tế

  

## Kiểm tra nginx bị lỗi

  

```bash

systemctl status nginx

journalctl -u nginx -n 50

tail -f /var/log/nginx/error.log

systemctl restart nginx

```

  

---

  

## Tìm process dùng CPU cao

  

```bash

ps aux | sort -k3 -nr | head -5

```

  

---

  

## Tìm process dùng RAM cao

  

```bash

ps aux | sort -k4 -nr | head -5

```

  

---

  

## Kiểm tra ổ đĩa đầy

  

```bash

df -h

du -sh *

du -sh * | sort -h

```

  

---

  

## Backup thư mục hằng ngày

  

Tạo script backup:

  

```bash

tar -czf /backup/project.tar.gz /home/user/project/

```

  

Thêm vào cron:

  

```bash

crontab -e

```

  

```bash

0 2 * * * /home/user/backup.sh

```

  

---

  

## Kiểm tra port web server

  

```bash

ss -tulpn | grep 80

```

  

Hoặc:

  

```bash

netstat -tulpn | grep 80

```

  

---

  

# 12. Câu trả lời ngắn hay dùng khi thi

  

## Pipeline là gì?

  

Pipeline là cơ chế dùng dấu `|` để lấy output của lệnh trước làm input cho lệnh sau, giúp kết hợp nhiều lệnh như `ps`, `grep`, `sort`, `head`.

  

## Hard link khác soft link?

  

Hard link dùng chung inode với file gốc, xóa file gốc dữ liệu vẫn còn nếu còn hard link. Soft link có inode riêng và chỉ chứa đường dẫn, nếu file gốc bị xóa thì link bị gãy.

  

## `git fetch` khác `git pull`?

  

`git fetch` chỉ tải thay đổi từ remote về, chưa merge. `git pull` tải thay đổi và merge luôn vào nhánh hiện tại.

  

## `tail -f` dùng làm gì?

  

`tail -f` dùng để theo dõi log realtime, thường dùng khi debug service như nginx.

  

## `systemctl` dùng làm gì?

  

`systemctl` dùng để quản lý service như xem trạng thái, start, stop, restart service.

  

  
**