# BIM Design — bản sao lưu v28 trước khi bổ sung NFA

Ứng dụng: **BIM Design · Tính toán chỉ tiêu quy hoạch công trình**.

- Phiên bản Sites: **28**.
- Commit nguồn chính xác: `e9cc98de44f64b769006d401a4c247df0a0bf4da`.
- Tag khôi phục trong Git bundle: **`v28-before-nfa`**.
- Mã nguồn được giữ nguyên; chưa bổ sung tính năng NFA.
- Đây là bản sao lưu. Việc tạo bản sao không sửa hoặc triển khai lại site đang chạy.

## Nội dung

- `BIM-Design-v28-before-nfa.bundle`: toàn bộ lịch sử Git tới v28, cùng nhánh `main` và tag khôi phục. Dùng gói này để có đủ các commit cũ mà bộ kiểm thử hồi quy cần tham chiếu.
- `BIM-Design-v28-source.zip`: ảnh chụp nguyên trạng toàn bộ 46 file được Git quản lý tại v28; có thể giải nén để xem hoặc chạy giao diện tĩnh.
- `BACKUP-MANIFEST.json`: nguồn gốc phiên bản, danh sách file, kích thước và SHA-256 của các gói sao lưu.
- `SHA256SUMS`: mã kiểm tra toàn vẹn các gói và manifest.

File DXF và thông số chỉ tồn tại trong phiên trình duyệt của người dùng không nằm trong Git và không có trong gói này. Không chứa thư mục node_modules, thông tin đăng nhập hay cấu hình xác thực Git cục bộ.

## Khôi phục đúng v28

Tải file bundle rồi chạy:

```bash
git clone --branch v28-before-nfa BIM-Design-v28-before-nfa.bundle BIM-Design-v28
cd BIM-Design-v28
git rev-parse HEAD
```

Kết quả phải là:

```text
e9cc98de44f64b769006d401a4c247df0a0bf4da
```

Git ở trạng thái detached HEAD để giữ nguyên mốc. Muốn phát triển tiếp, tạo nhánh mới:

```bash
git switch -c development
```

Mở `dist/index.html` qua máy chủ web tĩnh để chạy ứng dụng. Ví dụ trên máy cá nhân có Python:

```bash
python -m http.server 8000 --directory dist
```

Truy cập http://localhost:8000. Để chạy kiểm thử, máy cá nhân cần Node.js/npm, sau đó chạy `npm ci` và `npm test` trong repo đã khôi phục từ bundle. Bản zip riêng không kèm lịch sử Git, nên không đủ cho những kiểm thử so sánh commit cũ.

## Kiểm tra toàn vẹn

Sau khi tải các file, chạy:

```bash
sha256sum -c SHA256SUMS
```

Lần tạo bản sao này đã xác minh: 46/46 blob trong zip khớp với commit nguồn; `git bundle verify` đạt; clone sạch từ bundle khôi phục đúng commit và tree; `git fsck --full` đạt. Bộ kiểm thử ứng dụng không được chạy lại trong thao tác sao lưu; kết quả kiểm thử đã lưu cùng v28 nằm trong thư mục `qa` của mã nguồn.
