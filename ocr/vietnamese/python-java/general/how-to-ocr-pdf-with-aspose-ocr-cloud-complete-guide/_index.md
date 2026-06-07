---
category: general
date: 2026-06-06
description: Cách OCR PDF bằng Aspose OCR Cloud. Học cách trích xuất văn bản từ PDF,
  chuyển đổi trang PDF sang PNG và lưu hình ảnh các trang PDF bằng Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: vi
og_description: Cách OCR PDF với Aspose OCR Cloud. Hướng dẫn này cho thấy cách trích
  xuất văn bản thuần từ PDF, chuyển đổi trang PDF sang PNG và lưu hình ảnh các trang
  PDF.
og_title: Cách OCR PDF với Aspose OCR Cloud – Từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Cách OCR PDF với Aspose OCR Cloud – Hướng Dẫn Toàn Diện
url: /vi/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR PDF với Aspose OCR Cloud – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi **cách OCR PDF** mà không phải vật lộn với các công cụ desktop nặng? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn khi cần một cách nhanh chóng, lập trình để lấy văn bản từ tài liệu đã quét. Tin tốt là gì? Với Aspose OCR Cloud bạn có thể **trích xuất văn bản từ PDF**, chuyển mỗi trang thành PNG, và thậm chí **lưu hình ảnh trang PDF** để sử dụng sau, tất cả từ một script Python gọn gàng.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết: từ cài đặt SDK, cấp phép cho engine, và nhận dạng các PDF đa trang, đến việc trích xuất văn bản thuần, chuyển các trang sang PNG, và lưu các hình ảnh đó trên đĩa. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng để chèn vào bất kỳ dự án nào cần khả năng **cách OCR PDF**.

## Những gì bạn cần

- **Python 3.8+** (mã hoạt động trên 3.10 và các phiên bản mới hơn)  
- Một tài khoản Aspose OCR Cloud – bạn sẽ nhận được file giấy phép dùng thử miễn phí (`Aspose.OCR.lic`)  
- Gói `asposeocrcloud` (`pip install asposeocrcloud`)  
- Một file PDF đã quét, đa trang mà bạn muốn xử lý  

Chỉ vậy thôi. Không cần binary bổ sung, không phụ thuộc gốc, chỉ Python thuần.

## Cách OCR PDF – Cài đặt và Cấp phép

Trước khi bạn có thể gọi bất kỳ phương thức OCR nào, bạn phải cho SDK biết bạn là ai. Aspose sử dụng một file giấy phép nhẹ mà bạn đặt ở vị trí mà script của bạn có thể truy cập.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Mẹo chuyên nghiệp:* Nếu bạn bỏ qua bước cấp phép, SDK vẫn hoạt động nhưng sẽ chèn một watermark nhỏ vào các hình ảnh đầu ra. Không lý tưởng cho môi trường production.

## Bước 2: Cài đặt Aspose OCR Cloud Python SDK

Mở terminal và chạy:

```bash
pip install asposeocrcloud
```

Gói này sẽ tự động tải về tất cả các phụ thuộc cần thiết (requests, pillow, v.v.) nên bạn không cần tìm kiếm gì thêm.

## Bước 3: Tạo một OCR Engine và Chọn Ngôn ngữ

Engine là trái tim của quá trình. Bạn có thể chỉ định bất kỳ ngôn ngữ nào được Aspose hỗ trợ; tiếng Anh hoạt động cho hầu hết các trường hợp.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Tại sao phải đặt ngôn ngữ? Bởi vì OCR engine sử dụng các từ điển riêng cho từng ngôn ngữ để cải thiện độ chính xác. Nếu bạn đang xử lý các PDF tiếng Pháp, chỉ cần thay `ENGLISH` bằng `FRENCH`.

## Bước 4: Chỉ định PDF Đa Trang của Bạn

Đưa engine đường dẫn đầy đủ tới file bạn muốn xử lý. Các đường dẫn tương đối cũng được chấp nhận miễn là chúng giải quyết được từ thư mục làm việc của script.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Đảm bảo file có thể đọc được; nếu không bạn sẽ gặp lỗi `FileNotFoundError`.

## Bước 5: Chạy OCR – Bạn Nhận Được Danh Sách Kết Quả

Gọi `recognize_pdf` trả về một danh sách, trong đó mỗi phần tử tương ứng với một trang của PDF nguồn.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Mỗi `OcrResult` chứa hai thuộc tính hữu ích:

* `text` – biểu diễn văn bản thuần của trang (tuyệt vời cho **extract plain text pdf**)  
* `image` – một đối tượng Pillow `Image` của trang đã render (hoàn hảo cho **convert pdf page png**)

## Bước 6: Trích xuất Văn bản từ PDF và Chuyển Trang sang PNG

Bây giờ chúng ta lặp qua các kết quả, in ra văn bản đã trích xuất và lưu phiên bản PNG của mỗi trang.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Expected Console Output

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Bạn cũng sẽ thấy các file `page_1.png`, `page_2.png`, … xuất hiện trong `YOUR_DIRECTORY`. Đó là các hình ảnh raster của các trang mà bạn có thể đưa vào các pipeline xử lý ảnh tiếp theo.

## Bước 7: Lưu Hình ảnh Trang PDF (Xử lý Sau Tùy chọn)

Nếu bạn chỉ cần hình ảnh mà không cần văn bản, bạn có thể bỏ qua dòng `print(res.text)`. Ngược lại, nếu bạn muốn lưu văn bản vào các file `.txt` riêng, chỉ cần thêm một đoạn ghi nhỏ:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Thêm nhỏ này cho thấy việc **lưu hình ảnh trang PDF** và đồng thời lưu nội dung đã trích xuất là bao nhiêu dễ dàng.

## Ví dụ Hoạt Động Đầy Đủ

Kết hợp mọi thứ lại, đây là script hoàn chỉnh bạn có thể sao chép‑dán vào `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Chạy nó với:

```bash
python ocr_pdf.py
```

Bạn sẽ thấy đầu ra console của văn bản mỗi trang và một loạt các file PNG.

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}