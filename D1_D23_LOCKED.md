# D1-D23 LOCKED DESIGN CONTRACT

## Purpose
This file is the canonical recovery record for the D1-D23 design decisions explicitly supplied/recovered by the user. The original D1-D23 source remains the highest-priority authority. Recovered decisions below must not be re-asked or silently changed.

## Preservation / conflict rule
- Do NOT invent missing D1-D23 details.
- Do NOT silently reinterpret or replace an existing locked decision.
- If an older recovered answer conflicts with a later explicitly locked project decision, the later locked decision wins and the conflict must be recorded rather than hidden.
- If the original D1-D23 source is supplied later, preserve its exact terminology and semantics as the canonical source.

## D1-D5 — Combat Core

### D1 — Hero ngoài tầm đánh
- Hero tự động di chuyển tiến lại gần đối thủ khi ngoài tầm đánh.
- Hero dừng lại ở khoảng cách tấn công.
- Baseline Attack Range = 1.8.
- Hero không chạy xuyên qua mục tiêu.

### D2 — Companion hồi sinh
- Companion hồi sinh sau 25 giây.
- 25 giây là thông số configurable/data-driven, có thể chỉnh sửa.

### D3 — Targeting
- Ưu tiên mục tiêu gần nhất (Nearest Target).
- Nếu khoảng cách bằng nhau, ưu tiên Hero trước Companion: Hero > Companion.

### D4 — Hero chết / Defeat
- Hero chính chết thì trận đấu kết thúc ngay lập tức: Defeat.
- Toàn bộ Companion/Tùy tùng lập tức ngừng tấn công và biến mất.
- Không cho Companion tiếp tục đánh sau khi Hero chết.

### D5 — Interrupt / Priority khi thi triển kỹ năng
- Khi đủ Rage theo quyết định này: Rage = 80/100, Tuyệt kỹ có thể ngắt đòn đánh thường để tung ngay.
- Các chiêu thông thường khi hết Cooldown tự động thi triển theo độ ưu tiên, chiêu cao cấp trước.
- Khi tắt Auto, người chơi có thể tự bấm tay.
- Chi tiết cast/channel/interrupt nâng cao chỉ được bổ sung khi có quyết định tương ứng; không tự suy diễn thêm.

## D6-D19
- Chưa có nguyên văn trong nguồn được cung cấp ở lần khôi phục này.
- KHÔNG được AI tự tái tạo hoặc suy đoán.
- Khi người dùng cung cấp lại nguồn D6-D19, phải bổ sung đúng nguồn.

## D20 — Tiến trình Ải, Quái thường & Treo máy

### D20-1 — Giới hạn ải / mốc cấp độ
- Chưa giới hạn cứng.
- Thiết kế theo cấu hình dữ liệu (configurable).

### D20-2 — Phạm vi nhận tài nguyên / EXP
- Áp dụng cho Quái thường.
- Áp dụng cho chế độ Treo máy Idle/Offline.

### D20-3 — Điều kiện vượt ải / mốc theo Level
- Có điều kiện tiến trình theo Level của nhân vật.

### D20-4 — Hard-cap ải cố định
- Không áp dụng giới hạn ải cứng (Hard-cap) cố định.

### D20-5 — Cân bằng chỉ số quái & tiến trình
- Đưa toàn bộ vào Data Config để cân bằng sau.
- Khi đạt mốc Level nhất định, bắt buộc phải thỏa mãn điều kiện mới được sang mốc tiếp theo.

## D21 — EXP, Level & Đột phá Danh hiệu

### D21-1 — Công thức EXP theo Level
- EXP tăng dần.
- Lv1 -> Lv2 cần 100 EXP.
- Lv2 -> Lv3 cần 150 EXP.
- Tăng 50 EXP/level trong giai đoạn Lv1-Lv50.
- Giai đoạn Lv51-Lv100: bước tăng 100 EXP/level.
- Giai đoạn Lv101-Lv150: bước tăng 200 EXP/level.
- Không tự suy diễn công thức ngoài các mốc đã nêu.

### D21-2 — EXP từ quái thường
- Giết 1 quái thường nhận 10 EXP cố định.

### D21-3 — Level có tăng trực tiếp HP/ATK/DEF không?
- Không.

### D21-4 — Vai trò của Level
- Game không tăng chỉ số dựa trực tiếp vào Level.
- Level chủ yếu dùng làm điều kiện để Đột phá Danh hiệu.
- Chỉ số nhân vật tăng dựa vào bậc Danh hiệu.

### D21-5 — Chỉ số khi Đột phá Danh hiệu
- Tăng bậc Danh hiệu lập tức nâng cấp chỉ số gốc của Hero.
- Không áp dụng cơ chế cộng dồn chồng chéo (non-stacking).

### D21-6 — EXP vượt ngưỡng
- Nguồn lịch sử được cung cấp ở đây ghi: reset lượng EXP vượt ngưỡng về 0.
- Tuy nhiên, quyết định này đã được supersede bởi locked Level Gate decision về sau: khi Hero chạm giới hạn Level của Danh hiệu mà chưa Đột phá, EXP nhận thêm KHÔNG bị mất mà phải được lưu/cộng dồn; khi đủ điều kiện và thực hiện Đột phá, hệ thống tiếp tục xử lý EXP đã tích lũy theo rule Level Gate hiện hành.
- Vì vậy, "reset EXP vượt ngưỡng về 0" KHÔNG còn là rule hiện hành.

### D21-7 — Tài nguyên Đột phá Danh hiệu
- Không tốn tài nguyên Vàng/Bạc.
- Điều kiện thay cho tiêu hao Vàng là kiểm tra Cấp rơi trang bị (Chest/Drop Level).

### D21-8 — Đủ toàn bộ điều kiện
- Bắt buộc đạt đủ toàn bộ điều kiện.
- Quan hệ điều kiện là AND.

### D21-9 — Mở rộng Danh hiệu
- Hệ thống phải linh hoạt nhiều Rank/Tier.
- Hiện tại cho phép cấu hình thủ công bằng Data-driven ScriptableObject để dễ mở rộng và kiểm soát.

### D21-10 — UI Đột phá Danh hiệu
- Thiết kế theo đúng 4 ảnh giao diện mẫu tham chiếu đã chốt.
- Khi mở bảng Đột phá Danh hiệu, Hero và Quái vẫn tiếp tục chiến đấu bình thường.
- Không dừng trận như bảng so sánh trang bị.

## D22
- Chưa có nguyên văn trong nguồn được cung cấp ở lần khôi phục này.
- KHÔNG được AI tự tái tạo hoặc suy đoán.
- Khi người dùng cung cấp lại nguồn D22, phải bổ sung đúng nguồn.

## D23 — Trang bị, Rương & Drop

### D23-1 — Nguồn trang bị & Cấp Rương
- Khoảng 95% trang bị đến từ Rương.
- 5% đến từ phần thưởng ải/sự kiện.
- Cấp Rương thống nhất với Cấp rơi đồ (Drop Level).
- Nâng cấp Rương tiêu tốn Vàng và điều kiện được cấu hình data-driven.

### D23-2 — Thu hồi trang bị / Auto-Recycle
- Trang bị mở ra có Lực chiến (CP) thấp hơn trang bị đang mặc sẽ tự động bị thu hồi.
- Khi thu hồi, hoàn trả một lượng Vàng tương ứng.

## C1-C12 — Các quyết định chiến đấu được khôi phục trong nguồn hiện tại

### C6 — Rage
- Rage từ 0 đến 100.
- Đánh thường trúng đích tăng +1 Rage.
- Nhận sát thương tăng +1 Rage.
- Tuyệt kỹ tiêu hao 80 Rage hoặc 100 Rage tùy config.
- Không tự chọn một giá trị cố định khác ngoài các giá trị đã được nguồn cho phép.

### C7-C9 — Companion
- Companion có thanh HP.
- Companion có thể bị đánh chết.
- Companion hồi sinh sau 25 giây.
- Khi Hero chết, toàn bộ Companion lập tức ngừng hoạt động/biến mất.

### C3 — Hiển thị chữ số chiến đấu
- Sát thương thường, Crit và Miss có màu hiển thị riêng biệt.
- Chữ số Lifesteal hiển thị phía bên Hero.
- Các chữ số sát thương khác hiển thị phía kẻ địch.

## Important reconciliation — Companion HP
- Nguồn D2/C7-C9 vừa được người dùng khôi phục xác nhận Companion CÓ HP và có thể chết.
- Điều này supersede câu mô tả cũ trong một số memory record rằng Pets/satellites "không có HP".
- Từ thời điểm này, không được dùng rule "Companion không có HP" để thiết kế/đánh giá hệ thống nếu không có nguồn mới hơn từ người dùng.

## Current recovered status
- D1-D5: RECOVERED / LOCKED.
- D6-D19: MISSING ORIGINAL SOURCE — DO NOT INVENT.
- D20: RECOVERED / LOCKED.
- D21: RECOVERED / LOCKED, with D21-6 historical answer explicitly superseded by later Level Gate rule.
- D22: MISSING ORIGINAL SOURCE — DO NOT INVENT.
- D23: RECOVERED / LOCKED.
- C3, C6-C9: RECOVERED / LOCKED as supporting combat decisions.

## Conflict policy
If code, Antigravity, a future milestone, or another memory record conflicts with this contract, stop and report the conflict. Preserve the latest explicitly locked user decision. Do not silently change the design contract.
