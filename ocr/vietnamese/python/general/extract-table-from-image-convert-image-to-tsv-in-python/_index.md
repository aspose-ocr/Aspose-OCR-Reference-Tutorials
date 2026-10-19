---
category: general
date: 2026-07-05
description: Trích xuất bảng từ hình ảnh bằng Python OCR. Học cách trích xuất bảng,
  chuyển đổi hình ảnh sang TSV và thành thạo các kỹ thuật OCR bảng hình ảnh bằng Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: vi
og_description: Trích xuất bảng từ hình ảnh bằng Python OCR. Hướng dẫn này chỉ cách
  trích xuất bảng, chuyển đổi hình ảnh sang TSV và sử dụng các công cụ OCR bảng hình
  ảnh Python.
og_title: Trích xuất bảng từ hình ảnh – Chuyển hình ảnh sang TSV trong Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Trích xuất bảng từ hình ảnh – Chuyển đổi hình ảnh sang TSV trong Python
url: /vi/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Bảng từ Hình ảnh – Chuyển Hình ảnh sang TSV trong Python

Bạn đã bao giờ tự hỏi làm sao để trích xuất bảng từ hình ảnh mà không phải đau đầu không? Trong hướng dẫn này, chúng ta sẽ đi qua **cách trích xuất dữ liệu bảng** từ một bức ảnh bằng thư viện `aocr`, sau đó chuyển dữ liệu đó thành một tệp TSV gọn gàng. Không có phép màu, chỉ cần vài dòng Python và một chút xử lý hậu‑xử lý dựa trên AI.

Nếu bạn đã từng cố sao chép‑dán một bảng từ hoá đơn quét hoặc ảnh chụp màn hình và kết quả chỉ là một mớ hỗn độn, bạn sẽ hiểu vì sao việc sử dụng OCR là một phương pháp đáng học. Khi kết thúc, bạn sẽ có thể đưa bất kỳ hình ảnh chứa bảng nào vào Python và nhận được các giá trị tách bằng tab sạch sẽ, sẵn sàng cho bảng tính hoặc cơ sở dữ liệu.

---

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng máy của bạn đã có những thứ sau:

| Yêu cầu | Lý do cần |
|-------------|----------------|
| Python 3.9+ | Gói `aocr` hướng tới các môi trường Python hiện đại. |
| Thư viện `aocr` (`pip install aocr`) | Cung cấp engine OCR và AI post‑processor mà chúng ta sẽ dùng. |
| Một tệp hình ảnh chứa bảng (PNG, JPG, v.v.) | Dữ liệu nguồn mà chúng ta sẽ trích xuất. |
| Tùy chọn: môi trường ảo | Giúp cô lập các phụ thuộc — rất nên dùng. |

Có sẵn những thứ này sẽ giúp bạn tránh bị gián đoạn giữa chừng.

---

## Cài đặt các phụ thuộc

Đầu tiên, chúng ta sẽ cài đặt công cụ OCR. Mở terminal và chạy:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Mẹo:** Nếu gặp lỗi quyền, hãy thêm `--user` vào lệnh `pip install` hoặc dùng `pipx` để cài đặt toàn cục.

---

## Bước 1 – Khởi tạo Engine OCR

Engine là trái tim của quá trình. Hãy nghĩ nó như “bộ não” nhìn vào từng pixel và quyết định ký tự nào thuộc về vị trí nào.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Tại sao chúng ta tạo một engine thay vì gọi một hàm duy nhất? Đối tượng engine cho phép chúng ta gắn post‑processor tùy chỉnh sau này, mang lại khả năng kiểm soát chi tiết đầu ra — điều cần thiết khi bạn cần độ chính xác **ocr table image python**.

---

## Bước 2 – Gắn AI Post‑Processor

`aocr` đi kèm với một AI post‑processor nhẹ nhàng, giúp làm sạch kết quả OCR thô đồng thời giữ lại ranh giới ô. Không cần tham số bổ sung, giúp mã nguồn gọn gàng.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Nếu bỏ qua bước này, bạn vẫn sẽ nhận được văn bản thô, nhưng cấu trúc bảng sẽ bị nhiễu — giống như một bảng tính mà mỗi ô đều là một bí ẩn. Post‑processor thực hiện công việc nặng nề của việc căn chỉnh văn bản vào lưới gốc.

---

## Bước 3 – Tải Hình ảnh Bảng của Bạn

Bạn có thể tải hình ảnh từ bất kỳ đường dẫn nào, nhưng để dễ hiểu chúng ta sẽ dùng một thư mục mẫu. Thay `"YOUR_DIRECTORY/invoice_table.png"` bằng đường dẫn thực tế tới tệp của bạn.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Lưu ý:** `aocr.Image` tự động phát hiện định dạng ảnh và chuẩn hoá kênh màu, vì vậy bạn không cần tiền xử lý tệp trừ khi ảnh bị hư hỏng nghiêm trọng.

---

## Bước 4 – Thực hiện OCR có cấu trúc

Bây giờ engine sẽ quét ảnh và trả về một đối tượng bảng thô. Đối tượng này chứa các hàng, cột và văn bản thô cho mỗi ô.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Tại sao dùng `recognize_structured` thay vì lệnh `recognize` chung? Phiên bản có cấu trúc cố gắng suy ra ranh giới hàng/cột, cho bạn một kết quả dạng ma trận dễ dàng chuyển sang TSV hơn.

---

## Bước 5 – Làm sạch Dữ liệu bằng AI Post‑Processor

Chạy post‑processor sẽ tinh chỉnh đầu ra thô: loại bỏ ký tự lạ, gộp các đoạn bị tách, và đảm bảo văn bản của mỗi ô được căn chỉnh đúng.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Nếu bạn kiểm tra `processed_table.table`, sẽ thấy một danh sách các hàng, mỗi hàng là một danh sách các đối tượng `Cell`. Mỗi `Cell` có thuộc tính `.text` chứa chuỗi đã được làm sạch.

---

## Bước 6 – Xuất Bảng dưới dạng TSV

Bước cuối cùng là chuyển dữ liệu đã xử lý thành tệp giá trị tách bằng tab (TSV) — chính xác những gì bạn cần khi muốn **convert image to TSV** cho Excel hoặc Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Chạy script sẽ in mỗi hàng ra console (nếu bạn muốn) và ghi một tệp TSV sạch mà bạn có thể mở bằng bất kỳ chương trình bảng tính nào.

### Kiểm tra nhanh

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Bạn sẽ thấy các cột được căn chỉnh gọn gàng, ví dụ:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Nếu kết quả trông lộn xộn, hãy kiểm tra lại chất lượng ảnh (độ nét, độ tương phản) và cân nhắc điều chỉnh cấu hình engine OCR — `engine.set_config(...)` cho phép bạn thay đổi mô hình ngôn ngữ và ngưỡng confidence.

---

## Xử lý các Trường hợp Cạnh thường gặp

| Tình huống | Giải pháp đề xuất |
|-----------|-------------------|
| **Ảnh nghiêng** | Xoay trước bằng `Pillow` (`Image.rotate`) trước khi đưa vào `aocr`. |
| **Độ tương phản thấp** | Áp dụng cân bằng histogram (`cv2.equalizeHist`) để tăng khả năng đọc. |
| **Ô hợp nhất** | Xử lý TSV sau để tách ô dựa trên dấu phân cách đã biết hoặc dùng cờ `merge_cells=False` nếu có. |
| **PDF đa trang** | Chuyển mỗi trang thành ảnh trước (`pdf2image`) và chạy pipeline trong vòng lặp. |

Những điều chỉnh này giúp quy trình **ocr table image python** của bạn ổn định với nhiều nguồn dữ liệu khác nhau.

---

## Toàn bộ Script – Giải pháp Một‑Cửa

Dưới đây là script hoàn chỉnh, sẵn sàng chạy, bao gồm mọi bước đã thảo luận. Lưu lại dưới tên `extract_table.py` và thực thi `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ và các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}