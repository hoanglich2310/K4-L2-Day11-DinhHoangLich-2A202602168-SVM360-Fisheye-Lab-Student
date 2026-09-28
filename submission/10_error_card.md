# Error analysis card

## Zone × block

| zone | block | what | count |
|---|---|---|---:|
| center | B4 | MISSING | 2 |
| center | B4 | SPURIOUS | 2 |
| center | C0 | BOX_GEOMETRY | 1 |
| center | C0 | SPURIOUS | 1 |
| edge | B4 | MISSING | 2 |
| edge | B4 | SPURIOUS | 1 |
| mid | B4 | BOX_GEOMETRY | 5 |
| mid | B4 | MISSING | 4 |
| mid | B4 | SPURIOUS | 15 |
| mid | C0 | BOX_GEOMETRY | 1 |
| unknown | B4 | MISSING | 1 |
| unknown | B4 | STRUCTURE | 1 |

## Top defects
- SPURIOUS: 19 (ví dụ frame adasind_019560.jpg)
- MISSING: 9 (ví dụ frame adasind_258420.jpg)
- BOX_GEOMETRY: 7 (ví dụ frame adasind_019560.jpg)

## Phân tích của bạn

Hai bảng trên do `python3 lab11.py card` tính từ `findings.csv`; chạy lại lệnh sẽ cập nhật bảng và giữ nguyên mục này. Viết cho lỗi nổi bật nhất, dẫn frame/`object_ref`.

- Nguyên nhân khả dĩ (`why`) và vì sao bạn nghĩ vậy: lỗi nổi bật nhất là **SPURIOUS ở zone mid** (15 trong 19, ví dụ `adasind_258420.jpg` M4, M8, M11). Phần lớn không phải lỗi của tôi mà là box thừa của model (10 trong 18 dòng SPURIOUS của slice B4), và chúng thuộc hai nhóm `E4_model_domain`: (1) xe ba bánh bị gán Truck, Car hoặc Bus vì model không có class này (4 xe, 5 box: M4, M8, M11 ở 258420; M6 và M7 ở 310008), (2) người ngồi xe bị tách thành Pedestrian trái R03 (M2 ở 236370; M5, M7, M10 ở 258420). Tôi nghĩ vậy vì mẫu lặp qua nhiều vật và hai frame, box model trùng đúng vị trí vật của L và R (IoU cao) nên sai ở class chứ không sai ở hình học. Lưu ý bảng đếm cả các dòng lặp giữa vai r1_craft và r3_diag nên con số lớn hơn số vật thật. Phần lỗi của L trong SPURIOUS chỉ có 3 vật (L1, L4 ở 258420 và L7 ở 236370), cả ba tôi xếp `E5_unresolved` vì sát ngưỡng H=40 hoặc bất đồng về ranh xe đạp, chưa đủ bằng chứng để nói L thừa. Lỗi thật của tôi là ca **MISSING** người áo hồng ở 258420 (R7, `E1_annotator_error`), đã sửa ở P5.
- Cách sửa và ai nhận việc (`owner`): `ai_team` nhận nhóm class xe ba bánh và tách rider (đã escalate ticket 1: thêm class ThreeWheeler hoặc remap, và gộp người với xe hai bánh theo R03 trước khi đưa cho annotator). `qa` và `guideline` nhận phần ngưỡng H sát biên (đề xuất R12 ở `20_guideline_patch.md`). `annotator` (tôi) nhận ca bỏ sót người áo hồng, đã sửa ở `rework/annotations-v2.xml`; các ca `E5` giữ nhãn và kiểm tiếp bằng ảnh gốc chưa làm mờ hoặc frame liền kề.
- Bằng chứng (ảnh trong `screenshots/`, dòng findings, rule): `screenshots/esc_threewheeler_258420.png`, `screenshots/esc_threewheeler_310008.png` (xe ba bánh bị model gán sai), `screenshots/rider_split_258420.png` (người lái bị tách), `screenshots/bike_wheel_236370.png` (ca xe đạp IoU 0.46). Dòng findings r3_diag: `L6+R8`, `L5+R4`, `L7+R1`, `M4`, `M8`, `M11` (258420), `L5+R1`, `M6`, `M7` (310008), `M2`, `M5`, `M7`, `M10`; các luật liên quan R04, R03, R01, R02.
