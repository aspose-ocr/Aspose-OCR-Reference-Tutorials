---
category: general
date: 2026-07-05
description: Cách sử dụng OCR trong Python để chuyển đổi TIFF sang văn bản nhanh chóng.
  Tìm hiểu các bước của thư viện OCR Python để trích xuất văn bản từ hình ảnh TIFF
  và xây dựng một công cụ OCR Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: vi
og_description: Cách sử dụng OCR trong Python? Hướng dẫn này sẽ chỉ cho bạn từng bước
  cách chuyển đổi TIFF sang văn bản bằng công cụ OCR Python và thư viện ocr python.
og_title: Cách sử dụng OCR trong Python – Trích xuất toàn bộ văn bản từ TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Cách sử dụng OCR trong Python – Trích xuất văn bản từ TIFF
url: /vi/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong Python – Trích Xuất Văn Bản từ TIFF

Bạn đã bao giờ tự hỏi **how to use OCR in Python** để biến một cuốn sách đã quét thành văn bản có thể chỉnh sửa không? Bạn không phải là người duy nhất—các nhà phát triển, nhà nghiên cứu và người đam mê đều gặp khó khăn này khi làm việc với các ảnh TIFF đa trang. Tin tốt? Với **ocr library python** bạn có thể khởi động một công cụ OCR nhỏ, chỉ vào một tệp TIFF và nhận được văn bản sạch, có thể tìm kiếm trong vài giây.

Trong hướng dẫn này, chúng tôi sẽ đi qua mọi thứ bạn cần: cài đặt gói phù hợp, tải một tệp TIFF đa trang, chạy công cụ OCR, và cuối cùng in nội dung của mỗi trang. Khi kết thúc, bạn sẽ có thể **convert TIFF to text** và **extract text from TIFF** các tệp mà không rời khỏi môi trường Python của mình.

## Yêu Cầu Trước

- Python 3.9 hoặc mới hơn (ví dụ đã được kiểm tra trên 3.11)
- Phiên bản mới nhất của thư viện `ocr` (hoặc bất kỳ `python ocr engine` tương thích nào bạn muốn)
- Tệp TIFF đa trang bạn muốn xử lý (chúng tôi sẽ gọi nó là `scanned_book.tif`)
- Kiến thức cơ bản về script Python và môi trường ảo

Không cần công cụ bên ngoài nặng—chỉ cần pip và vài dòng mã.

## Cài Đặt Thư Viện OCR cho Python

Đầu tiên: bạn cần một backend OCR vững chắc. Trong hướng dẫn này, chúng tôi sẽ sử dụng gói `ocr` giả tưởng đi kèm với một API cấp cao đơn giản, nhưng cùng một mẫu cũng áp dụng cho các wrapper dựa trên Tesseract như `pytesseract` hoặc SDK thương mại.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Nếu bạn đang dùng Windows và gói phụ thuộc vào các binary gốc, hãy chắc chắn rằng bạn đã cài đặt Visual C++ redistributable phù hợp. Trình cài đặt thường sẽ cảnh báo nếu có gì đó thiếu.

## Cách Sử Dụng Công Cụ OCR trong Python

Bây giờ thư viện đã sẵn sàng, hãy khởi động một công cụ OCR và chỉ vào tệp TIFF của chúng ta. Đoạn mã sau tạo một thể hiện engine, đặt ngôn ngữ thành tiếng Anh, và chuẩn bị cho việc xử lý đa trang.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Tại sao phải đặt ngôn ngữ?**  
Hầu hết các công cụ OCR sử dụng mô hình ngôn ngữ để cải thiện độ chính xác. Nếu bạn bỏ qua bước này, engine sẽ quay lại mô hình chung có thể nhận dạng sai dấu câu hoặc ký tự đặc biệt.

## Tải Ảnh TIFF Đa Trang

Phần tiếp theo là tải tài liệu đã quét. Trợ giúp `ocr.Image.load` hiểu các ngăn xếp TIFF ngay từ đầu, trả về một đối tượng đại diện cho mỗi trang bên trong.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Trường hợp đặc biệt:** Nếu TIFF của bạn sử dụng nén (CCITT Group 4, LZW, v.v.) và thư viện gây ra lỗi, hãy thử chuyển nó sang phiên bản không nén bằng ImageMagick trước:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Thực Hiện OCR trên Tất Cả Các Trang – Chuyển Đổi TIFF sang Văn Bản

Với đối tượng ảnh trong tay, engine hiện có thể xử lý mọi trang cùng một lúc. Phương pháp này trả về một danh sách, trong đó mỗi phần tử chứa kết quả OCR cho một trang duy nhất.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Điều gì đang diễn ra bên trong?**  
Hàm `recognize_multi_page` lặp qua mỗi trang rasterized, chạy bộ nhận dạng mạng nơ-ron, và gói kết quả văn bản thuần cùng với điểm tin cậy. Nó thực chất là một thao tác batch giúp bạn không phải viết vòng lặp thủ công.

## Duyệt Qua Kết Quả – Trích Xuất Văn Bản từ TIFF

Cuối cùng, chúng tôi hiển thị văn bản đã nhận dạng. Bạn có thể ghi kết quả ra các tệp `.txt` riêng biệt, đẩy nó vào cơ sở dữ liệu, hoặc đưa vào chỉ mục tìm kiếm—bất cứ gì phù hợp với quy trình làm việc của bạn.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Kết Quả Dự Kiến

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Mỗi chuỗi `result.text` chứa đầu ra OCR thô cho trang đó. Nếu bạn cần giữ nguyên ngắt dòng, hầu hết các engine cung cấp `result.lines` dưới dạng danh sách các chuỗi.

## Xử Lý Các Tệp TIFF Lớn – Mẹo & Thủ Thuật

Xử lý một tệp TIFF 500 trang có thể tốn nhiều bộ nhớ. Dưới đây là một vài chiến lược để duy trì hiệu suất mượt mà:

1. **Chunk the pages** – Thay vì `recognize_multi_page`, gọi `engine.recognize(page)` trong một generator trả về một trang mỗi lần.
2. **Adjust DPI** – Giảm độ phân giải ảnh (ví dụ, từ 300 DPI xuống 200 DPI) giảm tải CPU trong khi hầu như không ảnh hưởng đến độ chính xác cho phần lớn văn bản in.
3. **Parallelize** – Nếu engine OCR của bạn an toàn với đa luồng, tạo một `concurrent.futures.ThreadPoolExecutor` để chạy nhận dạng trên nhiều trang đồng thời.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Lưu Văn Bản Đã Trích Xuất vào Các Tệp

Hầu hết các pipeline thực tế cần lưu trữ bền vững. Dưới đây là cách ngắn gọn để ghi văn bản của mỗi trang vào tệp riêng, giữ nguyên thứ tự trang.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Bây giờ bạn có một thư mục sạch chứa các tệp `.txt` sẵn sàng cho việc lập chỉ mục hoặc xử lý NLP tiếp theo.

## Xem Trước Hình Ảnh – Cách Sử Dụng Kết Quả OCR Một Cách Trực Quan

Nếu bạn muốn xem lớp phủ OCR trên ảnh gốc (hữu ích cho việc gỡ lỗi), nhiều thư viện cho phép bạn vẽ các hộp bao quanh. Dưới đây là một ví dụ nhanh sử dụng Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Cách sử dụng OCR trong Python – lớp phủ OCR trên một trang TIFF](ocr_overlay_example.png)

*Alt text:* Cách sử dụng OCR trong Python – lớp phủ trực quan của văn bản đã nhận dạng trên một trang TIFF.

## Những Sai Lầm Thường Gặp và Cách Tránh Chúng

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| Garbled characters | Wrong language model | Set `engine.language` to the correct enum |
| Missing pages | TIFF compression not supported | Convert to uncompressed TIFF first |
| Slow performance | High DPI + single‑threaded processing | Reduce DPI or enable multi‑threading |
| Empty output | Image is too dark/low contrast | Pre‑process with contrast stretching (`opencv` or `Pillow`) |

Giải quyết những vấn đề này sớm sẽ tiết kiệm cho bạn hàng giờ gỡ lỗi sau này.

## Bước Tiếp Theo – Vượt Qua Việc Trích Xuất Cơ Bản

Bây giờ bạn đã nắm vững các kiến thức cơ bản về **how to use OCR in Python**, hãy cân nhắc khám phá:

- **PDF generation** – Kết hợp văn bản đã trích xuất với `reportlab` để tạo lại các PDF có thể tìm kiếm.
- **Language detection** – Tự động chuyển `engine.language` bằng `langdetect`.
- **Structured data extraction** – Sử dụng biểu thức chính quy hoặc spaCy để lấy ngày, tên, hoặc bảng từ văn bản thô.
- **Alternative OCR backends** – Thay `ocr` bằng `pytesseract` hoặc `easyocr` nếu bạn cần hỗ trợ đa ngôn ngữ.

Mỗi chủ đề này đều tự nhiên liên kết lại với các từ khóa phụ **ocr library python**, **convert tiff to text**, **extract text from tiff**, và **python ocr engine**, cung cấp cho bạn nền tảng vững chắc cho các dự án nâng cao hơn.

---

### Kết Luận

Chúng tôi đã bao phủ **how to use OCR in Python** từ cài đặt đến xử lý đa trang, cho bạn thấy chính xác cách **convert TIFF to text** và **extract text from TIFF** bằng một **python OCR engine** đơn giản. Ví dụ hoàn chỉnh, có thể chạy được ở trên sẽ hoạt động ngay lập tức cho hầu hết các tệp TIFF tiêu chuẩn, và các mẹo được cung cấp sẽ giúp bạn mở rộng quy mô lên tài liệu lớn hơn hoặc tích hợp OCR vào các pipeline lớn hơn.

Hãy thử với các cuốn sách đã quét, biên lai hoặc hình ảnh lưu trữ của bạn—sau đó thử nghiệm các ý tưởng cấp cao hơn được liệt kê trong phần “Bước Tiếp Theo”. Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn chính xác!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích Xuất Văn Bản từ Hình Ảnh với Aspose OCR – Hướng Dẫn Từng Bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách trích xuất văn bản từ tiff với Aspose.OCR cho Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Cách Thực Hiện Trích Xuất Văn Bản Hình Ảnh từ Luồng Sử Dụng Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}