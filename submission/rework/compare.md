# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_236370.jpg
- L6+R3 edge BOX_GEOMETRY
## adasind_258420.jpg
- L1 mid SPURIOUS
- L5 mid SPURIOUS
- L7 mid SPURIOUS
- L10+R5 mid BOX_GEOMETRY
## adasind_310008.jpg

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 4 | 4 | 0 | 0 |
| mid | 9 | 8 | 1 | 5 |
| edge | 7 | 6 | 1 | 0 |
