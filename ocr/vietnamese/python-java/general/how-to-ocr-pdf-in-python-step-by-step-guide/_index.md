---
category: general
date: 2026-03-28
description: Học cách OCR PDF bằng Python nhanh chóng. Hướng dẫn này cho bạn biết
  cách trích xuất văn bản từ PDF, nhận dạng văn bản từ PDF và chuyển PDF đã quét thành
  văn bản bằng Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: vi
og_description: Thành thạo cách OCR PDF bằng Python. Trích xuất văn bản từ PDF, nhận
  dạng văn bản từ PDF và chuyển PDF đã quét thành văn bản trong vài phút.
og_title: Cách OCR PDF trong Python – Hướng dẫn đầy đủ
tags:
- PDF
- OCR
- Python
- Aspose
title: Cách OCR PDF trong Python – Hướng dẫn từng bước
url: /vi/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR PDF trong Python – Hướng Dẫn Từng Bước

Bạn đã bao giờ tự hỏi **cách OCR PDF** khi tệp chỉ là một bức ảnh của một trang chưa? Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ đi qua các bước chính xác để OCR PDF, trích xuất văn bản từ PDF và chuyển một PDF đã quét thành văn bản có thể tìm kiếm — tất cả chỉ bằng mã Python thuần.

Chúng tôi sẽ bao phủ mọi thứ từ cài đặt thư viện Aspose OCR đến việc lấy văn bản đã nhận dạng ra khỏi mỗi trang. Khi kết thúc, bạn sẽ có thể **OCR PDF với Python**, **trích xuất văn bản từ PDF**, và **chuyển đổi PDF đã quét thành văn bản** mà không phải mò mẫm qua các tài liệu rải rác. Không có phần thừa, chỉ có một ví dụ thực tế, có thể chạy ngay mà bạn có thể sao chép‑dán.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.8+ (phiên bản ổn định mới nhất hoạt động tốt nhất)  
* Giấy phép Aspose OCR for Python hoặc khóa dùng thử miễn phí – bạn có thể lấy nó từ trang web của Aspose.  
* Một tệp PDF đã quét mà bạn muốn xử lý (chúng tôi sẽ gọi nó là `input.pdf`).  

Nếu bạn đã có những thứ này, tuyệt vời — hãy bắt đầu. Nếu chưa, việc cài đặt gói là rất nhanh và chúng tôi sẽ chỉ cho bạn cách thực hiện.

## Cách OCR PDF – Thiết lập môi trường

Điều đầu tiên bạn phải làm là đưa mô-đun Aspose OCR vào máy của mình. Gói này có tên `aspose-ocr`, và bạn có thể cài đặt nó qua pip:

```bash
pip install aspose-ocr
```

> **Mẹo chuyên nghiệp:** Sử dụng môi trường ảo (`python -m venv venv`) để các phụ thuộc của bạn luôn gọn gàng.

Sau khi gói đã được cài đặt, bạn đã sẵn sàng để import và khởi động engine OCR. Đây là nền tảng cho mọi quy trình **ocr pdf with python** mà bạn sẽ xây dựng sau này.

## OCR PDF với Python – Nhập Aspose OCR

Bây giờ thư viện đã sẵn sàng, hãy đưa nó vào script của bạn. Chúng ta cũng sẽ đặt engine ở *chế độ PDF trực tiếp*, cho phép Aspose đọc dữ liệu PDF trực tiếp từ tệp thay vì chuyển mỗi trang thành ảnh trước.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Tại sao lại dùng `PdfMode.DIRECT`? Vì nó bỏ qua bước raster hoá thêm, làm cho quá trình nhanh hơn và giữ nguyên bố cục gốc — đặc biệt hữu ích khi bạn cần **recognize text from PDF** một cách chính xác.

## Nhận dạng Văn bản từ PDF – Chạy Engine

Với engine đã sẵn sàng, chỉ cần trỏ nó tới tệp PDF đã quét của bạn. Phương thức `recognize_from_pdf` thực hiện toàn bộ công việc nặng: phân tích mọi trang, chạy thuật toán OCR và trả về một đối tượng `OcrResult` chứa một tập hợp các đối tượng `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Nếu bạn thắc mắc liệu cách này có hoạt động với PDF được mã hoá không — có, miễn là bạn cung cấp mật khẩu qua `ocr_engine.password = "secret"` trước khi gọi `recognize_from_pdf`. Đây là một trường hợp đặc biệt mà nhiều hướng dẫn bỏ qua, nhưng lại rất hữu ích trong các pipeline thực tế.

## Trích xuất Văn bản từ PDF – Truy cập Kết quả Trang

Danh sách `ocr_result.pages` chứa một mục cho mỗi trang. Mỗi đối tượng `Page` có thuộc tính `.text` chứa đại diện văn bản thuần của trang đã quét. Hãy lặp qua và in ra kết quả để bạn có thể thấy chính xác những gì đã được trích xuất.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Chạy script sẽ xuất ra một thứ gì đó giống như:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Kết quả này chứng minh bạn đã **extract text from PDF** và **recognize text from PDF** thành công bằng Aspose OCR. Bây giờ bạn có thể đưa các chuỗi này vào cơ sở dữ liệu, chỉ mục tìm kiếm, hoặc bất kỳ pipeline NLP nào tiếp theo.

![ví dụ cách OCR PDF](placeholder-image.png "ví dụ cách OCR PDF")

*Image alt text:* **ví dụ cách OCR PDF** – hiển thị đầu ra console của văn bản đã nhận dạng cho mỗi trang.

## Chuyển đổi PDF đã quét thành Văn bản – Lưu Kết quả

Hầu hết các nhà phát triển không chỉ muốn xem văn bản trên console; họ cần một tệp lưu trữ lâu dài. Dưới đây là một helper nhỏ ghi văn bản của mỗi trang vào một tệp `.txt` riêng, thực chất **convert scanned PDF to text** trong một thư mục gọi là `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Sau khi script kết thúc, bạn sẽ có một thư mục gọn gàng:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Giờ bạn đã hoàn toàn **convert scanned PDF to text** và có thể đưa các tệp này vào bất kỳ quy trình nào tiếp theo — tìm kiếm, phân tích, hoặc thậm chí một lệnh `grep` đơn giản.

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

**Nếu PDF của tôi chứa cả hình ảnh và văn bản thực thì sao?**  
Aspose OCR sẽ cố gắng nhận dạng mọi thứ, nhưng bạn có thể tăng tốc bằng cách tắt OCR cho các trang đã có văn bản có thể chọn được. Đặt `ocr_engine.auto_detect_page_orientation = True` và sau đó gọi `ocr_engine.recognize_from_pdf(..., detect_text=False)` cho các trang đã biết là tốt.

**Tôi có thể điều chỉnh mô hình ngôn ngữ không?**  
Chắc chắn. Đặt `ocr_engine.language = aocr.Language.English` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) trước khi gọi `recognize_from_pdf`. Điều này cải thiện độ chính xác cho các tài liệu không phải tiếng Anh.

**Làm sao xử lý các PDF rất lớn (hơn 100 trang)?**  
Xử lý chúng theo từng khối. Phương thức `recognize_from_pdf` chấp nhận đối số `page_range`, ví dụ `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Lặp qua các khoảng để giữ mức sử dụng bộ nhớ thấp.

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả lại, đây là một script duy nhất mà bạn có thể lưu vào tệp `ocr_pdf.py` và chạy:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Chạy nó bằng:

```bash
python ocr_pdf.py
```

Bạn sẽ thấy đầu ra console xác nhận văn bản của mỗi trang và vị trí các tệp `.txt` đã được lưu.

## Kết luận

Chúng ta đã đề cập **cách OCR PDF** bằng Python, trình bày một cách sạch sẽ để **ocr pdf with python**, chỉ ra cách **extract text from PDF**, giải thích cơ chế phía sau **recognize text from PDF**, và cuối cùng cung cấp một đoạn mã sẵn sàng sử dụng để **convert scanned PDF to text**. Toàn bộ quy trình đã được gói gọn

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}