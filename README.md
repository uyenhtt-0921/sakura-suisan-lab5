# Product A (株式会社 桜水産市場) — LAB-5: backlog, ước lượng, báo cáo tiến độ

- **Dự án:** hệ thống vận hành chợ bán buôn thủy sản 株式会社 桜水産市場 (dự án luyện tập AIDD, dữ liệu hư cấu)
- **Mã học viên:** uyenhtt-0921
- **Đề:** Product A

## 1. Tổng quan

- Backlog chia từ **bộ thiết kế LAB-4 nộp ngày 2026-11-14** (9 tính năng, 48 màn hình, 43 đặc tả, 39 API, 10 thiết kế DB).
- **PREMISE.md có thay đổi:** 12 chỗ spec thêm / sửa, 17 giả định bổ sung, 6 hướng đã chốt — đều nêu nguồn là chỗ hở phát hiện khi break.
- **17 epic**, 193 issue (21 issue cha), 53 sub-issue; 225 việc có SWP, tổng **940 SWP = 6.580 giờ**; 18 issue làm rõ chờ khách.
- **Sprint giả lập đã chạy:** Sprint 1 (2026-11-16 → 2026-11-27) — nhận 43 SWP, xong 31 SWP; báo cáo ở `progress-report.md`.

## 2. Link

| Mục | Link |
|---|---|
| Repo | https://github.com/uyenhtt-0921/sakura-suisan-lab5 |
| GitHub Project | https://github.com/users/uyenhtt-0921/projects/2 |
| Báo cáo HTML chấm SWP (lần chính) | [`swp-report/estimate-swp-uyenhtt-0921-project-2-261117-0906.html`](swp-report/estimate-swp-uyenhtt-0921-project-2-261117-0906.html) |
| Báo cáo HTML chấm SWP (8 sub-issue tách thêm) | [`swp-report/estimate-swp-uyenhtt-0921-project-2-split-subissues-261117-0942.html`](swp-report/estimate-swp-uyenhtt-0921-project-2-split-subissues-261117-0942.html) |

**Mở thử bằng cửa sổ ẩn danh:** _chưa kiểm — cập nhật sau khi push (phase 07)._

## 3. Cấu trúc repo

| File / thư mục | Nội dung |
|---|---|
| `README.md` | Trang này: thông tin bài nộp, link, cấu trúc, bảng spec → epic |
| `PREMISE.md` | Backlog khác bản LAB-4 ở đâu: spec thêm / sửa, giả định, hướng đã chốt |
| `task-breakdown.md` | Nguyên tắc chia task, spec → issue, hạng mục 完納奨励金, chỗ hở của spec LAB-4 |
| `estimate.md` | Issue mẫu đã kiểm, cách quy ra giờ, tổng theo epic, so với LAB-1 |
| `progress-report.md` | Báo cáo Sprint 1: trạng thái, burndown, rủi ro trễ |
| `AI-report.md` | Cách dùng AI: skill, prompt, review, điểm đặc biệt |
| `swp-report/` | Báo cáo HTML của skill `tkm:estimate-swp` (2 lần chấm) |
| `images/` | Ảnh burndown Sprint 1 |
| `.gitignore` | Chặn file môi trường / khóa bí mật |

Không có thư mục `skills/`: bài dùng skill có sẵn của bộ Takumi, không tự viết hay chỉnh skill (các script phụ trợ nằm ngoài repo).

## 4. Spec → epic

Cột Spec liệt kê thư mục LAB-4 được issue của epic trích nhiều nhất; dòng PREMISE ghi ở cột Ghi chú.

<!-- auto:readme-spec-to-epic -->
| Spec (mã / file LAB-4, hoặc dòng PREMISE) | Epic trên Project (#số — tên) | Ghi chú |
|---|---|---|
| `specs/_common/`, `wireframes/`, `specs/trades/` | #12 — E01 Nền tảng ứng dụng và UI dùng chung | — |
| `adr/`, `specs/_common/`, `specs/system-design/database-design/_common/` | #13 — E02 Xác thực, tài khoản, phân quyền | PREMISE S3 |
| `specs/participants/`, `wireframes/`, `scope.md` | #14 — E03 Người tham gia và tư cách tham gia | PREMISE S4 |
| `specs/lots/`, `requirements/`, `wireframes/` | #15 — E04 Lô hàng: tiếp nhận, đánh giá, trạng thái | — |
| `specs/trades/`, `wireframes/`, `adr/` | #16 — E05 Giao dịch 相対 và kết quả せり | PREMISE S3 |
| `specs/adjustments/`, `specs/system-design/api-design/adjustments/`, `wireframes/` | #17 — E06 Điều chỉnh sau khi chốt (調整申請) | ràng buộc 完納奨励金 (`constraint:incentive`) |
| `specs/deliveries/`, `wireframes/`, `scope.md` | #18 — E07 Giao hàng (引渡し) | PREMISE S1, S8 |
| `specs/settlement/`, `specs/system-design/api-design/settlement/`, `wireframes/` | #19 — E08 Đối soát ngày, khóa ngày, tranh chấp, 入金 | ràng buộc 完納奨励金 (`constraint:incentive`); PREMISE S5, S10, S12 |
| `specs/settlement/`, `specs/adjustments/`, `scope.md` | #20 — E09 完納奨励金 | ràng buộc 完納奨励金 (`constraint:incentive`); PREMISE S2 |
| `adr/`, `specs/system-design/database-design/_common/`, `scope.md` | #1 — E10 Quy định và tỷ lệ theo phiên bản (規程・料率版) | ràng buộc 完納奨励金 (`constraint:incentive`); PREMISE S3 |
| `specs/reports/`, `specs/system-design/api-design/reports/`, `requirements/` | #21 — E11 Báo cáo cố định và CSV (K001) | ràng buộc 完納奨励金 (`constraint:incentive`) |
| `specs/accounting-export/`, `specs/system-design/api-design/accounting-export/`, `adr/` | #22 — E12 Xuất dữ liệu cho kế toán (K002) | PREMISE S7 |
| `specs/notifications/`, `requirements/`, `wireframes/` | #23 — E13 Thông báo trong ứng dụng và email | PREMISE S6 |
| `specs/_common/`, `adr/`, `specs/system-design/database-design/_common/` | #24 — E14 Nhật ký kiểm toán (audit log) | PREMISE S3 |
| `specs/_common/`, `adr/`, `scope.md` | #25 — E15 Vận hành chung: lịch, đính kèm, offline, giám sát, PDF, APPI | PREMISE S7, S11 |
| `adr/`, `scope.md`, `../` | #26 — E16 Chuyển đổi dữ liệu (N001, N002) | ràng buộc 完納奨励金 (`constraint:incentive`); PREMISE S9 |
| `specs/_common/`, `architecture/`, `adr/` | #27 — E17 Hạ tầng, môi trường, CI/CD | — |
<!-- /auto:readme-spec-to-epic -->
