---
category: general
date: 2026-06-25
description: Nhanh chóng lấy các ký tự được hỗ trợ bởi OCR bằng thư viện aocr. Tìm
  hiểu cách liệt kê các ký tự OCR, thiết lập ngôn ngữ và gỡ lỗi công cụ OCR của bạn
  trong Python.
draft: false
keywords:
- get OCR supported characters
- OCR engine Python
- list OCR characters
- supported OCR languages
- aocr library
language: vi
og_description: Nhận các ký tự được hỗ trợ OCR với aocr. Hướng dẫn này cho bạn cách
  liệt kê các ký tự OCR, chọn ngôn ngữ và xử lý các trường hợp đặc biệt trong Python.
og_title: Lấy các ký tự được hỗ trợ OCR trong Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  headline: Get OCR Supported Characters in Python – Complete Guide
  type: TechArticle
- description: Get OCR supported characters quickly using the aocr library. Learn
    how to list OCR characters, set languages, and debug your OCR engine in Python.
  name: Get OCR Supported Characters in Python – Complete Guide
  steps:
  - name: What if the language pack is missing?
    text: 'If you request a language that isn’t bundled, `aocr.Language` won’t contain
      the enum, and you’ll hit an `AttributeError`. Guard against this with a simple
      check:'
  - name: Empty character list
    text: 'Some niche languages might return an empty list if the underlying training
      data is incomplete. In that scenario, you can fall back to a default (e.g.,
      English) or raise a warning:'
  - name: Unicode normalization
    text: 'The list may contain combined characters (e.g., “é” as `e` + acute accent).
      If your downstream processing expects pre‑composed glyphs, run a normalization
      step:'
  type: HowTo
- questions:
  - answer: Yes, the `get_supported_characters()` method is stable across 1.x and
      2.x. The only change is that language enums were moved to `aocr.languages`.
    question: Does this work with aocr version 2.x?
  - answer: 'Absolutely. Use `ord(ch)` inside a list comprehension: ```python code_points
      = [hex(ord(ch)) for ch in supported_chars] ```'
    question: Can I get the Unicode code point for each character?
  - answer: 'aocr includes an `ARABIC` enum. The character list will contain Arabic
      glyphs, but you may need to enable RTL rendering in your downstream UI. ---
      ## Conclusion You now know **how to get OCR supported characters** using the
      aocr library in Python, how to switch between **supported OCR languages**, a'
    question: What about right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- OCR
- Python
- aocr
title: Lấy các ký tự được hỗ trợ OCR trong Python – Hướng dẫn đầy đủ
url: /vi/python/general/get-ocr-supported-characters-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lấy Các Ký Tự Hỗ Trợ OCR trong Python – Hướng Dẫn Toàn Diện

Bạn đã bao giờ tự hỏi cách **get OCR supported characters** cho một ngôn ngữ cụ thể khi đang chơi với một engine OCR chưa? Bạn không phải là người duy nhất. Dù bạn đang xây dựng một máy quét biên lai hay một bộ phân tích tài liệu đa ngôn ngữ, việc biết chính xác các glyph mà engine của bạn có thể nhận dạng là một cứu cánh. Trong tutorial này, chúng ta sẽ đi qua toàn bộ quy trình — cài đặt thư viện, cấu hình ngôn ngữ, và cuối cùng liệt kê các ký tự — để bạn có thể debug và tinh chỉnh pipeline OCR chỉ trong vài phút.

Chúng ta sẽ sử dụng thư viện **aocr**, một engine OCR nhẹ cho Python giúp việc truy vấn khả năng ngôn ngữ trở nên đơn giản. Khi kết thúc hướng dẫn, bạn sẽ có thể **list OCR characters**, chuyển đổi giữa **supported OCR languages**, và thậm chí phát hiện các khoảng trống trong phạm vi nhận dạng trước khi chúng gây rắc rối trong môi trường production.

---

## Các Điều Kiện Cần Có

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Python 3.8 hoặc mới hơn (gói aocr không còn hỗ trợ 3.7)
* Một terminal hoặc command prompt có kết nối internet
* Kiến thức cơ bản về scripting Python (nếu bạn đã từng viết `print()` thì đã đủ)

Không có phụ thuộc bên ngoài nặng — chỉ cần gói pip `aocr`.

---

## Cài Đặt Thư Viện aocr (OCR Engine Python)

Điều đầu tiên bạn cần là một cài đặt **OCR engine Python** hoạt động. Gói aocr có trên PyPI, vì vậy một lệnh pip duy nhất là đủ:

```bash
pip install aocr
```

Nếu bạn đang sử dụng môi trường ảo (được khuyến nghị mạnh mẽ), hãy kích hoạt nó trước:

```bash
python -m venv .venv
source .venv/bin/activate   # macOS/Linux
.\.venv\Scripts\activate    # Windows
```

> **Pro tip:** Ghim phiên bản (`pip install aocr==1.2.4`) để tránh các thay đổi API không mong muốn sau này.

---

## Chọn Ngôn Ngữ (Supported OCR Languages)

aocr đi kèm với một vài gói ngôn ngữ tích hợp. Mỗi gói định nghĩa tập hợp các điểm mã Unicode mà engine có thể nhận dạng. Để truy vấn các gói này, bạn cần đặt thuộc tính `language` trên đối tượng engine.

```python
import aocr

# Create the OCR engine instance
ocr_engine = aocr.OcrEngine()

# Pick the language you care about – here we use English
ocr_engine.language = aocr.Language.ENGLISH
```

Bạn có thể thay `aocr.Language.ENGLISH` bằng bất kỳ giá trị enum nào khác (`FRENCH`, `GERMAN`, v.v.). Nếu bạn cố gắng gán một ngôn ngữ không có trong gói, aocr sẽ ném ra `ValueError`. Đó là lý do tại sao nên kiểm tra danh sách **supported OCR languages** trước:

```python
print("Available languages:", [lang.name for lang in aocr.Language])
```

---

## Lấy Tập Hợp Các Ký Tự (Get OCR Supported Characters)

Bây giờ là phần trọng tâm của tutorial: thực sự **get OCR supported characters**. Engine cung cấp một phương thức tiện lợi gọi là `get_supported_characters()` trả về một danh sách các chuỗi ký tự đơn.

```python
# Step 3: Retrieve the set of characters that the engine can recognize
supported_chars = ocr_engine.get_supported_characters()
```

Ở phía sau, aocr đọc một file JSON đi kèm với gói ngôn ngữ và chuyển mỗi điểm mã Unicode thành một chuỗi Python. Kết quả là xác định, nghĩa là bạn sẽ nhận được cùng một danh sách mỗi khi chạy script trên cùng một phiên bản ngôn ngữ.

---

## Hiển Thị Số Lượng Ký Tự Được Hỗ Trợ

Biết số lượng giúp bạn nhanh chóng đánh giá độ bao phủ. Đối với tiếng Anh, bạn thường sẽ thấy vài nghìn ký tự (bao gồm dấu câu và chữ số).

```python
# Step 4: Show how many characters are supported
print(f"{len(supported_chars)} characters supported for ENGLISH:")
```

Lệnh `len()` có độ phức tạp O(1) vì Python lưu trữ độ dài danh sách nội bộ, nên không có penalty về hiệu năng ngay cả với các bảng chữ cái lớn.

---

## Xem Trước 100 Ký Tự Đầu Tiên Được Hỗ Trợ

Một kiểm tra nhanh bằng mắt có thể cho thấy engine có bao gồm các ký hiệu bạn cần không (ví dụ như dấu Euro hay dấu ngoặc thông minh). Hãy in ra một trăm ký tự đầu tiên:

```python
# Step 5: Preview the first 100 supported characters
print("".join(supported_chars[:100]), "...")
```

Phép `join` nối phần cắt thành một chuỗi duy nhất, dễ đọc hơn so với việc in ra một danh sách Python.

---

## Script Đầy Đủ – Tất Cả Các Bước Trong Một File

Dưới đây là ví dụ hoàn chỉnh, có thể chạy được, gộp tất cả các bước lại. Lưu lại dưới tên `list_supported_chars.py` và chạy `python list_supported_chars.py` từ terminal của bạn.

```python
# list_supported_chars.py
"""
Complete example showing how to get OCR supported characters
using the aocr library in Python.
"""

import aocr

def main():
    # 1️⃣ Create an OCR engine instance
    ocr_engine = aocr.OcrEngine()

    # 2️⃣ Select the language you want to work with (e.g., English)
    # You can change this to any language supported by aocr.
    ocr_engine.language = aocr.Language.ENGLISH

    # 3️⃣ Retrieve the set of characters that the engine can recognize
    supported_chars = ocr_engine.get_supported_characters()

    # 4️⃣ Show how many characters are supported
    print(f"{len(supported_chars)} characters supported for ENGLISH:")

    # 5️⃣ Preview the first 100 supported characters
    preview = "".join(supported_chars[:100])
    print(preview, "...")

if __name__ == "__main__":
    main()
```

**Kết quả mong đợi (được rút gọn để ngắn gọn):**

```
2565 characters supported for ENGLISH:
ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789.,!?'"()[]{}-+*/%$#@&... 
```

Số lượng chính xác có thể hơi khác nhau tùy phiên bản aocr, nhưng bạn sẽ luôn thấy một bảng chữ cái dài cộng với các dấu câu phổ biến.

---

## Xử Lý Các Trường Hợp Cạnh

### Ngôn ngữ bị thiếu?

Nếu bạn yêu cầu một ngôn ngữ không có trong gói, `aocr.Language` sẽ không chứa enum đó và bạn sẽ gặp `AttributeError`. Hãy bảo vệ bằng một kiểm tra đơn giản:

```python
if hasattr(aocr.Language, "SPANISH"):
    ocr_engine.language = aocr.Language.SPANISH
else:
    raise RuntimeError("Spanish language pack not installed.")
```

### Danh sách ký tự rỗng

Một số ngôn ngữ hiếm có thể trả về danh sách rỗng nếu dữ liệu huấn luyện nền tảng chưa đầy đủ. Trong trường hợp này, bạn có thể fallback về mặc định (ví dụ: English) hoặc phát ra cảnh báo:

```python
if not supported_chars:
    print("Warning: No characters returned for the selected language.")
```

### Chuẩn hoá Unicode

Danh sách có thể chứa các ký tự kết hợp (ví dụ, “é” dưới dạng `e` + dấu sắc). Nếu quy trình downstream của bạn mong đợi các glyph đã được ghép sẵn, hãy thực hiện bước chuẩn hoá:

```python
import unicodedata
normalized = [unicodedata.normalize("NFC", ch) for ch in supported_chars]
```

---

## Pro Tips cho Các Dự Án Thực Tế

* **Cache danh sách ký tự** – Nếu bạn xử lý hàng ngàn hình ảnh, việc gọi `get_supported_characters()` trong mỗi vòng lặp sẽ tạo overhead không cần thiết. Lưu danh sách vào một biến mức module hoặc serialize ra JSON để tái sử dụng sau.
* **Kiểm tra chéo ngôn ngữ** – Khi bạn hỗ trợ nhiều ngôn ngữ trong một ứng dụng, hãy giao nhau các tập ký tự để tìm tập con chung. Điều này giúp bạn thiết kế các thành phần UI nhất quán giữa các locale.
* **Debug lỗi OCR** – Nếu engine nhận dạng sai một glyph, so sánh ký tự gây lỗi với kết quả của `list_supported_chars`. Nếu nó không có trong danh sách, bạn đã phát hiện một khoảng trống cần đào tạo tùy chỉnh.
* **Kết hợp với font tùy chỉnh** – aocr tôn trọng phạm vi Unicode, nhưng chất lượng render có thể khác nhau tùy font. Kiểm tra các ký tự được hỗ trợ với đúng font bạn sẽ dùng trong production để tránh bất ngờ.

---

## Câu Hỏi Thường Gặp

**Q: Điều này có hoạt động với aocr phiên bản 2.x không?**  
A: Có, phương thức `get_supported_characters()` ổn định giữa 1.x và 2.x. Thay đổi duy nhất là các enum ngôn ngữ đã được chuyển sang `aocr.languages`.

**Q: Tôi có thể lấy mã Unicode cho mỗi ký tự không?**  
A: Chắc chắn. Sử dụng `ord(ch)` trong một list comprehension:

```python
code_points = [hex(ord(ch)) for ch in supported_chars]
```

**Q: Còn các script viết từ phải sang trái như Arabic thì sao?**  
A: aocr bao gồm enum `ARABIC`. Danh sách ký tự sẽ chứa các glyph Arabic, nhưng bạn có thể cần bật render RTL trong UI downstream.

---

## Kết Luận

Bây giờ bạn đã biết **cách get OCR supported characters** bằng thư viện aocr trong Python, cách chuyển đổi giữa **supported OCR languages**, và tại sao **listing OCR characters** lại quan trọng cho các pipeline nhận dạng văn bản mạnh mẽ. Với script đầy đủ và các mẹo trên, bạn có thể nhanh chóng xác minh phạm vi ngôn ngữ, debug các glyph thiếu, và xây dựng các ứng dụng OCR thông minh hơn.

Sẵn sàng cho bước tiếp theo? Hãy thử kết hợp danh sách ký tự này với bộ lọc word‑list tùy chỉnh, hoặc thử nghiệm với một engine OCR khác (Tesseract, EasyOCR) và so sánh kết quả. Càng khám phá, giải pháp OCR của bạn sẽ càng tốt.

Chúc lập trình vui vẻ, và hy vọng bộ ký tự của bạn luôn đầy đủ!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial dưới đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn hoạt động đầy đủ cùng các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Specify Allowed Characters OCR – Using Aspose.OCR for .NET](/ocr/english/net/ocr-settings/specify-allowed-characters/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Post Processing – Get Character Choices](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}