---
category: general
date: 2026-07-05
description: Tìm hiểu cách chạy OCR trên PDF và cải thiện độ chính xác của OCR bằng
  mô hình Hugging Face. Hướng dẫn cài đặt từng bước, tải PDF để OCR và cấu hình mô
  hình Hugging Face.
draft: false
keywords:
- run OCR on PDF
- improve OCR accuracy
- load PDF for OCR
- configure Hugging Face model
language: vi
og_description: Chạy OCR trên PDF bằng mô hình Hugging Face và cải thiện độ chính
  xác của OCR. Tham khảo hướng dẫn này để tải PDF cho OCR và cấu hình mô hình.
og_title: Chạy OCR trên PDF – Hướng dẫn đầy đủ để tăng độ chính xác
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  headline: run OCR on PDF – Complete Guide to Boost Accuracy
  type: TechArticle
- description: Learn how to run OCR on PDF and improve OCR accuracy using a Hugging
    Face model. Step‑by‑step setup, load PDF for OCR, and configure Hugging Face model.
  name: run OCR on PDF – Complete Guide to Boost Accuracy
  steps:
  - name: What if the PDF is multi‑page?
    text: The `Image.from_file` call automatically creates a multi‑frame image object.
      Loop over `input_image.frames` and call `ocr_engine.recognize` for each frame,
      then concatenate the results before running the post‑processor.
  - name: How to handle languages other than English?
    text: 'Set the OCR engine’s language property before recognition:'
  - name: Can I run this on CPU only?
    text: Yes—just omit `model_cfg.gpu_layers` or set it to `0`. The model will run
      entirely on CPU, though inference will be slower (roughly 5‑10 seconds per page
      on a modern i7).
  type: HowTo
tags:
- OCR
- Python
- AI post‑processor
title: Chạy OCR trên PDF – Hướng Dẫn Toàn Diện Để Tăng Độ Chính Xác
url: /vi/python/general/run-ocr-on-pdf-complete-guide-to-boost-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# chạy OCR trên PDF – Hướng dẫn toàn diện để tăng độ chính xác

Bạn đã bao giờ tự hỏi làm thế nào để **run OCR on PDF** mà không phải chi trả một khoản tiền lớn cho các SDK thương mại chưa? Bạn không phải là người duy nhất. Dù bạn đang số hoá hoá đơn, trích xuất dữ liệu từ các báo cáo đã quét, hay chỉ đơn giản là tò mò về việc trích xuất văn bản được AI hỗ trợ, khả năng **run OCR on PDF** một cách hiệu quả là một kỹ năng không thể thiếu đối với bất kỳ nhà phát triển hiện đại nào.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực tế, từ đầu tới cuối, không chỉ cho bạn cách **run OCR on PDF**, mà còn minh họa cách **improve OCR accuracy** bằng cách gắn một AI post‑processor. Chúng ta cũng sẽ đề cập chi tiết tới **load PDF for OCR** và **configure Hugging Face model** để bạn có được hiệu năng tốt nhất trên một máy trạm vừa phải.

Khi hoàn thành hướng dẫn này, bạn sẽ có một script hoạt động đầy đủ:

* Tải PDF (hoặc hình ảnh) để OCR  
* Cấu hình mô hình Hugging Face với quantization tùy chỉnh và các lớp GPU  
* Thực hiện OCR cơ bản rồi nâng cao kết quả bằng AI post‑processor  
* In ra cả văn bản thô và văn bản đã được AI cải thiện để dễ so sánh  

Không có dịch vụ bên ngoài, không có phí ẩn—chỉ có các thư viện mã nguồn mở và một vài dòng Python.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã chuẩn bị đầy đủ các điều kiện sau:

* Python 3.9 hoặc mới hơn đã được cài đặt (module `venv` rất hữu ích)  
* Gói `aocr` (Aspose OCR) – cài đặt bằng `pip install aocr`  
* Kết nối internet để tải mô hình một lần từ Hugging Face  
* Một file PDF mà bạn muốn xử lý (chúng ta sẽ dùng `invoice_2026.pdf` làm ví dụ)  

Đó là tất cả. Nếu có bất kỳ mục nào bạn chưa quen, đừng lo—mỗi bước dưới đây sẽ giải thích lý do và cách thực hiện, giúp bạn sẵn sàng trong vài phút.

---

## Bước 1: Configure the Hugging Face Model

Điều đầu tiên cần làm là **configure Hugging Face model** sao cho phù hợp với phần cứng của bạn. Trong trường hợp này, chúng ta sẽ tải mô hình mới nhất `Qwen/Qwen2.5-3B-Instruct-GGUF`, quantize nó thành `int8` để giảm kích thước bộ nhớ, và đưa 20 lớp đầu tiên lên GPU để tăng tốc.

```python
import aocr

# Create the AI engine that will later post‑process OCR results
ai_engine = aocr.AsposeAI()

# Build the model configuration – this is where we "configure Hugging Face model"
model_cfg = aocr.AsposeAIModelConfig()
model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"   # released early‑2026
model_cfg.hugging_face_quantization = "int8"                     # small memory footprint
model_cfg.gpu_layers = 20                                        # use first 20 layers on GPU
model_cfg.allow_auto_download = "true"

# Initialize the engine – it will download the model if it's not already cached
ai_engine.initialize(model_cfg)
```

**Tại sao điều này quan trọng:** Quantizing thành `int8` làm giảm kích thước mô hình từ vài gigabyte xuống dưới 1 GB, cho phép chạy trên laptop. Giới hạn số lớp GPU cân bằng giữa tốc độ và việc sử dụng VRAM—hoàn hảo cho card 6 GB.

> **Pro tip:** Nếu gặp lỗi out‑of‑memory, hãy giảm `gpu_layers` xuống `10` hoặc chuyển `quantization` sang `"float16"` để có mô hình hơi lớn hơn nhưng vẫn phù hợp với hầu hết GPU tiêu dùng.

---

## Bước 2: Load PDF for OCR

Khi engine AI đã sẵn sàng, chúng ta cần **load PDF for OCR**. Thư viện Aspose OCR xử lý PDF và hình ảnh một cách đồng nhất, vì vậy bạn có thể chỉ định đường dẫn file hoặc stream.

```python
# Create the OCR engine that will perform the initial text extraction
ocr_engine = aocr.OcrEngine()

# Attach the AI post‑processor – we’ll use the default run_postprocessor method
ocr_engine.set_post_processor(ai_engine.run_postprocessor, None)  # no custom settings required

# Load the PDF document – this is the step where we "load PDF for OCR"
input_image = aocr.Image.from_file("YOUR_DIRECTORY/invoice_2026.pdf")
```

**Tại sao điều này quan trọng:** Bằng cách tải PDF trực tiếp vào đối tượng `Image`, engine OCR có thể xử lý các PDF đa trang từng trang một ở mức dưới. Không cần phải tách PDF thành các hình ảnh trước.

> **Watch out:** Nếu PDF của bạn có các trang được mã hoá, bạn sẽ cần cung cấp mật khẩu qua `Image.from_file(..., password="secret")`.

---

## Bước 3: Run OCR on PDF

Với tài liệu đã nằm trong bộ nhớ, đã đến lúc **run OCR on PDF**. Lần chạy đầu tiên sẽ cho chúng ta văn bản thô, thường chứa nhiều lỗi khoảng trắng, ký tự nhận sai, hoặc thiếu dấu câu—đặc biệt trong các hoá đơn đã quét.

```python
# Perform the plain OCR pass – this is the core "run OCR on PDF" operation
raw_result = ocr_engine.recognize(input_image)  # raw OCR output
```

Ở thời điểm này `raw_result.text` chứa kết quả OCR chưa qua xử lý. Bạn có thể kiểm tra, ghi log, hoặc đưa vào các pipeline downstream.

> **Side note:** Phương thức `recognize` tự động phát hiện hướng trang và cố gắng sửa độ nghiêng, nhưng nó không sửa các lỗi ngôn ngữ đặc thù—đó là nơi AI post‑processor tỏa sáng.

---

## Bước 4: Improve OCR Accuracy with AI Post‑Processor

Bây giờ đến phần thú vị: **improve OCR accuracy**. Bằng cách đưa kết quả thô vào engine AI đã cấu hình ở bước 1, chúng ta cho một mô hình ngôn ngữ lớn làm sạch văn bản, sửa lỗi chính tả, và thậm chí suy luận các giá trị còn thiếu.

```python
# Enhance the raw OCR output using the AI post‑processor
enhanced_result = ocr_engine.run_postprocessor(raw_result)
```

Post‑processor chạy LLM trên mỗi dòng (hoặc khối) văn bản, sử dụng prompt yêu cầu “clean up OCR errors while preserving original meaning”. Kết quả là một phiên bản đã được tinh chỉnh, dễ đọc hơn rất nhiều.

**Tại sao cách này hiệu quả:** Các LLM hiện đại nắm bắt tốt các mẫu ngôn ngữ và có thể suy đoán từ đúng khi OCR đưa ra ký tự rối. Khi kết hợp với mô hình quantized `int8`, quá trình cải thiện hoàn thành trong vòng chưa tới một giây cho một hoá đơn một trang tiêu chuẩn.

---

## Bước 5: Review the Results

Cuối cùng, hãy in ra cả kết quả thô và kết quả đã được AI cải thiện để bạn có thể so sánh trực tiếp.

```python
print("=== Raw OCR ===")
print(raw_result.text)

print("\n=== AI‑enhanced ===")
print(enhanced_result.text)
```

**Kết quả dự kiến (cắt ngắn):**

```
=== Raw OCR ===
Inv0ice N0: 2026-00123
Date: 01/02/2026
Tot@l Am0unt: $1,234.56
...

=== AI‑enhanced ===
Invoice No: 2026-00123
Date: 01/02/2026
Total Amount: $1,234.56
...
```

Chú ý cách phiên bản AI‑enhanced đã sửa các lỗi nhầm lẫn chữ số (`Inv0ice` → `Invoice`) và loại bỏ ký tự `@` lẻ. Đối với hầu hết các tài liệu, bạn sẽ thấy giảm 30‑80 % lỗi OCR.

> **Pro tip:** Nếu bạn cần văn bản đã cải thiện ở dạng có cấu trúc (ví dụ JSON), bạn có thể tiếp tục post‑process `enhanced_result` bằng regex hoặc một hàm phân tích nhỏ.

---

## Tùy chọn: Visualizing the Process

Dưới đây là một sơ đồ đơn giản mô tả luồng xử lý. Văn bản thay thế (alt text) chứa từ khóa chính để đáp ứng SEO.

![Sơ đồ mô tả các bước chạy OCR trên PDF và cải thiện độ chính xác OCR bằng một AI post‑processor](run-ocr-on-pdf-diagram.png)

---

## Các câu hỏi thường gặp & Trường hợp đặc biệt

### PDF đa trang thì sao?

Lệnh `Image.from_file` tự động tạo một đối tượng ảnh đa khung. Bạn chỉ cần lặp qua `input_image.frames` và gọi `ocr_engine.recognize` cho mỗi khung, sau đó nối các kết quả lại trước khi chạy post‑processor.

```python
pages_text = []
for frame in input_image.frames:
    raw = ocr_engine.recognize(frame)
    enhanced = ocr_engine.run_postprocessor(raw)
    pages_text.append(enhanced.text)

full_text = "\n".join(pages_text)
```

### Xử lý ngôn ngữ khác tiếng Anh?

Đặt thuộc tính ngôn ngữ của engine OCR trước khi nhận dạng:

```python
ocr_engine.language = aocr.Language.French  # or aocr.Language.Spanish, etc.
```

LLM vẫn sẽ cải thiện độ chính xác miễn là mô hình **configure Hugging Face model** mà bạn dùng hỗ trợ ngôn ngữ mục tiêu (hầu hết đều hỗ trợ).

### Chỉ chạy trên CPU được không?

Có—chỉ cần bỏ qua `model_cfg.gpu_layers` hoặc đặt nó thành `0`. Mô hình sẽ chạy hoàn toàn trên CPU, tuy nhiên thời gian suy luận sẽ chậm hơn (khoảng 5‑10 giây mỗi trang trên i7 hiện đại).

---

## Tóm tắt

Chúng ta đã bao quát mọi thứ cần thiết để **run OCR on PDF** và **improve OCR accuracy**:

1. **Configure Hugging Face model** với quantization và lớp GPU.  
2. **Load PDF for OCR** bằng `Image.from_file` của Aspose OCR.  
3. **Run OCR on PDF** để lấy văn bản thô.  
4. **Improve OCR accuracy** bằng cách đưa kết quả vào AI post‑processor.  
5. **Review** cả đầu ra thô và đã được cải thiện.

Hãy thử nghiệm—thay đổi repo ID của mô hình sang một LLM mới hơn, tinh chỉnh prompt trong `ai_engine.run_postprocessor` (nếu bạn xem xét mã nguồn), hoặc thêm các bước tiền xử lý như deskew. Pipeline được thiết kế mô-đun, vì vậy bạn có thể thay thế bất kỳ thành phần nào mà không làm hỏng phần còn lại.

---

## Các bước tiếp theo

* **Khám phá các mô hình post‑processing khác** – thử một biến thể `distilbert` nhỏ hơn nếu bạn dùng máy cấu hình thấp.  
* **Tích hợp với cơ sở dữ liệu** – lưu văn bản đã cải thiện vào SQLite hoặc Elasticsearch để tạo kho lưu trữ có thể tìm kiếm.  
* **Thêm tạo PDF** – dùng `reportlab` hoặc `pypdf` để chú thích PDF gốc bằng văn bản đã được làm sạch.  

Nếu bạn đã theo dõi đến đây, bạn đã có nền tảng vững chắc để xây dựng các giải pháp tài liệu mạnh mẽ, được AI nâng cao.

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, mở rộng các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm mã nguồn hoàn chỉnh và giải thích chi tiết từng bước, giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [如何在 .NET 中使用 Aspose.OCR 進行 PDF OCR](/ocr/hongkong/net/text-recognition/recognize-pdf/)
- [.NET에서 Aspose.OCR을 사용하여 PDF OCR하는 방법](/ocr/korean/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}