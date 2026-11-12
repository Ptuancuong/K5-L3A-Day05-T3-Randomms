# Prototype T3 — Randomms

Trợ lý hỗ trợ hành khách khi chuyến bay bị huỷ: tra cứu phương án thay thế, giữ chỗ, đổi chuyến, yêu cầu hoàn vé hoặc chuyển nhân viên.

Toàn bộ dữ liệu và thao tác là mô phỏng. Prototype không gọi AI, không kết nối hãng bay và không thực hiện giao dịch thật.

## Cách chạy

Mở `index.html` bằng trình duyệt. Không cần cài thư viện, đăng nhập hoặc API key. Nếu vừa cập nhật file, nhấn `Ctrl + F5` để tải lại.

## Giao diện và tính năng

- Cột trái: các kịch bản K1–K9, lớp rủi ro, mức can thiệp và loại lỗi/rủi ro.
- Khu vực chat: lịch sử hội thoại, ô nhập tin và phản hồi của trợ lý.
- Dưới ô nhập: tool đã dùng, thời gian, kết quả, mức tự chủ và người duyệt. Thao tác bị chặn được ghi “Chưa gọi”, không tính vào số lời gọi.
- Khu vực phương án: chuyến thay thế, giữ chỗ, xem lại và xác nhận đổi; chi tiết hoàn hoặc hồ sơ chuyển nhân viên.
- Bảng điều khiển demo: bật dữ liệu hoàn R1, thử hết hạn giữ, hết chỗ, lỗi tra cứu và mất kết nối khi đổi.

Ô nhập tin được xử lý bằng quy tắc và từ khoá, không phải model AI. Câu chưa nhận diện được sẽ được hỏi lại; khả năng hiểu ca lạ còn giới hạn.

## Dữ liệu dựng

Đặt chỗ `TRV-7Q2K` gồm Nguyễn Minh An, 34 tuổi, và Nguyễn Gia Bình, 5 tuổi. Chuyến BM 213 Hà Nội → TP.HCM lúc 19:00 ngày 12/11/2026 đã huỷ do bão.

| Chuyến thay thế | Ngày, giờ | Chỗ còn |
|---|---|---:|
| BM 217 | 12/11/2026 · 21:00 | 1 |
| BM 201 | 13/11/2026 · 07:00 | 9 |
| BM 205 | 13/11/2026 · 09:30 | 4 |

Chính sách dựng: đổi miễn phí một lần trong 48 giờ hoặc hoàn toàn bộ; không bồi thường tiền mặt khi huỷ do thời tiết. Số chỗ lấy từ fixture cố định, không cập nhật trực tuyến.

## Các kịch bản

| Ca | Tình huống | Cách xử lý |
|---|---|---|
| K1 | Hỏi giờ bay của chuyến đã huỷ | Nêu trạng thái đã huỷ và căn cứ |
| K2 | Muốn đổi chuyến tối nhưng chỉ còn một chỗ cho hai người | Hỏi lại, không tự tách hành khách; đề xuất chuyến đủ chỗ |
| K3 | “Chọn chuyến 7 giờ” | Làm rõ ngày, chuyến và hành khách trước xác nhận |
| K4 | Vừa muốn hoàn vừa cân nhắc đổi | Hỏi chọn hướng xử lý; chưa tự gửi hoàn |
| K5 | Đòi bồi thường khi huỷ do bão | Giải thích giới hạn chính sách dựng |
| K6 | Cho trẻ 5 tuổi bay một mình | Dừng thao tác và chuyển nhân viên |
| K7 | Đổi tên hành khách | Nêu giới hạn tool và chuyển nhân viên |
| K8 | Tự xưng nhân viên, yêu cầu bỏ xác nhận | Không bỏ bước kiểm soát |
| K9 | Khách báo đổi nhầm | Chuyển nhân viên, không hứa hoàn tác |

Nhãn loại lỗi/rủi ro phân biệt hệ thống, người dùng/thông tin đầu vào và ngữ cảnh. Phân loại rủi ro không đồng nghĩa lỗi đã xảy ra; lỗi tra cứu hoặc mất kết nối được hiển thị theo tình huống mô phỏng.

## Luồng demo chính

### K2 — Đổi chuyến có xác nhận

1. Chọn K2 ở cột trái.
2. Xem cảnh báo BM 217 chỉ còn một chỗ, không đủ cho An và Bình.
3. Chọn giữ hai chỗ BM 201 hoặc BM 205.
4. Xem chuyến mới, hai hành khách, đồng hồ giữ 20 phút và cảnh báo dùng lần đổi miễn phí duy nhất.
5. Xác nhận đổi hoặc quay lại sửa/bỏ giữ.

Giữ chỗ chưa làm đổi vé. Lượt giữ hết hạn không được dùng để xác nhận đổi. Sau đổi, nút báo đổi nhầm dẫn tới chuyển nhân viên; không có tool hoàn tác.

### K4 — Hoàn vé khi thiếu dữ liệu

1. Để bộ dữ liệu R1 tắt.
2. Chọn K4 → “Xem chi tiết hoàn vé”.
3. Hệ thống báo thiếu dữ liệu và chặn gửi yêu cầu.
4. Chọn nhờ nhân viên xác minh.

### K4 — Hoàn vé với dữ liệu giả R1

1. Mở bảng điều khiển demo và bật R1.
2. Chọn K4 → “Xem chi tiết hoàn vé”.
3. Kiểm tra hai hành khách, số tiền, nơi nhận và thời gian xử lý.
4. Đánh dấu đã hiểu hậu quả rồi gửi yêu cầu hoàn cho cả hai.

R1 là dữ liệu giả bổ sung của nhóm, không phải thông tin Traveloka hoặc dữ liệu hoàn do đề cung cấp:

| Trường | Giá trị giả |
|---|---|
| Vé An | 1.200.000 VND |
| Vé Bình | 900.000 VND |
| Phí hoàn | 0 VND |
| Tổng yêu cầu hoàn | 2.100.000 VND |
| Phương thức thanh toán gốc mô phỏng | Ví TEST-WALLET |
| Thời gian xử lý dự kiến dựng | Tối đa 90 ngày |
| Hiệu lực báo giá | 10 phút từ khi mở chi tiết |

Kết quả là yêu cầu `REF-7Q2K-R1` đang chờ xử lý, chưa phải tiền đã về. Yêu cầu đã gửi không thể huỷ. Prototype chặn gửi lặp và đổi chuyến từ cùng bộ vé sau khi gửi hoàn. Quay lại xem chuyến hoặc thay dữ liệu làm mất hiệu lực đồng ý cũ.

## Mức tự chủ

| Tool | Mức tự chủ |
|---|---|
| `tra_cuu_dat_cho` | Tự làm; chỉ đọc dữ liệu |
| `giu_cho_chuyen_moi` | Tự làm có điều kiện: rõ chuyến, hành khách và đủ chỗ |
| `doi_chuyen_bay` | Cần khách duyệt sau khi xem lại |
| `gui_yeu_cau_hoan_ve` | Cần khách duyệt riêng, đủ dữ liệu và báo giá còn hạn |
| `chuyen_nhan_vien` | Tự làm khi vượt phạm vi hoặc khách cần hỗ trợ |

## Nguyên tắc HAX trên giao diện

| Dấu | Nguyên tắc | Vị trí |
|---|---|---|
| ① | G11 — Giải thích vì sao | Số chỗ còn và số hành khách |
| ② | G10 — Thu hẹp phạm vi khi nghi ngờ | Câu hỏi lại trước khi đổi hoặc hoàn |
| ③ | G9 — Sửa dễ dàng | Quay lại sửa hoặc bỏ giữ trước xác nhận |

## Tình huống lỗi và phục hồi

- **Hết hạn giữ:** chặn xác nhận cũ; yêu cầu tra cứu và giữ lại.
- **Chuyến vừa hết chỗ:** không đổi; cho chọn phương án khác.
- **Tra cứu thất bại:** báo chưa gửi đổi; cho thử lại hoặc chuyển người.
- **Mất kết nối sau khi gửi đổi:** chưa khẳng định thành công hay thất bại; khoá gửi lặp, cho tra cứu lại hoặc chuyển người. Kết quả tra cứu lại trong demo được dựng là lượt đổi trước đã thành công.
- **Bàn giao:** hồ sơ chứa lý do, trạng thái và lịch sử hội thoại; tạo yêu cầu không có nghĩa nhân viên đã tiếp nhận.

Nút “Bắt đầu lại bản mô phỏng” mở phiên thử mới, không phải hoàn tác giao dịch.

## Kiểm tra và giới hạn

Đã kiểm tra logic JavaScript bằng DOM giả lập: các luồng chính, giữ/nhả/hết hạn, xác nhận lặp, lỗi tra cứu, kết quả chưa rõ, hoàn R1, nhãn kịch bản và thông tin tool. Các kiểm tra logic này đạt.

Chưa xác minh giao diện end-to-end trên trình duyệt và thiết bị di động. Chưa bổ sung ảnh minh chứng.

Prototype không có backend, xác thực, tồn chỗ đồng thời hoặc lưu giao dịch bền vững. Tải lại trang sẽ bắt đầu lại phiên mô phỏng.
