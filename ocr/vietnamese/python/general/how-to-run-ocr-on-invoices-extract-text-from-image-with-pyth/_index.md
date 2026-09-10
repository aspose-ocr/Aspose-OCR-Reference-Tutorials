---
category: general
date: 2026-01-07
description: Cách chạy OCR và trích xuất văn bản từ hình ảnh cho việc xử lý hoá đơn.
  Tìm hiểu cách cải thiện độ chính xác của OCR, tải hình ảnh cho OCR và xử lý OCR
  hoá đơn một cách hiệu quả.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: vi
og_description: Cách thực hiện OCR trên hoá đơn từng bước. Trích xuất văn bản từ hình
  ảnh, cải thiện độ chính xác OCR và tải hình ảnh cho OCR bằng Aspose AI.
og_title: Cách chạy OCR trên hoá đơn – Hướng dẫn Python đầy đủ
tags:
- OCR
- Python
- Image Processing
title: Cách chạy OCR trên hoá đơn – Trích xuất văn bản từ hình ảnh bằng Python
url: /vi/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chạy OCR trên hoá đơn – Trích xuất văn bản từ hình ảnh bằng Python

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một hoá đơn đã quét và nhận được văn bản sạch, có thể tìm kiếm chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi đầu ra OCR thô đầy lỗi chính tả, ngắt dòng lộn xộn và thiếu dấu câu. Trong hướng dẫn này, chúng tôi sẽ trình bày một giải pháp toàn diện không chỉ **trích xuất văn bản từ hình ảnh** mà còn **cải thiện độ chính xác OCR** bằng việc xử lý hậu kỳ với mô hình AI của Aspose.

Bạn sẽ thấy cách **tải ảnh cho OCR**, chạy engine tích hợp, và sau đó áp dụng một công cụ kiểm tra chính tả nhẹ nhàng giúp kết quả sẵn sàng cho các phân tích downstream. Khi kết thúc, bạn sẽ có một script có thể tái sử dụng và chèn vào bất kỳ pipeline xử lý hoá đơn nào.

> **Bạn sẽ cần**  
> * Python 3.9 hoặc mới hơn  
> * Các gói `aspose-ocr` và `aspose-ai` (cài đặt qua `pip`)  
> * Một ảnh hoá đơn (PNG, JPEG, hoặc TIFF) – chúng tôi sẽ dùng `sample_invoice.png` làm ví dụ  
> * Tùy chọn: GPU có ít nhất 4 GB VRAM để tăng tốc suy luận mô hình (script cũng chạy trên CPU)

---

## Bước 1: Cài đặt các gói cần thiết và chuẩn bị môi trường

Trước khi chúng ta có thể **tải ảnh cho OCR**, chúng ta phải chắc chắn các thư viện cần thiết đã sẵn sàng. Engine OCR của Aspose đi kèm với một wrapper Python đơn giản, trong khi bộ xử lý hậu kỳ AI dựa trên mô hình quantized của Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Mẹo chuyên nghiệp:** Nếu bạn dự định sử dụng tăng tốc GPU, cài đặt `torch` với hỗ trợ CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Bước 2: Tải ảnh hoá đơn

Việc tải ảnh rất đơn giản, nhưng cần lưu ý tại sao chúng ta đặt đường dẫn dưới dạng raw string (`r"..."`). Điều này ngăn ngừa các lỗi ký tự escape không mong muốn trên đường dẫn Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Tại sao điều này quan trọng:* Sử dụng `ocr.Image.load` đảm bảo ảnh được tiền xử lý (binarization, deskew) theo các mặc định tối ưu của Aspose, vốn đã **cải thiện độ chính xác OCR** trước khi bất kỳ phép thuật AI nào diễn ra.

---

## Bước 3: Chạy Engine OCR tích hợp

Bây giờ chúng ta thực sự **chạy OCR** và lấy văn bản thô. Bước này hiển thị đầu ra điển hình bạn nhận được từ một lần chạy OCR thông thường—thường là một mớ hỗn độn của ngắt dòng và đôi khi lỗi chính tả.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Typical raw output** (truncated for brevity):

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Bạn có thể nhận thấy từ “Invoice” xuất hiện dưới dạng “Invo1ce” hoặc thiếu dấu câu. Đó là lúc bộ xử lý hậu kỳ AI can thiệp.

---

## Bước 4: Cấu hình mô hình AI Aspose

Mô hình AI chúng ta sẽ dùng là **Qwen2.5‑3B‑Instruct‑GGUF**, một LLM nhẹ được tinh chỉnh theo hướng dẫn, chạy thoải mái trên GPU tầm trung. Cấu hình dưới đây cho Aspose biết nơi tải mô hình, số lớp giữ trên GPU, và kích thước ngữ cảnh để xử lý các đoạn văn dài.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Tại sao cấu hình này?**  
> * `gpu_layers=30` cân bằng tốc độ và bộ nhớ—hầu hết suy luận diễn ra trên GPU, trong khi các lớp còn lại ở CPU để tránh lỗi OOM.  
> * `context_size=4096` đảm bảo mô hình có thể nhìn toàn bộ hoá đơn một lúc, ngăn nó cắt ngắn các trường quan trọng.

---

## Bước 5: Tạo bộ xử lý hậu kỳ Kiểm tra Chính tả đơn giản

Chúng ta sẽ bao bọc lời gọi AI trong một hàm nhỏ tên `simple_spell_check`. Prompt được viết ngắn gọn: “Correct spelling and punctuation:” (Sửa lỗi chính tả và dấu câu) kèm theo văn bản OCR thô. Mô hình sẽ trả về phiên bản đã được làm sạch.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Cách hoạt động:** `ai.run_prompt` gửi prompt tới LLM đã tải cục bộ, sau đó trả về một chuỗi duy nhất với chính tả đã sửa, dấu câu đúng, và bố cục ngắt dòng tự nhiên hơn.

---

## Bước 6: Áp dụng bộ xử lý hậu kỳ lên văn bản OCR thô

Bây giờ phép màu xảy ra. Chúng ta đưa đầu ra OCR thô vào bộ xử lý hậu kỳ và in kết quả đã được cải thiện.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Sample enhanced output**:

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Chú ý tới việc sửa đúng từ “Invoice”, sử dụng dấu hai chấm đúng cách, và các ngắt dòng nhất quán—đúng những gì bạn cần cho việc phân tích downstream đáng tin cậy.

---

## Bước 7: Dọn dẹp tài nguyên

Cả engine OCR và mô hình AI đều cấp phát tài nguyên gốc. Thực hành tốt là giải phóng chúng khi hoàn thành, đặc biệt trong các dịch vụ chạy lâu.

```python
ai.free_resources()
engine.dispose()
```

---

## Toàn bộ Script – Sẵn sàng dán

Dưới đây là script hoàn chỉnh, có thể chạy được, liên kết mọi bước lại với nhau. Lưu lại với tên `invoice_ocr.py`, thay `YOUR_DIRECTORY` bằng thư mục chứa ảnh hoá đơn của bạn, và chạy bằng `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Chạy script và bạn sẽ thấy cả bản dump OCR thô ồn ào và phiên bản đã được tinh chỉnh, **cải thiện độ chính xác OCR**, hiển thị cạnh nhau.

---

## Câu hỏi thường gặp & Trường hợp đặc biệt

### 1. Nếu ảnh hoá đơn của tôi là PDF đa trang thì sao?

Aspose OCR có thể tải trực tiếp các trang PDF. Thay dòng tải ảnh bằng:

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Lặp lại `page_index` để xử lý từng trang theo thứ tự.

### 2. GPU của tôi hết bộ nhớ—có thể chỉ dùng CPU không?

Chắc chắn. Đặt `gpu_layers=0` trong `AsposeAIModelConfig`. Mô hình sẽ chạy hoàn toàn trên CPU, chậm hơn nhưng an toàn cho phần cứng yếu.

### 3. Làm sao để xử lý hoá đơn không phải tiếng Anh?

Thay ID kho mô hình bằng mô hình chuyên ngôn ngữ, ví dụ `"mistralai/Mistral-7B-Instruct-v0.2"` để hỗ trợ đa ngôn ngữ. Các phần còn lại của pipeline không thay đổi.

### 4. Tôi có thể xâu chuỗi nhiều bộ xử lý hậu kỳ (ví dụ, định dạng ngày, trích xuất tổng) không?

Có. `ai.set_post_processor` chấp nhận một danh sách các callable. Ví dụ:

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

Kết quả sẽ đầu tiên được kiểm tra chính tả, sau đó mới trích xuất tổng.

---

## Mẹo hiệu năng & Thực hành tốt

| Tip | Why it Helps |
|-----|---------------|
| **Xử lý hàng loạt nhiều hoá đơn** – tải chúng vào danh sách và xử lý trong vòng lặp. | Giảm tải cho interpreter Python và giữ mô hình AI luôn nóng trong bộ nhớ. |
| **Cache mô hình** – tránh gọi `initialize` liên tục trong dịch vụ web. | Việc tải mô hình có thể mất ~30 giây; cache giúp phản hồi ngay lập tức. |
| **Thu nhỏ ảnh lớn** xuống độ rộng 1500 px trước khi OCR. | Ảnh nhỏ hơn tăng tốc cả OCR và suy luận AI mà không làm giảm độ chính xác. |
| **Đặt `allow_auto_download="false"` trong môi trường production** – đóng gói mô hình cùng với triển khai. | Đảm bảo thời gian khởi động xác định và tránh lỗi mạng. |

---

## Kết luận

Chúng tôi đã trình bày **cách chạy OCR** trên hoá đơn, từ việc tải ảnh đến việc tinh chỉnh kết quả bằng kiểm tra chính tả dựa trên AI. Bằng cách làm theo các bước này, bạn có thể một cách đáng tin cậy **trích xuất văn bản từ hình ảnh**, **cải thiện độ chính xác OCR**, và dễ dàng **xử lý OCR hoá đơn** trong bất kỳ workflow nào dựa trên Python.

Hãy thử với một vài mẫu hoá đơn khác nhau—có thể là biên lai viết tay hoặc hợp đồng đã quét. Pipeline này thích nghi với ít thay đổi, chứng minh rằng sự kết hợp OCR + AI được cấu trúc tốt là công cụ đa năng cho bất kỳ dự án tự động hoá tài liệu nào.

Nếu bạn thấy hướng dẫn này hữu ích, hãy chia sẻ với đồng nghiệp hoặc đánh dấu sao cho repository chứa các gói Aspose.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}