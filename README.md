# ĐỒ ÁN GIỮA KỲ: XỬ LÝ TIẾNG NÓI (K35)
## Xây dựng Sách Điện Tử DAISY 3 (Digital Talking Book) Hỗ Trợ Người Khiếm Thị

---

## 1. Giới Thiệu Dự Án (Project Overview)
Dự án tập trung xây dựng một bộ sách nói kỹ thuật số đa phương tiện hoàn chỉnh theo chuẩn **DAISY 3 (ANSI/NISO Z39.86-2005)** dành cho người khiếm thị và khuyết tật đọc. 

Đặc điểm cốt lõi của sách chuẩn DAISY 3:
* **Đồng bộ âm thanh & chữ chạy:** Đồng bộ văn bản hiển thị với giọng đọc audio ở cấp độ câu/cụm từ thông qua SMIL.
* **Điều hướng linh hoạt:** Cho phép người đọc khiếm thị chuyển nhanh giữa các chương, mục, đoạn và câu qua tệp NCX.
* **Tương thích cao:** Kiểm thử và phát trực tiếp trên các trình đọc chuyên dụng hàng đầu như **Thorium Reader** và **Dolphin EasyReader**.

### Thông Tin Tác Phẩm Lựa Chọn
* **Tác phẩm:** *Trong Gia Đình* (*En famille*)
* **Tác giả:** Hector Malot
* **Dịch giả & Hiệu đính:** GS. Huỳnh Lý & Mai Hương; hiệu đính: Huỳnh Phan Thanh Yên
* **Nhà xuất bản:** NXB Văn Học (liên kết Công ty Cổ phần Văn hóa Đông A)
* **Mã ISBN (`dc:Identifier` / `dc:Source`):** `978-604-69-8175-6`
* **Năm xuất bản (`dc:Date`):** 2017
* **Ngôn ngữ (`dc:Language`):** `vi-VN`
* **Thể loại (`dc:Subject`):** Văn học & Tiểu thuyết (nằm trong 16 nhóm thể loại chuẩn)
* **Tóm tắt nội dung:** Tác phẩm kinh điển về cuộc đời cô bé Perrine (Perin) 12 tuổi mồ côi cha mẹ, một mình giữa xứ người với bao khó khăn, gian khổ, nhưng bằng nghị lực, ý chí tự lập và lòng nhân ái phi thường đã vượt lên số phận để được ông nội đón nhận trở lại trong gia đình.

---

## 2. Phân Công Nhiệm Vụ & Trạng Thái Thực Hiện (Tasks & Status)

Dự án được phân chia theo 4 vai trò thành viên cốt lõi:

| STT | Vai Trò & Nhiệm Vụ | Nội Dung Trọng Tâm | Trạng Thái |
|:---:|---|---|:---:|
| **1** | **Thành viên 1: Xử lý Văn bản & Cấu trúc Dữ liệu** *(Text & XML Lead)* | • Tìm kiếm & đăng ký sách chuẩn ISBN.<br>• Làm sạch dữ liệu văn bản từ EPUB, chuẩn hóa chính tả và quy tắc tách câu tiếng Việt.<br>• Xây dựng cấu trúc DTBook XML 2005-3 phân cấp (`<frontmatter>`, `<bodymatter>`, `<level1>`, `<h1>`, `<p>`, `<sent>`).<br>• Đánh mã định danh duy nhất (`id`, `smilref`) cho từng câu/đoạn văn.<br>• Thiết lập siêu dữ liệu chuẩn (`<head>`, `<metadata>`). | **HOÀN THÀNH**<br>`(COMPLETED)` |
| **2** | **Thành viên 2: Xử lý Giọng nói & Âm thanh** *(TTS / STT & Audio Lead)* | • Lựa chọn mô hình giọng đọc TTS tiếng Việt (Edge-TTS, Azure Neural TTS, Google TTS).<br>• Áp dụng cú pháp SSML để tinh chỉnh ngắt nghỉ tự nhiên, cao độ (pitch), tốc độ (rate).<br>• Sinh âm thanh định dạng `.mp3` chất lượng cao theo từng phân đoạn câu/chương.<br>• Rà soát và kiểm duyệt chất lượng âm thanh. | **TIẾP THEO**<br>`(PENDING)` |
| **3** | **Thành viên 3: Tự động hóa & Đồng bộ Đa phương tiện** *(Alignment & DAISY Pipeline)* | • Xác định mốc thời gian phát (`clipBegin`, `clipEnd`) cho từng câu văn bản.<br>• Tự động sinh tệp đồng bộ đa phương tiện `mo0.smil`.<br>• Tự động sinh tệp điều hướng phân cấp `navigation.ncx`.<br>• Khai báo toàn bộ tài nguyên vào gói manifest `book.opf` và `resources.res`.<br>• Xây dựng pipeline liên kết tự động toàn diện. | **TIẾP THEO**<br>`(PENDING)` |
| **4** | **Thành viên 4: Kiểm thử, Đóng gói & Báo cáo** *(QA, Packaging & Report Lead)* | • Kiểm thử thực tế trải nghiệm đọc trên Thorium Reader và Dolphin EasyReader.<br>• Đóng gói cấu trúc nén `Trong_Gia_Dinh.zip` theo từng chương.<br>• Sinh chuỗi mã băm SHA-256 (`Trong_Gia_Dinh_sha256sums.txt`).<br>• Sắp xếp cây thư mục nộp bài chuẩn quy định.<br>• Soạn thảo báo cáo đồ án tổng kết. | **TIẾP THEO**<br>`(PENDING)` |

---

## 3. Chi Tiết Kết Quả Nhiệm Vụ 1 (Task 1 Deliverables)

* **Dữ liệu nguồn:** [`data/trong_gia_dinh.epub`](data/trong_gia_dinh.epub) (23 chương từ `C0.html` đến `C22.html`).
* **Kết quả xử lý:** Toàn bộ **23 chương** đã được trích xuất, chuẩn hóa, phân tách câu và tạo tài liệu DTBook XML đạt chuẩn 100%.
  * **Tổng số đoạn văn (`<p>`):** 3,188 đoạn.
  * **Tổng số câu (`<sent>`):** 8,859 câu.
  * **Kiểm thử DTD & XML Syntax:** 23/23 chương **PASSED**.
* **Dữ liệu đầu ra bàn giao (Handoff Artifacts):** Nằm tại thư mục [`results/task1/`](results/task1/), gồm thư mục `Trong_Gia_Dinh-Gioi_Thieu/` và 22 chương `Trong_Gia_Dinh-Chuong_01/` đến `Trong_Gia_Dinh-Chuong_22/`:
  1. `dtbook.xml`: Tệp XML chuẩn DAISY 3 (DTBook 2005-3) với đầy đủ siêu dữ liệu và neo đồng bộ ID.
  2. `segments.json`: Tệp dữ liệu trung gian có cấu trúc phẳng (`sent_id`, `smil_sid`, `p_id`, `seq_id`, `text`) phục vụ trực tiếp cho Thành viên 2 (TTS) và Thành viên 3 (SMIL Alignment).

---

## 4. Cấu Trúc Thư Mục Dự Án (Repository Structure)

```text
.
├── README.md               # Tổng quan dự án, phân công nhiệm vụ và trạng thái
├── agent.md                # Quy chuẩn kiến trúc & hướng dẫn dành cho AI Agent Coding
├── .gitignore              # Cấu hình bỏ qua cache Python và hệ điều hành
├── data/                   # Thư mục chứa dữ liệu đầu vào
│   └── trong_gia_dinh.epub # Tệp sách điện tử gốc đầu vào
├── src/                    # Toàn bộ mã nguồn xử lý pipeline Task 1
│   ├── config.py           # Khai báo cấu hình, siêu dữ liệu sách và đường dẫn
│   ├── extract_clean.py    # Module trích xuất EPUB, làm sạch và tách câu tiếng Việt
│   ├── generate_dtbook.py  # Module sinh tài liệu DTBook XML 2005-3 chuẩn NISO
│   ├── validate_dtbook.py  # Module kiểm thử cú pháp XML, tính duy nhất ID và DTD
│   └── run_task1.py        # Script thực thi pipeline chính
└── results/                # Thư mục chứa kết quả của các nhiệm vụ
    └── task1/              # Kết quả Task 1: 23 chương sách DAISY 3
        ├── Trong_Gia_Dinh-Gioi_Thieu/
        │   ├── dtbook.xml
        │   └── segments.json
        ├── Trong_Gia_Dinh-Chuong_01/
        │   ├── dtbook.xml
        │   └── segments.json
        └── ... (đến Chương 22)
```

---

## 5. Hướng Dẫn Chạy Pipeline

Yêu cầu môi trường: Python 3.9+ và thư viện `beautifulsoup4`.

```bash
# Cài đặt thư viện phụ thuộc (nếu chưa có)
pip install beautifulsoup4

# 1. Chạy thử nghiệm pilot (Chương 0 - Giới thiệu và Chương 1)
python3 src/run_task1.py --pilot

# 2. Chạy toàn bộ 23 chương của cuốn sách
python3 src/run_task1.py --all

# 3. Chạy xử lý một chương cụ thể (ví dụ chương 5)
python3 src/run_task1.py --chapter 5
```
