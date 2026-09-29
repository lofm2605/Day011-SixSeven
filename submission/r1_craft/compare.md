# So sánh L với R

Chỉ số L/R là thứ tự box cao ≥ H=40 trong từng frame, theo thứ tự XML; bắt đầu từ 1.
Box L trong ignore_region được báo IGNORE_SCOPE, không tính SPURIOUS.

## adasind_249480.jpg
## adasind_261480.jpg
- L2+R6 mid ATTRIBUTE
- L3+R5 mid ATTRIBUTE
## adasind_265065.jpg
- L5 center SPURIOUS
- L6+R3 mid WRONG_CLASS
- R5 mid MISSING
- R6 mid MISSING
- R7 mid MISSING

## Theo zone
| zone | n_ref | matched | missing | spurious |
|---|---|---|---|---|
| center | 4 | 4 | 0 | 2 |
| mid | 13 | 9 | 4 | 0 |
| edge | 0 | 0 | 0 | 0 |
