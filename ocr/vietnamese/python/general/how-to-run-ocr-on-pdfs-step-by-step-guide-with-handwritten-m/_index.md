---
category: general
date: 2026-01-12
description: Cách chạy OCR trên PDF bằng Aspose OCR, tải OCR PDF, bật chế độ OCR viết
  tay và tích hợp mô hình OCR của Hugging Face để xử lý hậu kỳ.
draft: false
keywords:
- how to run OCR
- load pdf OCR
- handwritten OCR mode
- hugging face OCR model
language: vi
og_description: Cách chạy OCR trên PDF bằng Aspose OCR, bật chế độ OCR viết tay và
  tăng độ chính xác bằng mô hình OCR của Hugging Face.
og_title: Cách chạy OCR trên PDF – Hướng dẫn đầy đủ
tags:
- OCR
- Python
- Aspose
- Hugging Face
title: Cách chạy OCR trên PDF – Hướng dẫn từng bước với chế độ viết tay
url: /vi/python/general/how-to-run-ocr-on-pdfs-step-by-step-guide-with-handwritten-m/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chạy OCR trên PDF – Hướng dẫn đầy đủ

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một tệp PDF đa ngôn ngữ chứa chữ viết tay lộn xộn chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như số hoá hoá đơn hoặc lưu trữ các lá thư lịch sử—việc trích xuất văn bản thuần túy không đủ. Hướng dẫn này sẽ chỉ cho bạn cách chạy OCR trên PDF, tải PDF OCR, chuyển sang chế độ OCR chữ viết tay, và sau đó tinh chỉnh kết quả bằng một **mô hình OCR của Hugging Face** để sửa lỗi chính tả và ngữ pháp.

Chúng tôi sẽ hướng dẫn mọi thứ bạn cần: từ cài đặt Aspose OCR Cloud SDK, cấu hình tăng tốc GPU, đến việc tích hợp mô hình Qwen nhẹ từ Hugging Face. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy mà bạn có thể đưa vào bất kỳ dự án Python nào.

> **Yêu cầu trước**  
> • Python 3.9 hoặc mới hơn  
> • Giấy phép Aspose OCR Cloud (đặt dưới dạng biến môi trường)  
> • Tùy chọn: GPU tương thích CUDA để tăng tốc suy luận  

---

## Nội dung hướng dẫn này

- Kích hoạt giấy phép Aspose OCR từ môi trường
- Tải PDF bằng `load_pdf OCR` và bật **chế độ OCR chữ viết tay**
- Chạy OCR có cấu trúc để lấy văn bản và dữ liệu ngôn ngữ ở mức khối
- Thiết lập một **mô hình OCR của Hugging Face** (Qwen 2.5‑3B‑Instruct) cho bước hậu xử lý
- Áp dụng kiểm tra chính tả và sửa ngữ pháp từng khối
- Dọn dẹp tài nguyên AI để tránh rò rỉ bộ nhớ

Nếu bạn từng thử một engine OCR thông thường và nhận được các ký tự vô nghĩa trên các ghi chú viết tay, cờ “handwritten OCR mode” là yếu tố thay đổi trò chơi mà bạn đã bỏ lỡ. Và nhờ mô hình Hugging Face, bạn cũng sẽ có được sự tinh chỉnh cấp chuyên nghiệp mà không cần rời khỏi môi trường Python.

![sơ đồ quy trình chạy OCR](https://example.com/ocr-workflow.png "cách chạy OCR")

*Văn bản thay thế hình ảnh: sơ đồ quy trình chạy OCR*

## Bước 1: Cài đặt các gói cần thiết

Đầu tiên, hãy chắc chắn rằng Aspose OCR Cloud SDK và thư viện `transformers` đã được cài đặt. Chạy lệnh sau trong terminal của bạn:

```bash
pip install aspose-ocr-cloud transformers huggingface-hub
```

> **Mẹo chuyên nghiệp:** Nếu bạn dự định sử dụng tăng tốc GPU, cũng hãy cài đặt `torch` với hỗ trợ CUDA (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`).

## Bước 2: Kích hoạt giấy phép Aspose OCR

Kích hoạt giấy phép từ biến môi trường giúp giữ khóa của bạn khỏi việc kiểm soát nguồn. Đặt `ASPOSE_OCR_LICENSE` trong shell, sau đó gọi `activate_from_env()`:

```python
import asposeocrcloud as ocr

# Pull the license string from the ASPOSE_OCR_LICENSE environment variable
ocr.activate_from_env()
```

> Tại sao điều này quan trọng: Nếu không có giấy phép hợp lệ, SDK sẽ quay lại chế độ dùng thử, giới hạn số trang và tắt việc sử dụng GPU.

## Bước 3: Khởi tạo Engine OCR ở chế độ Handwritten

Chúng tôi tạo một `OcrEngine`, bật GPU (nếu có), và yêu cầu rõ ràng **chế độ OCR chữ viết tay**. Chế độ này điều chỉnh mạng nơ-ron nền để xử lý tốt hơn các nét chữ viết liền.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Enable GPU acceleration – optional but speeds up large PDFs dramatically
ocr_engine.set_use_gpu(True)

# Switch to handwritten recognition mode for better accuracy on cursive text
ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)
```

> **Lưu ý:** Nếu bạn không có GPU, `set_use_gpu(False)` vẫn hoạt động; engine sẽ quay lại CPU.

## Bước 4: Tải PDF của bạn và chạy OCR có cấu trúc

Bây giờ chúng ta thực sự **tải PDF OCR**. Phương thức `load_image` chấp nhận PDF, TIFF, JPG, v.v. OCR có cấu trúc trả về các khối chứa cả văn bản thô và ngôn ngữ được phát hiện.

```python
# Replace the path with your own PDF location
pdf_path = "YOUR_DIRECTORY/multilingual_handwritten.pdf"
ocr_engine.load_image(pdf_path)

# Perform structured OCR – returns a hierarchy of blocks
structured_result = ocr_engine.recognize_structured()
```

Danh sách `structured_result.blocks` có thể trông như sau (được rút gọn để ngắn gọn):

```python
[
    Block(text="Bonjour le monde", language="fr"),
    Block(text="Hello world", language="en"),
    Block(text="こんにちは世界", language="ja")
]
```

## Bước 5: Cấu hình mô hình OCR của Hugging Face cho bước hậu xử lý

Chúng tôi sẽ sử dụng mô hình **Qwen 2.5‑3B‑Instruct** từ Hugging Face, đã được lượng tử hoá thành `int8` để giảm dung lượng bộ nhớ. Bộ bao bọc `AsposeAIModelConfig` cho biết cho bộ hậu xử lý AI của Aspose cách tải xuống và chạy mô hình.

```python
from asposeocrcloud import AsposeAI, AsposeAIModelConfig

model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25,                # Number of transformer layers to keep on GPU
    allow_auto_download="true"   # Auto‑download the model if not cached
)

spell_corrector = AsposeAI()
spell_corrector.set_post_processor("spell_corrector", model_cfg)
```

> **Tại sao chọn mô hình này?** Qwen 2.5‑3B‑Instruct cân bằng tốc độ và chất lượng. Lượng tử hoá `int8` giảm mức sử dụng RAM xuống ~4 GB, cho phép chạy trên hầu hết các laptop hiện đại.

## Bước 6: Áp dụng kiểm tra chính tả từng khối

Chúng tôi lặp qua từng khối OCR, đưa nó cho bộ hậu xử lý AI, và in ra văn bản đã được sửa cùng với ngôn ngữ được phát hiện. Đây là lõi của quy trình **load PDF OCR → post‑process**.

```python
for block in structured_result.blocks:
    # Run the correction; `run_postprocessor` returns an object with a .text attribute
    corrected = spell_corrector.run_postprocessor(block)
    print(f"[{block.language}] {corrected.text}")
```

### Kết quả dự kiến

```
[fr] Bonjour le monde
[en] Hello world
[ja] こんにちは世界
```

Nếu OCR gốc có lỗi chính tả như “Helllo wrold”, mô hình sẽ xuất ra phiên bản đã được sửa.

## Bước 7: Dọn dẹp tài nguyên AI

Luôn giải phóng bộ nhớ GPU khi bạn hoàn thành. Lệnh `free_resources()` sẽ gỡ tải mô hình và xóa bộ nhớ đệm CUDA.

```python
spell_corrector.free_resources()
```

## Những khó khăn thường gặp & Cách tránh

| Issue | Symptom | Fix |
|-------|----------|-----|
| **GPU không được phát hiện** | `set_use_gpu(True)` âm thầm chuyển sang CPU | Kiểm tra driver CUDA (`nvidia-smi`) và cài đặt đúng gói `torch`. |
| **Tải mô hình thất bại** | `allow_auto_download` gây lỗi mạng | Đảm bảo cho phép HTTPS ra ngoài, hoặc tải thủ công tệp GGUF và chỉ định `hugging_face_repo_id` tới đường dẫn cục bộ. |
| **Văn bản viết tay vẫn bị rối** | Điểm tin cậy thấp trong `structured_result` | Tăng `set_recognition_mode` lên `HANDWRITTEN` (đã thực hiện) và cân nhắc tiền xử lý PDF bằng việc tăng độ nét ảnh (`opencv`) trước khi OCR. |
| **Hết bộ nhớ trên GPU** | `RuntimeError: CUDA out of memory` | Giảm `gpu_layers` (ví dụ, xuống 10) hoặc chuyển sang suy luận trên CPU (`set_use_gpu(False)`). |

## Mở rộng quy trình làm việc

- **Xử lý hàng loạt:** Đóng gói toàn bộ script trong một hàm nhận danh sách các đường dẫn PDF và ghi kết quả đã chỉnh sửa ra các tệp `.txt` riêng.  
- **Từ vựng tùy chỉnh:** Nếu lĩnh vực của bạn sử dụng thuật ngữ chuyên biệt (ví dụ, viết tắt y tế), hãy tinh chỉnh mô hình Hugging Face với một bộ dữ liệu nhỏ.  
- **Mô hình thay thế:** Thay `Qwen/Qwen2.5-3B-Instruct-GGUF` bằng `mistralai/Mistral-7B-Instruct-v0.2` nếu bạn cần cửa sổ ngữ cảnh lớn hơn.  

## Kết luận

Bạn giờ đã biết **cách chạy OCR** trên PDF, tải PDF OCR, bật **chế độ OCR chữ viết tay**, và nâng cao độ chính xác với một **mô hình OCR của Hugging Face**. Script hoàn chỉnh—kích hoạt giấy phép, engine hỗ trợ GPU, OCR có cấu trúc, hậu xử lý AI, và dọn dẹp—bao phủ mọi bước mà nhà phát triển thường hỏi, từ “nếu tôi không có GPU thì sao?” đến “làm sao giải phóng tài nguyên?”. 

Hãy thử nghiệm với các tài liệu của bạn, khám phá các mô hình khác nhau, hoặc tích hợp pipeline vào một dịch vụ xử lý tài liệu lớn hơn. Khi bạn đã thành thạo sự kết hợp giữa Aspose OCR và AI của Hugging Face, không gì là không thể.

**Các bước tiếp theo**

- Thử quy trình tương tự trên các ảnh quét (`.png`, `.jpg`) để xem engine thích nghi như thế nào.  
- Khám phá tính năng **phân tích bố cục** của Aspose OCR để trích xuất bảng.  
- Tìm hiểu sâu hơn về các kỹ thuật lượng tử hoá của Hugging Face để giảm kích thước mô hình hơn nữa.  

Chúc bạn hack OCR vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}