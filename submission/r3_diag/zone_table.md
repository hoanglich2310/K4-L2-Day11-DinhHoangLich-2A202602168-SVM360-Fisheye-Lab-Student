# Zone table (slice của bạn)

Lệnh `python3 lab11.py model` tự ghi bảng số (cùng cách đếm với `r1_craft/compare.md` và `model_compare.md`); chạy lại lệnh sẽ cập nhật bảng và giữ nguyên phần nhận xét. Bạn chỉ viết mục Nhận xét.

| Zone | n_ref | L missing | L spurious | M missing (`LR_noM` + `R_only`) | M thừa (`LM_noR` + `M_only`) | Lỗi L chính (`what`) |
|---|---:|---:|---:|---:|---:|---|
| center | 4 | 0 | 0 | 2 | 2 | — |
| mid | 9 | 1 | 3 | 2 | 7 | SPURIOUS (2) |
| edge | 7 | 1 | 0 | 1 | 1 | BOX_GEOMETRY (1) |

## Nhận xét

- Zone nào người (L) và model (M) gãy nhiều nhất, dẫn số ở bảng trên: zone **mid** gãy nhiều nhất ở cả hai bên. Với L, mid có 1 thiếu và 3 thừa trên 9 vật của reference (zone center 0 và 0; edge 1 thiếu, 0 thừa). Với M, mid có 2 thiếu và 7 thừa, nhiều hơn hẳn center (2 thiếu, 2 thừa) và edge (1 thiếu, 1 thừa). Riêng edge, lỗi duy nhất của L là BOX_GEOMETRY ở xe đạp (L7 với R3).
- Giả thuyết vì sao (méo fisheye, box lỏng, thiếu `ego_body`, ...) và giới hạn của slice ba frame: lỗi của L ở mid chủ yếu không do méo mà do vật nhỏ sát ngưỡng H=40 (L1 cao 42–44 px, L4 khoảng 45 px là hai ca thừa nghi ngờ, còn người áo hồng cao khoảng 51 px là ca tôi bỏ sót). Lỗi của M chủ yếu là **nhầm class hoặc quy ước**, không phải hình học: xe ba bánh bị gán thành Truck, Car hoặc Bus (4 xe ở 2 frame) và người ngồi xe bị tách thành Pedestrian (4 ca ở 2 frame), nên nhiều box thừa ở mid không chứng minh méo fisheye làm model gãy. Ba lý do khiến kết luận yếu: (1) chỉ 3 frame và 20 vật của reference, mỗi zone chỉ 4–9 vật; (2) zone chỉ là bin r/R, không cho biết vật gần hay xa; (3) teaching reference chưa phải gold, có ca reference và tôi bất đồng mà chưa đủ bằng chứng (xe đạp ở frame 236370, xe tối màu ở frame 258420). Để tách ảnh hưởng của méo với lỗi class cần thêm frame ở cùng zone và một phép so cùng class.
