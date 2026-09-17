# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602148
- Ngày / CVAT local: 17/09/2026 / CVAT local (http://localhost:8080)
- Công cụ đã dùng: Brush, Polygon, CVAT local

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

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

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: `000000181542.jpg`, chiếc xe hơi (`car`) màu bạc ở làn đường chính phía trước, góc dưới bên phải ảnh.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Quy tắc chọn biên: Chỉ vẽ phần nhìn thấy rõ của thân xe và bánh xe theo phần nhìn thấy; dừng biên mask tại mép bánh xe tiếp giáp với mặt đường, không vẽ lan xuống phần bóng đổ (shadow).
- Nếu dùng gợi ý sau đó: Vùng gợi ý ban đầu bị tràn ăn theo bóng đổ của gầm xe xuống mặt đường nhựa; tôi dùng công cụ Brush/Eraser để gọt bỏ phần bóng đổ đó và kiểm tra lại đúng ranh giới của thân xe.
- Nếu không dùng gợi ý: Đã giải thích chi tiết như trên.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `hard_panoptic`, ảnh `000000460147.jpg`, khu vực mặt đường và vỉa hè người đi bộ phía trước.
- Lỗi thuộc loại: sai lớp (nhầm lẫn giữa `road` và `sidewalk`).
- Bằng chứng tôi nhìn thấy: Vùng vỉa hè lát gạch rộng cho người đi bộ ở trung tâm ảnh ban đầu bị gán nhầm nhãn `road`, còn lòng đường hẹp xe chạy lại bị gán thành `sidewalk`. Kiểm tra lại thấy có gờ bó vỉa hè và chức năng phân làn người đi bộ rõ ràng.
- Quy tắc và hành động sửa: Áp dụng quy tắc phân định theo chức năng/bó vỉa trong guideline-mini-sheet; đổi lại nhãn khu vực đi bộ thành `sidewalk` và lòng đường thành `road`, dùng Brush phóng to chỉnh lại ranh mép bó vỉa.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại file `hard_panoptic.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Sau khi sửa ranh và đổi đúng nhãn `sidewalk`, PQ của `sidewalk` tăng từ 0.000 lên 0.828, PQ tổng của task `hard_panoptic` tăng từ 0.434 lên 0.636 (29.0 / 30); điểm scorecard 3 tier đạt 79.1 / 82. Scorecard ba tier tối đa **82**, không phải điểm cuối trên 100. Không tự ghi PASS/top 3/bonus; người phụ trách xác nhận theo tiêu chí lớp. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `easy_semantic` (ảnh `7ee6d192-89e2408b.jpg`), dải đất/cỏ ven đường | Có phải là `sidewalk` hay `vegetation` / `road`? | Không có bó vỉa hay vỉa hè lát gạch; đường ngoại ô xe chạy tốc độ cao | Quyết định không vẽ `sidewalk`, gán vùng cỏ ven đường vào `vegetation` và mép nhựa vào `road`. |
| `cp5_occlusion` (ảnh `000000336232.jpg`), xe hơi bị cột/biển báo che ngang | Tách làm 2 object riêng lẻ hay giữ nguyên 1 instance? | Quy tắc occlusion: một vật thể bị vật khác che cắt ngang vẫn là một thực thể duy nhất | Quyết định nhóm cả 2 mảng nhìn thấy thành 1 instance ID `car` duy nhất, không tách làm 2 xe. |
| `cp4_curb` (ảnh `7d83710e-4697c3b2.jpg`), gờ đá bó vỉa tiếp giáp giữa đường và vỉa hè | Gờ đá thuộc về `road` hay thuộc về `sidewalk`? | Gờ đá bó vỉa được nâng cao so với mặt đường, có chức năng ngăn dòng xe và bảo vệ vỉa hè | Quyết định gán phần gờ đá bó vỉa vào `sidewalk` theo cao độ và chức năng. |
