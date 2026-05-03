---
category: general
date: 2026-05-03
description: Cách batch OCR hình ảnh bằng Aspose OCR và kiểm tra chính tả AI. Học
  cách trích xuất văn bản từ hình ảnh, áp dụng kiểm tra chính tả, sử dụng tài nguyên
  AI miễn phí và sửa lỗi OCR.
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: vi
og_description: Cách thực hiện OCR hàng loạt cho hình ảnh bằng Aspose OCR và kiểm
  tra chính tả AI. Tham khảo hướng dẫn từng bước để trích xuất văn bản từ hình ảnh,
  áp dụng kiểm tra chính tả, sử dụng tài nguyên AI miễn phí và sửa lỗi OCR.
og_title: Cách thực hiện OCR hàng loạt với Aspose OCR – Hướng dẫn Python đầy đủ
tags:
- OCR
- Python
- AI
- Aspose
title: Cách thực hiện OCR hàng loạt với Aspose OCR – Hướng dẫn Python đầy đủ
url: /vi/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR hàng loạt với Aspose OCR – Hướng dẫn Python đầy đủ

Bạn đã bao giờ tự hỏi **cách thực hiện OCR hàng loạt** cho một thư mục đầy các tệp PDF hoặc ảnh đã quét mà không cần viết một script riêng cho mỗi tệp chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình thực tế, bạn sẽ cần **trích xuất văn bản từ hình ảnh**, sửa lỗi chính tả, và cuối cùng giải phóng bất kỳ tài nguyên AI nào bạn đã cấp phát. Hướng dẫn này sẽ chỉ cho bạn cách thực hiện điều đó với Aspose OCR, một bộ xử lý hậu AI nhẹ, và một vài dòng Python.

Chúng ta sẽ đi qua các bước khởi tạo engine OCR, kết nối bộ kiểm tra chính tả AI, lặp qua một thư mục ảnh, và dọn dẹp mô hình sau khi hoàn thành. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy mà **tự động sửa lỗi OCR** và giải phóng **các tài nguyên AI** để GPU của bạn luôn hoạt động tốt.

## Những gì bạn cần

- Python 3.9+ (mã sử dụng type‑hints nhưng vẫn hoạt động trên các phiên bản 3.x trước đó)
- `asposeocr` package (`pip install asposeocr`) – cung cấp engine OCR.
- Truy cập mô hình Hugging Face `bartowski/Qwen2.5-3B-Instruct-GGUF` (tự động tải về).
- GPU có ít nhất vài GB VRAM (script đặt `gpu_layers = 30`, bạn có thể giảm nếu cần).

Không có dịch vụ bên ngoài, không có API trả phí – mọi thứ chạy cục bộ.

---

## Bước 1: Thiết lập Engine OCR – **Cách thực hiện OCR hàng loạt** một cách hiệu quả

Trước khi chúng ta có thể xử lý hàng nghìn hình ảnh, chúng ta cần một engine OCR vững chắc. Aspose OCR cho phép chúng ta chọn ngôn ngữ và chế độ nhận dạng trong một lần gọi.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**Tại sao điều này quan trọng:** Đặt `recognize_mode` thành `Plain` giữ cho đầu ra nhẹ, lý tưởng khi bạn dự định chạy kiểm tra chính tả sau này. Nếu bạn cần thông tin bố cục, bạn sẽ chuyển sang `Layout`, nhưng điều này sẽ tăng tải mà bạn có thể không muốn trong một công việc batch.

> **Mẹo chuyên nghiệp:** Nếu bạn đang xử lý các bản quét đa ngôn ngữ, bạn có thể truyền một danh sách như `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]`.

---

## Bước 2: Khởi tạo Bộ xử lý hậu AI – **Áp dụng kiểm tra chính tả** cho đầu ra OCR

Aspose AI đi kèm với một bộ xử lý hậu tích hợp có thể chạy bất kỳ mô hình nào bạn muốn. Ở đây chúng ta tải mô hình Qwen 2.5 đã được lượng tử hoá từ Hugging Face và kết nối quy trình kiểm tra chính tả.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**Tại sao điều này quan trọng:** Mô hình đã được lượng tử hoá (`q4_k_m`), giảm đáng kể việc sử dụng bộ nhớ trong khi vẫn cung cấp khả năng hiểu ngôn ngữ tốt. Bằng cách gọi `set_post_processor` chúng ta nói với Aspose AI thực hiện bước **apply spell check** tự động trên bất kỳ chuỗi nào chúng ta cung cấp.

> **Cảnh báo:** Nếu GPU của bạn không thể xử lý 30 lớp, giảm số lượng xuống 15 hoặc thậm chí 5 – script vẫn sẽ hoạt động, chỉ chậm hơn một chút.

---

## Bước 3: Chạy OCR và **Sửa lỗi OCR** trên một ảnh duy nhất

Bây giờ cả engine OCR và bộ kiểm tra chính tả AI đã sẵn sàng, chúng ta kết hợp chúng. Hàm này tải một ảnh, trích xuất văn bản thô, sau đó chạy bộ xử lý hậu AI để làm sạch.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**Tại sao điều này quan trọng:** Việc đưa trực tiếp chuỗi OCR thô vào mô hình AI cho chúng ta một bước **correct OCR errors** mà không cần viết regex hay từ điển tùy chỉnh. Mô hình hiểu ngữ cảnh, vì vậy nó có thể sửa “recieve” → “receive” và các lỗi tinh tế hơn.

---

## Bước 4: **Trích xuất văn bản từ hình ảnh** hàng loạt – Vòng lặp batch thực tế

Đây là nơi phép màu của **cách thực hiện OCR hàng loạt** tỏa sáng. Chúng ta lặp qua một thư mục, bỏ qua các tệp không hỗ trợ, và ghi mỗi kết quả đã sửa vào tệp `.txt`.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### Kết quả mong đợi

Với một ảnh chứa câu *“The quick brown fox jumps over the lazzy dog.”* bạn sẽ thấy một tệp văn bản có:

```
The quick brown fox jumps over the lazy dog.
```

Lưu ý chữ “z” đôi đã được tự động sửa – đó là kết quả của AI spell‑check.

**Tại sao điều này quan trọng:** Bằng cách tạo các đối tượng OCR và AI **một lần** và tái sử dụng chúng, chúng ta tránh được chi phí tải mô hình cho mỗi tệp. Đây là cách hiệu quả nhất để **cách thực hiện OCR hàng loạt** ở quy mô lớn.

---

## Bước 5: Dọn dẹp – **Giải phóng tài nguyên AI** một cách đúng đắn

Khi bạn hoàn thành, gọi `free_resources()` sẽ giải phóng bộ nhớ GPU, ngữ cảnh CUDA, và bất kỳ tệp tạm thời nào mà mô hình tạo ra.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

Bỏ qua bước này có thể để lại các bộ nhớ GPU chưa được giải phóng, có thể gây crash cho các tiến trình Python tiếp theo hoặc tiêu tốn VRAM. Hãy nghĩ nó như phần “tắt đèn” của một công việc batch.

---

## Những khó khăn thường gặp & Mẹo bổ sung

| Vấn đề | Điều cần kiểm tra | Cách khắc phục |
|-------|------------------|----------------|
| **Lỗi hết bộ nhớ** | GPU hết bộ nhớ sau vài chục ảnh | Giảm `gpu_layers` hoặc chuyển sang CPU (`model_cfg.gpu_layers = 0`). |
| **Thiếu gói ngôn ngữ** | OCR trả về chuỗi rỗng | Đảm bảo phiên bản `asposeocr` bao gồm dữ liệu ngôn ngữ tiếng Anh; cài lại nếu cần. |
| **Tệp không phải ảnh** | Script bị crash khi gặp `.pdf` lẻ | Điều kiện `if not file_name.lower().endswith(...)` đã bỏ qua chúng. |
| **Kiểm tra chính tả không được áp dụng** | Đầu ra giống hệt OCR thô | Kiểm tra `ai_processor.set_post_processor` đã được gọi trước vòng lặp. |
| **Tốc độ batch chậm** | Mất >5 giây cho mỗi ảnh | Bật `model_cfg.allow_auto_download = "false"` sau lần chạy đầu, để mô hình không tải lại mỗi lần. |

**Mẹo:** Nếu bạn cần **trích xuất văn bản từ hình ảnh** bằng ngôn ngữ khác tiếng Anh, chỉ cần thay đổi `ocr_engine.language` thành enum phù hợp (ví dụ, `aocr.Language.French`). Bộ xử lý hậu AI vẫn sẽ áp dụng kiểm tra chính tả, nhưng bạn có thể muốn một mô hình đặc thù cho ngôn ngữ đó để có kết quả tốt nhất.

---

## Tóm tắt & Các bước tiếp theo

Chúng ta đã bao quát toàn bộ quy trình cho **cách thực hiện OCR hàng loạt**:

1. **Khởi tạo** một engine OCR dạng plain‑text cho tiếng Anh.  
2. **Cấu hình** mô hình kiểm tra chính tả AI và gắn nó làm bộ xử lý hậu.  
3. **Chạy** OCR trên mỗi ảnh và để AI **sửa lỗi OCR** tự động.  
4. **Lặp** qua một thư mục để **trích xuất văn bản từ hình ảnh** hàng loạt.  
5. **Giải phóng tài nguyên AI** khi công việc kết thúc.

Từ đây bạn có thể:

- Đưa văn bản đã sửa vào pipeline NLP downstream (phân tích cảm xúc, trích xuất thực thể, v.v.).
- Thay bộ xử lý hậu kiểm tra chính tả bằng một summarizer tùy chỉnh bằng cách gọi `ai_processor.set_post_processor(your_custom_func, {})`.
- Song song hoá vòng lặp thư mục bằng `concurrent.futures.ThreadPoolExecutor` nếu GPU của bạn có thể xử lý nhiều luồng.

---

## Suy nghĩ cuối cùng

Thực hiện OCR hàng loạt không cần phải là một công việc nặng nhọc. Bằng cách kết hợp Aspose OCR với một mô hình AI nhẹ, bạn có được **giải pháp một cửa** có thể **trích xuất văn bản từ hình ảnh**, **áp dụng kiểm tra chính tả**, **sửa lỗi OCR**, và **giải phóng tài nguyên AI** một cách sạch sẽ. Hãy chạy script trên một thư mục thử nghiệm, điều chỉnh số lớp GPU cho phù hợp với phần cứng của bạn, và bạn sẽ có một pipeline sẵn sàng sản xuất trong vài phút.

Có câu hỏi về việc tùy chỉnh mô hình, xử lý PDF, hoặc tích hợp vào dịch vụ web? Để lại bình luận bên dưới hoặc nhắn tin cho tôi trên GitHub. Chúc lập trình vui vẻ, và chúc OCR của bạn luôn chính xác!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}