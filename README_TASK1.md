# BÁO CÁO NHIỆM VỤ 1: XỬ LÝ VĂN BẢN & CẤU TRÚC DỮ LIỆU (TEXT & XML LEAD)

## 1. Thông Tin Sách & Siêu Dữ Liệu (Metadata)

* **Tên sách (`dc:Title`):** Trong Gia Đình (*En famille*)
* **Tác giả (`dc:Creator`):** Hector Malot
* **Dịch giả & Hiệu đính:** GS. Huỳnh Lý & Mai Hương; hiệu đính: Huỳnh Phan Thanh Yên
* **Nhà xuất bản (`dc:Publisher`):** NXB Văn Học (liên kết Công ty Cổ phần Văn hóa Đông A)
* **Mã ISBN (`dc:Source` / `dc:Identifier`):** `978-604-69-8175-6`
* **Thể loại (`dc:Subject`):** Văn học & Tiểu thuyết (thuộc 16 nhóm thể loại chuẩn)
* **Năm xuất bản (`dc:Date`):** 2017
* **Ngôn ngữ (`dc:Language`):** `vi-VN`
* **Định dạng chuẩn (`dc:Format`):** ANSI/NISO Z39.86-2005 (DAISY 3 / DTBook 2005-3)
* **Tóm tắt nội dung (`dc:Description`):** Cuốn sách kể về cuộc đời cô bé Perrine (Perin), 12 tuổi, mồ côi cha mẹ và hành trình đầy khó khăn, thử thách với nghị lực phi thường để vươn lên và được ông nội đón nhận trở lại trong gia đình.

---

## 2. Cấu Trúc Mã Nguồn Pipeline

Mã nguồn được tổ chức theo module chuyên biệt trong thư mục [`src/`](file:///Users/admin/Documents/master/XLTN/src/):

```text
src/
├── config.py           # Khai báo cấu hình đường dẫn và toàn bộ siêu dữ liệu chuẩn
├── extract_clean.py    # Trích xuất HTML từ EPUB, làm sạch văn bản, tách câu tiếng Việt
├── generate_dtbook.py  # Xây dựng cây XML DTBook 2005-3, gán id và smilref theo chuẩn NISO
├── validate_dtbook.py  # Bộ kiểm thử tính hợp lệ của XML, DTD, cấu trúc thẻ, trùng lặp id
└── run_task1.py        # Kịch bản thực thi chính (--pilot, --all, --chapter <id>)
```

---

## 3. Thống Kê Kết Quả Xử Lý

Toàn bộ **23 chương** (`C0.html` đến `C22.html`) đã được xử lý và kiểm tra tính hợp lệ thành công 100%:

| Chương | Tiêu Đề Chương | Đoạn văn (`<p>`) | Câu (`<sent>`) | Kiểm Tra XML & DTD |
|---|---|---|---|---|
| **00** | Giới Thiệu | 16 | 38 | ✅ PASSED |
| **01** | Phần I: Mất Mẹ - Chương 1 | 118 | 247 | ✅ PASSED |
| **02** | Chương 2 | 207 | 507 | ✅ PASSED |
| **03** | Chương 3 | 89 | 261 | ✅ PASSED |
| **04** | Chương 4 | 63 | 195 | ✅ PASSED |
| **05** | Phần Ii: Giã Từ Cõi Chết - Chương 6 | 76 | 249 | ✅ PASSED |
| **06** | Chương 6 | 61 | 325 | ✅ PASSED |
| **07** | Chương 7 | 153 | 349 | ✅ PASSED |
| **08** | Phần Iii: Sống Với Thợ Thuyền - Chương 8 | 163 | 422 | ✅ PASSED |
| **09** | Chương 9 | 274 | 693 | ✅ PASSED |
| **10** | Phần Iv: Rôbinxơn Tí Hon - Chương 10 | 86 | 416 | ✅ PASSED |
| **11** | Chương 11 | 96 | 326 | ✅ PASSED |
| **12** | Phần V: Được Tin Cậy - Chương 12 | 275 | 537 | ✅ PASSED |
| **13** | Chương 13 | 143 | 382 | ✅ PASSED |
| **14** | Phần Vi: Theo Dõi Và Bao Vây - Chương 14 | 96 | 240 | ✅ PASSED |
| **15** | Chương 15 | 160 | 378 | ✅ PASSED |
| **16** | Chương 16 | 185 | 524 | ✅ PASSED |
| **17** | Chương 17 | 183 | 523 | ✅ PASSED |
| **18** | Phần Vii: Chờ Mong… Tuyệt Vọng - Chương 18 | 159 | 559 | ✅ PASSED |
| **19** | Chương 19 | 96 | 372 | ✅ PASSED |
| **20** | Chương 20 | 235 | 603 | ✅ PASSED |
| **21** | Phần Viii: Chiếc Đũa Thần Của Nàng Tiên - Chương 21 | 128 | 377 | ✅ PASSED |
| **22** | Chương 23 | 126 | 336 | ✅ PASSED |
| **TỔNG CỘNG** | **23 Chương** | **3,188 đoạn văn** | **8,859 câu** | **100% ĐẠT CHUẨN** |

---

## 4. Cấu Trúc Dữ Liệu Bàn Giao (Handoff)

Mỗi chương được xuất vào một thư mục riêng trong [`output/`](file:///Users/admin/Documents/master/XLTN/output/):
Ví dụ: `output/Trong_Gia_Dinh-Chuong_01/` gồm 2 tệp:

1. **`dtbook.xml`**:
   * Tuân thủ chuẩn `dtbook-2005-3.dtd` (DAISY 3).
   * Phân cấp: `<frontmatter>` (`<doctitle>`, `<docauthor>`) và `<bodymatter>` (`<level1>` với `<h1>` và các `<p>`).
   * Mỗi câu văn bản đọc được bọc trong thẻ `<sent id="id_X" smilref="mo0.smil#sid_X">` nằm trong `<p id="c{ch}_p{idx}" smilref="mo0.smil#seq_{idx}">`.
2. **`segments.json`**:
   * Tệp JSON tiền xử lý dành riêng cho **Thành viên 2 (TTS & Giọng đọc)** và **Thành viên 3 (Đồng bộ SMIL)**.
   * Chứa danh sách các đoạn câu với các mã neo (`sent_id`, `smil_sid`, `p_id`, `seq_id`) và nội dung câu `text` đã được chuẩn hóa, giúp nhóm chạy trực tiếp mô hình TTS hoặc Forced Alignment mà không phải bóc tách lại XML.

---

## 5. Hướng Dẫn Chạy Mã Nguồn

```bash
# 1. Chạy thử nghiệm pilot (Chương 0 & Chương 1)
python3 src/run_task1.py --pilot

# 2. Chạy toàn bộ 23 chương
python3 src/run_task1.py --all

# 3. Chạy đơn lẻ một chương bất kỳ (ví dụ chương 2)
python3 src/run_task1.py --chapter 2
```
