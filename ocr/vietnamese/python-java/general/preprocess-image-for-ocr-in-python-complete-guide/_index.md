---
category: general
date: 2026-06-25
description: Tiền xử lý hình ảnh cho OCR và nhận dạng văn bản từ tài liệu quét bằng
  Python. Hướng dẫn từng bước kèm mã nguồn đầy đủ.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: vi
og_description: Tiền xử lý hình ảnh cho OCR và nhận dạng văn bản từ tài liệu quét
  bằng Python. Hãy theo dõi hướng dẫn chi tiết, có thể chạy được này.
og_title: Tiền xử lý hình ảnh cho OCR trong Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Tiền xử lý hình ảnh cho OCR trong Python – Hướng dẫn toàn diện
url: /vi/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý hình ảnh cho OCR trong Python – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **preprocess image for OCR** sao cho văn bản xuất ra sạch sẽ và đáng tin cậy? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp rắc rối tương tự khi trang quét bị nghiêng hoặc độ tương phản quá kém. Tin tốt là chỉ cần vài dòng Python là có thể làm thẳng bức ảnh, nhị phân hoá hình ảnh và trả lại cho bạn văn bản rõ ràng, có thể tìm kiếm được.

Trong tutorial này, chúng ta sẽ đi qua các bước chính để **preprocess image for OCR** *và* **recognize text from scanned document** bằng một thư viện OCR phổ biến. Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy, hiểu tại sao mỗi thiết lập lại quan trọng, và biết cách điều chỉnh cho những trường hợp khó.

## Những gì bạn cần

- Python 3.8 hoặc mới hơn (code cũng chạy trên 3.10+)
- Một gói OCR cung cấp các lớp `OcrEngine`, `ImagePreProcessingOptions` và `Image` (ví dụ: module giả `ocr` được dùng trong ví dụ)
- Một tài liệu đã được quét hoặc chụp ảnh có chút nghiêng hoặc độ tương phản thấp
- IDE yêu thích của bạn hoặc một terminal đơn giản—không cần GUI nặng

Đó là tất cả. Không cần binary bổ sung, không cần Docker. Hãy bắt đầu.

## Preprocess Image for OCR – Các bước chi tiết

Dưới đây là quy trình cốt lõi được chia thành năm giai đoạn rõ ràng. Mỗi giai đoạn bao gồm **lý do** thực hiện, **code** chính xác, và một **giải thích** ngắn gọn về những gì đang diễn ra phía sau.

### Bước 1: Tạo một thể hiện OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Lý do quan trọng:*  
Đối tượng `OcrEngine` là bộ não của toàn bộ quá trình. Nó chứa các cấu hình như gói ngôn ngữ, ngưỡng độ tin cậy, và—quan trọng nhất đối với chúng ta—các cờ tiền xử lý hình ảnh. Khởi tạo nó trước giúp chúng ta có một nền tảng sạch sẽ để bật các thủ thuật tiếp theo.

### Bước 2: Bật tính năng Tự động Định hướng và Nhị phân hoá

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Lý do quan trọng:*  
- **Deskewing** (định hướng) xoay ảnh sao cho các dòng văn bản trở nên ngang. Các engine OCR gặp khó khăn khi đường cơ sở nghiêng hơn vài độ.  
- **Binarization** (nhị phân hoá) chuyển ảnh thành đen‑trắng thuần túy, loại bỏ nhiễu nền có thể làm rối các bộ phân loại ký tự.  
Cả hai tùy chọn đều *tự động* trong nhiều thư viện hiện đại, nhưng bạn vẫn phải bật chúng—do đó cần gán giá trị một cách rõ ràng.

> **Mẹo chuyên nghiệp:** Nếu ảnh nguồn của bạn đã được căn chỉnh hoàn hảo, bạn có thể đặt `auto_deskew=False` để tiết kiệm một vài miligiây thời gian xử lý.

### Bước 3: Tải ảnh bị nghiêng mà bạn muốn xử lý

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Lý do quan trọng:*  
Phương thức `Image.load` đọc file vào bộ nhớ và gói nó trong một đối tượng mà OCR engine hiểu được. Nó cũng trích xuất siêu dữ liệu như DPI, có thể ảnh hưởng tới hệ số phóng đại mặc định cho việc định hướng.

> **Trường hợp đặc biệt:** Nếu ảnh là TIFF đa trang, bạn sẽ cần lặp qua từng trang hoặc dùng một helper như `ocr.MultiPageImage.load`. Các thiết lập tiền xử lý vẫn áp dụng cho mọi trang.

### Bước 4: Thực hiện OCR trên ảnh đã tiền xử lý

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Lý do quan trọng:*  
Ở thời điểm này, engine sẽ áp dụng các bước định hướng và nhị phân hoá mà chúng ta đã bật ở trên, sau đó chạy mạng nơ‑ron (hoặc pipeline kiểu Tesseract cổ điển) trên bitmap đã được làm sạch. Đối tượng `result` trả về thường chứa văn bản thuần, điểm tin cậy, và đôi khi cả dữ liệu vị trí cho mỗi từ.

> **Nếu văn bản vẫn bị rối?**  
Kiểm tra độ phân giải ảnh: OCR hoạt động tốt nhất ở 300 dpi hoặc cao hơn. Nếu nguồn của bạn thấp hơn, hãy cân nhắc tăng kích thước trước khi tải, hoặc yêu cầu bản quét gốc từ nguồn tài liệu.

### Bước 5: Xuất văn bản đã nhận dạng

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Lý do quan trọng:*  
`result.text` là chuỗi plain‑text đại diện cho mọi thứ engine có thể đọc được. In ra màn hình tiện cho việc gỡ lỗi nhanh; trong một ứng dụng thực tế bạn có thể ghi nó vào file `.txt`, cơ sở dữ liệu, hoặc đưa vào pipeline NLP tiếp theo.

---

## Recognize Text from Scanned Document – Đi xa hơn những kiến thức cơ bản

Bây giờ pipeline cơ bản đã hoạt động, hãy khám phá một vài biến thể phổ biến mà bạn có thể gặp khi **recognize text from scanned document** trong môi trường thực tế.

### 1. Xử lý đa ngôn ngữ

Nếu tài liệu của bạn chứa cả tiếng Anh và tiếng Pháp, hãy cấu hình engine trước bước 1:

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

Hầu hết các engine OCR chấp nhận mã ISO‑639‑2; tải thêm gói ngôn ngữ sẽ tăng nhẹ thời gian xử lý nhưng cải thiện đáng kể độ chính xác trên các trang đa ngôn ngữ.

### 2. Tinh chỉnh ngưỡng Nhị phân hoá

Nhị phân hoá tự động hoạt động cho hầu hết các trường hợp, nhưng một số bản sao cũ cần ngưỡng tùy chỉnh:

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Thử nghiệm với các giá trị từ 120 đến 220 cho tới khi nền biến mất mà không xóa các ký tự mờ.

### 3. Trích xuất thông tin bố cục

Đôi khi bạn cần nhiều hơn văn bản thô—bạn muốn biết mỗi đoạn nằm ở vị trí nào trên trang. Nhiều engine cung cấp một collection `result.blocks`:

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

Điều này vô giá khi tái tạo bảng hoặc giữ thứ tự cột.

### 4. Xử lý một loạt tệp

Nếu bạn có một thư mục chứa nhiều PDF đã quét và đã chuyển sang JPEG, hãy bọc toàn bộ luồng trong một vòng lặp:

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

Vòng lặp tái sử dụng cùng một thể hiện `engine`, hiệu quả hơn so với việc tạo mới cho mỗi tệp.

### 5. Đối phó với ảnh có độ phân giải thấp

Ảnh có độ phân giải thấp (< 150 dpi) thường tạo ra các ký tự mờ. Một cách khắc phục nhanh là tăng kích thước bằng thuật toán chất lượng cao trước khi đưa ảnh vào engine OCR:

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

Việc upscale không tạo ra chi tiết mới, nhưng bước nhị phân hoá sẽ làm việc tốt hơn với các cạnh sắc nét, mang lại một chút cải thiện.

---

## Kết quả mong đợi

Chạy script năm bước gốc trên một bản quét hơi nghiêng, 300 dpi sẽ in ra một kết quả giống như:

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Nếu bạn thấy ký tự bị rối, hãy kiểm tra lại các cờ tiền xử lý, độ phân giải ảnh và cấu hình ngôn ngữ.

---

## Kết luận

Chúng ta đã bao quát mọi thứ cần thiết để **preprocess image for OCR** và **recognize text from scanned document** bằng Python. Bắt đầu từ một thể hiện engine mới, chúng ta đã bật tự động định hướng và nhị phân hoá, tải ảnh nghiêng, chạy nhận dạng, và in ra văn bản sạch. Đồng thời, chúng ta đã khám phá hỗ trợ đa ngôn ngữ, điều chỉnh ngưỡng thủ công, trích xuất bố cục, xử lý batch, và giải pháp cho ảnh độ phân giải thấp.

Hãy thử script trên các tài liệu của bạn—có thể là một chồng biên lai, mẫu đơn viết tay, hoặc một mảnh báo cũ. Khi đã quen, hãy thử kết hợp tạo PDF hoặc đưa kết quả vào chỉ mục tìm kiếm. Khả năng là vô hạn.

**Sẵn sàng cho thử thách tiếp theo?** Kiểm tra các tutorial của chúng tôi về *“Extract Tables from Scanned PDFs with Python”* và *“Train Custom OCR Models with TensorFlow”* để mở rộng bộ công cụ tự động hoá tài liệu của bạn.

Chúc lập trình vui vẻ, và hy vọng OCR của bạn luôn sắc nét!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ, ví dụ hoạt động và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}