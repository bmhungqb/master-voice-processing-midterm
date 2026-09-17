# ĐỒ ÁN GIỮA KỲ: XỬ LÝ TIẾNG NÓI (K35)
**Đề tài:** Xây dựng sách điện tử DAISY (DAISY 3 / Digital Talking Book) hỗ trợ người khiếm thị

---

## PHẦN 1: NỘI DUNG ĐỒ ÁN VÀ FORMAT NỘP YÊU CẦU

### 1. Giới thiệu & Mục tiêu
* **Mục tiêu:** Xây dựng sách nói điện tử đa phương tiện theo tiêu chuẩn **DAISY 3** (NISO Z39.86), cho phép người khiếm thị điều hướng linh hoạt (nhảy theo chương, mục, đoạn, câu) và đồng bộ chữ chạy với giọng đọc tương ứng.
* **Kỹ thuật cốt lõi trong môn học:**
  * **Text-to-Speech (TTS) & SSML:** Tổng hợp giọng đọc tự nhiên từ văn bản; dùng cú pháp SSML để tinh chỉnh ngắt nghỉ, cao độ (pitch), tốc độ (rate) và cảm xúc đọc.
  * **Speech-to-Text (STT) & Audio Segmentation (Forced Alignment):** Đối với nguồn đã có sẵn âm thanh, tiến hành nhận dạng và cắt ghép, căn chỉnh mốc thời gian âm thanh khớp với từng câu chữ.
  * **OCR:** Trích xuất văn bản từ tài liệu PDF/ảnh (sách giáo khoa, truyện thiếu nhi...).

### 2. Cấu trúc một bộ sách chuẩn DAISY 3
Mỗi cuốn sách chuẩn DAISY 3 bắt buộc gồm 5 loại tệp liên kết chặt chẽ với nhau:
* `*.xml` (DTBook): Chứa toàn bộ nội dung văn bản, cấu trúc phân cấp (tiêu đề, chương, đoạn, câu) và gán mã định danh duy nhất (`id`) cho từng thành phần.
* `*.smil`: File đồng bộ đa phương tiện, liên kết từng `id` trong file XML với mốc thời gian phát (`clipBegin`, `clipEnd`) trong file âm thanh `.mp3`.
* `*.opf`: File gói trung tâm (Package/Manifest) khai báo toàn bộ tài nguyên của sách và chứa khối thông tin siêu dữ liệu (`<metadata>`).
* `*.ncx`: File điều hướng phân cấp (mục lục), cho phép trình đọc nhảy nhanh đến chương/mục.
* `*.mp3`: Các file âm thanh giọng đọc. *Lưu ý: Phân chia thành các đoạn audio ngắn theo câu/đoạn/chương thay vì 1 file lớn duy nhất để tránh trễ và tiện bảo trì.*

### 3. Quy định chọn sách & Thông tin Metadata
* **Tiêu chí chọn sách:**
  * Sách phải có mã **ISBN** hợp lệ (căn cứ theo ISBN để đảm bảo không trùng lặp giữa các nhóm).
  * Điền đăng ký vào biểu mẫu (Google Sheets/Form) của lớp.
  * Ưu tiên sách **Tiếng Việt** (`language: "vi"`).
  * Ưu tiên **Sách giáo khoa** và các thể loại ưu tiên: *Giáo dục & Sư phạm*, *Trẻ em & Thiếu nhi*, *Lịch sử*, *Văn học & Tiểu thuyết*.
  * Ưu tiên bản tái bản mới nhất (nếu có nhiều lần xuất bản).
  * Yêu cầu thực hiện **trọn vẹn từng cuốn sách** (với sách quá đồ sộ như *Đại Việt Sử Ký Toàn Thư*, *Thủy Hử*, có thể chia thành từng chương/hồi nhưng vẫn giữ chung mã ISBN).
* **Metadata bắt buộc (trong thẻ `<metadata><dc-metadata>`):**
  * `dc:Title`: Tên sách
  * `dc:Creator`: Tác giả
  * `dc:Subject`: Tên thể loại sách (trong 16 thể loại quy định)
  * `dc:Description`: Tóm tắt sơ lược nội dung
  * `dc:Publisher`: Nhà xuất bản / Nhà phát hành
  * `dc:Date`: Năm/ngày phát hành (`yyyy`, `yyyy-mm` hoặc `yyyy-mm-dd`)
  * `dc:Source`: Mã ISBN
  * `dc:Language`: `vi`
  * *Trường mở rộng:* `collector` (người thu thập), `sourceURL` (link nguồn), `note` (ghi chú thêm).

### 4. Format và Cấu trúc thư mục nộp bài
Thư mục nộp được đóng gói và đặt tên theo **Mã số học viên (MSHV)** của các thành viên trong nhóm:

```text
GIỮA KỲ MSHV1_MSHV2_MSHV3_MSHV4/
├── Báo cáo đồ án (.docx hoặc .pdf)
├── Resource/ (Source code, Jupyter Notebook, Script xử lý pipeline)
└── Các thư mục sách (theo từng cuốn hoặc theo từng Chương/Hồi đối với sách lớn):
    ├── Tên_sách_1-Chương 1/
    │   ├── Tên_sách.zip             <-- File nén chứa toàn bộ các file .xml, .smil, .mp3, .opf, .ncx
    │   └── Tên_sách_sha256sums.txt  <-- File text chứa chuỗi mã băm SHA-256 của file zip trên
    ├── Tên_sách_1-Chương 2/
    │   ├── Tên_sách.zip
    │   └── Tên_sách_sha256sums.txt
    └── ...
```

* **Công cụ kiểm thử trước khi nộp:**
  * Kiểm tra hiển thị và đồng bộ audio-text trên **Thorium Reader** (Win/Mac/Linux) hoặc **Dolphin EasyReader**.
  * Chuyển đổi/kiểm tra chuẩn qua **DAISY Pipeline 2**.

---

## PHẦN 2: PHÂN CÔNG NHIỆM VỤ (4 THÀNH VIÊN)

### Thành viên 1: Xử lý Văn bản & Cấu trúc Dữ liệu (Text & XML Lead)
* **Tìm kiếm & Đăng ký sách:** Tìm sách có mã ISBN hợp lệ, thuộc nhóm thể loại ưu tiên (sách giáo khoa, thiếu nhi, lịch sử...), điền form đăng ký của lớp để tránh trùng lặp.
* **Số hóa & Làm sạch văn bản:** Thực hiện OCR từ tài liệu PDF/ảnh hoặc trích xuất text; xử lý chính tả, chuẩn hóa dấu câu, số liệu và ký tự đặc biệt.
* **Tạo file DTBook (`.xml`):** Xây dựng cấu trúc phân cấp (tiêu đề H1/H2, mục lục, đoạn văn, câu) tuân thủ tiêu chuẩn DTBook trong DAISY 3.
* **Đánh mã định danh (`id`):** Tự động gán mã `id` duy nhất cho từng câu/đoạn trong file XML để làm mốc neo đồng bộ với âm thanh.
* **Thiết lập Metadata:** Khai báo đầy đủ các trường thông tin bắt buộc và trường mở rộng vào thẻ `<metadata>` theo quy định.

### Thành viên 2: Xử lý Giọng nói & Âm thanh (TTS / STT & Audio Lead)
* **Lựa chọn mô hình giọng đọc:** Chọn và kết nối API công cụ TTS tiếng Việt (Google Cloud TTS, Azure Neural TTS, Edge-TTS, FPT.AI...) hoặc STT (Whisper, Wav2Vec2) nếu dữ liệu gốc là audio.
* **Cải thiện chất lượng bằng SSML:** Ứng dụng cú pháp SSML để chèn điểm ngắt nghỉ tự nhiên, điều chỉnh cao độ (pitch), tốc độ nói (rate) và sắc thái cảm xúc phù hợp với văn phong sách.
* **Sinh & Phân đoạn âm thanh:** Cắt/xuất âm thanh thành từng file nhỏ định dạng `.mp3` theo từng câu hoặc đoạn (không để một file audio quá dài để đảm bảo hiệu năng seek khi đọc).
* **Kiểm duyệt chất lượng audio:** Rà soát âm thanh đảm bảo không bị méo tiếng, nuốt chữ, lỗi phát âm dấu thanh tiếng Việt.

### Thành viên 3: Tự động hóa & Đồng bộ Đa phương tiện (Alignment & DAISY Pipeline)
* **Đồng bộ thời gian (Forced Alignment):** Xác định chính xác mốc thời gian bắt đầu (`clipBegin`) và kết thúc (`clipEnd`) của từng câu/đoạn văn ứng với từng file âm thanh `.mp3`.
* **Sinh file đồng bộ (`.smil`):** Viết script (Python/Notebook) tự động liên kết mã định danh `id` của file `.xml` với đoạn phát tương ứng trong file `.mp3`.
* **Sinh file điều hướng (`.ncx`):** Lập trình tự động tạo mục lục điều hướng đa cấp, giúp người đọc chuyển nhanh giữa các chương/mục.
* **Sinh file gói (`.opf`):** Viết mã tự động khai báo toàn bộ manifest tài nguyên (`.xml`, `.smil`, `.ncx`, `.mp3`) và gắn metadata vào file `.opf`.
* **Tự động hóa pipeline:** Xây dựng luồng thực thi tổng thể để tự động chuyển đổi từ text/audio thô ra toàn bộ các tệp DAISY 3.

### Thành viên 4: Kiểm thử, Đóng gói & Báo cáo (QA, Packaging & Report Lead)
* **Kiểm thử trên trình đọc chuyên dụng:** Nạp sách vào **Thorium Reader** và **Dolphin EasyReader** để kiểm thử thực tế (chữ highlight đúng theo giọng đọc, điều hướng chương mục mượt mà).
* **Đóng gói dữ liệu chuẩn:** Nén toàn bộ các tệp DAISY thành file `Tên_sách.zip` đúng cấu trúc kỹ thuật.
* **Tạo mã băm SHA-256:** Thực hiện lệnh băm file zip để tạo tệp `Tên_sách_sha256sums.txt` phục vụ kiểm tra tính toàn vẹn dữ liệu.
* **Tổ chức thư mục nộp bài:** Sắp xếp toàn bộ cây thư mục theo quy định: `GIỮA KỲ MSHV1_MSHV2_MSHV3_MSHV4/`.
* **Soạn thảo Báo cáo đồ án:** Viết tài liệu báo cáo tổng kết (giới thiệu sách, kiến trúc pipeline, phân tích ưu/nhược điểm công cụ, thống kê số liệu và hướng dẫn chạy mã nguồn).
