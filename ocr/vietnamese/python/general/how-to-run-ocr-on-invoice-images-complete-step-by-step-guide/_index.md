---
category: general
date: 2026-01-12
description: Cách chạy OCR và trích xuất văn bản từ hình ảnh hoá đơn bằng Aspose OCR
  và mô hình nhẹ của Hugging Face. Tìm hiểu cách tải mô hình, sửa lỗi OCR và thực
  hiện OCR trên hình ảnh.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: vi
og_description: Cách chạy OCR trên hình ảnh hoá đơn, trích xuất văn bản và sửa lỗi
  bằng mô hình LLM của Hugging Face. Hãy theo dõi hướng dẫn đầy đủ này để có kết quả
  hoàn hảo.
og_title: Cách chạy OCR trên hình ảnh hoá đơn – Hướng dẫn đầy đủ
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Cách chạy OCR trên hình ảnh hoá đơn – Hướng dẫn chi tiết từng bước
url: /vi/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách chạy OCR trên hình ảnh hoá đơn – Hướng dẫn chi tiết từng bước

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một hoá đơn đã quét và nhận được văn bản sạch, có thể tìm kiếm mà không phải tốn hàng giờ để làm sạch không? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, đầu ra OCR thô đầy những lỗi nhận dạng—ví dụ “O” thay cho “0”, “l” thay cho “1”, hoặc thậm chí toàn bộ từ bị lộn xộn. Tin tốt? Chỉ với vài dòng Python, bạn không chỉ **thực hiện OCR trên hình ảnh** mà còn tự động **sửa lỗi OCR** bằng một mô hình nhẹ từ Hugging Face.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết: từ việc tải hình ảnh hoá đơn, trích xuất văn bản thô, tải xuống mô hình đã lượng tử, đến việc tinh chỉnh kết quả để bạn có được bản sao chép hoàn hảo, sẵn sàng cho các quy trình tiếp theo. Khi kết thúc, bạn sẽ có thể **trích xuất văn bản từ hoá đơn** dưới dạng PDF hoặc PNG trong một script duy nhất, có thể lặp lại.

## Yêu cầu & Cài đặt

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Python 3.9+ | Cú pháp hiện đại và gợi ý kiểu |
| `aspose-ocr` package | Cung cấp `ocr.OcrEngine` được sử dụng trong ví dụ |
| `aspose-ai` package | Cung cấp bộ xử lý hậu kỳ `AsposeAI` |
| Access to a GPU (optional) | Tăng tốc các lớp LLM; nếu không, CPU vẫn hoạt động tốt |
| Internet connection (first run) | Cần để **tải mô hình Hugging Face** một cách tự động |

Bạn có thể cài đặt các thư viện cần thiết bằng:

```bash
pip install aspose-ocr aspose-ai
```

> **Mẹo chuyên nghiệp:** Nếu bạn dự định chạy LLM trên GPU, cài đặt `torch` với hỗ trợ CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Bây giờ môi trường đã sẵn sàng, hãy bắt đầu với mã.

---

## Bước 1 – Khởi tạo Engine OCR và Tải Hình Ảnh Hoá Đơn của Bạn

Điều đầu tiên bạn cần làm là tạo một thể hiện của engine OCR của Aspose và chỉ tới tệp bạn muốn xử lý. Bước này là nền tảng của **cách chạy OCR** trên bất kỳ hình ảnh nào.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Lý do quan trọng:** `load_image` chấp nhận PNG, JPEG, TIFF, và thậm chí các trang PDF, cho phép bạn **thực hiện OCR trên hình ảnh** bất kể định dạng.

## Bước 2 – Chạy OCR Cơ Bản để Thu Thập Văn Bản Thô

Khi hình ảnh đã được tải, engine có thể tạo ra một bản sao chép thô. Đầu ra này thường nhiễu, vì vậy chúng ta sẽ thực hiện bước sửa lỗi sau.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Đầu ra thô điển hình có thể trông như sau:

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Bạn có thấy các số không (`0`) ở nơi lẽ ra là chữ “O” không? Đó chính là loại lỗi chúng ta sẽ sửa sau.

## Bước 3 – Cấu hình Bộ Xử Lý Hậu AI với LLM Nhẹ

Bây giờ chúng ta đưa vào một **mô hình Hugging Face tải xuống** đủ nhỏ để chạy trên phần cứng vừa phải nhưng vẫn mạnh mẽ để hiểu ngôn ngữ hoá đơn. Ví dụ sử dụng mô hình Qwen 2.5 3B‑Instruct GGUF, đã lượng tử thành `int8` để giảm dung lượng bộ nhớ.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Tại sao chọn mô hình này?** Lượng tử `int8` làm giảm kích thước tệp xuống ~1.2 GB, cho phép chạy trên hầu hết laptop. Các lớp GPU tăng tốc suy luận, nhưng mã sẽ tự động chuyển sang CPU nếu không có GPU.

## Bước 4 – Chạy Sửa Lỗi Dựa trên LLM cho Kết Quả OCR Thô

Khi mô hình đã sẵn sàng, chúng ta đưa văn bản thô vào bộ xử lý hậu kỳ. LLM sẽ viết lại bản sao chép, sửa các lỗi OCR phổ biến và chuẩn hoá số.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Kết quả đã được làm sạch dự kiến:

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Bạn có thể thấy các số không đã chuyển lại thành chữ “O”, và “Am0unt” bây giờ là “Amount”. Đây là cốt lõi của việc **tự động sửa lỗi OCR**.

## Bước 5 – Giải Phóng Tài Nguyên và Dọn Dẹp

Các mô hình ngôn ngữ lớn có thể chiếm bộ nhớ GPU, vì vậy nên giải phóng tài nguyên khi hoàn thành.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Nếu bạn dự định xử lý nhiều hoá đơn trong một lô, bạn có thể giữ mô hình tải sẵn và chỉ giải phóng nó vào cuối script.

## Ví dụ Hoạt Động Đầy Đủ

Kết hợp mọi thứ lại, đây là một script đơn có thể lưu vào file `.py` và chạy:

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

Chạy script sẽ tạo ra đầu ra tương tự như khối “AI‑corrected” đã trình bày trước đó. Bạn có thể thay đổi đường dẫn hình ảnh bằng bất kỳ **hoá đơn** hoặc **biên lai** nào khác để **trích xuất văn bản từ hoá đơn** hàng loạt.

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu tôi không có GPU thì sao?

Tham số `gpu_layers` là tùy chọn. Đặt nó thành `0` hoặc bỏ qua, mô hình sẽ chạy hoàn toàn trên CPU. Dự kiến suy luận chậm hơn—khoảng 2–3 giây mỗi trang trên laptop hiện đại.

### Hoá đơn của tôi là PDF đa trang. Làm sao để xử lý chúng?

Chuyển mỗi trang thành một hình ảnh riêng (ví dụ, dùng `pdf2image`) và lặp qua các trang bằng cùng script. Engine OCR có thể xử lý mỗi hình ảnh độc lập, và LLM sẽ sửa mỗi khối văn bản.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Tải mô hình thất bại do tường lửa?

Tải mô hình thủ công từ Hugging Face model hub, giải nén vào thư mục cục bộ, và chỉ định `hugging_face_repo_id` tới đường dẫn địa phương:

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Độ chính xác của việc sửa lỗi như thế nào?

Đối với các hoá đơn tiếng Anh thông thường, LLM sửa hơn 95 % các lỗi OCR phổ biến. Các ghi chú viết tay phức tạp vẫn có thể cần kiểm tra thủ công.

## Mẹo & Thủ Thuật cho Sử Dụng Sản Xuất

- **Xử lý hàng loạt:** Đóng gói các bước 2‑4 trong một hàm và cung cấp danh sách các đường dẫn tệp. Tái sử dụng cùng một thể hiện `AsposeAI` để tránh tải lại mô hình.
- **Ghi log:** Thay `print` bằng mô-đun `logging` của Python để ghi lại cả đầu ra thô và đã sửa cho mục đích kiểm toán.
- **Xử lý lỗi:** Bao quanh lời gọi OCR bằng khối `try/except`. Nếu một hình ảnh thất bại, ghi lại tên tệp và tiếp tục.
- **Tinh chỉnh hiệu năng:** Thử nghiệm với `gpu_layers`. Nhiều lớp trên GPU sẽ tăng tốc suy luận nhưng cũng tăng nhu cầu VRAM.

## Kết Luận

Chúng tôi đã trình bày **cách chạy OCR** trên hình ảnh hoá đơn từ đầu đến cuối, cho bạn thấy cách **thực hiện OCR trên hình ảnh**, **tải mô hình Hugging Face**, và **tự động sửa lỗi OCR**. Script hoàn chỉnh minh họa quy trình thực tiễn mà bạn có thể tích hợp vào bất kỳ pipeline tự động hoá dựa trên Python nào.

Bước tiếp theo? Hãy thử mở rộng pipeline để **trích xuất các trường chính** (số hoá đơn, ngày, tổng tiền) bằng biểu thức chính quy trên văn bản đã sửa, hoặc đưa đầu ra đã làm sạch vào cơ sở dữ liệu để tạo bản ghi có thể tìm kiếm. Bạn cũng có thể thử nghiệm các LLM nhẹ khác từ Hugging Face nếu cần ngôn ngữ hoặc kiến thức chuyên ngành khác.

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn rõ ràng như pha lê!

![cách chạy OCR trên hình ảnh hoá đơn](ocr_invoice_example.png "cách chạy OCR trên hoá đơn")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}