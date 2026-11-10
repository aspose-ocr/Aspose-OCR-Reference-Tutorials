---
category: general
date: 2026-06-25
description: Tìm hiểu cách thực hiện OCR trong Python, khám phá cách tải hình ảnh
  tối ưu cho OCR, và nâng cao độ chính xác bằng xử lý hậu kỳ AI của Aspose.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: vi
og_description: Cách thực hiện OCR trong Python? Hãy theo hướng dẫn này để tải ảnh
  cho OCR, chạy nhận dạng cơ bản và cải thiện kết quả bằng xử lý hậu kỳ AI của Aspose.
og_title: Cách thực hiện OCR trong Python – Hướng dẫn đầy đủ về Aspose OCR & AI
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Cách thực hiện OCR trong Python – Hướng dẫn toàn diện Aspose OCR & AI
url: /vi/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện OCR trong Python – Hướng Dẫn Toàn Diện Aspose OCR & AI

Bạn đã bao giờ tự hỏi **cách thực hiện OCR** trong Python mà không phải vật lộn với các thủ thuật ảnh mức thấp chưa? Bạn không phải là người duy nhất. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn cách tải ảnh để OCR, thực hiện trích xuất văn bản thô, và sau đó tinh chỉnh kết quả bằng bộ xử lý hậu kỳ AI của Aspose. Khi kết thúc, bạn sẽ có một script sẵn sàng sử dụng để biến các bản scan nhiễu thành văn bản sạch, có thể tìm kiếm — không cần dịch vụ bổ sung.

Chúng tôi sẽ bao quát mọi thứ từ cài đặt SDK đến việc giải phóng tài nguyên trong các ứng dụng chạy lâu dài. Nếu bạn đã từng cố gắng **load image for OCR** và nhận được một mớ hỗn độn, hướng dẫn này là liều thuốc giải cứu. Bạn sẽ thấy tại sao việc kết hợp OCR truyền thống với mô hình ngôn ngữ mang lại kết quả trông như được gõ bởi con người.

## Prerequisites

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- Python 3.9 hoặc mới hơn (mã sử dụng type hints mà các trình thông dịch cũ không hỗ trợ)
- Giấy phép Aspose OCR đang hoạt động hoặc bản dùng thử miễn phí (phiên bản cộng đồng dùng để đánh giá)
- GPU có ít nhất 4 GB VRAM nếu bạn muốn tăng tốc mô hình AI (tùy chọn nhưng hữu ích)
- Một ảnh mẫu, ví dụ `sample_invoice.png`, được đặt ở nơi bạn có thể tham chiếu

Nếu bất kỳ mục nào trong số này còn lạ, đừng hoảng sợ — cài đặt SDK chỉ cần một dòng lệnh, và cài đặt GPU có thể tắt sau.

## Step 1: Install Aspose OCR and Dependencies

Mở terminal và chạy:

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Gói đầu tiên cung cấp `aspose.ocr`, gói thứ hai thêm các tiện ích AI post‑processor. Cả hai đều là wheel Python thuần, vì vậy bạn không cần biên dịch gì thêm.

## Step 2: Load Image for OCR and Initialise the Engine

Bây giờ chúng ta sẽ **load image for OCR** bằng `OcrEngine` của Aspose. Hãy tưởng tượng việc này như việc đưa một tờ giấy cho một nhân viên thư ký siêng năng đọc mọi ký tự.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Why this matters:** Lệnh `load_image` là cầu nối giữa hệ thống tệp của bạn và engine OCR. Nếu đường dẫn sai, bạn sẽ nhận được `FileNotFoundError` trước khi bất kỳ quá trình nhận dạng nào bắt đầu. Luôn kiểm tra kỹ các dấu phân cách thư mục, đặc biệt trên Windows so với macOS/Linux.

## Step 3: Set Up the Aspose AI Post‑Processor

Aspose AI có thể tải xuống một mô hình ngôn ngữ từ Hugging Face, lưu bộ nhớ đệm cục bộ, và thực hiện suy luận trên GPU (hoặc CPU). Dưới đây chúng ta cấu hình một mô hình nhẹ 3 tỷ tham số, phù hợp với hầu hết các laptop hiện đại.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Tip:** Nếu bạn đang dùng máy chỉ có CPU, đặt `gpu_layers = 0`. Mô hình vẫn sẽ chạy, chỉ chậm hơn một chút. Phép lượng tử `int8` giữ dung lượng bộ nhớ rất nhỏ trong khi vẫn duy trì hầu hết độ chính xác của mô hình.

## Step 4: Register a Custom Post‑Processor

Mô hình AI cần một prompt để biết phải làm gì. Ở đây chúng ta yêu cầu nó hành động như một người kiểm tra OCR, sửa lỗi chính tả, ghép các từ bị tách, và loại bỏ các artefact.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Why a custom processor?** Bộ xử lý hậu kỳ mặc định có thể thêm các giải thích hoặc định dạng không cần thiết. Bằng cách cung cấp hàm riêng của chúng ta, chúng ta giữ đầu ra chỉ là văn bản đã được làm sạch, rất phù hợp cho việc lập chỉ mục downstream hoặc lưu trữ trong cơ sở dữ liệu.

## Step 5: Run the AI‑Enhanced OCR Pipeline

Bây giờ chúng ta đưa đầu ra OCR thô vào lớp AI. Engine sẽ gọi `correction_processor` của chúng ta, hàm này sẽ giao tiếp với mô hình ngôn ngữ.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Bạn sẽ thấy cải thiện đáng kể: các ký tự thiếu được khôi phục, các lỗi nhận dạng thường gặp như “0” so với “O” được sửa, và các ngắt dòng trở nên hợp lý hơn.

## Step 6: Clean‑Up – Free Resources

Nếu bạn dự định chạy đoạn mã này trong một dịch vụ web hoặc daemon chạy lâu, việc giải phóng bộ nhớ GPU là rất quan trọng. Quên gọi `free_resources` có thể gây ra lỗi “out‑of‑memory” sau vài trăm yêu cầu.

```python
ocr_ai.free_resources()
```

Xong rồi — pipeline OCR đầy đủ của bạn đã sẵn sàng cho môi trường production.

## Full Script Recap

Dưới đây là ví dụ hoàn chỉnh, có thể chạy ngay. Sao chép‑dán vào một file tên `ocr_with_ai.py`, điều chỉnh đường dẫn ảnh, và chạy `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Expected Output

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Chú ý cách “Inv0ice” biến thành “Invoice” và ký tự “O” lẻ phía sau số tiền biến mất. Đó là AI đang thực hiện phép màu của nó.

## Common Questions & Edge Cases

### What if I don’t have a GPU?

Đặt `model_config.gpu_layers = 0` và tùy chọn tăng `model_config.context_size` lên 2048 để cải thiện hiệu năng CPU. Mô hình sẽ chạy chậm hơn, nhưng bạn vẫn nhận được cùng chất lượng sửa lỗi.

### My image is rotated—will `load_image` handle it?

Aspose OCR tự động phát hiện hướng, nhưng đối với các bản scan nghiêng quá mức, bạn có thể muốn quay trước bằng Pillow:

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### How do I process multiple files in a folder?

Bao bọc toàn bộ pipeline trong một vòng `for` và lưu mỗi `enhanced_text` vào danh sách hoặc ghi trực tiếp vào CSV. Nhớ gọi `ocr_ai.free_resources()` **một lần** sau vòng lặp, không phải sau mỗi file — việc khởi tạo lại mô hình liên tục sẽ lãng phí tài nguyên.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Can I swap the language model?

Chắc chắn. Chỉ cần thay đổi `model_config.hugging_face_repo_id` thành bất kỳ mô hình GGUF‑compatible nào trên Hugging Face (ví dụ `Meta/Llama-3.2-1B-Instruct-GGUF`). Giữ cài đặt lượng tử nhất quán với phần cứng của bạn.

## Pro Tips & Pitfalls

- **Pro tip:** Đặt `temperature=0.0` để có các sửa chữa quyết định. Nhiệt độ cao hơn có thể tạo ra các thay đổi sáng tạo nhưng không chính xác.
- **Watch out for:** Tài liệu cực dài (> 5000 ký tự). Cửa sổ ngữ cảnh của mô hình giới hạn ở 1024 token trong ví dụ; hãy chia văn bản thành các đoạn trước khi gửi tới AI.
- **Security note:** Nếu bạn chạy trong môi trường được quy định, hãy chắc chắn URL tải mô hình được đưa vào whitelist. Cờ `allow_auto_download` có thể

## What Should You Learn Next?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ, ví dụ hoạt động và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách sử dụng AspOCR: Tiền xử lý Bộ lọc OCR cho .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Trích xuất Văn bản hình ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}