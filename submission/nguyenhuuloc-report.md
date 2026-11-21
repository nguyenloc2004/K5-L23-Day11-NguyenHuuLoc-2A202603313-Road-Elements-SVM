# Báo cáo cá nhân — Ngày 11
Họ tên: Nguyễn Hữu Lộc               Mã học viên: 2A202603313  
Phiên bản CVAT (Help → About): 2.81.0 (self-host bằng Docker)  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 2 (bản revision 1 cất ở `submission/r1/`)  
Thời điểm export (ngày giờ trên CVAT): front 2026-11-21 03:43 UTC (10:43 giờ VN), fisheye 2026-11-21 03:29 UTC (10:29 giờ VN). Lần nộp đầu: 2026-11-21 00:09 UTC    Số lần nộp lại sau Rework: 1

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | lane, road_curb (polyline); crosswalk, drivable (polygon); traffic_light, traffic_sign (rectangle). Đã so bằng script với `configs/road_v1_labels.json`, không có label thừa |
| Thuộc tính và giá trị | Đúng | Tên, kiểu nhập, giá trị mặc định và danh sách giá trị khớp từng thuộc tính |
| 4 tag ảnh | Đúng | camera, timeofday, weather, source, mỗi tag có thuộc tính select `value` |
Cách kết thúc polyline trên bản CVAT này: chọn công cụ Polyline → label `lane` → Shape, click các điểm từ gần ra xa, nhấn phím **N** để kết thúc. Thêm điểm vào polyline có sẵn: giữ Shift rồi click lên đoạn đường.  
Cách đặt tag ảnh trên bản CVAT này: chọn công cụ Tag ở thanh bên trái → chọn label (camera, timeofday, weather, source) → Tag. Sau đó mở Details của tag trong bảng Objects để chọn `value`, vì CVAT tự điền giá trị đầu tiên của danh sách.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 32 | 11 | 7 | 24 | 39 | 23 |
| front-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| fisheye | 8 | 9 | 11 | 11 | 11 | 3 | 6 |
| fisheye-extra (đã làm 0 / 4) | 0 | 0 | 0 | 0 | 0 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A05 | lane | Vẽ L1/R1 hay bỏ trống | Bỏ trống | Đường không có vạch sơn, chỉ có lề (đã gán `road_curb`). Không vẽ vạch không có thật; xin coach xác nhận để miễn QC1-02. Người kiểm QC 1 cũng ghi ca này được miễn |
| A03 | lane L1 `kind` | single / double | single | Hai nét vàng tách xa dần, không song song suốt chiều dài; nét bên trái thuộc dải phân cách hoặc làn rẽ. Người kiểm QC 1 cho là double; xin lead chốt |
| A06 | lane R1, drivable direct | Vẽ R1 tới vạch đứt sát mép phải hay bỏ trống | Bỏ trống R1; cạnh phải `direct` theo bề rộng một làn | Dưới cầu cạn không có vạch bên phải làn đang đi; vạch đứt sát mép ảnh thuộc làn ngoài. Lint báo QC1-02, xin coach xác nhận để miễn |
| B03, B04 | lane position (fisheye_rear) | L/R theo ảnh hay theo hướng xe | Theo phía trên ảnh: vạch bên phải ảnh là R1 (B03), bên trái ảnh là L1 (B04) | Guideline không nói rõ cho camera nhìn ra sau; cần lead chốt quy ước |
| B02–B05 | traffic_light / traffic_sign edge_zone | Bật hay tắt khi đèn, biển sát viền | Bật cho 5 hộp có tâm ngoài 80 % bán kính (B02: 2 đèn; B03: biển Keep Left; B04; B05), tắt cho các hộp còn lại | Guideline mục 4: tâm hộp ngoài 80 % bán kính vòng ảnh thì bật. Đã kiểm lại bằng lint, không còn cảnh báo |
| B05–B08 | drivable (fisheye_left/right) | Vẽ vùng lái chỉ phía trước xe hay cả trước lẫn sau | Vẽ hết phần mặt đường thấy được cả trước và sau, cắt ở mép thân xe | Guideline chỉ nói "đi được nếu đường trống" và không gồm thân xe; không có quy tắc riêng cho camera hai bên |
| fisheye, nhiều ảnh | traffic_sign group (biển châu Âu, ảnh mờ) | prohibitory / mandatory / other | Theo chức năng: tròn viền đỏ → prohibitory, tròn xanh có mũi tên (Keep Left, B03) → mandatory | Guideline chỉ có bảng biển Mỹ; biển mờ chọn nhóm gần nhất theo chức năng |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: Nguyễn Hải Nam (2A202603309), kiểm 6 ảnh A01–A06 của `front` revision 1  Quyết định nhận được: **Rework** (1 lỗi nặng QC1-02; 4 lỗi chính / 83 nhãn = 4,8 %)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-05 (A01, hai polyline cùng R1) | 1 | Đồng ý | Đã sửa: vạch vàng bên phải đổi từ R1 sang R2, A01 chỉ còn một R1 |
| QC1-06 (A03, L1 vàng đôi gán single) | 1 | Không đồng ý: hai nét vàng ở góc trái dưới không song song mà tách xa dần nhau. Nét bên trái là mép dải phân cách hoặc làn rẽ, không phải nửa của một vạch đôi, nên L1 là vạch đơn (`kind = single`). Đã ghi vào bảng ca khó | Không sửa |
| QC1-07 (A04, drivable tràn sang dải đỗ xe bên phải) | 1 | Đồng ý: polygon bên phải R1 lấn sang dải sát làn xe đạp | Đã sửa: polygon bên phải R1 đổi thành `alternative`, cạnh phải dừng ở vạch trắng trước làn xe đạp |
| QC1-02 (A06, thiếu R1) | 1 | Không đồng ý: dưới cầu cạn không có vạch sơn bên phải làn đang đi. Vạch đứt trắng ở sát mép phải ảnh thuộc làn ngoài xa hơn, không phải R1. Ca không thấy vạch, xin coach xác nhận để miễn QC1-02 như A05 | Không sửa |
| QC1-07 (A06, drivable direct bị cụt bên phải) | 1 | Không đồng ý: hệ quả của lỗi trên. Không có R1 nên cạnh phải vùng `direct` lấy theo bề rộng một làn, không kéo tới vạch của làn ngoài | Không sửa |

Sửa thêm ngoài phiếu ở revision 2 (từ lint và tự kiểm): bật `edge_zone` cho 5 hộp ở B02–B05 (QC1-11); sửa `group` biển ở A03 (warning), A06 (mandatory, warning), A12 (mandatory), B03 (Keep Left → mandatory); thêm `drivable` alternative ở A01, B04, B05; thêm điểm cho `road_curb` theo cung ở B02 (QC1-11); gán thêm biển ở B03 và lane `position = other` ở B06–B08.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| nguyenhuuloc-front.zip | Có (`road_check lint` đọc được, 12 ảnh, `contains_images: false`) | A01: <!-- TODO: số trên CVAT --> / 11 | A02: <!-- TODO: số trên CVAT --> / 8 | Có, 12/12 ảnh `front` |
| nguyenhuuloc-fisheye.zip | Có (`road_check lint` đọc được, 8 ảnh, `contains_images: false`, 0 cảnh báo) | B01: <!-- TODO: số trên CVAT --> / 4 | B02: <!-- TODO: số trên CVAT --> / 10 | Có, 8/8 ảnh đúng FV/RV/MVL/MVR |

## 6. Ảnh chụp màn hình
<!-- TODO: chèn 4 ảnh chụp -->
1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20: nhiều nhất là **QC1-11** (fisheye): quên bật `edge_zone` cho 5 hộp đèn và biển sát viền ở B02–B05, và một `road_curb` chỉ có 3 điểm ở B02. Lỗi chung phía sau là **để nguyên giá trị mặc định** của CVAT: `edge_zone` tắt, `group = prohibitory`, `area_type = direct`. Người kiểm bắt thêm QC1-07 (vùng lái tràn sang dải đỗ xe) ở A04: tôi cần nhớ quy tắc dải đỗ xe sát lề không tính vào vùng lái, kể cả khi trống. Cách tránh ở Ngày 20: sau khi vẽ xong mỗi shape, mở Details và kiểm từng thuộc tính, không tin giá trị mặc định; với ảnh fisheye, rà riêng các hộp gần viền; chạy `road_check lint` sau mỗi vài ảnh thay vì chỉ chạy lúc cuối.  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào: polyline `lane` được đổi thành đích row-anchor (mục 8): mỗi hàng y có một giá trị x cho mỗi vị trí L1, R1, L2, R2. Lỗi đã sửa ở A01 là có **hai polyline cùng mang R1**: vạch trắng thật và vạch vàng xa hơn. Khi tạo đích, hàng y nào có cả hai vạch thì R1 có hai giá trị x, và script phải chọn một hoặc lấy trung bình. Model vì thế học R1 nằm ở vị trí sai, có thể là giữa hai vạch, tức là giữa làn bên cạnh. Với LKA, xe sẽ tưởng mép phải làn mình xa hơn thực tế và lệch dần sang phải. Sau khi sửa (vạch vàng thành R2), mỗi hàng chỉ còn một x cho R1.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Ảnh A01, vạch R1 (`lane#1`), so với Nguyễn Hải Nam (`road_lab.rowanchor`).

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | 721.8 | 661.3 | 600.9 | 540.4 | 483.2 |
| x của bạn kia | 718.2 | 660.1 | 602.1 | 544.9 | 485.4 |

Trả lời 3 câu:

1. Vạch R1 của tôi đi từ y = 720 tới y ≈ 512. Dừng sớm 40 px thì điểm cuối ở y ≈ 552, vẫn xa hơn hàng 560, nên cả năm hàng giữ nguyên. Hàng 560 chỉ thành "không có làn" khi điểm cuối thật nằm trong khoảng 520–560. Nếu "dừng sớm" ở đầu gần (bắt đầu từ y = 680) thì hàng 720 thành "không có làn".
2. Hàng 720 lệch 3,6 px, hàng 560 lệch 2,2 px. Lệch ở hàng gần (720) ảnh hưởng LKA nhiều hơn, vì đó là khoảng cách ngang ngay trước xe mà bộ điều khiển dùng để giữ làn.
3. Phép nội suy x tại mỗi hàng không đổi, vì nó chỉ tìm hai điểm kẹp hàng y. Các bước dựa vào thứ tự điểm sẽ gặp khó: `road_check` kiểm chiều vẽ (QC1-04) và so hai đầu polyline với GT (`lane_stop_px`), còn `rowanchor` cũng so điểm đầu với điểm cuối để kiểm chiều vẽ.
