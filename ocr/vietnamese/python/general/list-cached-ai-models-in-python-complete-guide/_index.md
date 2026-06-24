---
category: general
date: 2026-06-22
description: Tìm hiểu cách liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm bằng
  AI SDK trong Python. Bao gồm các bước để lấy thư mục bộ nhớ đệm của mô hình và quản
  lý các mô hình AI cục bộ một cách hiệu quả.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: vi
og_description: Liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm bằng Python sử
  dụng AI SDK. Thực hiện theo hướng dẫn từng bước này để lấy thư mục bộ nhớ đệm của
  mô hình và xử lý các mô hình AI cục bộ.
og_title: Danh sách các mô hình AI được cache trong Python – Hướng dẫn chi tiết
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Danh sách các mô hình AI được lưu trong bộ nhớ đệm bằng Python – Hướng dẫn
  toàn diện
url: /vi/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm bằng Python – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi cách **liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm** trên máy làm việc của mình mà không phải đào bới qua các thư mục khó hiểu chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi cần xác minh những mô hình nào đã được lưu cục bộ, đặc biệt khi làm việc với băng thông hạn chế hoặc triển khai offline. Trong hướng dẫn này, bạn sẽ thấy một cách nhanh chóng, không rườm rà để truy vấn AI SDK, in nội dung bộ nhớ đệm và khám phá chính xác vị trí của các tệp đó.

Chúng tôi cũng sẽ đề cập đến các chủ đề liên quan như **lấy thư mục bộ nhớ đệm của mô hình**, xử lý bộ nhớ đệm trống, và các thực hành tốt nhất cho **quản lý bộ nhớ đệm mô hình AI** trong các script sản xuất. Khi kết thúc, bạn sẽ có một đoạn mã tự chứa mà bạn có thể chèn vào bất kỳ dự án Python nào.

## Yêu cầu trước

- Python 3.8 hoặc mới hơn đã được cài đặt.
- AI SDK (gói `ai`) được cài đặt qua `pip install ai-sdk` hoặc kho nội bộ của tổ chức bạn.
- Kiến thức cơ bản về chạy script từ dòng lệnh.

Không cần thư viện bổ sung nào, vì vậy ví dụ vẫn nhẹ và di động.

---

## Liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm – Tổng quan nhanh

Điều đầu tiên bạn cần làm là nhập SDK và gọi các hàm trợ giúp của nó. SDK cung cấp hai phương thức hữu ích:

1. `ai.list_local()` – trả về một danh sách Python các định danh mô hình đã được lưu trong bộ nhớ đệm.
2. `ai.get_local_path()` – trả về thư mục tuyệt đối nơi các tệp mô hình đó nằm.

Cả hai lời gọi đều đồng bộ và ném ra một `AIError` rõ ràng nếu có gì sai, giúp việc xử lý lỗi trở nên đơn giản.

> **Tại sao nên sử dụng các hàm này?**  
> Biết chính xác tập hợp các mô hình đã được lưu trong bộ nhớ đệm giúp bạn tránh tải xuống không cần thiết, gỡ lỗi sự không khớp phiên bản, và tự động dọn dẹp các artefact cũ. Đây là một phần nhỏ trong quy trình **AI SDK Python** lớn hơn, nhưng nó có thể tiết kiệm cho bạn hàng giờ tìm kiếm thủ công trong hệ thống tệp.

### Bước 1: Nhập AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Tại sao điều này quan trọng:* Việc nhập gói đăng ký các C‑extension nền và tải các tệp cấu hình (như đường dẫn bộ nhớ đệm) từ môi trường của bạn. Bỏ qua bước này sẽ gây ra `ModuleNotFoundError` ngay khi bạn gọi bất kỳ hàm SDK nào.

### Bước 2: Liệt kê tất cả các mô hình đã được lưu trong bộ nhớ đệm

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Bạn sẽ thấy:** Nếu bạn có ba mô hình được lưu, đầu ra có thể trông như sau:

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Nếu bộ nhớ đệm trống, bạn sẽ nhận được một danh sách rỗng:

```
Cached models: []
```

> **Mẹo chuyên nghiệp:** Bao quanh lời gọi trong một khối try/except nếu bạn nghi ngờ SDK có thể chưa được khởi tạo đúng cách.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Bước 3: Lấy thư mục bộ nhớ đệm của mô hình

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Đầu ra điển hình trên hệ thống kiểu Unix:

```
Model cache directory: /home/you/.cache/ai/models
```

Trên Windows bạn có thể thấy một thứ gì đó như `C:\Users\you\AppData\Local\ai\models`. Biết đường dẫn này là cần thiết khi bạn cần **quản lý bộ nhớ đệm mô hình AI** một cách thủ công—có thể để xóa các phiên bản cũ hoặc sao chép tệp vào ổ đĩa chia sẻ.

---

## Tóm tắt trực quan

![Sơ đồ cho thấy cách liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm, lấy tên của chúng và xác định vị trí thư mục bộ nhớ đệm](https://example.com/images/list-cached-ai-models.png)

*Alt text:* Sơ đồ minh họa quy trình **liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm** bằng AI SDK trong Python.

## Xử lý các trường hợp biên và những bẫy thường gặp

### Bộ nhớ đệm trống

Nếu `ai.list_local()` trả về một danh sách rỗng, bạn có thể tự hỏi liệu SDK có được cấu hình sai không. Hãy kiểm tra lại biến môi trường `AI_CACHE_DIR` (hoặc tệp cấu hình của SDK) để chắc chắn nó trỏ tới một vị trí có thể ghi được.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Vấn đề quyền truy cập

Khi truy cập `ai.get_local_path()`, một `PermissionError` có thể xuất hiện trên các hệ thống có quyền hạn hạn chế. Cách khắc phục thường là chạy script với quyền người dùng thích hợp hoặc điều chỉnh ACL của thư mục.

### Sự không khớp phiên bản

Đôi khi bộ nhớ đệm chứa một phiên bản cũ hơn của mô hình trong khi mã của bạn yêu cầu một phiên bản mới hơn. SDK sẽ tự động tải xuống phiên bản mới, nhưng bạn có thể ngăn trước bằng cách kiểm tra thẻ phiên bản trong danh sách:

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Dọn dẹp các mô hình cũ

Nếu bạn cần giải phóng không gian, bạn có thể xóa trực tiếp thư mục mô hình cụ thể:

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

Chạy `purge_model('bert-base-uncased')` sẽ xóa mô hình đó và giải phóng không gian đĩa.

---

## Đoạn mã đầy đủ bạn có thể sao chép‑dán

Dưới đây là một script sẵn sàng chạy kết hợp tất cả các bước, thêm xử lý lỗi cơ bản, và in ra một bản tóm tắt thân thiện.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Kết quả mong đợi (khi bộ nhớ đệm đã được lấp đầy):**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Chạy script với `python list_models.py` và bạn sẽ ngay lập tức biết những gì đang có trên đĩa.

---

## Câu hỏi thường gặp

**Q: Điều này có hoạt động trên mọi hệ điều hành không?**  
A: Có. SDK trừu tượng hoá các đường dẫn riêng của OS, vì vậy `ai.get_local_path()` trả về một chuỗi hợp lệ trên Linux, macOS và Windows.

**Q: Tôi có thể liệt kê các mô hình từ bộ nhớ đệm từ xa không?**  
A: `list_local()` tích hợp chỉ báo cáo các artefact được lưu cục bộ. Đối với các registry từ xa, bạn sẽ sử dụng `ai.list_remote()` (nếu phiên bản SDK của bạn hỗ trợ).

**Q: Nếu tên SDK không phải là `ai` thì sao?**  
A: Thay dòng import bằng tên gói thực tế, ví dụ `import myai as ai`. Tất cả các lời gọi tiếp theo vẫn giữ nguyên vì hợp đồng API nhất quán giữa các triển khai.

---

## Kết luận

Bây giờ bạn đã có một phương pháp vững chắc, sẵn sàng cho sản xuất để **liệt kê các mô hình AI đã được lưu trong bộ nhớ đệm** bằng thư viện **AI SDK Python**, lấy **thư mục bộ nhớ đệm của mô hình**, và thậm chí dọn dẹp các tệp cũ. Kiến thức này giúp bạn giữ môi trường sạch sẽ, tránh tải xuống dư thừa, và gỡ lỗi các vấn đề phiên bản một cách dễ dàng.

Sẵn sàng cho bước tiếp theo? Hãy thử mở rộng script để tự động tải xuống các mô hình thiếu, hoặc tích hợp nó vào pipeline CI kiểm tra sức khỏe bộ nhớ đệm trước mỗi lần build. Khám phá các chiến lược **quản lý bộ nhớ đệm mô hình AI** sẽ làm cho các ứng dụng AI của bạn nhanh hơn và đáng tin cậy hơn.

Chúc lập trình vui vẻ, và chúc bộ nhớ đệm của bạn luôn gọn nhẹ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với các giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách xử lý hàng loạt ảnh OCR với List trong Aspose.OCR cho .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Trích xuất văn bản ảnh C# với lựa chọn ngôn ngữ bằng Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Cách trích xuất văn bản từ các tệp ZIP bằng Aspose.OCR cho .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}