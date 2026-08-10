---
category: general
date: 2026-06-16
description: In ra JSON dạng đẹp trong Python nhanh chóng và học cách chuyển JSON
  thành dict hoặc tải chuỗi JSON trong Python để thao tác dữ liệu. Hướng dẫn từng
  bước.
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: vi
og_description: In ra JSON dạng đẹp trong Python và ngay lập tức xem cách chuyển JSON
  thành dict hoặc tải chuỗi JSON trong Python. Thành thạo xử lý JSON trong vài phút.
og_title: In Đẹp JSON Python – Hướng Dẫn Định Dạng và Chuyển Đổi Toàn Diện
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: In Đẹp JSON Python – Hướng Dẫn Toàn Diện về Định Dạng & Chuyển Đổi
url: /vi/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# In Python Định Dạng JSON Đẹp – Hướng Dẫn Toàn Diện Về Định Dạng & Chuyển Đổi

Bạn đã bao giờ cần **pretty print JSON Python** và tự hỏi tại sao kết quả luôn hiển thị như một dòng duy nhất, không đọc được không? Bạn không phải là người duy nhất. Trong nhiều dự án, chuỗi JSON thô là một mớ hỗn độn, khiến việc gỡ lỗi giống như tìm kim trong bãi cỏ.  

Tin tốt? Với chỉ một vài hàm tích hợp sẵn, bạn có thể biến khối dữ liệu hỗn loạn thành một dạng hiển thị có thụt lề đẹp mắt, và sau đó **convert JSON to dict** để xử lý downstream mượt mà. Trong hướng dẫn này, chúng ta sẽ đi qua từng bước—từ việc tải một chuỗi JSON trong Python đến việc lặp qua dữ liệu của nó—để bạn có thể tập trung vào logic thay vì vật lộn với việc định dạng.

## Những Điều Hướng Dẫn Này Bao Quát

- Cách **pretty print JSON Python** bằng cách sử dụng `json.dumps` với đối số `indent`.  
- Cách chính xác để **load JSON string Python** vào một dictionary gốc.  
- Chuyển đổi dictionary kết quả thành các đối tượng Python hữu ích, bao gồm một ví dụ thực tế in ra mỗi từ cùng điểm tin cậy.  
- Những lỗi thường gặp (như xử lý ký tự không phải ASCII) và cách khắc phục nhanh.  
- Một script hoàn chỉnh, có thể chạy được mà bạn có thể sao chép‑dán và điều chỉnh ngay lập tức.

Kết thúc hướng dẫn này, bạn sẽ có thể biến bất kỳ payload JSON nào thành định dạng dễ đọc cho con người và thao tác với nó bằng Python thuần—không cần thư viện bên ngoài.

---

## Yêu Cầu Trước

- Python 3.8 trở lên (module `json` là một phần của thư viện chuẩn).  
- Hiểu biết cơ bản về dictionary và vòng lặp.  
- Tùy chọn, một engine OCR hoặc bất kỳ dịch vụ nào trả về JSON—ví dụ của chúng tôi sử dụng một lời gọi mock `engine.recognize()`, nhưng bạn có thể thay thế bằng nguồn dữ liệu của riêng mình.

---

## Bước 1: Thực Hiện OCR (hoặc Bất Kỳ Nhận Dạng Tạo JSON) 

Đầu tiên, bạn cần một kết quả tương thích JSON. Trong nhiều quy trình computer‑vision, engine OCR trả về một đối tượng có cấu trúc có thể được serialize thành JSON. Đây là một placeholder tối thiểu:

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **Tại sao bước này quan trọng:**  
> Ngay cả khi bạn không thực hiện OCR, bạn thường nhận dữ liệu từ một API, một tệp, hoặc một hàng đợi tin nhắn. Đối tượng phải có khả năng serialize thành JSON trước khi chúng ta có thể **pretty print** nó.

---

## Bước 2: Pretty Print JSON Python

Bây giờ chúng ta biến dữ liệu thô thành một chuỗi có thụt lề đẹp mắt. Tham số `indent` thực hiện phần lớn công việc.

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

Kết quả sẽ trông như sau:

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **Mẹo chuyên nghiệp:** Sử dụng `indent=4` nếu bạn thích khoảng cách rộng hơn, hoặc thêm `sort_keys=True` để sắp xếp các khóa theo thứ tự alphabet.

---

## Bước 3: Load JSON String Python → Dictionary Gốc

Một chuỗi đã được pretty‑print rất tốt cho con người, nhưng Python lại thích dictionary cho công việc thực tế. Đây là nơi chúng ta **load JSON string Python** vào một cấu trúc gốc.

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

Bạn sẽ thấy:

```
✅ Loaded dict type: <class 'dict'>
```

> **Tại sao chúng ta làm điều này:**  
> Dictionary cho phép tra cứu O(1), dữ liệu có thể thay đổi, và tích hợp liền mạch với phần còn lại của hệ sinh thái Python. Cố gắng làm việc trực tiếp với chuỗi JSON sẽ buộc bạn phải phân tích chuỗi một cách cồng kềnh.

---

## Bước 4: Lặp Qua Các Từ Được Nhận Diện – Trường Hợp Thực Tế

Hãy trích xuất mỗi từ và điểm tin cậy của nó. Điều này minh họa cả **convert json to dict** (dictionary chúng ta đã có) và việc lặp thực tế.

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

Kết quả mong đợi:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **Mẹo trường hợp biên:** Nếu JSON có thể thiếu khóa `"words"`, hãy bảo vệ khỏi `KeyError`:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## Bước 5: Xử Lý Ký Tự Không‑ASCII (Hỗ Trợ Unicode)

Các engine OCR thường trả về ký tự như “é” hoặc “ü”. `json.dumps` mặc định sẽ escape chúng thành `\u00e9`. Để giữ chúng đọc được, truyền `ensure_ascii=False`.

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

Bây giờ đầu ra hiển thị **café** thay vì phiên bản escaped. Điều này rất quan trọng khi bạn **convert json to dict** sau này; dictionary sẽ chứa các chuỗi Unicode đúng.

---

## Bước 6: Lưu và Tải Lại JSON Đã Được Pretty‑Print (Tùy Chọn)

Đôi khi bạn muốn lưu JSON đã định dạng vào một tệp để kiểm tra sau.

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

Tệp sẽ chứa JSON được thụt lề đẹp mắt, và `json.load` sẽ tự động phân tích lại thành một dictionary.

---

## Bước 7: Tổng Hợp Tất Cả – Giải Pháp Một Tệp

Dưới đây là một script tự chứa tích hợp mọi bước đã thảo luận. Bạn có thể đặt nó vào một tệp có tên `pretty_json_demo.py` và chạy.

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

Chạy nó:

```bash
python pretty_json_demo.py
```

Bạn sẽ thấy JSON đã được pretty‑print, kiểu dictionary, mỗi từ cùng điểm tin cậy, và một phiên bản thân thiện Unicode được lưu vào `pretty_output.json`.  

**Đó là toàn bộ câu chuyện**—từ đầu ra OCR thô đến một dictionary Python sạch sẽ, có thể thao tác.

---

## Các Câu Hỏi Thường Gặp (FAQs)

| Câu Hỏi | Trả Lời |
|----------|--------|
| **Tôi có cần thư viện bên ngoài không?** | Không. Module `json` tích hợp sẵn xử lý cả việc pretty printing và loading. |
| **Nếu JSON của tôi rất lớn thì sao?** | Sử dụng `json.dump` với một file handle để tránh tải toàn bộ vào bộ nhớ; bạn vẫn có thể đặt `indent` để tạo file pretty. |
| **Tôi có thể sắp xếp các khóa không?** | Có—thêm `sort_keys=True` vào `json.dumps` để có thứ tự xác định, giúp việc kiểm thử dựa diff. |
| **Làm sao xử lý JSON sai định dạng?** | Bao bọc `json.loads` trong khối `try/except json.JSONDecodeError` và ghi lại chuỗi gây lỗi. |
| **Có giải pháp nhanh hơn không?** | Đối với payload khổng lồ, các thư viện như `orjson` hoặc `ujson` nhanh hơn, nhưng chúng không hỗ trợ `indent` out‑of‑ |

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoàn chỉnh với các ví dụ hoạt động và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách sử dụng Aspose OCR để nhận kết quả JSON trong nhận dạng hình ảnh](/ocr/english/net/text-recognition/get-result-as-json/)
- [Cách sử dụng Aspose OCR để lấy kết quả JSON trong nhận dạng hình ảnh](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [Cách sử dụng Aspose OCR để nhận kết quả JSON trong nhận dạng hình ảnh (tiếng Đức)](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}