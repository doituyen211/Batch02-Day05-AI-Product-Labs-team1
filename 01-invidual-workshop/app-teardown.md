# Template — Thin SPEC Cuối Day 05

---

## 1. Track, product/app và user

**Track:** Food & Local Delivery

**Product/app thật:** GrabFood / ShopeeFood

**User cụ thể:**

- Tài xế (người gặp sự cố)
- Khách hàng (người cần giải quyết đơn hàng)

**Nhóm có phải user thật không? Nếu không, khác ở đâu?**  
Có. Các thành viên đều là end-user thường xuyên sử dụng food delivery và từng gặp tình huống bị hủy đơn do lỡ cuộc gọi của tài xế hoặc quán hết món.

---

## 2. Evidence summary

| Evidence                                                     | Nguồn        | User / pain nói lên điều gì?                             | SPEC phải đổi gì?                                                              |
| ------------------------------------------------------------ | ------------ | -------------------------------------------------------- | ------------------------------------------------------------------------------ |
| Đơn bị hủy vì khách không nghe máy xác nhận đổi món          | Group tài xế | Nút thắt cổ chai nằm ở cuộc gọi điện thoại thủ công      | Phải làm UI notification in-app để khách quyết định 1-chạm                     |
| Review chửi vì tài xế tự đổi trà đào sang trà vải gây dị ứng | App Store    | Đổi món sai gây hậu quả nghiêm trọng hơn cả việc hủy đơn | AI không được đoán mò → cần cơ chế failure / veto (score = 0 → human fallback) |

---

## 3. Pain statement

User **(tài xế và khách hàng)** đang gặp khó ở **bước xử lý sự cố hết món tại quán**,  
vì **hệ thống hiện tại bắt buộc phải gọi điện thoại thủ công**,  
dẫn tới:

- tài xế mất thời gian chờ và xử lý
- khách hàng dễ bị hủy đơn oan nếu đang bận / không nghe máy

Bằng chứng chính là **hàng loạt review 1 sao và phản ánh từ cộng đồng tài xế về giao thiếu món hoặc hủy đơn không rõ lý do**.

---

## 4. Build slice

Cho **khách hàng** đang **chờ giao đơn food delivery**,  
prototype sẽ dùng AI để:

- automate việc đổi món khi đủ chắc chắn
- hoặc augment bằng cách gợi ý lựa chọn trong app theo confidence score

Tạo ra:

- **Push notification UI cho khách xác nhận trong 30–60 giây**

Xử lý failure mode:

- nếu AI không tìm được phương án phù hợp → **nhường quyền cho tài xế gọi điện như hiện tại**

---

## 5. Auto/Aug decision

☑ **Conditional automation**

**Lý do chọn:**

- Rủi ro về thực phẩm (dị ứng, ăn chay, tôn giáo, khẩu vị) rất cao
- AI chỉ được tự động hóa khi confidence > 90%
- Case còn lại phải chuyển sang human hoặc augment

**Human role:**

- Khách hàng: reviewer (khi AI auto), decider (khi AI augment)
- Tài xế: rescuer (khi AI failure)

---

## 6. Four paths

| Path           | Prototype phải thể hiện gì                                             |
| -------------- | ---------------------------------------------------------------------- |
| Happy          | AI auto-swap sang món phù hợp nhất. Có nút Undo trong 30s              |
| Low-confidence | UI hiển thị 2–3 món AI lọc ra → khách chọn 1 tap                       |
| Failure        | Popup: “Món hết, tài xế đang gọi…” + trigger call flow                 |
| Correction     | Nếu user undo → log event vào system (ví dụ: “user không thích Pepsi”) |

---

## 7. Failure mode nguy hiểm nhất

Nếu user **đặt món chay (salad)** nhưng quán chỉ còn **món mặn (thịt)**,  
AI có thể:

- sai lầm khi ưu tiên “giá trị tương đương” thay vì dietary rule

Hậu quả:

- vi phạm chế độ ăn chay / dị ứng
- mất trust vĩnh viễn với user

**Giải pháp trong prototype:**

- Rule VETO: nếu sai dietary tag → trừ 100 điểm confidence → không được auto-swap
- lập tức chuyển sang human fallback (tài xế gọi điện)

Owner kiểm thử path này: **[Tên thành viên]**

---

## 8. Owner plan cho sáng Day 06

| Thành viên      | Việc phụ trách      | Bằng chứng cần có trong repo      |
| --------------- | ------------------- | --------------------------------- |
| Đới Trọng Tuyển | Research / evidence | evidence-pack.md, app-teardown.md |
| Đới Trọng Tuyển | SPEC & Prompting    | thin-spec.md, prompt-test-log.md  |
| Đới Trọng Tuyển | Prototype (Code)    | Streamlit/Python app chạy local   |
| Đới Trọng Tuyển | Test / failure path | Video demo AI vào failure path    |
| Đới Trọng Tuyển | Demo script / repo  | Slide deck + narrative trình bày  |
