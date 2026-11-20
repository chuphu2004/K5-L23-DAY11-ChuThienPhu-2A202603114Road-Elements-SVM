# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): chuthienphu        Người kiểm (học viên): chuthienphu (tự QC, coach cho phép)  
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `chuthienphu-front.zip`, `chuthienphu-fisheye.zip` (revision 1)  
Số ảnh kiểm: 6 — A01, A04, A08, B01, B03, B06 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 121

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 10 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 23 | 7 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 23 | 4 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 23 | 1 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 23 | 3 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 36 | 8 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 21 | 15 (5 nặng, 10 chính) | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 38 | 10 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 17 | 2 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 36 | 0 | chính |
| QC1-12 file | lỗi file | 121 | 0 | nhẹ / nặng |

## Danh sách lỗi (mỗi lỗi một dòng)
Cách ghi nhãn: `label #k` = thứ tự trong cùng label của ảnh · `[i]` = vị trí phần tử trong `<image>` của annotations.xml (đếm từ 0, gồm cả tag) · `(x, y)` = điểm đầu (box: góc trên trái).

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A01 | lane #3 [5] (1274.5, 711) | nặng | Vạch vàng liền mép phải (vạch mép đường, phải gán theo làn) để position = other. Theo L1/R1 đã gán thì đây là R2 (là R1 nếu lead chọn làn phải); không cách nào là other |
| 2 | QC1-04 | A01 | lane #3 [5] (1274.5, 711) | chính | Đoạn đầu (1243.5, 699)→(1274.5, 711) rời vệt sơn: điểm đầu nằm dưới tâm vạch vàng khoảng 8 px (tâm sơn ở y ≈ 703), quá ngưỡng 5 px |
| 3 | QC1-05 | A01 | lane #4 [7] (0.22, 599.32) | chính | Vẽ lặp: vạch liền đôi mép trái đã có lane #2 [2] (cùng L2/solid/white/double, hai đường cách nhau ≤ 3 px). Một vạch chỉ một polyline; xoá lane #4 |
| 4 | QC1-07 | A01 | drivable #1 [3] (420, 506) | chính | direct đặt ở làn phải, nhưng L1/R1 cho thấy xe đang ở làn giữa (R1 ở đáy ảnh x ≈ 713, tâm ảnh x = 640). Làn phải phải là alternative (xem Ca mơ hồ A01) |
| 5 | QC1-07 | A01 | drivable #2 [4] (341, 514) | chính | Làn giữa (làn đang đi theo L1/R1) gán alternative, phải là direct |
| 6 | QC1-04 | A04 | lane (thiếu), vạch liền trắng (≈670, 332)→(1280, ≈525) | chính | Bỏ sót R2: vạch liền trắng ngăn làn bên phải với dải đệm và làn xe đạp xanh, thấy rõ suốt chiều dài (guideline: L2, R2 nếu thấy) |
| 7 | QC1-08 | A08 | traffic_light #15 [20] (360, 92) | nặng | Cụm đèn xe 3 ngăn quay về xe, ngăn dưới đang sáng xanh; gán color = unknown, phải là green |
| 8 | QC1-08 | A08 | traffic_light #16 [21] (764, 164) | nặng | Đèn quay về xe đang sáng xanh; gán unknown |
| 9 | QC1-08 | A08 | traffic_light #17 [22] (669, 148) | nặng | Đèn quay về xe đang sáng xanh; gán unknown |
| 10 | QC1-08 | A08 | traffic_light #18 [23] (649, 211) | nặng | Đèn treo trên cần, đang sáng xanh; gán unknown |
| 11 | QC1-08 | A08 | traffic_light #5 [10] (517, 178) | nặng | Gán yellow nhưng không có ngăn vàng nào sáng (vỏ vàng, các ngăn tối). Hướng đèn không chắc nên chọn mức cao hơn (xem Ca mơ hồ) |
| 12 | QC1-08 | A08 | traffic_light #1 [6] (871, 145) | chính | Vỏ đèn vàng nhìn nghiêng (thấy chụp che ở cạnh), không thấy ngăn nào sáng: yellow là màu vỏ, phải là unknown |
| 13 | QC1-08 | A08 | traffic_light #2 [7] (203, 103) | chính | Như dòng 12: đèn nhìn nghiêng, không thấy ngăn sáng, gán yellow, phải là unknown |
| 14 | QC1-08 | A08 | traffic_light #3 [8] (291, 138) | chính | Như dòng 12: gán yellow, phải là unknown |
| 15 | QC1-08 | A08 | traffic_light #10 [15] (463, 177) | chính | Như dòng 12: gán yellow, phải là unknown |
| 16 | QC1-08 | A08 | traffic_light #11 [16] (360, 110) | chính | Box thừa: chỉ ôm ngăn xanh của chính cụm traffic_light #15 [20]; mỗi cụm một box sát vỏ |
| 17 | QC1-08 | A08 | traffic_light #13 [18] (765, 175) | chính | Box thừa nằm trong cụm traffic_light #16 [21] |
| 18 | QC1-08 | A08 | traffic_light #12 [17] (674, 160) | chính | Box thừa nằm trong cụm traffic_light #17 [22] |
| 19 | QC1-08 | A08 | traffic_light #7 [12] (675, 175) | chính | Box thừa (nửa dưới cụm traffic_light #17 [22]), lại gán yellow |
| 20 | QC1-08 | A08 | traffic_light #8 [13] (668, 167) | chính | Box thừa (phần vỏ trái dưới cụm traffic_light #17 [22]), gán yellow |
| 21 | QC1-08 | A08 | traffic_light #19 [24] (517, 178) | chính | Box thừa ôm chung hai đầu đèn đã có box riêng (#5 [10] và #14 [19]) |
| 22 | QC1-09 | A08 | traffic_light #15 [20] (360, 92) | chính | type = pedestrian nhưng là đèn xe (đèn tròn, cụm 3 ngăn): vehicle |
| 23 | QC1-09 | A08 | traffic_light #16 [21] (764, 164) | chính | type = pedestrian, phải là vehicle |
| 24 | QC1-09 | A08 | traffic_light #17 [22] (669, 148) | chính | type = pedestrian, phải là vehicle |
| 25 | QC1-09 | A08 | traffic_light #18 [23] (649, 211) | chính | type = pedestrian, phải là vehicle (đèn tròn treo trên cần) |
| 26 | QC1-09 | A08 | traffic_light #1 [6] (871, 145) | chính | facing = front nhưng đèn nhìn nghiêng: side |
| 27 | QC1-09 | A08 | traffic_light #2 [7] (203, 103) | chính | facing = front, phải là side |
| 28 | QC1-09 | A08 | traffic_light #3 [8] (291, 138) | chính | facing = front, phải là side |
| 29 | QC1-09 | A08 | traffic_light #10 [15] (463, 177) | chính | facing = front, phải là side |
| 30 | QC1-09 | A08 | traffic_sign #4 [28] (777, 37) | chính | Tấm "PASSENGER CARS ONLY" gắn kèm biển chỉ dẫn là biển phụ / hạn chế, không phải information (supplementary hoặc prohibitory, xem Ca mơ hồ) |
| 31 | QC1-09 | A08 | traffic_sign #8 [32] (990, 184) | chính | Chồng biển trắng có vòng và gạch chéo đỏ (biển cấm) gán information, phải là prohibitory |
| 32 | QC1-10 | A08 | traffic_sign (thiếu), box ≈ (699, 224)–(708, 240) | chính | Bỏ sót tấm biển trắng cao khoảng 16 px trên cột, nằm giữa traffic_sign #9 [33] và #2 [26] |
| 33 | QC1-07 | A08 | drivable #3 [38] (318, 399) | chính | direct dừng ở mép xa của vạch ngựa vạn (y ≈ 430), bỏ sót mặt đường trên vạch ngựa vạn ngay trước mũi xe (tới y ≈ 505) |
| 34 | QC1-07 | A08 | drivable #2 [5] (662, 316) | chính | alternative cũng dừng ở mép xa vạch ngựa vạn, bỏ sót dải trước xe |
| 35 | QC1-03 | B03 | lane #1 [2] (1134.4, 552.9) | nặng | "R1" không phải vạch làn: nối một vệt sơn mòn nằm ngang (x 600–750, y ≈ 660) qua mặt đường trống tới cạnh một vật trắng (rác) ở (≈1143, 548) |
| 36 | QC1-03 | B03 | lane #7 [13] (1138, 553) | nặng | Không phải vạch: bắt đầu từ vật trắng trên đường, vắt qua vỉa lên dải gạch lát vỉa hè |
| 37 | QC1-03 | B03 | lane #6 [12] (137, 621) | nặng | Vạch của đường xe đạp nằm sau đảo giao thông và vỉa, không phải vạch sát xe: không thể là L1 (nếu gán thì other) |
| 38 | QC1-06 | B03 | lane #6 [12] (137, 621) | chính | color = other nhưng vạch màu trắng |
| 39 | QC1-03 | B03 | lane #2 [3] (484.5, 357) | nặng | Vạch đứt (mòn) bên trái làn của xe, đối xứng với lane #4 [5] qua tâm ảnh: là L1/R1, không phải other |
| 40 | QC1-03 | B03 | lane #4 [5] (780, 357) | nặng | Vạch đứt bên phải làn của xe: là L1/R1, không phải other |
| 41 | QC1-03 | B03 | lane #3 [4] (1017.5, 425) | nặng | Vạch đứt kế tiếp bên ngoài lane #4 [5]: là L2/R2, không phải other |
| 42 | QC1-07 | B03 | drivable #1 [7] (263, 648) | chính | direct phủ cả mặt đường nhiều làn phía sau (từ vỉa đảo bên trái tới vỉa bên phải), không chỉ làn của xe; làn bên cạnh phải là alternative |
| 43 | QC1-10 | B03 | traffic_sign #3 [10] (597, 883) | chính | Huy hiệu in trên thân xe mình (đáy ảnh), không phải biển báo; thân xe không gán |
| 44 | QC1-07 | B06 | drivable #2 [13] (175, 206) | chính | Một polygon direct phủ gần hết mặt đường thấy được: nhiều làn, vạch ngựa vạn, ray tàu điện, làn xe đạp sau hàng khối bê tông tới vỉa xa. direct chỉ là làn đang đi |
| 45 | QC1-07 | B06 | drivable #1 [12] (688, 45) | chính | Phần đường xa bên kia ray (gần xe đỏ) gán direct; đó không phải làn của xe |
| 46 | QC1-07 | B06 | crosswalk #2 [11] (997, 736) | chính | Polygon mảnh khoảng 55 × 15 px sát mép thân xe, không có vạch ngựa vạn: thừa |
| 47 | QC1-06 | B06 | lane #1 [2] (1170.5, 785) | chính | Vạch là một hàng khối sơn trắng: kind = double sai (single); các khối có khe hở nên style solid cũng nghi sai (dashed) |
| 48 | QC1-04 | B06 | lane #2 [3] (240, 181) | chính | Chỉ vẽ một vệt khoảng 28 px của một vạch đứt phía xa; vạch đứt phải là một polyline qua các vệt thấy được (dừng sớm) |
| 49 | QC1-06 | B06 | lane #2 [3] (240, 181) | chính | style = solid cho vệt của vạch đứt, phải là dashed |
| 50 | QC1-04 | B06 | lane (thiếu), vạch đứt qua ≈ (208–232, 262–290) và (262–295, 199–228) | chính | Bỏ sót vạch đứt trắng thấy rõ ở nửa xa (position other) |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A01 | Xe đang đè vạch đứt giữa làn giữa và làn phải (điểm tụ x ≈ 400, có vẻ đang chuyển làn). Làn đang đi là làn nào? Phiếu chọn làn giữa (khớp L1/R1, tâm ảnh nằm trái R1) nên ghi QC1-07 ở dòng 4–5. Nếu lead chọn làn phải thì drivable đúng, nhưng lane #1 [1], #5 [9], #2 [2] sai position (QC1-03 nặng) và vạch vàng là R1 | |
| A04 | Dải vạch đứt trắng ngắn sát vỉa trái, bên chiều ngược (≈ (113, 406)→(300, 376)): là L2 hay vạch dải đỗ (không gán)? Chưa tính lỗi | |
| A04, B03 | Bảng kế hoạch ảnh (không có trong repo) có yêu cầu đèn/biển cho A04 và B03 không? Nếu có thì còn thiếu: A04 hai biển tên đường (≈ 207–240 × 193–205 và 225–238 × 180–191) và một tấm tối có thể là biển quay lưng (232–252 × 152–169); B03 ít nhất 5 biển (ví dụ biển tròn xanh 1131–1157 × 361–401, biển chữ nhật xanh 842–872 × 240–268) và 2 cụm đèn (401–414 × 236–261, 203–217 × 270–307). Chưa tính lỗi | |
| A08 | Vệt chấm mờ từ (371, 366) tới ≈ (500, 310), cũng là mép trái vùng direct: có là vạch L1 không? Nếu có thì lane #3 [40] và #4 [41] phải là L2, lane #1 [0] là other (thêm lỗi QC1-03 nặng) | |
| A08 | Vạch trái đổi từ liền sang chấm (lane #3 [40] solid + lane #4 [41] dashed, lint QC1-05): một polyline hay hai polyline theo style? Chưa tính lỗi | |
| A08 | traffic_light #5 [10]: đầu đèn vỏ vàng, các ngăn tối. Quay về xe (off) hay nhìn nghiêng (unknown)? Phiếu ghi nặng theo luật chọn mức cao hơn (dòng 11) | |
| A08 | Các khối màu cam: traffic_light #6 [11] (429–439 × 231–242), traffic_light #4 [9] (899–922 × 211–232), traffic_sign #1 [25], #2 [26]: là đèn đi bộ đang sáng tay cam hay biển cảnh báo cam? Cạnh traffic_light #9 [14] có một ngăn xanh đang sáng (609–615 × 207–214): có thiếu một đầu đèn không? Chưa tính lỗi | |
| A08 | traffic_sign #4 [28] nên là supplementary hay prohibitory (đã tính lỗi vì information sai theo cả hai cách)? traffic_sign #8 [32] là 2–3 tấm xếp chồng: cần box riêng từng tấm? traffic_sign #11 [35] (băng-rôn xanh trên cột) và #12 [36] (tấm trắng sáng) có phải biển giao thông? | |
| A08 | drivable #1 [4]: dải giữa vạch R2 và vỉa phải (khoảng 70 % bề rộng làn) là lề / dải đỗ (không tính) hay làn (alternative)? Chưa tính lỗi | |
| B01 | Hai dải xám bên phải trong bóng cây (lane #2 [7] = R1, lane #1 [1] = R2, đều kind = double): là vạch sơn (một vạch đôi) hay hai mép bó vỉa? Cách hiểu nào cũng còn nhãn sai (vạch đôi vẽ hai lần, hoặc kind sai, hoặc lane thừa), và road_curb #1 [3] lại nằm phía trong hai vạch này. Chưa tính lỗi | |
| B01 | crosswalk #1 [6] không gồm vệt ngựa vạn trên nền gạch / đường ray bên trái: có thuộc cùng vạch qua đường không? traffic_light #1 [2] facing = front nhưng không có ngăn sáng, bóng chụp che hướng sang bên: có phải back/side? Chưa tính lỗi | |
| B03 | lane #5 [11] (R2, solid): vệt trắng mảnh có móc ở đầu xa là mũi tên trên mặt đường hay một vệt của vạch đứt? Quy ước L/R cho fisheye_rear (theo xe hay theo ảnh) để chọn L1/R1 cho lane #2 [3] / #4 [5]? Chưa tính lỗi cho lane #5 | |
| B06 | 8 road_curb, trong đó 7 đường quanh hàng khối bê tông phân cách, chồng lên nhau và một phần đè lên vạch sơn lane #1 [2]: khối phân cách có gán road_curb không? Chưa tính lỗi | |

## Quyết định
Lỗi nặng: 12   Lỗi chính: 38 / 121 nhãn = 31,4 %   Lỗi nhẹ: 0   Ca chờ lead: 13  
Quyết định (Release / Hold / Rework): Rework  
Lý do (theo luật của phiếu): Có 12 lỗi nặng, mà chỉ một lỗi nặng là đủ Rework: 7 × QC1-03 (A01 vạch vàng mép phải để position other; B03 sáu lane sai position hoặc không phải vạch) và 5 × QC1-08 (A08 đèn quay về xe đang sáng xanh gán unknown, một đèn gán yellow khi không có ngăn vàng sáng). Lỗi chính 38/121 = 31,4 %, vượt 5 %, cũng đủ Rework. 13 ca mơ hồ chưa có lời đáp nhưng không đổi kết luận (lead trả lời theo hướng nào thì vẫn còn lỗi nặng), nên không Hold. Cảnh báo QC1-02 của lint ở A03, A05, A06, A07, A09, A14 nằm ngoài 6 ảnh mẫu; phiếu này không xét miễn cho các ảnh đó.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
