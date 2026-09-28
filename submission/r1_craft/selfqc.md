# Tự soát


## Checklist thủ công
- [x] Phạm vi H=40 và vật cần vẽ — mọi box cao ≥42 px (nhỏ nhất: Car occluded ở frame 258420 cao 42, Bike xa cao 44). Không thấy vật ≥40 px nào còn thiếu box; các nét nhỏ hơn (người ở xa bên trái frame 258420 cao khoảng 28 px) không box.
- [x] lens_border và ego_body — đã đo mép vòng kính thật ở x=300/540/800 và so với polygon import: lệch từ 6 tới khoảng 46 px ở mép trên và mép dưới giữa ảnh (lớn nhất frame 310008 mép trên, khoảng 46 px); số đo ở mép dưới bên trái (x=300) bị chân/thân người lái che nên không dùng để kết luận. Vùng lệch đều là viền tối hoặc trời, không có box nào ở đó. Giữ nguyên bản import, không vẽ mới (R08). ego_body vẽ ở cả ba frame vì đều thấy chân/dép người lái (R07); cả ba frame của slice này đều không thuộc hai frame ngoại lệ.
- [x] Class sáu nhãn — bốn xe ba bánh (auto-rickshaw) gán ThreeWheeler, không gọi Bus/Truck; xe bán tải nhỏ có bạt gán Truck (R04); xe trắng ở xa gán Car. Không dùng class ngoài bảng sáu class.
- [x] Rider và Bike — xe máy và người ngồi trên xe là một Bike; xe tay ga chở hai người là một Bike. Cậu bé áo xanh đứng bên cạnh xe đạp, tay giữ ghi-đông, chân chạm đất nên tách thành Pedestrian và Bike (R03). Đã sửa một lỗi ở bước này: ban đầu tôi vẽ thêm một box Bike riêng cho bánh trước lớn; phóng to thì đó là bánh trước của chính chiếc xe đạp đỗ, nên đã xóa box trùng và nới box prefill (nửa sau xe) thành một box ôm cả xe.
- [x] Geometry trên ảnh fisheye gốc — box vẽ trên ảnh gốc, không nắn thẳng vật cong. Đã sửa hai box prefill lệch: Pedestrian (299,737,337,844) lệch khoảng 10 px sang trái, Truck nới mép phải và đáy để ôm hết thùng bạt và bánh sau. Polygon K12 của Truck khoét phần người ngồi xe máy che phía trước.
- [x] truncated và occluded — Car ở mép trái frame 236370 truncated (cắt bởi khung ảnh). occluded=true cho: Truck (người và xe máy đứng chắn phía trước thùng), Bike xe đạp (cậu bé và xe máy che một phần), Car trắng và người che ô ở frame 258420, người đi bộ ngoài cùng trái ở frame 310008 (bị người thứ hai che). Hai attribute độc lập, không lẫn.
- [x] Vật thiếu hoặc box trùng — đã loại một box Bike trùng (mảnh bánh trước xe đạp). Các cặp box chồng nhau còn lại (Bike xe máy với Bike xe đạp ở frame 236370; nhóm người đi bộ ở frame 310008) là hai vật khác nhau.
- [x] ignore_region có reason — mỗi frame có 1 polygon ego_body và 2 lens_border, mỗi polygon đúng một reason. Đã kiểm bằng tính toán: tỷ lệ diện tích mỗi box nằm trong ignore_region là 0 ở cả ba frame.
- [x] Tên task raw_fisheye và export CVAT 1.1 — task tên "Day11 · ADASIND · B4-edge · raw_fisheye", export CVAT for images 1.1 theo task, không kèm ảnh.

## Fill ratio (K12)
- adasind_236370.jpg box 6 center: 0.643
- adasind_236370.jpg box 7 mid: 0.600
- adasind_310008.jpg box 1 edge: 0.735
- adasind_310008.jpg box 2 edge: 0.671
mean edge: 0.703 (n=2)
mean center: 0.643 (n=1)
