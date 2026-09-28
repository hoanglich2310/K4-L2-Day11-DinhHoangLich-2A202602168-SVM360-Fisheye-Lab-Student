# QA review · B4-edge

Mã khóa: 7913-3425

**Hình thức: cold review.** Chưa có bản khóa của bạn cùng nhóm để soát (Toán chưa gửi kịp), nên tôi soát lại chính slice B4-edge của mình sau khi chờ hơn 5 phút kể từ lúc khóa (khóa 16:56, mở QA 17:01). Đây là soát của cùng một người nên độc lập kém hơn QA chéo; tôi nêu rõ để người đọc cân nhắc. Chỉ dùng luật `docs/02-rules-vi.md` và ảnh gốc; chưa mở teaching reference, model overlay hay worked HTML.

| frame | object_ref | rule_id | nhận xét |
|---|---|---|---|
| adasind_258420.jpg | ngoài file, vùng (178,742)–(248,808) | R01 | Có một xe tối màu hình hộp (nhiều khả năng xe tải) ở phía xa phía sau xe trắng và xe tay ga, cao khoảng 66 px trên ảnh gốc, vượt ngưỡng H=40 nhưng chưa có box. Bị che một phần bởi xe trắng và xe tay ga nên có thể cần `occluded`. Class (Truck hay Bus) cần soát thêm theo R04. |
| adasind_258420.jpg | L3 (Car) | R02 | Box Car (213,773)–(258,815) chỉ ôm phần bên trái. Phần thân xe trắng nhìn thấy còn kéo sang phải tới khoảng x=274, tức thiếu khoảng 16 px bên phải so với phần nhìn thấy. |
| adasind_236370.jpg | L3 (Pedestrian) | R02 | Cạnh trên của box (y=762) cao hơn đỉnh mũ của cậu bé khoảng 10–12 px; box lỏng ở phía trên. Không đổi kết quả gán nhãn, chỉ là độ chặt của box. |
| adasind_310008.jpg | lens_border (2 polygon) | R08 | Mép trên polygon `lens_border` nằm thấp hơn mép vòng kính đo trên ảnh khoảng 45 px (đo ở x=300 và x=540), nên polygon che phần trời nhìn thấy bên trong vòng kính. Không có box nào ở vùng này nên không ảnh hưởng box, nhưng luật R08 yêu cầu soát và sửa điểm lệch. |

Không thấy vi phạm R03 (rider) ở slice này: xe máy và xe tay ga có người ngồi là một `Bike`; cậu bé dắt xe đạp ở frame 236370 tách `Pedestrian` và `Bike`. Không box nào nằm trong `ignore_region` (R09).

Ghi finding r2_qa: cell=L_only, rule_id có giá trị, why để trống.
