---
category: general
date: 2026-06-28
description: Tiền xử lý hình ảnh cho OCR với tự động xoay, nhị phân hoá và giảm nhiễu
  trong Python. Nhận đầu ra JSON có cấu trúc bằng cách sử dụng công cụ OCR.
draft: false
keywords:
- preprocess image for OCR
- auto rotate image OCR
- OCR engine Python
- OCR structured JSON output
- image binarization for OCR
- denoise OCR image
language: vi
og_description: Tiền xử lý hình ảnh cho OCR với tự động xoay, nhị phân hoá và giảm
  nhiễu trong Python. Học cách trích xuất JSON có cấu trúc bằng công cụ OCR.
og_title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Python toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with auto‑rotate, binarization and denoising
    in Python. Get structured JSON output using an OCR engine.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
    text: '**Binarization** – converting the picture to pure black‑and‑white, which
      sharpens character edges.'
  - name: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
    text: '**Denoising** – removing speckles that the OCR engine might mistake for
      glyphs.'
  - name: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
    text: '**Add language packs** (`engine.set_language(''eng+spa'')`) for multilingual
      documents.'
  - name: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
    text: '**Integrate with Pandas** to turn the JSON tables into DataFrames for analytics.'
  - name: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
    text: '**Run batch processing** by looping over a folder of images and appending
      results to a master JSON file.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Python đầy đủ
url: /vi/python/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý hình ảnh cho OCR – Hướng dẫn Python đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **preprocess image for OCR** để engine thực sự đọc được những gì bạn thấy chưa? Bạn không đơn độc—hầu hết các nhà phát triển đều gặp cùng một vấn đề khi tài liệu đã quét của họ bị rối loạn. Tin tốt là gì? Một vài bước được đặt đúng chỗ—auto‑rotate, binarization và denoising—có thể biến một bức ảnh lộn xộn thành văn bản sạch, có thể đọc được bởi máy.

Trong hướng dẫn này, chúng ta sẽ đi qua một quy trình làm việc **Python** không chỉ làm sạch hình ảnh mà còn trả lại cho bạn một tệp JSON được cấu trúc đẹp mắt. Khi kết thúc, bạn sẽ biết cách auto‑rotate một hình ảnh cho OCR, áp dụng image binarization cho OCR, và thậm chí denoise dữ liệu hình ảnh OCR trước khi đưa vào một thể hiện **OCR engine Python**.

## Những gì bạn cần

- Python 3.9+ (bất kỳ phiên bản mới nào cũng hoạt động)
- `Pillow` để xử lý hình ảnh (`pip install pillow`)
- `ocrutil` – một thư viện tiện ích giả tưởng bao bọc OCR engine (cài đặt qua `pip install ocrutil`)
- Một hình ảnh lệch mẫu (`skewed.jpg`) đặt trong thư mục bạn có thể tham chiếu

Chỉ vậy—không có framework nặng, không có ma thuật GPU. Chỉ cần Python thuần túy và một vài thư viện tiện lợi.

## Bước 1: Tải hình ảnh của bạn – Chuẩn bị cho OCR

Điều đầu tiên cần làm: chúng ta cần một đối tượng hình ảnh mà phần còn lại của pipeline có thể xử lý.

```python
from PIL import Image
import ocrutil

# Load the image you want to process
img_path = "YOUR_DIRECTORY/skewed.jpg"
img = Image.open(img_path)          # Pillow gives us a convenient Image object
print(f"Loaded image size: {img.size}")
```

*Tại sao điều này quan trọng:* Tải hình ảnh bằng Pillow đảm bảo chúng ta giữ lại toàn bộ dữ liệu pixel gốc, điều này rất quan trọng khi chúng ta áp dụng binarization sau này. Bỏ qua bước này hoặc sử dụng bộ tải chất lượng thấp có thể làm hỏng độ chính xác của OCR.

## Bước 2: Auto‑rotate hình ảnh cho OCR (auto rotate image OCR)

Một bức ảnh chụp bằng điện thoại thường bị nghiêng hoặc thậm chí lộn ngược. Trợ giúp `ocrutil.auto_rotate` phát hiện đường cơ sở của văn bản và xoay hình ảnh cho phù hợp.

```python
# Automatically correct 90°/180° rotation
img = ocrutil.auto_rotate(img)
print("Auto‑rotation applied.")
```

*Mẹo chuyên nghiệp:* Nếu bạn biết tài liệu của mình luôn thẳng đứng, bạn có thể bỏ qua bước này, nhưng trong thực tế “auto rotate image OCR” giúp bạn tiết kiệm rất nhiều công việc dọn dẹp thủ công.

## Bước 3: Preprocess Image for OCR – Binarization + Denoising

Bây giờ chúng ta đến phần cốt lõi: **preprocess image for OCR**. Hai thủ thuật hiệu quả nhất là:

1. **Binarization** – chuyển đổi hình ảnh thành đen‑trắng thuần khiết, giúp làm sắc nét các cạnh ký tự.
2. **Denoising** – loại bỏ các đốm nhiễu mà OCR engine có thể nhầm lẫn thành glyphs.

```python
# Apply preprocessing: binarization + denoising
img = ocrutil.preprocess(img)   # Under the hood: thresholding + median filter
print("Preprocessing completed.")
```

Nếu bạn xem nhanh hình ảnh sau bước này (ví dụ, `img.show()`), bạn sẽ thấy độ tương phản mạnh mẽ với nền—đúng là những gì một OCR engine tốt cần.

## Bước 4: Thiết lập OCR Engine (OCR engine Python)

Với một hình ảnh sạch, chúng ta khởi tạo OCR engine. Lớp `ocrutil.OcrEngine` bao bọc một backend OCR nguồn mở phổ biến (nghĩ đến Tesseract) đồng thời cung cấp một API Python thân thiện.

```python
# Create and configure the OCR engine
engine = ocrutil.OcrEngine()
engine.set_image(img)           # Feed the preprocessed image
print("Engine ready for recognition.")
```

*Tại sao chúng ta làm điều này:* Cung cấp hình ảnh đã tiền xử lý cho đối tượng **OCR engine Python** đảm bảo engine làm việc với dữ liệu chất lượng cao nhất mà bạn có thể cung cấp, điều này trực tiếp dẫn đến độ chính xác cao hơn.

## Bước 5: Nhận dạng Văn bản Thuần (Tùy chọn nhưng Hữu ích)

Đôi khi bạn chỉ cần văn bản thô. Bước này là tùy chọn vì mục tiêu chính của hướng dẫn là đầu ra có cấu trúc, nhưng nó hữu ích cho các kiểm tra nhanh.

```python
# Get plain text (useful for debugging)
plain_text = engine.recognize()
print("Plain‑text output:\n", plain_text[:200])   # Print first 200 chars
```

Bạn sẽ thấy một chuỗi trông giống như tài liệu gốc, dù không có thông tin bố cục. Nếu văn bản bị rối, hãy quay lại và điều chỉnh các tham số tiền xử lý.

## Bước 6: Trích xuất Dữ liệu Có cấu trúc và Lưu dưới dạng JSON (OCR structured JSON output)

Sức mạnh thực sự của các OCR engine hiện đại là khả năng trả về thông tin bố cục—bảng, cột và thậm chí các trường biểu mẫu. `engine.recognize_structured()` làm đúng điều đó, và chúng ta sẽ ghi kết quả vào một tệp JSON gọn gàng.

```python
# Recognize structured data (tables, layout) and export to JSON
structured_result = engine.recognize_structured()
output_path = "YOUR_DIRECTORY/out.json"
ocrutil.save_result(structured_result, output_path)
print(f"Structured OCR result saved to {output_path}")
```

Một đoạn trích của JSON có thể trông như sau:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "type": "text",
          "bbox": [12, 34, 560, 120],
          "text": "Invoice #12345"
        },
        {
          "type": "table",
          "bbox": [15, 130, 580, 400],
          "rows": [
            ["Item", "Qty", "Price"],
            ["Widget A", "2", "$19.99"]
          ]
        }
      ]
    }
  ]
}
```

*Điều này mang lại cho bạn:* Một biểu diễn có thể đọc được bởi máy mà bạn có thể đưa thẳng vào cơ sở dữ liệu, API, hoặc công cụ báo cáo—không còn sao chép‑dán thủ công nữa.

## Bonus: Xác nhận trực quan (Image with Alt Text)

Dưới đây là ảnh chụp trước‑và‑sau của pipeline tiền xử lý. Hãy chú ý cách độ tương phản tăng lên và nhiễu biến mất.

![Tiền xử lý hình ảnh cho OCR – gốc vs đã làm sạch](/images/ocr_preprocess_example.png){: .align-center alt="ví dụ preprocess image for OCR"}

*Nếu bạn tò mò:* Thay thế `ocrutil.preprocess` bằng quy trình OpenCV của riêng bạn và bạn vẫn sẽ tuân theo cùng một triết lý **preprocess image for OCR**—ngưỡng, lọc, rồi đưa vào.

## Những Cạm Bẫy Thường Gặp & Cách Tránh

- **Over‑binarizing:** Đặt ngưỡng quá cao có thể xóa bỏ các ký tự mờ. Nếu bạn thấy thiếu chữ, hãy hạ ngưỡng trong `ocrutil.preprocess`.
- **Wrong DPI:** OCR engine giả định ~300 dpi cho tài liệu in. Nếu hình ảnh của bạn có độ phân giải thấp, hãy cân nhắc tăng kích thước trước khi tiền xử lý.
- **Skipping auto‑rotate:** Ngay cả độ nghiêng 5 độ cũng có thể làm sai lệch việc phát hiện dòng. Bước “auto rotate image OCR” ít tốn và tiết kiệm hàng giờ gỡ lỗi sau này.

## Mở rộng Quy trình làm việc

Bây giờ bạn đã có một nền tảng vững chắc, bạn có thể muốn:

1. **Add language packs** (`engine.set_language('eng+spa')`) cho tài liệu đa ngôn ngữ.  
2. **Integrate with Pandas** để chuyển các bảng JSON thành DataFrames cho phân tích.  
3. **Run batch processing** bằng cách lặp qua một thư mục hình ảnh và thêm kết quả vào tệp JSON chính.

Tất cả các mở rộng này vẫn dựa trên ý tưởng cốt lõi: **preprocess image for OCR** trước khi bạn gọi engine.

## Kết luận

Bạn vừa học cách **preprocess image for OCR** trong Python—auto‑rotate, binarize, denoise, và cuối cùng đưa hình ảnh sạch vào một **OCR engine Python** mà xuất ra cả văn bản thuần và **OCR structured JSON output** phong phú. Bằng cách làm theo các bước này, bạn sẽ cải thiện đáng kể tỷ lệ nhận dạng và có được dữ liệu sẵn sàng cho quá trình xử lý tiếp theo.

Sẵn sàng nâng cấp? Hãy thử thay thế `ocrutil.preprocess` tích hợp bằng một pipeline OpenCV tùy chỉnh, thử nghiệm các kỹ thuật binarization khác nhau, hoặc đưa JSON vào bảng điều khiển báo cáo. Không có giới hạn, và nền tảng bạn vừa xây dựng sẽ giúp bạn tránh gặp lại các vấn đề về chất lượng hình ảnh.

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn sắc nét!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích xuất Văn bản từ Hình ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)
- [Cách Đặt Giá trị Ngưỡng trong Nhận dạng Hình ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}