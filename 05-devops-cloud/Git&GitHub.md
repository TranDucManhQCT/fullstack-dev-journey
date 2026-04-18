# Git & GitHub


## Tổng quan

<details>
  <summary><b>Git là gì?</b></summary>

Git là một hệ thống kiểm soát phiên bản phân tán được dùng để quản lý tiến độ của một dự án, từ đơn giản như một trang `index.html` hoặc phức tạp như một ứng dụng `full-stack` hoàn chỉnh. Có thể quay lại bất kỳ phiên bản nào trong lịch sử, hỗ trợ cộng tác song song nhiều tính năng mà không làm gián đoạn luồng chính.

</details>
<details>
  <summary><b>GitHub là gì?</b></summary>

GitHub là một nền tảng lưu trữ mã nguồn trực tuyến dựa trên Git. Nó cung cấp giao diện web để xem lịch sử commit, quản lý pull request, review code, báo cáo lỗi (Issues), và tích hợp CI/CD. 

</details>



<details>
  <summary><b>Git Bash là gì?</b></summary>

Git Bash là ứng dụng mô phỏng môi trường Bash trên Windows, đi kèm khi bạn cài Git. Giúp bạn dùng các lệnh Unix/Linux quen thuộc như ls, cd, mkdir cùng với toàn bộ lệnh Git.

</details>

## Cài đặt 

Để kiểm ra Git đã được cài đặt sẵn chưa. Mở `Terminal` (hoặc `Git Bash`) và nhập lệnh sau: 
```
git --version
```

**Đã cài đặt**: Bạn sẽ thấy thông báo dạng `git version 2.x.x`.

**Chưa cài đặt**: Hệ thống sẽ báo lỗi `command not found`.

1. Truy cập trang chủ [git-scm.com](git-scm.com).

2. Tải bản cài đặt phù hợp với hệ điều hành (Windows, macOS, Linux).

3. Chạy file setup và giữ các thiết lập mặc định (Recommended).

---

## Cấu trúc kho lưu trữ (Repository)

Để có thể **chia sẻ trực tuyến** một đoạn code, ta cần quy trình triển khai dựa trên tương tác giữa hai loại kho lưu trữ kết nối với nhau:

- **Kho lưu trữ từ xa (Remote Repository):** thường đặt trên GitHub, dùng để chia sẻ và cộng tác nhóm.

- **Kho lưu trữ cục bộ (Local Repository):** nơi bạn viết code, tạo commit và thử nghiệm. Không cần internet.

## Các lệnh triển khai & Kết nối

<details>
  <summary><b>git init — Khởi tạo Local Repository</b></summary>

- Biến một thư mục thông thường thành một kho lưu trữ cục bộ (Git Repo). Chỉ cần chạy một lần khi bắt đầu dự án mới.

- Thư mục ẩn <code>.git/</code> được tạo ra — chứa toàn bộ lịch sử commit, cấu hình và siêu dữ liệu của repo. Không xóa thư mục nà

</details>

```
git init
```
<details>
  <summary><b>git remote add — Kết nối với Remote Repository</b></summary>

- Đổi tên nhánh hiện tại thành main. Tiêu chuẩn hiện đại dùng main thay cho master (từ năm 2020).

- <code>-M</code>	Viết tắt của --move --force — buộc đổi tên ngay cả khi đã có nhánh trùng tên. Khác với -m (chữ thường) sẽ báo lỗi nếu trùng

</details>


Để thực hiện quá trình truyền tải dữ liệu, cần định nghĩa một điểm đích. Lệnh **`git remote add`** thực hiện việc gán một định danh (thông thường là origin) cho một URL cụ thể trên hệ thống máy chủ GitHub.

```
git remote add origin <Repository_URL>
```
* `add`: Thêm kết nối từ xa mới.
* `origin`: đặt biệt danh cho URL của kho lưu trữ từ xa ( origin là một biệt danh phổ biến).
* `<repository_url>`: Chỗ dành cho URL của kho lưu trữ từ xa.

Nhằm tuân thủ các tiêu chuẩn hiện đâị, nhánh chính mặc định được thiết lập là main. Lệnh **`git branch -M`** thực hiện thao tác đổi tên nhánh để chuẩn hóa cấu trúc phát triển dự án.

```
git branch -M main
```
* Biểu tượng cờ viết hoa `-M` (Move/Rename) buộc đổi tên nhánh hiện tại thành main.