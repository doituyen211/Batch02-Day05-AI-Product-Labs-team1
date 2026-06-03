# Template — Thin SPEC Cuối Day 05

## 1. Track, product/app và user

**Track:** Food & Local Delivery

**Product/app thật:** GrabFood / ShopeeFood

**User cụ thể:**

- Tài xế (người gặp sự cố)
- Khách hàng (người cần giải quyết)

**Nhóm có phải user thật không? Nếu không, khác ở đâu?**  
Có, các thành viên đều là end-user thường xuyên gặp tình trạng bị hủy đơn do lỡ cuộc gọi của tài xế.

---

## 2. Evidence summary

| Evidence                                                             | Nguồn        | User/pain nói lên điều gì?                                          | SPEC phải đổi gì?                                                       |
| -------------------------------------------------------------------- | ------------ | ------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| Đơn hủy vì khách không nghe máy xác nhận đổi món                     | Group Tài Xế | Nút thắt cổ chai nằm ở cuộc gọi điện thoại thủ công                 | Phải làm UI Notification In-app để khách quyết định 1-chạm              |
| Review chửi bới vì tài xế tự đổi trà đào sang trà vải (khách dị ứng) | App Store    | Đổi món sai sở thích/dị ứng gây hậu quả nặng nề hơn cả việc hủy đơn | AI không được phép đoán mò. Phải có cơ chế Failure/Veto (Trừ điểm về 0) |

---

## 3. Pain statement

User **[Tài xế và Khách hàng]** đang gặp khó ở **[bước xử lý sự cố hết món tại quán]**,  
vì **[hệ thống hiện tại bắt buộc phải gọi điện thoại thủ công]**,  
dẫn tới **[tài xế lãng phí thời gian chờ, khách hàng dễ bị hủy đơn oan nếu bận họp]**.

Bằng chứng chính là **[hàng loạt review 1 sao phàn nàn về việc giao thiếu món hoặc hủy đơn không báo trước]**.

---

## 4. Build slice

Cho **[Khách hàng] đang [chờ giao đơn Food Delivery]**,  
prototype sẽ dùng AI để **[automate đổi món tự động hoặc augment gợi ý lựa chọn in-app tùy theo Confidence Score]**,  
tạo ra **[Push Notification UI cho khách xác nhận trong 30s–60s]**,  
và xử lý **[failure mode - AI không tìm được món phù hợp]** bằng **[mitigation - Dừng AI và nhường quyền cho Tài xế gọi điện như cũ]**.

---

## 5. Auto/Aug decision

**Chọn một:**

[x] Conditional automation: AI tự làm trong case hẹp; case mơ hồ/rủi ro chuyển người.

**Lý do chọn:**  
Sự an toàn về thực phẩm (ăn chay, dị ứng, khẩu vị cay/ngọt) rất quan trọng. AI chỉ được tự làm khi tự tin >90% (vd: hết Coca đổi Pepsi).

**Human role:**

- Khách hàng: reviewer (nếu AI auto), decider (nếu AI augment)
- Tài xế: rescuer (nếu AI failure)

---

## 6. Four paths

| Path           | Prototype phải thể hiện gì?                                                                            |
| -------------- | ------------------------------------------------------------------------------------------------------ |
| Happy          | Giao diện khách hàng tự động đổi sang món thay thế phù hợp nhất (Auto-swap). Có nút Undo đếm ngược 30s |
| Low-confidence | UI hiển thị danh sách 2 món do AI lọc ra, yêu cầu khách chạm để chọn (Augment)                         |
| Failure        | UI khách hàng nhảy popup: "Món hết, tài xế đang gọi...". UI tài xế nhận lệnh: "Yêu cầu gọi điện"       |
| Correction     | Khi khách bấm Undo ở Happy Path, log JSON ghi nhận "User X không thích Pepsi" để nạp lại vào Rule DB   |

---

## 7. Failure mode nguy hiểm nhất

Nếu user **[gọi món Chay (Salad) nhưng quán chỉ còn đồ Mặn (Thịt)]**,  
AI có thể **[failure: gợi ý đổi sang đồ mặn do bằng giá tiền]**,  
hậu quả là **[impact: xúc phạm tín ngưỡng ăn chay, mất khách vĩnh viễn]**.

Prototype sẽ xử lý bằng **[fallback: Trong prompt quy định Rule VETO trừ 100 điểm nếu sai tag dietary. AI sẽ lập tức nhả quyền để tài xế gọi điện (human fallback)]**.

Owner kiểm thử path này là **[Tên thành viên]**.

---

## 8. Owner plan cho sáng Day 06

| Thành viên      | Việc phụ trách      | Bằng chứng cần có trong repo                       |
| --------------- | ------------------- | -------------------------------------------------- |
| Đới Trọng Tuyển | Research / evidence | `evidence-pack.md`, `app-teardown.md` hoàn thiện   |
| Đới Trọng Tuyển | SPEC & Prompting    | `thin-spec.md` và `prompt-test-log.md`             |
| Đới Trọng Tuyển | Prototype (Code)    | Source code Streamlit App (Python) chạy được local |
| Đới Trọng Tuyển | Test / failure path | Video màn hình chứng minh AI đi vào Path Failure   |
| Đới Trọng Tuyển | Demo script / repo  | Slide Deck (HTML) và Narrative trình bày           |
