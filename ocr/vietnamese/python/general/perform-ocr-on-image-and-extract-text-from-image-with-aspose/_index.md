---
category: general
date: 2026-11-20
description: Thực hiện OCR trên hình ảnh bằng Aspose OCR và sau đó trích xuất văn
  bản từ hình ảnh bằng bộ xử lý hậu xử lý AI tích hợp. Học quy trình làm việc Python
  đầy đủ trong vài phút.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: vi
lastmod: 2026-11-20
og_description: Thực hiện OCR trên hình ảnh bằng Aspose OCR, sau đó trích xuất văn
  bản từ hình ảnh thông qua xử lý hậu AI. Hãy làm theo hướng dẫn Python từng bước
  này.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Thực hiện OCR trên hình ảnh và trích xuất văn bản từ hình ảnh bằng Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Thực hiện OCR trên hình ảnh và trích xuất văn bản từ hình ảnh bằng Aspose
url: /vi/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh và trích xuất văn bản từ hình ảnh bằng Aspose

Nếu bạn cần **perform OCR on image** các tệp trong Python, hướng dẫn này cho bạn một giải pháp toàn diện từ đầu đến cuối. Sử dụng Aspose OCR kết hợp với bộ xử lý hậu‑xử lý Aspose AI, bạn có thể đáng tin cậy **extract text from image** các tệp và cải thiện đầu ra OCR thô bằng một mô hình ngôn ngữ nhẹ.

Trong hướng dẫn này, bạn sẽ:

* Cài đặt engine Aspose OCR.
* Chạy OCR để **extract text from image**.
* Tùy chọn cấu hình mô hình AI cho việc hậu‑xử lý.
* Đăng ký một hàm post‑processor tùy chỉnh.
* Tạo ra văn bản được cải thiện và dọn dẹp tài nguyên.

Các bước này hoạt động với bất kỳ hình ảnh raster nào (PNG, JPEG, BMP) và chỉ yêu cầu gói `aspose-ocr`.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn có:

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Python 3.8+ | Yêu cầu bởi Aspose SDK. |
| `aspose-ocr` pip package | Cung cấp các lớp `AsposeOCR`, `AsposeAI`, và cấu hình mô hình. |
| An image file (e.g., `sample_image.png`) | Nguồn mà bạn sẽ **perform OCR on image**. |
| Optional: GPU support | Nếu bạn dự định chạy mô hình lớn hơn trên GPU, hãy đặt `gpu_layers` cho phù hợp. |

Cài đặt SDK bằng:

```bash
pip install aspose-ocr
```

## Bước 1: Thực hiện OCR trên hình ảnh

Hoạt động đầu tiên là đọc hình ảnh và lấy văn bản thô. Đây là bước cốt lõi **perform OCR on image**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Tại sao điều này hoạt động:** `AsposeOCR.recognize_image` chạy một mô hình nhận dạng ký tự quang học đã được huấn luyện trước, được tối ưu cho tốc độ và độ chính xác trên các phông chữ phổ biến. Phương thức trả về một chuỗi Unicode thuần, là cơ sở cho bất kỳ xử lý tiếp theo nào.

> **Mẹo chuyên nghiệp:** Nếu hình ảnh chứa nhiều ngôn ngữ, hãy đặt `ocr_engine.language = "eng+spa"` (hoặc bất kỳ mã ISO‑639‑2 nào được hỗ trợ) trước khi gọi `recognize_image`.

## Bước 2: Khởi tạo AI post‑processor

Aspose AI cung cấp một lớp hậu‑xử lý nhẹ có thể làm sạch các lỗi OCR, sửa dấu câu, hoặc áp dụng logic kinh doanh tùy chỉnh.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Tại sao bạn cần nó:** OCR thô thường nhận dạng sai ký tự (ví dụ, “0” so với “O”). Bước AI tinh chỉnh đầu ra, làm cho kết quả **extract text from image** đáng tin cậy hơn cho các tác vụ downstream như lập chỉ mục hoặc phân tích.

## Bước 3: (Tùy chọn) Cấu hình mô hình AI

Bạn có thể chỉ định bộ xử lý tới một mô hình Hugging Face cụ thể, bật tải xuống tự động, hoặc buộc thực thi trên CPU. Bước này là tùy chọn nhưng hữu ích khi bạn muốn hành vi xác định.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Giải thích:**  
* `allow_auto_download` giúp bạn tránh việc quản lý mô hình thủ công.  
* `hugging_face_repo_id` chọn một mô hình; `gpt2` là sự cân bằng tốt giữa kích thước và chất lượng cho việc sửa lỗi văn bản ngắn.  
* `gpu_layers` kiểm soát số lớp transformer chạy trên GPU; `0` buộc thực thi hoàn toàn trên CPU, an toàn trên mọi máy.

## Bước 4: Đăng ký hàm post‑processing tùy chỉnh

Aspose AI cho phép bạn chèn bất kỳ callable nào nhận chuỗi OCR thô và trả về phiên bản đã chuyển đổi. Dưới đây là một ví dụ đơn giản chuyển mọi thứ thành chữ hoa.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Khi nào nên tùy chỉnh:** Sử dụng hàm tùy chỉnh khi bạn cần làm sạch theo miền, chẳng hạn loại bỏ các định danh bí mật, chuẩn hoá ngày tháng, hoặc áp dụng các sửa lỗi dựa trên regex. Mô hình AI sẽ chạy *sau* hàm này, cho phép bạn kết hợp các quy tắc xác định với các cải tiến xác suất.

## Bước 5: Cải thiện kết quả OCR bằng AI post‑processor

Bây giờ chạy toàn bộ pipeline: văn bản OCR thô đầu tiên được truyền qua hàm tùy chỉnh của bạn, sau đó qua mô hình AI, và cuối cùng bạn nhận được đầu ra đã tinh chỉnh.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Kết quả bạn sẽ thấy:**  
Nếu hình ảnh gốc chứa “Hello world”, console có thể hiển thị:

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

Trong một kịch bản thực tế, mô hình AI sẽ sửa lỗi chính tả, thêm dấu câu thiếu, hoặc định dạng lại ngắt dòng, cung cấp cho bạn một kết quả **extract text from image** sạch hơn, sẵn sàng cho việc lưu trữ hoặc phân tích.

## Bước 6: Giải phóng tài nguyên khi hoàn thành

Cả engine OCR và AI post‑processor đều cấp phát tài nguyên gốc. Giải phóng chúng một cách rõ ràng tránh rò rỉ bộ nhớ, đặc biệt trong các dịch vụ chạy lâu.

```python
# Clean up native resources
ai_processor.free_resources()
```

Nếu bạn cũng khởi tạo `ocr_engine` với backend nặng, bạn có thể gọi `ocr_engine.dispose()` (nếu có) theo cách tương tự.

## Các biến thể phổ biến và trường hợp đặc biệt

| Tình huống | Điều chỉnh đề xuất |
|-----------|------------------------|
| **PDF lớn với nhiều trang** | Lặp qua mỗi trang, gọi `recognize_image` cho mỗi trang rasterized, và tổng hợp kết quả. |
| **Môi trường hỗ trợ GPU** | Đặt `model_config.gpu_layers` thành số lớp bạn muốn trên GPU (ví dụ, `4`). Đảm bảo driver CUDA đã được cài đặt. |
| **Văn bản không phải tiếng Anh** | Thay đổi `ocr_engine.language` thành mã ngôn ngữ phù hợp và, nếu cần, chọn mô hình Hugging Face đặc thù cho ngôn ngữ. |
| **Quét rất nhiễu** | Tiền xử lý hình ảnh bằng OpenCV (loại bỏ nhiễu, ngưỡng) trước khi gọi `recognize_image`. |
| **Cần giữ nguyên chữ hoa/thường gốc** | Thay thế hàm `my_post_processor` bằng một hàm không làm gì hoặc quy tắc tinh vi hơn thay vì `text.upper()`. |

## Ví dụ hoạt động đầy đủ

Kết hợp mọi thứ lại, đây là một script đơn lẻ bạn có thể chạy ngay (thay `YOUR_DIRECTORY/sample_image.png` bằng đường dẫn thực tế của bạn):

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

Chạy script này sẽ in cả đầu ra OCR thô và phiên bản được AI cải thiện, minh họa cách bạn có thể **perform OCR on image** các tệp và đáng tin cậy **extract text from image** trong một quy trình làm việc duy nhất, có thể tái tạo.

## Kết luận

Bây giờ bạn đã biết cách **perform OCR on image** các tệp với Aspose OCR, sau đó **extract text from image** bằng AI post‑processor tích hợp. Hướng dẫn đã bao gồm:

* Khởi tạo engine OCR.
* Chạy OCR để lấy văn bản thô.
* (Tùy chọn) cấu hình mô hình Hugging Face nhẹ.
* Thêm một

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [How to Correct OCR Errors – Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image Python – Complete Aspose OCR Guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}