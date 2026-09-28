# Rework delta

| zone | matched before | matched after | missing before | missing after | spurious before | spurious after |
|---|---:|---:|---:|---:|---:|---:|
| center | 4 | 4 | 0 | 0 | 0 | 0 |
| mid | 8 | 8 | 1 | 1 | 3 | 5 |
| edge | 6 | 6 | 1 | 1 | 0 | 0 |

## Findings action=rework
- adasind_258420.jpg new@178,742,248,808 MISSING: không áp dụng
- adasind_258420.jpg L3 BOX_GEOMETRY: chưa sửa
- adasind_258420.jpg R7 MISSING: đã sửa
- adasind_258420.jpg R7+M12 MISSING: đã sửa

## Nhận xét của tôi (số trước và sau)

Bản rework khóa với mã 4904-DDBB chỉ sửa 3 ca P1 có căn cứ trên slice B4-edge (frame adasind_258420), đều lấy từ QA và chẩn đoán:

1. **Thêm Pedestrian (92,792,109,843)** (E1, lỗi của tôi): ca này đã sửa, R7 được ghép. Đây là cải thiện thật (missing giảm 1).
2. **Nới box Car** từ (213,773,258,815) thành (211,773,274,814): làm IoU với R5 của reference giảm từ 0.562 xuống 0.41 (dưới ngưỡng 0.5) nên cặp không còn ghép, thành 1 missing và 1 spurious mới. Với model M6 thì IoU là 0.90. Tôi giữ box mới vì phóng to ảnh thấy thân xe trắng còn kéo tới x≈274, nên đây nghiêng về reference ngắn (E0), không phải tôi sai.
3. **Thêm Truck bị che (178,742,248,808)**: reference và model đều không có vật này nên thành 1 spurious mới. Tôi giữ vì vật cao khoảng 66 px vượt H=40 (R01); class Truck hay Bus còn chưa chắc (cần hỏi coach).

**Đọc số:** mid có matched 8→8, missing 1→1, spurious 3→5; center và edge không đổi. Vì vậy số trong bảng **không cải thiện** dù có một lỗi thật đã được sửa: lỗi thật được sửa (+1 matched, −1 missing) bị bù bởi hai bất đồng với reference (Car ngắn và xe tối màu thiếu) nên bảng ở mức kết quả không đổi và spurious tăng 2. Tôi không chỉnh số cho đẹp. Không sửa các ca `E5_unresolved` (xe đạp L7, hai vật sát H=40 L1/L4) vì chưa đủ bằng chứng.

**Giới hạn của phép so:** chỉ 3 frame và 20 vật của reference; ghép greedy theo IoU≥0.5 rất nhạy với một box lệch vài pixel; teaching reference chưa phải gold nên "spurious" ở đây có thể là reference thiếu chứ không phải L thừa.
