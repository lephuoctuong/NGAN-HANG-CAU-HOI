# Bản sửa V2 — Công văn quy định là nguồn bắt buộc do giáo viên cung cấp

## Thay đổi chính

1. Đã loại bỏ `DEFAULT_CV7991` khỏi `constants.ts`.
2. Bước 0 không còn tự điền Công văn mặc định.
3. Nút `Nạp dữ liệu mẫu` chỉ nạp bài học/đề mẫu/ma trận mẫu; KHÔNG nạp Công văn.
4. Khi nâng cấp lần đầu, ứng dụng xóa giá trị `qbank_cv7991` của phiên bản cũ để tránh tái sử dụng Công văn mẫu.
5. Mục 2 hiển thị rõ trạng thái bắt buộc cung cấp Công văn.
6. Không tự động chuyển sang Bước 1 ngay sau khi tải một tệp; giáo viên có thể nạp đủ các nguồn trước khi tiếp tục.
7. Bước 1–5 đều yêu cầu Công văn có nội dung trước khi chạy.
8. Server API `/api/generate/step1`, `/api/generate/step2`, `/api/generate/step3`, `/api/generate/step5` đều kiểm tra Công văn bắt buộc.
9. Bước 2 nhận toàn bộ nội dung Công văn do giáo viên cung cấp, thay vì chỉ nhận trạng thái “đã đính kèm”.
10. Bước 3 nhận toàn bộ Công văn + tài liệu nguồn + kết quả Bước 1 + Ma trận/Bản đặc tả Bước 2.
11. Bước 5 nhận toàn bộ Công văn khi tạo các mã đề tương đương.
12. Khi Công văn thay đổi, các kết quả Bước 1, 2, 3, 5 được xem là không còn hợp lệ và bị xóa để tránh dùng dữ liệu nguồn cũ.
13. Điều hướng trực tiếp bằng thanh bước cũng bị khóa nếu chưa có Công văn.
14. Đã loại bỏ fallback nội dung Toán “Phương trình bậc hai và Định lý Vi-ét” trong logic tự sinh Ma trận của `Step2Matrix.tsx`.
15. Nếu Bước 1 không cung cấp được đơn vị kiến thức, Bước 2 không tự bịa danh sách nội dung mẫu.

## Kiểm tra

- Đã kiểm tra cú pháp/transpile toàn bộ `.ts` và `.tsx`: OK.
- Không chạy được `npm ci` trong môi trường đóng gói do quá trình tải dependency vượt thời gian, vì vậy ZIP này không kèm `node_modules` và chưa tạo `dist`.
- Khi đưa source vào môi trường Google AI Studio, hãy cài dependency và chạy build theo `package.json`.
