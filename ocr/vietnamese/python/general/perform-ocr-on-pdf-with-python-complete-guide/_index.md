---
category: general
date: 2026-06-25
description: Thực hiện OCR trên PDF bằng Python — học cách tải PDF để OCR, trích xuất
  văn bản từ các trang PDF và xem trước văn bản đã nhận dạng một cách hiệu quả.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: vi
og_description: Thực hiện OCR trên PDF bằng Python. Hướng dẫn này chỉ cách tải PDF
  để OCR, trích xuất văn bản từ các trang PDF và xem trước văn bản đã nhận dạng một
  cách nhanh chóng.
og_title: Thực hiện OCR trên PDF bằng Python – Hướng dẫn chi tiết từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Thực hiện OCR trên PDF bằng Python – Hướng dẫn toàn diện
url: /vi/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên PDF bằng Python – Hướng dẫn toàn diện

Bạn đã bao giờ cần **perform OCR on PDF** nhưng không chắc bắt đầu từ đâu? Có thể bạn có một đống hợp đồng đã quét, hoặc một cuốn cẩm nang dày dặn không hợp tác với công cụ trích xuất văn bản thông thường của bạn. Nói ngắn gọn, bạn muốn **load PDF for OCR**, lấy văn bản ra và xem trước nhanh—tất cả mà không làm đầy bộ nhớ máy.

Chà, bạn đã đến đúng nơi. Trong hướng dẫn này, chúng tôi sẽ đi qua một script Python hoàn chỉnh có khả năng **extracts text from PDF pages**, cho bạn thấy cách **preview recognized text**, và thậm chí giải quyết vấn đề cổ điển **how to OCR large PDF** một cách hiệu quả.

Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy, hiểu rõ từng tùy chỉnh cấu hình, và một vài mẹo để tránh những bẫy thường gặp khiến người mới bối rối.

---

## Những gì bạn sẽ học

- Cách **load PDF for OCR** bằng thư viện `aocr`.
- Các bước chính xác để **perform OCR on PDF** các trang từng bước.
- Các cách **extract text from PDF pages** trong khi kiểm soát việc sử dụng bộ nhớ.
- Cách **preview recognized text** để kiểm tra kết quả.
- Các chiến lược xử lý **large PDFs** mà không làm cạn kiệt RAM.

> **Mẹo:** Hướng dẫn này giả định bạn đã cài Python 3.9+ và có kiến thức cơ bản về môi trường ảo. Nếu bạn mới với Python, hãy thiết lập virtualenv trước—tin tôi đi, nó sẽ tiết kiệm rất nhiều rắc rối sau này.

## Các yêu cầu trước

| Requirement | Why it matters |
|-------------|----------------|
| `aocr` Python package (or any compatible OCR engine) | Cung cấp lớp `OcrEngine` được sử dụng trong toàn bộ script. |
| `pip` and a virtual environment | Giữ các phụ thuộc tách biệt khỏi Python hệ thống của bạn. |
| Sufficient disk space for temporary image extracts | Cần đủ không gian đĩa cho các hình ảnh tạm thời được trích xuất. |
| Optional: `tqdm` for progress bars | Cải thiện trải nghiệm người dùng khi xử lý các công việc **how to OCR large PDF**. |

Cài đặt các thành phần cần thiết bằng:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Nếu PDF của bạn được bảo vệ bằng mật khẩu, bạn sẽ cần cung cấp mật khẩu sau này—xem phần “Edge Cases”.

## Bước 1: Perform OCR on PDF – Thiết lập Engine

Trước hết, chúng ta cần một thể hiện của OCR engine. Hãy nghĩ nó như bộ não sẽ đọc hình ảnh của mỗi trang và xuất ra văn bản thuần.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Tại sao đặt `max_memory_mb`?**  
> OCR engines thường lưu bộ nhớ đệm hình ảnh các trang trong RAM. Bằng cách giới hạn bộ nhớ, bạn ngăn script bị sập khi xử lý hợp đồng 500 trang.

## Bước 2: Load PDF for OCR và Cấu hình Cài đặt

Bây giờ chúng ta thực sự **load PDF for OCR**. Đường dẫn có thể là tuyệt đối hoặc tương đối; chỉ cần chắc rằng tệp tồn tại.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Nếu PDF được mã hoá, `engine.load_pdf` thường sẽ ném ra một ngoại lệ. Trong trường hợp đó, bạn có thể gọi `engine.load_pdf(pdf_path, password="secret")`—sẽ được giải thích chi tiết hơn sau.

## Bước 3: Extract Text from PDF Pages – Vòng lặp chính

Đây là nơi chúng ta **perform OCR on PDF** từng trang một. Chúng ta cũng sẽ **preview recognized text** cho vài trăm ký tự đầu tiên để bạn có thể xác nhận mọi thứ hoạt động.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Mẹo chuyên nghiệp:** Thanh tiến trình `tqdm` cung cấp chỉ báo trực quan, đặc biệt hữu ích khi xử lý các tài liệu **how to OCR large PDF** mất vài phút để xử lý.

## Bước 4: Putting It All Together – Script sẵn sàng chạy

Dưới đây là ví dụ đầy đủ, có thể chạy được. Lưu lại dưới tên `pdf_ocr.py` và thực thi bằng `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Kết quả dự kiến (trích đoạn)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Bạn sẽ thấy một đoạn preview ngắn cho mỗi trang, sau đó là xác nhận cuối cùng rằng tệp văn bản đã được ghi lại.

## Các trường hợp đặc biệt & Mẹo thực tế

| Situation | What to Do |
|-----------|------------|
| **Encrypted PDF** | Cung cấp mật khẩu: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **Very large PDF (> 1000 pages)** | Tăng `max_memory_mb` một cách thận trọng, hoặc xử lý theo từng khối (ví dụ, 200 trang mỗi lần). |
| **Mixed content (printed + handwritten)** | Chuyển `engine.recognition_mode` sang `aocr.RecognitionMode.MIXED` nếu thư viện hỗ trợ. |
| **Missing fonts or poor scan quality** | Tiền xử lý các trang bằng thư viện cải thiện hình ảnh (ví dụ, Pillow) trước khi gọi `recognize()`. |
| **Out‑of‑memory crashes** | Giảm `preview_len` hoặc ghi trực tiếp văn bản của mỗi trang ra đĩa thay vì giữ toàn bộ trong danh sách. |

## Cách OCR Large PDF hiệu quả – Chiến lược nâng cao

Khi giải quyết **how to OCR large PDF**, tốc độ và độ ổn định trở nên quan trọng. Dưới đây là một vài mẹo bạn có thể áp dụng vào script:

1. **Parallelize per page** – Sử dụng `concurrent.futures.ThreadPoolExecutor` nếu OCR engine hỗ trợ đa luồng.  
2. **Cache intermediate images** – Một số engine cho phép lưu các trang rasterized trên SSD, giảm đáng kể tải CPU khi chạy lại.  
3. **Batch write output** – Thay vì thêm vào danh sách Python, mở tệp đầu ra một lần và ghi văn bản của mỗi trang ngay khi sẵn sàng.  
4. **Adjust DPI** – Giảm DPI trong quá trình rasterization giảm bộ nhớ nhưng có thể ảnh hưởng đến độ chính xác; tìm mức cân bằng (thường 200‑300 DPI).

Dưới đây là một đoạn mã nhanh cho thấy cách bạn có thể parallelize bước OCR (tùy chọn, bỏ comment để sử dụng):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Lưu ý: việc song song có thể tăng mức sử dụng CPU, vì vậy hãy theo dõi nhiệt độ hệ thống khi chạy lâu.

## Câu hỏi thường gặp

**Q: Tôi có thể dùng script này với các thư viện OCR khác như Tesseract không?**  
A: Chắc chắn. Thay thế các lời gọi `aocr` bằng `pytesseract.image_to

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh, hoạt động với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}