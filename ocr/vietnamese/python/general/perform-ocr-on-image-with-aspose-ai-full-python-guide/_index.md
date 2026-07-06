---
category: general
date: 2026-06-19
description: Tìm hiểu cách thực hiện OCR trên hình ảnh bằng Aspose OCR và bộ xử lý
  hậu kỳ AI trong Python. Bao gồm mô hình tự động tải xuống, kiểm tra chính tả và
  tăng tốc GPU.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: vi
og_description: Thực hiện OCR trên hình ảnh bằng Aspose OCR và bộ xử lý hậu kỳ AI.
  Hướng dẫn từng bước với mô hình tự động tải xuống, kiểm tra chính tả và tăng tốc
  GPU.
og_title: Thực hiện OCR trên hình ảnh – Hướng dẫn Python đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Thực hiện OCR trên hình ảnh với Aspose AI – Hướng dẫn Python đầy đủ
url: /vi/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh – Hướng dẫn Python đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **thực hiện OCR trên hình ảnh** mà không phải vật lộn với hàng chục thư viện chưa? Theo kinh nghiệm của tôi, vấn đề thường là phải điều khiển một engine OCR thô, sau đó cố gắng làm sạch đầu ra nhiễu. May mắn là Aspose OCR cho Python kết hợp với bộ xử lý hậu AI giúp toàn bộ quy trình trở nên dễ dàng.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực tế, toàn diện, cho thấy chính xác cách **thực hiện OCR trên hình ảnh**, nâng cao độ chính xác với mô hình tự tải về, bật kiểm tra chính tả, và thậm chí tận dụng tăng tốc GPU khi có sẵn. Khi hoàn thành, bạn sẽ có một script có thể tái sử dụng và chèn vào bất kỳ dự án lập hoá đơn, quét biên lai, hay số hoá tài liệu nào.

## Những gì bạn sẽ xây dựng

Chúng ta sẽ tạo một chương trình Python nhỏ thực hiện:

1. Khởi tạo engine Aspose OCR và tải một hình ảnh hoá đơn mẫu.  
2. Thực hiện một lần OCR cơ bản và in ra văn bản thô.  
3. Cấu hình **Aspose AI** với **mô hình tự tải về** từ Hugging Face.  
4. Chạy **bộ xử lý hậu AI** (bao gồm **bộ kiểm tra chính tả**) để làm sạch đầu ra OCR.  
5. Giải phóng tất cả tài nguyên một cách sạch sẽ.

Không cần dịch vụ bên ngoài, không cần API key—chỉ vài dòng Python và sức mạnh của Aspose.

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng máy có GPU đủ mạnh, việc thiết lập `gpu_layers` có thể giảm vài giây cho bước xử lý hậu.

## Yêu cầu trước

- Python 3.8 hoặc mới hơn (mã sử dụng type hints nhưng không bắt buộc).  
- Gói `aspose-ocr` và `aspose-ai` được cài đặt qua `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Một hình ảnh mẫu (PNG, JPG, hoặc TIFF) được lưu ở vị trí bạn có thể tham chiếu, ví dụ `sample_invoice.png`.  
- (Tùy chọn) GPU hỗ trợ CUDA và driver phù hợp nếu bạn muốn **tăng tốc GPU**.

Bây giờ nền tảng đã sẵn sàng, hãy bắt đầu với mã.

![ví dụ thực hiện OCR trên hình ảnh](image.png)

## Thực hiện OCR trên hình ảnh – Bước 1: Khởi tạo engine OCR và tải hình ảnh

Điều đầu tiên chúng ta cần là một thể hiện engine OCR. Aspose OCR cung cấp một API hướng đối tượng sạch sẽ, trừu tượng hoá việc tiền xử lý hình ảnh cấp thấp.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Tại sao điều này quan trọng:**  
Việc đặt ngôn ngữ từ sớm cho engine biết bộ ký tự nào sẽ được mong đợi, giúp cải thiện tốc độ và độ chính xác nhận dạng. Nếu bạn làm việc với tài liệu đa ngôn ngữ, chỉ cần đổi `"en"` thành `"fr"` hoặc `"de"` tùy nhu cầu.

## Bước 2: Thực hiện OCR cơ bản và xem văn bản thô

Bây giờ chúng ta thực sự chạy quá trình nhận dạng. Đối tượng kết quả chứa văn bản thô, điểm tin cậy, và thậm chí các hộp bao quanh nếu bạn cần chúng sau này.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Kết quả điển hình có thể trông như sau (chú ý các ký tự bị đọc sai thỉnh thoảng):

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Bạn có thể thấy các số `0` ở nơi engine nghĩ là chữ “O”. Đó là lúc **bộ xử lý hậu AI** tỏa sáng.

## Cấu hình Aspose AI – mô hình tự tải về và kiểm tra chính tả

Trước khi đưa kết quả OCR thô cho lớp AI, chúng ta cần cho Aspose AI biết mô hình nào sẽ được sử dụng. Thư viện có thể tự động tải mô hình từ Hugging Face, vì vậy bạn không cần phải quản lý các tệp `.bin` lớn.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Giải thích các cài đặt**

| Cài đặt | Chức năng | Khi nào điều chỉnh |
|---------|-----------|--------------------|
| `allow_auto_download` | Cho phép Aspose tự động tải mô hình khi chạy lần đầu. | Giữ `true` trừ khi bạn đã tải trước để dùng offline. |
| `hugging_face_repo_id` | Định danh mô hình trên Hugging Face. | Thay bằng mô hình khác nếu bạn cần mô hình chuyên ngành. |
| `hugging_face_quantization` | Chọn mức lượng tử (`int8`, `float16`, v.v.). | Dùng `int8` cho môi trường bộ nhớ thấp; `float16` cho độ chính xác cao hơn. |
| `gpu_layers` | Số lớp transformer được thực thi trên GPU. | Đặt `0` để chỉ dùng CPU, hoặc giá trị lên tới tổng số lớp của mô hình (20 cho Qwen2.5‑3B). |

## Chạy bộ xử lý hậu AI trên kết quả OCR

Với engine đã sẵn sàng, chúng ta chỉ cần đưa đầu ra OCR thô vào pipeline AI. **Bộ kiểm tra chính tả** tích hợp sẽ sửa các lỗi chính tả rõ ràng, trong khi mô hình ngôn ngữ có thể diễn đạt lại hoặc bổ sung thông tin nếu bạn bật các bộ xử lý bổ sung sau này.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Kết quả mong đợi sau bước kiểm tra chính tả:

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Chú ý các số `0` đã được sửa thành chữ cái đúng, và “Am0unt” bị lỗi đã chuyển thành “Amount”. **Bộ xử lý hậu AI** hoạt động bằng cách gửi văn bản thô qua mô hình đã chọn, sau đó trả về phiên bản đã được tinh chỉnh dựa trên quá trình huấn luyện của nó.

### Trường hợp đặc biệt & Mẹo

- **Hình ảnh độ phân giải thấp**: Nếu engine OCR gặp khó khăn, hãy cân nhắc phóng to hình ảnh trước (`Pillow` có thể hỗ trợ) hoặc tăng `ocr_engine.ImagePreprocessingOptions`.  
- **Kịch bản không phải Latin**: Đổi `ocr_engine.Language` sang mã ISO thích hợp (`"zh"` cho tiếng Trung, `"ar"` cho tiếng Ả Rập).  
- **GPU không được phát hiện**: Cài đặt `gpu_layers` sẽ tự động chuyển sang CPU nếu không có GPU tương thích, vì vậy bạn không cần xử lý lỗi bổ sung.  
- **Giới hạn kích thước mô hình**: Mô hình Qwen2.5‑3B nén khoảng ~4 GB; hãy đảm bảo ổ đĩa của bạn có đủ không gian cho việc tự tải về.

## Giải phóng tài nguyên – tắt sạch sẽ

Các đối tượng Aspose giữ các handle gốc, vì vậy tốt nhất là giải phóng chúng khi đã xong. Điều này ngăn ngừa rò rỉ bộ nhớ, đặc biệt trong các dịch vụ chạy lâu dài.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Bạn có thể bọc toàn bộ script trong khối `try…finally` nếu muốn dọn dẹp một cách rõ ràng.

## Script đầy đủ – sao chép‑dán sẵn

Dưới đây là toàn bộ chương trình, sẵn sàng chạy sau khi bạn thay `YOUR_DIRECTORY` bằng đường dẫn tới hình ảnh của mình.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Chạy nó với:

```bash
python perform_ocr_on_image.py
```

Bạn sẽ thấy đầu ra thô và đã được làm sạch được in ra console.

## Kết luận


## Bạn nên học gì tiếp theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Trích xuất văn bản hình ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Chuyển đổi Hình ảnh thành Văn bản – Thực hiện OCR trên Hình ảnh từ URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}