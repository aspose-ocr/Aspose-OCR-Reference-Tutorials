---
category: general
date: 2026-05-03
description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR và kiểm tra chính tả AI.
  Tìm hiểu cách OCR hình ảnh, tải hình ảnh cho OCR, nhận dạng văn bản từ hoá đơn và
  giải phóng tài nguyên GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR và kiểm tra chính tả
  AI. Hướng dẫn chi tiết từng bước về cách OCR hình ảnh, tải hình ảnh để OCR và giải
  phóng tài nguyên GPU.
og_title: Trích xuất văn bản từ hình ảnh – Hướng dẫn toàn diện về OCR và Kiểm tra
  chính tả
tags:
- OCR
- Aspose
- AI
- Python
title: Trích xuất văn bản từ hình ảnh – OCR với Aspose AI Spell‑Check
url: /vi/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# trích xuất văn bản từ hình ảnh – Hướng dẫn OCR & Kiểm tra chính tả hoàn chỉnh

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không chắc thư viện nào sẽ cung cấp cả tốc độ và độ chính xác? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế—như xử lý hoá đơn, số hoá biên lai, hoặc quét hợp đồng—việc có được văn bản sạch, có thể tìm kiếm từ một bức ảnh là rào cản đầu tiên.

Tin tốt là Aspose OCR kết hợp với một mô hình Aspose AI nhẹ có thể thực hiện công việc này chỉ trong vài dòng Python. Trong hướng dẫn này, chúng ta sẽ đi qua **cách OCR hình ảnh**, tải ảnh đúng cách, chạy bộ xử lý hậu kỳ kiểm tra chính tả tích hợp, và cuối cùng **giải phóng tài nguyên GPU** để ứng dụng của bạn tiết kiệm bộ nhớ.

Khi kết thúc hướng dẫn này, bạn sẽ có thể **nhận dạng văn bản từ hình ảnh hoá đơn**, tự động sửa các lỗi OCR thường gặp, và giữ GPU của bạn sạch sẽ cho lô tiếp theo.

---

## Những gì bạn cần

- Python 3.9 hoặc mới hơn (code sử dụng type hints nhưng vẫn hoạt động trên các phiên bản 3.x cũ hơn)
- `aspose-ocr` và `aspose-ai` packages (cài đặt bằng `pip install aspose-ocr aspose-ai`)
- GPU hỗ trợ CUDA là tùy chọn; script sẽ chuyển sang CPU nếu không tìm thấy.
- Một hình ảnh mẫu, ví dụ `sample_invoice.png`, đặt trong thư mục bạn có thể tham chiếu.

Không có khung ML nặng, không tải xuống mô hình khổng lồ—chỉ một mô hình lượng tử Q4‑K‑M nhỏ gọn, phù hợp với hầu hết các GPU.

---

## Bước 1: Khởi tạo Engine OCR – trích xuất văn bản từ hình ảnh

Điều đầu tiên bạn làm là tạo một thể hiện `OcrEngine` và chỉ định ngôn ngữ bạn mong đợi. Ở đây chúng ta chọn tiếng Anh và yêu cầu đầu ra dạng plain‑text, lý tưởng cho các bước xử lý tiếp theo.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Tại sao điều này quan trọng:** Đặt ngôn ngữ sẽ thu hẹp bộ ký tự, cải thiện độ chính xác. Chế độ plain‑text loại bỏ thông tin bố cục mà bạn thường không cần khi chỉ muốn trích xuất văn bản từ hình ảnh.

---

## Bước 2: Tải ảnh cho OCR – cách OCR hình ảnh

Bây giờ chúng ta cung cấp cho engine một bức ảnh thực tế. Hàm trợ giúp `Image.load` hiểu các định dạng phổ biến (PNG, JPEG, TIFF) và trừu tượng hoá các quirks của file‑IO.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Mẹo:** Nếu ảnh nguồn của bạn lớn, hãy cân nhắc thay đổi kích thước chúng trước khi gửi tới engine; kích thước nhỏ hơn có thể giảm sử dụng bộ nhớ GPU mà không làm giảm chất lượng nhận dạng.

---

## Bước 3: Cấu hình mô hình Aspose AI – nhận dạng văn bản từ hoá đơn

Aspose AI đi kèm với một mô hình GGUF siêu nhỏ mà bạn có thể tự động tải xuống. Ví dụ này sử dụng repository `Qwen2.5‑3B‑Instruct‑GGUF`, được lượng tử hoá thành `q4_k_m`. Chúng ta cũng chỉ định runtime cấp phát 20 lớp trên GPU, cân bằng tốc độ và việc sử dụng VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Phía sau:** Mô hình lượng tử có dung lượng khoảng 1.5 GB trên đĩa, chỉ một phần nhỏ so với mô hình độ chính xác đầy đủ, nhưng vẫn nắm bắt đủ ngữ nghĩa để phát hiện các lỗi chính tả OCR thường gặp.

---

## Bước 4: Khởi tạo AsposeAI và gắn bộ xử lý hậu kỳ kiểm tra chính tả

Aspose AI bao gồm một bộ xử lý hậu kỳ kiểm tra chính tả đã sẵn sàng. Khi gắn nó, mọi kết quả OCR sẽ được tự động làm sạch.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Tại sao nên dùng bộ xử lý hậu kỳ?** Các engine OCR thường đọc sai “Invoice” thành “Invo1ce” hoặc “Total” thành “T0tal”. Kiểm tra chính tả chạy một mô hình ngôn ngữ nhẹ trên chuỗi thô và sửa các lỗi này mà bạn không cần viết từ điển tùy chỉnh.

---

## Bước 5: Chạy bộ xử lý hậu kỳ kiểm tra chính tả trên kết quả OCR

Khi mọi thứ đã được kết nối, một lần gọi duy nhất sẽ trả về văn bản đã được sửa. Chúng tôi cũng in ra cả phiên bản gốc và phiên bản đã làm sạch để bạn có thể thấy sự cải thiện.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Kết quả mẫu cho một hoá đơn có thể trông như sau:

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Chú ý cách “Invo1ce” đã chuyển thành từ đúng “Invoice”. Đó là sức mạnh của bộ kiểm tra chính tả AI tích hợp.

---

## Bước 6: Giải phóng tài nguyên GPU – giải phóng tài nguyên GPU một cách an toàn

Nếu bạn chạy đoạn mã này trong một dịch vụ lâu dài (ví dụ, một web API xử lý hàng chục hoá đơn mỗi phút), bạn phải giải phóng ngữ cảnh GPU sau mỗi lô. Nếu không, bạn sẽ gặp rò rỉ bộ nhớ và cuối cùng nhận lỗi “CUDA out of memory”.

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Mẹo chuyên nghiệp:** Gọi `free_resources()` trong một khối `finally` hoặc một context manager để nó luôn được thực thi, ngay cả khi có ngoại lệ xảy ra.

---

## Ví dụ Hoạt động Đầy đủ

Kết hợp tất cả các phần lại với nhau sẽ cho bạn một script tự chứa mà bạn có thể đưa vào bất kỳ dự án nào.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Lưu file, điều chỉnh đường dẫn tới ảnh của bạn, và chạy `python extract_text_from_image.py`. Bạn sẽ thấy văn bản hoá đơn đã được làm sạch được in ra console.

---

## Câu hỏi Thường gặp (FAQ)

**Q: Điều này có hoạt động trên máy chỉ có CPU không?**  
A: Chắc chắn. Nếu không phát hiện GPU, Aspose AI sẽ chuyển sang thực thi trên CPU, mặc dù sẽ chậm hơn. Bạn có thể buộc sử dụng CPU bằng cách đặt `model_cfg.gpu_layers = 0`.

**Q: Nếu hoá đơn của tôi ở ngôn ngữ khác tiếng Anh thì sao?**  
A: Thay đổi `ocr_engine.language` thành giá trị enum phù hợp (ví dụ, `aocr.Language.Spanish`). Mô hình kiểm tra chính tả hỗ trợ đa ngôn ngữ, nhưng bạn có thể có kết quả tốt hơn với mô hình chuyên cho ngôn ngữ đó.

**Q: Tôi có thể xử lý nhiều ảnh trong một vòng lặp không?**  
A: Có. Chỉ cần đưa các bước tải, nhận dạng và xử lý hậu kỳ vào trong một vòng `for`. Nhớ gọi `ocr_ai.free_resources()` sau vòng lặp hoặc sau mỗi lô nếu bạn đang tái sử dụng cùng một instance AI.

**Q: Kích thước tải xuống của mô hình là bao nhiêu?**  
A: Khoảng 1.5 GB cho phiên bản lượng tử `q4_k_m`. Nó được lưu vào cache sau lần chạy đầu tiên, vì vậy các lần thực thi tiếp theo là ngay lập tức.

---

## Kết luận

Trong hướng dẫn này, chúng tôi đã trình bày cách **trích xuất văn bản từ hình ảnh** bằng Aspose OCR, cấu hình một mô hình AI siêu nhỏ, áp dụng bộ xử lý hậu kỳ kiểm tra chính tả, và an toàn **giải phóng tài nguyên GPU**. Quy trình bao gồm mọi thứ từ tải ảnh đến dọn dẹp sau khi sử dụng, cung cấp cho bạn một pipeline đáng tin cậy cho các trường hợp **nhận dạng văn bản từ hoá đơn**.

Bước tiếp theo? Hãy thử thay thế bộ kiểm tra chính tả bằng một mô hình trích xuất thực thể tùy chỉnh

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}