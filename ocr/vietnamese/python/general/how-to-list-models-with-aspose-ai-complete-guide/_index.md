---
category: general
date: 2026-07-05
description: Cách liệt kê các mô hình với Aspose AI, bật tải tự động và tải mô hình
  Hugging Face trong Python. Hãy làm theo hướng dẫn từng bước này để thiết lập bộ
  nhớ đệm và bắt đầu sử dụng Aspose AI ngay hôm nay.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: vi
og_description: Cách liệt kê các mô hình với Aspose AI, bật tải tự động và tải mô
  hình Hugging Face. Học cách thiết lập bộ nhớ đệm và sử dụng Aspose AI trong vài
  phút.
og_title: Cách liệt kê các mô hình với Aspose AI – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Cách liệt kê các mô hình với Aspose AI – Hướng dẫn đầy đủ
url: /vi/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng dẫn đầy đủ cách liệt kê mô hình với Aspose AI

Câu hỏi “cách liệt kê mô hình với Aspose AI” xuất hiện ngay khi bạn bắt đầu thử nghiệm các mô hình ngôn ngữ lớn trong Python. Trong hướng dẫn này, chúng ta sẽ đi qua việc bật **tự động tải xuống**, cấu hình bộ nhớ đệm cục bộ, và kéo một mô hình trực tiếp từ Hugging Face—để bạn có thể khởi động nhanh mà không phải tìm kiếm file thủ công.

Nếu bạn từng tự hỏi *“làm sao tôi dùng Aspose cho AI dựa trên OCR?”* hoặc *“cách dễ nhất để thiết lập cache cho các file mô hình là gì?”* thì bạn đang ở đúng chỗ. Khi kết thúc, bạn sẽ có một script hoạt động đầy đủ, liệt kê mọi mô hình được lưu trữ cục bộ, tự động tải xuống những mô hình còn thiếu, và cho bạn biết chính xác vị trí các file trên đĩa.

---

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn bạn có:

- Python 3.9 hoặc mới hơn (thư viện sử dụng type hints cần trình thông dịch cập nhật)
- Truy cập `pip` để cài đặt gói **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Kết nối internet để tải lần đầu từ Hugging Face.
- Một thư mục để lưu cache mô hình (ví dụ: `./model_cache`).

Đó là tất cả—không cần container Docker bổ sung, không cần môi trường ảo nặng ngoài một cài đặt Python sạch.

---

## ## Cách liệt kê mô hình với Aspose AI

Trọng tâm của hướng dẫn này là khả năng **liệt kê mô hình** mà Aspose AI đã lưu cache cục bộ. Khi cache đã được thiết lập, thư viện có thể liệt kê mọi thứ nó biết, giúp việc gỡ lỗi và kiểm soát phiên bản trở nên dễ dàng.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Tại sao cách này hoạt động:**  
- `AsposeAI()` tạo điểm vào cấp cao mà giao tiếp với engine suy luận bên dưới.  
- `AsposeAIModelConfig()` chứa tất cả các tùy chọn bạn có thể điều chỉnh; đặt `allow_auto_download` thành `"true"` báo cho thư viện tự động tải các file còn thiếu từ kho mà bạn chỉ định.  
- `directory_model_path` là *thư mục cache*—nơi lưu trữ tất cả các binary đã tải về.  
- `initialize()` áp dụng cấu hình, thực hiện tải xuống lần đầu nếu cache trống.  
- Cuối cùng, `list_local()` quét thư mục cache và trả về một danh sách Python các định danh mô hình, chúng ta sẽ in ra.

### Kết quả mong đợi (lần chạy đầu)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Nếu bạn chạy script lần nữa, thư viện sẽ bỏ qua việc tải xuống và chỉ liệt kê mô hình đã có, chứng minh rằng **cách thiết lập cache** thực sự tiết kiệm thời gian cho các lần chạy tiếp theo.

---

## ## Bật tự động tải xuống cho các mô hình thiếu

Thường bạn sẽ làm việc với nhiều mô hình trong các dự án khác nhau. Việc kéo từng mô hình một cách thủ công từ Hugging Face có thể rất tẻ nhạt. Bằng cách bật tự động tải xuống, Aspose AI sẽ lo phần còn lại.

```python
cfg.allow_auto_download = "true"
```

> **Mẹo chuyên nghiệp:** Giữ `allow_auto_download` ở `"true"` **chỉ** trong môi trường phát triển hoặc CI. Trong môi trường production, bạn có thể khóa cache để tránh lưu lượng mạng không mong muốn.

Nếu sau này bạn muốn tắt tính năng này, chỉ cần đặt cờ về `"false"` trước khi gọi lại `initialize()`.

---

## ## Tải mô hình Hugging Face ngay khi cần

Dòng

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

cho Aspose AI biết kho lưu trữ từ xa nào để kéo. Thư viện hỗ trợ bất kỳ mô hình công khai nào trên Hugging Face cung cấp file GGUF. Muốn dùng mô hình khác? Thay đổi repo ID:

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Khi bạn chạy script, Aspose AI sẽ kiểm tra cache:

- **Nếu mô hình đã tồn tại**, nó sẽ tải ngay lập tức.  
- **Nếu chưa**, cờ tự động tải xuống sẽ kích hoạt việc tải về, lưu file dưới `directory_model_path`, và sau đó đăng ký để sử dụng ngay.

Cách tiếp cận này loại bỏ quy trình “tải‑xong‑chạy” hai bước mà nhiều tutorial buộc bạn phải làm.

---

## ## Cách sử dụng Aspose AI sau khi mô hình đã được liệt kê

Liệt kê mô hình chỉ là một phần của câu chuyện. Khi bạn biết mô hình đã có, bạn có thể bắt đầu suy luận:

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Tại sao điều này quan trọng:**  
- `run_inference()` trừu tượng hoá việc tokenization, batching và xử lý GPU.  
- Bằng cách truyền *tên mô hình* bạn lấy được từ `list_local()`, bạn đảm bảo lời gọi suy luận khớp chính xác với file trên đĩa.

---

## ## Cách thiết lập vị trí cache cho nhiều dự án

Nếu bạn quản lý nhiều dự án, có thể muốn mỗi dự án có thư mục cache riêng. Trường `directory_model_path` chỉ là một chuỗi đơn giản, vì vậy bạn có thể xây dựng nó một cách động:

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Bây giờ mỗi dự án sẽ có một thư mục con riêng (`./model_cache/sentiment_analysis`), ngăn chặn xung đột phiên bản và giúp việc dọn dẹp trở nên đơn giản.

---

## ## Những lỗi thường gặp và cách tránh

| Triệu chứng | Nguyên nhân khả dĩ | Giải pháp |
|------------|---------------------|-----------|
| **`PermissionError` khi truy cập cache** | Thư mục cache thuộc sở hữu người dùng khác (thường trên máy chủ chung) | Tạo thư mục thủ công với quyền phù hợp: `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Mô hình không xuất hiện trong `list_local()`** | `allow_auto_download` được đặt thành `"false"` và mô hình chưa được cache | Bật tạm thời cờ, chạy một lần, sau đó tắt lại nếu muốn |
| **Phiên bản mô hình không mong muốn** | Hai repo khác nhau có cùng tên nhưng file khác nhau | Ghim chính xác repo ID (kèm tag/commit) hoặc khóa cache bằng cách tắt tự động tải xuống sau lần kéo thành công đầu tiên |
| **Lỗi thiếu bộ nhớ** | Các file GGUF lớn trên máy không đủ RAM/VRAM | Dùng mô hình nhỏ hơn (ví dụ: `Qwen2.5-1.5B`) hoặc đặt `cfg.device = "cpu"` để buộc suy luận trên CPU |

---

## ## Script đầy đủ bạn có thể sao chép‑dán

Dưới đây là ví dụ hoàn chỉnh, sẵn sàng chạy, tích hợp tất cả các khái niệm đã trình bày. Lưu lại dưới tên `list_models_demo.py` và thực thi bằng `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**Khi chạy** script sẽ tạo ra đầu ra tương tự như ví dụ trước, tiếp theo là một câu trả lời ngắn gọn từ mô hình. Bạn có thể thay đổi prompt tùy ý—đây là cách nhanh nhất để kiểm tra mô hình thực sự có thể sử dụng sau khi bạn **đã biết cách liệt kê mô hình**.

---

## ## Tóm tắt

Chúng ta đã bao quát mọi thứ cần thiết để **liệt kê mô hình** bằng Aspose AI, từ việc bật **tự động tải xuống** đến cấu hình **cache** bền vững và kéo **mô hình Hugging Face** khi cần. Những điểm chính:

1. Tạo đối tượng `AsposeAI` và `AsposeAIModelConfig`.  
2. Đặt `allow_auto_download = "true"` và chỉ định `directory_model_path` tới thư mục bạn kiểm soát.  
3. Khởi tạo AI, sau đó gọi `list_local()` để xem chính xác những gì đã được cache.  
4. Sử dụng tên mô hình đã liệt kê cho việc suy luận, và bạn đã sẵn sàng xây dựng các ứng dụng thực tế.

---

## Điều gì tiếp theo?

- **Thử nghiệm với các mô hình khác** – thay `cfg.hugging_face_repo_id` bằng repo khác và quan sát danh sách thay đổi.  
- **Tinh chỉnh cache


## Bạn nên học gì tiếp theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn hoạt động đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Set Aspose OCR License and Verify It in Java](/ocr/english/java/ocr-basics/set-license/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}