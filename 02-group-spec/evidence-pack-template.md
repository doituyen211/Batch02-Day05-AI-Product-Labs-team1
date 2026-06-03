# Template — Evidence Pack

## 1. Nhóm và track

**Tên nhóm:** team1
**Track:** Food & Local Delivery  
**Product/app đã chọn:** GrabFood / ShopeeFood

**Build slice đang nghĩ:**  
Smart Auto-Substitute Engine (Xử lý sự cố hết món tự động bằng AI Confidence Score).

---

## 2. Self-use evidence

| Observation                                                                                                                       | Screenshot/link                | Path liên quan | Điều học được                                                                                                      |
| --------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ | -------------- | ------------------------------------------------------------------------------------------------------------------ |
| Bản thân đang họp, đặt Highland Coffee. Quán hết bánh mỳ thịt nướng. Tài xế gọi không được nên hủy luôn nguyên đơn (cả cốc cafe). | (Lịch sử đơn hàng bị hủy)      | Failure        | Sự cố "Hết 1 món nhỏ" có thể phá hủy "Toàn bộ giá trị đơn hàng". Việc bắt khách nghe điện thoại là UX tồi.         |
| Tài xế phải đứng bấm điện thoại, tranh cãi với chủ quán xem nên đổi món gì cho khách.                                             | (Quan sát thực tế tại quán ăn) | Low-confidence | Tài xế không có data về sở thích của khách để gợi ý đổi món. AI có thể làm việc này tốt hơn dựa vào lịch sử order. |

---

## 3. User / review / social evidence

| Quote / review / observation                                                                       | Nguồn                     | User là ai?     | Pain/failure mode                                                                                                        |
| -------------------------------------------------------------------------------------------------- | ------------------------- | --------------- | ------------------------------------------------------------------------------------------------------------------------ |
| "App tệ, tài xế tự ý đổi ly trà đào của tôi thành trà vải mà không hỏi ý kiến, tôi bị dị ứng vải!" | App Store Review (Grab)   | Khách hàng      | Tài xế tự quyết đổi món (Manual Rule) dẫn đến vi phạm dietary (dị ứng). Cần AI có fail-safe (Trừ 100 điểm nếu sai tags). |
| "Mỗi lần quán hết món là xác định chuyến đó chạy không công vì chờ khách nghe máy mất 10 phút."    | Group FB Tài xế công nghệ | Tài xế (Driver) | Bottleneck thời gian chờ đợi.                                                                                            |

---

## 4. Competitor / analog evidence

| App / mô hình tham khảo | Họ xử lý task này thế nào?                                                                                        | Pattern học được                                                           | Có áp dụng trong 1 ngày không?                                                  |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| UberEats (US)           | Cho phép khách chọn sẵn "Substitute Preference" (Ví dụ: Nếu hết thì Hủy/Đổi món A/Tài xế tự chọn) lúc thanh toán. | Đẩy trách nhiệm dự đoán cho khách hàng lúc đặt đơn → làm dài flow checkout | Không nên bắt chước. Ta dùng AI xử lý real-time lúc sự cố xảy ra sẽ mượt UX hơn |

---

## 5. Evidence → Insight

**Evidence nổi bật nhất:**  
Cả tài xế và khách hàng đều sợ những cuộc điện thoại phát sinh khi quán hết đồ. Nhưng khách cũng cực kỳ ghét việc bị tự ý đổi món sai sở thích/dị ứng.

**Insight:**  
User (Khách) không chỉ cần **[được thông báo khi hết món]**,  
họ thật ra cần **[giữ được quyền kiểm soát bữa ăn của mình một cách nhanh gọn nhất]**,  
vì **[việc tự ý đổi món mặn/chay, hoặc gọi điện phiền hà đều dẫn đến rớt đơn]**.

**Opportunity:**  
AI có thể giúp bằng cách:

- [tính toán độ phù hợp của menu còn lại để tự động đổi món hoặc cho khách chọn nhanh 1-chạm]
- giúp user [nhận được đồ ăn thay thế tốt nhất mà không cần nghe điện thoại]
- trong khi vẫn kiểm soát [failure/risk bằng cách bắt buộc tài xế gọi điện nếu AI điểm thấp]

---

## 6. Evidence đổi SPEC như thế nào?

[x] Đổi Auto/Aug decision  
[x] Đổi failure mode

**Trước evidence, nhóm định:**  
Bắt AI tự động đổi món (Auto-swap 100%) trong mọi trường hợp.

**Sau evidence, nhóm đổi thành:**  
Dùng Conditional Automation:

- Tự động đổi nếu Conf > 90%
- Bắt khách chọn trên app nếu 50–89%
- Gọi điện nếu < 50%

**Lý do:**  
Phát hiện rủi ro nghiêm trọng về dị ứng / ăn chay. Không thể để AI quyết định bừa nếu dữ liệu không chắc chắn.
