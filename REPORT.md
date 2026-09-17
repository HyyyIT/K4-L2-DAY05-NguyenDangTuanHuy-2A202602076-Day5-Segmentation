# Báo cáo Day 5 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên VLearn. Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202602076
- Ngày / CVAT local: 17/09/2026 / CVAT Web
- Công cụ đã dùng: Brush, Polygon, AI Tool (gợi ý tự động)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh VLearn đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | chưa có | 0 / 1 | 3 |
| cp2_slice | chưa có | 0 / 1 | 3 |
| cp5_occlusion | chưa có | 0 / 1 | 3 |
| cp3_thin | chưa có | 0 / 1 | 3 |
| cp4_curb | chưa có | 0 / 1 | 3 |
| cp6_coverage | chưa có | 0 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh `000000181542.jpg`, xe hơi (`car`) màu trắng đỗ tiền cảnh bên phải.
- Class và quy tắc tôi dùng để chọn biên: Class `car`. Quy tắc biên: chỉ bao quanh phần vỏ/kính và lốp xe nhìn thấy được (visible pixels); điểm tiếp xúc bánh xe với mặt đường dừng sát lốp, không ăn vào bóng râm (shadow) dưới gầm xe.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: AI gợi ý thân xe khá chuẩn nhưng thường bị tràn vùng ra bóng đổ dưới mặt đường và viền gương chiếu hậu. Tôi dùng Polygon cắt gọt lại ranh giới gầm xe sát mép lốp thực tế.
- Nếu không dùng gợi ý: (Đã nêu ở trên)

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: `easy_semantic` / ảnh `81ae7cbb-6bc63a4a.jpg` / khu vực ranh giới giữa vỉa hè và mặt đường.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Biên (boundary) và nhầm nhãn giữa 2 vùng liền kề (`road` vs `sidewalk`).
- Bằng chứng tôi nhìn thấy: Mặt đường nhựa và viền vỉa hè có màu xám tương đồng nhau, nét vẽ ban đầu của `sidewalk` bị lấn sang phần lòng đường `road`.
- Quy tắc và hành động sửa: Thu nhỏ nét Brush (2-4px), phóng to ảnh để bám đúng theo gờ bó vỉa (curb line) nhô cao, trả lại phần diện tích lòng đường cho nhãn `road`.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại file `easy_semantic.zip`.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Task `easy_semantic` đạt mIoU 0.748 (lớp `road` đạt IoU 0.976, `building` 0.860, `sky` 0.939), điểm đạt 15.5 / 20. Scorecard ba tier đạt 26.4 / 82. Không đưa file ground truth vào fork.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1. `easy_semantic` (ảnh `817bca71`, góc vỉa hè) | `road` hay `sidewalk` ở đoạn hạ thấp cho xe ra vào | Cùng chất liệu mặt đường nhưng là lối kết nối vỉa hè | Quyết định: Phân định theo cốt cao độ gờ bó vỉa; xin coach xác nhận chuẩn quy ước với đoạn bằng phẳng không gờ. |
| 2. `medium_instance` (ảnh `000000373353`, người sau xe) | 1 instance `person` bị che cắt đôi hay tách thành 2 mask | Thân người bị đuôi xe che ngang, lộ phần trên và 2 chân | Quyết định: Coi là 1 object duy nhất (multi-polygon cùng ID) theo đúng quy tắc occlusion của instance segmentation. |
| 3. `hard_panoptic` (ảnh `000000350023`, cột đèn trên nền cây) | Tách riêng cột đèn (`traffic light`) hay gộp vào nền cây (`vegetation`) | Cột mảnh 2-3px trước tán cây rậm rạp | Quyết định: Dùng cọ mảnh tỉa riêng cột đèn trước, tránh để vùng nền cây (`stuff`) nuốt chửng chi tiết mảnh (`thin structure`). |

