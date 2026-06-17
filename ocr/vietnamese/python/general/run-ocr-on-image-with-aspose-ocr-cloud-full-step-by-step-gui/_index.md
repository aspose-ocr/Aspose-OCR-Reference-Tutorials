---
category: general
date: 2026-03-28
description: Tìm hiểu cách chạy OCR trên hình ảnh, tự động tải mô hình Hugging Face,
  làm sạch văn bản OCR và cấu hình mô hình LLM trong Python bằng Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: vi
og_description: Chạy OCR trên hình ảnh và làm sạch đầu ra bằng mô hình Hugging Face
  tự tải xuống. Hướng dẫn này cho thấy cách cấu hình mô hình LLM trong Python.
og_title: Chạy OCR trên hình ảnh – Hướng dẫn đầy đủ Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Chạy OCR trên hình ảnh với Aspose OCR Cloud – Hướng dẫn chi tiết từng bước
url: /vi/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên Hình ảnh – Hướng dẫn đầy đủ Aspose OCR Cloud

Bạn đã bao giờ cần chạy OCR trên các tệp hình ảnh nhưng kết quả thô trông như một mớ hỗn độn? Theo kinh nghiệm của tôi, vấn đề khó khăn nhất không phải là việc nhận dạng mà là việc làm sạch. May mắn là Aspose OCR Cloud cho phép bạn gắn một bộ xử lý hậu xử lý LLM có thể *tự động làm sạch văn bản OCR*. Trong hướng dẫn này, chúng tôi sẽ hướng dẫn bạn mọi thứ cần thiết: từ **tải xuống mô hình Hugging Face** đến cấu hình LLM, chạy engine OCR, và cuối cùng là tinh chỉnh kết quả.

Khi hoàn thành hướng dẫn này, bạn sẽ có một script sẵn sàng chạy mà:

1. Tải về mô hình Qwen 2.5 gọn nhẹ từ Hugging Face (tự động tải cho bạn).  
2. Cấu hình mô hình để chạy một phần mạng trên GPU và phần còn lại trên CPU.  
3. Thực thi engine OCR trên một ảnh ghi chú viết tay.  
4. Sử dụng LLM để làm sạch văn bản đã nhận dạng, cung cấp đầu ra dễ đọc cho con người.

> **Prerequisites** – Python 3.8+, gói `asposeocrcloud`, một GPU có ít nhất 4 GB VRAM (tùy chọn nhưng được khuyến nghị), và kết nối internet để tải mô hình lần đầu.

---

## Bạn sẽ cần gì

- **Aspose OCR Cloud SDK** – cài đặt qua `pip install asposeocrcloud`.  
- **Một ảnh mẫu** – ví dụ: `handwritten_note.jpg` đặt trong thư mục cục bộ.  
- **Hỗ trợ GPU** – nếu bạn có GPU hỗ trợ CUDA, script sẽ chuyển 30 lớp sang GPU; nếu không, nó sẽ tự động quay lại CPU.  
- **Quyền ghi** – script sẽ lưu bộ nhớ đệm mô hình trong `YOUR_DIRECTORY`; hãy chắc chắn thư mục tồn tại.

---

## Bước 1 – Cấu hình mô hình LLM (tải mô hình Hugging Face)

Điều đầu tiên chúng ta làm là chỉ cho Aspose AI nơi lấy mô hình. Lớp `AsposeAIModelConfig` xử lý việc tự động tải, lượng tử hoá và phân bổ lớp GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Tại sao điều này quan trọng** – Lượng tử hoá thành `int8` giảm đáng kể việc sử dụng bộ nhớ (≈ 4 GB so với 12 GB). Phân chia mô hình giữa GPU và CPU cho phép bạn chạy một LLM 3 tỷ tham số ngay trên RTX 3060 thông thường. Nếu bạn không có GPU, đặt `gpu_layers=0` và SDK sẽ giữ mọi thứ trên CPU.

> **Tip:** Lần chạy đầu tiên sẽ tải xuống khoảng ~ 1.5 GB, vì vậy hãy kiên nhẫn trong vài phút và đảm bảo kết nối ổn định.

---

## Bước 2 – Khởi tạo AI Engine với cấu hình mô hình

Bây giờ chúng ta khởi động engine AI của Aspose và truyền vào cấu hình vừa tạo.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Điều gì đang diễn ra phía sau?** SDK kiểm tra `directory_model_path` để tìm mô hình đã tồn tại. Nếu tìm thấy phiên bản phù hợp, nó sẽ tải ngay; nếu không, nó sẽ tải file GGUF từ Hugging Face, giải nén và chuẩn bị pipeline suy luận.

---

## Bước 3 – Tạo OCR Engine và Gắn AI Post‑Processor

OCR engine thực hiện việc nhận dạng ký tự. Bằng cách gắn `ocr_ai.run_postprocessor` chúng ta kích hoạt **làm sạch văn bản OCR** tự động sau khi nhận dạng.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Tại sao cần post‑processor?** Văn bản OCR thô thường có các ngắt dòng sai chỗ, dấu câu bị nhận sai, hoặc ký tự lạ. LLM có thể viết lại đầu ra thành các câu đúng, sửa lỗi chính tả và thậm chí suy luận các từ thiếu—như biến một đống dữ liệu thô thành văn bản mượt mà.

---

## Bước 4 – Chạy OCR trên tệp ảnh

Sau khi đã kết nối mọi thứ, đã đến lúc đưa ảnh vào engine.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Trường hợp đặc biệt:** Nếu ảnh quá lớn (> 5 MP), bạn có thể muốn thu nhỏ trước để tăng tốc xử lý. SDK chấp nhận đối tượng Pillow `Image`, vì vậy bạn có thể tiền xử lý bằng `PIL.Image.thumbnail()` nếu cần.

---

## Bước 5 – Để AI làm sạch văn bản đã nhận dạng và hiển thị cả hai phiên bản

Cuối cùng chúng ta gọi post‑processor đã gắn trước đó. Bước này minh họa sự khác biệt giữa *trước* và *sau* khi làm sạch.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Kết quả mong đợi

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Chú ý cách LLM đã:

- Sửa các lỗi nhận dạng thường gặp (`Th1s` → `This`).  
- Loại bỏ ký tự lạ (`&` → `and`).  
- Chuẩn hoá các ngắt dòng thành câu hoàn chỉnh.

---

## 🎨 Tổng quan trực quan (Quy trình chạy OCR trên ảnh)

![Quy trình chạy OCR trên hình ảnh](run_ocr_on_image_workflow.png "Sơ đồ mô tả quy trình chạy OCR trên hình ảnh từ tải mô hình đến kết quả đã làm sạch")

Sơ đồ trên tóm tắt toàn bộ pipeline: **tải mô hình Hugging Face → cấu hình LLM → khởi tạo AI → OCR engine → AI post‑processor → làm sạch văn bản OCR**.

---

## Câu hỏi thường gặp & Mẹo chuyên nghiệp

### Nếu tôi không có GPU thì sao?

Đặt `gpu_layers=0` trong `AsposeAIModelConfig`. Mô hình sẽ chạy hoàn toàn trên CPU, chậm hơn nhưng vẫn hoạt động. Bạn cũng có thể chuyển sang mô hình nhỏ hơn (ví dụ `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) để thời gian suy luận hợp lý.

### Làm sao để thay đổi mô hình sau này?

Chỉ cần cập nhật `hugging_face_repo_id` và chạy lại `ocr_ai.initialize(model_config)`. SDK sẽ phát hiện thay đổi phiên bản, tải mô hình mới và thay thế các file đã lưu.

### Tôi có thể tùy chỉnh prompt cho post‑processor không?

Có. Truyền một dictionary vào `custom_settings` với khóa `prompt_template`. Ví dụ:

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Nên lưu văn bản đã làm sạch vào file không?

Chắc chắn rồi. Sau khi làm sạch, bạn có thể ghi kết quả ra file `.txt` hoặc `.json` để xử lý tiếp:

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Kết luận

Chúng ta vừa trình bày cách **chạy OCR trên ảnh** bằng Aspose OCR Cloud, tự động **tải mô hình Hugging Face**, cấu hình **cài đặt mô hình LLM** một cách chuyên nghiệp, và cuối cùng **làm sạch văn bản OCR** bằng một bộ xử lý hậu LLM mạnh mẽ. Toàn bộ quy trình được gói gọn trong một script Python dễ chạy, hoạt động trên cả máy có GPU và chỉ CPU.

Nếu bạn đã quen thuộc với pipeline này, hãy thử:

- **LLM khác** – thử `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` để có cửa sổ ngữ cảnh lớn hơn.  
- **Xử lý batch** – lặp qua thư mục ảnh và tổng hợp kết quả đã làm sạch vào CSV.  
- **Prompt tùy chỉnh** – điều chỉnh AI cho lĩnh vực của bạn (tài liệu pháp lý, ghi chú y tế, v.v.).

Hãy tự do thay đổi giá trị `gpu_layers`, đổi mô hình, hoặc chèn prompt của riêng bạn. Bầu trời là giới hạn, và đoạn code bạn có ngay bây giờ là bệ phóng.

Chúc lập trình vui vẻ, và mong đầu ra OCR của bạn luôn sạch sẽ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}