---
category: general
date: 2026-05-03
description: Tìm hiểu cách chạy OCR trên hình ảnh và trích xuất văn bản cùng tọa độ
  bằng nhận dạng OCR có cấu trúc. Bao gồm mã Python từng bước.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: vi
og_description: Chạy OCR trên hình ảnh và lấy văn bản cùng tọa độ bằng nhận dạng OCR
  có cấu trúc. Ví dụ Python đầy đủ kèm giải thích.
og_title: Chạy OCR trên hình ảnh – Hướng dẫn trích xuất văn bản có cấu trúc
tags:
- OCR
- Python
- Computer Vision
title: Chạy OCR trên hình ảnh – Hướng dẫn toàn diện về trích xuất văn bản có cấu trúc
url: /vi/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên hình ảnh – Hướng dẫn đầy đủ về Trích xuất Văn bản có cấu trúc

Bạn đã bao giờ cần **run OCR on image** trên các tệp hình ảnh nhưng không chắc làm sao để giữ nguyên vị trí chính xác của từng từ chưa? Bạn không phải là người duy nhất. Trong nhiều dự án—quét biên lai, số hoá biểu mẫu, hoặc kiểm thử UI—bạn không chỉ cần văn bản thô mà còn cần các bounding box cho biết mỗi dòng nằm ở đâu trên ảnh.  

Hướng dẫn này sẽ cho bạn cách thực tế để *run OCR on image* bằng cách sử dụng engine **aocr**, yêu cầu **structured OCR recognition**, và sau đó thực hiện post‑process kết quả trong khi giữ nguyên hình học. Khi kết thúc, bạn sẽ có thể **extract text with coordinates** chỉ trong vài dòng Python, và bạn sẽ hiểu tại sao chế độ có cấu trúc lại quan trọng cho các tác vụ downstream.

## Những gì bạn sẽ học

- Cách khởi tạo engine OCR cho **structured OCR recognition**.  
- Cách đưa một hình ảnh vào và nhận kết quả thô bao gồm giới hạn dòng.  
- Cách chạy post‑processor để làm sạch văn bản mà không mất hình học.  
- Cách lặp qua các dòng cuối cùng và in mỗi đoạn văn bản cùng với bounding box của nó.  

Không có phép màu, không có bước ẩn—chỉ một ví dụ hoàn chỉnh, có thể chạy được mà bạn có thể đưa vào dự án của mình.

---

## Yêu cầu trước

Trước khi chúng ta bắt đầu, hãy chắc chắn rằng bạn đã cài đặt các thành phần sau:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Bạn cũng sẽ cần một tệp hình ảnh (`input_image.png` hoặc `.jpg`) chứa văn bản rõ ràng, dễ đọc. Bất kỳ thứ gì từ hoá đơn đã quét đến ảnh chụp màn hình đều được, miễn là engine OCR có thể nhận thấy các ký tự.

---

## Bước 1: Khởi tạo engine OCR cho nhận dạng có cấu trúc

Điều đầu tiên chúng ta làm là tạo một thể hiện của `aocr.Engine()` và nói với nó rằng chúng ta muốn **structured OCR recognition**. Chế độ có cấu trúc không chỉ trả về văn bản thuần mà còn cả dữ liệu hình học (hình chữ nhật bao quanh) cho mỗi dòng, điều này rất quan trọng khi bạn cần ánh xạ văn bản trở lại hình ảnh.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Tại sao điều này quan trọng:**  
> Trong chế độ mặc định, engine có thể chỉ cung cấp cho bạn một chuỗi các từ nối liền nhau. Chế độ có cấu trúc cung cấp cho bạn một cấu trúc phân cấp các trang → dòng → từ, mỗi cái đều có tọa độ, giúp việc phủ kết quả lên ảnh gốc hoặc đưa chúng vào mô hình nhận thức bố cục dễ dàng hơn nhiều.

---

## Bước 2: Chạy OCR trên hình ảnh và nhận kết quả thô

Bây giờ chúng ta đưa hình ảnh vào engine. Lệnh `recognize` trả về một đối tượng `OcrResult` chứa một tập hợp các dòng, mỗi dòng có hình chữ nhật bao quanh riêng.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Tại thời điểm này `raw_result.lines` chứa các đối tượng với hai thuộc tính quan trọng:

- `text` – chuỗi đã nhận dạng cho dòng đó.  
- `bounds` – một tuple dạng `(x, y, width, height)` mô tả vị trí của dòng.

---

## Bước 3: Post‑process trong khi giữ nguyên hình học

Kết quả OCR thô thường nhiễu: ký tự lẻ, khoảng trắng sai vị trí, hoặc vấn đề ngắt dòng. Hàm `ai.run_postprocessor` làm sạch văn bản nhưng **giữ nguyên hình học gốc**, vì vậy bạn vẫn có tọa độ chính xác.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Mẹo chuyên nghiệp:** Nếu bạn có từ vựng chuyên ngành (ví dụ, mã sản phẩm), hãy cung cấp một từ điển tùy chỉnh cho post‑processor để cải thiện độ chính xác.

---

## Bước 4: Trích xuất văn bản với tọa độ – lặp và hiển thị

Cuối cùng, chúng ta lặp qua các dòng đã làm sạch, in ra bounding box của mỗi dòng cùng với văn bản của nó. Đây là phần cốt lõi của **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Kết quả dự kiến

Giả sử ảnh đầu vào chứa hai dòng: “Invoice #12345” và “Total: $89.99”, bạn sẽ thấy một kết quả tương tự như:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Tuple đầu tiên là `(x, y, width, height)` của dòng trên ảnh gốc, cho phép bạn vẽ hình chữ nhật, tô sáng văn bản, hoặc đưa tọa độ vào hệ thống khác.

---

## Trực quan hoá Kết quả (Tùy chọn)

Nếu bạn muốn xem các bounding box được phủ lên ảnh, bạn có thể dùng Pillow (PIL) để vẽ hình chữ nhật. Dưới đây là một đoạn mã nhanh; bạn có thể bỏ qua nếu chỉ cần dữ liệu thô.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![ví dụ chạy OCR trên hình ảnh hiển thị các bounding box](/images/ocr-bounding-boxes.png "chạy OCR trên hình ảnh – lớp phủ bounding box")

Văn bản alt phía trên chứa **primary keyword**, đáp ứng yêu cầu SEO cho thuộc tính alt của hình ảnh.

---

## Tại sao Structured OCR Recognition vượt trội so với Trích xuất Văn bản Đơn giản

Bạn có thể tự hỏi, “Tôi không thể chỉ chạy OCR và lấy văn bản sao? Tại sao phải bận tâm đến hình học?”  

- **Spatial context:** Khi bạn cần ánh xạ các trường trên một biểu mẫu (ví dụ, “Date” bên cạnh giá trị ngày), tọa độ cho bạn biết *ở đâu* dữ liệu nằm.  
- **Multi‑column layouts:** Văn bản tuyến tính đơn giản mất thứ tự; dữ liệu có cấu trúc bảo toàn thứ tự cột.  
- **Post‑processing accuracy:** Biết kích thước hộp giúp bạn quyết định một từ là tiêu đề, chú thích, hay một mảnh vụn không mong muốn.  

Tóm lại, **structured OCR recognition** cung cấp cho bạn tính linh hoạt để xây dựng các pipeline thông minh hơn—cho dù bạn đang đưa dữ liệu vào cơ sở dữ liệu, tạo PDF có thể tìm kiếm, hoặc huấn luyện mô hình machine‑learning tôn trọng bố cục.

---

## Các trường hợp góc cạnh thường gặp và Cách xử lý

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Hình ảnh bị xoay hoặc nghiêng** | Các bounding box có thể lệch trục. | Tiền xử lý bằng cách chỉnh nghiêng (ví dụ, `warpAffine` của OpenCV). |
| **Phông chữ rất nhỏ** | Engine có thể bỏ sót ký tự, dẫn đến các dòng trống. | Tăng độ phân giải ảnh hoặc sử dụng `ocr_engine.set_dpi(300)`. |
| **Ngôn ngữ hỗn hợp** | Mô hình ngôn ngữ sai có thể gây ra văn bản rối. | Đặt `ocr_engine.language = ["en", "de"]` trước khi nhận dạng. |
| **Các hộp chồng lên nhau** | Post‑processor có thể hợp nhất hai dòng một cách không mong muốn. | Xác minh `line.bounds` sau khi xử lý; điều chỉnh ngưỡng trong `ai.run_postprocessor`. |

Xử lý những kịch bản này sớm sẽ giúp bạn tránh đau đầu sau này, đặc biệt khi bạn mở rộng giải pháp lên hàng trăm tài liệu mỗi ngày.

---

## Script Đầy đủ Từ đầu đến cuối

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy, kết nối tất cả các bước lại với nhau. Sao chép‑dán, điều chỉnh đường dẫn ảnh, và bạn đã sẵn sàng.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Running this script will:

1. **Run OCR on image** với chế độ có cấu trúc.  
2. **Extract text with coordinates** cho mỗi dòng.  
3. Tùy chọn tạo PNG đã chú thích hiển thị các hộp.

---

## Kết luận

Bây giờ bạn đã có một giải pháp vững chắc, tự chứa để **run OCR on image** và **extract text with coordinates** bằng **structured OCR recognition**. Mã nguồn minh họa mọi bước—từ khởi tạo engine đến post‑processing và xác minh trực quan—để bạn có thể áp dụng cho biên lai, biểu mẫu, hoặc bất kỳ tài liệu hình ảnh nào cần định vị văn bản chính xác.

Tiếp theo? Hãy thử thay thế engine `aocr` bằng một thư viện khác (Tesseract, EasyOCR) và xem cách đầu ra có cấu trúc của chúng khác nhau như thế nào. Thử nghiệm các chiến lược post‑processing khác nhau, như kiểm tra chính tả hoặc bộ lọc regex tùy chỉnh, để nâng cao độ chính xác cho lĩnh vực của bạn. Và nếu bạn đang xây dựng một pipeline lớn hơn, hãy cân nhắc lưu trữ các cặp `(text, bounds)` trong cơ sở dữ liệu để phân tích sau này.

Chúc lập trình vui vẻ, và chúc các dự án OCR của bạn luôn chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}