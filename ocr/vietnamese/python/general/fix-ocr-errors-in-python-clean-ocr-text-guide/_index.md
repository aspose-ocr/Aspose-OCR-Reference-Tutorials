---
category: general
date: 2026-03-18
description: Sửa lỗi OCR trong Python nhanh chóng. Tìm hiểu cách làm sạch OCR, cách
  làm sạch văn bản OCR, thay thế số 0 bằng O và áp dụng xử lý hậu kỳ OCR bằng Python.
draft: false
keywords:
- fix OCR errors
- how to clean OCR
- clean OCR text python
- replace zero with O
- python OCR post processing
language: vi
og_description: Sửa lỗi OCR trong Python nhanh chóng. Tìm hiểu cách làm sạch OCR,
  thay thế số 0 bằng O và sử dụng xử lý hậu OCR bằng Python trong một hướng dẫn duy
  nhất.
og_title: Sửa lỗi OCR trong Python – Hướng dẫn làm sạch văn bản OCR
tags:
- OCR
- Python
- Text Cleaning
title: Sửa lỗi OCR trong Python – Hướng dẫn làm sạch văn bản OCR
url: /vi/python/general/fix-ocr-errors-in-python-clean-ocr-text-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Sửa lỗi OCR trong Python – Hướng dẫn làm sạch văn bản OCR

Bạn đã bao giờ nhìn vào một hoá đơn đã quét và nghĩ, *“Làm sao tôi có thể sửa lỗi OCR trước khi đưa vào cơ sở dữ liệu?”* Bạn không phải là người duy nhất. Trong thế giới tự động hoá tài liệu, một ký tự bị đọc sai có thể làm hỏng toàn bộ pipeline, vì vậy việc học **how to clean OCR** output là rất cần thiết.  

Trong tutorial này, bạn sẽ thấy một cách thực tế, end‑to‑end để **fix OCR errors** bằng cách sử dụng một post‑processor nhỏ thay thế chữ số “0” bằng chữ “O”—một lỗi thường gặp trong mã sản phẩm. Khi hoàn thành, bạn sẽ có thể tích hợp giải pháp này vào bất kỳ workflow OCR nào bằng Python và có được văn bản sạch hơn, đáng tin cậy hơn.

> **What you’ll get:** một script Python hoàn chỉnh, có thể chạy được, giải thích lý do mỗi dòng quan trọng, mẹo mở rộng logic, và một kiểm tra nhanh tính hợp lý của output mong đợi.

## Prerequisites — Những gì bạn cần trước khi bắt đầu

- Python 3.8 hoặc mới hơn (cú pháp hoạt động trên tất cả các phiên bản gần đây).  
- Thư viện OCR cơ bản (ví dụ: Tesseract qua `pytesseract`) trả về chuỗi thô.  
- Kiến thức cơ bản về hàm và đối tượng trong Python.  

Nếu bạn đã có một bước OCR trả về một chuỗi, bạn đã sẵn sàng—không cần cài đặt thêm cho phần post‑processing.

## Bước 1: Thiết lập một Wrapper kiểu AI tối thiểu (Tại sao chúng ta cần nó)

Trong nhiều dự án, engine OCR nằm trong một lớp “AI” lớn hơn, chịu trách nhiệm preprocessing, inference và post‑processing. Để giữ ví dụ tự chứa, chúng ta sẽ tạo một lớp `AIProcessor` nhỏ mô phỏng mẫu này. Điều này giúp dễ dàng chèn code vào code‑base hiện có mà không cần viết lại bất kỳ gì.

```python
# ai_wrapper.py
class AIProcessor:
    """
    Simple wrapper that stores a post‑processing callable.
    In real projects this could be a full‑fledged model class.
    """
    def __init__(self):
        self._post_processor = None

    def set_post_processor(self, func):
        """Register a function that will clean OCR output."""
        if not callable(func):
            raise TypeError("Post‑processor must be callable")
        self._post_processor = func

    def run_postprocessor(self, text):
        """Apply the registered post‑processor to raw OCR text."""
        if self._post_processor is None:
            raise RuntimeError("No post‑processor has been set")
        return self._post_processor(text)
```

**Why this matters:** việc giữ post‑processor tách biệt khỏi engine OCR tuân theo nguyên tắc single‑responsibility và cho phép bạn thay đổi logic làm sạch mà không chạm vào code OCR.

## Bước 2: Viết hàm **Fixes OCR Errors**

Bây giờ chúng ta tạo phần cốt lõi của tutorial: một hàm **fixes OCR errors** bằng cách thay thế số “0” bằng chữ “O”. Mẫu này áp dụng cho mã sản phẩm, số serial, và bất kỳ định danh alphanumeric nào mà engine OCR thường nhầm lẫn hai ký tự này.

```python
# post_processors.py
def correct_ocr_errors(text: str) -> str:
    """
    Replace common OCR mis‑reads.
    Example: change digit "0" to letter "O" in product codes.
    """
    # You could add more rules here, e.g.:
    # text = text.replace('1', 'I')
    # text = text.replace('5', 'S')
    return text.replace("0", "O")
```

**Why we replace 0 with O:** Trong nhiều phông chữ, số 0 và chữ O in hoa trông giống hệt nhau, vì vậy OCR thường đoán nhầm. Khi sửa sớm, việc xác thực downstream (như kiểm tra regex) sẽ hoạt động như mong muốn.

## Bước 3: Kết nối Post‑Processor vào Instance AI

Với wrapper và hàm làm sạch đã sẵn sàng, chúng ta gắn chúng lại với nhau. Điều này mô phỏng cách bạn đăng ký một post‑processor tùy chỉnh trong pipeline sản xuất.

```python
# main.py
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Create the AI‑like object
ai = AIProcessor()

# Register our OCR‑fixing function
ai.set_post_processor(correct_ocr_errors)
```

Nếu bạn cần **how to clean OCR** output cho ngôn ngữ hoặc định dạng dữ liệu khác, chỉ cần viết một hàm khác và gọi `set_post_processor` lại—không cần chạm vào phần còn lại của pipeline.

## Bước 4: Cung cấp văn bản OCR thô và nhận kết quả đã làm sạch

Hãy mô phỏng một chuỗi OCR thô chứa ký tự “0” đáng sợ trong mã sản phẩm. Trong thực tế, bạn sẽ thay thế placeholder bằng `pytesseract.image_to_string(image)` hoặc một lời gọi tương tự.

```python
# Simulated OCR output (replace with your own OCR call)
raw_text = "Product code: 10A0B"

# Run the post‑processor to obtain cleaned text
cleaned_text = ai.run_postprocessor(raw_text)

print("Before cleaning :", raw_text)
print("After cleaning  :", cleaned_text)
```

**Expected output**

```
Before cleaning : Product code: 10A0B
After cleaning  : Product code: 1OAOB
```

Chú ý cách các số 0 đã biến thành chữ O in hoa, cho chúng ta một chuỗi phù hợp với định dạng mong đợi của hầu hết hệ thống quản lý tồn kho.

## Bước 5: Mở rộng Logic – Các biến thể thực tế

Việc thay thế đơn giản ở trên giải quyết một trường hợp hẹp, nhưng trong sản xuất bạn sẽ gặp các quirks khác:

| Lỗi thường gặp | Ví dụ OCR | Sửa mong muốn | Cách thêm |
|----------------|------------|-------------|------------|
| “1” đọc thành “I” | `I23` | `123` | `text = text.replace('I', '1')` |
| “5” đọc thành “S” | `S9` | `59` | `text = text.replace('S', '5')` |
| Khoảng trắng thừa | `  ABC  ` | `ABC` | `text = text.strip()` |
| Nhầm lẫn chữ hoa/thường | `oRder` | `Order` | `text = text.title()` |

```python
def correct_ocr_errors(text: str) -> str:
    text = text.replace("0", "O")
    text = text.replace("I", "1")
    text = text.replace("S", "5")
    return text.strip()
```

**Pro tip:** Nếu bạn có danh mục mã hợp lệ đã biết, hãy cân nhắc xác thực chuỗi đã làm sạch bằng regex hoặc bảng tra cứu. Bước bổ sung này sẽ bắt bất kỳ lỗi OCR còn lại mà việc thay thế ký tự đơn giản không phát hiện.

## Bước 6: Tích hợp với Engine OCR thực tế (Tùy chọn)

Dưới đây là một minh họa nhanh về cách bạn sẽ chèn post‑processor vào luồng OCR thực tế bằng `pytesseract`. Phần này là tùy chọn nhưng cho thấy pipeline end‑to‑end.

```python
import pytesseract
from PIL import Image
from ai_wrapper import AIProcessor
from post_processors import correct_ocr_errors

# Initialize AI wrapper and register the cleaner
ai = AIProcessor()
ai.set_post_processor(correct_ocr_errors)

# Load an image containing a product label
image = Image.open("sample_label.png")

# Perform OCR (this returns raw text)
raw_ocr = pytesseract.image_to_string(image)

# Clean the OCR output
cleaned = ai.run_postprocessor(raw_ocr)

print("Raw OCR   :", raw_ocr)
print("Cleaned   :", cleaned)
```

> **Note:** `pytesseract` yêu cầu Tesseract OCR được cài đặt trên hệ thống của bạn. Đoạn mã trên hoạt động trên Windows, macOS và Linux miễn là binary nằm trong PATH của bạn.

## Bước 7: Xác minh Kết quả bằng chương trình

Khi bạn tự động hoá các lô lớn, việc khẳng định bước làm sạch hoạt động như mong đợi là rất tiện lợi. Một unit test nhanh có thể tiết kiệm hàng giờ debug sau này.

```python
def test_correct_ocr_errors():
    assert correct_ocr_errors("0O0") == "OOO"
    assert correct_ocr_errors(" 10A0B ") == "1OAOB"
    print("All tests passed!")

test_correct_ocr_errors()
```

Chạy test này xác nhận rằng hàm **fixes OCR errors** một cách nhất quán, ngay cả khi có thêm khoảng trắng.

## Hình minh họa

Dưới đây là một bản phác thảo trực quan của pipeline (từ khóa chính xuất hiện trong alt text để SEO).

![Sơ đồ pipeline sửa lỗi OCR – hiển thị OCR thô đưa vào post‑processor thay thế số 0 bằng O]()

## Kết luận – Những gì chúng ta đã đạt được

Chúng ta đã đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **how to clean OCR** output trong Python, cụ thể là cách **replace zero with O** và **fix OCR errors** bằng một post‑processor mô-đun. Bằng cách tách logic làm sạch khỏi engine OCR, bạn có được tính linh hoạt, khả năng kiểm thử và một vị trí rõ ràng để thêm các quy tắc trong tương lai như *how to clean OCR* cho các nhầm lẫn ký tự khác.

Sẵn sàng cho bước tiếp theo? Hãy thử thêm một validator regex cho mã sản phẩm, thử nghiệm fuzzy matching cho văn bản nhiễu, hoặc khám phá thư viện đầy đủ tính năng như `ocrmypdf` đã tích hợp sẵn các hook post‑processing. Mẫu chúng ta đã đề cập mở rộng tốt, dù bạn xử lý vài hoá đơn hay hàng triệu tài liệu đã quét.

---

*Chúc lập trình vui vẻ, và hy vọng pipeline OCR của bạn luôn không lỗi!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}