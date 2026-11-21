# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Hải Nam        Người kiểm (học viên): Nguyễn Hữu Lộc  
Ngày: 2026-11-21                               Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `NguyenHaiNam-front.zip` (CVAT task 19, export 2026-11-20 11:55 UTC; không kèm manifest nên không có `revision`)  
Số ảnh kiểm: 6 (A01, A02, A03, A04, A06, A07) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 66 (46 shape + 20 tag)

> Ghi chú phạm vi: lô nhận được chỉ có file front. Ngoài 6 ảnh mẫu, lint cho thấy A08–A12 chưa có nhãn nào và không có file fisheye (xem QC1-12).

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 1 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 2 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 18 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 18 | 2 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 18 | 3 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 18 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 15 | 0 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 13 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 5 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 1 | 2 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-01 | A07 | tag camera | nặng | Ảnh không có tag camera (phải là `front`) |
| 2 | QC1-01 | A07 | tag timeofday, weather, source | nhẹ | Thiếu ba tag còn lại (tính 1 dòng, 3 tag) |
| 3 | QC1-02 | A06 | lane L1 | nặng | Không có polyline lane nào; ảnh có vạch vàng liền bên trái làn mình (người kiểm đã gán L1 ở cùng ảnh) |
| 4 | QC1-02 | A07 | lane R1 | nặng | Không có R1; ba polyline đều để L1 |
| 5 | QC1-03 | A07 | lane #1–#3 | nặng | Ba vạch cùng `position = L1`; ít nhất một vạch là R1/R2 |
| 6 | QC1-04 | A03 | lane #2 (R1) | chính | Vẽ từ xa về gần (điểm đầu y=366, điểm cuối y=647) |
| 7 | QC1-04 | A03 | lane #3 (R1) | chính | Vẽ từ xa về gần (điểm đầu y=386, điểm cuối y=581) |
| 8 | QC1-05 | A03 | lane #2, #3 (R1) | chính | Một vạch đứt R1 bị tách thành 2 polyline |
| 9 | QC1-05 | A04 | lane L1 (3 polyline) | chính | Vạch vàng đôi L1 bị tách thành 3 đoạn, có đoạn để `dashed` |
| 10 | QC1-05 | A01 | lane L2 (2 polyline) | chính | Hai polyline cùng L2 (vàng liền đơn và trắng liền đôi), một vạch sai position hoặc bị tách |
| 11 | QC1-12 | A08–A12 | image | nặng | 5/12 ảnh bắt buộc chưa có nhãn nào; không có file `-fisheye.zip` |
| 12 | QC1-12 | lô | file | nhẹ | Không kèm `<tên>-manifest.json` |

> Dòng 1, 2, 6, 7, 11, 12 đọc thẳng từ file nên chắc chắn. Dòng 3, 4, 5, 8, 9, 10 lấy từ cảnh báo lint và thuộc tính trong XML; người kiểm phải mở ảnh trên CVAT xác nhận trước khi gửi phiếu.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Lint báo thiếu L1 và R1; đường không thấy vạch kẻ rõ. Có được miễn QC1-02 không? | |
| A04 | Vạch vàng đôi có một bên đứt: `style` nên là `solid` hay `dashed`? | |

## Quyết định
Lỗi nặng: 5   Lỗi chính: 5 / 66 nhãn = 7,6 %   Lỗi nhẹ: 2   Ca chờ lead: 2  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có lỗi nặng (A07 thiếu tag camera, thiếu L1/R1 ở A06/A07, A08–A12 chưa gán, thiếu file fisheye), nên Rework ngay. Tỉ lệ lỗi chính 7,6 % cũng vượt 5 %. Hai ca mơ hồ không làm đổi kết luận nên không Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
