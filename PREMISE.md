# PREMISE — backlog LAB-5 khác bản LAB-4 ở đâu

Bản LAB-4 làm gốc: bộ thiết kế Product A nộp ngày 2026-11-14 (`lab4-design/specs/`, không nộp lại). Mã `G0x-y` là quyết định đã chốt
ở LAB-4 (PREMISE LAB-4 §6); `G-A..`, `G-B..`, `G-C..` là chỗ hở phát hiện khi break (xem `task-breakdown.md` mục 4). Issue ghi `#số` trên
[GitHub Project](https://github.com/users/uyenhtt-0921/projects/2). Chỉ trích mã RFP, không chép nội dung RFP.

## 1. Spec thêm / bỏ / sửa so với LAB-4

Không đặt bản sửa spec trong repo: các thay đổi dưới đây nằm ở mức thiết kế trong DoD của issue bị ảnh hưởng.

<!-- auto:premise-changes -->
| Mã | Spec (mã / file LAB-4) | Thêm / Bỏ / Sửa | Trước → sau | Vì sao | Issue bị ảnh hưởng |
|---|---|---|---|---|---|
| S1 | `specs/system-design/api-design/deliveries/` (chỉ có API-DLV-001..003) | Thêm | Không có API danh sách giao hàng → thêm truy vấn danh sách theo trạng thái / 滞留 cho G001 | G-B2: khi break G001 không có API nào trả danh sách | #130 |
| S2 | `specs/_common/api-list.md` (không có API-INC), `scope.md` §3 I001 / I002 | Thêm | Không có API và spec màn hình 奨励金 → thêm API chạy tính, danh sách kỳ / kết quả, delta chờ; I002 gộp vào I001 | G-B1: BM-53 tính 奨励金 có, nhưng màn hình gọi gì thì không có | #166, #167, #168 |
| S3 | Màn hình ngoài 16 màn hình lõi (`scope.md` §3: A001–A002, M001–M003, B001/B003, C002/C003/C005, D002/D003, E002, J001–J003, L001, M005/M006, M008) | Thêm | Chỉ có mô tả một dòng → issue tự đề xuất RPC / API theo REQ + BM-50 (vd. `rpc_cancel_trade`, `rpc_save_rate_version_draft`) | G-A1, G-A5, G-A17, G-C1, G-C24, G-C27, G-C39: không có BM-51 / 52 / 53 (review Lab 4 đã ghi nhận) | #61, #62, #101, #4, #6, #7, #205, #207 |
| S4 | `scope.md` §3 B004 (Lab 1 F02-04 là màn hình riêng) | Sửa | Trang riêng → chế độ lọc 失効間近 của B001 + thẻ trên A003 | G-A10: catalogue Lab 4 và Lab 2 đã gộp, scope vẫn ghi màn hình riêng | #46 |
| S5 | `settlement/SETTLEMENT_FUNCTIONS.md` §2.10 | Sửa | Bảng chữ ký ghi `rpc_reverse_payment` → hai hàm `rpc_request_payment_reversal` / `rpc_decide_payment_reversal` | G-B12: tiêu đề và bảng chữ ký mâu thuẫn; G09-2 cần người khác duyệt | #157, #159 |
| S6 | BM-50 notifications (`rpc_enqueue_notification`) | Sửa | Không có khóa chống trùng → khóa (loại sự kiện + đối tượng + ngày) | G-C23: batch chạy lại cùng ngày sẽ gửi trùng | #191 |
| S7 | BM-50 (nguồn dữ liệu M007) | Thêm | Chưa có schema cảnh báo hệ thống → bảng `system_alerts` | G-C18, G-C37: M007 và lỗi xuất kế toán không có nơi ghi | #180, #192 |
| S8 | `system-design/database-design/deliveries/DELIVERIES_DATABASE.md` (`delivery_exceptions`) | Sửa | Không có `client_request_id` → thêm để G003 gửi lại an toàn khi offline | G-B3: diff D3 chỉ nêu lots / delivery_events | #135 |
| S9 | Chuyển đổi dữ liệu N001 / N002 (không có thiết kế) | Thêm | → bảng lô chuyển đổi, staging, ánh xạ, RPC nhập có audit | G-C43: PLATFORM_DESIGN không có mục chuyển đổi; Lab 1 có F16 | #262, #263, #236 |
| S10 | `wireframes/H001` | Sửa | Thiếu khối 「当日完了の精算対象取引」 → làm theo H001_SPEC | G-B15: wireframe chưa cập nhật theo G09-1 | #143 |
| S11 | PDF 取引票 / 照合表 (Lab 1 F15-05; `settlement/H001_SPEC.md` mục 6) | Sửa | Lab 1 giao PDF, spec khóa nút "hạng mục sau" → 3 issue PDF chờ câu trả lời | G-C38: mâu thuẫn giữa Lab 1, scope và spec H001 / K001 / API-STL-002 | #222, #223, #224, #221 |
| S12 | Nền khóa ngày (`SETTLEMENT_DATABASE.md` §4.1 + nhánh trigger ở các BM-50) | Thêm | `guard_locked_day` mô tả rải ở nhiều BM-50 → một issue nền riêng | G-B6: khi ghép backlog không nhóm nào nhận phần nền | #49 |
<!-- /auto:premise-changes -->

## 2. Giả định bổ sung

Chỉ lấp chỗ spec / RFP để ngỏ; không ghi đè khối RFP đã nêu rõ. Câu hỏi còn chờ khách nằm ở các issue làm rõ (nhãn `kind:clarification`).

<!-- auto:premise-assumptions -->
| Mã | Giả định | Chỗ spec / RFP để ngỏ | Ảnh hưởng tới issue / estimate |
|---|---|---|---|
| A1 | Ngưỡng chưa có số (khóa tài khoản, hết phiên, số ngày cảnh báo 失効間近, hạn thanh toán 30 ngày, giới hạn nhập, dung lượng 受付伝票, rate limit) làm tham số cấu hình; giá trị mặc định chốt sau | PLATFORM_DESIGN 要確認 (NFR-SEC-03); Lab1-QA#8, #11; REQ-02 Q2 | Không đổi SWP (làm thành tham số) — #57, #58, #46, #91, #97, #253 |
| A2 | Lập điều chỉnh / xin mở khóa = vai trò SETTLEMENT; duyệt = người thứ hai SYS_ADMIN; MFA cho mọi người duyệt; maker ≠ checker | REQ ghi 要確認 vai trò duyệt; PREMISE Lab 4 §5 Q2 | Một bảng quyền đổi một chỗ — #59, #54, #109, #149, #159 |
| A3 | M003 chỉ xem ma trận quyền; đổi quyền = đổi mã + migration | Lab 1 F01-03 không nói sửa quyền qua màn hình; ADR-002 đặt bảng quyền trong mã | M003 nhỏ (3 SWP) — #63 |
| A4 | Trạng thái lô dùng enum DB hiện có, không thêm 「公開」 | FR-LOT-007 liệt kê 公開 nhưng enum `lot_state` không có | Không thêm issue — #85 |
| A5 | Lịch sử thay đổi (B003, C003, D003, E002, RPT-02) đọc từ `audit_logs`; E14 cung cấp truy vấn theo đối tượng | Không có bảng lịch sử riêng; nguồn RPT-02 ghi 要確認 | Không thêm bảng; E14-03 phục vụ nhiều màn hình — #205, #72, #103, #104 |
| A6 | Tranh chấp đang mở không chặn khóa ngày; trạng thái open / in_progress / resolved / closed | SETTLEMENT_DATABASE Q9 | Không thêm điều kiện chặn — #145, #152 |
| A7 | Offline G002: lần giao chưa gửi không cộng tạm vào 累積; xung đột giữ trên thiết bị và báo người dùng | REQ-2611-04 Q5 | Màn hình offline đơn giản hơn — #133 |
| A8 | Kỳ 奨励金 do người dùng chọn (`period_from`, `period_to`) cho tới khi có câu trả lời | Spec không định nghĩa kỳ; "kỳ sau" nhận delta chưa rõ | Có thể phải sửa API / màn hình khi khách trả lời — #163, #166, #167 |
| A9 | Mã lỗi còn "要確認" đặt tên khi làm và ghi vào `error-codes.md` cùng issue | INC detail, DLV detail ghi mã 要確認 | Không thêm issue — #112, #163, #127 |
| A10 | `audit_logs` lưu 7 năm bằng phân vùng theo thời gian, không xóa tự động; thu TRUNCATE ở prod + runbook quyền owner | DR-RET-01; COMMON_DATABASE Q2 | Thêm E14-04 — #48, #206 |
| A11 | M004: ngày nghỉ là cột cờ, chỉ để hiển thị / lập lịch, không chặn thao tác; giờ mở / đóng chợ ngoài phạm vi | M004 chỉ có wireframe | M004 nhỏ — #45 |
| A12 | Báo cáo dùng lại truy vấn màn hình (RPT-05 = H001, RPT-07 = I001, RPT-12 = J001); batch 11:00 của E08 và E11 tách theo đầu ra; làm 11 báo cáo (RPT-06 là liên kết K002) | REQ-07 Q2; K001 ghi "12 báo cáo" | Không làm trùng truy vấn — #173, #176, #178, #8, #142, #181 |
| A13 | Phần dùng chung có một chủ: E15-02 đính kèm, E15-03 khung offline, E01-04 logger, E13-06 truy vấn đếm cho A003; epic khác chỉ gọi lại | PLATFORM_DESIGN chia trách nhiệm chưa rõ | Tránh làm trùng giữa các epic — #77, #79, #34, #200, #80, #133 |
| A14 | Bản tỷ lệ đã công bố có trigger chặn UPDATE / DELETE, chỉ RPC rút lại được; lý do rút ghi audit | Lab 2 không có trigger; ADR-006 không nói cơ chế | Thêm E10-01b — #261, #7 |
| A15 | Danh mục mã hành động audit do E14-02 tạo từ các spec hàm, có test chặn RPC thiếu audit | Không có danh mục mã action | Thêm E14-02 — #204 |
| A16 | Hạ tầng: đo giới hạn serverless khi dựng CSV; xác nhận gói Supabase có PITR và đo RPO / RTO; cổng giờ cấm deploy 02:00–10:00 JST trong pipeline | Spec chỉ nêu mục tiêu | Nằm trong DoD các issue hạ tầng — #181, #254, #250, #248 |
| A17 | H005 入金 và đo KPI (U-19) không có dòng Lab 1 tương ứng: cột Lab 1 để trống, giờ tính là phần tăng | Bổ sung của Lab 4 (G04-3) và Lab 3 | Tăng giờ E08, E15 so với Lab 1 (estimate §5) — #114, #160, #219, #220 |
<!-- /auto:premise-assumptions -->

## 3. Hướng đã chốt

Cho chỗ LAB-4 còn nhiều phương án, hoặc nay đổi phương án.

<!-- auto:premise-decisions -->
| Mã | Vấn đề | Các phương án ở LAB-4 | Phương án chốt | Vì sao |
|---|---|---|---|---|
| D1 | Ai làm chủ trigger khóa ngày chung `guard_locked_day` và phụ thuộc chéo epic | (a) mỗi BM-50 tự thêm nhánh cho bảng của mình; (b) một chỗ chung | (b) issue nền E08-17 (#49); các epic chỉ khai báo ngoại lệ đã chốt (G09-1, G09-4, G09-7, G09-8); phụ thuộc chéo ghi bằng id issue | Tránh nhiều nhóm cùng sửa một trigger (G-A7, G-B5, G-B6) |
| D2 | Bảng `incentive_adjustments` và ba đường sinh delta 奨励金 | Lab 4 đặt bảng trong BM-50 adjustments; logic delta mô tả ở INC detail, ADJ decision và phần 入金 | Bảng thuộc E09-01 (#161); ba đường (điều chỉnh, 入金, hủy 入金) gọi chung hàm delta E09-08 (#118) và khóa người mua + kỳ E09-06 (#111) | Một chỗ tính thì số không lệch (G-B16, G09-6) |
| D3 | Kiểm tư cách người mua khi 完了確定 giao hàng | (a) gọi API kiểm tra trước như Lab 2; (b) kiểm trong transaction (Lab 4 G08-1) | (b): E07-03b (#127) gọi hàm chung `eligibility_check` (E03-05 (#69)) trong transaction | Bẫy nghiệp vụ §1 của Lab 4; dòng Lab 1 F02-03 cũng gắn G002 (G-A18) |
| D4 | Ai xác nhận tư cách khi người mua bị đình chỉ lúc 完了確定 (R-19 + N-10) | Lab 4 hoãn, hỏi khách; tạm giữ US-11 AC3 của Lab 2 | Giữ hành vi hiện có và quy tắc chặn khóa `DELIVERY_COMPLETION_PENDING` (G09-9); tạo issue làm rõ E07-09 (#139) | Quyết định nghiệp vụ của khách, không tự chốt (G-B9) |
| D5 | Backlog tính thế nào với prototype Lab 2 (22 màn hình chạy thật) | (a) tính từ đầu theo thiết kế Lab 4; (b) trừ phần đã có | (a) tính từ đầu; prototype chỉ là tham khảo | So 1–1 với ước lượng Lab 1, vốn cũng tính từ đầu (người dùng chốt ở phase 02) |
| D6 | Thứ tự khóa dòng trong `rpc_confirm_trade` | G08-5 ghi giao dịch → lô → người mua; TRD_CONFIRM_TRADE_DETAIL ghi lô → người mua (chưa có dòng giao dịch) | Theo TRD_CONFIRM (lô → người mua) và kiểm thứ tự khóa xuyên RPC ở E05-02c (#96) | Không mâu thuẫn thật: lúc chốt chưa có dòng giao dịch để khóa (G-A20) |
<!-- /auto:premise-decisions -->
