---
category: general
date: 2026-06-25
description: 'Nhận dạng văn bản từ file PNG bằng Python: hướng dẫn từng bước để tạo
  công cụ OCR bằng Python, chạy OCR trên tài liệu kỹ thuật và trích xuất văn bản từ
  hình ảnh tài liệu kỹ thuật.'
draft: false
keywords:
- recognize text from png
- ocr image to text python
- create OCR engine python
- extract text from technical document image
- run OCR on technical document
language: vi
og_description: Nhận dạng văn bản từ file PNG bằng Python. Tìm hiểu cách tạo công
  cụ OCR bằng Python, chạy OCR trên tài liệu kỹ thuật và trích xuất văn bản từ hình
  ảnh tài liệu kỹ thuật.
og_title: Nhận dạng văn bản từ PNG trong Python – Hướng dẫn đầy đủ về công cụ OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  headline: Recognize Text from PNG in Python – Complete OCR Engine Guide
  type: TechArticle
- description: 'recognize text from png with Python: step‑by‑step guide to create
    OCR engine python, run OCR on technical document and extract text from technical
    document image.'
  name: Recognize Text from PNG in Python – Complete OCR Engine Guide
  steps:
  - name: Low‑Resolution Images
    text: 'If the PNG originates from a scanned fax, you might be dealing with 72
      dpi. OCR accuracy drops dramatically below 150 dpi. A quick fix is to upscale
      the image using a bicubic algorithm before recognition:'
  - name: Rotated Pages
    text: 'Technical manuals sometimes come scanned at an angle. The engine can auto‑deskew,
      but you can also pre‑rotate:'
  - name: Multi‑Page Documents
    text: 'When you need to **run OCR on technical document** PDFs that have been
      exported to PNG per page, wrap the logic in a loop:'
  - name: Language Selection
    text: 'Aspose OCR defaults to English, but you can switch to other languages (e.g.,
      German) by loading the appropriate language pack:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Nhận dạng văn bản từ PNG trong Python – Hướng dẫn đầy đủ về công cụ OCR
url: /vi/python-java/general/recognize-text-from-png-in-python-complete-ocr-engine-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng Văn bản từ PNG trong Python – Hướng dẫn Toàn bộ Động cơ OCR

Bạn đã bao giờ cần **nhận dạng văn bản từ các tệp PNG** nhưng không chắc thư viện Python nào nên chọn? Bạn không phải là người duy nhất. Dù bạn đang số hoá các hướng dẫn quét, trích xuất số sê-ri từ nhãn sản phẩm, hay lấy dữ liệu từ hình ảnh tài liệu kỹ thuật, một pipeline OCR đáng tin cậy có thể tiết kiệm cho bạn hàng giờ sao chép‑dán thủ công.

Trong tutorial này chúng ta sẽ thực hành một ví dụ cho thấy cách **tạo động cơ OCR python**, đưa vào một PNG, và **trích xuất văn bản từ hình ảnh tài liệu kỹ thuật** chỉ với vài dòng code. Khi kết thúc, bạn cũng sẽ biết cách **chạy OCR trên tài liệu kỹ thuật** có chất lượng đa dạng, và sẽ có một script có thể tái sử dụng cho dự án tiếp theo.

## Những gì bạn sẽ học

- Cài đặt và thiết lập một thư viện OCR cho Python (Aspose OCR được dùng, nhưng các bước áp dụng cho hầu hết các gói OCR hiện đại).  
- **Tạo động cơ OCR python** và cấu hình từ điển tùy chỉnh cho thuật ngữ chuyên ngành.  
- Tải một ảnh PNG, chạy OCR, và **nhận dạng văn bản từ png** một cách hiệu quả.  
- Xử lý các vấn đề thường gặp như độ phân giải thấp, trang bị xoay, và nền nhiễu.  
- Mở rộng script để xử lý hàng loạt nhiều tài liệu kỹ thuật.

> **Yêu cầu trước** – Bạn nên có Python 3.8+ đã được cài đặt, quen thuộc cơ bản với pip, và một ảnh PNG chứa văn bản có thể máy đọc được. Không cần kinh nghiệm OCR trước.

---

## Bước 1: Cài đặt Thư viện OCR (Create OCR Engine Python)

Điều đầu tiên cần làm: chúng ta cần một thư viện thực sự thực hiện công việc nặng. Aspose OCR for Python via .NET là một lựa chọn thương mại cung cấp độ chính xác cao ngay từ đầu, nhưng cùng một mẫu cũng hoạt động với các giải pháp mã nguồn mở như `pytesseract`. Để ví dụ tự chứa, chúng ta sẽ dùng Aspose OCR.

```bash
pip install aspose-ocr
```

> **Mẹo:** Nếu bạn gặp lỗi quyền trên Windows, chạy lệnh từ PowerShell được nâng quyền hoặc thêm `--user` vào cuối.

Sau khi cài đặt, bạn có thể import module và khởi tạo một engine:

```python
import aspose.ocr as ocr
```

Dòng import duy nhất này cho phép bạn truy cập vào lớp `OcrEngine`, là nền tảng của **tạo một OCR engine python**.

## Bước 2: Khởi tạo Động cơ OCR và Tinh chỉnh (Run OCR on Technical Document)

Bây giờ chúng ta sẽ tạo một instance của engine và tùy chọn cung cấp một từ điển tùy chỉnh. Từ điển tùy chỉnh là danh sách các từ mà OCR sẽ coi là hợp lệ — hoàn hảo cho thuật ngữ kỹ thuật, mã sản phẩm, hoặc các từ viết tắt nội bộ.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: define a custom dictionary for domain‑specific terms
engine.custom_dictionary = [
    "AsposeOCR", "OCRSDK", "Invoice#2026", "SKU-12345"
]
```

Tại sao cần từ điển? Hãy tưởng tượng bạn đang quét một hướng dẫn bảo trì thường xuyên đề cập tới “SKU‑12345”. Nếu không có từ điển, OCR có thể đọc thành “SKU‑12345” hoặc thậm chí “S K U‑12345”. Bằng cách thêm thuật ngữ vào `custom_dictionary`, bạn cải thiện đáng kể độ chính xác **ocr image to text python** cho tài liệu cụ thể đó.

## Bước 3: Tải Ảnh PNG (Extract Text from Technical Document Image)

Tiếp theo, chúng ta tải PNG chứa văn bản mà chúng ta muốn **nhận dạng văn bản từ png**. Aspose OCR hỗ trợ nhiều định dạng ảnh, nhưng PNG là lựa chọn tốt vì giữ nguyên chất lượng không mất dữ liệu.

```python
# Step 3: Load the image file
image_path = "YOUR_DIRECTORY/technical_doc.png"
image = ocr.Image.load(image_path)
```

Nếu PNG của bạn quá lớn (ví dụ, một bản vẽ kiến trúc được quét), bạn có thể muốn giảm kích thước trước khi OCR để giữ mức sử dụng bộ nhớ hợp lý:

```python
# Optional downscale for huge images
max_dim = 2000  # pixels
if max(image.width, image.height) > max_dim:
    scale = max_dim / max(image.width, image.height)
    image = image.resize(int(image.width * scale), int(image.height * scale))
```

## Bước 4: Thực hiện OCR (OCR Image to Text Python)

Với engine đã sẵn sàng và ảnh đã được tải, việc nhận dạng thực tế chỉ là một lời gọi phương thức:

```python
# Step 4: Run OCR on the loaded image
result = engine.recognize(image)
```

Ở phía sau, `engine.recognize` chạy một chuỗi các bước tiền xử lý — nhị phân hoá, chỉnh góc, phân tích bố cục — trước khi đưa bitmap đã được làm sạch vào mạng nơ-ron. Đó là lý do một dòng lệnh có thể **run OCR on technical document** những tệp mà các script đơn giản sẽ gặp khó khăn.

## Bước 5: Xuất Văn bản Được Nhận dạng (Recognize Text from PNG)

Cuối cùng, chúng ta in ra văn bản đã trích xuất. Bạn cũng có thể ghi nó vào file, đưa vào cơ sở dữ liệu, hoặc truyền cho các pipeline NLP tiếp theo.

```python
# Step 5: Output the recognized text
print("=== OCR Result ===")
print(result.text)
```

Nếu bạn chạy script với một PNG hợp lệ, bạn sẽ thấy kết quả tương tự:

```
=== OCR Result ===
Invoice #2026
Product: AsposeOCR SDK
SKU-12345
Total: $1,299.00
```

> **Ví dụ Hình ảnh**  
> ![recognize text from png output](images/ocr_result.png)  
> *Alt text:* *recognize text from png – mẫu kết quả OCR hiển thị trong console.*

Ảnh chụp màn hình này cho thấy việc trích xuất sạch sẽ, trong đó từ điển tùy chỉnh đã giữ nguyên mã sản phẩm.

---

## Đi sâu hơn: Xử lý Các Trường hợp Thường gặp

### Ảnh Độ Phân Giải Thấp

Nếu PNG xuất phát từ một fax được quét, bạn có thể đang làm việc với 72 dpi. Độ chính xác OCR giảm mạnh dưới 150 dpi. Một cách khắc phục nhanh là phóng to ảnh bằng thuật toán bicubic trước khi nhận dạng:

```python
if image.dpi < 150:
    image = image.resize(image.width * 2, image.height * 2, interpolation=ocr.InterpolationMode.BICUBIC)
```

### Trang Bị Xoay

Các tài liệu kỹ thuật đôi khi được quét lệch góc. Engine có thể tự động chỉnh góc, nhưng bạn cũng có thể tự xoay trước:

```python
# Detect and correct rotation
angle = engine.auto_rotate(image)
if angle != 0:
    image = image.rotate(-angle)
```

### Tài liệu Nhiều Trang

Khi bạn cần **run OCR on technical document** PDF đã được xuất ra PNG từng trang, hãy bọc logic trong một vòng lặp:

```python
import glob

for png_path in sorted(glob.glob("pages/*.png")):
    img = ocr.Image.load(png_path)
    txt = engine.recognize(img).text
    with open("output.txt", "a", encoding="utf-8") as f:
        f.write(f"--- Page {png_path} ---\n{txt}\n\n")
```

### Lựa chọn Ngôn ngữ

Aspose OCR mặc định là tiếng Anh, nhưng bạn có thể chuyển sang ngôn ngữ khác (ví dụ, tiếng Đức) bằng cách tải gói ngôn ngữ tương ứng:

```python
engine.language = ocr.Language.German
```

Điều này hữu ích khi **extract text from technical document image** của bạn bao gồm các bảng hoặc thông số đa ngôn ngữ.

---

## Script Hoàn chỉnh

Dưới đây là script đầy đủ, sẵn sàng chạy, kết nối mọi thứ lại với nhau. Lưu lại dưới tên `ocr_technical_doc.py` và thay `YOUR_DIRECTORY/technical_doc.png` bằng đường dẫn tới PNG của bạn.



## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách thực hiện trích xuất Văn bản Hình ảnh từ Luồng bằng Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Chuyển đổi Hình ảnh thành Văn bản – Thực hiện OCR trên Hình ảnh từ URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}