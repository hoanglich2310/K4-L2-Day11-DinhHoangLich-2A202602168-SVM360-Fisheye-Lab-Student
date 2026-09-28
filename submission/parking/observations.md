# Quan sát vạch ô đỗ

Toạ độ dưới đây tính theo ảnh gốc `parking-lot-core.jpg` (960×720, gốc ở góc trên trái).

- Hai vạch `parking_line` đã vẽ (mô tả vị trí trong ảnh): tôi vẽ ba polyline, hai vạch chính và một vạch phụ.
  1. Vạch sơn dày chéo ở tiền cảnh dưới giữa ảnh, đi từ khoảng (402, 650) xuống (537, 716).
  2. Vạch sơn dày chéo ở tiền cảnh bên phải, đi từ khoảng (694, 621) tới (957, 682).
  3. Vạch phụ mảnh hơn ở bên trái giữa ảnh, từ khoảng (172, 520) tới (250, 559).

  Lý do chọn: hai vạch (1) và (2) song song, cùng bề rộng và cùng góc nghiêng, đặt cách nhau xấp xỉ một bề ngang ô đỗ theo phối cảnh. Đó là dấu hiệu của các vạch chia hai ô liền kề. Vạch (3) cũng cùng góc nghiêng với hai vạch trên. Mỗi polyline chỉ đi theo phần sơn nhìn thấy và dừng đúng chỗ vạch kết thúc.
- Một vạch/dấu sơn hoặc biên **không** vẽ, và vì sao: tôi không vẽ dải sơn ngang dài và mảnh chạy quanh độ cao y ≈ 530–545, từ mép trái ảnh vào tới giữa ảnh. Dải này chạy dọc theo cả hàng thay vì tách từng ô riêng, nên nhiều khả năng là biên hàng đỗ hoặc mép lối xe chạy, không phải vạch chia ô. Tôi cũng bỏ qua các nét sơn ngắn ở rìa dưới trái (khoảng x ≈ 27, y 683–719 và x ≈ 50, y 525–572) vì ảnh cắt cụt nên không đủ dữ kiện để nói chúng chia ô.
- Polygon `free_space` dừng ở đâu; có phần bị che nào không: polygon bao vùng mặt đường trống của lối xe chạy ở giữa ảnh, từ khoảng y = 490 (chưa lên dải bãi sáng ở xa) xuống y ≈ 650 và trải từ x ≈ 250 tới x ≈ 955. Cạnh trên nằm dưới dải mặt đường quá sáng ở xa; cạnh trái bắt đầu từ x = 250 nên chiếc xe đỏ ở xa bên trái (x ≈ 193–220, y ≈ 457–478) nằm ngoài polygon. Không có xe, cây hay vật che nào nằm trong vùng đã vẽ. Cạnh dưới-trái (từ (250, 560) xuống (400, 650)) là đường tôi chọn để giữ polygon trong vùng chắc chắn là lối xe chạy chứ không theo một ranh vật lý nào.
- Ca chưa chắc cần hỏi người soát (nếu không có, ghi “không có”): vẫn chưa chắc hai vạch chéo ở tiền cảnh là vạch chia ô của bãi đỗ xiên góc hay chỉ là vạch hướng dẫn lối đi. Tôi chọn coi chúng là vạch chia ô vì chúng song song và đều nhau. Nếu người soát thấy dấu hiệu ngược lại (ví dụ mũi tên, hướng xe chạy), tôi sẵn sàng bỏ chúng.
