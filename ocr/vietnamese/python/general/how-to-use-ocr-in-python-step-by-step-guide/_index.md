---
category: general
date: 2026-08-12
description: Cách sử dụng OCR trong Python để nhận dạng văn bản từ hình ảnh, trích
  xuất văn bản, chuyển đổi hình ảnh thành văn bản và làm sạch văn bản OCR bằng xử
  lý hậu kỳ AI.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- clean up OCR text
language: vi
lastmod: 2026-08-12
og_description: Cách sử dụng OCR trong Python để chuyển ảnh thành văn bản có thể chỉnh
  sửa. Học cách nhận dạng văn bản từ hình ảnh, trích xuất văn bản, chuyển đổi hình
  ảnh thành văn bản và làm sạch văn bản OCR bằng AI.
og_image_alt: Screenshot of Python code converting an image to clean text using OCR
  and AI post‑processing
og_title: Cách sử dụng OCR trong Python – hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  headline: How to use OCR in Python – step‑by‑step guide
  type: TechArticle
- description: How to use OCR in Python to recognize text from image, extract text,
    convert image to text, and clean up OCR text with AI post‑processing.
  name: How to use OCR in Python – step‑by‑step guide
  steps:
  - name: Loads an image file (PNG, JPEG, or TIFF).
    text: Loads an image file (PNG, JPEG, or TIFF).
  - name: Recognizes text from the image using an OCR engine.
    text: Recognizes text from the image using an OCR engine.
  - name: Improves the raw output with an AI‑driven post‑processor.
    text: Improves the raw output with an AI‑driven post‑processor.
  - name: Prints the cleaned‑up text to the console.
    text: Prints the cleaned‑up text to the console.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- AI post‑processing
title: Cách sử dụng OCR trong Python – hướng dẫn từng bước
url: /vi/python/general/how-to-use-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong Python – hướng dẫn từng bước

Nếu bạn cần **how to use OCR** để chuyển đổi tài liệu đã quét hoặc ảnh chụp màn hình thành văn bản có thể chỉnh sửa, hướng dẫn này cung cấp giải pháp hoàn chỉnh bằng Python. Bạn sẽ học cách nhận dạng văn bản từ hình ảnh, trích xuất văn bản từ hình ảnh, chuyển hình ảnh thành văn bản và làm sạch văn bản OCR bằng một bộ xử lý hậu xử lý AI nhẹ.

Hướng dẫn bao gồm mọi thứ từ cài đặt các thư viện cần thiết đến xử lý hình ảnh chất lượng thấp, giúp bạn tích hợp OCR vào bất kỳ quy trình tự động nào mà không phải đoán bước nào còn thiếu.

## Những gì bạn sẽ xây dựng

1. Tải một tệp hình ảnh (PNG, JPEG hoặc TIFF).  
2. Nhận dạng văn bản từ hình ảnh bằng công cụ OCR.  
3. Cải thiện đầu ra thô bằng bộ xử lý hậu xử lý dựa trên AI.  
4. In văn bản đã được làm sạch ra console.

Không cần dịch vụ bên ngoài—mọi thứ chạy cục bộ, làm cho giải pháp phù hợp với môi trường offline hoặc các dự án nhạy cảm về quyền riêng tư.

## Yêu cầu trước

- Python 3.9 hoặc mới hơn.  
- `pytesseract` và `Pillow` libraries (`pip install pytesseract pillow`).  
- Binary Tesseract‑OCR đã được cài đặt và có sẵn trong `PATH` của hệ thống.  
- Kiến thức cơ bản về hàm trong Python.  

Nếu bạn đã có những mục này, bạn có thể chuyển thẳng tới khối mã đầu tiên.

## Cách sử dụng OCR với Python

Cốt lõi của **how to use OCR** là khởi tạo công cụ OCR và cung cấp cho nó một hình ảnh. Trong hướng dẫn này, chúng ta sử dụng `pytesseract`, một lớp bao bọc nhẹ quanh công cụ mã nguồn mở Tesseract.

```python
import pytesseract
from PIL import Image

def load_image(path: str) -> Image.Image:
    """
    Open an image file and return a Pillow Image object.
    Pillow handles many formats (PNG, JPEG, TIFF) and ensures
    the image is in a mode that Tesseract can read.
    """
    return Image.open(path)
```

> **Tại sao bước này quan trọng** – Tesseract yêu cầu một hình ảnh sạch, được định hướng đúng. Sử dụng Pillow đảm bảo dữ liệu hình ảnh được chuẩn hoá trước khi OCR chạy, giúp cải thiện độ chính xác của thao tác **recognize text from image** tiếp theo.

## Nhận dạng văn bản từ hình ảnh

Bây giờ chúng ta gọi `pytesseract.image_to_string` để trích xuất chuỗi thô. Đây là lời gọi truyền thống “recognize text from image”.

```python
def ocr_recognize(image: Image.Image) -> str:
    """
    Run Tesseract OCR on the supplied image and return the raw text.
    """
    raw_text = pytesseract.image_to_string(image, lang='eng')
    return raw_text
```

> **Tại sao chúng ta tách hàm này** – Tách riêng bước OCR cho phép bạn thay đổi công cụ sau này (ví dụ, chuyển sang EasyOCR) mà không ảnh hưởng đến phần còn lại của quy trình. Nó cũng giúp việc kiểm thử đơn vị dễ dàng hơn.

## Trích xuất văn bản từ hình ảnh và cải thiện chất lượng

Kết quả OCR thô thường chứa các ngắt dòng, ký tự lẻ, hoặc từ bị nhận dạng sai. Một bộ xử lý hậu xử lý AI có thể tự động làm sạch các hiện tượng này. Dưới đây là một ví dụ tối thiểu sử dụng thư viện `transformers` để chạy một mô hình ngôn ngữ nhỏ cục bộ. Bạn có thể thay thế bằng bất kỳ dịch vụ độc quyền nào nếu muốn.

```python
from transformers import pipeline

# Initialize a zero‑shot text‑generation pipeline once (expensive operation)
_ai_postprocessor = pipeline("text2text-generation", model="google/flan-t5-small")

def clean_ocr_text(raw: str) -> str:
    """
    Send the raw OCR string to a lightweight AI model that rewrites
    the text, removing obvious errors and normalizing whitespace.
    """
    # The prompt guides the model to act as a post‑processor
    prompt = f"Clean up the following OCR output, fixing spelling mistakes and removing extra line breaks:\n\n{raw}"
    result = _ai_postprocessor(prompt, max_length=512, do_sample=False)
    # The pipeline returns a list of dicts; we take the generated text
    cleaned = result[0]["generated_text"]
    return cleaned.strip()
```

> **Tại sao bộ xử lý hậu xử lý AI lại hữu ích** – Các công cụ OCR truyền thống giỏi trong việc nhận dạng ký tự nhưng gặp khó khăn với bố cục và nhiễu. Một mô hình ngôn ngữ hiểu ngữ cảnh, vì vậy nó có thể chuyển “Th1s 1s 4 test.” thành “This is a test.” Bước này trực tiếp đáp ứng yêu cầu **clean up OCR text**.

## Chuyển hình ảnh thành văn bản – script đầy đủ

Kết hợp mọi thứ lại với nhau tạo ra một script ngắn thực hiện **convert image to text** từ đầu đến cuối.

```python
import sys
from pathlib import Path

def main(image_path: str):
    """
    Complete pipeline:
    1. Load image.
    2. Recognize text from image.
    3. Clean up OCR text.
    4. Print the final result.
    """
    # 1️⃣ Load the image file
    img = load_image(image_path)

    # 2️⃣ Recognize text from image (raw OCR)
    raw_text = ocr_recognize(img)
    print("=== Raw OCR output ===")
    print(raw_text)
    print("\n---\n")

    # 3️⃣ Clean up OCR text with AI post‑processor
    cleaned_text = clean_ocr_text(raw_text)
    print("=== Cleaned‑up text ===")
    print(cleaned_text)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python ocr_pipeline.py <path-to-image>")
        sys.exit(1)

    image_file = Path(sys.argv[1])
    if not image_file.is_file():
        print(f"Error: file '{image_file}' does not exist.")
        sys.exit(1)

    main(str(image_file))
```

### Kết quả mong đợi

Chạy script với một hình ảnh mẫu (`sample.png`) có thể tạo ra:

```
=== Raw OCR output ===
Th1s 1s 4 sampl3
text from an im4ge.

--- 

=== Cleaned‑up text ===
This is a sample text from an image.
```

Chú ý cách bộ xử lý hậu xử lý AI đã sửa các ký tự đọc sai và loại bỏ ngắt dòng lẻ. Điều này minh họa quy trình **extract text from image** đầy đủ và cho thấy lợi ích của việc làm sạch văn bản OCR.

## Xử lý các trường hợp góc cạnh thường gặp

| Tình huống                              | Điều chỉnh đề xuất                                                               |
|----------------------------------------|---------------------------------------------------------------------------------|
| Hình ảnh độ tương phản thấp            | Chuyển sang ảnh xám và tăng độ tương phản bằng `ImageEnhance` trước khi OCR.    |
| Tài liệu đa ngôn ngữ                  | Cung cấp danh sách ngăn cách bằng dấu phẩy cho `lang` (ví dụ, `lang='eng+fra'`). |
| Hình ảnh rất lớn ( > 2000 px )         | Giảm kích thước bằng `img.thumbnail((2000, 2000))` để tăng tốc Tesseract.      |
| Thiếu binary Tesseract                | Kiểm tra `pytesseract.pytesseract.tesseract_cmd` trỏ tới tệp thực thi.         |
| Bộ xử lý AI quá chậm                   | Sử dụng mô hình nhỏ hơn (`t5-small`) hoặc chạy bộ xử lý trên GPU.               |

> **Mẹo chuyên nghiệp:** Lưu trữ đối tượng mô hình AI (`_ai_postprocessor`) khi import module, như đã minh họa, để tránh tải lại mỗi lần gọi. Điều này giảm độ trễ đáng kể khi xử lý nhiều hình ảnh.

## Các cách tiếp cận thay thế

- **EasyOCR**: Thư viện OCR thuần Python hỗ trợ hơn 80 ngôn ngữ mà không cần binary bên ngoài. Thay thế `ocr_recognize` bằng `EasyOCR.Reader` nếu bạn muốn giải pháp chỉ dùng pip.  
- **Cloud OCR APIs**: Google Cloud Vision, Azure Computer Vision, hoặc Amazon Textract cung cấp độ chính xác cao hơn cho bố cục phức tạp nhưng yêu cầu truy cập mạng và thanh toán.  
- **Custom post‑processing**: Đối với việc làm sạch quyết định, biểu thức chính quy (`re.sub`) có thể sửa các mẫu phổ biến (ví dụ, loại bỏ ngắt dòng có dấu gạch nối) mà không cần mô hình AI.

## Tóm tắt

Bây giờ bạn đã biết **cách sử dụng OCR** trong Python để nhận dạng văn bản từ hình ảnh, trích xuất văn bản từ hình ảnh, chuyển hình ảnh thành văn bản và làm sạch văn bản OCR bằng bộ xử lý hậu xử lý AI. Script hoàn chỉnh minh họa một pipeline sẵn sàng cho sản xuất mà bạn có thể mở rộng với các bước tiền xử lý bổ sung (giảm nhiễu, chỉnh góc) hoặc các hành động tiếp theo (lưu vào cơ sở dữ liệu, đưa vào chỉ mục tìm kiếm).

### Các bước tiếp theo

- Thử nghiệm các mô hình AI khác nhau (ví dụ, `gpt‑2`, `flan‑ul2`) để xem mô hình nào cung cấp việc làm sạch tốt nhất cho lĩnh vực của bạn.  
- Tích hợp pipeline vào dịch vụ web bằng Flask hoặc FastAPI, biến script thành endpoint OCR theo yêu cầu.  
- Khám phá xử lý hàng loạt: lặp qua một thư mục hình ảnh và ghi mỗi kết quả đã làm sạch vào tệp `.txt` tương ứng.

Bạn có thể tự do điều chỉnh mã cho quy trình làm việc cụ thể của mình, và để văn bản sạch, có thể tìm kiếm giúp nâng cao giai đoạn tiếp theo của ứng dụng. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Chuyển Hình Ảnh thành Văn Bản: Trích xuất Văn bản từ Hình ảnh bằng Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích xuất Văn bản từ Hình ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}