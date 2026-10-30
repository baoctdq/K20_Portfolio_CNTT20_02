## Thông tin sinh viên

- Họ và tên: Phạm Quốc Bảo
- Mã sinh viên – Lớp: [Điền MSV của bạn] – CNTT20_02
- Ngày thực hiện: 30/10/2026
- Link repository: https://github.com/baoctdq/K20_Portfolio_CNTT20_02.git
- URL website: https://baoctdq.github.io/K20_Portfolio_CNTT20_02/
- Tình huống: [x] Website của tôi  [ ] Repo luyện của giảng viên

## 1. Nhận định của tôi trước khi hỏi AI

- Trang/thao tác gặp lỗi: Trang chủ (index.html) - Lỗi không tải được file CSS khi đưa lên GitHub Pages.
- Mong muốn và hiện tượng thực tế: Mong muốn giao diện hiển thị đúng cấu trúc layout grid và style đã code, nhưng thực tế trang web chỉ hiện HTML thô, mất toàn bộ định dạng.
- Dữ kiện đã kiểm tra (cấu trúc tệp, Request URL, Status…): Cấu trúc tệp có thư mục `css/style.css`. Khi nhấn F12 kiểm tra tab Network, Request URL của file style.css báo lỗi `Status 404 Not Found`.
- Tôi nghi nguyên nhân là: Sai đường dẫn tương đối (relative path) khi nhúng file CSS vào thẻ `<link>` trong HTML.
- Vì sao tôi nhận định như vậy: Khi chạy bằng Live Server trên máy (localhost) thì giao diện bình thường, nhưng khi đẩy lên môi trường GitHub Pages thì đường dẫn bị sai lệch dẫn đến không tìm thấy file.

## 2. Tôi hỏi AI và nhận được gợi ý

- Nguồn: [x] Công cụ AI: Gemini  [ ] Phản hồi mẫu của giảng viên
- Câu hỏi/prompt tôi đã gửi (hoặc tình huống của phản hồi mẫu):

  "File css/style.css của tôi chạy trên localhost thì nhận bình thường, nhưng khi push lên GitHub Pages thì bị lỗi 404 Not Found. Thẻ link hiện tại của tôi trong thẻ head là: <link rel="stylesheet" href="/css/style.css">"

- Gợi ý chính của AI:

  AI giải thích rằng dấu gạch chéo `/` ở đầu đường dẫn sẽ trỏ về thư mục gốc của tên miền (tức là `baoctdq.github.io/css/...`). Vì repository của bạn nằm trong một thư mục con (sub-path là `/K20_Portfolio_CNTT20_02/`), nên đường dẫn tuyệt đối này bị sai.
  AI gợi ý sửa thành đường dẫn tương đối: Bỏ dấu `/` ở đầu, thay bằng `<link rel="stylesheet" href="./css/style.css">` hoặc `href="css/style.css"`.

## 3. Quyết định của tôi

- [x] Chấp nhận gợi ý
- [ ] Chỉnh sửa gợi ý rồi áp dụng
- [ ] Bác bỏ gợi ý

- Tôi quyết định làm gì: Thay đổi giá trị thuộc tính `href` trong thẻ `<link>` của file `index.html` theo gợi ý.
- Lý do, dựa trên dữ kiện nào: Gợi ý hợp lý vì GitHub Pages cấp phát URL dạng thư mục con (project trang cá nhân) chứ không phải domain gốc, việc dùng `./` sẽ giúp trình duyệt bắt đầu tìm kiếm từ thư mục hiện tại của file `index.html`.

## 4. Thực hiện và kiểm chứng

- Tệp/vị trí đã sửa (không sửa thì ghi rõ): Dòng chứa thẻ `<link>` trong phần `<head>` của file `index.html`.
- Nội dung thay đổi hoặc cách xử lý khác: Đổi `href="/css/style.css"` thành `href="./css/style.css"`.
- Commit của bản sửa, nếu có: `fix: update css relative path for github pages deployment`
- Bản sửa đã deploy: [x] Có  [ ] Chưa  [ ] Không phát sinh bản sửa

| Nội dung kiểm tra | Trước xử lý | Sau xử lý/thử lại |
| --- | --- | --- |
| Request URL và Status của tài nguyên liên quan | URL: .../css/style.css - Status: 404 Not Found | URL: .../K20_Portfolio_CNTT20_02/css/style.css - Status: 200 OK |
| Giao diện/chức năng trên URL website | Web hiện HTML thô, vỡ toàn bộ layout lưới (Grid). | Web hiển thị đầy đủ CSS, layout và màu sắc đúng thiết kế. |

- Cách thử lại và kết quả thực tế: Đợi GitHub Actions chạy xong quy trình deploy. Mở trang web ở chế độ ẩn danh (hoặc dùng Ctrl + F5 để xóa cache), kết quả file CSS đã được nạp thành công.
- Căn cứ để đối chiếu (URL tệp, commit, đường dẫn ảnh chụp hoặc dữ kiện quan sát): Quan sát trực tiếp giao diện hiển thị trên URL website và xác nhận mã 200 OK trong tab Network của DevTools.

## 5. Kết luận

- [x] Đã xử lý được  [ ] Xử lý được một phần  [ ] Chưa xử lý được
- Điều tôi rút ra hoặc việc cần làm tiếp: Cần cẩn trọng phân biệt giữa đường dẫn tuyệt đối (bắt đầu bằng `/`) và đường dẫn tương đối (`./` hoặc tên thư mục) khi xây dựng dự án web, đặc biệt là khi deploy lên các nền tảng sử dụng sub-path như GitHub Pages.