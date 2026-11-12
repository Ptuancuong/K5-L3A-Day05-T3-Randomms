# Dàn ý bài nộp *(spec.md — nộp trước 23:59 ngày lab của lớp)*

> Copy dàn ý này vào `spec.md` của nhóm. Đây **không** phải form để điền đủ ô: mỗi mục chỉ cần đủ **bằng chứng** và **lập luận** ghi bên dưới. Viết ngắn, gạch đầu dòng là được. Hướng dẫn từng chặng: `02-guide.md`. Cách chấm: `04-rubric.md`.
>
> **Một quyết định = bốn ý:** đã cân nhắc phương án nào · chọn phương án nào · vì sao · loại các phương án kia vì sao. Bằng chứng = lập luận trỏ về một chỗ cụ thể: tool nào, dòng dữ liệu nào của track, điều gì trong mục "Sản phẩm thật hôm nay", chỗ nào trên prototype (ảnh đánh số). Không chạy agent.

```markdown
[Danh sách thành viên và việc mỗi người làm — copy bảng từ README]
| Họ và tên | Mã học viên | Việc đã làm |
|---|---|---|
| Phạm Tuấn Cường | 2A202603584 | §1: xác định lát cắt và phạm vi. §5: xây dựng prototype, minh hoạ nguyên tắc HAX/PAIR và mức tự chủ trên giao diện. |
| Bùi Xuân Thành | 2A202603521 | §2: xây dựng kịch bản rủi ro, chọn hai ca nguy hiểm nhất. §3: thiết kế cách AI xử lý khi sai, câu trả lời, bước tiếp theo và nguyên tắc HAX/PAIR. |
| Nguyễn Minh Đạt | 2A202603582 | §4: xác định mức tự chủ cho từng tool và lập luận lựa chọn. §6: xây dựng tiêu chí Pass/Fail, kiểm tra hai ca nguy hiểm nhất và ghi nhận lỗi còn lại. |

## §1. Lát cắt & phạm vi
**Lát cắt:** Trong **Đặt chỗ của tôi**, khi **hành khách** vừa nhận tin chuyến bay bị huỷ và nhắn hỏi, **AI đề xuất và giữ chỗ chuyến thay thế, hỏi lại cho rõ, đổi vé, hay chuyển nhân viên**, để khách tới nơi kịp mà không mất vé hay tiền vì một thao tác không đảo lại được.
**Ba việc không làm:**
1. Không đổi tên hành khách: bộ tool không hỗ trợ; yêu cầu được chuyển nhân viên.
2. Không tự quyết định phương án trẻ nhỏ bay một mình: trường hợp này cần nhân viên kiểm tra điều kiện vận chuyển.
3. Không hứa bồi thường ngoài chính sách dựng: chuyến bị huỷ do thời tiết không có bồi thường tiền mặt.


### Dữ liệu và nguồn sự thật

Nguồn chính là fixture của `tracks/t3-travel.md` trong repo đề; thông tin sản phẩm thật được dùng làm bối cảnh theo tài liệu đề, không phải chính sách hoạt động của prototype.

| Dữ liệu | Giá trị dựng |
|---|---|
| Thời điểm fixture | 15:00 ngày 12/11/2026 |
| Đặt chỗ | TRV-7Q2K · Phổ thông Tiết kiệm |
| Hành khách | Nguyễn Minh An, 34 tuổi; Nguyễn Gia Bình, 5 tuổi |
| Chuyến cũ | BM 213 · Hà Nội → TP.HCM · 12/11/2026 19:00 · huỷ do bão |
| BM 217 | 12/11 21:00 · còn 1 chỗ, không đủ cả hai |
| BM 201 | 13/11 07:00 · còn 9 chỗ |
| BM 205 | 13/11 09:30 · còn 4 chỗ |
| Chính sách dựng | Đổi miễn phí một lần trong 48 giờ hoặc hoàn toàn bộ; không bồi thường tiền mặt do thời tiết |

**Fixture bổ sung R1 do nhóm tự dựng:** minh hoạ trường hợp đã có dữ liệu hoàn để kiểm tra toàn bộ bước duyệt và gửi. Đây không phải dữ liệu do đề hoặc Traveloka cung cấp.

| Trường | Giá trị giả R1 |
|---|---|
| Vé An | 1.200.000 VND |
| Vé Bình | 900.000 VND |
| Phí hoàn | 0 VND |
| Tổng yêu cầu | 2.100.000 VND, cho cả hai hành khách |
| Phương thức thanh toán gốc mô phỏng | Ví TEST-WALLET |
| Thời gian xử lý dự kiến dựng | Tối đa 90 ngày; không phải cam kết dịch vụ thật |
| Hiệu lực báo giá | 10 phút từ lúc mở chi tiết |
| Sau gửi | REF-7Q2K-R1 đang chờ xử lý; không huỷ được yêu cầu, chưa phải tiền đã về |

Mặc định R1 tắt: thiếu dữ liệu thì chặn gửi và chuyển nhân viên. Bật R1 ở bảng demo chỉ đổi fixture, không cho phép bỏ xác nhận. Thông tin không có trong fixture thì AI không được tự khẳng định.


## §2. Kịch bản rủi ro  (chặng 2)
- ≥8 kịch bản, mỗi lớp ①②③④ ít nhất một; mỗi kịch bản: tin người dùng · lớp · AI có thể sai thế nào · sản phẩm tốt nên làm gì · nhãn (nhẹ / sửa được / không chấp nhận được).
- Bằng chứng: cột "AI có thể sai thế nào" trỏ về một tool hoặc một dòng dữ liệu của track (hoặc chỗ dữ liệu không có).
- Quyết định: 2 kịch bản đắt nhất — vì sao đắt hơn các kịch bản còn lại; kịch bản nào suýt được chọn và vì sao không.

## §3. Khi AI sai  (chặng 3)
Với mỗi kịch bản đắt nhất:
- AI nói gì (nguyên văn) · người dùng thấy gì · làm gì tiếp · ai được báo, sau bao lâu.
- Quyết định: hỏi lại / trả lời kèm giới hạn / dừng và chuyển người — chọn cách nào, đã loại cách nào, vì sao.
- Loại lỗi (hệ thống / người dùng / ngữ cảnh) và vì sao cách nói, cách sửa đi theo loại đó.
- 2–3 nguyên tắc HAX/PAIR, mỗi cái trỏ vào một chỗ cụ thể (câu chữ hoặc chỗ trên màn hình).
- Lỗi nào sửa câu chữ không cứu được (nếu có), và thiết kế cứu nó thế nào.

## §4. Mức tự chủ  (chặng 4)
Với mỗi tool:
- Mức của nhóm (tự làm / cần người duyệt / cấm). Nếu cần người duyệt: ai duyệt · người duyệt thấy gì · quá hạn thì sao.
- Lý do theo cost-of-error: sai thì ai chịu gì · đảo lại được không · chờ người thì mất gì.
- Phương án đã cân nhắc và vì sao loại.
Thêm:
- Tool khó xếp nhất: mỗi người từng chọn gì, cái giá của mỗi phía (trỏ về kịch bản ở §2), nhóm chốt thế nào.
- Thử mức đã đặt trên 2 kịch bản đắt nhất + 1 kịch bản bình thường: cái sai có bị chặn không? còn việc nào làm khi lẽ ra phải hỏi? người dùng bình thường có phải chờ vô ích không?
- Luật thêm hoặc tool tách bước (nếu có), và vì sao.
- Một mức tự chủ đã đổi lời hứa nào với người dùng.

## §5. Prototype  (chặng 5)
- Link hoặc file · công cụ · phần nào mock · có lời gọi AI thật không.
- 1–2 ảnh có đánh số; mỗi số: thể hiện gì · nguyên tắc HAX/PAIR nào · mức tự chủ nào.
- Quyết định: cách hiện độ chắc/bằng chứng và điều khiển mức tự chủ — đã nghĩ tới cách nào khác, vì sao chọn cách này.

## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
```
