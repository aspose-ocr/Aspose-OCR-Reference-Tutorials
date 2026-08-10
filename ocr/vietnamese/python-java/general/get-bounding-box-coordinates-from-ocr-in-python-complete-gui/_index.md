---
category: general
date: 2026-06-22
description: Lấy tọa độ hộp bao quanh từ hình ảnh bằng Python. Học cách trích xuất
  văn bản từ hình ảnh bằng Python với Aspose OCR và phân tích JSON trong vài phút.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: vi
og_description: Lấy tọa độ hộp bao quanh từ hình ảnh bằng Python. Hướng dẫn này chỉ
  cách trích xuất văn bản từ hình ảnh bằng Python với Aspose OCR và phân tích dữ liệu
  bố cục.
og_title: Lấy tọa độ hộp bao quanh từ OCR trong Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Lấy tọa độ hộp bao từ OCR trong Python – Hướng dẫn toàn diện
url: /vi/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lấy Tọa Độ Hộp Bao (Bounding Box) từ OCR trong Python – Hướng Dẫn Toàn Diện

Bạn đã bao giờ cần **lấy tọa độ hộp bao** cho mỗi từ trong một hoá đơn đã quét, nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất. Trong nhiều dự án tự động hoá, bạn phải xác định vị trí văn bản trên ảnh để làm nổi bật, che khuất, hoặc đưa vào các phân tích tiếp theo. Tin tốt? Chỉ với vài dòng Python và Aspose.OCR, bạn có thể lấy cả văn bản **và** vị trí chính xác của nó trong một lần xử lý.

Trong tutorial này, chúng ta sẽ thực hành một ví dụ thực tế cho thấy cách **trích xuất văn bản từ ảnh theo phong cách python**, sau đó khai thác dữ liệu bố cục JSON để lấy các hộp bao. Không có phần thừa, chỉ có script hoạt động, giải thích lý do mỗi bước quan trọng, và mẹo tránh các lỗi thường gặp.

---

## Những gì bạn sẽ xây dựng

Khi hoàn thành hướng dẫn này, bạn sẽ có một script Python sẵn sàng chạy mà:

1. Tải một ảnh (ví dụ: hoá đơn PNG) vào Aspose OCR.  
2. Cấu hình engine để xuất thông tin bố cục dưới dạng JSON.  
3. Phân tích JSON thành một dictionary của Python.  
4. Lặp qua từng từ được nhận dạng, in ra văn bản **và** tọa độ hộp bao của nó.

Bạn cũng sẽ thấy cách điều chỉnh code cho PDF đa trang, các định dạng ảnh khác, và hệ tọa độ tùy chỉnh.

### Yêu cầu trước

- Python 3.8+ đã được cài đặt trên máy của bạn.  
- Giấy phép Aspose.OCR for Python hoạt động hoặc bản dùng thử miễn phí (thư viện vẫn hoạt động không có giấy phép nhưng sẽ thêm watermark).  
- `pip install aspose-ocr` (tên gói trên PyPI).  
- Một ảnh mẫu có tên `invoice.png` đặt trong thư mục bạn có thể tham chiếu.

Đó là tất cả—không cần framework nặng, không cần dịch vụ bên ngoài. Hãy bắt đầu.

---

## Bước 1: Cài đặt và Import các Thư viện Cần thiết

Đầu tiên, đảm bảo gói Aspose OCR và module tích hợp `json` đã sẵn sàng. Module `json` đã đi kèm với Python, vì vậy chúng ta chỉ cần cài đặt Aspose.

```bash
pip install aspose-ocr
```

Bây giờ import chúng trong script của bạn:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Tại sao lại quan trọng:** Import `aspose.ocr` cho phép bạn truy cập vào engine OCR hiệu năng cao, trong khi `json` giúp chuyển chuỗi bố cục thô thành một dictionary Python gốc để duyệt dễ dàng.

---

## Bước 2: Tạo OCR Engine và Tải Ảnh của Bạn

Engine là trái tim của quá trình. Bạn khởi tạo nó, sau đó chỉ định ảnh muốn quét.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Mẹo chuyên nghiệp:** Thay `"YOUR_DIRECTORY/invoice.png"` bằng đường dẫn tuyệt đối hoặc tương đối trỏ tới file thực tế của bạn. Nếu file không tồn tại, Aspose sẽ ném ra `FileNotFoundError`, vì vậy hãy kiểm tra lại chính tả.

---

## Bước 3: Cấu hình Engine để Xuất Dữ liệu Bố cục JSON

Aspose OCR có thể trả về văn bản thuần, JSON chỉ OCR, hoặc JSON bố cục đầy đủ bao gồm tọa độ cho từ, dòng, và thậm chí ký tự riêng lẻ. Đối với **lấy tọa độ hộp bao**, chúng ta cần JSON bố cục.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Tại sao lại là JSON?** JSON không phụ thuộc ngôn ngữ, dễ đọc cho con người, và ánh xạ sạch sẽ sang dictionary Python. JSON bố cục chứa một mảng `"words"` trong đó mỗi mục giữ văn bản và một mảng `boundingBox` gồm tám số (bốn điểm góc).

---

## Bước 4: Thực hiện Nhận dạng và Lấy Chuỗi JSON Thô

Bây giờ chúng ta thực sự chạy OCR. Phương thức `recognize()` trả về một đối tượng `OcrResult`, từ đó chúng ta có thể trích xuất chuỗi JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Nếu bạn in `layout_json` sẽ thấy một thứ gì đó như:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Trường hợp biên:** Một số ảnh có thể tạo ra mảng `"words"` rỗng nếu engine OCR không phát hiện được bất kỳ văn bản nào. Trong trường hợp đó, hãy kiểm tra chất lượng ảnh (độ tương phản, độ phân giải) trước khi tiếp tục.

---

## Bước 5: Phân tích JSON thành Dictionary Python

Làm việc với cấu trúc Python gốc dễ dàng hơn rất nhiều so với việc xử lý chuỗi. Sử dụng hàm `json.loads()` để chuyển đổi chuỗi.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Bây giờ `layout_data["words"]` là một danh sách các dictionary, mỗi dictionary đại diện cho một từ và hộp bao của nó.

---

## Bước 6: Lặp qua Các Từ và **Lấy Tọa Độ Hộp Bao**

Đây là phần cốt lõi của tutorial: lặp qua mỗi từ, trích xuất văn bản và in ra tọa độ. Đây chính là nơi chúng ta **lấy tọa độ hộp bao**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Kết quả mẫu** (các số của bạn sẽ khác tùy vào ảnh):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Tại sao lại là định dạng tám điểm?** Bốn góc (trên‑trái, trên‑phải, dưới‑phải, dưới‑trái) cho phép bạn vẽ một đa giác quanh từ, ngay cả khi văn bản bị nghiêng. Nếu bạn chỉ cần một hình chữ nhật đơn giản, có thể tính `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, và `height = max(y…) - y_min`.

---

## Các Cải Tiến Tùy Chọn

### 1. Chuyển Hộp Bao thành Hình Chữ Nhật Đơn Giản

Nếu công cụ downstream của bạn mong đợi `(x, y, width, height)` thay vì tám điểm, hãy thêm một hàm trợ giúp:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Xử Lý PDF Đa Trang

Aspose OCR có thể chấp nhận luồng PDF. Thay dòng tải ảnh bằng:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Lặp `set_page_number` cho mỗi trang, thu thập tọa độ theo trang.

### 3. Hiển Thị Hộp Bao

Nếu bạn muốn xem các hộp được vẽ lên ảnh gốc, sử dụng Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Bây giờ bạn sẽ thấy các đường viền màu đỏ quanh mỗi từ được nhận dạng—hoàn hảo để debug hoặc hiển thị UI.

---

## Câu Hỏi Thường Gặp & Các Bẫy

- **JSON quá lớn thì sao?** Đối với tài liệu lớn, cân nhắc stream JSON hoặc xử lý từng trang một để giảm tiêu thụ bộ nhớ.  
- **Tại sao một số từ lại thiếu?** Độ tương phản thấp hoặc văn bản viết tay thường làm engine OCR gặp khó. Tiền xử lý ảnh (tăng độ tương phản, nhị phân hoá) trước khi đưa vào Aspose.  
- **Có thể lấy tọa độ mức ký tự không?** Có—đặt `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` để nhận mảng `"characters"` với `boundingBox` riêng.  
- **Hệ tọa độ có bắt đầu từ 0 không?** Đúng. (0, 0) là góc trên‑trái của ảnh.

---

## Script Đầy Đủ – Sẵn Sàng Sao Chép & Chạy

Dưới đây là ví dụ hoàn chỉnh, có thể chạy ngay. Lưu lại dưới tên `extract_bboxes.py` và thực thi `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}