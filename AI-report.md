# Báo cáo sử dụng AI — LAB-5

Thời gian: 2026-11-16 → 2026-11-17.
Công cụ: Claude Code (Opus điều phối) + bộ kỹ năng Takumi (`tkm:*`), `gh` CLI. Mục 3 là ý kiến của người làm.

## 1. Skill, prompt và agent cho từng việc

| Việc | Skill / cách làm | Agent (model) | Prompt / brief tiêu biểu |
|---|---|---|---|
| Lập kế hoạch | `tkm:create-plan` | main session | 8 phase, 6 cổng duyệt; bảng quyết định (repo / Project public, cách quy giờ, sprint, owner giả định) do người dùng chốt trước |
| Quy giờ | Script đọc Excel LAB-1 (dựng lại công thức vì file không lưu giá trị) + rubric của `tkm:estimate-swp` | main session | "Chấm Scope × Complexity cho 9 dòng chức năng LAB-1 trải từ nhỏ tới lớn, chia giờ Plan B không dự phòng cho SWP, đề xuất một hệ số và nêu giới hạn" |
| Break task | Brief chung + 3 agent song song, ghép bằng script | 3 agent (Sonnet): E01–E05, E06–E09, E10–E17 | Brief: 17 epic cố định theo nhóm LAB-1; schema YAML (id, epic, cha, kind, owner, dòng LAB-1, spec, mã tham chiếu, 2–4 dòng DoD); độ hạt ≤ 5 ngày; "mỗi biến 完納奨励金 một issue"; "không bịa: mỗi issue phải có spec mở được; chỗ hở ghi vào file gaps, không tự quyết". Danh sách 60 dòng LAB-1 đưa vào **không kèm ngày công** để không neo |
| Đưa lên GitHub | Script `gh` (dấu `backlog-id` trong body + file ánh xạ để chạy lại không trùng; `--parent`, `--blocked-by` gốc của GitHub); hướng dẫn `tkm:git-issues`, `tkm:git-projects` | main session | Chạy thử 1 epic → đọc lại → chạy hết; mọi lần ghi đều đọc lại để kiểm |
| Chấm SWP | `tkm:estimate-swp` (`--no-push-kpi`), `tkm:confidence` | 5 worker (Sonnet) cho 221 việc; main session chấm trực tiếp 8 sub-issue bổ sung | Worker chỉ được đọc file lô của mình + rubric, ghi một file JSON; validator của skill tính lại SWP theo ma trận |
| Ghi SWP / giờ lên Project | Script `gh project item-edit` | main session (không giao agent) | Ghi `SWP` và `Hours = SWP × 7` cho 225 việc, bỏ qua item đã đúng, đọc lại toàn bộ (0 lệch, tổng 940) |
| Báo cáo tiến độ | Nhật ký sprint (YAML) → script vẽ burndown + sinh bảng số liệu | main session | "Giả lập phải có lệch kế hoạch thật; số liệu báo cáo = Project = nhật ký; mỗi rủi ro có người và hạn" |
| File nộp | Bảng sinh bằng script từ nguồn duy nhất (backlog, điểm SWP, ánh xạ số issue, file nội dung tự soạn) | main session | Script báo lỗi nếu id hay mã PREMISE không tồn tại, hoặc chỗ hở chưa có cách xử lý |

Không viết hay chỉnh skill nào; các script phụ trợ là script dùng một lần của bài, để ngoài repo.

## 2. Review output của AI

**Con người duyệt ở 7 cổng:** bảng đổi giờ (cổng 01); backlog + PREMISE (02); xác nhận trước khi tạo repo / Project / 255 issue public (03);
10 issue mẫu SWP, từng issue hai bước (04); hai quyết định sau khi chấm — giữ hệ số 7 giờ dù lệch LAB-1, nới độ hạt thành ≤ 6 và tách 4 issue (04);
báo cáo tiến độ trước khi ghi trạng thái lên Project (05); xác nhận trước khi push (07).

**Máy kiểm trước khi đưa người duyệt:** script ghép backlog kiểm id trùng, cha 2 tầng, spec mở được, phủ đủ 75 dòng LAB-1 và 92 tài liệu
LAB-4, phụ thuộc trỏ tới id có thật, không vòng phụ thuộc; validator của skill SWP; script đọc lại GitHub sau mọi lần ghi; script nhật ký sprint
kiểm ngày, phụ thuộc, năng lực. Mỗi luật kiểm mới đều được thử bằng một lỗi cố ý để chắc nó bắt được.

**Vấn đề phát hiện trong output của AI và cách xử lý:**

| Vấn đề | Phát hiện bởi | Xử lý |
|---|---|---|
| Plan ghi "issue ≤ 2 ngày = SWP ≤ 8" nhưng hệ số 7 giờ / SWP cho thấy SWP 8 = 8 ngày | main session khi quy giờ | Đưa ra cổng 01; người dùng chốt ≤ 5, sau nới thành ≤ 6 |
| 3 agent break task để lại 27 phụ thuộc dạng mô tả ("E14 (write_audit)") và không ai nhận trigger khóa ngày chung | main session đối chiếu chéo 3 phần | Đổi sang id thật; thêm issue nền khóa ngày (PREMISE §1 S12); thêm luật kiểm vào script |
| Worker SWP ghi nhóm việc `Unknown` với độ tin cậy `high`; một worker thử chạy lệnh shell ngoài phạm vi | validator của skill; hệ thống quyền chặn lệnh | Gửi lại đúng worker sửa một lần; kết quả vẫn qua validator |
| Script của skill đọc dữ liệu sai mã ký tự (hỏng chữ Nhật / Việt); main session tự kiểm SWP sai chỉ số ma trận; đọc sai tên field `sWP` | main session tự phát hiện khi kiểm | Chạy lại ở chế độ UTF-8; dùng hàm tính của skill; sửa script |
| Tổng giờ LAB-5 gấp 2,25 lần LAB-1; 45 issue vượt ngưỡng độ hạt | so sánh sau khi chấm | Đưa người dùng quyết; không chỉnh ngược hệ số cho khớp (`estimate.md` mục 4) |
| Bản nháp báo cáo tiến độ có 4 số / quan hệ sai (số câu hỏi đã gửi, chưa gửi, số việc bị chặn, một quan hệ "chặn" không có trong backlog) | main session kiểm lại bằng script trước khi đưa duyệt | Sửa trước khi người dùng đọc |
| Script sinh bảng tra sai nhóm LAB-1 từ E06 trở đi | main session đọc lại bảng | Sửa thành ánh xạ tường minh trước khi sinh |

## 3. Điểm đặc biệt trong cách dùng AI

**Chỗ tôi tin là hiệu quả**
- **Một nguồn dữ liệu, mọi thứ khác sinh ra từ đó.** Backlog nằm trong một file; issue trên GitHub, field trên Project và mọi bảng trong
  các file nộp đều do script sinh. Nhờ vậy sau khi tách 4 issue lớn ở bước chấm SWP, chỉ cần chạy lại script là số issue, tổng SWP
  và bảng so sánh tự khớp, không phải sửa tay ở 5 chỗ.
- **AI viết, máy kiểm, người quyết.** Trước mỗi cổng duyệt, script đã kiểm những thứ máy kiểm được (id, phụ thuộc, spec có thật, phủ đủ
  dòng LAB-1, số liệu báo cáo khớp nhật ký). Tôi chỉ phải đọc những chỗ cần phán đoán: bảng đổi giờ, issue mẫu, hướng xử lý khoảng lệch.
  Mỗi luật kiểm đều được thử bằng một lỗi cố ý trước khi tin.
- **Chia việc cho nhiều agent theo nhóm epic, có brief chung.** 3 agent chia backlog song song trong khoảng 10 phút. Brief cố định danh sách
  epic và định dạng, nên ghép lại được ngay; phần chồng lấn giữa các nhóm (trigger khóa ngày, phụ thuộc chéo) do main session đối chiếu.
- **AI nêu vấn đề thay vì tự quyết.** Mâu thuẫn "≤ 2 ngày = SWP ≤ 8", tổng giờ gấp 2,25 lần LAB-1, 45 issue vượt ngưỡng đều được đưa
  ra kèm phương án để tôi chọn, không bị chỉnh âm thầm cho đẹp số.

**Chỗ chưa tốt, cần cải thiện khi làm thật**
- **Hệ số giờ suy từ quá ít dữ liệu.** 7 giờ / SWP lấy từ 9 dòng LAB-1 cấp chức năng, lớn hơn nhiều so với issue; kết quả là tổng gấp
  2,25 lần LAB-1. Khi làm thật nên hiệu chỉnh trên giờ thực tế của vài sprint đầu thay vì giữ cố định.
- **Ngưỡng "issue to tối đa bao nhiêu" chốt trước khi biết thang điểm.** Quy tắc "≤ 5 SWP" đặt ở cổng 01, nhưng phải tới lúc chấm mới thấy 45 issue vượt và phải nới
  thành ≤ 6. Nên chấm thử 10–20 issue trước rồi mới chốt ngưỡng.
- **Nhiều lỗi nhỏ của chính AI chỉ lộ ra khi kiểm.** Sai mã ký tự khi chạy script của skill, đọc sai tên field, tra sai nhóm LAB-1, 4 số sai
  trong bản nháp báo cáo. Tất cả đều được bắt trước khi tới tay tôi, nhưng tốn thêm lượt và token; bước "kiểm bằng script" nên là mặc định
  ngay từ đầu chứ không phải thêm sau.
- **Worker chấm SWP không cô lập đúng như skill yêu cầu.** Để tiết kiệm token, worker được đọc file thay vì nhận dữ liệu trong prompt; một
  worker đã thử chạy lệnh ngoài phạm vi và bị chặn. Kết quả vẫn qua validator, nhưng khi làm thật nên dùng đúng worker không công cụ.
- **Spec LAB-4 thiếu cho màn hình ngoài lõi** khiến nhiều issue (tài khoản, phiên bản tỷ lệ, chuyển đổi dữ liệu) do AI tự đề xuất RPC / API,
  độ tin cậy thấp. Lẽ ra nên viết spec ngắn cho các màn hình này ở LAB-4.

**Chỗ chưa có ý tưởng**
- Cách giả lập sprint vẫn do AI soạn diễn biến; chưa có cách sinh diễn biến "giống thật" mà không tự đặt kịch bản.
- Chưa biết cách để khách trả lời 18 câu hỏi làm rõ nhanh hơn; trong sprint giả lập chỉ 3 / 5 câu có trả lời đầy đủ, và đây là rủi ro lớn
  nhất cho lịch.
