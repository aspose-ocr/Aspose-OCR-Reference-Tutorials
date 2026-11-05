---
category: general
date: 2026-06-22
description: Nhận dạng văn bản từ các tệp png bằng Aspose OCR trong Python. Học cách
  thực hiện OCR hàng loạt các hình ảnh và thiết lập các lớp GPU để xử lý nhanh hơn.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: vi
og_description: Nhận dạng văn bản từ các tệp PNG bằng Aspose OCR trong Python. Hướng
  dẫn này chỉ cách thực hiện OCR hàng loạt trên hình ảnh và thiết lập các lớp GPU
  để tăng tốc.
og_title: Nhận dạng văn bản từ PNG – Hướng dẫn Aspose OCR từng bước
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Nhận dạng văn bản từ PNG – Hướng dẫn đầy đủ với Aspose OCR & AI
url: /vi/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nhận dạng văn bản từ png – Hướng dẫn Aspose OCR & AI đầy đủ tính năng

Bạn đã bao giờ cần **nhận dạng văn bản từ png** nhưng lại gặp rắc rối trong các chi tiết cài đặt? Bạn không phải là người duy nhất. Dù bạn đang số hoá biên lai, quét mẫu đơn, hay chuyển ảnh chụp màn hình thành văn bản có thể tìm kiếm, việc thành thạo batch OCR images trong Python có thể tiết kiệm hàng giờ cho bạn.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ đã sẵn sàng chạy, không chỉ **nhận dạng văn bản từ png** mà còn cho bạn thấy cách **set GPU layers** để tăng tốc đáng kể. Khi hoàn thành, bạn sẽ có một script độc lập, giải thích rõ ràng từng bước, và một vài mẹo thực tế mà bạn có thể sao chép‑dán vào dự án của mình.

## Những gì hướng dẫn này bao phủ

- Cài đặt các gói Python Aspose OCR và Aspose AI  
- Cấu hình mô hình AI với việc tải tự động từ Hugging Face  
- Tạo một post‑processor nhỏ để sửa các lỗi OCR thường gặp  
- Chạy vòng lặp **batch OCR images** trên toàn bộ thư mục PNG  
- Sử dụng tùy chọn **set GPU layers** để tận dụng card đồ họa  
- Dọn dẹp tài nguyên một cách an toàn sau khi xử lý  

Không có dịch vụ bên ngoài, không có phép màu ẩn — chỉ có mã Python thuần túy mà bạn có thể đặt vào file `.py` và chạy.

![Diagram of recognize text from png workflow](workflow.png){alt="sơ đồ quy trình nhận dạng văn bản từ png"}

## Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Python 3.8+ | Các bánh xe Aspose AI nhắm vào các trình thông dịch mới |
| GPU tương thích CUDA (tùy chọn) | Cần nếu bạn muốn **set GPU layers** để tăng tốc |
| Kết nối Internet lần chạy đầu tiên | Mô hình sẽ tự động tải về từ Hugging Face |
| `pip` đã được cài đặt | Để tải các gói Aspose |

Nếu bạn đã có những thứ này, tuyệt vời — bạn đã sẵn sàng. Nếu chưa, các bước cài đặt dưới đây sẽ hướng dẫn bạn khắc phục.

---

## Bước 1: Cài đặt các gói Aspose OCR và Aspose AI

Đầu tiên, lấy các thư viện từ PyPI. Lệnh dưới đây sẽ tải cả engine OCR và trợ giúp AI trong một lần.

```bash
pip install aspose-ocr aspose-ai
```

*Pro tip:* Sử dụng môi trường ảo (`python -m venv .venv`) để các gói được cô lập khỏi cài đặt Python toàn cục của bạn.

---

## Bước 2: Tạo và cấu hình đối tượng Aspose AI

Thành phần AI cung cấp chế độ “thông minh” cho engine OCR. Chúng ta sẽ chỉ tới mô hình `Qwen/Qwen2.5-3B-Instruct-GGUF`, yêu cầu tải tự động nếu thiếu, và **set GPU layers** thành 30 (bạn có thể điều chỉnh sau).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Tại sao lại quan trọng:**  
- `allow_auto_download` loại bỏ bước tải thủ công một mô hình khoảng 2 GB.  
- `gpu_layers=30` yêu cầu transformer chạy 30 lớp đầu tiên trên GPU, giảm thời gian suy luận đáng kể khi có GPU tương thích.  
- Sử dụng lượng tử hoá `int8` giữ bộ nhớ thấp mà không làm giảm nhiều độ chính xác.

---

## Bước 3: Định nghĩa một Post‑Processor đơn giản để làm sạch lỗi OCR

OCR không hoàn hảo — đặc biệt với PNG độ phân giải thấp. Một cách nhanh là thay thế các ký tự thường bị nhận sai. Hàm dưới đây đổi “0” thành “o” và “1” thành “l”, một mẫu thường thấy trong hoá đơn đã quét.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Chúng ta sẽ gắn hàm này vào đối tượng AI ở bước tiếp theo để mọi kết quả nhận dạng đều tự động đi qua.

---

## Bước 4: Gắn Post‑Processor và Engine OCR

Bây giờ chúng ta kết nối mọi thứ: engine OCR, mô hình AI, và post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Đằng sau màn hình:**  
`OcrEngine` ủy thác công việc nặng cho mô hình AI bạn đã cấu hình. Sau khi mô hình trả về văn bản thô, Aspose gọi `fix_common_errors` để làm sạch đầu ra trước khi bạn nhận được.

---

## Bước 5: Batch OCR Images – Xử lý mọi PNG trong một thư mục

Đây là phần cốt lõi của hướng dẫn: một vòng lặp duyệt thư mục, tải mỗi file `.png`, chạy OCR, và in kết quả đã được làm sạch. Mẫu này là cách chuẩn để **batch OCR images** một cách hiệu quả.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Kết quả mong đợi** (ví dụ cho một biên lai):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Nếu bạn có hàng chục hoặc hàng trăm file, vòng lặp này sẽ xử lý chúng tuần tự, tái sử dụng cùng một instance AI để tránh việc tải mô hình lặp lại.

---

## Bước 6: Dọn dẹp – Giải phóng tài nguyên và hủy Engine

Khi hoàn thành, nên giải phóng bộ nhớ GPU và các tài nguyên gốc khác. Aspose cung cấp các phương thức rõ ràng để thực hiện việc này.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Bỏ qua bước này có thể để lại bộ nhớ GPU còn sót lại, dẫn đến lỗi hết bộ nhớ khi chạy script lần sau.

---

## Bonus: Điều chỉnh GPU Layers cho phần cứng khác nhau

Giá trị `gpu_layers` bạn đặt ở trên là điểm cân bằng cho nhiều GPU hiện đại, nhưng bạn có thể cần điều chỉnh:

| Bộ nhớ GPU (GB) | `gpu_layers` đề xuất |
|-----------------|----------------------|
| 4 GB hoặc ít hơn | 10‑15 |
| 6‑8 GB | 20‑30 |
| 12 GB+ | 35‑45 (hoặc cao hơn) |

Nếu bạn vượt quá bộ nhớ GPU, engine sẽ tự động chuyển các lớp còn lại sang CPU, vì vậy bạn sẽ không bị crash — chỉ chậm hơn. Hãy thử nghiệm và theo dõi việc sử dụng bằng `nvidia‑smi`.

---

## Những lỗi thường gặp & Cách tránh

1. **Tải mô hình thất bại** – Đảm bảo môi trường của bạn có thể truy cập `https://huggingface.co`. Proxy công ty có thể cần cấu hình (`https_proxy` env var).  
2. **GPU không được phát hiện** – Kiểm tra thư viện `torch` (được cài đặt như một phụ thuộc) có thấy GPU không: `import torch; print(torch.cuda.is_available())`. Nếu trả về `False`, cài bánh xe PyTorch tương thích CUDA.  
3. **Đường dẫn ảnh không đúng** – `Path.glob("*.png")` phân biệt chữ hoa/thường trên Linux. Dùng `*.PNG` hoặc `*.png` tương ứng, hoặc thêm `pathlib.Path(...).rglob("*.[pP][nN][gG]")` để an toàn.  
4. **Post‑processor quá mức** – Việc thay thế đơn giản có thể biến ký tự “0” thực sự thành “o”. Kiểm tra trên mẫu đại diện và điều chỉnh logic nếu cần.

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Chạy bằng:

```bash
python recognize_text_from_png_batch.py
```

Bạn sẽ thấy mỗi tên file PNG kèm theo văn bản đã trích xuất, chính xác như ví dụ ở trên.

---

## Kết luận

Chúng ta vừa đi qua một quy trình hoàn chỉnh, sẵn sàng sản xuất để **nhận dạng văn bản từ png** bằng Aspose OCR và Aspose AI trong Python. Bằng cách gói các bước vào một script sạch sẽ, bạn có thể dễ dàng **batch OCR images**, và nhờ vào `set gpu layers`


## Bạn nên học gì tiếp theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong bài viết này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}