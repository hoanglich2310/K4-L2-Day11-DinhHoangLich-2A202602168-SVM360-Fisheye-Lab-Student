# Sensor context

- Rig: dữ liệu ADASIND là một camera fisheye duy nhất, ảnh dọc 1080×1920. Quan sát từ các frame slice `B4-edge` (adasind_236370, 258420, 310008): camera nhìn ra phía trước theo hướng đi, đặt ngang tầm người ngồi trên xe hai bánh (thấy chân/dép của người lái và bóng người lái trên mặt đường). Repo không kèm tài liệu rig, nên tôi chỉ ghi theo quan sát và không suy ra vị trí lắp, độ cao hay thông số calibration.
- `ego_body`: nhìn thấy ở phần đáy và góc dưới trái của khung (chân và dép của người lái, phần thân xe sát đáy). Đây là vùng thuộc xe gắn camera, không phải vật thể cần box. Tôi chỉ vẽ `ego_body` ở frame thực sự thấy phần này.
- Vòng kính (lens circle): là hình tròn/elip lớn gần như phủ hết khung. Theo `assets/frames.csv`, frame 236370 có tâm khoảng (436, 938) và bán kính khoảng 818 px, nên vòng kính bị cắt ở hai mép trái/phải của ảnh và để lại vành đen ở góc trên và dưới. Vật ở sát vành kính bị méo và có thể `truncated`.
- Giới hạn: ba frame của slice này chỉ đại diện một camera, không đại diện bốn camera SVM. Tôi không suy khoảng cách gần/xa của vật từ việc nó nằm ở vùng center/mid/edge.
