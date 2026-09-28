# Escalation ticket

## Ticket 1

- **Frame:** `adasind_258420.jpg` (các cặp `L5+R4`, `L6+R8`, `L7+R1`; box model M8 Truck, M11 Car, M4 Truck) và `adasind_310008.jpg` (cặp `L5+R1`; cùng một box model bị gán hai class M6 Truck và M7 Bus).
- **Ảnh chụp:** `submission/screenshots/esc_threewheeler_258420.png` và `submission/screenshots/esc_threewheeler_310008.png` (xanh lá = nhãn của tôi, xanh dương = teaching reference, đỏ = model).
- **Expected impact:** Model pre-label không có class xe ba bánh nên gán cả 4 xe ba bánh của hai frame vào Truck, Car hoặc Bus (5 box model). Đây là 4 trên 20 vật của reference ở slice này (20%), và là nguyên nhân của 5 trong 10 box thừa của model trong `findings.csv`. Nếu annotator nhận pre-label và nhận nguyên, nhãn sẽ sai class ở đúng loại phương tiện phổ biến nhất trong cảnh; các thống kê Truck, Car, Bus của báo cáo chất lượng sẽ bị thổi phồng FP và ThreeWheeler bị thiếu FN. Vì mẫu lặp ở hai frame và bốn vật, đây không phải một box lệch ngẫu nhiên.
- **Owner:** `ai_team`
- **Recommendation:** (1) Thêm class ThreeWheeler vào taxonomy của model và tinh chỉnh trên một tập nhỏ xe ba bánh đã gán đúng theo R04 (ghép auto-rickshaw, e-rickshaw, xích lô). (2) Trong lúc chờ, thêm bước hậu xử lý: box model trùng vị trí (IoU cao) với một xe ba bánh mà bị gán Truck, Car hoặc Bus thì đánh dấu "cần soát" chứ không tự nhận. Đầu ra hai class cho cùng một box (M6 Truck và M7 Bus) nên được loại bỏ hoặc chỉ giữ class điểm cao nhất. (3) Phép kiểm sau khi sửa: chạy lại `python3 lab11.py local-quality` và `python3 lab11.py model` trên cùng ba frame, kỳ vọng các dòng `LR_noM` của xe ba bánh biến mất và ma trận nhầm lớp không còn ô ThreeWheeler → Truck/Car/Bus. Cần thử thêm trên camera khác vì bằng chứng hiện chỉ từ một camera.
