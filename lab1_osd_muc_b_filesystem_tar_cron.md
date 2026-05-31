# Lab 1 OSD - Mục B: Hệ thống tập tin và quản trị hệ thống tập tin

> Nội dung này trả lời **Bài 2 đến Bài 11** trong mục **B - Hệ thống tập tin và quản trị hệ thống tập tin** của file `Lab1-OSD.pdf`, kèm phần bổ sung về **lệnh `tar`**, **các tùy chọn của `tar`** và **cron job**.

---

## 0. Quy ước trước khi làm bài

Các lệnh trong đề dùng nhiều đường dẫn tuyệt đối như `/grandfather`, `/abc`, `/a`, `/athena`. Khi tạo thư mục trực tiếp dưới `/`, Linux thường yêu cầu quyền quản trị.

Nếu đang dùng tài khoản thường, thêm `sudo` trước các lệnh ghi/xóa ở thư mục hệ thống. Ví dụ:

```bash
sudo mkdir -p /grandfather/father/son
sudo rm -rf /grandfather
```

Nên làm trong máy ảo hoặc môi trường lab. Không nên xóa nhầm thư mục hệ thống thật.

Một số lệnh kiểm tra hữu ích:

```bash
pwd                 # xem thư mục hiện tại
whoami              # xem user hiện tại
ls -l               # xem chi tiết file/thư mục
ls -li              # xem inode + chi tiết file/thư mục
stat ten_file       # xem metadata chi tiết của file
```

---

# Bài 2 - Bài tập về soft link / symbolic link

## 2.1. Khái niệm cần nhớ

**Soft link**, còn gọi là **symbolic link** hoặc **symlink**, là một file đặc biệt chỉ chứa đường dẫn trỏ tới file/thư mục khác.

Đặc điểm chính:

- Soft link có **inode riêng** khác với file gốc.
- Soft link trỏ tới file gốc bằng **đường dẫn**.
- Xóa soft link thì file gốc không bị mất.
- Xóa file gốc thì soft link bị hỏng, thường gọi là **dangling symlink** hoặc **broken symlink**.
- Có thể tạo soft link tới file hoặc thư mục.
- Có thể tạo soft link khác filesystem/partition.

Cú pháp tạo soft link:

```bash
ln -s FILE_GOC FILE_LINK
```

Ví dụ:

```bash
ln -s /duong/dan/file_goc.txt /duong/dan/file_link.txt
```

---

## 2.a. Tạo đường dẫn và tập tin `/grandfather/father/son/rootfile.txt`

Tạo cây thư mục:

```bash
sudo mkdir -p /grandfather/father/son
```

Tạo file và nhập nội dung ban đầu:

```bash
echo "Noi dung ban dau cua rootfile" | sudo tee /grandfather/father/son/rootfile.txt
```

Kiểm tra nội dung:

```bash
cat /grandfather/father/son/rootfile.txt
```

Kết quả dự kiến:

```text
Noi dung ban dau cua rootfile
```

Giải thích:

- `mkdir -p` tạo toàn bộ cây thư mục cha nếu chưa tồn tại.
- `echo` in chuỗi ra màn hình chuẩn.
- `tee file` nhận dữ liệu từ stdin rồi ghi vào file.
- Vì file nằm dưới `/`, dùng `sudo tee` để có quyền ghi.

---

## 2.b. Tạo `/grandmother/mother/daughter/softfile.txt` là soft link đến `rootfile.txt`

Tạo thư mục chứa soft link:

```bash
sudo mkdir -p /grandmother/mother/daughter
```

Tạo symbolic link:

```bash
sudo ln -s /grandfather/father/son/rootfile.txt /grandmother/mother/daughter/softfile.txt
```

Kiểm tra link:

```bash
ls -l /grandmother/mother/daughter/softfile.txt
```

Kết quả dạng:

```text
lrwxrwxrwx 1 root root ... /grandmother/mother/daughter/softfile.txt -> /grandfather/father/son/rootfile.txt
```

Kiểm tra nội dung hai file:

```bash
cat /grandfather/father/son/rootfile.txt
cat /grandmother/mother/daughter/softfile.txt
```

Nhận xét:

- Nội dung của `softfile.txt` giống `rootfile.txt`.
- Thực chất khi đọc `softfile.txt`, hệ thống sẽ lần theo đường dẫn mà symlink đang trỏ tới rồi đọc nội dung của `rootfile.txt`.

---

## 2.c. Dùng `tee -a` nhập thêm nội dung cho `softfile.txt`

Thêm nội dung qua soft link:

```bash
echo "Dong them vao thong qua softfile" | sudo tee -a /grandmother/mother/daughter/softfile.txt
```

Kiểm tra file gốc:

```bash
cat /grandfather/father/son/rootfile.txt
```

Kết quả dự kiến:

```text
Noi dung ban dau cua rootfile
Dong them vao thong qua softfile
```

Nhận xét:

- `rootfile.txt` thay đổi.
- Lý do: `softfile.txt` chỉ là link trỏ tới `rootfile.txt`. Khi ghi vào soft link, Linux ghi vào file đích thật sự.
- Tùy chọn `-a` của `tee` nghĩa là **append**, tức ghi thêm vào cuối file thay vì ghi đè.

---

## 2.d. Dùng `tee -a` nhập thêm nội dung cho `rootfile.txt`

Thêm nội dung trực tiếp vào file gốc:

```bash
echo "Dong them vao truc tiep rootfile" | sudo tee -a /grandfather/father/son/rootfile.txt
```

Kiểm tra qua soft link:

```bash
cat /grandmother/mother/daughter/softfile.txt
```

Kết quả dự kiến:

```text
Noi dung ban dau cua rootfile
Dong them vao thong qua softfile
Dong them vao truc tiep rootfile
```

Nhận xét:

- `softfile.txt` cũng hiển thị nội dung mới.
- Lý do: soft link luôn đọc nội dung từ file đích `rootfile.txt`.

---

## 2.e. Kiểm tra link count, permission, owner và so sánh bằng `diff`

Dùng `ls -l`:

```bash
ls -l /grandfather/father/son/rootfile.txt
ls -l /grandmother/mother/daughter/softfile.txt
```

Dùng `ls -li` để xem inode:

```bash
ls -li /grandfather/father/son/rootfile.txt /grandmother/mother/daughter/softfile.txt
```

Dùng `stat`:

```bash
stat /grandfather/father/son/rootfile.txt
stat /grandmother/mother/daughter/softfile.txt
```

So sánh nội dung:

```bash
diff /grandfather/father/son/rootfile.txt /grandmother/mother/daughter/softfile.txt
```

Hoặc dùng:

```bash
diff -s /grandfather/father/son/rootfile.txt /grandmother/mother/daughter/softfile.txt
```

Nhận xét:

- `rootfile.txt` thường có dạng quyền như `-rw-r--r--`.
- `softfile.txt` thường có dạng `lrwxrwxrwx`, ký tự đầu là `l`, nghĩa là symbolic link.
- Link count của `rootfile.txt` vẫn thường là `1`, vì soft link **không làm tăng hard link count** của file gốc.
- `softfile.txt` có inode riêng, khác inode của `rootfile.txt`.
- `diff` không in gì nếu hai file giống nhau.
- `diff -s` sẽ báo rõ hai file giống nhau, ví dụ:

```text
Files /grandfather/father/son/rootfile.txt and /grandmother/mother/daughter/softfile.txt are identical
```

---

## 2.f. Tạo thêm `softfile2.txt`, xóa `softfile.txt`, rồi kiểm tra

Tạo soft link thứ hai:

```bash
sudo ln -s /grandfather/father/son/rootfile.txt /grandmother/mother/daughter/softfile2.txt
```

Xóa soft link thứ nhất:

```bash
sudo rm /grandmother/mother/daughter/softfile.txt
```

Kiểm tra tồn tại:

```bash
ls -l /grandfather/father/son/rootfile.txt
ls -l /grandmother/mother/daughter/
```

Kiểm tra nội dung:

```bash
cat /grandfather/father/son/rootfile.txt
cat /grandmother/mother/daughter/softfile.txt
cat /grandmother/mother/daughter/softfile2.txt
```

Kết quả dự kiến:

- `rootfile.txt` vẫn tồn tại và đọc được.
- `softfile.txt` không còn tồn tại, `cat` báo lỗi:

```text
No such file or directory
```

- `softfile2.txt` vẫn tồn tại và vẫn đọc được nội dung của `rootfile.txt`.

Nhận xét:

- Xóa một soft link chỉ xóa file link đó.
- File gốc không bị ảnh hưởng.
- Các soft link khác vẫn hoạt động bình thường nếu file gốc còn tồn tại.

---

## 2.g. Xóa `rootfile.txt`, rồi kiểm tra lại

Xóa file gốc:

```bash
sudo rm /grandfather/father/son/rootfile.txt
```

Kiểm tra:

```bash
ls -l /grandfather/father/son/
ls -l /grandmother/mother/daughter/
cat /grandmother/mother/daughter/softfile2.txt
```

Kết quả dự kiến:

- `rootfile.txt` không còn tồn tại.
- `softfile.txt` đã bị xóa từ bước trước.
- `softfile2.txt` vẫn còn là một symlink, nhưng bị hỏng vì file đích không còn.
- Khi đọc `softfile2.txt`, hệ thống báo lỗi:

```text
No such file or directory
```

Nhận xét:

- Soft link không chứa dữ liệu thật của file gốc.
- Khi file gốc bị xóa, soft link còn lại chỉ là đường dẫn trỏ đến một vị trí không còn file.

---

## 2.h. Trong Linux có bao nhiêu lệnh tạo symbolic link?

Trong quản trị Linux cơ bản, lệnh chuẩn để tạo symbolic link là:

```bash
ln -s
```

Hoặc dạng đầy đủ:

```bash
ln --symbolic
```

Ví dụ:

```bash
ln -s file_goc.txt file_link.txt
```

Ngoài ra, trên GNU/Linux có thể gặp tùy chọn `cp -s` hoặc `cp --symbolic-link` để tạo symbolic link thay vì copy nội dung. Tuy nhiên, trong bài lab về filesystem, lệnh chính cần nhớ là:

```bash
ln -s
```

---

# Bài 3 - Bài tập về hard link / physical link

## 3.1. Khái niệm cần nhớ

**Hard link** là nhiều tên file khác nhau cùng trỏ đến **cùng một inode** trên filesystem.

Đặc điểm chính:

- Hard link và file gốc có **cùng inode**.
- Hard link làm tăng **link count** của inode.
- Không có khái niệm “file gốc” thật sự ở cấp inode; mọi hard link đều bình đẳng.
- Xóa một tên file không làm mất dữ liệu nếu vẫn còn hard link khác trỏ đến inode đó.
- Không tạo hard link đến thư mục thông thường để tránh vòng lặp filesystem.
- Hard link thường không tạo được qua filesystem/partition khác nhau.

Cú pháp:

```bash
ln FILE_GOC FILE_HARDLINK
```

---

## 3.a. Tạo `rootdoc.txt`, `harddoc.txt`, `harddoc2.txt`

Tạo thư mục:

```bash
sudo mkdir -p /abc /def /hgi
```

Tạo file gốc:

```bash
echo "Noi dung ban dau cua rootdoc" | sudo tee /abc/rootdoc.txt
```

Tạo hard link:

```bash
sudo ln /abc/rootdoc.txt /def/harddoc.txt
sudo ln /abc/rootdoc.txt /hgi/harddoc2.txt
```

Kiểm tra inode và link count:

```bash
ls -li /abc/rootdoc.txt /def/harddoc.txt /hgi/harddoc2.txt
```

Kết quả dự kiến dạng:

```text
123456 -rw-r--r-- 3 root root ... /abc/rootdoc.txt
123456 -rw-r--r-- 3 root root ... /def/harddoc.txt
123456 -rw-r--r-- 3 root root ... /hgi/harddoc2.txt
```

Nhận xét:

- Ba file có cùng inode, ví dụ đều là `123456`.
- Link count là `3`, vì có 3 tên file cùng trỏ đến một inode.
- Quyền, owner, group, kích thước thường giống nhau vì thực chất là cùng một file ở mức inode.

---

## 3.b. Thực hiện tương tự Bài 2 và nhận xét

### 3.b.1. Kiểm tra nội dung các hard link

```bash
cat /abc/rootdoc.txt
cat /def/harddoc.txt
cat /hgi/harddoc2.txt
```

Nhận xét:

- Nội dung giống nhau vì cả ba tên file cùng trỏ đến cùng inode.

---

### 3.b.2. Ghi thêm nội dung vào `harddoc.txt`

```bash
echo "Dong them vao thong qua harddoc" | sudo tee -a /def/harddoc.txt
```

Kiểm tra lại:

```bash
cat /abc/rootdoc.txt
cat /def/harddoc.txt
cat /hgi/harddoc2.txt
```

Nhận xét:

- Cả ba file đều hiển thị nội dung mới.
- Lý do: ghi vào bất kỳ hard link nào cũng là ghi vào cùng inode.

---

### 3.b.3. Ghi thêm nội dung vào `rootdoc.txt`

```bash
echo "Dong them vao thong qua rootdoc" | sudo tee -a /abc/rootdoc.txt
```

Kiểm tra lại:

```bash
cat /abc/rootdoc.txt
cat /def/harddoc.txt
cat /hgi/harddoc2.txt
```

Nhận xét:

- `harddoc.txt` và `harddoc2.txt` cũng thay đổi theo.
- Không phải vì chúng “trỏ đường dẫn” đến `rootdoc.txt`, mà vì chúng cùng trỏ đến một inode.

---

### 3.b.4. So sánh permission, owner, inode, link count

```bash
ls -li /abc/rootdoc.txt /def/harddoc.txt /hgi/harddoc2.txt
stat /abc/rootdoc.txt
stat /def/harddoc.txt
stat /hgi/harddoc2.txt
```

Nhận xét:

- Inode giống nhau.
- Link count giống nhau và bằng số hard link hiện có.
- Permission, owner, group, size giống nhau.
- Khác với soft link, hard link không có ký tự đầu là `l` trong `ls -l`; nó vẫn hiện như file thường, ví dụ `-rw-r--r--`.

---

### 3.b.5. So sánh bằng `diff`

```bash
diff -s /abc/rootdoc.txt /def/harddoc.txt
diff -s /abc/rootdoc.txt /hgi/harddoc2.txt
```

Nhận xét:

- `diff -s` sẽ báo các file identical.
- Thực tế chúng là cùng nội dung của cùng một inode.

---

### 3.b.6. Xóa `harddoc.txt`, kiểm tra các file còn lại

```bash
sudo rm /def/harddoc.txt
ls -li /abc/rootdoc.txt /hgi/harddoc2.txt
cat /abc/rootdoc.txt
cat /hgi/harddoc2.txt
```

Nhận xét:

- `harddoc.txt` bị xóa.
- `rootdoc.txt` và `harddoc2.txt` vẫn tồn tại và vẫn đọc được.
- Link count giảm từ `3` xuống `2`.

---

### 3.b.7. Xóa `rootdoc.txt`, kiểm tra `harddoc2.txt`

```bash
sudo rm /abc/rootdoc.txt
ls -li /hgi/harddoc2.txt
cat /hgi/harddoc2.txt
```

Nhận xét:

- Dù tên `rootdoc.txt` bị xóa, dữ liệu vẫn còn vì `harddoc2.txt` vẫn trỏ đến inode đó.
- Link count giảm xuống `1`.
- Đây là điểm khác biệt rất quan trọng so với soft link.

---

## 3.2. So sánh nhanh soft link và hard link

| Tiêu chí | Soft link / symbolic link | Hard link / physical link |
|---|---|---|
| Lệnh tạo | `ln -s file_goc file_link` | `ln file_goc file_link` |
| Inode | Khác inode với file gốc | Cùng inode |
| Link count file gốc | Không tăng | Tăng |
| Khi xóa link | File gốc không bị ảnh hưởng | Dữ liệu còn nếu còn hard link khác |
| Khi xóa file gốc | Link bị hỏng | Dữ liệu vẫn còn qua hard link khác |
| Link tới thư mục | Có thể | Thường không cho phép |
| Khác filesystem | Có thể | Thường không thể |
| Dấu hiệu `ls -l` | Bắt đầu bằng `l`, ví dụ `lrwxrwxrwx` | Giống file thường, ví dụ `-rw-r--r--` |

---

# Bài 4 - Lệnh `cat`, `touch`, `more`, `less`

## 4.1. Lệnh `touch` dùng để làm gì?

`touch` có hai công dụng chính:

1. Tạo file rỗng nếu file chưa tồn tại.
2. Cập nhật thời gian truy cập và chỉnh sửa của file nếu file đã tồn tại.

Ví dụ tạo file rỗng:

```bash
touch file1.txt
ls -l file1.txt
```

Tạo nhiều file rỗng:

```bash
touch file2.txt file3.txt file4.txt
```

Cập nhật timestamp của file:

```bash
ls -l file1.txt
touch file1.txt
ls -l file1.txt
```

Một số tùy chọn thường dùng:

```bash
touch -a file1.txt              # chỉ cập nhật access time
touch -m file1.txt              # chỉ cập nhật modification time
touch -t 202605311230 file1.txt # đặt thời gian theo dạng YYYYMMDDhhmm
touch -c file_khong_tao.txt     # không tạo file nếu file chưa tồn tại
```

---

## 4.2. Lệnh `cat` có mấy công dụng?

`cat` thường có các công dụng sau:

### Công dụng 1: Xem nội dung file

```bash
cat file1.txt
```

### Công dụng 2: Tạo file bằng nhập từ bàn phím

```bash
cat > demo.txt
```

Sau đó nhập nội dung, kết thúc bằng `Ctrl + D`.

### Công dụng 3: Ghi đè nội dung file

```bash
echo "Dong moi" > demo.txt
cat demo.txt
```

Dấu `>` ghi đè toàn bộ nội dung cũ.

### Công dụng 4: Ghi thêm nội dung vào cuối file

```bash
echo "Dong them" >> demo.txt
cat demo.txt
```

Dấu `>>` ghi thêm vào cuối file.

### Công dụng 5: Nối nhiều file

```bash
cat file1.txt file2.txt > file_gop.txt
```

### Công dụng 6: Hiển thị số dòng

```bash
cat -n demo.txt
```

### Công dụng 7: Kết hợp pipe

```bash
cat demo.txt | grep "Dong"
```

Nhận xét:

- `cat` phù hợp để xem file ngắn.
- Với file dài, nên dùng `more` hoặc `less`.

---

## 4.3. Lệnh `more`

`more` dùng để xem nội dung file theo từng trang màn hình.

Ví dụ:

```bash
more /etc/passwd
```

Một số thao tác khi đang ở trong `more`:

| Phím | Chức năng |
|---|---|
| `Space` | Sang trang tiếp theo |
| `Enter` | Xuống một dòng |
| `q` | Thoát |
| `/chuoi` | Tìm kiếm chuỗi |

Ví dụ kết hợp pipe:

```bash
ls -l /etc | more
```

---

## 4.4. Lệnh `less`

`less` cũng dùng để xem file theo trang, nhưng linh hoạt hơn `more`.

Ví dụ:

```bash
less /etc/passwd
```

Một số thao tác trong `less`:

| Phím | Chức năng |
|---|---|
| `Space` | Sang trang tiếp theo |
| `b` | Quay lại trang trước |
| `Enter` | Xuống một dòng |
| `g` | Về đầu file |
| `G` | Đến cuối file |
| `/chuoi` | Tìm kiếm xuống dưới |
| `?chuoi` | Tìm kiếm lên trên |
| `n` | Kết quả tìm kiếm tiếp theo |
| `N` | Kết quả tìm kiếm trước đó |
| `q` | Thoát |

Ví dụ:

```bash
ls -la /usr/bin | less
```

So sánh nhanh:

| Lệnh | Đặc điểm |
|---|---|
| `cat` | In toàn bộ nội dung ra màn hình, phù hợp file ngắn |
| `more` | Xem từng trang, ít tính năng hơn |
| `less` | Xem từng trang, có thể cuộn lên/xuống, tìm kiếm tốt hơn |

---

# Bài 5 - Lệnh `wc` và `sort`

## 5.1. Hiển thị số lượng từ trong một file text

Tạo file mẫu:

```bash
cat > text.txt <<'EOF'
Linux la he dieu hanh ma nguon mo.
Hoc Linux giup quan tri he thong tot hon.
EOF
```

Đếm số từ:

```bash
wc -w text.txt
```

Chỉ in số lượng, không in tên file:

```bash
wc -w < text.txt
```

Giải thích:

- `wc` là word count.
- `-w` đếm số từ.

---

## 5.2. Hiển thị số dòng trong một file text

```bash
wc -l text.txt
```

Chỉ in số dòng:

```bash
wc -l < text.txt
```

Giải thích:

- `-l` đếm số dòng.

---

## 5.3. Hiển thị số ký tự trong một file text

Đếm số ký tự:

```bash
wc -m text.txt
```

Đếm số byte:

```bash
wc -c text.txt
```

Lưu ý:

- Với tiếng Anh không dấu, số byte và số ký tự thường giống nhau.
- Với tiếng Việt có dấu UTF-8, một ký tự có thể chiếm nhiều byte, nên `wc -m` và `wc -c` có thể khác nhau.

---

## 5.4. Hiển thị danh sách file trong `/usr/bin` theo thứ tự tăng dần / giảm dần

Tăng dần:

```bash
ls /usr/bin | sort
```

Giảm dần:

```bash
ls /usr/bin | sort -r
```

Sắp xếp không phân biệt hoa thường:

```bash
ls /usr/bin | sort -f
```

Sắp xếp theo kiểu số nếu tên có số:

```bash
ls /usr/bin | sort -n
```

---

## 5.5. Hiển thị số lượng file trong một thư mục cụ thể, ví dụ `/etc`

Cách 1: Đếm toàn bộ entry trong `/etc`:

```bash
ls -1 /etc | wc -l
```

Giải thích:

- `ls -1 /etc` in mỗi entry một dòng.
- `|` đưa output của `ls` sang input của `wc`.
- `wc -l` đếm số dòng.

Cách 2: Chỉ đếm file thường, không đếm thư mục:

```bash
find /etc -maxdepth 1 -type f | wc -l
```

Cách 3: Đếm thư mục con trong `/etc`:

```bash
find /etc -maxdepth 1 -type d | wc -l
```

Nhận xét:

- `ls -1 /etc | wc -l` đếm cả file, thư mục, symlink và các entry khác.
- `find /etc -maxdepth 1 -type f | wc -l` chỉ đếm file thường.

---

# Bài 6 - Lệnh `head`, `tail`

## 6.1. Copy `/etc/passwd` sang `/mydir/mypasswords.txt`

Xem file `/etc/passwd`:

```bash
cat /etc/passwd
```

Tạo thư mục `/mydir`:

```bash
sudo mkdir -p /mydir
```

Copy file:

```bash
sudo cp /etc/passwd /mydir/mypasswords.txt
```

Kiểm tra:

```bash
ls -l /mydir/mypasswords.txt
cat /mydir/mypasswords.txt
```

Giải thích:

- `/etc/passwd` chứa thông tin tài khoản user cục bộ trên hệ thống.
- Mỗi dòng thường tương ứng với một user.

---

## 6.2. Dùng `head` cho biết thông tin 3 user đầu

```bash
head -n 3 /mydir/mypasswords.txt
```

Hoặc viết ngắn:

```bash
head -3 /mydir/mypasswords.txt
```

Giải thích:

- `head` mặc định in 10 dòng đầu.
- `-n 3` chỉ in 3 dòng đầu.

---

## 6.3. Dùng `tail` cho biết thông tin 3 user cuối

```bash
tail -n 3 /mydir/mypasswords.txt
```

Hoặc:

```bash
tail -3 /mydir/mypasswords.txt
```

Giải thích:

- `tail` mặc định in 10 dòng cuối.
- `-n 3` chỉ in 3 dòng cuối.

---

## 6.4. Lệnh cho biết thông tin từ user thứ 4 đến hết

Dùng `tail` với cú pháp `+N`:

```bash
tail -n +4 /mydir/mypasswords.txt
```

Giải thích:

- `tail -n +4` in từ dòng thứ 4 đến hết file.
- Trong ngữ cảnh file `/etc/passwd`, dòng thứ 4 có thể xem là thông tin user thứ 4.

---

## 6.5. Cho biết thông tin user thứ 4 đến user thứ 15

Cách 1: Dùng `sed`:

```bash
sed -n '4,15p' /mydir/mypasswords.txt
```

Cách 2: Kết hợp `head` và `tail`:

```bash
head -n 15 /mydir/mypasswords.txt | tail -n 12
```

Giải thích cách 2:

- `head -n 15` lấy 15 dòng đầu.
- Trong 15 dòng đó, dòng 4 đến dòng 15 gồm 12 dòng.
- `tail -n 12` lấy 12 dòng cuối của nhóm 15 dòng đầu.

---

## 6.6. Dùng `wc` để cho biết tổng số user trong `mypasswords.txt`

```bash
wc -l /mydir/mypasswords.txt
```

Chỉ lấy số lượng:

```bash
wc -l < /mydir/mypasswords.txt
```

Nhận xét:

- Vì mỗi user trong `/etc/passwd` thường nằm trên một dòng, số dòng có thể xem là tổng số user/account trong file.

---

# Bài 7 - Kiểu file

## 7.1. Có bao nhiêu cách xem kiểu file?

Có nhiều cách xem kiểu file trong Linux. Các cách thường dùng nhất:

1. Dùng `ls -l` để xem ký tự đầu tiên của permission string.
2. Dùng `file` để nhận diện loại file theo nội dung/metadata.
3. Dùng `stat` để xem metadata chi tiết.
4. Dùng `find -type` hoặc `find -printf` để lọc/in loại file.
5. Dùng `ls -F` để thêm ký hiệu phân loại sau tên file.

---

## 7.2. Cách 1: Dùng `ls -l`

```bash
ls -l /etc | head
```

Ký tự đầu tiên cho biết loại file:

| Ký tự | Loại file |
|---|---|
| `-` | File thường |
| `d` | Thư mục |
| `l` | Symbolic link |
| `c` | Character device |
| `b` | Block device |
| `p` | Named pipe / FIFO |
| `s` | Socket |

Ví dụ:

```text
-rw-r--r-- 1 root root ... file.txt
```

Ký tự đầu là `-`, nghĩa là file thường.

```text
drwxr-xr-x 2 root root ... folder
```

Ký tự đầu là `d`, nghĩa là thư mục.

```text
lrwxrwxrwx 1 root root ... link -> target
```

Ký tự đầu là `l`, nghĩa là symbolic link.

---

## 7.3. Cách 2: Dùng lệnh `file`

```bash
file /etc/passwd
file /etc
file /bin/sh
```

Ví dụ kết quả:

```text
/etc/passwd: ASCII text
/etc: directory
/bin/sh: symbolic link to dash
```

Nhận xét:

- `file` cố gắng nhận diện loại file dựa trên nội dung và metadata.
- Rất hữu ích khi cần biết file là text, executable, image, archive, PDF, binary...

---

## 7.4. Cách 3: Dùng `stat`

```bash
stat /etc/passwd
stat /etc
```

Có thể in ngắn gọn loại file:

```bash
stat -c '%F %n' /etc/passwd /etc /bin/sh
```

Giải thích:

- `%F` in loại file.
- `%n` in tên file.

---

## 7.5. Cách 4: Dùng `find`

In loại file bằng ký hiệu:

```bash
find /etc -maxdepth 1 -printf '%y %p\n' | head
```

Một số ký hiệu của `find -printf '%y'`:

| Ký hiệu | Loại |
|---|---|
| `f` | File thường |
| `d` | Thư mục |
| `l` | Symbolic link |
| `b` | Block device |
| `c` | Character device |
| `p` | FIFO |
| `s` | Socket |

Lọc chỉ file thường:

```bash
find /etc -maxdepth 1 -type f
```

Lọc chỉ thư mục:

```bash
find /etc -maxdepth 1 -type d
```

Lọc chỉ symlink:

```bash
find /etc -maxdepth 1 -type l
```

---

## 7.6. Cách 5: Dùng `ls -F`

```bash
ls -F /etc | head
```

Một số ký hiệu:

| Ký hiệu | Ý nghĩa |
|---|---|
| `/` | Thư mục |
| `*` | File thực thi |
| `@` | Symbolic link |
| `|` | FIFO |
| `=` | Socket |

---

# Bài 8 - So sánh và giải thích kết quả

## 8.a. So sánh `&&` và `;`

### Nhóm lệnh 1

```bash
cat taptinkhongco && mkdir -p /a1/b1/c1 ; ls / | grep a1
```

Dự đoán kết quả:

- `cat taptinkhongco` lỗi vì file không tồn tại.
- Vì dùng `&&`, lệnh `mkdir -p /a1/b1/c1` **không được thực hiện**.
- Sau dấu `;`, lệnh `ls / | grep a1` vẫn được thực hiện.
- Nếu trước đó chưa có `/a1`, sẽ không thấy output `a1`.

Giải thích:

- `cmd1 && cmd2`: chỉ chạy `cmd2` nếu `cmd1` thành công, tức exit code bằng `0`.
- `cmd1 ; cmd2`: chạy `cmd2` bất kể `cmd1` thành công hay thất bại.

Kiểm tra:

```bash
ls -ld /a1
```

Nếu `/a1` chưa tồn tại, kết quả sẽ là lỗi:

```text
No such file or directory
```

### Nhóm lệnh 2

```bash
cat taptinkhongco ; mkdir -p /a2/b1/c1 ; ls / | grep a2
```

Dự đoán kết quả:

- `cat taptinkhongco` vẫn lỗi.
- Nhưng do dùng `;`, lệnh `mkdir -p /a2/b1/c1` vẫn chạy.
- Sau đó `ls / | grep a2` sẽ in ra:

```text
a2
```

Nhận xét:

- `&&` phụ thuộc vào trạng thái thành công/thất bại của lệnh trước.
- `;` chỉ dùng để ngăn cách lệnh, không kiểm tra lệnh trước có lỗi hay không.

---

## 8.b. So sánh `>` và `>>`

### Lệnh in ra màn hình

```bash
echo "line1"
```

Kết quả:

```text
line1
```

Lệnh này chỉ in ra stdout, không ghi vào file.

---

### Ghi đè bằng `>`

```bash
echo "line1" > abc.txt
echo "line2" > abc.txt
echo "line3" > abc.txt
cat abc.txt
```

Kết quả cuối cùng của `abc.txt`:

```text
line3
```

Giải thích:

- Dấu `>` chuyển stdout vào file và **ghi đè** nội dung cũ.
- Mỗi lần dùng `> abc.txt`, file bị thay bằng nội dung mới.
- Sau ba lệnh, nội dung chỉ còn `line3`.

---

### Ghi thêm bằng `>>`

```bash
echo "line1" > abc.txt
echo "line2" >> abc.txt
echo "line3" >> abc.txt
cat abc.txt
```

Kết quả:

```text
line1
line2
line3
```

Giải thích:

- Lệnh đầu dùng `>` để tạo mới/ghi đè file.
- Các lệnh sau dùng `>>` để append, tức ghi thêm vào cuối file.

---

## 8.c. So sánh redirect stdout và stderr

### Lệnh 1

```bash
cat taptinkhongco > abc1.txt
```

Dự đoán:

- Vì file `taptinkhongco` không tồn tại, `cat` sinh lỗi.
- Lỗi được in ra màn hình vì đó là stderr.
- `abc1.txt` được tạo mới hoặc bị truncate về rỗng, vì stdout bị redirect vào file nhưng `cat` không có stdout hợp lệ.

Kiểm tra:

```bash
cat abc1.txt
ls -l abc1.txt
```

---

### Lệnh 2

```bash
cat taptinkhongco 2> abc1.txt
```

Dự đoán:

- Lỗi không hiện trên màn hình.
- Lỗi được ghi vào `abc1.txt`.

Kiểm tra:

```bash
cat abc1.txt
```

Kết quả dạng:

```text
cat: taptinkhongco: No such file or directory
```

Giải thích:

| Cú pháp | Ý nghĩa |
|---|---|
| `>` hoặc `1>` | Redirect stdout |
| `2>` | Redirect stderr |
| `>>` | Append stdout |
| `2>>` | Append stderr |
| `2>&1` | Gộp stderr vào stdout |

Ví dụ redirect cả stdout và stderr:

```bash
cat taptinkhongco > abc1.txt 2>&1
```

---

# Bài 9 - Dự đoán kết quả lệnh `ls ~ | tee home.txt | cat`

Lệnh:

```bash
ls ~ | tee home.txt | cat
```

## Dự đoán kết quả

Lệnh này sẽ:

1. Liệt kê nội dung thư mục home của user hiện tại bằng `ls ~`.
2. Gửi danh sách đó qua pipe cho `tee home.txt`.
3. `tee home.txt` vừa ghi output vào file `home.txt`, vừa chuyển tiếp output sang pipe tiếp theo.
4. `cat` nhận output từ pipe và in ra màn hình.

Kết quả trên màn hình sẽ là danh sách file/thư mục trong home directory.

Đồng thời, file `home.txt` sẽ chứa cùng nội dung đó.

Kiểm tra:

```bash
cat home.txt
```

Lưu ý:

- `home.txt` được tạo trong **thư mục hiện tại**, không nhất thiết nằm trong `~`.
- Nếu muốn chắc chắn tạo trong home directory, dùng:

```bash
ls ~ | tee ~/home.txt | cat
```

Giải thích pipe:

```text
ls ~  --->  tee home.txt  --->  cat  ---> màn hình
              |
              +---- ghi vào file home.txt
```

---

# Bài 10 - Các lệnh về đường dẫn, `pwd`, `ls`, màu file và `mkdir`

## 10.1. Chuyển vào `/etc/init.d`, so sánh `pwd` và `pwd -P`

Chạy:

```bash
cd /etc/init.d
pwd
pwd -P
```

Giải thích:

- `pwd` thường in đường dẫn logic hiện tại.
- `pwd -P` in đường dẫn vật lý, tức đã resolve symbolic link.

Nếu `/etc/init.d` không đi qua symbolic link, hai kết quả giống nhau:

```text
/etc/init.d
/etc/init.d
```

Nếu đường dẫn hiện tại có symlink, ví dụ đi vào thư mục qua một link mềm, thì:

- `pwd` có thể hiển thị đường dẫn có symlink.
- `pwd -P` hiển thị đường dẫn thật sau khi resolve symlink.

Ví dụ minh họa:

```bash
mkdir -p /tmp/real_dir
ln -s /tmp/real_dir /tmp/link_dir
cd /tmp/link_dir
pwd
pwd -P
```

Kết quả có thể là:

```text
/tmp/link_dir
/tmp/real_dir
```

---

## 10.2. So sánh nhóm lệnh dùng `cd -P` và `cd -L`

### Nhóm 1

```bash
cd / && pwd && cd -P /etc/init.d && pwd && cd
```

Giải thích từng phần:

- `cd /`: chuyển về thư mục gốc.
- `pwd`: in `/`.
- `cd -P /etc/init.d`: chuyển vào `/etc/init.d` theo chế độ physical, resolve symlink.
- `pwd`: in đường dẫn hiện tại.
- `cd`: chuyển về home directory của user hiện tại.

Nếu `/etc/init.d` không phải symlink, kết quả chính sẽ là:

```text
/
/etc/init.d
```

Lệnh `cd` cuối không in gì, chỉ chuyển về home.

---

### Nhóm 2

```bash
cd / && pwd && cd -L /etc/init.d && pwd && cd ~
```

Giải thích từng phần:

- `cd /`: chuyển về thư mục gốc.
- `pwd`: in `/`.
- `cd -L /etc/init.d`: chuyển vào `/etc/init.d` theo chế độ logical, giữ đường dẫn logic nếu có symlink.
- `pwd`: in đường dẫn logic hiện tại.
- `cd ~`: chuyển về home directory.

So sánh:

| Lệnh | Ý nghĩa |
|---|---|
| `cd -P` | Đi theo đường dẫn vật lý, resolve symlink |
| `cd -L` | Đi theo đường dẫn logic, giữ symlink trong path nếu có |

Trong nhiều hệ thống, `/etc/init.d` là thư mục thật nên hai nhóm lệnh có thể cho kết quả giống nhau.

---

## 10.3. Chuyển vào thư mục `/etc`

```bash
cd /etc
pwd
```

Kết quả:

```text
/etc
```

---

## 10.4. So sánh `ls`, `ls -i`, `ls -l`, `ls -a`, `ls -ila`

Chạy trong `/etc`:

```bash
ls
ls -i
ls -l
ls -a
ls -ila
```

Giải thích:

| Lệnh | Ý nghĩa |
|---|---|
| `ls` | Liệt kê file/thư mục, không hiện file ẩn |
| `ls -i` | Liệt kê kèm inode number |
| `ls -l` | Liệt kê dạng dài: quyền, link count, owner, group, size, thời gian, tên |
| `ls -a` | Hiện tất cả, bao gồm file ẩn bắt đầu bằng `.` |
| `ls -ila` | Kết hợp `-i`, `-l`, `-a`: hiện inode + chi tiết + file ẩn |

Ví dụ một dòng của `ls -l`:

```text
-rw-r--r-- 1 root root 1234 May 31 10:00 passwd
```

Ý nghĩa:

| Thành phần | Ý nghĩa |
|---|---|
| `-rw-r--r--` | Loại file và quyền |
| `1` | Link count |
| `root` | Owner |
| `root` | Group |
| `1234` | Kích thước byte |
| `May 31 10:00` | Thời gian sửa đổi |
| `passwd` | Tên file |

---

## 10.5. Hiển thị kết xuất từng lệnh theo từng trang màn hình

Dùng `more`:

```bash
ls | more
ls -i | more
ls -l | more
ls -a | more
ls -ila | more
```

Dùng `less`:

```bash
ls | less
ls -i | less
ls -l | less
ls -a | less
ls -ila | less
```

Nhận xét:

- `more` và `less` giúp xem output dài theo từng trang.
- `less` tiện hơn vì có thể cuộn lên/xuống và tìm kiếm tốt hơn.

---

## 10.6. File có màu white, blue, green, cyan, orange là kiểu gì?

Màu sắc của `ls` phụ thuộc vào biến môi trường `LS_COLORS` và theme terminal. Có thể kiểm tra bằng:

```bash
echo $LS_COLORS
dircolors -p | less
```

Trên nhiều bản Linux thông dụng, quy ước thường gặp là:

| Màu | Kiểu thường gặp |
|---|---|
| White / trắng | File thường |
| Blue / xanh dương | Thư mục |
| Green / xanh lá | File thực thi |
| Cyan / xanh lơ | Symbolic link |
| Orange hoặc Yellow / cam-vàng | Thường là device file, FIFO, socket hoặc một nhóm đặc biệt tùy cấu hình màu |

Cách kiểm tra chính xác hơn là dùng:

```bash
ls -l ten_file
file ten_file
stat ten_file
```

Nhận xét:

- Không nên dựa hoàn toàn vào màu, vì màu có thể thay đổi theo cấu hình terminal.
- Cách chắc chắn hơn là xem ký tự đầu trong `ls -l` hoặc dùng `file`/`stat`.

---

## 10.7. Giải thích kết quả các lệnh `mkdir`

### Lệnh 1

```bash
mkdir /a/b/c/d/e/f/g/h
```

Nếu các thư mục cha `/a`, `/a/b`, `/a/b/c`... chưa tồn tại, lệnh sẽ lỗi:

```text
No such file or directory
```

Giải thích:

- `mkdir` mặc định chỉ tạo được thư mục cuối nếu thư mục cha đã tồn tại.
- Không có `-p`, Linux không tự tạo toàn bộ thư mục cha.

---

### Lệnh 2

```bash
mkdir /a /a/b /a/b/c
```

Kết quả:

- Tạo `/a` trước.
- Sau đó tạo `/a/b`.
- Sau đó tạo `/a/b/c`.

Lệnh có thể thành công vì các thư mục được liệt kê theo đúng thứ tự từ cha đến con.

Nếu `/a` đã tồn tại, lệnh có thể báo:

```text
File exists
```

---

### Lệnh 3

```bash
mkdir -p /a/b/c/d/e/f
```

Kết quả:

- Tạo toàn bộ thư mục cha còn thiếu.
- Không báo lỗi nếu thư mục đã tồn tại.

Giải thích:

- `-p` nghĩa là **parents**.
- Đây là tùy chọn nên dùng khi cần tạo cây thư mục nhiều cấp.

---

# Bài 11 - Tổng hợp thao tác Linux cơ bản

## 11.1. Login Linux và sử dụng các lệnh cơ bản

Sau khi đăng nhập Linux, có thể chạy các lệnh sau:

```bash
date
pwd
ls
who
su
cal
cat
more
head
tail
```

Giải thích:

| Lệnh | Công dụng |
|---|---|
| `date` | Hiển thị ngày giờ hệ thống |
| `pwd` | Hiển thị thư mục hiện tại |
| `ls` | Liệt kê file/thư mục |
| `who` | Hiển thị user đang đăng nhập |
| `su` | Chuyển user, thường dùng để chuyển sang root nếu biết mật khẩu |
| `cal` | Hiển thị lịch |
| `cat` | Xem/tạo/nối file |
| `more` | Xem file theo từng trang |
| `head` | Xem phần đầu file |
| `tail` | Xem phần cuối file |

Ví dụ:

```bash
date
pwd
ls -la
who
cal
head -n 5 /etc/passwd
tail -n 5 /etc/passwd
```

---

## 11.2. Dùng `cat` tạo file `thegioimang.txt`

Cách nhập trực tiếp bằng `cat`:

```bash
cat > thegioimang.txt
```

Nhập nội dung:

```text
Chào mừng các bạn đến với diễn đàn Mạng Máy Tính - wWw.TheGioiMang.oRg.
Nơi giao lưu trao đổi và chia sẻ các kiến thứ Mạng Máy Tính nói riêng và CNTT nói chung.
Chúc các bạn thành công và hạnh phúc !!!
```

Kết thúc bằng `Ctrl + D`.

Cách dùng heredoc để nhập nhanh:

```bash
cat > thegioimang.txt <<'EOF'
Chào mừng các bạn đến với diễn đàn Mạng Máy Tính - wWw.TheGioiMang.oRg.
Nơi giao lưu trao đổi và chia sẻ các kiến thứ Mạng Máy Tính nói riêng và CNTT nói chung.
Chúc các bạn thành công và hạnh phúc !!!
EOF
```

Kiểm tra:

```bash
cat thegioimang.txt
```

Lưu ý:

- Trong đề có chỗ ghi `thegioi.txt`, nhưng trước đó yêu cầu tạo `thegioimang.txt`.
- Nếu giáo viên yêu cầu đúng tên `thegioi.txt`, có thể tạo thêm bản copy:

```bash
cp thegioimang.txt thegioi.txt
```

Các phần dưới sẽ dùng `thegioimang.txt` làm file chính vì đây là file được yêu cầu tạo ở bước 2.

---

## 11.3. Tạo cây thư mục `athena`

Cây thư mục đề bài:

```text
athena
|-- class1
|-- class2
|   |-- basic_network
|-- class3
|   |-- Linux
|-- class4
|   |-- ccna
|-- class5
|   |-- ccnp
|-- class6
|-- mcsa
|-- ceh
```

Lệnh tạo cây thư mục:

```bash
mkdir -p athena/class1
mkdir -p athena/class2/basic_network
mkdir -p athena/class3/Linux
mkdir -p athena/class4/ccna
mkdir -p athena/class5/ccnp
mkdir -p athena/class6
mkdir -p athena/mcsa
mkdir -p athena/ceh
```

Có thể viết gọn:

```bash
mkdir -p athena/class1 \
         athena/class2/basic_network \
         athena/class3/Linux \
         athena/class4/ccna \
         athena/class5/ccnp \
         athena/class6 \
         athena/mcsa \
         athena/ceh
```

Kiểm tra:

```bash
find athena -type d | sort
```

Nếu có lệnh `tree`:

```bash
tree athena
```

Nếu chưa có `tree` trên Ubuntu/Debian:

```bash
sudo apt install tree
```

---

## 11.4. Copy file, tạo file rỗng, dùng `pwd`

### Copy `thegioimang.txt` vào `class1`, `class2`, `class3`, `class4`

```bash
cp thegioimang.txt athena/class1/
cp thegioimang.txt athena/class2/
cp thegioimang.txt athena/class3/
cp thegioimang.txt athena/class4/
```

Hoặc viết gọn bằng vòng lặp:

```bash
for d in athena/class1 athena/class2 athena/class3 athena/class4; do
  cp thegioimang.txt "$d/"
done
```

Kiểm tra:

```bash
ls -l athena/class1 athena/class2 athena/class3 athena/class4
```

---

### Tạo thêm 2 file rỗng bằng `touch`, copy sang `class5` và `class6`

Tạo file rỗng:

```bash
touch empty1.txt empty2.txt
```

Copy:

```bash
cp empty1.txt athena/class5/
cp empty2.txt athena/class6/
```

Kiểm tra:

```bash
ls -l empty1.txt empty2.txt
ls -l athena/class5/empty1.txt
ls -l athena/class6/empty2.txt
```

Nhận xét:

- File tạo bằng `touch` có kích thước `0` byte nếu chưa có nội dung.

---

### Sử dụng `pwd`

```bash
pwd
```

Kết quả là đường dẫn thư mục hiện tại, ví dụ:

```text
/home/student
```

---

## 11.5. Xóa `thegioimang.txt` trong `class1`, `class3`

```bash
rm athena/class1/thegioimang.txt
rm athena/class3/thegioimang.txt
```

Kiểm tra:

```bash
ls -l athena/class1
ls -l athena/class3
```

Nhận xét:

- File trong `class1` và `class3` bị xóa.
- File cùng tên ở `class2` và `class4` không bị ảnh hưởng vì đây là các bản copy độc lập.

---

## 11.6. Di chuyển `ccna` qua `ccnp` và `Linux` qua `ceh`

Theo cây thư mục đã tạo:

- `ccna` nằm ở `athena/class4/ccna`.
- `ccnp` nằm ở `athena/class5/ccnp`.
- `Linux` nằm ở `athena/class3/Linux`.
- `ceh` nằm ở `athena/ceh`.

Di chuyển `ccna` vào `ccnp`:

```bash
mv athena/class4/ccna athena/class5/ccnp/
```

Sau lệnh này, đường dẫn mới là:

```text
athena/class5/ccnp/ccna
```

Di chuyển `Linux` vào `ceh`:

```bash
mv athena/class3/Linux athena/ceh/
```

Sau lệnh này, đường dẫn mới là:

```text
athena/ceh/Linux
```

Kiểm tra:

```bash
find athena -type d | sort
```

---

## 11.7. Copy nội dung thư mục `ceh` vào bên trong thư mục `ccnp`

Dùng:

```bash
cp -r athena/ceh/* athena/class5/ccnp/
```

Nếu muốn copy cả file ẩn, dùng cách chắc hơn:

```bash
cp -a athena/ceh/. athena/class5/ccnp/
```

Kiểm tra:

```bash
find athena/class5/ccnp -maxdepth 2 -print
```

Giải thích:

- `cp -r` copy đệ quy thư mục con.
- `cp -a` là archive mode, giữ quyền, owner, timestamp, symlink tốt hơn trong nhiều trường hợp.

---

## 11.8. Tạo hard link và soft link giữa `thegioimang.txt` và hai file rỗng

Giả sử dùng file nguồn còn tồn tại ở:

```text
athena/class2/thegioimang.txt
```

Vì `empty1.txt` và `empty2.txt` trong `class5`, `class6` đang là file thường rỗng, nếu muốn biến chúng thành link thì xóa bản rỗng trước:

```bash
rm athena/class5/empty1.txt
rm athena/class6/empty2.txt
```

Lấy đường dẫn tuyệt đối của file nguồn:

```bash
SOURCE="$(readlink -f athena/class2/thegioimang.txt)"
echo "$SOURCE"
```

Tạo hard link dùng tên `empty1.txt`:

```bash
ln "$SOURCE" athena/class5/empty1.txt
```

Tạo symbolic link dùng tên `empty2.txt`:

```bash
ln -s "$SOURCE" athena/class6/empty2.txt
```

Kiểm tra:

```bash
ls -li "$SOURCE" athena/class5/empty1.txt athena/class6/empty2.txt
```

Nhận xét:

- `athena/class5/empty1.txt` là hard link: cùng inode với `thegioimang.txt`.
- `athena/class6/empty2.txt` là soft link: inode khác, dòng `ls -l` có dạng `empty2.txt -> /duong/dan/thegioimang.txt`.
- Ghi vào hard link hoặc file gốc đều làm nội dung bên kia thay đổi.
- Ghi vào soft link cũng làm file gốc thay đổi, nhưng nếu file gốc bị xóa thì soft link sẽ hỏng.

---

## 11.9. Xóa hard link và soft link

Xóa link:

```bash
rm athena/class5/empty1.txt
rm athena/class6/empty2.txt
```

Kiểm tra file gốc:

```bash
ls -li "$SOURCE"
cat "$SOURCE"
```

Nhận xét:

- Xóa hard link `empty1.txt` chỉ làm link count giảm, không xóa dữ liệu nếu vẫn còn tên file khác trỏ đến inode.
- Xóa soft link `empty2.txt` chỉ xóa file link, không ảnh hưởng file gốc.

---

## 11.10. Tổng hợp lệnh và nhận xét

| Nhóm lệnh | Lệnh tiêu biểu | Nhận xét |
|---|---|---|
| Xem ngày giờ | `date` | Hiển thị thời gian hệ thống |
| Xem thư mục hiện tại | `pwd` | Rất cần khi thao tác file để tránh nhầm đường dẫn |
| Liệt kê file | `ls`, `ls -l`, `ls -a`, `ls -i` | Cho biết file, quyền, inode, file ẩn |
| Tạo file rỗng | `touch` | Tạo file 0 byte hoặc cập nhật timestamp |
| Tạo file có nội dung | `cat > file` | Nhập trực tiếp từ bàn phím, kết thúc bằng `Ctrl + D` |
| Xem file | `cat`, `more`, `less`, `head`, `tail` | `cat` cho file ngắn, `less` tốt cho file dài |
| Tạo thư mục | `mkdir`, `mkdir -p` | `-p` tạo toàn bộ thư mục cha |
| Copy | `cp`, `cp -r`, `cp -a` | Copy file/thư mục; `-r` cho thư mục |
| Di chuyển/đổi tên | `mv` | Dùng để move hoặc rename |
| Xóa | `rm`, `rm -r` | Cẩn thận khi xóa, đặc biệt với `sudo` và đường dẫn `/` |
| Hard link | `ln source link` | Cùng inode, tăng link count |
| Soft link | `ln -s source link` | Inode riêng, trỏ bằng đường dẫn |
| Đếm | `wc -l`, `wc -w`, `wc -m` | Đếm dòng, từ, ký tự |
| Sắp xếp | `sort`, `sort -r` | Sắp xếp tăng/giảm |
| Pipe | `cmd1 | cmd2` | Chuyển output lệnh trước thành input lệnh sau |
| Redirect | `>`, `>>`, `2>` | Chuyển stdout/stderr vào file |

---

# Phần bổ sung - Lệnh `tar`

## 12.1. `tar` dùng để làm gì?

`tar` là lệnh dùng để đóng gói nhiều file/thư mục thành một file archive.

Tên `tar` xuất phát từ **tape archive**.

Lưu ý quan trọng:

- `tar` mặc định chỉ **đóng gói**, chưa nén.
- Muốn nén, thường kết hợp với `gzip`, `bzip2` hoặc `xz`.

Ví dụ:

| Định dạng | Ý nghĩa |
|---|---|
| `.tar` | Chỉ đóng gói, không nén |
| `.tar.gz` hoặc `.tgz` | Đóng gói + nén gzip |
| `.tar.bz2` | Đóng gói + nén bzip2 |
| `.tar.xz` | Đóng gói + nén xz |

---

## 12.2. Cú pháp chung

```bash
tar [OPTION] -f ARCHIVE_NAME FILE_OR_FOLDER
```

Ví dụ:

```bash
tar -cvf backup.tar athena/
```

Giải thích:

- `c`: create, tạo archive.
- `v`: verbose, hiển thị file đang xử lý.
- `f`: file, chỉ định tên file archive.
- `backup.tar`: tên file archive.
- `athena/`: thư mục cần đóng gói.

---

## 12.3. Các tùy chọn thường dùng của `tar`

| Tùy chọn | Tên đầy đủ / ý nghĩa | Ví dụ |
|---|---|---|
| `-c` | create archive | `tar -cf a.tar folder/` |
| `-x` | extract archive | `tar -xf a.tar` |
| `-t` | list nội dung archive | `tar -tf a.tar` |
| `-v` | verbose, hiển thị chi tiết | `tar -cvf a.tar folder/` |
| `-f` | chỉ định file archive | `tar -cf a.tar folder/` |
| `-z` | dùng gzip | `tar -czf a.tar.gz folder/` |
| `-j` | dùng bzip2 | `tar -cjf a.tar.bz2 folder/` |
| `-J` | dùng xz | `tar -cJf a.tar.xz folder/` |
| `-C` | đổi thư mục trước khi giải nén/đóng gói | `tar -xf a.tar -C /tmp` |
| `-p` | preserve permission | `tar -xpf a.tar` |
| `-r` | append file vào archive `.tar` chưa nén | `tar -rf a.tar new.txt` |
| `-u` | update file mới hơn vào archive | `tar -uf a.tar file.txt` |
| `--delete` | xóa file khỏi archive `.tar` chưa nén | `tar --delete -f a.tar old.txt` |
| `--exclude` | loại trừ file/thư mục | `tar --exclude='*.log' -czf a.tar.gz folder/` |
| `--strip-components=N` | bỏ N cấp thư mục đầu khi giải nén | `tar -xf a.tar --strip-components=1` |
| `-P` | giữ đường dẫn tuyệt đối | `tar -cPf abs.tar /etc/hosts` |

Lưu ý:

- `-f` gần như luôn cần có khi làm việc với file archive.
- Tùy chọn sau `-f` phải là tên archive, ví dụ `tar -cvf backup.tar folder/`.
- Không nên dùng `-P` nếu chưa hiểu rõ, vì giải nén archive chứa đường dẫn tuyệt đối có thể ghi đè file hệ thống.

---

## 12.4. Tạo file `.tar` không nén

```bash
tar -cvf athena.tar athena/
```

Kiểm tra:

```bash
ls -lh athena.tar
```

Xem nội dung archive:

```bash
tar -tvf athena.tar
```

---

## 12.5. Tạo file `.tar.gz` bằng gzip

```bash
tar -czvf athena.tar.gz athena/
```

Giải thích:

- `z`: nén gzip.
- File kết quả thường nhỏ hơn `.tar`.
- gzip nhanh, phổ biến.

---

## 12.6. Tạo file `.tar.bz2` bằng bzip2

```bash
tar -cjvf athena.tar.bz2 athena/
```

Giải thích:

- `j`: nén bzip2.
- Thường nén tốt hơn gzip nhưng chậm hơn.

---

## 12.7. Tạo file `.tar.xz` bằng xz

```bash
tar -cJvf athena.tar.xz athena/
```

Giải thích:

- `J`: nén xz.
- Thường nén tốt nhưng tốn CPU hơn.

---

## 12.8. Giải nén archive

Giải nén `.tar`:

```bash
tar -xvf athena.tar
```

Giải nén `.tar.gz`:

```bash
tar -xzvf athena.tar.gz
```

Giải nén `.tar.bz2`:

```bash
tar -xjvf athena.tar.bz2
```

Giải nén `.tar.xz`:

```bash
tar -xJvf athena.tar.xz
```

Giải nén vào thư mục chỉ định:

```bash
mkdir restore
tar -xvf athena.tar -C restore/
```

---

## 12.9. Backup thư mục bằng `tar`

Ví dụ backup thư mục `athena`:

```bash
tar -czvf athena-backup.tar.gz athena/
```

Backup kèm ngày hiện tại:

```bash
tar -czvf "athena-backup-$(date +%F).tar.gz" athena/
```

Kết quả ví dụ:

```text
athena-backup-2026-05-31.tar.gz
```

---

## 12.10. Loại trừ file khi backup

Ví dụ loại trừ file log:

```bash
tar --exclude='*.log' -czvf backup.tar.gz athena/
```

Loại trừ một thư mục:

```bash
tar --exclude='athena/tmp' -czvf backup.tar.gz athena/
```

---

## 12.11. Thêm file vào archive `.tar`

Chỉ dùng được thuận tiện với archive `.tar` chưa nén:

```bash
tar -rvf athena.tar newfile.txt
```

Kiểm tra:

```bash
tar -tvf athena.tar | grep newfile.txt
```

Lưu ý:

- Không nên dùng `-r` trực tiếp với `.tar.gz`, `.tar.bz2`, `.tar.xz`.
- Với archive nén, thường giải nén ra, thêm file, rồi nén lại.

---

# Phần bổ sung - Cron job

## 13.1. Cron job là gì?

**Cron** là cơ chế lập lịch chạy lệnh tự động trên Linux/Unix.

Một **cron job** là một lệnh hoặc script được cấu hình để chạy theo thời gian định sẵn, ví dụ:

- Mỗi phút.
- Mỗi ngày lúc 2 giờ sáng.
- Mỗi thứ Hai.
- Khi hệ thống khởi động.
- Backup dữ liệu định kỳ.
- Xóa log cũ.

Dịch vụ cron thường chạy nền dưới dạng daemon.

Kiểm tra trạng thái trên Ubuntu/Debian:

```bash
systemctl status cron
```

Khởi động cron:

```bash
sudo systemctl start cron
```

Bật cron tự chạy khi boot:

```bash
sudo systemctl enable cron
```

Trên một số hệ Red Hat/CentOS/Fedora, service có thể là `crond`:

```bash
systemctl status crond
```

---

## 13.2. Quản lý crontab của user

Mở file crontab của user hiện tại:

```bash
crontab -e
```

Xem danh sách cron job:

```bash
crontab -l
```

Xóa toàn bộ crontab của user hiện tại:

```bash
crontab -r
```

Cẩn thận với `crontab -r` vì nó xóa toàn bộ job mà không hỏi lại trên nhiều hệ thống.

---

## 13.3. Cú pháp thời gian của crontab

Một dòng cron job có dạng:

```text
* * * * * command
| | | | |
| | | | +----- day of week: 0-7, trong đó 0 hoặc 7 là Chủ nhật
| | | +------- month: 1-12
| | +--------- day of month: 1-31
| +----------- hour: 0-23
+------------- minute: 0-59
```

Ví dụ:

```cron
30 7 * * * /home/student/script.sh
```

Nghĩa là chạy lúc 07:30 mỗi ngày.

---

## 13.4. Ký hiệu thời gian thường dùng

| Cú pháp | Ý nghĩa |
|---|---|
| `*` | Mọi giá trị |
| `*/5` | Mỗi 5 đơn vị |
| `1,15,30` | Tại các giá trị 1, 15, 30 |
| `1-5` | Từ 1 đến 5 |
| `0 0 * * *` | 00:00 mỗi ngày |
| `0 2 * * *` | 02:00 mỗi ngày |
| `*/10 * * * *` | Mỗi 10 phút |
| `30 7 * * 1-5` | 07:30 từ thứ Hai đến thứ Sáu |
| `0 0 1 * *` | 00:00 ngày đầu mỗi tháng |

---

## 13.5. Các shortcut của cron

| Shortcut | Ý nghĩa |
|---|---|
| `@reboot` | Chạy khi hệ thống khởi động |
| `@yearly` hoặc `@annually` | Mỗi năm một lần |
| `@monthly` | Mỗi tháng một lần |
| `@weekly` | Mỗi tuần một lần |
| `@daily` hoặc `@midnight` | Mỗi ngày một lần |
| `@hourly` | Mỗi giờ một lần |

Ví dụ:

```cron
@reboot /home/student/startup.sh
@daily /home/student/backup.sh
```

---

## 13.6. Ví dụ cron job đơn giản

Mở crontab:

```bash
crontab -e
```

Thêm dòng:

```cron
* * * * * /usr/bin/date >> /home/student/cron-test.log 2>&1
```

Giải thích:

- Chạy mỗi phút.
- `/usr/bin/date` in ngày giờ.
- `>> /home/student/cron-test.log` ghi thêm kết quả vào file log.
- `2>&1` đưa lỗi stderr vào cùng stdout.

Kiểm tra sau vài phút:

```bash
cat /home/student/cron-test.log
```

---

## 13.7. Ví dụ cron job backup bằng `tar`

Tạo thư mục backup:

```bash
mkdir -p /home/student/backups
```

Mở crontab:

```bash
crontab -e
```

Thêm job backup thư mục `athena` lúc 02:00 mỗi ngày:

```cron
0 2 * * * /usr/bin/tar -czf /home/student/backups/athena-$(/usr/bin/date +\%F).tar.gz /home/student/athena >> /home/student/backups/backup.log 2>&1
```

Lưu ý rất quan trọng:

- Trong crontab, ký tự `%` có ý nghĩa đặc biệt, nên khi dùng `date +%F` phải viết là `date +\%F`.
- Nên dùng đường dẫn tuyệt đối như `/usr/bin/tar`, `/usr/bin/date`, `/home/student/...`.

Nếu không biết đường dẫn lệnh `tar` và `date`, kiểm tra bằng:

```bash
which tar
which date
```

Ví dụ kết quả:

```text
/usr/bin/tar
/usr/bin/date
```

---

## 13.8. Chạy script bằng cron

Tạo script backup:

```bash
nano /home/student/backup-athena.sh
```

Nội dung:

```bash
#!/bin/bash

BACKUP_DIR="/home/student/backups"
SOURCE_DIR="/home/student/athena"
DATE="$(date +%F)"

mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_DIR/athena-$DATE.tar.gz" "$SOURCE_DIR"
```

Cấp quyền chạy:

```bash
chmod +x /home/student/backup-athena.sh
```

Thêm vào crontab:

```cron
0 2 * * * /home/student/backup-athena.sh >> /home/student/backups/backup.log 2>&1
```

Nhận xét:

- Cách dùng script dễ đọc và dễ bảo trì hơn viết lệnh dài trực tiếp trong crontab.
- Trong script, không cần escape `%` như trong dòng crontab trực tiếp.

---

## 13.9. Lưu ý khi viết cron job

1. **Dùng đường dẫn tuyệt đối**

Không nên viết:

```cron
0 2 * * * tar -czf backup.tar.gz athena
```

Nên viết:

```cron
0 2 * * * /usr/bin/tar -czf /home/student/backup.tar.gz /home/student/athena
```

2. **Môi trường cron rất tối giản**

Cron không tự có đầy đủ `PATH`, biến môi trường, thư mục hiện tại như terminal tương tác.

Có thể khai báo PATH ở đầu crontab:

```cron
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

3. **Luôn ghi log để debug**

```cron
* * * * * /home/student/job.sh >> /home/student/job.log 2>&1
```

4. **Script cần quyền thực thi**

```bash
chmod +x /home/student/job.sh
```

5. **Kiểm tra timezone hệ thống**

```bash
timedatectl
```

6. **Không dùng lệnh cần nhập mật khẩu hoặc tương tác**

Cron chạy tự động nên không phù hợp với lệnh cần người dùng nhập thêm dữ liệu.

---

# Tổng kết kiến thức chính

## Soft link

- Tạo bằng `ln -s`.
- Có inode riêng.
- Trỏ đến file gốc bằng đường dẫn.
- Xóa file gốc làm soft link bị hỏng.

## Hard link

- Tạo bằng `ln`.
- Cùng inode với file gốc.
- Xóa một hard link không làm mất dữ liệu nếu còn hard link khác.
- Không dùng được qua filesystem khác trong trường hợp thông thường.

## Redirect và pipe

| Cú pháp | Ý nghĩa |
|---|---|
| `>` | Ghi đè stdout vào file |
| `>>` | Ghi thêm stdout vào file |
| `2>` | Ghi đè stderr vào file |
| `2>>` | Ghi thêm stderr vào file |
| `2>&1` | Gộp stderr vào stdout |
| `|` | Chuyển output lệnh trước cho input lệnh sau |
| `&&` | Chạy lệnh sau nếu lệnh trước thành công |
| `;` | Chạy lệnh sau bất kể lệnh trước thành công hay thất bại |

## Các lệnh quản trị file cơ bản

| Lệnh | Công dụng |
|---|---|
| `pwd` | Xem thư mục hiện tại |
| `ls` | Liệt kê file/thư mục |
| `cd` | Chuyển thư mục |
| `mkdir` | Tạo thư mục |
| `touch` | Tạo file rỗng/cập nhật timestamp |
| `cat` | Xem/tạo/nối file |
| `cp` | Copy file/thư mục |
| `mv` | Di chuyển/đổi tên |
| `rm` | Xóa file/thư mục |
| `head` | Xem đầu file |
| `tail` | Xem cuối file |
| `more`, `less` | Xem file/output theo trang |
| `wc` | Đếm dòng/từ/ký tự |
| `sort` | Sắp xếp |
| `file` | Nhận diện kiểu file |
| `stat` | Xem metadata file |
| `tar` | Đóng gói/nén/giải nén archive |
| `crontab` | Quản lý cron job |

---

# Gợi ý dọn môi trường sau khi làm lab

Chỉ chạy nếu chắc chắn đây là môi trường lab/máy ảo:

```bash
sudo rm -rf /grandfather /grandmother /abc /def /hgi /mydir /a /a1 /a2
rm -rf athena text.txt abc.txt abc1.txt home.txt thegioimang.txt thegioi.txt empty1.txt empty2.txt *.tar *.tar.gz *.tar.bz2 *.tar.xz
```

Không dùng `sudo rm -rf` nếu chưa hiểu rõ đường dẫn đang xóa.
