---
category: general
date: 2026-03-28
description: Thực hiện OCR trên hình ảnh và lấy văn bản sạch cùng tọa độ hộp bao.
  Học cách trích xuất OCR, làm sạch OCR và hiển thị kết quả từng bước.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: vi
og_description: Thực hiện OCR trên hình ảnh, làm sạch kết quả và hiển thị tọa độ hộp
  bao trong một hướng dẫn ngắn gọn.
og_title: Thực hiện OCR trên hình ảnh – Kết quả sạch và hộp bao
tags:
- OCR
- Computer Vision
- Python
title: Thực hiện OCR trên hình ảnh – Làm sạch kết quả và hiển thị tọa độ hộp bao
url: /vi/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh – Làm sạch kết quả và hiển thị tọa độ Bounding Box

Bạn đã bao giờ cần **perform OCR on image** nhưng luôn nhận được văn bản lộn xộn và không chắc mỗi từ nằm ở đâu trên ảnh? Bạn không phải là người duy nhất. Trong nhiều dự án—số hoá hoá đơn, quét biên lai, hay chỉ đơn giản là trích xuất văn bản—việc có được đầu ra OCR thô chỉ là rào cản đầu tiên. Tin tốt là gì? Bạn có thể làm sạch đầu ra đó và ngay lập tức xem tọa độ bounding box của mỗi vùng mà không cần viết một loạt mã lặp lại.

Trong hướng dẫn này, chúng ta sẽ đi qua **cách trích xuất OCR**, chạy một **cách làm sạch OCR** post‑processor, và cuối cùng **hiển thị tọa độ bounding box** cho mỗi vùng đã được làm sạch. Khi kết thúc, bạn sẽ có một script duy nhất, có thể chạy ngay, biến một bức ảnh mờ thành văn bản gọn gàng, có cấu trúc, sẵn sàng cho các bước xử lý tiếp theo.

## Những gì bạn cần

- Python 3.9+ (cú pháp dưới đây hoạt động trên 3.8 và mới hơn)
- Một engine OCR hỗ trợ `recognize(..., return_structured=True)` – ví dụ, một thư viện giả `engine` được dùng trong đoạn mã. Thay thế bằng Tesseract, EasyOCR, hoặc bất kỳ SDK nào trả về dữ liệu vùng.
- Kiến thức cơ bản về hàm và vòng lặp trong Python
- Một file ảnh bạn muốn quét (PNG, JPG, v.v.)

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Tesseract, hàm `pytesseract.image_to_data` đã cung cấp sẵn bounding box. Bạn có thể bọc kết quả của nó trong một adapter nhỏ để mô phỏng API `engine.recognize` như dưới đây.

---

![diagram showing how to perform OCR on image and visualize bounding box coordinates](image-placeholder.png "diagram showing how to perform OCR on image and visualize bounding box coordinates")

*Alt text: sơ đồ minh họa cách thực hiện OCR trên hình ảnh và hiển thị tọa độ bounding box*

## Bước 1 – Thực hiện OCR trên hình ảnh và lấy các vùng có cấu trúc

Điều đầu tiên là yêu cầu engine OCR trả về không chỉ văn bản thuần mà còn một danh sách có cấu trúc các vùng văn bản. Danh sách này chứa chuỗi thô và hình chữ nhật bao quanh nó.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Tại sao điều này quan trọng:**  
Khi bạn chỉ yêu cầu văn bản thuần, bạn sẽ mất ngữ cảnh không gian. Dữ liệu có cấu trúc cho phép bạn sau này **hiển thị tọa độ bounding box**, căn chỉnh văn bản với bảng, hoặc cung cấp vị trí chính xác cho mô hình downstream.

## Bước 2 – Cách làm sạch đầu ra OCR bằng post‑processor

Các engine OCR giỏi trong việc nhận dạng ký tự, nhưng chúng thường để lại các khoảng trắng thừa, ký tự ngắt dòng, hoặc ký tự nhận dạng sai. Một post‑processor sẽ chuẩn hoá văn bản, sửa các lỗi OCR phổ biến, và cắt bỏ khoảng trắng thừa.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Nếu bạn tự xây dựng bộ làm sạch, hãy cân nhắc:

- Loại bỏ các ký tự không phải ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Gộp nhiều khoảng trắng thành một khoảng trắng duy nhất
- Áp dụng bộ kiểm tra chính tả như `pyspellchecker` để sửa các lỗi chính tả rõ ràng

**Tại sao bạn nên quan tâm:**  
Một chuỗi gọn gàng giúp việc tìm kiếm, lập chỉ mục, và các pipeline NLP downstream trở nên đáng tin cậy hơn rất nhiều. Nói cách khác, **how to clean OCR** thường là yếu tố quyết định giữa một bộ dữ liệu có thể sử dụng và một cơn đau đầu.

## Bước 3 – Hiển thị tọa độ Bounding Box cho mỗi vùng đã được làm sạch

Bây giờ văn bản đã sạch sẽ, chúng ta lặp qua từng vùng, in ra hình chữ nhật và chuỗi đã được làm sạch. Đây là phần mà chúng ta cuối cùng **hiển thị tọa độ bounding box**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Kết quả mẫu**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Bạn có thể đưa các tọa độ này vào một thư viện vẽ (ví dụ, OpenCV) để phủ các hộp lên ảnh gốc, hoặc lưu chúng vào cơ sở dữ liệu để truy vấn sau.

## Script đầy đủ, sẵn sàng chạy

Dưới đây là chương trình hoàn chỉnh kết hợp ba bước trên. Thay thế các lời gọi `engine` placeholder bằng SDK OCR thực tế của bạn.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Cách chạy

```bash
python perform_ocr.py sample_invoice.jpg
```

Bạn sẽ thấy danh sách các bounding box kèm theo văn bản đã được làm sạch, giống như kết quả mẫu ở trên.

## Câu hỏi thường gặp & Trường hợp đặc biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu engine OCR không hỗ trợ `return_structured` thì sao?** | Viết một wrapper mỏng để chuyển đổi đầu ra thô của engine (thường là danh sách các từ kèm tọa độ) thành các đối tượng có thuộc tính `text` và `bounding_box`. |
| **Có thể lấy điểm tin cậy (confidence scores) không?** | Nhiều SDK cung cấp chỉ số confidence cho mỗi vùng. Thêm nó vào câu lệnh in: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Làm sao xử lý văn bản bị quay?** | Tiền xử lý ảnh bằng `cv2.minAreaRect` của OpenCV để cân chỉnh trước khi gọi `recognize`. |
| **Nếu tôi cần đầu ra ở dạng JSON?** | Serialize `processed_result.regions` bằng `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Có cách nào để trực quan hoá các hộp không?** | Dùng OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` trong vòng lặp, sau đó `cv2.imwrite("annotated.jpg", img)`. |

## Kết luận

Bạn vừa học được **cách thực hiện OCR trên hình ảnh**, làm sạch đầu ra thô, và **hiển thị tọa độ bounding box** cho mỗi vùng. Quy trình ba bước — nhận dạng → post‑process → lặp — là một mẫu có thể tái sử dụng trong bất kỳ dự án Python nào cần trích xuất văn bản đáng tin cậy.

### Tiếp theo?

- **Khám phá các back‑end OCR khác nhau** (Tesseract, EasyOCR, Google Vision) và so sánh độ chính xác.
- **Tích hợp với cơ sở dữ liệu** để lưu trữ dữ liệu vùng cho kho lưu trữ có thể tìm kiếm.
- **Thêm phát hiện ngôn ngữ** để định hướng mỗi vùng qua bộ kiểm tra chính tả phù hợp.
- **Phủ các hộp lên ảnh gốc** để xác minh trực quan (xem đoạn mã OpenCV ở trên).

Nếu gặp bất kỳ vấn đề nào, hãy nhớ rằng lợi thế lớn nhất đến từ một bước post‑processing vững chắc; một chuỗi sạch sẽ dễ làm việc hơn rất nhiều so với một đống ký tự thô.

Chúc lập trình vui vẻ, và chúc các pipeline OCR của bạn luôn gọn gàng!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}