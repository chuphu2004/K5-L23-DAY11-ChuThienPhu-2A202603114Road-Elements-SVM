# Báo cáo cá nhân — Ngày 11
Họ tên: Chu Thien Phu              Mã học viên: 2A202603114
Phiên bản CVAT (Help → About): 2.74.1 (CVAT local, `http://localhost:8080`, tài khoản `phuhuy12`)
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 01:01 (giờ máy, UTC+7)    Số lần nộp lại sau Rework: 0

## 1. Kiểm project
Project `d11-road-chuthienphu`, tạo từ `configs/road_v1_labels.json` (sinh bởi `python -m road_lab.taxonomy`). Đã đối chiếu label của project qua API CVAT với file này: khớp 10/10 label, đúng kiểu, đúng thuộc tính và giá trị.

| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane`, `road_curb`: polyline · `crosswalk`, `drivable`: polygon · `traffic_light`, `traffic_sign`: rectangle |
| Thuộc tính và giá trị | Đúng | `lane`: position L1/R1/L2/R2/other, style solid/dashed, color white/yellow/other, kind single/double · `drivable`: area_type direct/alternative · `traffic_light`: color red/yellow/green/off/unknown, type vehicle/pedestrian/beacon, facing front/side/back, edge_zone checkbox · `traffic_sign`: group prohibitory/mandatory/warning/information/supplementary/other, facing, edge_zone |
| 4 tag ảnh | Đúng | `camera` (front/fisheye_front/fisheye_rear/fisheye_left/fisheye_right), `timeofday` (day/dusk/night), `weather` (clear/overcast/rain/fog/other), `source` (real/simulated); mỗi tag một thuộc tính select `value` |

Bốn task trong project: `front` (A01–A12), `front-extra` (A13–A16), `fisheye` (B01–B08), `fisheye-extra` (B09–B12); mỗi task một job, ảnh giữ nguyên tên gốc.

Cách kết thúc polyline trên bản CVAT này: Chọn Polyline, label `lane` → Shape, click các điểm từ gần ra xa, bấm phím **N** để kết thúc.
Cách đặt tag ảnh trên bản CVAT này: Dùng công cụ Tag ở thanh bên trái, chọn label tag (đặt `camera` trước, rồi `timeofday`, `weather`, `source`). Sau đó mở **Details** của tag trong bảng Objects để sửa `value`, vì CVAT tự điền giá trị đầu danh sách.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 30 | 15 | 8 | 28 | 50 | 24 |
| front-extra (đã làm 4 / 4) | 4 | 9 | 3 | 6 | 8 | 20 | 13 |
| fisheye | 8 | 21 | 24 | 10 | 12 | 9 | 6 |
| fisheye-extra (đã làm 4 / 4) | 4 | 3 | 6 | 4 | 4 | 0 | 0 |

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- |
| A02 | tag timeofday | day / dusk | day | Nắng thấp, bóng dài, nhưng bầu trời còn xanh hoàn toàn, chưa có màu hoàng hôn |
| A03 | tag weather | clear / overcast | clear | Nhiều mây mỏng nhưng nắng chiều vẫn chiếu lên nóc nhà, đường khô; timeofday = dusk vì trời ửng hồng và xe đã bật đèn |
| A04 | tag timeofday | day / dusk | day | Trời âm u nên tối, xe bật đèn, nhưng bầu trời vẫn trắng sáng; weather = overcast |
| A16 | tag timeofday, weather | day / dusk; clear / overcast | day, clear | Đèn văn phòng và đèn xe đang sáng gợi ý dusk, nhưng trời vẫn còn sáng, đường khô, không có dấu hiệu mưa hay sương |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: chuthienphu (tự QC, coach cho phép; phiếu `chuthienphu-qc1-for-chuthienphu.md`, mẫu 6 ảnh A01, A04, A08, B01, B03, B06, 121 nhãn)  Quyết định nhận được: Rework (12 lỗi nặng; lỗi chính 38/121 = 31,4 %)  
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-03 | 7 | Có: A01 vạch vàng mép phải để `other` (phải là R2); B03 ở camera rear các vạch sát xe để `other` (phải L1/R1, L2/R2) và ba polyline không phải vạch làn (`lane #1`, `#6`, `#7`) | Chưa, sửa ở revision 2 |
| QC1-04 | 4 | Có: A01 điểm đầu vạch vàng lệch ~8 px; A04 thiếu R2; B06 vạch đứt xa chỉ vẽ một vệt và một vạch đứt bị bỏ sót | Chưa, sửa ở revision 2 |
| QC1-05 | 1 | Có: A01 `lane #4` vẽ lặp `lane #2` (hai đường cách nhau ≤ 3 px) | Chưa, sửa ở revision 2 |
| QC1-06 | 3 | Có: B03 `lane #6` color; B06 `lane #1` kind, `lane #2` style | Chưa, sửa ở revision 2 |
| QC1-07 | 8 | Một phần: đồng ý A08, B03, B06; A01 (dòng 4–5) phụ thuộc ca mơ hồ "xe đang ở làn nào" khi chuyển làn | Chưa, sửa ở revision 2 sau khi chốt ca mơ hồ |
| QC1-08 | 15 | Có: A08 bốn đèn xe quay về xe đang sáng xanh gán `unknown` (nặng), đèn nhìn nghiêng gán `yellow`, box thừa; dòng 11 (đèn `#5`) chờ lead | Chưa, sửa ở revision 2 |
| QC1-09 | 10 | Có: A08 `type`/`facing` của đèn, `group` của biển `#4`, `#8` | Chưa, sửa ở revision 2 |
| QC1-10 | 2 | Có: A08 thiếu một biển trắng nhỏ; B03 gán biển trên huy hiệu in trên thân xe | Chưa, sửa ở revision 2 |

Nhận xét: lỗi tập trung ở A08 (28/50 lỗi, chủ yếu đèn và biển) và B03 (quy ước `position` ở camera rear). Kể cả bỏ A08 ra, A01 và B03 vẫn có lỗi nặng nên Rework là đúng luật. 13 ca mơ hồ trong phiếu chưa có lời đáp của lead.

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `chuthienphu-front.zip` | Có (`road_check lint`, 16 ảnh, 16/16 đủ bốn tag) | A01: 10 / 10 | A02: 8 / 8 | Có (`front`) |
| `chuthienphu-fisheye.zip` | Có (`road_check lint`, 12 ảnh, 12/12 đủ bốn tag) | B01: 8 / 8 | B02: 12 / 12 | Có (`fisheye_front`) |

Mỗi zip gộp hai task (front + front-extra, fisheye + fisheye-extra) vào một `annotations.xml`, vì `road_check` chỉ đọc một `annotations.xml` trong mỗi zip. Manifest `chuthienphu-manifest.json` (revision 1): `contains_images = false` cho cả hai file; lint: 7 nặng, 2 chính, 3 nhẹ.

Cảnh báo lint còn lại đã được kiểm lại trên ảnh và giữ nguyên:

| Ảnh | Cảnh báo lint | Xử lý |
| --- | --- | --- |
| A03 | QC1-02 chưa có L1 | Không có tồn tại L1/R1 trong ảnh này |
| A05 | QC1-02 chưa có L1, R1 | Không có tồn tại L1/R1 trong ảnh này |
| A06 | QC1-02 chưa có R1 | Không có tồn tại L1/R1 trong ảnh này |
| A07 | QC1-02 chưa có L1 | Không có tồn tại L1/R1 trong ảnh này |
| A09 | QC1-02 chưa có R1 | Không có tồn tại L1/R1 trong ảnh này |
| A14 | QC1-02 chưa có R1 | Không có tồn tại L1/R1 trong ảnh này |
| A01 | QC1-05 hai polyline cùng L2 | Giữ nguyên |
| A08 | QC1-05 hai polyline cùng L1 | Giữ nguyên |
| A03, A04, A15 | QC1-08 box đèn thấp hơn 8 px | Không bắt buộc; giữ nguyên |

## 6. Ảnh chụp màn hình
1. Tab Labels của project.
2. Một ảnh camera trước đã gán đủ (làn, vùng lái, đèn/biển).
3. Một ảnh fisheye đã gán, phóng to đoạn polyline cong.
4. Một đoạn XML có <polyline label="lane">.

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi |  |  |  |  |  |
| x của bạn kia |  |  |  |  |  |

Trả lời 3 câu:

1. Năm số x đó chính là đích mà một model row-anchor học cho vạch này. Nếu bạn dừng polyline sớm 40 px, hàng nào đổi thành "không có làn"?
2. So với bạn được kiểm (cùng ảnh): ở hàng 720 và hàng 560, hai bạn lệch nhau bao nhiêu pixel? Lệch ở hàng nào ảnh hưởng LKA nhiều hơn (slide 25)?
3. Nếu polyline vẽ từ xa về gần (ngược quy tắc 2), cách tính trên có đổi không? Script nào sẽ gặp khó?
