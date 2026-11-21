# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Bạn cùng lớp           Người kiểm (học viên): Nguyễn Hải Nam (2A202603309)  
Ngày: 21/11/2026                                Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `peer-front.zip` (revision 1)  
Số ảnh kiểm: 6 (A01–A06)                        Số nhãn đã kiểm (shape + tag): 83 (59 shapes + 24 tags)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 15 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 15 | 0 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 15 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 15 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 13 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 17 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 11 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 11 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 6 | 0 | nhẹ / nặng |

*(Ghi chú: Có 5 box đèn và biển báo ở A03, A04 có chiều cao < 8 px được tính mức nhẹ/gợi ý theo QC1-08 và QC1-10, không tính vào tỉ lệ lỗi chính).*

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-05 | A01 | lane (R1) | chính | Trùng 2 polyline cùng mang position R1 (vạch phân làn bị gán trùng). |
| 2 | QC1-06 | A03 | lane (L1) | chính | Vạch vàng đôi phân cách làn ngược chiều nhưng gán kind = single thay vì double. |
| 3 | QC1-07 | A04 | drivable (alternative) | chính | Vùng lái tràn sang dải đỗ xe sát lề bên phải (quy tắc: không gồm dải đỗ xe). |
| 4 | QC1-02 | A06 | lane (R1) | nặng | Bỏ sót vạch R1 bên phải trong khi ảnh nhìn thấy rõ vạch. |
| 5 | QC1-07 | A06 | drivable (direct) | chính | Vùng lái bị cụt, thiếu phần mặt đường bên phải do bỏ sót vạch R1. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Ảnh đường nông thôn không có vạch sơn kẻ đường, thiếu cả L1 và R1 nhưng có road_curb. | Ca này được miễn trừ lỗi QC1-02 theo quy định tại CHECKPOINTS.md do thực tế đường không có vạch sơn. |

## Quyết định
Lỗi nặng: 1   Lỗi chính: 4 / 83 nhãn = 4.8 %   Lỗi nhẹ: 5 (box < 8px)   Ca chờ lead: 0  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Lô có **1 lỗi NẶNG** thuộc mã **QC1-02** tại ảnh **A06** (bỏ sót vạch R1). Theo luật của phiếu QC 1: *"Có ít nhất một lỗi nặng $\rightarrow$ Rework"*.
