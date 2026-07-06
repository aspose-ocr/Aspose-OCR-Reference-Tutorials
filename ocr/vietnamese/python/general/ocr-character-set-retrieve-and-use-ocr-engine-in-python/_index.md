---
category: general
date: 2026-06-06
description: 'Hướng dẫn bộ ký tự OCR: học cách sử dụng công cụ OCR để liệt kê các
  ký tự được hỗ trợ cho các bảng chữ Latin và Cyrillic với các ví dụ Python đầy đủ.'
draft: false
keywords:
- ocr character set
- use OCR engine
- supported OCR characters
- script detection OCR
- OCR library Python
language: vi
og_description: 'Hướng dẫn bộ ký tự OCR: khám phá cách sử dụng engine OCR trong Python
  để liệt kê các ký tự được hỗ trợ cho các bộ chữ viết khác nhau, kèm theo mã và mẹo.'
og_title: Bộ ký tự OCR – Truy xuất và Sử dụng công cụ OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: 'OCR character set guide: learn how to use OCR engine to list supported
    characters for Latin and Cyrillic scripts with full Python examples.'
  headline: OCR Character Set – Retrieve and Use OCR Engine in Python
  type: TechArticle
tags:
- OCR
- Python
- Character Sets
title: Bộ ký tự OCR – Truy xuất và sử dụng Engine OCR trong Python
url: /vi/python/general/ocr-character-set-retrieve-and-use-ocr-engine-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Bộ ký tự OCR – Truy xuất và Sử dụng Engine OCR trong Python

Bạn muốn biết **bộ ký tự OCR** mà thư viện của mình hỗ trợ? Trong hướng dẫn này chúng tôi sẽ chỉ cho bạn cách **sử dụng engine OCR** để truy vấn các ký tự được hỗ trợ cho các script khác nhau, và tại sao điều này lại quan trọng đối với các dự án thực tế.

Nếu bạn từng nhìn chằm chằm vào màn hình trống và tự hỏi tại sao một số ký tự không bao giờ xuất hiện sau khi xử lý OCR, bạn không phải là người duy nhất. Câu trả lời thường ẩn trong bộ ký tự mà engine biết. Khi đọc xong hướng dẫn này, bạn sẽ có thể:

* Liệt kê mọi ký tự mà một engine OCR có thể nhận dạng cho một script nhất định.  
* Xử lý các trường hợp script không được hỗ trợ.  
* Nhúng thông tin bộ ký tự vào việc kiểm tra hợp lệ hoặc logic UI downstream.

Không có bất kỳ thủ thuật hộp đen nào—chỉ là Python thuần, một vài dòng code, và một chút giải thích.

---

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

* Python 3.8+ được cài đặt (code sử dụng f‑strings).  
* Thư viện OCR cung cấp `ocr.OcrEngine`—trong ví dụ này chúng tôi giả định có một package tên `ocr` đã được cài đặt qua `pip install ocr-lib`.  
* Kiến thức cơ bản về hệ thống import của Python và việc in ra màn hình.

Nếu bạn chưa có thư viện, chạy:

```bash
pip install ocr-lib
```

Xong—không cần binary hay phụ thuộc native nào cho các truy vấn bộ ký tự cơ bản mà chúng ta sẽ thực hiện.

---

## Bước 1: Khởi tạo Instance của Engine OCR

Tạo một đối tượng engine là việc đầu tiên bạn làm khi **sử dụng engine OCR**. Hãy nghĩ nó như bật một máy quét; nếu không có nó, bạn không thể đặt câu hỏi nào.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Lớp `OcrEngine` là một wrapper nhẹ quanh engine nhận dạng bên dưới. Nó không bắt đầu xử lý nặng cho tới khi bạn yêu cầu, vì vậy chi phí khởi động gần như không đáng kể.

> **Mẹo chuyên nghiệp:** Nếu ứng dụng của bạn tạo nhiều instance engine, hãy tái sử dụng một instance duy nhất. Điều này tiết kiệm bộ nhớ và giảm độ trễ khởi tạo.

---

## Bước 2: Truy vấn Bộ ký tự OCR cho một Script Cụ thể

Bây giờ chúng ta đã có engine, có thể hỏi nó biết những ký tự nào cho một hệ thống viết nhất định. Phương thức `get_supported_characters(script_name)` trả về một `list` Python chứa các ký tự Unicode.

```python
# Step 2: Get the list of characters the engine can recognize for the Latin script
latin_chars = engine.get_supported_characters("Latin")
print(f"Supported Latin chars ({len(latin_chars)}): {latin_chars}")
```

Chạy đoạn code trên sẽ in ra thứ gì đó như:

```
Supported Latin chars (26): ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
```

Kết quả chính xác phụ thuộc vào phiên bản thư viện OCR, nhưng bạn sẽ luôn nhận được một danh sách phẳng các ký tự. Nếu bạn cần cả chữ hoa và chữ thường, chỉ cần yêu cầu script `"Latin"` rồi áp dụng `.lower()` cho mỗi phần tử, hoặc truy vấn script `"Latin‑lower"` riêng nếu thư viện phân biệt chúng.

### Tại sao điều này lại quan trọng?

Khi bạn đưa vào một hình ảnh chứa các dấu phụ lạ (ví dụ: “ñ” hoặc “ø”), engine OCR có thể âm thầm thay chúng bằng ký tự placeholder hoặc bỏ hoàn toàn. Biết trước **bộ ký tự OCR** giúp bạn kiểm tra đầu vào, cảnh báo người dùng, hoặc chuyển sang engine khác.

---

## Bước 3: Lấy Ký tự cho Script Khác – Ví dụ Cyrillic

Phương thức này hoạt động với bất kỳ script nào mà engine tuyên bố hỗ trợ. Hãy xem nó hoạt động như thế nào với Cyrillic.

```python
# Step 3: Get the list of characters the engine can recognize for the Cyrillic script
cyrillic_chars = engine.get_supported_characters("Cyrillic")
print(f"Supported Cyrillic chars ({len(cyrillic_chars)}): {cyrillic_chars}")
```

Kết quả thường thấy:

```
Supported Cyrillic chars (33): ['А', 'Б', 'В', 'Г', 'Д', 'Е', 'Ё', 'Ж', 'З', 'И', 'Й', 'К', 'Л', 'М', 'Н', 'О', 'П', 'Р', 'С', 'Т', 'У', 'Ф', 'Х', 'Ц', 'Ч', 'Ш', 'Щ', 'Ъ', 'Ы', 'Ь', 'Э', 'Ю', 'Я']
```

Nếu engine **không** hỗ trợ script được yêu cầu, nó thường ném `ValueError` (hoặc trả về danh sách rỗng tùy vào cách triển khai). Hãy bảo vệ mã của bạn trước trường hợp này.

```python
def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

# Example usage:
safe_get_characters(engine, "Arabic")   # Might trigger the error branch
```

---

## Bước 4: Trực quan hoá Bộ ký tự OCR (Tùy chọn)

Đôi khi một hình ảnh nhanh giúp ích, đặc biệt khi bạn cần trình bày cho các bên liên quan biết những ký tự nào đã được bao phủ. Dưới đây là một ví dụ tối thiểu dùng `matplotlib` để vẽ lưới ký tự.

```python
import matplotlib.pyplot as plt

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14, ha='center', va='center')
    plt.title(title)
    plt.show()

# Visualize Latin characters
plot_character_grid(latin_chars, title="Latin OCR Character Set")
```

> **Văn bản thay thế hình ảnh:** ![Bộ ký tự OCR](ocr_character_set.png){alt="Tổng quan bộ ký tự OCR"}

Biểu đồ không bắt buộc cho giải pháp cốt lõi, nhưng nó minh họa cách bạn có thể **sử dụng engine OCR** để khai thác siêu dữ liệu ngoài việc in ra màn hình.

---

## Bước 5: Tích hợp Bộ ký tự vào Quy trình Thực tế

Bây giờ chúng ta có thể truy xuất **bộ ký tự OCR**, hãy xem một kịch bản thực tế: kiểm tra đầu ra OCR trước khi lưu vào cơ sở dữ liệu.

```python
def validate_ocr_output(text, allowed_chars):
    """Return True if every character in `text` exists in `allowed_chars`."""
    invalid = [c for c in text if c not in allowed_chars]
    if invalid:
        print(f"Invalid characters found: {invalid}")
        return False
    return True

# Suppose we ran OCR on an image and got this result:
ocr_result = "HELLO WORLD!"

# Use the previously fetched Latin set for validation:
if validate_ocr_output(ocr_result, set(latin_chars)):
    print("All characters are supported – safe to store.")
else:
    print("Result contains unsupported symbols – consider manual review.")
```

Mẫu này ngăn dữ liệu rác lọt vào các pipeline downstream, một vấn đề phổ biến khi làm việc với tài liệu đa ngôn ngữ.

---

## Những Cạm Bẫy Thường Gặp và Các Trường Hợp Cạnh

| Cạm bẫy | Nguyên nhân | Cách tránh |
|---------|-------------|------------|
| **Tên script sai** (ví dụ: `"Cyrillic "` có dấu cách thừa) | Engine xử lý chuỗi nguyên văn và không tìm thấy script. | Loại bỏ khoảng trắng: `script.strip()` trước khi gọi `get_supported_characters`. |
| **Danh sách ký tự rỗng** | Một số engine khai báo script nhưng chưa tải mô hình ngôn ngữ. | Gọi `engine.load_language_model(script)` nếu thư viện có phương thức này, hoặc đảm bảo các file mô hình đã có. |
| **Vấn đề chuẩn hoá Unicode** | Các ký tự như “é” có thể xuất hiện dưới dạng hợp thành (`\u00E9`) hoặc tách rời (`e\u0301`). | Chuẩn hoá chuỗi bằng `unicodedata.normalize('NFC', text)` trước khi kiểm tra. |
| **Hiệu năng với script lớn** (ví dụ: Chinese) | Truy xuất hàng nghìn ký tự có thể chậm. | Lưu cache kết quả sau lần gọi đầu tiên; hầu hết ứng dụng chỉ cần danh sách một lần. |

---

## Ví dụ Hoàn chỉnh

Kết hợp mọi thứ lại, đây là một script duy nhất bạn có thể sao chép‑dán và chạy:

```python
import ocr
import matplotlib.pyplot as plt

def safe_get_characters(engine, script):
    try:
        chars = engine.get_supported_characters(script)
        if not chars:
            print(f"No characters returned for script '{script}'.")
        else:
            print(f"Supported {script} chars ({len(chars)}): {chars}")
        return chars
    except Exception as e:
        print(f"Error retrieving characters for script '{script}': {e}")
        return []

def plot_character_grid(chars, title="OCR Character Set"):
    cols = 10
    rows = (len(chars) + cols - 1) // cols
    fig, ax = plt.subplots(figsize=(cols, rows))
    ax.set_axis_off()
    for idx, ch in enumerate(chars):
        row = idx // cols
        col = idx % cols
        ax.text(col / cols, 1 - row / rows, ch, fontsize=14


## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code đầy đủ cùng giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Hướng dẫn Aspose OCR – Nhận dạng ký tự quang học](/ocr/english/)
- [Xử lý hậu OCR – Lấy các lựa chọn ký tự](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Cách Đặt Giá Trị Ngưỡng trong Nhận dạng Hình ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}