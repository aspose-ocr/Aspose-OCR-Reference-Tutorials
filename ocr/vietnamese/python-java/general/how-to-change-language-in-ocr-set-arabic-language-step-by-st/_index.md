---
category: general
date: 2026-06-22
description: Cách thay đổi ngôn ngữ trong các công cụ OCR một cách nhanh chóng. Học
  cách thiết lập ngôn ngữ OCR tiếng Ả Rập (ar) bằng mã đơn giản và tránh các lỗi thường
  gặp.
draft: false
keywords:
- how to change language
- ocr language arabic
- how to set OCR
- change OCR language
- set language OCR
language: vi
og_description: Cách thay đổi ngôn ngữ trong các công cụ OCR được giải thích trong
  câu đầu tiên. Hãy làm theo hướng dẫn này để nhanh chóng thiết lập ngôn ngữ OCR tiếng
  Ả Rập.
og_title: Cách Thay Đổi Ngôn Ngữ trong OCR – Hướng Dẫn Toàn Diện
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  headline: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  type: TechArticle
- description: How to change language in OCR engines quickly. Learn to set Arabic
    (ar) OCR language using simple code and avoid common pitfalls.
  name: How to Change Language in OCR – Set Arabic Language Step‑by‑Step
  steps:
  - name: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
    text: '**Grab the OCR engine instance** – this is usually a singleton or a factory‑created
      object.'
  - name: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
    text: '**Pull the settings object** – most libraries keep language, DPI, and other
      options in a separate config container.'
  - name: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
    text: '**Set the language code** – for Arabic the ISO‑639‑2 code is `"ar"`.'
  type: HowTo
tags:
- OCR
- multilingual
- programming
title: Cách Thay Đổi Ngôn Ngữ trong OCR – Cài Đặt Ngôn Ngữ Ả Rập Bước‑Theo‑Bước
url: /vi/python-java/general/how-to-change-language-in-ocr-set-arabic-language-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thay Đổi Ngôn Ngữ trong OCR – Hướng Dẫn Lập Trình Toàn Diện

Cách thay đổi ngôn ngữ trong các engine OCR là một rào cản thường gặp khi bạn bắt đầu làm việc với tài liệu đa ngôn ngữ. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn từng bước để thiết lập ngôn ngữ OCR sang tiếng Ả Rập, kèm theo một mẫu mã có thể chạy được và giải thích cho mỗi dòng. Nếu bạn từng tự hỏi *“làm sao để đặt OCR* sang một script khác mà không làm hỏng pipeline*, bạn đang ở đúng nơi*.

Chúng tôi sẽ bao phủ mọi thứ bạn cần: các thư viện bắt buộc, cách lấy thể hiện của engine OCR, cách truy cập vào cài đặt của nó, và cuối cùng là cách thay đổi ngôn ngữ OCR một cách an toàn. Khi kết thúc, bạn sẽ có thể chuyển từ tiếng Anh sang tiếng Ả Rập (hoặc bất kỳ ngôn ngữ nào được hỗ trợ) chỉ bằng một lời gọi phương thức. Không có ma thuật, chỉ có mã rõ ràng và một vài mẹo thực tiễn.

## Yêu Cầu Trước

- Python 3.8+ (hoặc bất kỳ phiên bản gần đây nào)
- Thư viện OCR cung cấp một đối tượng settings – ví dụ sử dụng **pytesseract** được bọc trong một lớp trợ giúp nhỏ, nhưng cùng một mẫu sẽ hoạt động với các engine khác như EasyOCR hoặc Microsoft Computer Vision SDK.
- Dữ liệu ngôn ngữ tiếng Ả Rập đã được cài đặt cho engine OCR (`ara.traineddata` cho Tesseract).  
  *Mẹo:* trên Ubuntu bạn có thể cài đặt bằng `sudo apt-get install tesseract-ocr-ara`.

## Cách Thay Đổi Ngôn Ngữ trong OCR – Tổng Quan

Thay đổi ngôn ngữ thực chất là một quy trình ba bước:

1. **Lấy thể hiện của engine OCR** – thường là một singleton hoặc một đối tượng được tạo bởi factory.
2. **Lấy đối tượng settings** – hầu hết các thư viện lưu ngôn ngữ, DPI và các tùy chọn khác trong một container cấu hình riêng.
3. **Đặt mã ngôn ngữ** – đối với tiếng Ả Rập, mã ISO‑639‑2 là `"ar"`.

Dưới đây là một script tối thiểu, có thể chạy đầy đủ, minh họa các bước trên.

![How to change language in OCR screenshot](image-placeholder.png "How to change language in OCR example")

## Bước 1: Tạo Hoặc Lấy Thể Hiện Engine OCR

Đầu tiên chúng ta cần một engine. Trong các dự án thực tế, engine có thể được tạo ở nơi khác và truyền qua lại; để rõ ràng, chúng ta sẽ khởi tạo ngay tại đây.

```python
# step1_engine.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    """A thin wrapper around pytesseract to expose a settings object."""
    def __init__(self):
        # pytesseract itself doesn't expose a mutable settings object,
        # so we store options in a dict that we later pass to image_to_string().
        self._options = {"lang": "eng"}  # default to English

    def get_settings(self):
        """Return a Settings object that can modify OCR options."""
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        """Run OCR on the given image using current options."""
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        """Convert the internal options dict to a Tesseract command line."""
        # Example: '-l eng' or '-l ar+eng' for multiple languages
        lang_option = self._options.get("lang", "eng")
        return f"-l {lang_option}"
```

**Tại sao chúng ta bọc engine** – nhiều SDK OCR (bao gồm Tesseract) yêu cầu ngôn ngữ được truyền dưới dạng chuỗi mỗi lần gọi. Bằng cách đóng gói các tùy chọn trong một đối tượng settings, chúng ta có được một API sạch sẽ, *how to set OCR*‑style, phản ánh đoạn mã gốc mà bạn đã cung cấp.

## Bước 2: Truy Cập Đối Tượng Settings Của Engine

Bây giờ chúng ta đã có engine, chúng ta lấy cài đặt của nó. Điều này phản chiếu dòng thứ hai của ví dụ gốc (`settings = engine.get_settings()`).

```python
# step2_settings.py
class OcrSettings:
    """Provides getters and setters for OCR configuration."""
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        """
        Change OCR language.
        :param lang_code: ISO‑639‑2 language code, e.g., 'ar' for Arabic.
        """
        # Validate the language code – a tiny safety net.
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        """Return the currently configured language code."""
        return self._engine._options.get("lang", "eng")
```

Ở đây chúng ta cung cấp **how to set OCR** ngôn ngữ qua `set_language`. Phương thức này cũng thực hiện một kiểm tra cơ bản, là một thói quen lập trình phòng thủ tốt.

## Bước 3: Đặt Ngôn Ngữ OCR Thành Tiếng Ả Rập (ocr language arabic)

Cuối cùng chúng ta gọi phương thức với mã tiếng Ả Rập `"ar"`. Đây là phần cốt lõi của thao tác *change OCR language*.

```python
# step3_change_language.py
from step1_engine import SimpleOCREngine

# Obtain the OCR engine instance (could be a singleton in a larger app)
engine = SimpleOCREngine()

# Access the settings object
settings = engine.get_settings()

# Set the OCR language to Arabic – this is the "how to change language" line.
settings.set_language("ar")

# Optional: verify the change
print("Current OCR language:", settings.get_language())

# Run OCR on a sample Arabic image (replace with your own path)
# result = engine.recognize("sample_arabic.png")
# print("OCR Output:", result)
```

**Kết quả mong đợi**

```
Current OCR language: ar
```

Nếu bạn bỏ comment dòng `recognize` và trỏ nó tới một hình ảnh tiếng Ả Rập thực, bạn sẽ thấy các ký tự tiếng Ả Rập được in ra console (miễn là dữ liệu ngôn ngữ đã được cài đặt).

## Cách Đặt OCR Cho Nhiều Ngôn Ngữ

Đôi khi bạn cần *ocr language arabic* **cộng** tiếng Anh, đặc biệt cho tài liệu hỗn hợp. Phương thức `set_language` có thể nhận một danh sách ngăn cách bằng `+`:

```python
settings.set_language("ar+eng")
print("Now recognizing both Arabic and English:", settings.get_language())
```

*Trường hợp đặc biệt*: Nếu gói ngôn ngữ yêu cầu chưa được cài đặt, Tesseract sẽ ném lỗi như `Error opening language file`. Để tránh crash, bạn có thể bắt ngoại lệ và quay lại ngôn ngữ mặc định.

```python
try:
    settings.set_language("ar")
except Exception as e:
    print("Failed to set Arabic language:", e)
    settings.set_language("eng")  # fallback
```

## Thay Đổi Ngôn Ngữ OCR Một Cách Động Khi Chạy

Trong nhiều ứng dụng, người dùng chọn ngôn ngữ từ một dropdown. Vì các cài đặt nằm trong đối tượng engine, bạn có thể chuyển ngôn ngữ ngay lập tức mà không cần tạo lại engine.

```python
def switch_language(lang_code: str):
    settings.set_language(lang_code)
    print(f"OCR language switched to {lang_code}")

# Example usage:
switch_language("fr")   # switch to French
switch_language("ar")   # back to Arabic
```

Mẫu này đáp ứng yêu cầu *set language OCR* đồng thời giữ cho mã gọn gàng.

## Những Rủi Ro Phổ Biến và Mẹo Chuyên Nghiệp

| Rủi ro | Điều Gì Xảy Ra | Cách Khắc Phục |
|--------|----------------|----------------|
| Thiếu gói ngôn ngữ | Tesseract trả về “Failed loading language ‘ar’” | Cài đặt dữ liệu ngôn ngữ (`sudo apt-get install tesseract-ocr-ara` hoặc tải về từ repo). |
| Sử dụng mã ISO sai | Không có đầu ra hoặc ký tự bị rối | Kiểm tra lại mã (`ar` cho tiếng Ả Rập, `eng` cho tiếng Anh, `chi_sim` cho tiếng Trung giản thể). |
| Quên xây dựng lại cấu hình | Engine vẫn dùng ngôn ngữ cũ | Luôn gọi `engine._build_config()` (được xử lý nội bộ khi bạn gọi `recognize`). |
| Truyền danh sách thay vì chuỗi | TypeError | Dùng `"ar+eng"` dưới dạng một chuỗi duy nhất, không phải `["ar", "eng"]`. |

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Thành Phần Kết Hợp)

```python
# full_example.py
import pytesseract
from PIL import Image

class SimpleOCREngine:
    def __init__(self):
        self._options = {"lang": "eng"}

    def get_settings(self):
        return OcrSettings(self)

    def recognize(self, image_path: str) -> str:
        img = Image.open(image_path)
        return pytesseract.image_to_string(img, config=self._build_config())

    def _build_config(self) -> str:
        return f"-l {self._options.get('lang', 'eng')}"

class OcrSettings:
    def __init__(self, engine: SimpleOCREngine):
        self._engine = engine

    def set_language(self, lang_code: str):
        if not isinstance(lang_code, str) or len(lang_code) < 2:
            raise ValueError("Language code must be a non‑empty string.")
        self._engine._options["lang"] = lang_code

    def get_language(self) -> str:
        return self._engine._options.get("lang", "eng")

# ---------- Usage ----------
engine = SimpleOCREngine()
settings = engine.get_settings()

# Change to Arabic (how to change language)
settings.set_language("ar")
print("Current OCR language:", settings.get_language())

# Uncomment and point to a real Arabic image to test OCR
# output = engine.recognize("sample_arabic.png")
# print("OCR result:", output)
```

Chạy script bằng `python full_example.py`. Nếu mọi thứ đã được thiết lập, bạn sẽ thấy:

```
Current OCR language: ar
```

…và kết quả OCR cho hình ảnh tiếng Ả Rập nếu bạn bật hai dòng cuối cùng.

## Kết Luận

Bạn đã biết **cách thay đổi ngôn ngữ trong OCR** engines, cụ thể là cách đặt ngôn ngữ OCR sang tiếng Ả Rập bằng một mẫu sạch, có thể tái sử dụng. Hướng dẫn đã đi qua việc lấy engine, truy cập cài đặt, và cuối cùng áp dụng thay đổi ngôn ngữ — bao phủ cả trường hợp *ocr language arabic* và trường hợp rộng hơn *change OCR language*.  

Bước tiếp theo? Hãy thử thêm hỗ trợ cho nhiều ngôn ngữ hơn, thử nghiệm chuỗi đa ngôn ngữ (`"ar+eng"`), hoặc tích hợp logic này vào một dịch vụ web cho phép người dùng tải lên tài liệu bằng bất kỳ script nào. Nếu bạn tò mò về *set language OCR* trong các thư viện khác (EasyOCR, Google Vision...

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách OCR Văn bản Hình ảnh với Ngôn ngữ Sử dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Trích xuất văn bản ảnh C# với lựa chọn ngôn ngữ sử dụng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cách Trích xuất OCR – Cấu hình OCR](/ocr/english/net/ocr-configuration/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}