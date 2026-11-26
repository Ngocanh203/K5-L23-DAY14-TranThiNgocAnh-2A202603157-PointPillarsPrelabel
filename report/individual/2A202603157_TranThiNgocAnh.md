# Báo cáo Day 14 — Trần Thị Ngọc Ánh — 2A202603157

- Mã học viên dùng với `--student`: `157`
- `seed_tag` trong `frames_A.txt`: `393590736f`

## 1. Dự đoán trước sweep (bước 5b)

- Tham số tôi dự đoán sẽ giảm công sửa nhiều nhất: tăng `score_thr` từ `0.1` lên `0.3` và giữ `min_points=0`.
- Lý do: Với cấu hình gốc trên tập A, có 53 hộp cần xóa, 4 hộp cần thêm và 1 hộp cần sửa. Riêng `s03f58` và `s05f24` đã có 46 hộp cần xóa. Tôi dự đoán nâng ngưỡng tin cậy lên `0.3` sẽ giảm số hộp thừa. Tôi giữ `min_points=0` để tránh lọc thêm các hộp của vật thật có ít điểm LiDAR.

## 2. Tập A: sửa tay và tune

| Cấu hình | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| Gốc | 53 | 4 | 1 | 20,4 |
| `best_config.json` | — | — | — | — |

| Frame | Xóa | Thêm | Sửa | Chi phí |
|---|---:|---:|---:|---:|
| `s03f58` | 25 | 1 | 0 | 8,5 |
| `s04f48` | 7 | 0 | 0 | 2,1 |
| `s05f24` | 21 | 3 | 1 | 9,8 |

- Tham số đã đổi trong `best_config.json`: [Điền sau khi sweep]
- Kết quả leave-one-out: [Dán kết quả từ `scripts/pp_sweep.py`]
- Cấu hình có ổn định trên từng frame không? Vì sao tôi vẫn chọn hoặc không chọn cấu hình đó? [Điền sau khi đọc kết quả leave-one-out]

## 3. Trước/sau (bước 8)

<!-- Thay TÊN_FRAME bằng tên ảnh JPG đã tạo rồi bỏ dấu chú thích.
![So sánh cấu hình gốc và sau tune](../../d14_157/compare/TÊN_FRAME.jpg)
-->

- Mức thay đổi chi phí trên tập A: [Điền theo `scripts/pp_compare.py`]
- Đối chiếu dự đoán ở mục 1: [Tự kết luận đúng hay sai, dựa trên số hộp xóa, thêm và sửa]

## 4. Tập B

Số đo trên `d14_157/ref_B.json` sau khi sửa và lưu đủ 12 frame trong CVAT.

| Xóa | Thêm | Sửa | Chi phí |
|---:|---:|---:|---:|
| — | — | — | — |

- Loại box tốn công sửa nhất ở tập B: [Điền theo quan sát khi rà và sửa 12 frame]

## 5. Giới hạn

- Tập A chỉ có 3 frame. Cấu hình có chi phí thấp nhất trên tập A có thể cho kết quả khác trên tập B.
- PointPillars huấn luyện trên KITTI chỉ học trực tiếp ba lớp. Các hộp Truck và Bus cần được kiểm tra lại bằng LiDAR và camera.
- Chi phí sửa là điểm tính theo trọng số của thao tác xóa, thêm và sửa. Bài đo này chưa ghi thời gian thao tác thực tế.