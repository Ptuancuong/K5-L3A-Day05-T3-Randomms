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
### 5.1. File, công cụ và phần mô phỏng
- File chạy: [prototype/index.html](prototype/index.html).
- Hướng dẫn: [prototype/README.md](prototype/README.md).
- Công cụ: HTML, CSS, JavaScript thuần, AI hỗ trợ viết và kiểm tra code.
- Mở file trực tiếp bằng trình duyệt; không cần cài thư viện, backend, đăng nhập hoặc API key.
- Không có lời gọi AI thật. Ô chat phân loại bằng quy tắc dựng, nút ca thử cung cấp K1–K9. Đây không phải chatbot hiểu ngôn ngữ tổng quát.
- Tra cứu, giữ/nhả chỗ, đổi, gửi hoàn, bàn giao, lỗi và phục hồi đều mô phỏng cục bộ. Số chỗ lấy từ fixture cố định; không có tồn chỗ trực tuyến hoặc nhân viên thật nhận ca.
- Tải lại trang sẽ bắt đầu lại phiên mô phỏng; không có lưu trạng thái giao dịch bền vững.

### 5.2. Bố cục và các nhánh bấm được

**Không gian 1 — hội thoại và phương án:** thanh đặt chỗ cho biết chuyến đã huỷ, hai hành khách và trạng thái hiện tại. Hội thoại bên trái; phương án, chi tiết hoàn hoặc hồ sơ hỗ trợ bên phải. Màn hẹp xếp thành một cột.

**Không gian 2 — xem lại và quyết định:** chi tiết chuyến, người đi, đồng hồ giữ, cảnh báo dùng quyền đổi và nút xác nhận. Nhánh hoàn dùng cùng vùng quyết định, trình bày tiền, nơi nhận, thời gian và xác nhận riêng. Không mở thêm chuỗi trang ngoài phạm vi.

| Nhánh | Cách bấm | Kết quả thiết kế |
|---|---|---|
| K2 | Chọn tin mẫu → BM 201/BM 205 → giữ → xem lại → xác nhận | Không chọn được BM 217 cho cả hai; giữ chưa đổi; đổi sau duyệt |
| Sửa lựa chọn | Giữ → quay lại sửa/bỏ giữ | Nhả lượt giữ mô phỏng, chưa đổi vé, chọn lại |
| Hết hạn | Giữ → bảng demo → cho hết hạn ngay | Khoá xác nhận cũ; phải quay lại kiểm tra và giữ mới |
| K4 thiếu dữ liệu | K4 → xem chi tiết hoàn, R1 tắt | Cảnh báo thiếu dữ liệu; không có gửi hoàn hợp lệ; chuyển người |
| K4 đủ dữ liệu giả | Bật R1 → K4 → chi tiết → đọc → đánh dấu đồng ý → gửi | REF-7Q2K-R1 chờ xử lý; không báo tiền đã về; không huỷ được |
| Ngoài thẩm quyền | Tin đổi tên hoặc trẻ bay một mình | Không thực hiện yêu cầu; lập hồ sơ bàn giao |
| K9 | Sau đổi → báo đổi nhầm | Chuyển người, không hứa hoàn tác |
| Lỗi hệ thống | Chọn tình huống demo trước xác nhận | Hết chỗ/lỗi đọc thì chưa đổi; kết quả chưa rõ thì khoá gửi lặp và tra lại |
| Ca lạ | Nhập câu chưa được nhận diện | Hỏi rõ hướng hỗ trợ; không tự đổi/hoàn chỉ vì chưa hiểu |

Ca lạ dùng phân loại theo quy tắc nên vẫn có thể nhận diện thiếu hoặc nhầm. Các bước đổi/hoàn tiếp tục có kiểm tra và xác nhận riêng. Không khẳng định prototype xử lý được mọi câu nhập.

### 5.3. Bằng chứng và nguyên tắc trên màn hình

| Dấu | Vị trí cụ thể | Nguyên tắc | Mức tự chủ thể hiện |
|---|---|---|---|
| ① | Thẻ BM 217: một chỗ cho hai hành khách | G11: giải thích căn cứ | Chặn phương án không đủ chỗ |
| ② | Câu AI hỏi lại K2/K4 trong hội thoại | G10: thu hẹp phạm vi khi chưa rõ | Chưa tự đổi hoặc gửi hoàn |
| ③ | Nút quay lại sửa/bỏ giữ; quay lại xem chuyến ở nhánh hoàn | G9: sửa trước hành động | Nhả giữ được; xác nhận cũ không còn hiệu lực |
| Cảnh báo và nút duyệt | Màn xem lại chuyến/chi tiết hoàn R1 | G11 và G9 | Cần khách duyệt hành động khó đảo |
| Hồ sơ chuyển | Lý do, trạng thái và lịch sử gửi kèm | Đường lui khi ngoài phạm vi | Chỉ tạo yêu cầu mô phỏng, chưa phải người đã nhận |

**Ảnh minh chứng:

Lưu ở `prototype/screenshots/01-k2.png` và `prototype/screenshots/02-xac-nhan.png`.

### 5.4. Các lựa chọn giao diện và phương án đã loại

- **Hiện căn cứ thay vì % tự tin:** số chỗ, hành khách và trạng thái giúp khách tự kiểm tra; không có dữ liệu để tạo phần trăm tin cậy có ý nghĩa.
- **Tách hội thoại và xác nhận:** chat giúp làm rõ, còn màn xem lại tập hợp quyết định. Loại chỉ dùng nút “Đồng ý” trong chat vì không rõ đang duyệt hành động nào.
- **Giữ chỗ có đồng hồ và nhãn chưa đổi:** tránh khách tưởng vé đã đổi. Loại báo “đã xong” khi mới giữ.
- **Bảng demo tách khỏi luồng chính:** người xem có thể tạo ca lỗi nhưng các công tắc không bị nhầm thành tính năng của hãng thật.
- **Hoàn R1 có nhãn nguồn và xác nhận riêng:** cho thử đầy đủ mà không bịa dữ liệu của fixture gốc. Loại tự điền dữ liệu không ghi nguồn.
- **Không có nút hoàn tác đổi hoặc huỷ yêu cầu hoàn:** hệ thống không có quyền đó; hỗ trợ người là đường phục hồi, không hứa kết quả.


## §6. Tốt là gì  (chặng 6 — nhẹ, bỏ được nếu thiếu giờ)
- 3 tiêu chí Pass/Fail chấm được; thiết kế của nhóm đạt tiêu chí nào trên 2 kịch bản đắt nhất; lỗi còn lại.

## §7. Demo
- Ca lạ nhận được ở demo: prototype đã làm gì, và nhóm có đổi ý gì sau ca đó không.
```
