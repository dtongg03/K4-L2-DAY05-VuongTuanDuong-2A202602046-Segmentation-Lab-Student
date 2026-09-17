# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602046 — Vương Tuấn Dương
- Ngày / CVAT local: 17/09/2026 / CVAT local
- Công cụ đã dùng: CVAT local và mô hình SAM 2.1 Tiny chạy trên GPU

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | `easy_semantic.zip` | 3 / 3 | 20 |
| medium_instance | `medium_instance.zip` | 3 / 3 | 32 |
| hard_panoptic | `hard_panoptic.zip` | 2 / 2 | 30 |
| cp1_holes | `cp1_holes.zip` | 1 / 1 | 3 |
| cp2_slice | `cp2_slice.zip` | 1 / 1 | 3 |
| cp5_occlusion | `cp5_occlusion.zip` | 1 / 1 | 3 |
| cp3_thin | `cp3_thin.zip` | 1 / 1 | 3 |
| cp4_curb | `cp4_curb.zip` | 1 / 1 | 3 |
| cp6_coverage | `cp6_coverage.zip` | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: ảnh `000000181542.jpg`, người phụ nữ mặc áo dài sáng màu ở gần giữa ảnh.
- Class và quy tắc tôi dùng để chọn biên: class `person`; tôi bám theo phần cơ thể và quần áo nhìn thấy, dừng mask tại mép người, không lấy bóng đổ, mặt đường hoặc các xe máy đi ngang vào cùng mask.
- Nếu dùng gợi ý sau đó: tôi dùng SAM 2.1 Tiny để tạo gợi ý cho các vật còn lại. Với vùng có nhiều xe và người chồng lấn, gợi ý đôi lúc ăn sang vật bên cạnh hoặc nền đường; tôi xem lại từng object, tách riêng các vật và chỉnh biên trước khi Save.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `medium_instance` / ảnh `000000181542.jpg` / nhóm xe máy đi ngang phía trước người phụ nữ.
- Lỗi thuộc loại: biên và gộp-tách.
- Bằng chứng tôi nhìn thấy: một gợi ý mask bám sang phần xe máy nằm cạnh và lấy thêm một mảng mặt đường; hai xe gần nhau cũng dễ bị nhìn thành cùng một object.
- Quy tắc và hành động sửa: mỗi phương tiện là một instance riêng; tôi xóa phần mask tràn sang xe bên cạnh và mặt đường, sau đó tách các phương tiện thành các object độc lập theo phần nhìn thấy.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại ZIP của task.

Tôi dùng chức năng tự kiểm để kiểm tra cấu trúc file export; phần nhận xét trong báo cáo dựa trên việc xem lại ảnh và object trong CVAT. Tôi không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| `000000181542.jpg`, các xe máy cắt ngang phía trước người phụ nữ | Gộp phần xe che khuất với người, hoặc giữ người và từng xe là các instance riêng | Người và xe là các vật thể khác class; chỉ gán phần nhìn thấy và không suy đoán xuyên qua vật che | Giữ người là một instance `person`; mỗi xe máy là một instance `motorcycle` riêng. |
| `000000458325.jpg`, hai dãy ô tô đỗ dọc hai bên đường | Gộp các xe liền nhau thành một vùng, hoặc tách từng xe dù bị che một phần | Xe cùng class nhưng vẫn là các vật thể đếm được riêng; đường viền kính, đèn và khoảng hở giúp phân biệt | Tách từng xe thành một instance `car`, chỉ vẽ phần nhìn thấy của xe bị che. |
| `000000460147.jpg`, xe chuyên chở ô tô ở gần giữa ảnh | Coi toàn bộ cụm là một phương tiện, hoặc tách xe chở và các ô tô được chở | Xe chở có thân và bánh riêng; các ô tô trên giá vẫn có hình dáng và ranh giới riêng | Gán xe chở theo class phù hợp của phương tiện lớn và giữ các ô tô nhìn thấy thành các instance `car` riêng. |
