---
category: general
date: 2026-06-19
description: Thực hiện OCR trên hình ảnh bằng thư viện OCR của Python. Tìm hiểu cách
  phát hiện văn bản từ hình ảnh, nhận dạng văn bản từ JPEG và trích xuất văn bản từ
  ảnh quét một cách hiệu quả.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: vi
og_description: Thực hiện OCR trên hình ảnh bằng Python và trích xuất văn bản từ các
  tệp quét. Hướng dẫn này sẽ đưa bạn qua các bước tải hình ảnh, chỉnh nghiêng và nhận
  dạng văn bản từng bước.
og_title: Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn trích xuất toàn bộ văn
  bản
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn trích xuất toàn bộ văn
  bản
url: /vi/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn trích xuất văn bản đầy đủ

Bạn đã bao giờ cần **thực hiện OCR trên các tệp hình ảnh** nhưng gặp khó khăn vì mã nguồn quá khó hiểu? Bạn không phải là người duy nhất. Dù bạn đang chuyển một đống biên lai đã quét thành PDF có thể tìm kiếm được hay lấy chú thích từ một tệp JPEG cho dự án khoa học dữ liệu, khả năng nhận dạng văn bản từ JPEG và các định dạng khác là kỹ năng không thể thiếu đối với bất kỳ nhà phát triển nào ngày nay.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy ngay, cho bạn thấy cách **phát hiện văn bản từ các tệp hình ảnh**, **trích xuất văn bản từ tài liệu hình ảnh đã quét**, và thậm chí **tải hình ảnh cho OCR** chỉ trong vài dòng mã. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng cho môi trường production mà có thể chèn vào dự án của mình—không thiếu import, không có các “xem tài liệu” mơ hồ.

## Những gì bạn sẽ xây dựng

- Một script Python nhỏ tạo một engine OCR, bật tính năng tự động cân chỉnh (auto‑deskew), tải một JPEG (hoặc bất kỳ định dạng nào được hỗ trợ), và in ra văn bản đã nhận dạng.
- Giải thích **tại sao** mỗi thiết lập quan trọng, không chỉ **cách** viết nó.
- Mẹo xử lý PDF đa trang, ngôn ngữ không phải tiếng Anh, và các lỗi thường gặp như ảnh mờ.

### Yêu cầu trước

- Python 3.8+ đã được cài đặt (ví dụ sử dụng gói `ocr` có sẵn qua `pip install ocr-lib` – thay thế bằng tên thư viện thực tế của bạn).
- Kiến thức cơ bản về hàm Python và môi trường ảo.
- Một tệp hình ảnh (JPEG, PNG, TIFF) mà bạn muốn xử lý; chúng tôi sẽ dùng `skewed_page.jpg` làm ví dụ.

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Windows, chạy terminal với quyền Administrator khi cài đặt thư viện OCR để tránh các lỗi quyền truy cập.

---

## Thực hiện OCR trên hình ảnh – Cài đặt và cấu hình

Điều đầu tiên bạn cần là một thể hiện engine OCR sạch sẽ. Hãy nghĩ nó như bộ não của toàn bộ quá trình; nếu không cấu hình đúng, ngay cả hình ảnh sắc nét nhất cũng sẽ trả về kết quả vô nghĩa.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Tại sao điều này quan trọng:**  
Cài đặt `engine.language` giúp thu hẹp bộ ký tự mà engine OCR mong đợi, từ đó tăng độ chính xác đáng kể. Nếu bỏ qua, engine sẽ phải đoán, thường xuyên nhận dạng sai các từ đơn giản.

---

## Bật tính năng tự động cân chỉnh – Sửa các ảnh quét nghiêng

Các trang được quét hiếm khi hoàn toàn thẳng. Một góc nghiêng nhẹ có thể làm sai lệch việc phân đoạn ký tự, biến “Hello” thành “H3llo”. Cờ `auto_deskew` sẽ thực hiện công việc nặng này cho bạn.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Trường hợp đặc biệt:** Nếu bạn biết các ảnh của mình đã thẳng, việc tắt deskew có thể giảm vài mili giây thời gian xử lý—rất hữu ích khi xử lý hàng ngàn trang trong một batch job.

---

## Tải hình ảnh cho OCR – Hỗ trợ JPEG, PNG, TIFF

Bây giờ chúng ta thực sự **tải hình ảnh cho OCR**. Phương thức `ocr.Image.load` rất linh hoạt; nó chấp nhận đường dẫn tới bất kỳ định dạng raster nào được hỗ trợ.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Tại sao bước này quan trọng:** Thư viện đọc tệp vào một bitmap nội bộ, thực hiện bất kỳ chuyển đổi không gian màu nào cần thiết. Bỏ qua bước này và truyền một luồng byte thô sẽ gây ra `FileNotFoundError` hoặc, tệ hơn, trả về kết quả rỗng mà không có cảnh báo.

Nếu bạn cần **nhận dạng văn bản từ các tệp JPEG** cụ thể, chỉ cần đảm bảo phần mở rộng tệp là `.jpeg` hoặc `.jpg`. Lệnh gọi tương tự cũng hoạt động với PNG (`.png`) hoặc TIFF (`.tif`) mà không cần thay đổi.

---

## Thực hiện OCR trên hình ảnh – Chạy engine

Với engine đã được chuẩn bị và hình ảnh đã ở trong bộ nhớ, đã đến lúc **thực hiện OCR trên hình ảnh**. Dòng lệnh duy nhất này thực hiện toàn bộ công việc: tiền xử lý, phân đoạn, phân loại và ghép văn bản.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Bên trong engine đang làm gì?**  
- Engine áp dụng phép biến đổi deskew (nếu được bật).  
- Nó chạy một mạng nơ-ron hoặc backend Tesseract để nhận dạng ký tự.  
- Cuối cùng, nó ghép các ký tự thành từ và dòng, trả về một đối tượng `result` phong phú.

---

## Trích xuất văn bản từ hình ảnh đã quét – Xuất kết quả

Bước cuối cùng là **trích xuất văn bản từ hình ảnh đã quét** và hiển thị nó. Thuộc tính `result.text` chứa phiên bản văn bản thuần.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Kết quả thường trông như sau:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Nếu engine OCR không tìm thấy ký tự nào, `result.text` sẽ là một chuỗi rỗng. Trong trường hợp đó, hãy kiểm tra lại chất lượng ảnh hoặc cân nhắc điều chỉnh thuộc tính `engine.confidence_threshold` (nếu thư viện của bạn hỗ trợ).

---

## Xử lý các biến thể phổ biến

### Nhận dạng văn bản từ JPEG so với PNG

Cả hai định dạng đều được hỗ trợ, nhưng nén JPEG có thể tạo ra các artefact làm rối engine. Nếu bạn gặp nhiều lỗi nhận dạng, hãy thử chuyển JPEG sang PNG trước:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Phát hiện văn bản từ hình ảnh với nhiều ngôn ngữ

Nếu tài liệu của bạn chứa cả tiếng Anh và tiếng Tây Ban Nha, hãy bật chế độ đa ngôn ngữ:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Engine sẽ cân nhắc cả hai bảng chữ cái trong quá trình nhận dạng.

### Trích xuất văn bản từ PDF đã quét

Đối với PDF, bạn cần raster hoá mỗi trang thành hình ảnh trước. Các thư viện như `pdf2image` giúp việc này trở nên đơn giản:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Ví dụ hoàn chỉnh

Dưới đây là script đầy đủ mà bạn có thể sao chép‑dán vào tệp `ocr_demo.py`. Nó bao gồm xử lý lỗi và một helper nhỏ để đo thời gian thực thi.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Kết quả mong đợi** (giả sử ảnh quét rõ ràng):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Câu hỏi thường gặp

**H: Tôi có thể chạy script này trên máy chủ không có giao diện (headless) không?**  
Đ: Hoàn toàn có thể. Thư viện hoạt động mà không cần GUI; chỉ cần đảm bảo các binary gốc cần thiết (ví dụ, Tesseract) đã được cài đặt trên máy chủ.

**H: Nếu ảnh bị mờ thì sao?**  
Đ: Hãy cân nhắc thêm bộ lọc làm nét trước khi gọi `engine.recognize`. Nhiều thư viện OCR cung cấp `image_preprocessing.sharpen = True` hoặc bạn có thể dùng `cv2.GaussianBlur` của OpenCV theo hướng ngược lại.

**H: Script có hỗ trợ xử lý hàng loạt không?**  
Đ: Có. Đơn giản gói `perform_ocr` trong một vòng lặp qua danh sách các đường dẫn tệp,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}