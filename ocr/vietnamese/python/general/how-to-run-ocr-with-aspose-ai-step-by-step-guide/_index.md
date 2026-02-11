---
category: general
date: 2026-02-09
description: cách chạy OCR bằng Aspose AI và mô hình Hugging Face – học cách tải mô
  hình Hugging Face, sửa lỗi OCR và giải phóng bộ nhớ GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: vi
og_description: Cách chạy OCR với Aspose AI được giải thích trong đoạn đầu – khám
  phá cách tải mô hình Hugging Face, sửa lỗi OCR và giải phóng bộ nhớ GPU.
og_title: Cách chạy OCR với Aspose AI – Hướng dẫn đầy đủ
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Cách chạy OCR với Aspose AI – Hướng dẫn từng bước
url: /vi/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách chạy OCR với Aspose AI – Complete Guide

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một hóa đơn đã quét và nhận được các con số hoàn toàn sạch sẽ mà không phải tốn hàng giờ để sửa lỗi chính tả không? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, văn bản thô xuất ra từ một công cụ OCR cổ điển vẫn chứa các ký tự lạ, ký hiệu tiền tệ bị hỏng, hoặc các chữ số rối loạn — đặc biệt khi ảnh nguồn có nhiễu.  

Tin tốt là bạn có thể kết nối một LLM với Aspose OCR, tải xuống một mô hình Hugging Face ngay lập tức, và để AI tinh chỉnh kết quả cho bạn. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình, từ việc tải mô hình (đúng vậy, chúng tôi sẽ chỉ cho bạn cách **download hugging face model** tự động) đến việc giải phóng tài nguyên GPU khi bạn hoàn thành. Khi kết thúc, bạn sẽ có một script có thể tái tạo được mà **corrects OCR errors**, chạy nhanh trên một GPU vừa phải, và tự dọn dẹp để bạn không lãng phí bộ nhớ.

## Những gì bạn sẽ học

- Cấu hình Aspose AI để lấy mô hình **Qwen2.5‑3B‑Instruct‑GGUF** từ Hugging Face.
- Chạy engine Aspose OCR tiêu chuẩn trên một tệp hình ảnh.
- Sử dụng một prompt LLM tùy chỉnh giữ nguyên các số và ký hiệu tiền tệ.
- Giải phóng bộ nhớ GPU bằng routine tích hợp **free gpu memory**.
- Tinh chỉnh quy trình cho các trường hợp đặc biệt như PDF đa trang hoặc GPU cấp thấp.

> **Prerequisites** – Python 3.9+, `aspose-ocr` package, internet access for the first model download, and a GPU with at least 4 GB VRAM (optional but recommended). If you don’t have a GPU, the script will automatically fall back to CPU for the remaining layers.

---

## Cách chạy OCR và cải thiện kết quả

Dưới đây là script Python đầy đủ, sẵn sàng chạy. Lưu nó dưới tên `ocr_with_ai.py` và thay thế các đường dẫn placeholder bằng các tệp của bạn.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip:** Tham số `gpu_layers` cho phép bạn quyết định bao nhiêu lớp transformer sẽ ở trên GPU. Nếu bạn gặp lỗi out‑of‑memory, hãy giảm số này và phần còn lại sẽ chạy trên CPU – bạn vẫn sẽ **free gpu memory** sau này bằng `ai.free_resources()`.

### Kết quả dự kiến

Chạy script trên một mẫu hóa đơn sẽ cho ra kết quả như sau:

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Chú ý cách AI đã sửa ký tự “O” trong `$1O0.00` thành số 0 đúng trong khi vẫn giữ dấu đô la. Đó là bản chất của **correct OCR errors** cho các tài liệu tài chính.

---

## Tải mô hình Hugging Face – Điều gì xảy ra phía sau?

Khi bạn đặt `allow_auto_download="true"` wrapper Aspose AI sẽ kiểm tra `directory_model_path`. Nếu các tệp mô hình không có ở đó, nó sẽ kết nối tới Hugging Face Hub, tải phiên bản **int8‑quantized** của `Qwen2.5‑3B‑Instruct‑GGUF`, và lưu cục bộ. Lần tải này thường dưới 2 GB, cho phép thực hiện ngay cả trên SSD vừa phải.

> **Why int8?** Việc lượng tử hoá thành 8‑bit giảm đáng kể việc sử dụng bộ nhớ—rất quan trọng khi bạn cũng muốn **free gpu memory** sau khi xử lý. Sự đánh đổi là một chút giảm độ chính xác, nhưng đối với việc hậu xử lý văn bản OCR, ảnh hưởng là không đáng kể.

Nếu bạn muốn tự lưu trữ mô hình, chỉ cần đặt các tệp `.gguf` vào `YOUR_DIRECTORY/Models` và Aspose sẽ tự động nhận chúng mà không cần truy cập internet nữa.

---

## Cách giải phóng GPU – Thực hành tốt nhất

Tài nguyên GPU là một nguồn tài nguyên chung trên nhiều workstation. Để lại các tensor tồn tại sau khi script kết thúc có thể gây lỗi “CUDA out of memory” cho các công việc tiếp theo. Lệnh `ai.free_resources()` thực hiện ba việc:

1. **Disposes the underlying transformer** – tất cả các trọng số cư trú trên GPU được giải phóng.
2. **Clears the PyTorch cache** – `torch.cuda.empty_cache()` được gọi nội bộ.
3. **Deletes temporary files** – bất kỳ bộ nhớ đệm trên đĩa nào được tạo trong quá trình tải xuống sẽ bị xóa.

Bạn cũng có thể tự gọi `torch.cuda.empty_cache()` nếu bạn đang kết hợp Aspose AI với các công việc PyTorch khác, nhưng phương pháp tích hợp sẵn thường đã đủ.

---

## Hướng dẫn chi tiết từng bước (H2s với từ khóa phụ)

### Tải mô hình Hugging Face tự động

Constructor `AsposeAIModelConfig` ẩn đi sự phức tạp khi làm việc với API của Hugging Face. Chỉ cần đảm bảo bạn có kết nối internet lần đầu khi chạy script. Sau đó, mô hình sẽ nằm trong `YOUR_DIRECTORY/Models`, và các lần chạy tiếp theo sẽ khởi động ngay lập tức.

### Giải phóng bộ nhớ GPU sau khi suy luận

Nếu bạn chạy đoạn này trong một dịch vụ chạy lâu (ví dụ, một Flask API), hãy gọi `ai.free_resources()` sau mỗi yêu cầu. Điều này ngăn rò rỉ bộ nhớ và đảm bảo yêu cầu tiếp theo có thể tái sử dụng GPU mà không gặp trục trặc.

### Sửa lỗi OCR với Prompt tùy chỉnh

Hàm `financial_prompt` của chúng tôi trả về một dictionary với một khóa duy nhất là `prompt`. Bạn có thể tùy chỉnh nó cho bất kỳ lĩnh vực nào:

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Thay đổi tên hàm trong `ai.set_post_processor(...)` và bạn sẽ có một pipeline **correct OCR errors** cho hồ sơ y tế.

### Cách chạy OCR trên PDF đa trang

Aspose OCR có thể xử lý PDF ngay từ đầu:

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Sau khi bạn có được chuỗi thô, cùng một post‑processor LLM sẽ làm sạch văn bản của mỗi trang. Không cần mã bổ sung.

### Khi bạn không có GPU – Cách giải phóng GPU (ngay cả khi không có GPU)

Ngay cả trên máy chỉ có CPU, việc gọi `ai.free_resources()` cũng không gây hại. Nó chỉ xóa các bộ nhớ đệm nội bộ, có thể giải phóng RAM. Vì vậy, lời khuyên **how to free gpu** áp dụng cho mọi trường hợp: luôn dọn dẹp sau khi sử dụng.

---

## Những khó khăn thường gặp & Cách chúng tôi giải quyết

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| **Out‑of‑Memory on GPU** | `gpu_layers` được đặt quá cao cho card của bạn | Giảm `gpu_layers` xuống 10 hoặc 5, để phần còn lại chạy trên CPU |
| **Model never downloads** | Tường lửa công ty chặn HTTPS tới huggingface.co | Tải mô hình thủ công trên mạng khác, sau đó chỉ định `directory_model_path` tới thư mục cục bộ |
| **Numbers get corrupted** | Prompt không đủ rõ ràng về việc giữ nguyên các chữ số | Thêm “preserve all numeric values and currency symbols exactly as they appear” vào prompt |
| **`free_resources` raises an exception** | Sử dụng phiên bản Aspose OCR cũ hơn | Nâng cấp lên gói `aspose-ocr` mới nhất (pip install --upgrade aspose-ocr) |

---

## Tổng kết ví dụ đầy đủ

Đây là script một lần nữa, lần này kèm theo các chú thích nội tuyến giải thích từng dòng để tham khảo trong tương lai:

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Kết luận

Chúng tôi đã trình bày **how to run OCR** với Aspose, tải mô hình Hugging Face theo yêu cầu, tạo một prompt mà **corrects OCR errors**, và cuối cùng **free gpu memory** để workstation của bạn luôn phản hồi nhanh. Toàn bộ quy trình được gói trong một tệp Python duy nhất, tự chứa—không cần script bên ngoài, không cần xử lý mô hình thủ công, và không có bộ nhớ GPU còn lại.

Bước tiếp theo? Hãy thử thay thế `financial_prompt` bằng một

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}