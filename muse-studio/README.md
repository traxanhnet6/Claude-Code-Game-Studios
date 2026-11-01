# Muse Code Game Studio

Bản chuyển đổi của bộ khung **Claude Code Game Studios** (thư mục gốc của repo này) sang môi trường **Muse** của Meta. Mục tiêu không phải chép lại 49 agent và 74 skill, mà rút ra phần mạnh nhất và chạy thật bằng cơ chế Muse có: kỹ năng tìm bằng mô tả, đội con giao việc bằng brief tự chứa, cổng kiểm chứng trong quy trình, trình duyệt chơi thử thật, deploy tĩnh qua git và Render, đóng gói APK Android.

## Kiến trúc bản Muse

- `muse-game-studio/` là kỹ năng điều hành: hệ thống vai, vòng làm việc một lượt và năm cổng cứng. Thư mục `references/roles/` chứa 11 brief vai, mỗi brief dán thẳng vào nhiệm vụ của một đội con khi parent điều phối.
- Năm kỹ năng con đứng riêng để tìm kiếm kỹ năng của Muse tra được theo mô tả: cổng nghệ thuật, bằng chứng chơi thử, kiểm tra cân bằng, kiểm tra phạm vi, cổng phát hành.
- Parent giữ hai ghế điều phối của bản gốc (producer và technical-director) thay vì giao thành đội riêng, vì trên Muse parent chính là nơi giữ toàn cảnh, bộ nhớ và quyền deploy.
- Chế độ rigor mặc định là minimal, theo đúng bài học đo đạc của bản gốc: quy trình nặng giấy tờ không làm game hay hơn. Chỉ nâng rigor cho một hệ thống khi hệ thống đó có rủi ro thật như di trú save hoặc bản phát hành.

## Năm cổng cứng

1. **Bằng chứng hình ảnh**: việc đổi thứ người chơi nhìn thấy chỉ được đóng khi đã chạy game thật, nhìn tận mắt và giữ ảnh bằng chứng. Kiểm tra tự động xanh không thay thế.
2. **Cổng khắt khe hình ảnh**: hình chưa đạt chuẩn so với mẫu tham chiếu thì sửa nội bộ tới khi đạt. Không bao giờ gửi người dùng xem hình dưới chuẩn và không hỏi ý kiến về hình xấu.
3. **Cây yên và suite độc lập**: không kiểm chứng hay deploy từ cây đang có đội khác sửa dở. Chụp mã băm trước và sau lượt chạy, chạy lại toàn bộ suite bằng tiến trình riêng và đọc danh sách lỗi đầy đủ từ tệp nhật ký, không kết luận từ mã thoát của đường ống lệnh.
4. **Đối chiếu bản live**: sau deploy phải tải tệp trực tuyến về đối chiếu mã băm với bản nguồn, xác nhận trang thật sự nạp tệp mới, rồi chơi thử nghiệm thu trên chính bản live mới được gửi link.
5. **Kỷ luật token**: brief cho đội con phải tự chứa đủ dữ kiện, báo cáo chỉ khi có kết quả đóng được, không báo tiến trình rỗng.

## Bảng đối chiếu gốc sang chuyển đổi

| Bản gốc Claude Code | Bản Muse | Ghi chú |
| --- | --- | --- |
| 49 agent trong `.claude/agents/` | 11 brief vai trong `muse-game-studio/references/roles/` | Chỉ giữ vai có việc thật trong game web và Android của người dùng |
| Agent creative-director | Brief Giám đốc sáng tạo | Phán quyết mâu thuẫn sáng tạo, tự chọn khi lệnh đứng đã bao phủ |
| Agent art-director + skill art-bible + asset-audit | Brief Giám đốc nghệ thuật + kỹ năng `muse-game-studio-art-gate` | Thêm cổng khắt khe hình ảnh theo lệnh đứng của người dùng |
| Agent qa-lead + skill playtest-report + smoke-check + test-evidence-review | Brief Trưởng kiểm thử + kỹ năng `muse-game-studio-playtest-evidence` | Bằng chứng phải là ảnh chụp có ngày, mới hơn code nó chứng minh |
| Agent economy-designer + skill balance-check | Brief Thiết kế kinh tế + kỹ năng `muse-game-studio-balance-check` | Giá trị không có khoảng chuẩn thì ghi chưa phán, không tự đặt khoảng |
| Agent systems-designer | Brief Thiết kế hệ thống | Công thức kèm ba ví dụ số tính tay |
| Agent gameplay-programmer | Brief Lập trình gameplay | Cấm tự đổi số cân bằng khi cài |
| Agent ui-programmer + ux-designer + accessibility-specialist | Brief Lập trình giao diện | Gộp ba vai, thêm luật vùng an toàn tránh khung giao diện nổi |
| Agent world-builder + level-designer | Brief Xây dựng thế giới và bản đồ | Tranh và logic là hai mặt của một bản đồ, kiểm bằng tìm đường trên lưới |
| Agent writer + narrative-director | Brief Biên kịch | Gộp điều phối truyện vào biên kịch, tên riêng mới luôn là đề xuất |
| Agent android-specialist + skill build-android (track riêng của fork này) | Brief Chuyên gia Android | Giữ nguyên năm điều không thương lượng: ký số kiểm chứng, quyền tối thiểu, dung lượng thật, bằng chứng trên máy, versionCode chỉ tăng |
| Agent release-manager + skill release-checklist + gate-check | Brief Quản lý phát hành + kỹ năng `muse-game-studio-release-gate` | Cổng phát hành gộp cả web tĩnh và APK |
| Agent producer + skill scope-check | Parent tự giữ ghế điều phối + kỹ năng `muse-game-studio-scope-check` | Verdict NOT ASSESSED khi baseline rỗng hoặc không đọc được hiện trạng |
| 18 hook trong `.claude/hooks/` | Năm cổng cứng trong quy trình + cron của Muse khi thật cần lặp lịch | Muse không có hook chặn commit, bản chuyển đổi không hứa hẹn điều đó |
| Lệnh gạch chéo và skill user-invocable | Kỹ năng Muse tìm bằng `muse.skill_search` theo mô tả | Không có cú pháp lệnh gạch chéo trên Muse |
| AskUserQuestion và chế độ collaborative hỏi trước khi ghi | Lệnh đứng đã chốt thì tự làm, chỉ hỏi khi thiếu quyết định thật | Người dùng của studio này ghét bị hỏi và ghét báo cáo rỗng |
| project.yaml và modes.rigor | Lệnh đứng trong bộ nhớ người dùng + rigor minimal mặc định | Không tạo thêm một tệp cấu hình thứ hai để đội phải đồng bộ |
| Agent chuyên Godot, Unity, Unreal (17 tệp) và các vai engine, network, analytics, community, live-ops, devops, security, tools, prototyper, audio, localization, technical-artist, qa-tester | Bỏ, hoặc gộp phần dùng được vào brief gần nhất | Game đích là web HTML5/JavaScript và APK Android, các vai engine không có việc thật; phần âm thanh và kiểm thử tay đã gộp vào brief giám đốc nghệ thuật và trưởng kiểm thử |

## Cách dùng trên Muse

1. Nạp kỹ năng `muse_game_studio` khi bắt đầu một đợt làm game.
2. Chọn vai theo bảng trên, đọc brief tương ứng trong `references/roles/` và dán vào nhiệm vụ đội con cùng dữ kiện cụ thể của việc.
3. Chạy vòng một lượt: nhận lệnh thành một kết quả đóng được, giao đội song song theo tệp không chồng nhau, parent tự kiểm chứng, qua đủ năm cổng mới deploy và nghiệm thu live.
4. Khi việc thuộc một mảng chuyên sâu, tra thêm kỹ năng con tương ứng bằng tìm kiếm kỹ năng.

## Điểm yếu còn lại

- Brief vai là văn bản điều phối, không phải cơ chế ép buộc: parent vẫn phải tự kiểm chứng đầu ra của đội con như cổng ba đã ghi, vì không có hook nào chặn thay.
- Năm kỹ năng con dùng chung thư mục bằng chứng và tài liệu chuẩn của từng dự án game, nên khi áp sang dự án mới phải trỏ lại đúng tài liệu kinh tế, art bible và kinh thánh cốt truyện của dự án đó ở lượt đầu tiên.
