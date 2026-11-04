---
category: general
date: 2026-08-12
description: Chạy OCR trên hình ảnh bằng Python và Aspose AI để trích xuất văn bản
  từ hình ảnh và cải thiện độ chính xác của OCR bằng bộ xử lý hậu kỳ kiểm tra chính
  tả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: vi
lastmod: 2026-08-12
og_description: Chạy OCR trên hình ảnh bằng Python và ngay lập tức trích xuất văn
  bản từ hình ảnh đồng thời cải thiện độ chính xác của OCR bằng xử lý hậu kỳ AI của
  Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Chạy OCR trên hình ảnh bằng Python – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Chạy OCR trên hình ảnh bằng Python – hướng dẫn từng bước
url: /vi/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên hình ảnh với Python – hướng dẫn từng bước

Nếu bạn cần **run OCR on image** các tệp trong Python, hướng dẫn này sẽ đưa bạn qua toàn bộ quy trình. Bạn sẽ học cách **extract text from image**, áp dụng **OCR text correction**, và **improve OCR accuracy** chỉ với vài dòng mã.

Xử lý các tài liệu đã quét, biên lai hoặc ảnh chụp màn hình thường tạo ra văn bản nhiễu. Bằng cách gắn một bộ xử lý hậu xử lý kiểm tra chính tả, bạn có thể biến đầu ra OCR thô thành nội dung sạch, có thể tìm kiếm được mà không cần chuyển sang công cụ riêng. Bài hướng dẫn này bao gồm mọi thứ bạn cần—từ việc tải hình ảnh đến hiển thị kết quả đã chỉnh sửa.

## Yêu cầu trước

* Python 3.9 hoặc mới hơn đã được cài đặt.
* Truy cập vào các gói Python Aspose.OCR và Aspose.AI (hoặc các wrapper mã nguồn mở tương đương).
* Một hình ảnh mẫu (ví dụ, `sample.png`) được đặt trong thư mục đã biết.
* Kiến thức cơ bản về các hàm Python và mã hướng đối tượng.

Bạn có thể cài đặt các thư viện cần thiết bằng pip:

```bash
pip install aspose-ocr aspose-ai
```

> **Mẹo:** Sử dụng môi trường ảo (`python -m venv .venv`) để giữ các phụ thuộc riêng biệt.

## Bước 1: Run OCR on image – tạo thể hiện engine

Bước đầu tiên là tạo một đối tượng `OcrEngine`. Đối tượng này bao bọc cấu hình của engine OCR và cung cấp các phương thức để xử lý và nhận dạng hình ảnh.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Tạo engine một lần và tái sử dụng nó cho nhiều hình ảnh sẽ giảm chi phí khởi động và đảm bảo các cài đặt nhất quán trong suốt phiên làm việc.

## Bước 2: Load image for OCR

Trước khi nhận dạng có thể diễn ra, engine phải biết hình ảnh nào sẽ được phân tích. Phương thức `load_image` chấp nhận đường dẫn tệp hoặc luồng nhị phân.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Tại sao điều này quan trọng:** Việc tải hình ảnh đúng cách là nền tảng cho OCR chính xác. Cung cấp hình ảnh độ phân giải cao (≥300 dpi) thường **improves OCR accuracy** vì engine có thể phân biệt ký tự rõ ràng hơn.

## Bước 3: Extract text from image – thực hiện nhận dạng cơ bản

Sau khi hình ảnh đã được tải, bạn có thể gọi `recognize()` để nhận được một đối tượng kết quả. Kết quả chứa văn bản thô, điểm tin cậy, và tùy chọn các hộp bao quanh cho mỗi từ.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

Ở thời điểm này, bạn đã thành công **run OCR on image** và trích xuất các ký tự thô. Tuy nhiên, văn bản có thể chứa lỗi chính tả, đặc biệt với các bản quét chất lượng thấp.

## Bước 4: OCR text correction – gắn bộ kiểm tra chính tả hậu xử lý

Aspose AI cung cấp một pipeline hậu xử lý linh hoạt. Bằng cách tích hợp một bộ kiểm tra chính tả tùy chỉnh, bạn có thể sửa các lỗi OCR thường gặp (ví dụ, “l” vs. “1”, “O” vs. “0”).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Cách hoạt động của spell‑checker:** `MySpellChecker` nên triển khai một phương thức `process(text: str) -> str`. Bên trong, bạn có thể sử dụng các thư viện như `pyspellchecker` hoặc `symspellpy` để thay thế các chuỗi từ không hợp lý bằng các lựa chọn đã được từ điển xác thực.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Bước 5: Display original and corrected OCR text

Cuối cùng, so sánh đầu ra thô và đã chỉnh sửa. Điều này giúp bạn xác nhận rằng **OCR text correction** thực sự **improved OCR accuracy** cho trường hợp sử dụng của bạn.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Kết quả mong đợi

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

Dòng đã chỉnh sửa cho thấy spell‑checker đã thay thế các nhận dạng sai thường gặp của OCR (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Bước 6: Improve OCR accuracy – danh sách kiểm tra thực hành tốt

Ngay cả khi đã có hậu xử lý, bạn vẫn có thể tăng chất lượng cơ bản của engine OCR:

| Checklist item | Why it helps |
|----------------|--------------|
| **Sử dụng hình ảnh độ phân giải cao (≥300 dpi)** | Nhiều dữ liệu pixel hơn giảm sự mơ hồ của ký tự. |
| **Chuyển đổi hình ảnh màu sang thang xám** | Loại bỏ nhiễu màu có thể làm rối engine. |
| **Áp dụng chỉnh nghiêng hình ảnh** | Cân chỉnh văn bản nghiêng, ngăn ngừa lỗi ngắt dòng. |
| **Đặt ngôn ngữ/khu vực một cách rõ ràng** | Hướng dẫn bộ nhận dạng tới bộ ký tự đúng. |
| **Bật mô hình ngôn ngữ** (if the library supports it) | Cung cấp dự đoán dựa trên ngữ cảnh, tiếp tục **improving OCR accuracy**. |

Bạn có thể thực hiện các bước tiền xử lý này bằng Pillow hoặc OpenCV trước khi đưa hình ảnh vào `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Kịch bản đầy đủ có thể chạy

Kết hợp mọi thứ lại, đoạn script sau đã sẵn sàng để sao chép‑dán vào tệp có tên `run_ocr.py` và thực thi.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Chạy script sẽ in ra văn bản gốc và đã chỉnh sửa, xác nhận rằng bạn đã thành công **run OCR on image**, **extracted text from image**, và **improved OCR accuracy** thông qua **OCR text correction**.

## Kết luận

Bây giờ bạn đã biết cách **run OCR on image** các tệp trong Python, trích xuất văn bản thô, và áp dụng bộ kiểm tra chính tả hậu xử lý để đạt được kết quả sạch hơn. Bằng cách tuân theo danh sách kiểm tra để **improve OCR accuracy**, bạn có thể áp dụng quy trình này cho biên lai, hoá đơn, thẻ ID, hoặc bất kỳ tài liệu quét nào.

### Tiếp theo là gì?

* Khám phá **language‑specific dictionaries** cho OCR đa ngôn ngữ.
* Tích hợp pipeline với cơ sở dữ liệu hoặc chỉ mục tìm kiếm (ví dụ, Elasticsearch) để làm cho văn bản đã trích xuất có thể tìm kiếm được.
* Thay thế bộ kiểm tra chính tả đơn giản bằng mô hình ngôn ngữ neural (ví dụ, sửa chữa dựa trên GPT) để đạt độ chính xác cao hơn.

Bạn có thể thoải mái thử nghiệm các kỹ thuật tiền xử lý hình ảnh khác nhau, các bộ hậu xử lý khác nhau, hoặc các engine OCR thay thế. Mẫu cốt lõi—**run OCR on image → extract text from image → OCR text correction → improve OCR accuracy**—vẫn không thay đổi, cung cấp cho bạn nền tảng vững chắc cho bất kỳ dự án số hoá tài liệu nào.

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Chuyển đổi hình ảnh thành văn bản: Trích xuất văn bản từ hình ảnh bằng Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Trích xuất văn bản từ hình ảnh với Aspose OCR – Hướng dẫn từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích xuất văn bản từ hình ảnh – Tối ưu hoá OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}