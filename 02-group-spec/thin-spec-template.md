# Workshop — Mổ App AI Thật

**Thời gian:** 45 phút  
**Hình thức:** Cá nhân  
**Người thực hiện:** [Tên của bạn]

---

## 1. Chọn một sản phẩm để dùng thử

| Sản phẩm          | AI feature                                                | Cách truy cập                                         |
| ----------------- | --------------------------------------------------------- | ----------------------------------------------------- |
| Grab / ShopeeFood | Flow xử lý sự cố “Hết món” hiện tại (Rule-based / Manual) | App Grab/ShopeeFood → Đặt đơn → Giả định quán hết món |

**Ghi chú:**  
Vì các app Food Delivery ở VN hiện chưa có AI xử lý luồng này, bài mổ này sẽ phân tích điểm gãy của flow manual hiện tại để chứng minh sự cần thiết của AI product định làm.

---

## 2. Dùng thử: promise vs reality

**Product hứa gì?**  
Giao đồ ăn nhanh chóng, tiện lợi, không phiền hà.

**User nào được hứa sẽ được giúp?**  
Người bận rộn đang làm việc, sinh viên, người dùng phổ thông.

**Kỳ vọng làm được task nào?**  
Đặt xong là rung đùi chờ đồ ăn tới, không phải can thiệp.

### Khi dùng thật, điểm gãy xuất hiện ở đâu?

- Quán hết nguyên liệu sau khi tài xế tới nơi
- App bắt tài xế phải gọi điện cho khách để thỏa thuận đổi món
- Khách đang họp / đang đi xe → lỡ cuộc gọi

**Hậu quả:**

- Đơn bị hủy (tài xế mất công)
- Hoặc tài xế tự ý giao thiếu món (khách bực mình)

**Evidence:**

> Review thật trên App Store:  
> “Tôi đặt combo gà rán mà hết nước ngọt, tài xế gọi không được nên tự ý hủy luôn đơn của tôi bắt tôi đợi 40 phút không có gì ăn.”

---

## 3. Vẽ 4 paths (As-is: Tình trạng hiện tại của App)

| Path           | Câu hỏi cần trả lời     | Tình trạng hiện tại của ShopeeFood/Grab                                                 |
| -------------- | ----------------------- | --------------------------------------------------------------------------------------- |
| Happy          | Khi mọi thứ trơn tru?   | Quán có đủ đồ → Tài xế lấy → Giao xong                                                  |
| Low-confidence | Khi có sự cố (hết món)? | Hệ thống đẩy 100% rủi ro cho tài xế. Tài xế phải gọi điện giải quyết với khách          |
| Failure        | Khi gọi điện thất bại?  | Tài xế hủy đơn (“Không liên lạc được khách” / “Quán hết món”). Cả 2 phía đều chịu UX tệ |
| Correction     | Khi user phàn nàn?      | Gọi CSKH xin voucher đền bù (chi phí vận hành cao)                                      |

---

## 4. Viết finding thành quyết định

Thay vì viết:

> “Quy trình đổi món của app hiện tại quá tệ và mất thời gian.”

Viết lại thành product insight:

Khi user (tài xế) **bấm nút báo quán hết một món**,  
Product hiện tại **bắt buộc tài xế gọi điện thoại thủ công**,  
Hậu quả là **tài xế mất 3–5 phút chờ đợi, khách dễ lỡ cuộc gọi dẫn đến hủy đơn oan**,  
Lỗi thuộc layer **UX Recovery / Workflow Design**.

### Nên sửa bằng:

**Conditional Automation AI:**

- AI tự động phân tích menu để auto-swap món phù hợp
- Hoặc bắn push notification cho khách chọn nhanh trong app
- Chỉ dùng human (call) như fallback cuối cùng

---

## 5. Sketch as-is / to-be

### As-is (Hiện tại)

Tài xế tới quán → Quán báo hết món → Tài xế mở app lấy số → Gọi điện → Khách không nghe máy → Chờ 5 phút → Hủy đơn → UX tệ

---

### To-be (Đề xuất có AI)

Tài xế tới quán → Bấm “Hết món Pizza Bò” trên app →  
AI Engine tính confidence score →

- **> 90%:** Tự động đổi sang Pizza Gà + notify khách → Xong
- **50–89%:** App khách bật popup chọn (Pizza Gà / Mỳ Ý) → 1 tap → Xong
- **< 50%:** Gọi điện như hiện tại (fallback)

---

## 6. Tự kiểm trước khi nộp

- [x] Có screenshot / observation cụ thể
- [x] Có đủ 4 paths
- [x] Finding được viết thành product decision
