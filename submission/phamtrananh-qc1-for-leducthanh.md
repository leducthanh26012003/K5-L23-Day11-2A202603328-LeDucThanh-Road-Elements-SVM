# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Lê Đức Thanh (`leducthanh`)        Người kiểm (học viên): Phạm Trần Anh (`phamtrananh`)  
Ngày: 20/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `leducthanh-front.zip`, `leducthanh-fisheye.zip` — revision 1 (`leducthanh-manifest.json`, tạo 20/11/2026 23:38)  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 73

Ảnh kiểm:
- **Front:** A04 (vàng đôi, drivable direct/alternative), A06 (6 đèn, 4 biển), A12 (vạch qua đường, đèn, biển).
- **Fisheye:** B02 (đèn sát mép, edge_zone), B03 (camera sau, lane theo cung), B06 (camera trái, lane `other`).

Phiếu dự thảo do Lê Đức Thanh tự kiểm lô của mình, gửi Phạm Trần Anh xác nhận rồi nộp. Phạm Trần Anh cần mở lại trên CVAT ít nhất 3 lỗi được ghi và ảnh B03 (ghi "không lỗi") trước khi nộp.

Phiếu này kiểm bản revision 1. Lỗi đã được sửa ở revision 2 (`leducthanh-manifest.json` mới), trừ drivable ở B02.

Mỗi ảnh được mở cùng nhãn vẽ chồng lên và so với guideline Road v1.0.
- Số nhãn đã kiểm = 70 nhãn có trong file (24 tag + 46 shape) + 3 nhãn phải có nhưng bị thiếu (R2 ở A04, đèn ở B02, drivable ở B06).
- Ảnh kiểm không thấy lỗi: **B03**.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 1 | nhẹ (tag camera 6/6 đúng; lỗi là tag `weather`) |
| QC1-02 đủ L1, R1 | bỏ sót | 7 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 12 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 12 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 12 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 12 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 18 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 13 | 1 | chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 19 | 3 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 6 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 16 | 0 | chính |
| QC1-12 file | lỗi file | 73 | 0 | nhẹ / nặng |

Cách đếm số mục kiểm:
- **QC1-01:** 4 tag × 6 ảnh.
- **QC1-02:** số vạch L1/R1 phải có, gồm A04 2, A06 2, A12 2, B03 1 (bên trái là lề, không có L1); B02 không có lane, B06 là camera bên.
- **QC1-03 đến QC1-06:** 12 polyline lane, đã tính cả R2 bị thiếu ở A04.
- **QC1-07:** drivable + crosswalk + road_curb.
- **QC1-08:** đèn. **QC1-09:** đèn + biển. **QC1-10:** biển.
- **QC1-11:** mọi shape ở 3 ảnh fisheye.
- **QC1-12:** mọi nhãn.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A12 | `lane` #13 (L1, dashed, white) | nặng | Ở hàng y ≈ 442 đã có `lane` #12 là L1 tại x ≈ 396, sát xe hơn. #13 tại x ≈ 310 là vạch thứ hai bên trái, phải là **L2**. Đang có 3 polyline cùng L1 |
| 2 | QC1-04 | A04 | `lane` R2 (thiếu) | chính | Bỏ sót vạch trắng liền giữa làn bên phải và làn xe đạp, chạy từ khoảng (790, 370) tới (1280, 520). Đây là R2, vạch kế tiếp bên ngoài R1 |
| 3 | QC1-07 | B02 | `drivable` #2 (direct) | chính | Sai phạm vi: polygon chỉ phủ một dải nhỏ phía sau vạch qua đường (y 363–419). Thiếu toàn bộ mặt đường trước xe, gồm vùng vạch qua đường, tới mép thân xe |
| 4 | QC1-07 | B06 | `drivable` (thiếu) | chính | Ảnh không có polygon drivable nào, dù mặt đường cạnh xe thấy rõ. Trọng tâm của slot B06 là "drivable + lane position = other" |
| 5 | QC1-08 | B02 | `traffic_light` (thiếu) | chính | Bỏ sót đèn đỏ ở mép trái, khoảng (45, 363)–(62, 393), cao ≈ 30 px (≥ 8 px). Khi gán: color = red; tâm nằm ngoài 80 % bán kính nên edge_zone = bật |
| 6 | QC1-09 | A06 | `traffic_sign` #3 | chính | Biển ONE WAY (mũi tên trắng nền đen) đang để group = information. Theo bảng nhóm biển phải là **mandatory** |
| 7 | QC1-09 | A12 | `traffic_sign` #5 | chính | Biển ONE WAY đang để group = supplementary, phải là **mandatory**. Biển này là biển chính, không phải tấm phụ dưới biển khác |
| 8 | QC1-09 | A12 | `traffic_sign` #4 | chính | Biển tên đường "Greene St" (xanh lá) đang để group = supplementary. Theo chức năng chỉ dẫn, phải là **information** |
| 9 | QC1-01 | A06 | tag `weather` | nhẹ | Đang để `other`, nhưng phần trời nhìn thấy bên phải (sau hàng rào) trắng xám, mặt đường khô. Nên là `overcast` |

Số id là thứ tự shape trong ảnh của file export (không tính tag), bắt đầu từ 0.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A12 | `lane` #0 (L1, trước vạch qua đường, (14, 533)–(172, 485)) thẳng hàng với #13 ở sau vạch qua đường. Đây là cùng một vạch L2 bị vạch qua đường cắt (gán L2, một hay hai polyline?), hay là L1 của đoạn trước giao lộ? | |
| A06 | Mặt đường dưới gầm đường ray không kẻ vạch và rộng nhiều làn. Có cần polygon `drivable` alternative cho phần đường bên phải vùng direct không? | |
| A12 | `traffic_light` #6 (đèn đi bộ, facing side) đang hiện hình người đi bộ màu trắng. color nên là `green` (đang cho đi) hay `off`? | |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 7 / 73 nhãn = 9,6 %   Lỗi nhẹ: 1   Ca chờ lead: 3  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu):
- Có 1 lỗi nặng (QC1-03 ở A12): một lỗi nặng là đủ để Rework.
- Tỉ lệ lỗi chính là 9,6 % số nhãn đã kiểm, vượt ngưỡng 5 %.
- Ba ca mơ hồ không làm đổi kết luận, vì lô đã phải Rework theo hai luật trên, nên không cần Hold.

Việc cần sửa trước khi nộp lại (revision 2):
- **A12:** đổi #13 thành L2, chốt lại #0 sau khi lead trả lời.
- **A04:** vẽ R2.
- **B02:** vẽ lại drivable direct tới mép thân xe; thêm đèn đỏ ở mép trái.
- **B06:** vẽ drivable.
- **Group biển:** A06 #3 và A12 #5 thành `mandatory`, A12 #4 thành `information`.
- **A06:** đổi `weather` thành `overcast`.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
