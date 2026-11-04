---
category: general
date: 2026-06-28
description: Cách thực hiện OCR hàng loạt bằng Python. Học cách OCR nhiều hình ảnh,
  trích xuất văn bản từ PNG và chuyển đổi hình ảnh thành văn bản với hướng dẫn OCR
  Python đầy đủ.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: vi
og_description: Cách thực hiện OCR hàng loạt trong Python được giải thích trong câu
  đầu tiên. Hãy theo dõi hướng dẫn OCR bằng Python này để trích xuất văn bản từ các
  tệp PNG một cách hiệu quả.
og_title: Cách thực hiện OCR hàng loạt bằng Python – Hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Cách thực hiện OCR hàng loạt trong Python – Hướng dẫn chi tiết từng bước
url: /vi/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng Dẫn Toàn Diện Cách Thực Hiện Batch OCR trong Python – Bước‑đến‑Bước

Bạn đã bao giờ tự hỏi **cách batch OCR** một chồng trang đã quét mà không phải viết vòng lặp làm nghẽn UI chưa? Bạn không phải là người duy nhất. Xử lý hàng chục file PNG từng cái một có thể cảm giác như đang xem sơn khô, đặc biệt khi mỗi ảnh mất một hoặc hai giây để giải mã.  

Trong tutorial này, chúng tôi sẽ chỉ cho bạn một cách sạch sẽ, không chặn UI để **OCR nhiều hình ảnh** cùng lúc, **trích xuất văn bản từ file PNG**, và **chuyển đổi hình ảnh thành văn bản** bằng một engine OCR hiện đại của Python. Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy mà có thể đưa vào bất kỳ dự án nào – hoàn hảo cho một *python ocr tutorial* nhanh hoặc một job batch cấp production.

## Những Gì Bạn Sẽ Xây Dựng

- Khởi tạo một engine OCR và đặt ngôn ngữ của nó thành Latin (hoặc bất kỳ ngôn ngữ nào bạn cần).  
- Cung cấp danh sách các đường dẫn hình ảnh (PNG trong ví dụ của chúng tôi) cho engine.  
- Khởi chạy một thao tác batch trả về một đối tượng kiểu Future.  
- Lấy tất cả kết quả đồng thời bằng một thread pool, để luồng chính của bạn luôn tự do.  
- In ra văn bản đã nhận dạng cho mỗi trang, được ngăn cách rõ ràng.

Không có phép màu ẩn nào, chỉ là Python thuần và một thư viện OCR bên thứ ba (chúng tôi sẽ dùng gói `pyocr` giả tưởng để minh họa).  

**Yêu cầu trước**  
- Python 3.8+ đã được cài đặt.  
- Hiểu biết cơ bản về các hàm Python và `concurrent.futures`.  
- Truy cập được một thư viện OCR cung cấp lớp `OcrEngine` (ví dụ: `pip install pyocr`).  

Nếu bạn còn thiếu bất kỳ mục nào, hãy cài đặt ngay – việc này dễ hơn bạn nghĩ.

---

## Cách Thực Hiện Batch OCR trong Python – Các Khái Niệm Cốt Lõi

Trước khi đi vào code, hãy trả lời câu hỏi “tại sao” cho mỗi bước.

1. **Tại sao phải đặt ngôn ngữ?**  
   Độ chính xác của OCR tăng vọt khi engine biết trước các ký tự sẽ xuất hiện. Latin phù hợp cho tiếng Anh, Pháp, Tây Ban Nha, v.v. Chuyển sang `Language.Japanese` hoặc `Language.Arabic` nếu cần.

2. **Tại sao dùng một thao tác batch?**  
   Lệnh batch cho phép engine lên lịch công việc nội bộ, thường tận dụng các thread gốc hoặc tăng tốc GPU. Nó trả về một handle mà bạn có thể truy vấn sau, nghĩa là bạn không bị chặn trong khi mỗi ảnh đang được xử lý.

3. **Tại sao lại dùng ThreadPoolExecutor?**  
   Đối tượng Future mà chúng ta nhận được là *lazy* – nó chỉ bắt đầu kéo kết quả khi chúng ta yêu cầu. Bằng cách truyền một thread pool cho `getAll`, chúng ta để Python lấy văn bản của mỗi trang một cách song song, giảm đáng kể thời gian chạy tổng thể.

4. **Tại sao phải enumerate (đánh số) các kết quả?**  
   Thứ tự của các kết quả khớp với thứ tự của các đường dẫn đầu vào, vì vậy chúng ta có thể an toàn gắn nhãn số trang cho mỗi kết quả.

Hiểu được những “tại sao” này sẽ giúp bạn áp dụng mẫu này cho các thư viện khác hoặc cho các bộ dữ liệu lớn hơn.

---

## Bước 1: Cài Đặt và Import Các Gói Cần Thiết

Đầu tiên, chắc chắn rằng thư viện OCR đã được cài đặt. Ví dụ dùng gói `pyocr` chung; thay thế bằng thư viện thực tế bạn muốn (ví dụ: `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Bây giờ import mọi thứ chúng ta cần.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Mẹo chuyên nghiệp:** Sử dụng `Path` từ `pathlib` giúp script của bạn không phụ thuộc vào hệ điều hành và dễ đọc hơn.

---

## Bước 2: Tạo Engine OCR và Đặt Ngôn Ngữ

Việc tạo engine rất đơn giản. Chúng ta sẽ khóa nó ở ngôn ngữ Latin cho demo này.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

Lệnh `setLanguage` là tùy chọn đối với một số engine, nhưng đây là thói quen tốt. Nó báo cho mô hình OCR biết tập ký tự bạn quan tâm, cải thiện tốc độ và độ chính xác.

---

## Bước 3: Liệt Kê Các File Ảnh Cần Xử Lý (Extract Text from PNG)

Thu thập tất cả các file PNG bạn muốn chuyển đổi. Dùng `Path.glob` cho phép bạn chỉ cần đặt một thư mục mà không cần chỉnh sửa script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Tại sao lại quan trọng:** Bằng cách sắp xếp danh sách, chúng ta đảm bảo thứ tự xác định, sau này sẽ khớp mỗi kết quả với đúng số trang.

---

## Bước 4: Khởi Chạy Thao Tác Batch OCR (Convert Image to Text)

Bây giờ chúng ta truyền danh sách cho engine. Phương thức này trả về một container kiểu Future mà chúng ta sẽ truy vấn sau.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Bên trong, engine có thể khởi tạo các thread làm việc riêng hoặc thậm chí một pipeline GPU. Điều chúng ta cần chỉ là có một handle (`batch_future`) biết cách lấy các kết quả riêng lẻ.

---

## Bước 5: Lấy Tất Cả Kết Quả Đồng Thời (OCR Multiple Images)

Đây là nơi chúng ta thực sự *batch* công việc. Bằng cách cung cấp một `ThreadPoolExecutor` cho `getAll`, văn bản của mỗi trang sẽ được lấy trong một thread riêng.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Bạn có thể điều chỉnh `max_workers` dựa trên số core CPU hoặc khuyến nghị của thư viện OCR. Nhiều worker ≠ luôn nhanh hơn – hãy theo dõi mức sử dụng CPU.

---

## Bước 6: Xuất Văn Bản Đã Nhận Dạng (Python OCR Tutorial Finale)

Cuối cùng, in ra văn bản của mỗi trang. Đối tượng `Result` cung cấp `getText()` – thay đổi nếu thư viện của bạn dùng tên phương thức khác.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Kết quả mong đợi (mẫu)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Nếu bất kỳ ảnh nào thất bại, hầu hết các engine sẽ trả về một chuỗi rỗng hoặc ném exception – bạn có thể bọc vòng lặp trong khối `try/except` để xử lý các trường hợp ngoại lệ một cách nhẹ nhàng.

---

## Script Đầy Đủ – Sẵn Sàng Chạy

Dưới đây là script hoàn chỉnh, tự chứa. Sao chép‑dán vào một file tên `batch_ocr.py`, chỉnh `YOUR_DIRECTORY`, và chạy `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Lưu, chạy, và xem console hiện ra văn bản đã trích xuất. Đơn giản, nhanh, và hoàn toàn bất đồng bộ.

---

## Những Sai Lầm Thường Gặp & Cách Tránh

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Không có đầu ra** – chuỗi rỗng | Engine OCR không tìm thấy văn bản (ảnh quá nhiễu) | Tiền xử lý ảnh: nhị phân, căn chỉnh, hoặc tăng DPI |
| **`FileNotFoundError`** | Đường dẫn thư mục sai hoặc thiếu file PNG | Kiểm tra lại `YOUR_DIRECTORY` và chắc chắn các file có đuôi `.png` |
| **CPU sử dụng cao** | `max_workers` đặt quá cao so với máy | Giảm `max_workers` hoặc bật tăng tốc GPU nếu hỗ trợ |
| **Ký tự Unicode bị lộn** | Engine mặc định ngôn ngữ khác | Gọi `engine.setLanguage(Language.Latin)` (hoặc ngôn ngữ phù hợp) trước khi batch OCR |

Xử lý những vấn đề này sớm sẽ tiết kiệm hàng giờ debug.

---

## Mở Rộng Tutorial – Các Bước Tiếp Theo

- **OCR nhiều ảnh** ở các định dạng khác (JPEG, TIFF) – chỉ cần thay đổi mẫu glob.  
- **Extract text from PNG** và đưa vào chỉ mục tìm kiếm (ví dụ: Elasticsearch).  
- **Convert image to text** để tạo PDF bằng `reportlab` hoặc `PyPDF2`.  
- **Parallelize trên nhiều máy** với `multiprocessing` hoặc hàng đợi tác vụ như Celery cho bộ dữ liệu khổng lồ.  

Mỗi chủ đề này đều dựa trên **python ocr tutorial** bạn vừa hoàn thành.

---

## Kết Luận

Chúng ta đã đi qua **cách batch OCR** một tập hợp các file PNG, minh chứng sức mạnh của API hướng batch, và cho bạn thấy cách **extract text from PNG** bằng cách dùng thread‑pool. Script hoàn chỉnh ở trên đã sẵn sàng cho môi trường production, và bạn giờ đã có nền tảng vững chắc cho bất kỳ dự án Python nào liên quan tới OCR.

Hãy thử chạy, điều chỉnh cài đặt ngôn ngữ, và thậm chí thay `pyocr` bằng `pytesseract` – mẫu vẫn giữ nguyên. Có câu hỏi hay muốn chia sẻ một trường hợp sử dụng thú vị? Để lại bình luận, và chúng ta cùng thảo luận nhé.

*Chúc bạn lập trình vui vẻ!*

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial dưới đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn đầy đủ và các giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}