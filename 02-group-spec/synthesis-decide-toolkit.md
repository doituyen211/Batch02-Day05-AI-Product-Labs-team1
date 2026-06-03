# Toolkit — Từ Evidence Đến Build Slice

Dùng sau khi nhóm đã có evidence. Mục tiêu là chốt một build slice đủ nhỏ cho Day 06.

---

## 1. Gom evidence thành cụm

- “Tài xế mất thời gian gọi điện cho khách.”
- “Khách hàng lỡ cuộc gọi nên bị hủy đơn oan.”
- “Tài xế tự ý đổi món gây phẫn nộ (vd: đổi đồ chay thành đồ mặn).”

---

## 2. Viết insight

User (khách hàng và tài xế) không chỉ cần **một quy trình giải quyết sự cố thiếu món**,  
họ thật ra cần **một hệ thống giảm thiểu tối đa giao tiếp thủ công nhưng vẫn tôn trọng tuyệt đối ranh giới khẩu vị / dị ứng**,

vì:

- nhiều review cho thấy cuộc gọi vừa phiền vừa dễ thất bại
- tự ý đổi món sai gây mất trust nghiêm trọng
- hệ thống hiện tại không có cơ chế cân bằng giữa speed và safety

---

## 3. Viết opportunity

Cơ hội là dùng AI để:

- phân tích menu + lịch sử user + context đơn hàng
- chấm điểm **Confidence Score cho từng phương án thay thế món**

giúp user:

- hoàn tất đơn hàng mượt mà bằng notification / in-app flow thay vì cuộc gọi

trong khi vẫn kiểm soát:

- failure/risk bằng cách fallback về người thật nếu AI không chắc chắn

---

## 4. Chọn build slice

- **User cụ thể chưa?**  
  → Đạt (Tài xế trigger lỗi, khách hàng nhận xử lý)

- **Task đủ hẹp chưa?**  
  → Đạt (Chỉ focus flow: Tài xế báo hết món → AI xử lý → UI phản hồi khách)

- **AI decision rõ chưa?**  
  → Đạt (AI chọn 1 trong 3 path dựa trên score 0–100)

- **Failure path rõ chưa?**  
  → Đạt (case đặc biệt: đổi món chay ↔ mặn, dị ứng)

- **Có evidence không?**  
  → Đạt (App Store review + cộng đồng tài xế)

---

## 5. Câu chốt cuối

Dựa trên **sự chán nản của tài xế và khách hàng khi phải gọi điện xử lý đơn thiếu món**,  
nhóm sẽ build **Smart Auto-Substitute Engine**,

cho **khách hàng đặt Food Delivery**,  
để giải quyết **thời gian chết và nguy cơ hủy đơn oan**,

bằng cách AI:

- automate việc đề xuất / đổi món hợp lý
- hoặc augment decision qua lựa chọn nhanh trong app

và sẽ test failure path:

- AI phát hiện rủi ro đổi món sai (ăn kiêng / dị ứng) và chuyển quyền quyết định về con người

---

## 6. Backlog (Không build trong Day 06)

- Xử lý hoàn tiền qua ví điện tử
- App thực tế cho tài xế (scan QR, map nâng cao)
- Thuật toán tracking thời gian giao hàng realtime
