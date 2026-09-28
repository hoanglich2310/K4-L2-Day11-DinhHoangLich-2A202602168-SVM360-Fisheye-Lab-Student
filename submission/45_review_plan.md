# Kế hoạch review từ lỗi quan sát được

Từ `findings.csv` và `zone_table.md`, chọn **hai lát cắt của bài ADASIND một camera** cần review trước. Bảng này
giải thích dữ liệu thật bạn vừa làm; nó không thay cho kế hoạch bốn camera giả lập ở `45_sampling_plan.csv`.

| Lát cắt / frame | Số ca và loại lỗi | Vì sao review trước | Bằng chứng cần giữ |
|---|---|---|---|
| `adasind_258420.jpg`, zone mid (vật nhỏ ở xa, cảnh đông) | Nhiều dòng nhất của slice: 14 dòng `r3_diag` và 3 dòng `r1_craft`. Gồm 1 ca bỏ sót do tôi (người áo hồng, E1, đã sửa), 2 ca sát ngưỡng H=40 chưa quyết (L1, L4, E5), 1 xe tối màu mà reference không có, box Car của reference ngắn hơn phần nhìn thấy, và các lỗi class của model (xe ba bánh, tách rider). | Có lỗi thật của người gán duy nhất được tìm thấy ở P4, lại tập trung nhiều vật nhỏ sát H nơi guideline chưa rõ (R12). Số ca lớn nhất nên review đúng slice này sẽ cho nhiều thông tin nhất trên mỗi lần soát. | `screenshots/esc_threewheeler_258420.png`, `screenshots/rider_split_258420.png`, dòng findings `R7`, `L1`, `L4`, `L3` (QA), `rework/delta.md`. |
| `adasind_236370.jpg`, ranh xe đạp và xe máy ở giữa và rìa | 4 dòng: `L7+R3`, `L7`, `R3+M8` (cùng một bất đồng, IoU 0.46) và `M2` (rider bị tách). Đều xếp `E5_unresolved` hoặc `E4`. | Đây là bất đồng lớn nhất giữa tôi, reference và model mà **luật không phân xử được**: bánh lớn thuộc xe đạp hay xe máy. Nếu không review thì cả reference lẫn nhãn của tôi có thể sai mà không ai biết. | `screenshots/bike_wheel_236370.png`, dòng findings `L7+R3`, decision log D02, và ảnh gốc chưa làm mờ hoặc frame liền kề nếu lấy được. |

Giới hạn của kết luận từ ba frame ADASIND: chỉ một camera, ba frame và 20 vật của reference, mỗi zone chỉ 4–9 vật; không đủ để nói tỷ lệ lỗi hay so sánh camera. Hai lát cắt được chọn theo **số ca và mức mơ hồ** chứ không theo rủi ro an toàn. Teaching reference chưa phải gold nên có ca reference hụt (R5, xe tối màu). Phần QA là cold review của cùng một người nên độc lập kém hơn QA chéo, và người soát cần xem ảnh chứ không chỉ đọc bảng.

## Chuyển sang kế hoạch bốn camera giả lập

Cách soát độ phủ của 200 frame ở `45_sampling_plan.csv`: nhóm các frame theo cảnh hoặc khoảng thời gian liên tiếp và coi một cảnh là một đơn vị độc lập, không đếm nhiều frame liền nhau trong cùng cảnh như nhiều ca độc lập; với mỗi camera × normal/hard kiểm số cảnh khác nhau, điều kiện sáng, và các bin kích thước vật (đặc biệt vật sát H) chứ không chỉ số frame. Sau đó xem bảng camera × zone × class để tìm ô còn trống (ví dụ camera trái ít vật nhỏ ở rìa) và bổ sung. Kế hoạch này chỉ giúp **tìm ca cần soi**, chưa đo được tỷ lệ lỗi: mẫu chọn nghiêng theo rủi ro nên lệch so với phân bố thật, muốn ước lượng tỷ lệ lỗi phải có thêm một mẫu ngẫu nhiên riêng, và kết quả từ ADASIND một camera không suy sang ba camera còn lại.
