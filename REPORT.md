# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Họ và tên: NGUYỄN ĐỨC TÙNG
- Mã học viên theo lớp: 2A202602227
- Ngày / CVAT local: 17/09/2026 / http://localhost:8080
- Công cụ đã dùng: Thủ công, 100% tự tay vẽ (Brush, Polygon)

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; "quy tắc biên" là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh 000000373353.jpg, một người trong nhóm nhiều người túm tụm qua đường
- Class và quy tắc tôi dùng để chọn biên: class `person`. Vì nhiều người đứng sát/chồng lên nhau nên rất khó nhận biết số lượng người chỉ nhìn tổng thể; tôi dùng mắt để nhận diện rõ từng bộ phận cơ thể (đầu, vai, tay, chân...) của mỗi người nhằm phân biệt ranh giới giữa người này với người khác trước khi vẽ mask riêng cho từng người.
- Nếu dùng gợi ý sau đó: không dùng.
- Nếu không dùng gợi ý: không dùng; toàn bộ object trong task Medium được vẽ thủ công theo cách trên.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi "đã sửa" khi chưa sửa.

- Task/ảnh/vùng: easy_semantic, vùng sidewalk (toàn bộ 3 ảnh)
- Lỗi thuộc loại: biên (ranh road–sidewalk vẽ theo màu bề mặt thay vì chức năng/bó vỉa)
- Bằng chứng tôi nhìn thấy: chạy `scoring/score.py`, per-class IoU của `sidewalk` chỉ đạt 0.339 trong khi `road` đạt 0.977 — chênh lệch lớn cho thấy ranh hai class này bị lệch hệ thống, không phải lỗi ngẫu nhiên.
- Quy tắc và hành động sửa: theo guideline, ranh road–sidewalk phải xác định theo bó vỉa/chức năng chứ không theo màu. Do giới hạn thời gian buổi lab, tôi **chưa quay lại sửa** phần này trong CVAT — ghi nhận đây là lỗi đã xác định rõ nguyên nhân nhưng chưa xử lý.
- Sau sửa đã Save và export lại chưa? Chưa — file `easy_semantic.zip` đã nộp là bản gốc, IoU sidewalk 0.339 vẫn còn nguyên.

Kết quả tự chấm (scoring/score.py, so với ground truth thầy gửi cho 3 tier — chưa có điểm cho 6 checkpoint vì chưa nhận ground truth checkpoint):
- easy_semantic: mIoU 0.760, 16.0/20
- medium_instance: mean matched IoU×recall 0.677, 19.7/32 (đếm thừa 19 object so với GT, FP 28, FN 9)
- hard_panoptic: PQ 0.448, 16.6/30 (đáng chú ý: class `car` có 36 false positive)

Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | cp1_holes: mask xe có nên khoét lỗ ở vùng cửa sổ/kính hay không | Cửa sổ trong suốt trông như "thấy nền phía sau" nên dễ nhầm là phải cắt rời khỏi mask | Quyết định: không khoét — kính/khe vẫn tính là một phần của mask vật theo quy tắc bài, trừ khi task nói khác |
| 2 | Phân biệt cp2_slice và cp5_occlusion: khi nào tách 2 ID, khi nào giữ 1 ID | Ban đầu tôi nhầm lẫn hai quy tắc này với nhau | Quyết định: cp2_slice (2 vật thật sát nhau) → luôn 2 ID riêng dù nhìn dính liền; cp5_occlusion (1 vật bị che) → vẫn 1 ID dù phần nhìn thấy bị chia rời |
| 3 | hard_panoptic, các mask class `car`: có khả năng một số xe bị tách thành nhiều mask nhỏ thay vì gộp về 1 object | Scorer báo 36 false positive ở class `car` — số lượng lớn bất thường so với 25 true positive | Câu hỏi cho coach: tôi nghi ngờ đã tách nhầm một số xe thành nhiều mask nhưng chưa kịp xác minh lại từng ảnh trước hạn nộp — có thể xem chi tiết giúp tôi không? |
