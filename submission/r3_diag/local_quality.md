# Đối chiếu chất lượng cục bộ — rectangle

Teaching reference, không phải gold set đã phê duyệt; không có điểm đạt tự động.
Nguồn: export r1_craft đã khóa SHA256 `7913342535f4da3432bf72ed47906bf33d322bdf7aab79e48781aa3dff7c8b10`; slice `B4-edge`.
Ghép hình học greedy một-một theo IoU ≥ 0.50, rồi so class; H ≥ 40 px.
Box trái nằm chủ yếu trong ignore_region reference không tính. Polygon, polyline, track không được chấm.
Đây là phép tính offline của lab, không phải báo cáo hay kết quả tương đương CVAT Premium.

Frame được tính: adasind_236370.jpg, adasind_258420.jpg, adasind_310008.jpg. Frame thiếu trong export: không.
TP=18; FP=3; FN=2; số lần đối chiếu=23; mean IoU của TP=0.782.

| Chỉ số | Micro | Macro | Nhãn thấp nhất |
|---|---:|---:|---:|
| accuracy | 0.783 | 0.957 | 0.870 |
| precision | 0.857 | 0.898 | 0.600 |
| recall | 0.900 | 0.928 | 0.750 |
| jaccard | 0.783 | 0.860 | 0.500 |
| dice | 0.878 | 0.911 | 0.667 |

| Nhãn | TP | FP | FN | Accuracy | Precision | Recall | Jaccard | Dice |
|---|---:|---:|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 2 | 1 | 0.870 | 0.600 | 0.750 | 0.500 | 0.667 |
| Car | 2 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Pedestrian | 8 | 1 | 1 | 0.913 | 0.889 | 0.889 | 0.800 | 0.889 |
| ThreeWheeler | 4 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |
| Truck | 1 | 0 | 0 | 1.000 | 1.000 | 1.000 | 1.000 | 1.000 |

| Frame | TP | FP | FN | Accuracy | Precision | Recall |
|---|---:|---:|---:|---:|---:|---:|
| adasind_236370.jpg | 6 | 1 | 1 | 0.750 | 0.857 | 0.857 |
| adasind_258420.jpg | 7 | 2 | 1 | 0.700 | 0.778 | 0.875 |
| adasind_310008.jpg | 5 | 0 | 0 | 1.000 | 1.000 | 1.000 |

Confusion matrix: hàng = teaching reference; cột = export đã khóa.
`<missing>` là thiếu box; `<extra>` là box thừa. Xem `local_quality_confusion.csv`.

| Reference \ Export | Bike | Car | Pedestrian | ThreeWheeler | Truck | <missing> |
|---|---:|---:|---:|---:|---:|---:|
| Bike | 3 | 0 | 0 | 0 | 0 | 1 |
| Car | 0 | 2 | 0 | 0 | 0 | 0 |
| Pedestrian | 0 | 0 | 8 | 0 | 0 | 1 |
| ThreeWheeler | 0 | 0 | 0 | 4 | 0 | 0 |
| Truck | 0 | 0 | 0 | 0 | 1 | 0 |
| <extra> | 2 | 0 | 1 | 0 | 0 | 0 |

Chi tiết xung đột trong `local_quality_conflicts.csv`; dữ liệu máy đọc trong `local_quality.json`.
Mismatching label đóng góp một FP cho class vẽ và một FN cho class reference; attribute khác được báo riêng.
Micro accuracy đếm mỗi cặp ghép sai class là một lần đối chiếu; Jaccard đếm cả FP và FN.
Macro/worst bỏ nhãn không xuất hiện ở cả hai phía; chỉ số không có mẫu là N/A.
