# Estimate — Product A (桜水産市場)

**Báo cáo HTML của skill `tkm:estimate-swp`:**
- [`swp-report/estimate-swp-uyenhtt-0921-project-2-261117-0906.html`](swp-report/estimate-swp-uyenhtt-0921-project-2-261117-0906.html) — lần chính, 221 việc.
- [`swp-report/estimate-swp-uyenhtt-0921-project-2-split-subissues-261117-0942.html`](swp-report/estimate-swp-uyenhtt-0921-project-2-split-subissues-261117-0942.html) — lần bổ sung, 8 sub-issue tách từ 4 issue ≥ 8 SWP.

Tải về rồi mở bằng trình duyệt (file tự chứa, không cần mạng). SWP và giờ của từng issue nằm trong field `SWP`, `Hours` trên
[Project](https://github.com/users/uyenhtt-0921/projects/2).

## 1. Issue mẫu skill chọn để kiểm

Skill chọn 5 issue mẫu mỗi lần chấm bằng script (thấp nhất, trung vị, cao nhất, lệch xa trung vị, độ tin cậy thấp nhất). Mỗi issue được duyệt
riêng, hai bước: chọn mức khó, rồi chọn điểm cụ thể.

<!-- auto:estimate-samples -->
| Issue | Lần chấm | Skill chấm (Scope × Complexity → SWP) | Bạn chốt | Lý do |
|---|---|---|---|---|
| #66 [E03-11] Làm rõ với khách: chuyển trạng thái theo FIG-010 (gỡ tạm dừng 仲卸 / 売買参加者) có ép ở server không, có thêm trạng thái 登録 không | chính (221 việc) | S1 × C0 → 1 SWP | 1 SWP (giữ nguyên) | Đồng ý: một câu hỏi cho khách + cập nhật 3 chỗ spec, không lập trình |
| #164 [E09-09] 入金 thay đổi sau khi kỳ đã tính: tự sinh incentive_adjustments nguồn payment_id (G09-2) | chính (221 việc) | S2 × C3 → 4 SWP | 4 SWP (giữ nguyên) | Đồng ý: phạm vi hẹp trong rpc_record_payment; độ khó ở khóa và 入金 trả một phần song song |
| #2 [E10-01] Migration phiên bản quy định–tỷ lệ: maker/checker là user, trạng thái withdrawn, rate_version_items, chặn sửa bản đã công bố | chính (221 việc) | S5 × C3 → 10 SWP | 10 SWP (giữ nguyên) | Đồng ý: migration đổi ràng buộc, bảng mới, chuyển dữ liệu seed, trigger, RLS (sau đó tách thành #260 + #261 vì ≥ 8) |
| #150 [E08-10] H002 業務日ロック・締め解除画面 + API-STL-003 danh sách ngày nghiệp vụ | chính (221 việc) | S5 × C2 → 8 SWP | 8 SWP (giữ nguyên) | Đồng ý: một màn hình nhiều trạng thái chặn + API danh sách (sau đó tách thành #256 + #257 vì ≥ 8) |
| #68 [E03-10] Làm rõ với khách: 買出人 và 卸売業者 xét hiệu lực theo trường nào, nguồn dữ liệu, và 卸売業者 có được làm người mua không | chính (221 việc) | S1 × C0 → 1 SWP | 1 SWP (giữ nguyên) | Đồng ý: câu hỏi cho khách + cập nhật spec |
| #261 [E10-01b] Bất biến bản đã công bố: trigger chặn UPDATE/DELETE bản published (chỉ chuyển withdrawn qua RPC) + RLS chỉ đọc | bổ sung (8 sub-issue) | S2 × C2 → 3 SWP | 3 SWP (giữ nguyên) | Đồng ý: một trigger + RLS trên một bảng |
| #258 [E09-12a] Bộ test vector 奨励金 chạy tự động trong CI (FIG-013 / BR-INC-01) | bổ sung (8 sub-issue) | S3 × C2 → 5 SWP | 5 SWP (giữ nguyên) | Đồng ý: 6 vector cố định, làm tròn cần thiết kế số liệu |
| #259 [E09-12b] Bộ test tích hợp 奨励金 đồng thời: 入金 song song, 入金 lúc I001 đang chạy, 入金 đảo, điều chỉnh sau khi tính | bổ sung (8 sub-issue) | S3 × C3 → 6 SWP | 6 SWP (giữ nguyên) | Đồng ý: 4 kịch bản song song, kiểm khóa người mua + kỳ |
| #256 [E08-10a] API-STL-003 danh sách ngày nghiệp vụ kèm trạng thái chặn từng ngày (khóa, xin mở khóa, lý do chặn) | bổ sung (8 sub-issue) | S3 × C2 → 5 SWP | 5 SWP (giữ nguyên) | Đồng ý: một endpoint gộp nhiều trạng thái chặn |
| #262 [E16-02a] Bảng khung chuyển đổi: migration_batches, staging theo loại dữ liệu, bảng ánh xạ, cột migration_batch_id, RLS chỉ SYS_ADMIN | bổ sung (8 sub-issue) | S3 × C2 → 5 SWP | 5 SWP (giữ nguyên) | Đồng ý: vài bảng mới + cột trên bảng nghiệp vụ; spec chưa có (G-C43) |
<!-- /auto:estimate-samples -->

**Vì sao giữ nguyên cả 10:** mỗi điểm khớp với khối lượng đọc được từ DoD của issue, và các mẫu trải đủ từ câu hỏi cho khách (1 SWP) tới
migration nhiều ràng buộc (10 SWP). Không sửa điểm nào nên không có quy tắc hiệu chỉnh lan sang issue khác (trạng thái `accepted`).
Việc cần làm sau khi duyệt là chuyện độ hạt: 4 issue ≥ 8 SWP (#2, #150, #165, #229) vượt ngưỡng nên được tách thành 8 sub-issue và chấm lại.

## 2. Cách quy ra giờ

- **Cách chọn:** quy ước đổi SWP ra giờ bằng một hệ số cố định, không ước giờ trực tiếp cho từng issue.
- **Vì sao:** SWP đã có cách chấm nhất quán (Scope × Complexity tra bảng); ước giờ trực tiếp cho 225 việc dễ lệch theo người ước.
  Hệ số lấy từ dữ liệu LAB-1 để có cơ sở so sánh.
- **Quy tắc:** **Giờ = SWP × 7.** Giờ gồm làm, unit test, sửa lỗi, đã trừ 20% nhờ AI (giống Plan B của LAB-1); không gồm dự phòng 30%,
  vì dự phòng tính ở mức dự án như LAB-1.
- **Cách ra hệ số 7:** chấm Scope × Complexity cho 9 dòng chức năng LAB-1 (từ màn hình xem log tới nhập dữ liệu cũ), chia giờ LAB-1 (Plan B,
  không dự phòng) cho SWP → 7,16 giờ / SWP (khoảng 5,2–9,7); lấy 7 vì bằng đúng 1 ngày công của LAB-1.
- **Áp dụng nhất quán:** script ghi `Hours = SWP × 7` lên Project cho mọi việc có SWP và đọc lại để kiểm (0 lệch). Issue cha và epic ghi
  **tổng các issue con** (SWP và giờ), nên mọi issue trên Project đều có số. Giờ epic = tổng giờ issue; không làm tròn ở bước nào.
- **Lưu ý khi cộng cột trên Project:** chỉ cộng các việc có điểm trực tiếp (bỏ issue nhãn `epic` và issue có sub-issue), nếu không sẽ
  tính trùng. Tổng 225 việc = tổng 17 epic = 940 SWP.

## 3. Tổng theo epic

<!-- auto:estimate-epics -->
| Epic | Số issue (có SWP) | Tổng SWP | Tổng giờ | Ghi chú |
|---|---|---|---|---|
| #12 E01 Nền tảng ứng dụng và UI dùng chung | 12 | 45 | 315 | 1 issue cha (tổng con) |
| #13 E02 Xác thực, tài khoản, phân quyền | 11 | 49 | 343 | — |
| #14 E03 Người tham gia và tư cách tham gia | 11 | 37 | 259 | 2 issue làm rõ |
| #15 E04 Lô hàng: tiếp nhận, đánh giá, trạng thái | 14 | 51 | 357 | 1 issue cha (tổng con); 1 issue làm rõ |
| #16 E05 Giao dịch 相対 và kết quả せり | 12 | 52 | 364 | 1 issue cha (tổng con); 1 issue làm rõ |
| #17 E06 Điều chỉnh sau khi chốt (調整申請) | 12 | 54 | 378 | 1 issue cha (tổng con) |
| #18 E07 Giao hàng (引渡し) | 14 | 61 | 427 | 3 issue cha (tổng con); 1 issue làm rõ |
| #19 E08 Đối soát ngày, khóa ngày, tranh chấp, 入金 | 21 | 89 | 623 | 4 issue cha (tổng con) |
| #20 E09 完納奨励金 | 16 | 63 | 441 | 1 issue cha (tổng con); 1 issue làm rõ |
| #1 E10 Quy định và tỷ lệ theo phiên bản (規程・料率版) | 11 | 39 | 273 | 1 issue cha (tổng con); 1 issue làm rõ |
| #21 E11 Báo cáo cố định và CSV (K001) | 14 | 52 | 364 | 1 issue cha (tổng con); 1 issue làm rõ |
| #22 E12 Xuất dữ liệu cho kế toán (K002) | 7 | 30 | 210 | 1 issue làm rõ |
| #23 E13 Thông báo trong ứng dụng và email | 12 | 50 | 350 | 1 issue cha (tổng con); 1 issue làm rõ |
| #24 E14 Nhật ký kiểm toán (audit log) | 5 | 24 | 168 | — |
| #25 E15 Vận hành chung: lịch, đính kèm, offline, giám sát, PDF, APPI | 23 | 95 | 665 | 1 issue cha (tổng con); 5 issue làm rõ |
| #26 E16 Chuyển đổi dữ liệu (N001, N002) | 14 | 73 | 511 | 2 issue cha (tổng con); 2 issue làm rõ |
| #27 E17 Hạ tầng, môi trường, CI/CD | 16 | 76 | 532 | 3 issue cha (tổng con); 1 issue làm rõ |
| **Tổng** | **225** | **940** | **6.580** | 1 SWP = 7 giờ; chưa gồm dự phòng 30% |
<!-- /auto:estimate-epics -->

Thêm dự phòng 30% như LAB-1 thì 6.580 giờ → 8.554 giờ.

## 4. So với estimate LAB-1

Cột LAB-1 là giờ phát triển theo chức năng (sheet `01_Server` BE + FE + Design, và `03_Infrastructure`), Plan B (có giảm 20% nhờ AI),
**chưa gồm dự phòng** — cùng cách tính với LAB-5. Quản lý, BrSE, test hệ thống, UAT của LAB-1 không có trong cả hai cột.

<!-- auto:estimate-lab1 -->
| Phần (chức năng LAB-1 → epic) | LAB-1 (giờ) | LAB-5 (giờ) | Chênh | Vì sao |
|---|---|---|---|---|
| 共通基盤 → E01 | 158,9 | 315 | +156,1 (×1,98) | Thêm thư viện JST / JPY, quy ước bàn phím và bộ component tách riêng; Lab 1 gộp trong 3 dòng |
| F01 認証・アカウント管理 → E02 | 161,7 | 343 | +181,3 (×2,12) | MFA, khóa tài khoản, hết phiên, RLS mọi bảng tách thành issue riêng (PREMISE §2 A1, A2) |
| F02 参加者・参加資格管理 → E03 | 182,3 | 259 | +76,7 (×1,42) | Gần Lab 1; thêm 2 issue làm rõ (E03-10, E03-11) |
| F03 ロット受付・評価記録 → E04 | 228,6 | 357 | +128,4 (×1,56) | Thêm offline phía C001 (E04-05a/b) và điều chỉnh thuộc tính lô có làm rõ |
| F04 相対取引 + F05 せり結果記録 → E05 | 251,0 | 364 | +113,0 (×1,45) | Kiểm tư cách trong transaction + bộ test đua (Lab 4 G08-1, G08-5); hủy giao dịch có làm rõ |
| F06 確定後修正（調整申請・承認） → E06 | 163,8 | 378 | +214,2 (×2,31) | Lab 4 thêm draft, trả về, lịch sử adjustment_events, delta 奨励金 (G08-2, G08-3, G08-6) |
| F07 引渡し（荷受け）管理 → E07 | 249,2 | 427 | +177,8 (×1,71) | Giao nhiều ngày theo ngày của chính lần giao (G09-1, G09-7), offline G002 / G003, R-19 (PREMISE §3 D4) |
| F08 照合・締め処理 → E08 | 159,9 | 623 | +463,1 (×3,89) | Lab 4 thêm H005 入金 + hủy có duyệt (G04-3, G09-2), mở khóa có duyệt và 3 điều kiện chặn (G04-2, G09-5), nền khóa ngày (PREMISE §1 S12) |
| F09 完納奨励金計算 → E09 | 143,5 | 441 | +297,5 (×3,07) | Các biến G08-4, G09-2, G09-3, G09-6 thành issue riêng; API / màn hình mới (PREMISE §1 S2); bộ test vector + đồng thời |
| F10 規程・料率版管理 → E10 | 126,7 | 273 | +146,3 (×2,15) | Thêm bảng rate_version_items, trigger bất biến (PREMISE §2 A14), bỏ cột cũ có kiểm soát (E10-10) |
| F11 報告・CSV出力 → E11 | 188,3 | 364 | +175,7 (×1,93) | 11 báo cáo tách riêng, batch 11:00 và lần chạy treo (PREMISE §2 A12) |
| F12 会計システム連携 → E12 | 74,5 | 210 | +135,4 (×2,82) | Lô xuất, chặn mở khóa khi đã xuất (G09-5), cảnh báo lỗi (PREMISE §1 S7) |
| F13 通知 → E13 | 128,4 | 350 | +221,6 (×2,72) | Hàng đợi outbox, worker thử lại, Critical trong 5 phút, chống trùng (PREMISE §1 S6) |
| F14 監査証跡 → E14 | 80,2 | 168 | +87,8 (×2,10) | Thêm danh mục mã hành động và kế hoạch lưu 7 năm (PREMISE §2 A10, A15) |
| F15 共通・運用基盤 → E15 | 242,2 | 665 | +422,8 (×2,75) | Khung offline 5 phần, đo KPI U-19 không có ở Lab 1 (PREMISE §2 A17), 5 issue làm rõ |
| F16 データ移行 → E16 | 128,8 | 511 | +382,2 (×3,97) | Thiết kế chuyển đổi chưa có, issue tự thiết kế (PREMISE §1 S9); 2 issue làm rõ |
| 03_Infrastructure → E17 | 254,8 | 532 | +277,2 (×2,09) | Terraform, CI / CD, rate limit tách nhỏ; load test và hỗ trợ DR là môi trường chuẩn bị |
| **Tổng** | **2.922,9** | **6.580** | **+3.657,1 (×2,25)** | Thêm lý do chung: hệ số 7 giờ / SWP hiệu chỉnh trên dòng Lab 1 cấp chức năng nên cao với issue nhỏ (mục 2) |
<!-- /auto:estimate-lab1 -->

**Đọc bảng:** LAB-5 gấp khoảng 2,25 lần LAB-1. Hai nguyên nhân gộp lại:
1. **Thiết kế LAB-4 chi tiết hơn bản LAB-1 ước lượng.** Các quyết định G04–G09, màn hình H005, đo KPI, offline và chuyển đổi dữ liệu thành
   issue riêng; lệch lớn nhất ở E08 đối soát, E16 chuyển đổi, E09 完納奨励金 và E12 xuất kế toán.
2. **Hệ số 7 giờ / SWP lấy từ dòng LAB-1 cấp chức năng.** Với issue nhỏ hơn, mỗi issue mang thêm phần chi phí cố định (review, tích hợp),
   nên tổng giờ cao hơn khi chia mịn. Không chỉnh ngược hệ số cho khớp LAB-1, vì như vậy phép so sánh mất ý nghĩa.

Hệ quả cho lịch nằm ở `progress-report.md` mục 3 (rủi ro mốc vận hành chính thức).
