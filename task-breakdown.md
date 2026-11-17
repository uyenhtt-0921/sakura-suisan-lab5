# Task breakdown — Product A (桜水産市場)

Backlog chia từ bộ thiết kế LAB-4 (nộp 2026-11-14) thành epic → issue → sub-issue trên
[GitHub Project](https://github.com/users/uyenhtt-0921/projects/2). Mọi bảng dưới đây sinh bằng script từ một file nguồn backlog duy nhất,
nên số issue khớp Project. Đường dẫn spec tính từ `lab4-design/specs/product-a/`.

## 1. Nguyên tắc chia task

**Độ hạt — chia tới đâu thì dừng**
- Một issue là **một kết quả kiểm được**: một màn hình + API của nó, một RPC / transaction có quy tắc, một job, một quy tắc nghiệp vụ có test.
- Dừng khi issue **≤ 6 SWP** (≤ 42 giờ, khoảng một nửa sprint 2 tuần của một người). Ban đầu ngưỡng là ≤ 5; sau khi chấm SWP thì 41 issue
  ở đúng mức 6, nên nới lên ≤ 6 và tách 4 issue ≥ 8 (xem `estimate.md` mục 1).
- Không chia vụn dưới khoảng nửa ngày; việc lặt vặt cùng màn hình gộp vào một issue.
- Tách backend và frontend thành hai issue khi mỗi phần từ khoảng 2 ngày trở lên; nhỏ hơn thì để một issue `fullstack`.

**Khi nào tách sub-issue**
- Việc lớn hơn ngưỡng nhưng là một khối giao chung (vd. `rpc_confirm_trade`: khung transaction, kiểm tư cách, test đua) → issue cha + sub-issue.
  Issue cha không tự làm; SWP và giờ của nó trên Project ghi bằng tổng con (khi cộng cột chỉ lấy việc có điểm trực tiếp để không trùng).
- Chỉ 2 tầng dưới epic: issue → sub-issue.

**Định nghĩa xong (DoD)**
- Mỗi issue có 2–4 dòng DoD kiểm được trong nội dung issue, gồm unit test / test DB cho phần mình.
- Issue làm rõ (`kind:clarification`): xong khi khách trả lời và spec đã cập nhật.
- Test hệ thống, UAT, diễn tập chuyển đổi không thành issue (mục 2, dòng cuối).

**Cách dùng epic → issue → sub-issue trên Project**
- 17 epic theo đúng 17 nhóm chức năng của LAB-1 (共通基盤, F01–F16, hạ tầng) để so sánh ước lượng; epic là issue nhãn `epic` + `epic:Exx`.
- Issue gắn vào epic, sub-issue gắn vào issue cha bằng quan hệ sub-issue gốc của GitHub; phụ thuộc giữa issue ghi bằng quan hệ "blocked by".
- Field trên Project: `Status` (Todo / In Progress / Blocked / Done), `Sprint` (Iteration), `Owner (giả định)` (vai trò BE1, BE2, FE-Lead,
  FE, QA, Infra — không gán tài khoản thật), `SWP` (điểm đã review), `Hours` (= SWP × 7).
- Nhãn: `kind:*` (backend / frontend / fullstack / infra / clarification), `constraint:*` (ràng buộc nghiệp vụ, trong đó `constraint:incentive`
  cho 完納奨励金).
- Quy mô: 17 epic, 193 issue (21 issue cha), 53 sub-issue → 225 việc có SWP; 18 issue làm rõ.

## 2. Spec → issue

Mọi tài liệu trong 3 danh mục của LAB-4 (43 đặc tả, 39 API, 10 DB = 92 tài liệu) đều có issue. Phần không thành issue nằm ở các dòng cuối.

<!-- auto:tb-spec-to-issue -->
| Spec (LAB-4) | Epic | Issue / sub-issue | Phần spec chưa thành issue và vì sao |
|---|---|---|---|
| SPEC-SD-001 `specs/_common/PLATFORM_DESIGN.md` | E01, E02, E04, E06, E07, E08, E10, E11, E12, E13, E14, E15, E16, E17 | #30, #32, #33, #34, #35, #36, #37, #39, #41, #53, #56, #57, #58, #59, #60, #54, #43, #80, #82, #85, #88, #105, #50, #142, #6, #3, #11, #181, #192, #196, #48, #204, #205, #206, #79, #208, #212, #216, #180, #217, #219, #220, #226, #210, #218, #225, #76, #228, #232, #239, #28, #29, #31, #242, #243, #244, #245, #246, #247, #248, #249, #250, #215, #251, #252, #253, #254, #255, #179 | — |
| SPEC-LAB4-312 `specs/accounting-export/ACC_EXPORT_BATCH_DETAIL.md` | E12 | #187, #188, #189 | — |
| SPEC-LAB4-307 `specs/accounting-export/ACCOUNTING_EXPORT_FUNCTIONS.md` | E12 | #187, #188, #189, #192, #186 | — |
| SPEC-LAB4-311 `specs/accounting-export/K002_SPEC.md` | E12 | #190 | — |
| SPEC-LAB4-242 `specs/adjustments/ADJ_CREATE_DETAIL.md` | E06 | #87 | — |
| SPEC-LAB4-241 `specs/adjustments/ADJ_DECISION_DETAIL.md` | E06, E09 | #108, #109, #110, #119, #111, #165, #258, #259 | — |
| SPEC-LAB4-230 `specs/adjustments/ADJUSTMENTS_FUNCTIONS.md` | E06, E09 | #47, #105, #110, #119, #120, #112, #162, #117, #118 | — |
| SPEC-LAB4-238 `specs/adjustments/F001_SPEC.md` | E06, E15 | #106, #121, #214 | — |
| SPEC-LAB4-239 `specs/adjustments/F002_SPEC.md` | E06 | #122 | — |
| SPEC-LAB4-240 `specs/adjustments/F003_SPEC.md` | E06 | #123 | — |
| SPEC-LAB4-201 `specs/deliveries/DELIVERIES_FUNCTIONS.md` | E07, E11, E16 | #50, #124, #127, #128, #129, #130, #133, #134, #135, #137, #174, #234 | — |
| SPEC-LAB4-206 `specs/deliveries/DLV_COMPLETE_DETAIL.md` | E07 | #125, #126, #127, #128, #139 | — |
| SPEC-LAB4-207 `specs/deliveries/DLV_RECORD_DETAIL.md` | E07, E15 | #124, #79, #212, #211 | — |
| SPEC-LAB4-205 `specs/deliveries/G002_SPEC.md` | E05, E07, E15 | #103, #131, #132, #133, #136, #213 | — |
| SPEC-LAB4-111 `specs/lots/C001_SPEC.md` | E01, E04, E15 | #38, #40, #41, #75, #78, #81, #92, #213, #214 | — |
| SPEC-LAB4-112 `specs/lots/C004_SPEC.md` | E04 | #84 | — |
| SPEC-LAB4-113 `specs/lots/LOT_CREATE_LOT_DETAIL.md` | E04, E15 | #73, #74, #77, #79, #211 | — |
| SPEC-LAB4-114 `specs/lots/LOT_RECORD_JUDGEMENT_DETAIL.md` | E04 | #83 | — |
| SPEC-LAB4-108 `specs/lots/LOTS_FUNCTIONS.md` | E04, E16 | #74, #80, #81, #82, #83, #233 | — |
| SPEC-LAB4-333 `specs/notifications/A004_SPEC.md` | E13 | #201 | — |
| SPEC-LAB4-330 `specs/notifications/NOTIFICATIONS_FUNCTIONS.md` | E13 | #191, #193, #194, #195, #198, #199, #200, #202, #203, #197 | — |
| SPEC-LAB4-334 `specs/notifications/NTF_SEND_RETRY_DETAIL.md` | E13 | #52, #191, #193, #194, #195, #196 | — |
| SPEC-LAB4-105 `specs/participants/B002_SPEC.md` | E03 | #65, #67, #72, #66 | — |
| SPEC-LAB4-107 `specs/participants/PAR_EVALUATE_ELIGIBILITY_DETAIL.md` | E03 | #69 | — |
| SPEC-LAB4-106 `specs/participants/PAR_SAVE_PARTICIPANT_DETAIL.md` | E03, E16 | #64, #230, #231 | — |
| SPEC-LAB4-101 `specs/participants/PARTICIPANTS_FUNCTIONS.md` | E03, E05, E11, E16 | #44, #64, #67, #69, #70, #71, #46, #68, #95, #175, #230 | — |
| SPEC-LAB4-305 `specs/reports/K001_SPEC.md` | E10, E11 | #8, #170, #173, #174, #175, #177, #178, #182, #183, #184, #185 | — |
| SPEC-LAB4-301 `specs/reports/REPORTS_FUNCTIONS.md` | E08, E11, E17 | #142, #169, #170, #173, #174, #175, #176, #177, #178, #181, #172, #254 | — |
| SPEC-LAB4-306 `specs/reports/RPT_RUN_EXPORT_DETAIL.md` | E11 | #169, #170, #171 | — |
| SPEC-LAB4-224 `specs/settlement/H001_SPEC.md` | E08, E15 | #142, #143, #222, #224, #221 | Nút PDF chờ câu trả lời E15-17 (PREMISE §1 S11) |
| SPEC-LAB4-225 `specs/settlement/H002_SPEC.md` | E08 | #150, #256, #257 | — |
| SPEC-LAB4-226 `specs/settlement/H003_SPEC.md` | E08 | #154 | — |
| SPEC-LAB4-227 `specs/settlement/H004_SPEC.md` | E08 | #155 | — |
| SPEC-LAB4-250 `specs/settlement/INC_CALCULATE_INCENTIVE_DETAIL.md` | E09, E10, E11 | #161, #112, #116, #162, #117, #111, #163, #118, #115, #165, #166, #167, #258, #259, #7, #3, #176 | — |
| SPEC-LAB4-210 `specs/settlement/SETTLEMENT_FUNCTIONS.md` | E07, E08, E09, E11 | #128, #113, #140, #145, #147, #151, #156, #164, #158, #173 | — |
| SPEC-LAB4-251 `specs/settlement/STL_DISPUTE_UPDATE_DETAIL.md` | E08 | #51, #151, #153 | — |
| SPEC-LAB4-252 `specs/settlement/STL_LOCK_AND_UNLOCK_REQUEST_DETAIL.md` | E08 | #144, #145, #147, #148 | — |
| SPEC-LAB4-229 `specs/settlement/STL_RECORD_PAYMENT_DETAIL.md` | E08, E09, E16 | #114, #156, #157, #159, #160, #116, #111, #164, #158, #235 | — |
| SPEC-LAB4-228 `specs/settlement/STL_UNLOCK_DECISION_DETAIL.md` | E08 | #149 | — |
| SPEC-LAB4-117 `specs/trades/D001_SPEC.md` | E01, E05, E15 | #38, #41, #98, #100, #222, #223 | — |
| SPEC-LAB4-118 `specs/trades/E001_SPEC.md` | E01, E05 | #40, #99 | — |
| SPEC-LAB4-115 `specs/trades/TRADES_FUNCTIONS.md` | E05, E16 | #93, #94, #97, #234 | — |
| SPEC-LAB4-119 `specs/trades/TRD_CONFIRM_TRADE_DETAIL.md` | E05, E15 | #93, #94, #95, #96, #223 | — |
| SPEC-LAB4-308 `specs/system-design/api-design/accounting-export/API-ACC-001_API.md` | E12 | #146, #190 | — |
| SPEC-LAB4-309 `specs/system-design/api-design/accounting-export/API-ACC-002_API.md` | E12 | #188 | — |
| SPEC-LAB4-310 `specs/system-design/api-design/accounting-export/API-ACC-003_API.md` | E12 | #189 | — |
| SPEC-LAB4-231 `specs/system-design/api-design/adjustments/API-ADJ-001_API.md` | E06 | #87 | — |
| SPEC-LAB4-232 `specs/system-design/api-design/adjustments/API-ADJ-002_API.md` | E06 | #120 | — |
| SPEC-LAB4-233 `specs/system-design/api-design/adjustments/API-ADJ-003_API.md` | E06 | #120 | — |
| SPEC-LAB4-234 `specs/system-design/api-design/adjustments/API-ADJ-004_API.md` | E06 | #108, #109 | — |
| SPEC-LAB4-235 `specs/system-design/api-design/adjustments/API-ADJ-005_API.md` | E06 | #87 | — |
| SPEC-LAB4-236 `specs/system-design/api-design/adjustments/API-ADJ-006_API.md` | E06, E15 | #107, #77 | — |
| SPEC-LAB4-237 `specs/system-design/api-design/adjustments/API-ADJ-007_API.md` | E06 | #106 | — |
| SPEC-LAB4-202 `specs/system-design/api-design/deliveries/API-DLV-001_API.md` | E07, E15 | #124, #209 | — |
| SPEC-LAB4-203 `specs/system-design/api-design/deliveries/API-DLV-002_API.md` | E07 | #125 | — |
| SPEC-LAB4-204 `specs/system-design/api-design/deliveries/API-DLV-003_API.md` | E07 | #129, #138 | — |
| SPEC-LAB4-109 `specs/system-design/api-design/lots/API-LOT-001_API.md` | E04, E15 | #74, #209, #211 | — |
| SPEC-LAB4-110 `specs/system-design/api-design/lots/API-LOT-002_API.md` | E04 | #83 | — |
| SPEC-LAB4-120 `specs/system-design/api-design/lots/API-LOT-003_API.md` | E04, E15 | #78, #77 | — |
| SPEC-LAB4-331 `specs/system-design/api-design/notifications/API-NTF-001_API.md` | E13 | #200 | — |
| SPEC-LAB4-332 `specs/system-design/api-design/notifications/API-NTF-002_API.md` | E13 | #200 | — |
| SPEC-LAB4-102 `specs/system-design/api-design/participants/API-PAR-001_API.md` | E03 | #64 | — |
| SPEC-LAB4-103 `specs/system-design/api-design/participants/API-PAR-002_API.md` | E03 | #64 | — |
| SPEC-LAB4-104 `specs/system-design/api-design/participants/API-PAR-003_API.md` | E03 | #70 | — |
| SPEC-LAB4-302 `specs/system-design/api-design/reports/API-RPT-001_API.md` | E11 | #171, #184 | — |
| SPEC-LAB4-303 `specs/system-design/api-design/reports/API-RPT-002_API.md` | E11 | #171, #184 | — |
| SPEC-LAB4-304 `specs/system-design/api-design/reports/API-RPT-003_API.md` | E11 | #171, #185 | — |
| SPEC-LAB4-211 `specs/system-design/api-design/settlement/API-STL-001_API.md` | E08, E15 | #140, #224 | — |
| SPEC-LAB4-212 `specs/system-design/api-design/settlement/API-STL-002_API.md` | E08, E15 | #141, #221 | — |
| SPEC-LAB4-213 `specs/system-design/api-design/settlement/API-STL-003_API.md` | E08 | #150, #256, #257 | — |
| SPEC-LAB4-214 `specs/system-design/api-design/settlement/API-STL-004_API.md` | E08 | #144, #145 | — |
| SPEC-LAB4-215 `specs/system-design/api-design/settlement/API-STL-005_API.md` | E08 | #148 | — |
| SPEC-LAB4-216 `specs/system-design/api-design/settlement/API-STL-006_API.md` | E08 | #149 | — |
| SPEC-LAB4-217 `specs/system-design/api-design/settlement/API-STL-007_API.md` | E08 | #152 | — |
| SPEC-LAB4-218 `specs/system-design/api-design/settlement/API-STL-008_API.md` | E08 | #152 | — |
| SPEC-LAB4-219 `specs/system-design/api-design/settlement/API-STL-009_API.md` | E08 | #152 | — |
| SPEC-LAB4-220 `specs/system-design/api-design/settlement/API-STL-010_API.md` | E08 | #153 | — |
| SPEC-LAB4-221 `specs/system-design/api-design/settlement/API-STL-011_API.md` | E08 | #114, #160 | — |
| SPEC-LAB4-222 `specs/system-design/api-design/settlement/API-STL-012_API.md` | E08 | #157 | — |
| SPEC-LAB4-223 `specs/system-design/api-design/settlement/API-STL-013_API.md` | E08 | #114 | — |
| SPEC-LAB4-253 `specs/system-design/api-design/settlement/API-STL-014_API.md` | E08 | #159 | — |
| SPEC-LAB4-116 `specs/system-design/api-design/trades/API-TRD-001_API.md` | E05 | #97 | — |
| SPEC-DB-001 `specs/system-design/database-design/_common/COMMON_DATABASE.md` | E01, E02, E06, E08, E09, E10, E14, E15, E16, E17 | #32, #42, #57, #61, #43, #47, #107, #161, #168, #49, #2, #4, #6, #7, #9, #5, #11, #48, #205, #207, #77, #214, #216, #76, #233, #215, #260, #261 | — |
| SPEC-DB-009 `specs/system-design/database-design/accounting-export/ACCOUNTING_EXPORT_DATABASE.md` | E12 | #146 | — |
| SPEC-DB-007 `specs/system-design/database-design/adjustments/ADJUSTMENTS_DATABASE.md` | E06, E09 | #47, #161 | — |
| SPEC-DB-005 `specs/system-design/database-design/deliveries/DELIVERIES_DATABASE.md` | E07, E08 | #50, #134, #135, #137, #49 | — |
| SPEC-DB-003 `specs/system-design/database-design/lots/LOTS_DATABASE.md` | E04, E16 | #73, #85, #233 | — |
| SPEC-DB-010 `specs/system-design/database-design/notifications/NOTIFICATIONS_DATABASE.md` | E13, E15, E17 | #52, #197, #180, #249 | — |
| SPEC-DB-002 `specs/system-design/database-design/participants/PARTICIPANTS_DATABASE.md` | E03, E16 | #44, #66, #231 | — |
| SPEC-DB-008 `specs/system-design/database-design/reports/REPORTS_DATABASE.md` | E11 | #169 | — |
| SPEC-DB-006 `specs/system-design/database-design/settlement/SETTLEMENT_DATABASE.md` | E08, E15, E16 | #113, #51, #49, #45, #235 | — |
| SPEC-DB-004 `specs/system-design/database-design/trades/TRADES_DATABASE.md` | E05, E16 | #91, #101, #234 | — |
| Lab 1 WBS: quản lý dự án, BrSE / phiên dịch, chạy test hệ thống (ST, UAT, hồi quy, tải, bảo mật), diễn tập chuyển đổi, đào tạo, hỗ trợ vận hành ban đầu | — | — | Việc gắn lịch và con người, không chia thành kết quả kiểm được; giữ ở WBS. Unit test và test tự động nằm trong DoD từng issue |
| `scope.md` §3 phần "lưu bản scan" dữ liệu cũ hơn 1 năm | E16 | — | Chưa rõ ai giữ bản scan; hỏi trong E16-01 |
| Xuất kế toán tự động theo lịch (Lab 1 F12-01 "システム（バッチ）") | E12 | — | YAGNI cho tới khi khách trả lời E12-07 (G-C20) |
<!-- /auto:tb-spec-to-issue -->

## 3. Hạng mục chịu ràng buộc đặc thù: 完納奨励金

完納奨励金 có nhiều biến (phiên bản tỷ lệ theo ngày, thời điểm 入金, điều chỉnh trước / sau khi tính, làm tròn, đồng thời). Mỗi biến một issue
riêng, nhãn `constraint:incentive`, để chấm điểm, test và theo dõi từng biến; gộp chung thì không biết biến nào đã xong, biến nào đang chờ khách.

<!-- auto:tb-constraints -->
| Ràng buộc | Issue | Vì sao tách riêng |
|---|---|---|
| Bảng kết quả và delta 奨励金 (tử số nguyên, unique theo lần chạy + người mua + phiên bản) | #161 | Nền dữ liệu cho mọi biến bên dưới; sai khóa unique thì tính trùng |
| Tỷ lệ theo loại người mua, lấy từ phiên bản quy định có hiệu lực theo ngày giao dịch | #112, #260, #261, #7, #3 | Biến "phiên bản theo ngày": đổi tỷ lệ không được làm sai kỳ đã tính (bẫy §2) |
| "Đúng hạn" tính từ 入金 thật (gồm dòng đảo âm), không đọc trades.paid_date | #116 | Biến "đúng hạn": nguồn dữ liệu khác Lab 2; chặn bởi câu hỏi E09-11 |
| Lần tính đầu của kỳ đọc cả adjustment_lines đã duyệt (G08-4) | #162 | Biến "điều chỉnh trước khi tính": bỏ sót thì tính trên số chưa sửa |
| Làm tròn xuống một lần mỗi người mua mỗi kỳ sau khi cộng phần chưa làm tròn (G09-3) | #117 | Biến "làm tròn": làm tròn từng dòng cho 330 thay vì 331 (test vector) |
| Khóa theo người mua + kỳ cho mọi đường sinh delta và chạy tính (G09-6) | #111 | Biến "đồng thời": hai đường chạy cùng lúc sinh delta sai |
| Lưu kết quả kỳ nguyên tử, chặn tính lại kỳ đã có | #163 | Biến "kỳ đã tính": sửa sau khi tính chỉ qua delta (bẫy §5) |
| Delta sang kỳ sau = floor(Σ sau) − floor(Σ trước) khi điều chỉnh được duyệt sau khi đã tính (FR-INC-03) | #118, #119 | Biến "delta kỳ sau": không sửa kết quả kỳ đã chốt |
| 入金 đổi / bị hủy sau khi kỳ đã tính → tự sinh delta; hủy 入金 cần người khác duyệt (G09-2) | #164, #158, #156, #157, #159, #160 | Biến "入金 sau khi tính": nguồn delta thứ hai, có maker ≠ checker |
| Định nghĩa 適格金額, 支払期日, ngưỡng tối thiểu, "kỳ sau" | #115 | Câu hỏi khách; chặn E09-03 nên tách thành issue riêng để theo dõi |
| Bộ test vector và test tích hợp đồng thời | #165, #258, #259 | Chứng minh từng biến bằng số cụ thể (FIG-013, BR-INC-01) |
| API, I001, I002 hiển thị phiên bản áp dụng và căn cứ tính | #166, #167, #168 | FR-AUDIT-03: mỗi kết quả phải chỉ ra phiên bản đã áp dụng |
| Báo cáo RPT-07 dùng lại truy vấn I001; nhập 入金 lịch sử không sinh delta | #176, #235 | Số 奨励金 ở báo cáo và dữ liệu chuyển đổi phải khớp màn hình |
<!-- /auto:tb-constraints -->

## 4. Chỗ hở / mâu thuẫn của spec LAB-4 phát hiện khi break

89 chỗ hở do 3 agent ghi trong lúc chia (`G-A` epic E01–E05, `G-B` E06–E09, `G-C` E10–E17), main session phân loại cách xử lý.

<!-- auto:tb-gaps -->
| Mã | Spec | Chỗ hở / mâu thuẫn | Xử lý |
|---|---|---|---|
| G-A1 | `scope.md` §3; `wireframes/_catalogue.md`; `specs/_common/PLATFORM_DESIGN.md` §7 | A001, A002, M001, M002, M003 không có spec riêng (BM-51/52/53), không có wireframe HTML; chỉ có một dòng trong catalogue và đoạn bảo mật ở PLATFORM_DESIGN. Các issue E02-06, E02-08, E02-11 chỉ trỏ catalogue + scope + PLATFORM. Tương tự B001, B003, B004, C002, C003, C005, D002, D003, E002 chỉ có một dòng mô tả (review đã ghi nhận: `review/independent-review.md` dòng 116, 128). | đã sửa thiết kế — PREMISE §1 dòng S3 |
| G-A2 | `specs/_common/PLATFORM_DESIGN.md` §7, §8 (N7), §11 Q2; NFR-SEC-03 | Ngưỡng khóa tài khoản (số lần sai, số phút khóa), thời gian timeout phiên, thời gian giữ log kỹ thuật: RFP không nêu, PLATFORM ghi 要確認. | giả định — PREMISE §2 dòng A1 |
| G-A3 | PREMISE §5 Q2; `specs/_common/PLATFORM_DESIGN.md` §6 (A10); ADR-002 | Phạm vi MFA: mặc định SYS_ADMIN, RULE_ADMIN và 「người có quyền duyệt」, nhưng danh sách quyền duyệt (F003, mở khóa H002, đảo 入金 G09-2, duyệt phiên bản quy định J003?) chưa được liệt kê thành bảng vai trò. Ma trận quyền 7 vai trò × tính năng chưa có tài liệu Lab 4 nào chốt (PREMISE §2 #6 ghi RFP chưa chốt; Lab 2 có map 16 khóa). | giả định — PREMISE §2 dòng A2 |
| G-A4 | ADR-002; `scope.md` §3 (M003 🟡 chỉ xem) | M003 ở Lab 2 là chỉ xem; ADR-002 đặt bảng quyền trong mã (không trong DB) nên màn hình không thể sửa quyền. Lab 1 (F01-03) ghi 「ロール・権限管理」 mà không nói có sửa được ma trận hay không. | giả định — PREMISE §2 dòng A3 |
| G-A5 | PREMISE §4 #10; `specs/_common/api-list.md`; COMMON_DATABASE §4.1-4.2 | Không có spec RPC/API cho quản lý tài khoản (tạo/sửa, tạm dừng, mở khóa, đặt lại MFA): tên RPC, quy trình mật khẩu ban đầu và đặt lại mật khẩu, chính sách mật khẩu đều chưa được mô tả; chỉ có quy tắc 「tài khoản không xóa, luôn còn ≥ 1 SYS_ADMIN」 (Lab2-A#10). `api-list.md` không có API nhóm auth/accounts. | đã sửa thiết kế — PREMISE §1 dòng S3 |
| G-A6 | `specs/_common/PLATFORM_DESIGN.md` §8 (Đo KPI), §10 D4, D7 | Đổi chiều trách nhiệm log KPI: PLATFORM D7 gộp 「log có cấu trúc cho KPI」 chung với diễn tập DR; brief chia 「giám sát, KPI」 cho E15. E01-04 chỉ làm thư viện log ở route handler; việc thu thập KPI-01..05 và Sentry nằm E15/E17. | giả định — PREMISE §2 dòng A13 |
| G-A7 | `specs/_common/PLATFORM_DESIGN.md` §3; ADR-003, ADR-004; `COMMON_DATABASE.md` §4.3, §4.9 | Phụ thuộc chéo nhiều epic: `write_audit` + audit_logs (E14), trigger `guard_locked_day` và ngoại lệ cột tiến độ/`lots.state` (E06/E08), hạ tầng đính kèm Storage + bảng `attachments` (E15), khung offline PWA (E15), thẻ đếm A003 lấy từ E06/E07/E08/E13. Hầu hết issue E02-E05 có ghi `depends_on` dạng mô tả vì chưa biết id. | đã sửa thiết kế — PREMISE §3 dòng D1 |
| G-A8 | `specs/participants/B002_SPEC.md` §6 Q7 | Lưu hồ sơ người tham gia: hai người sửa cùng lúc có dùng khóa lạc quan không (B002_SPEC Q7, API-PAR-002). | để mở — Khóa lạc quan hay "người lưu sau thắng" do Tech Lead chọn khi làm E03-02; không đổi ước lượng |
| G-A9 | `requirements/REQ-2611-01-participants.md` §4 (FR-PARTY-005), §8 Q2; B002_SPEC Q6 | Khoảng cảnh báo 失効間近 mặc định bao nhiêu ngày, và nơi cấu hình (M004? bảng tham số riêng?). Thông báo email/in-app cho người sắp hết hạn (FR-PARTY-005 AC3) thuộc E13 nhưng chưa thấy issue hứa hẹn. | giả định — PREMISE §2 dòng A1 |
| G-A10 | `wireframes/_catalogue.md` (B004); `scope.md` §3 | B004 độc lập hay gộp vào B001: Lab 1 liệt kê B004 là một màn hình riêng (F02-04), Lab 2 và catalogue Lab 4 giữ cách gộp (B001 lọc 失効間近 + thẻ A003). scope.md vẫn đếm 48 màn hình gồm B004. | đã sửa thiết kế — PREMISE §1 dòng S4 |
| G-A11 | `specs/system-design/database-design/lots/LOTS_DATABASE.md` (Q3); `requirements/REQ-2611-02-lots.md` §4; domain-traps | Trạng thái lô 「公開」 (FR-LOT-007 liệt kê 受付 → 下見済 → 公開 → 確定 → 引渡し完了) không có trong enum DB `lot_state` (received, inspected, in_trade, sold_out, delivered). Chưa rõ có bước 公開 hay không. Ngoài ra có hai bộ mã trùng tên: REQ dùng FR-LOT-001..009 còn RFP dùng FR-LOT-01..04 (FR-LOT-004 nghĩa là offline ở REQ nhưng là 「điều chỉnh thuộc tính」 ở RFP). | giả định — PREMISE §2 dòng A4 |
| G-A12 | `requirements/REQ-2611-02-lots.md` §8; `specs/lots/LOTS_FUNCTIONS.md` §3; PLATFORM §11 Q5 | C001/offline và đính kèm còn nhiều tham số chưa có nguồn: định dạng và dung lượng tối đa của 受付伝票 (REQ-02 Q2), ngưỡng 「mất mạng ngắn」 (NFR-AVL-02), ai xử lý mục 同期失敗 và hòa giải (REQ-02 Q3), thời hạn giữ và việc xóa hàng đợi khi đăng xuất trên tablet dùng chung (LOTS_FUNCTIONS Q3), khóa nghiệp vụ chặn lô trùng gồm trường nào (REQ-02 Q1), thang đánh giá 目利き (REQ-02 Q4). | giả định — PREMISE §2 dòng A1 |
| G-A13 | `specs/lots/LOTS_FUNCTIONS.md` §3 Q4; ADR-012; PLATFORM §3 | Ranh giới E04/E15 cho offline: E04-05 chỉ làm hàng đợi phía màn hình C001 (submit/flush), còn PWA, service worker, nơi lưu hàng đợi (IndexedDB?) và cơ chế chung dùng cho G002/G003 do E15. LOTS_FUNCTIONS Q4 để mở 「nơi lưu hàng đợi」. | giả định — PREMISE §2 dòng A13 |
| G-A14 | PREMISE §4 #5; `specs/trades/TRADES_FUNCTIONS.md` §2.4 | `due_date` = ngày nghiệp vụ + 30 là giả định của Lab 2 (RFP không cho số ngày), 要確認 (Lab1-QA#8). Issue E05-01 ghi cứng 30 ngày; nếu khách đổi thì ảnh hưởng 奨励金 (E09) và báo cáo. | giả định — PREMISE §2 dòng A1 |
| G-A15 | `specs/trades/TRADES_FUNCTIONS.md` §3 Q2; REQ-2611-03 Q3 | Giới hạn nhập giao dịch (quantity 1..100.000, unit_price 1..100.000.000) do Lab 2 đặt, RFP không nêu; đơn vị số lượng chờ Lab1-QA#11. Chưa quyết có đưa xuống DB. | giả định — PREMISE §2 dòng A1 |
| G-A16 | `requirements/REQ-2611-03-trades.md` §8; PREMISE §5 Q10; `specs/participants/PARTICIPANTS_FUNCTIONS.md` §3 | Bốn điều khách chưa trả lời ảnh hưởng thẳng đến luồng chính: (a) 卸売業者 có làm người mua không; (b) 買出人/卸売業者 xét hiệu lực theo trường nào; (c) hai người chốt cùng lô, người sau bị từ chối có đúng ý khách (REQ-03 Q1); (d) 相対 có cần bước 「chờ xác nhận」 người thứ hai (REQ-03 Q4, FIG-012). D001_SPEC và PLATFORM đang giả định một bước chốt. | tạo issue làm rõ #68 (E03-10) |
| G-A17 | `review/independent-review.md` dòng 128; `specs/_common/api-list.md` | Không có BM-51/52/53 và không có danh mục API cho: hủy giao dịch (`rpc_cancel_trade`, D003), tra cứu D002/E002, C005, tra cứu C002/C003. `api-list.md` chỉ có 39 API; review đã chấp nhận D003 là 「để Lab sau」. | đã sửa thiết kế — PREMISE §1 dòng S3 |
| G-A18 | Lab 1 dòng #9; `specs/deliveries/DLV_COMPLETE_DETAIL.md` | Dòng Lab 1 F02-03 gắn với D001, E001 và G002; E03-05/E03-06 chỉ làm hàm dùng chung. Phần gọi hàm trong transaction là E05-02b (D001, E001) và issue của E07 (G002) - nhóm làm E07 phải gắn `lab1: F02-03` cho phần mình để tránh thiếu phủ. | đã sửa thiết kế — PREMISE §3 dòng D3 |
| G-A19 | `requirements/REQ-2611-01-participants.md` §4 (FR-PARTY-003); `COMMON_DATABASE.md` §4.3 | Nguồn lịch sử đổi trạng thái người tham gia (B003): không có bảng riêng; FR-PARTY-003 yêu cầu lưu người, thời điểm, lý do, trước/sau, hợp lý nhất là `audit_logs`. B003 vì thế phụ thuộc E14 (cần màn hình/truy vấn đọc audit theo đối tượng). | giả định — PREMISE §2 dòng A5 |
| G-A20 | PREMISE §6 G08-5; `specs/trades/TRD_CONFIRM_TRADE_DETAIL.md` §5 | Thứ tự khóa G08-5 (giao dịch → lô → người mua) khác thứ tự thực tế trong `rpc_confirm_trade` (lô → người mua, vì chưa có dòng trade); đã được TRD_CONFIRM_TRADE_DETAIL ghi chú. Rủi ro: RPC khác tự suy diễn thứ tự khác. | đã sửa thiết kế — PREMISE §3 dòng D6 |
| G-B1 | `scope.md` (I001, I002); `_common/api-list.md`; `INC_CALCULATE_INCENTIVE_DETAIL.md` ("chưa có BM-52") | I001 và I002 không có spec màn hình, không có BM-52 (không có API-INC trong `api-list.md`), chỉ có scope + catalogue + BM-53 tính 奨励金. I002 "gộp vào I001" nhưng Lab 1 F09-03 vẫn là một dòng riêng | đã sửa thiết kế — PREMISE §1 dòng S2 |
| G-B2 | `scope.md` (G001, G004); `api-design/deliveries/`; `wireframes/_catalogue.md` | G001 và G004 không có spec, không có wireframe riêng; API-DLV chỉ có 3 API (ghi, hoàn tất, chi tiết), không có API danh sách cho G001 | đã sửa thiết kế — PREMISE §1 dòng S1 |
| G-B3 | `DELIVERIES_FUNCTIONS.md` §2.9; `DELIVERIES_DATABASE.md` Q4 | G003: chưa đặt tên RPC ghi ngoại lệ; chưa có wireframe và API; `client_request_id` của `delivery_exceptions` còn mở (diff D3 chỉ nêu `lots`, `delivery_events`) | đã sửa thiết kế — PREMISE §1 dòng S8 |
| G-B4 | `scope.md` (H005); `STL_RECORD_PAYMENT_DETAIL.md` §5; PREMISE §4 #8 | H005 không có wireframe, không có BM-51, và không thuộc dòng Lab 1 nào (bổ sung Lab 4). Hủy 入金 cũng không có dòng Lab 1. Quy tắc phủ "mọi dòng Lab 1" không áp dụng cho các issue này | giả định — PREMISE §2 dòng A17 |
| G-B5 | PREMISE §6; PLATFORM_DESIGN | Phụ thuộc chéo epic chưa có id của nhóm khác: E10 (`rate_versions`, `rate_version_items`) cho E09-02, E08-03 (cột 適用規程版); E12 (`accounting_export_batches`) cho E08-08, E08-09, E08-07b; E15 (khung hàng đợi offline, PDF, `attachments`) cho E07-06b, E07-07c, E06-05; E02 (MFA AAL2) cho E06-06a, E08-09, E08-15b | đã sửa thiết kế — PREMISE §3 dòng D1 |
| G-B6 | `PLATFORM_DESIGN.md` A4; `ADJUSTMENTS_FUNCTIONS.md` §2.8; ADR-003 | Chủ sở hữu trigger khóa ngày chung (`guard_locked_day`, `business_date_of`) chồng nhau giữa E01 / E04 / E05 và E06-02, E07-01. Ở đây chỉ làm phần của adjustments (danh sách miễn, trigger chỉ-thêm) và phần giao hàng (G09-1, G09-4, G09-7) | đã sửa thiết kế — PREMISE §1 dòng S12 |
| G-B7 | `ADJUSTMENTS_FUNCTIONS.md` (Câu hỏi mở); `SETTLEMENT_FUNCTIONS.md` §3; PREMISE §5 Q2 | Vai trò lập / duyệt điều chỉnh, vai trò xin / duyệt mở khóa, vai trò duyệt hủy 入金, phạm vi MFA đều 要確認 | giả định — PREMISE §2 dòng A2 |
| G-B8 | `SETTLEMENT_FUNCTIONS.md` §2.7, 2.8, 2.4; REQ-2611-05 Q1, Q2, Q9 | Tranh chấp: danh sách trạng thái, loại nguyên nhân, SLA, prefix `dispute_code`, `resolution` có bắt buộc khi resolved, và "còn tranh chấp mở thì khóa ngày được không" đều 要確認 | giả định — PREMISE §2 dòng A6 |
| G-B9 | `DLV_COMPLETE_DETAIL.md` §4.5; `independent-review.md` §6, §7.2 | R-19 + N-10: ai xác nhận tư cách khi 完了確定, và ngày D không khóa được khi người mua bị đình chỉ sau khi đã nhận đủ hàng (`DELIVERY_COMPLETION_PENDING`) | tạo issue làm rõ #139 (E07-09) |
| G-B10 | Lab1-QA#1, #8; PREMISE §5 Q4; REQ-2611-06 Q4; `INC_CALCULATE_INCENTIVE_DETAIL.md` §5 | 適格金額, 支払期日 (+30 ngày), ngưỡng tối thiểu, mỗi phiên bản có đủ 4 loại không, và "kỳ sau" nhận delta là kỳ nào + `posting_business_date` đều chưa chốt. Chặn việc tính đúng | tạo issue làm rõ #115 (E09-11) |
| G-B11 | `INC_CALCULATE_INCENTIVE_DETAIL.md` §4.1, 4.2; `DELIVERIES_FUNCTIONS.md` §2.3 | Mã lỗi thiếu phiên bản quy định, thiếu loại người mua, lỗi kỳ trùng khoảng (409) đều "mã: 要確認"; `CONFIRMER_REQUIRED` chưa có trong `error-codes.md` | giả định — PREMISE §2 dòng A9 |
| G-B12 | `SETTLEMENT_FUNCTIONS.md` §2.10; `ADJ_DECISION_DETAIL.md` §4.1 | Mâu thuẫn nhỏ: `SETTLEMENT_FUNCTIONS.md` §2.10 đặt tiêu đề hai hàm xin / duyệt đảo nhưng bảng chữ ký ghi `rpc_reverse_payment`; `ADJUSTMENTS_FUNCTIONS.md` §2.4 nói kiểm AAL2 trong transaction còn `ADJ_DECISION_DETAIL.md` §4.1 nói kiểm ở route trước khi vào DB | đã sửa thiết kế — PREMISE §1 dòng S5 |
| G-B13 | `F002_SPEC.md`; `REPORTS_FUNCTIONS.md`; `H001_SPEC.md` §6 | Hai chỗ trùng đầu ra: nhật ký điều chỉnh F06-04 (F002) và báo cáo RPT-08 (K001, E11); 滞留 / số tranh chấp trên A003 (E01); RPT-07 奨励金 (E11) và RPT-05 đối soát (E08-05 batch 11:00 JST vs batch báo cáo ngày ở E11) | giả định — PREMISE §2 dòng A12 |
| G-B14 | `DELIVERIES_FUNCTIONS.md` §2.8, §3 | Offline G002: có cộng tạm mục chưa gửi vào 「累積」 hay không, và cách hòa giải xung đột khi đồng bộ (REQ-2611-04 Q5) còn 要確認 | giả định — PREMISE §2 dòng A7 |
| G-B15 | `H001_SPEC.md` §4.1 mục E.5; `independent-review.md` §8; Lab 1 dòng #56 | Wireframe H001 chưa có khối 「当日完了の精算対象取引」; H002 đã thêm ba trạng thái chặn (N-09 đã xử lý ở main session) nhưng PNG có thể chưa chụp lại. Nút PDF của H001 bị khóa, trong khi Lab 1 F15-05 yêu cầu PDF 照合表 (E15) | đã sửa thiết kế — PREMISE §1 dòng S10 |
| G-B16 | `ADJUSTMENTS_DATABASE.md`; `COMMON_DATABASE.md` | Bảng `incentive_adjustments` nằm trong BM-50 của adjustments nhưng logic sinh delta chia ba nơi (điều chỉnh E06-06c, 入金 E09-09, hủy 入金 E09-10) | đã sửa thiết kế — PREMISE §3 dòng D2 |
| G-C1 | CDB §4.5 (Q9), §4.8; independent-review.md dòng 115; scope.md §3 | J001–J003 không có spec riêng (không phải màn hình lõi, không có wireframe HTML); không có REQ và không có hàm `rpc_*` nào ghi `rate_versions` / `rate_version_items` (Lab 2 chỉ đọc). Tên RPC trong issue (`rpc_save_rate_version_draft`, `rpc_publish_rate_version`, `rpc_withdraw_rate_version`) là đề xuất của backlog. | đã sửa thiết kế — PREMISE §1 dòng S3 |
| G-C2 | CDB §4.5 (Q7); domain-traps §2; ADR-006 | Rút lại (`withdrawn`): lưu người/thời điểm/lý do bằng `audit_logs` hay cột riêng, và DB có trigger chặn sửa bản `published` hay không (Lab 2 không có trigger) — CDB để mở, domain-traps §2 lại cấm sửa bản đã công bố. | giả định — PREMISE §2 dòng A14 |
| G-C3 | domain-traps §2; ADR-006 (Bối cảnh) | GOV-RULE-01 "≤ 4 lần/năm": không nói đếm theo ngày công bố hay `effective_from`, và rút lại có tính vào số lần không. Không có spec cho cơ chế cưỡng chế. | tạo issue làm rõ #5 (E10-09) |
| G-C4 | CDB §4.8, §5 Q4 | Mỗi phiên bản có bắt buộc đủ 4 loại người tham gia hay cho thiếu (vd 買出人 không có 奨励金). | tạo issue làm rõ #5 (E10-09) |
| G-C5 | ADR-006; INC_CALCULATE_INCENTIVE_DETAIL §4.2 | Rút lại một bản đã được dùng bởi `incentive_results` đã tính: ADR-006/INC detail chỉ nói bản withdrawn không bao giờ được chọn, không nói kết quả đã tính, kỳ chưa tính nhưng thuộc ngày hiệu lực của bản đó, hay có sinh delta. | tạo issue làm rõ #5 (E10-09) |
| G-C6 | glossary-ja-vi (vai trò); PD §6 A10; PREMISE §4 #7 | Ai là người duyệt: chỉ có ROLE-RULE-ADMIN (規程管理者) liên quan quy định; maker ≠ checker cần ít nhất hai tài khoản có quyền công bố, TBL-ROLE-01 không nói rõ SYS_ADMIN có được công bố hay không. MFA bắt buộc cho RULE_ADMIN (A10). | tạo issue làm rõ #5 (E10-09) |
| G-C7 | Lab 1 #40, #42; K001_SPEC §6.4; REPORTS_FUNCTIONS §2.1 | F10-04 (J001 版履歴) và F11-02 (RPT-12) cùng nguồn mã RPT-12; REQ-07 Q2 còn để mở tham số của RPT-12 (`month` hay `rule_version_id`/`effective_date`). | giả định — PREMISE §2 dòng A12 |
| G-C8 | PREMISE §4 #5; CDB §4.5; PD §6 A7 | "規程" (quy định) rộng hơn tỷ lệ 奨励金: hạn thanh toán 30 ngày, ngưỡng cảnh báo 失効間近, ngưỡng thông báo là hằng số/cấu hình ngoài phiên bản; Lab 4 chỉ phiên bản hóa tỷ lệ + thuế. Lab 1 gọi chung "規程・料率版". | để mở — Ngoài phạm vi thiết kế Lab 4 (chỉ phiên bản hóa tỷ lệ); hỏi khi khách yêu cầu phiên bản hóa quy định khác |
| G-C9 | REPORTS_FUNCTIONS §2.2, §3; REQ-07 Q2, Q3 | Danh sách cột, thứ tự, đơn vị RPT-01..12 và tập giá trị bộ lọc chưa có (Lab1-QA#15); mã hóa/dấu phân cách/tên file CSV chưa chốt; số dòng tối đa chưa có. Chặn mọi issue báo cáo cụ thể. | tạo issue làm rõ #172 (E11-12) |
| G-C10 | REPORTS_FUNCTIONS §2.2 | RPT-02 cần lịch sử trạng thái lô nhưng không có bảng log trạng thái; nguồn "log trạng thái" còn `要確認`. | giả định — PREMISE §2 dòng A5 |
| G-C11 | REPORTS_FUNCTIONS §2.7; PD §5 EV4, §11 Q7 | Lịch chạy batch báo cáo ngày, công cụ lập lịch, ngày mặc định ("ngày làm việc trước đó" cần lịch M004), số lần tự thử lại và có lưu file batch không đều là `要確認`. | tạo issue làm rõ #179 (E17-13) |
| G-C12 | API-STL-002; K001_SPEC §3; PV G1 | Hai đường CSV cho cùng dữ liệu đối soát: API-STL-002 (CSV H001) và RPT-05 trong K001; Lab 2 cũng có CSV 奨励金 ở I001 trùng RPT-07. Số liệu có thể lệch nếu viết hai nơi. | giả định — PREMISE §2 dòng A12 |
| G-C13 | K001_SPEC §3; Lab 1 #41-#42 | K001 nói "12 báo cáo cố định" nhưng chạy được 11 (RPT-06 chỉ là liên kết sang K002); Lab 1 F11-01 liệt kê 8 báo cáo ngày không có RPT-06. Không mâu thuẫn nhưng dễ đếm sai. | giả định — PREMISE §2 dòng A12 |
| G-C14 | REPORTS_FUNCTIONS §2.2; PD §8 N5 | Không phân trang ở bản 0.1; ngày cao điểm 1.200 giao dịch, giới hạn thời gian/bộ nhớ của serverless khi dựng CSV chưa được đo. | giả định — PREMISE §2 dòng A16 |
| G-C15 | REPORTS_FUNCTIONS §3; REQ-07 Q1 | Ma trận vai trò xem/xuất từng báo cáo chưa có; vai trò 市場管理者 xuất hiện ở REQ nhưng không có trong `app_role`. | tạo issue làm rõ #172 (E11-12) |
| G-C16 | ACCOUNTING_EXPORT_FUNCTIONS §2.2-2.3, §3; REQ-08 Q1, Q2 | Cột CSV, đơn vị gộp, cách lấy tiền thuế (chỉ 奨励金 có thuế trong Lab 2, `trades` chỉ có `amount`), trạng thái dòng (chờ/đã xác nhận/đã điều chỉnh), cách kế toán nhận file. Chặn E12-02. | tạo issue làm rõ #186 (E12-07) |
| G-C17 | REQ-08 Q4, Q5; ACCOUNTING_EXPORT_FUNCTIONS §3 | Lỗi xuất có phải Critical và ai nhận cảnh báo chưa chốt. | tạo issue làm rõ #197 (E13-10) |
| G-C18 | NOTIFICATIONS_DATABASE §5 Q8; PD §5 EV1 | F12-02 "出力エラー監視" cần nguồn cảnh báo (M007); nguồn M007 chưa chốt (notification_deliveries hay bảng riêng). | đã sửa thiết kế — PREMISE §1 dòng S7 |
| G-C19 | ACCOUNTING_EXPORT_FUNCTIONS §2.5, §3 | Xuất lại lô đã `succeeded` có cho không, và dòng điều chỉnh sau khóa vào batch nào (sau khi lô đầu đã gửi). | tạo issue làm rõ #186 (E12-07) |
| G-C20 | ACCOUNTING_EXPORT_FUNCTIONS §2.6; K002_SPEC | Lab 1 F12-01 ghi tác nhân "ROLE-SETTLEMENT / システム（バッチ）" nhưng wireframe K002 chỉ có nút thủ công; xuất tự động còn `要確認`. | tạo issue làm rõ #186 (E12-07) |
| G-C21 | REQ-09 Q1, Q2; NOTIFICATIONS_FUNCTIONS §3 | Danh sách sự kiện cần thông báo, sự kiện Critical, người nhận mỗi sự kiện chưa có. Chặn việc nối nguồn sự kiện (E13-04, E13-05) và cấu hình M005. | tạo issue làm rõ #197 (E13-10) |
| G-C22 | NOTIFICATIONS_FUNCTIONS §2.1 | Người nhận nội bộ có nhận email không: `profiles` không có cột email (email ở `auth.users`); Lab 1 F13-01 nói "アプリ内・電子メール". | tạo issue làm rõ #197 (E13-10) |
| G-C23 | NOTIFICATIONS_FUNCTIONS §2.1 | `rpc_enqueue_notification` không có khóa chống trùng khi batch chạy lại cùng sự kiện. | đã sửa thiết kế — PREMISE §1 dòng S6 |
| G-C24 | NOTIFICATIONS_FUNCTIONS phạm vi; REQ-09 mục 7 (FR-NOTI-005/006 `no-spec`) | M005 và M006 chỉ có wireframe một dòng (FUNC 2.8, 2.9), không có BM-51, không có API riêng; M006 ai được xem và có gửi lại tay không đều mở. | đã sửa thiết kế — PREMISE §1 dòng S3 |
| G-C25 | Lab 1 #46 | Lab 1 F13-01 liệt kê A003 (đếm thông báo ở dashboard); phần màn hình thuộc E01, không nằm trong E13. | giả định — PREMISE §2 dòng A13 |
| G-C26 | NTF_SEND_RETRY_DETAIL §4.5; REQ-09 Q4, Q5 | Khoảng cách thử lại và cách hiểu "tối đa 3" chưa có; Critical phải xong trong 5 phút nên tần suất worker phải nhỏ hơn khoảng thử lại; phụ thuộc công cụ lập lịch (tần suất tối thiểu). | tạo issue làm rõ #197 (E13-10) |
| G-C27 | independent-review.md dòng 116; CDB §4.3; wireframes/_catalogue.md (L001) | L001 không có REQ/spec riêng (chỉ FR-AUDIT-02 và wireframe một dòng). Bộ lọc "参加者" không có cột tương ứng trong `audit_logs` (chỉ `entity_type/entity_id` + jsonb). | đã sửa thiết kế — PREMISE §1 dòng S3 |
| G-C28 | CDB §4.3, §5 Q2; ADR-004 (Hệ quả) | `audit_logs.actor_id` không có FK (cố ý hay sót — Q2); owner DB vẫn tắt được trigger; `TRUNCATE` phải thu ở prod. | giả định — PREMISE §2 dòng A10 |
| G-C29 | ADR-004 (Hệ quả); PD §7 | Cần kế hoạch lưu `audit_logs` 7 năm (bảng chỉ lớn lên); thời gian giữ log kỹ thuật `要確認`. | giả định — PREMISE §2 dòng A10 |
| G-C30 | ADR-004; CDB §4.3 | Ai được đọc audit: RLS chỉ SETTLEMENT và SYS_ADMIN; RULE_ADMIN (duyệt phiên bản) và người duyệt điều chỉnh không có quyền xem lịch sử mình duyệt. | để mở — Giữ RLS hiện hành (SETTLEMENT, SYS_ADMIN); mở quyền đọc audit cho người duyệt là quyết định bảo mật của khách |
| G-C31 | PD §7; các FUNCTIONS | Không có danh mục mã `action` cho audit; mỗi spec hàm tự đặt (`trade.confirm`, `report.run`, `accounting.export`...). | giả định — PREMISE §2 dòng A15 |
| G-C32 | SETTLEMENT_DATABASE §5 Q5; PV E6; wireframes/_catalogue.md (M004) | M004: chọn cột `is_market_holiday` hay bảng lịch, ngày nghỉ có chặn thao tác không, "業務日の開始・締め" (giờ mở/đóng) không có thiết kế. | giả định — PREMISE §2 dòng A11 |
| G-C33 | CDB §4.9, §5 Q8 | Đính kèm: định dạng, dung lượng tối đa, có xóa tệp không, tệp có dữ liệu cá nhân không, tải khi offline có không — còn mở. | tạo issue làm rõ #76 (E15-19) |
| G-C34 | PD §5 EV6, §11 Q8 | Lưu lạnh sau 3 năm: chưa có cơ chế (EV6 ghi "Chưa có cơ chế: 要確認"), nơi lưu và cách lấy lại chưa chốt. Lab 1 INF-9 và F15-02 đều đòi. | tạo issue làm rõ #76 (E15-19) |
| G-C35 | ADR-012 (Hệ quả); PD §11 Q5; REQ-04 Q5 | Offline: ngưỡng "mất mạng ngắn", cách hòa giải xung đột sau đồng bộ, `client_request_id` cho `delivery_exceptions` (G003, "còn hỏi"), tải ảnh khi offline. | tạo issue làm rõ #210 (E15-15) |
| G-C36 | ADR-012 (Hệ quả); PD §6 A10 | Hàng đợi offline nằm trên thiết bị (IndexedDB): mất thiết bị là mất thao tác chưa gửi, dữ liệu chưa mã hóa; thiết bị dùng chung (A10 nói mỗi người một tài khoản). | để mở — Mã hóa hàng đợi phía thiết bị ngoài phạm vi; ghi là rủi ro khi dùng thiết bị chung |
| G-C37 | NOTIFICATIONS_DATABASE §5 Q8; wireframes/_catalogue.md (M007) | M007: nguồn dữ liệu chưa chốt (`notification_deliveries` hay bảng riêng), không có schema cảnh báo hệ thống, không có phân loại cảnh báo. | đã sửa thiết kế — PREMISE §1 dòng S7 |
| G-C38 | scope.md §2; REQ-07 §2.3; H001_SPEC mục 6; API-STL-002 | **Mâu thuẫn PDF:** Lab 1 F15-05 và scope.md giao PDF 取引票 (D001) / 照合表 (H001), nhưng REQ-07 loại PDF, K001 "chỉ CSV", H001_SPEC khóa nút PDF "hạng mục sau", API-STL-002 ghi PDF ngoài phạm vi. Không có mẫu biểu 取引票/照合表, không biết thiết bị in (INV-DEVICE-01). | tạo issue làm rõ #221 (E15-17) |
| G-C39 | wireframes/_catalogue.md (M008); PD §7, §8 N8, N9; ADR-004 | M008 không có spec nào (không REQ, không BM-50/51), chỉ wireframe một dòng và nhắc APPI ở PD. Yêu cầu 削除/訂正 mâu thuẫn với lưu 7 năm, append-only (`audit_logs`, `payments`) và không xóa tài khoản/người tham gia. | tạo issue làm rõ #225 (E15-18) |
| G-C40 | PD §8 (Đo KPI); PREMISE §3.1 #1, §5 Q3 | Công thức KPI-01..05 chờ khách; KPI-02 đo ở client/kịch bản UAT; KPI-05 cần nhật ký cuộc gọi ngoài hệ thống. U-19 là hạng mục mới nên không có dòng nào trong 60 dòng Lab 1 (issue KPI để `lab1: []`). | tạo issue làm rõ #218 (E15-16) |
| G-C41 | PD §5 EV2-EV6, §11 Q7 | Nhiều job định kỳ (batch báo cáo, quét thông báo, worker email, quét lần chạy treo, lưu lạnh, xuất tự động nếu có) nhưng chưa chọn công cụ lập lịch; tần suất tối thiểu ảnh hưởng Critical 5 phút. | tạo issue làm rõ #179 (E17-13) |
| G-C42 | Lab 1 #53; api-list.md | Ranh giới trách nhiệm đính kèm: F15-02 "không có màn hình" nhưng API-LOT-003 (E04) và API-ADJ-006 (E06) là endpoint của epic khác. | giả định — PREMISE §2 dòng A13 |
| G-C43 | scope.md §3; PD; PREMISE §2 #2 | N001/N002 không có spec/wireframe chi tiết, không có thiết kế DB staging/mapping/lô chuyển đổi; PD không có mục chuyển đổi (chỉ PREMISE §2 #2). Lab 1 tham chiếu MIG-01..04 nhưng nội dung chỉ có trong RFP. | đã sửa thiết kế — PREMISE §1 dòng S9 |
| G-C44 | PREMISE §2 #2, §5 Q7 | Mốc "1 năm gần nhất" tính từ ngày nào (go-live, ngày cắt dữ liệu, năm lịch); Lab1-QA#6 vẫn `New`. | tạo issue làm rõ #228 (E16-01) |
| G-C45 | ADR-003, ADR-004; PD §6 A4, A12; PREMISE §6 G09-2 | Nhập lịch sử đụng ràng buộc Lab 4: trigger khóa ngày (nhập vào ngày đã khóa), `audit_logs`/`payments` append-only (rollback là xóa), bộ đếm mã L-/T-/S-, phiên bản tỷ lệ cho 奨励金 lịch sử (chưa có phiên bản nào trước go-live), 入金 nhập lịch sử có thể sinh delta (G09-2). Chưa có hướng. | tạo issue làm rõ #239 (E16-11) |
| G-C46 | Lab 1 #58 (DS-DIRTY-01) | Định dạng, chất lượng dữ liệu nguồn (DS-DIRTY-01), danh sách master và khối lượng chưa biết; bộ quy tắc làm sạch chưa thể định nghĩa. | tạo issue làm rõ #228 (E16-01) |
| G-C47 | Lab 1 #59; PREMISE §2 #2 | N002 "金額照合" cần số liệu nguồn làm chuẩn (control total) — ai cung cấp, dạng nào chưa nói. Phần cũ hơn 1 năm "lưu bản scan ★" không có issue/chủ. | tạo issue làm rõ #228 (E16-01) |
| G-C48 | PD §8 (Môi trường), §11 Q9 | Phạm vi Terraform "要確認" (Vercel, Supabase, DNS, giám sát có provider hay không). | tạo issue làm rõ #179 (E17-13) |
| G-C49 | PD §7, §11 Q2; CDB §5 Q1 | Rate limit nằm trong Lab 1 INF-10 nhưng không có spec nào cho cơ chế và ngưỡng; ngưỡng khóa tài khoản/timeout phiên `要確認` (NFR-SEC-03). | giả định — PREMISE §2 dòng A1 |
| G-C50 | PD §5 EV2, §11 Q7 | Tên miền, chủ sở hữu DNS và nhà cung cấp email chưa biết. | tạo issue làm rõ #179 (E17-13) |
| G-C51 | PD §8 N3; PREMISE §2 #9 | PITR yêu cầu gói Supabase phù hợp; thời gian giữ PITR và quy trình restore thực tế chưa có trong spec. RPO 15 phút / RTO 4 giờ chỉ là mục tiêu. | giả định — PREMISE §2 dòng A16 |
| G-C52 | PD §8 N1, §10 | Quy tắc "không deploy prod trong 02:00-10:00 JST" là quy tắc thiết kế, chưa có cơ chế cưỡng chế. | giả định — PREMISE §2 dòng A16 |
| G-C53 | PD §4, §10, §11 Q9 | Người sở hữu migration `要確認`; bước bỏ `trades.paid_date` / `rate_versions.rate_bp` không hoàn tác; ngưỡng dừng phát hành `要確認`. | tạo issue làm rõ #179 (E17-13) |
<!-- /auto:tb-gaps -->
