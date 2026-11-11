---
category: general
date: 2026-04-29
description: Tìm hiểu cách chạy OCR trên các bản quét của bạn, sử dụng mô hình Hugging
  Face tự động và nhận dạng văn bản từ các bản quét bằng Aspose OCR trong vài phút.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: vi
og_description: Cách chạy OCR trên các bản quét bằng Aspose OCR, tự động tải xuống
  mô hình Hugging Face và nhận văn bản sạch, có dấu câu.
og_title: Cách chạy OCR với Aspose & Hugging Face – Hướng dẫn đầy đủ
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Cách chạy OCR với Aspose & Hugging Face – Hướng dẫn đầy đủ
url: /vi/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hướng Dẫn Chạy OCR với Aspose & Hugging Face – Toàn Bộ Quy Trình

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một đống tài liệu đã quét mà không phải tốn hàng giờ chỉnh sửa cài đặt chưa? Bạn không phải là người duy nhất. Trong nhiều dự án, các nhà phát triển cần **nhận dạng văn bản từ ảnh quét** nhanh chóng, nhưng lại gặp khó khăn với việc tải mô hình và xử lý hậu kỳ.  

Tin tốt: hướng dẫn này sẽ cho bạn một giải pháp đã sẵn sàng chạy, **sử dụng mô hình Hugging Face**, tự động tải về và thêm dấu câu để kết quả trông như được con người viết. Khi kết thúc, bạn sẽ có một script xử lý mọi hình ảnh trong một thư mục và tạo file `.txt` sạch sẽ bên cạnh mỗi ảnh quét.

## Những Gì Bạn Cần Chuẩn Bị

- Python 3.8+ (code dùng f‑strings, các phiên bản cũ hơn sẽ không hoạt động)
- Gói `aspose-ocr` (cài đặt bằng `pip install aspose-ocr`)
- Kết nối Internet để tải mô hình lần đầu tiên  
- Một thư mục chứa các ảnh quét (`.png`, `.jpg`, hoặc `.tif`)

Đó là tất cả—không cần binary bổ sung, không cần can thiệp mô hình thủ công. Hãy bắt đầu.

![how to run OCR example](https://example.com/ocr-demo.png "hướng dẫn chạy OCR")

## Bước 1: Nhập Các Lớp Aspose OCR & Thiết Lập Môi Trường

Chúng ta bắt đầu bằng cách kéo các lớp cần thiết từ thư viện Aspose OCR. Nhập toàn bộ ở đầu giúp script gọn gàng và dễ phát hiện các phụ thuộc còn thiếu.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Lý do quan trọng*: `OcrEngine` thực hiện công việc nặng, trong khi `AsposeAI` cho phép chúng ta gắn một mô hình ngôn ngữ lớn để xử lý hậu kỳ thông minh hơn. Nếu bỏ qua việc nhập, phần còn lại của code sẽ không biên dịch—vì vậy đừng quên.

## Bước 2: Cấu Hình Mô Hình Hugging Face Có Hỗ Trợ GPU  

Bây giờ chúng ta chỉ định cho Aspose nơi tải mô hình và số lớp sẽ chạy trên GPU. Cờ `allow_auto_download="true"` thực hiện việc **tự động tải mô hình** cho bạn.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Mẹo chuyên nghiệp**: Nếu bạn không có GPU, đặt `gpu_layers=0`. Mô hình sẽ chuyển sang CPU, chậm hơn nhưng vẫn hoạt động.

### Tại Sao Chọn Mô Hình Hugging Face?

Hugging Face lưu trữ một bộ sưu tập khổng lồ các LLM đã sẵn sàng dùng. Khi trỏ tới `Qwen/Qwen2.5-3B-Instruct-GGUF`, bạn nhận được một mô hình gọn nhẹ, được tinh chỉnh để thực hiện lệnh, có khả năng thêm dấu câu, chỉnh sửa khoảng cách và thậm chí sửa các lỗi OCR nhỏ. Đây chính là bản chất của **use hugging face model** trong thực tế.

## Bước 3: Khởi Tạo AI Engine và Bật Xử Lý Hậu Kỳ Dấu Câu  

AI engine không chỉ để chat—ở đây chúng ta gắn một *punctuation adder* để làm sạch đầu ra OCR thô.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Điều gì đang diễn ra?* Lệnh `set_post_processor` đăng ký một bộ xử lý hậu kỳ tích hợp, chạy sau khi engine OCR hoàn thành. Nó nhận chuỗi thô và chèn dấu phẩy, dấu chấm và chữ hoa ở những vị trí thích hợp, làm cho văn bản cuối cùng dễ đọc hơn rất nhiều.

## Bước 4: Tạo OCR Engine và Gắn AI Engine  

Kết nối AI engine với OCR engine cho chúng ta một đối tượng duy nhất có thể đọc ký tự và tinh chỉnh kết quả.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Nếu bỏ qua bước này, OCR vẫn hoạt động, nhưng bạn sẽ mất phần tăng cường dấu câu—kết quả sẽ giống như một dải các từ liền nhau.

## Bước 5: Xử Lý Mọi Ảnh Trong Thư Mục  

Đây là phần cốt lõi của hướng dẫn. Chúng ta lặp qua từng ảnh, chạy OCR, áp dụng bộ xử lý hậu kỳ, và ghi văn bản đã làm sạch vào file `.txt` bên cạnh.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### Những Gì Bạn Có Thể Mong Đợi

Chạy script sẽ in ra thứ gì đó như:

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Mỗi dòng cho bạn biết điểm confidence (kiểm tra nhanh sức khỏe) và tạo các file `invoice_001.png.txt`, `receipt_2024.tif.txt`, v.v., chứa văn bản có dấu câu, dễ đọc cho con người.

### Các Trường Hợp Đặc Biệt & Biến Thể

- **Ảnh không phải tiếng Anh**: Đổi `hugging_face_repo_id` sang mô hình đa ngôn ngữ (ví dụ `microsoft/Multilingual-LLM-GGUF`).
- **Lô lớn**: Bao bọc vòng lặp trong `concurrent.futures.ThreadPoolExecutor` để xử lý song song, nhưng cần chú ý tới giới hạn bộ nhớ GPU.
- **Xử lý hậu kỳ tùy chỉnh**: Thay `"punctuation_adder"` bằng script của bạn nếu cần làm sạch đặc thù (ví dụ, loại bỏ số hóa đơn).

## Bước 6: Dọn Dẹp Tài Nguyên  

Khi công việc kết thúc, giải phóng tài nguyên ngăn ngừa rò rỉ bộ nhớ, đặc biệt quan trọng nếu bạn chạy script trong một dịch vụ lâu dài.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Bỏ qua bước này có thể để lại bộ nhớ GPU bị kẹt, gây ảnh hưởng tới các lần chạy tiếp theo.

## Tóm Tắt: Cách Chạy OCR Từ Đầu Đến Cuối  

Chỉ trong vài dòng lệnh, chúng ta đã minh họa **cách chạy OCR** trên một thư mục các ảnh quét, **sử dụng mô hình Hugging Face** tự tải lần đầu, và **nhận dạng văn bản từ ảnh quét** với dấu câu được tự động thêm. Script hoàn chỉnh sẵn sàng sao chép, điều chỉnh đường dẫn và thực thi.

## Các Bước Tiếp Theo & Chủ Đề Liên Quan  

- **Xử lý hậu kỳ hàng loạt**: Khám phá `ocr_engine.run_batch_postprocessor` để xử lý bulk nhanh hơn.  
- **Mô hình thay thế**: Thử họ họ `openai/whisper` nếu bạn cần chuyển giọng nói thành văn bản cùng với OCR.  
- **Tích hợp với cơ sở dữ liệu**: Lưu trữ văn bản đã trích xuất vào SQLite hoặc Elasticsearch để tạo kho lưu trữ có thể tìm kiếm.  

Hãy thoải mái thử nghiệm—đổi mô hình, điều chỉnh `gpu_layers`, hoặc thêm bộ xử lý hậu kỳ của riêng bạn. Sự linh hoạt của Aspose OCR kết hợp với hub mô hình của Hugging Face tạo nên nền tảng đa năng cho bất kỳ dự án số hoá tài liệu nào.

---

*Chúc lập trình vui! Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc tham khảo tài liệu Aspose OCR để biết các tùy chọn cấu hình sâu hơn.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}