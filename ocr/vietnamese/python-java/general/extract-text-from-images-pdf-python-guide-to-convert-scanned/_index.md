---
category: general
date: 2026-06-06
description: Trích xuất văn bản từ các tệp PDF hình ảnh bằng Python OCR. Tìm hiểu
  cách chuyển đổi tài liệu quét sang văn bản một cách nhanh chóng với nhận dạng hàng
  loạt bất đồng bộ.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: vi
og_description: Trích xuất văn bản từ hình ảnh PDF bằng Python. Hướng dẫn chi tiết
  này chỉ cách chuyển đổi tài liệu quét sang văn bản bằng OCR bất đồng bộ.
og_title: Trích xuất văn bản từ PDF hình ảnh – Hướng dẫn OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Trích xuất văn bản từ PDF hình ảnh – Hướng dẫn Python để chuyển đổi tài liệu
  quét thành văn bản
url: /vi/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ PDF Hình ảnh – Hướng dẫn Python để Chuyển Đổi Tài liệu Quét thành Văn bản

Bạn đã bao giờ cần **trích xuất văn bản từ pdf hình ảnh** mà không phải mất hàng giờ gõ lại? Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **chuyển đổi tài liệu quét thành văn bản** bằng một quy trình OCR bất đồng bộ đơn giản trong Python.  

Nếu bạn từng nhìn chằm chằm vào một đống PDF đã quét và nghĩ, “Phải có cách nhanh hơn,” thì bạn đang ở đúng nơi. Chúng tôi sẽ đi qua từng dòng mã, giải thích lý do mỗi phần quan trọng, và thậm chí đề cập đến một vài trường hợp đặc biệt mà bạn có thể gặp phải.

## Những gì Bạn sẽ Học

- Cách khởi tạo một engine OCR và đặt ngôn ngữ nhận dạng.  
- Cơ chế đưa một danh sách hỗn hợp các file PNG và PDF vào bộ nhận dạng hàng loạt.  
- Chạy công việc OCR bất đồng bộ để ứng dụng của bạn vẫn phản hồi được.  
- Lấy kết quả về, ghép chúng với các file nguồn, và in ra đầu ra sạch sẽ.  

**Yêu cầu trước**: Python 3.8+, hiểu biết cơ bản về `asyncio` hoặc `concurrent.futures`, và một thư viện OCR cung cấp lớp `OcrEngine` tương tự như trong ví dụ (ví dụ: Aspose.OCR, wrapper Tesseract, hoặc wrapper tùy chỉnh). Không cần cài đặt phức tạp—chỉ cần cài thư viện và bạn đã sẵn sàng.

![trích xuất văn bản từ pdf hình ảnh](https://example.com/placeholder.png "Ảnh chụp màn hình kết quả OCR – trích xuất văn bản từ pdf hình ảnh")

## Trích xuất Văn bản từ PDF Hình ảnh – Cài Đặt Engine OCR

Điều đầu tiên bạn cần là một thể hiện engine OCR được cấu hình cho ngôn ngữ của tài liệu. Trong ví dụ của chúng tôi, chúng tôi sẽ dùng tiếng Pháp, nhưng bạn có thể thay đổi sang bất kỳ ngôn ngữ nào được hỗ trợ.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Tại sao điều này quan trọng**: Đặt ngôn ngữ từ đầu sẽ cải thiện độ chính xác đáng kể. Engine sử dụng các từ điển và mô hình ký tự riêng cho từng ngôn ngữ; việc cung cấp ngôn ngữ sai là nguyên nhân phổ biến gây ra đầu ra rối rắm.

## Chuẩn bị Danh sách File – Hình ảnh và PDF Cùng Nhau

Bộ nhận dạng hàng loạt của chúng tôi có thể xử lý cả ảnh raster (`.png`, `.jpg`) và các file PDF. Chỉ cần đưa một danh sách Python đơn giản chứa các đường dẫn file.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Mẹo**: Giữ danh sách phẳng; engine sẽ tự động giải nén mỗi trang PDF thành ảnh trước khi nhận dạng. Nếu bạn có hàng ngàn file, hãy cân nhắc chia danh sách thành các batch nhỏ hơn để tránh tăng đột biến bộ nhớ.

## Khởi động Nhận dạng Hàng loạt Bất đồng bộ

Thay vì chặn luồng chính, chúng tôi sẽ khởi chạy công việc OCR ở nền. Phương thức trả về một `Future` sẽ cuối cùng chứa danh sách các đối tượng `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Cách hoạt động**: Bên trong, engine tạo một pool luồng (hoặc một tác vụ async, tùy vào triển khai). Điều này cho phép bạn tiếp tục thực hiện các công việc khác—như cập nhật UI, tải thêm file, hoặc ghi log tiến độ—trong khi phần xử lý nặng diễn ra ở nền.

## Thực hiện Công việc Hữu ích Khi OCR Đang Chạy

Một lỗi thường gặp là ngồi chờ và liên tục poll future trong vòng lặp chặt. Thay vào đó, bạn có thể thực hiện bất kỳ công việc không liên quan nào. Để minh họa, chúng tôi sẽ chỉ in một dòng trạng thái.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Thu thập Kết quả Khi Future Hoàn thành

Khi bạn đã sẵn sàng thu thập đầu ra OCR, sử dụng `as_completed` từ `concurrent.futures`. Mẫu này hoạt động dù bạn có một hay nhiều future.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Bạn sẽ thấy**: Mỗi đường dẫn file kèm theo biểu diễn văn bản thuần được trích xuất. Đối với PDF, `result.text` chứa văn bản đã được nối lại của mọi trang.

### Đầu ra Dự kiến (ví dụ)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Nếu bạn nhận thấy thiếu ký tự, hãy kiểm tra lại ngôn ngữ đã đặt có khớp với ngôn ngữ tài liệu không, và cân nhắc tiền xử lý ảnh (điều chỉnh góc, tăng độ tương phản) trước khi đưa vào engine.

## Xử lý Các Trường hợp Đặc biệt và Những Cạm bẫy Thông thường

| Tình huống | Cách giải quyết |
|-----------|-----------------|
| **Ngôn ngữ hỗn hợp** | Đầu tiên chạy bước phát hiện ngôn ngữ, sau đó khởi tạo các engine riêng cho từng ngôn ngữ. |
| **PDF lớn (> 100 MB)** | Tách PDF thành các trang riêng trên đĩa (ví dụ: dùng `PyPDF2`) và đưa chúng vào như các mục riêng biệt. |
| **Chữ viết không phải Latin** | Đảm bảo thư viện OCR có gói ngôn ngữ cần thiết; một số thư viện yêu cầu tải thêm file dữ liệu. |
| **Nút thắt hiệu năng** | Tăng kích thước pool luồng (`engine.set_thread_pool_size(8)`) hoặc chuyển sang backend hỗ trợ GPU nếu có. |
| **Thiếu văn bản trong ảnh độ phân giải thấp** | Tiền xử lý bằng OpenCV: `cv2.resize`, `cv2.threshold`, và `cv2.medianBlur` để cải thiện khả năng đọc. |

## Ví dụ Hoàn chỉnh (Sẵn sàng Sao chép)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Lưu file này dưới tên `extract_text_async.py`, thay `YOUR_DIRECTORY` bằng đường dẫn tới các file của bạn, cài gói OCR (`pip install your-ocr-lib`), và chạy `python extract_text_async.py`. Bạn sẽ thấy đầu ra console như đã minh họa ở trên.

## Các Bước Tiếp Theo – Vượt Qua Việc Trích xuất Cơ bản

- **Hậu xử lý**: Loại bỏ khoảng trắng thừa, chuẩn hoá Unicode (`unicodedata.normalize`), hoặc chạy bộ kiểm tra chính tả để làm sạch nhiễu OCR.  
- **Đầu ra có cấu trúc**: Xuất kết quả ra CSV, JSON, hoặc trực tiếp vào cơ sở dữ liệu để tìm kiếm downstream.  
- **Batch song song**: Nếu bạn có hàng trăm file, khởi tạo nhiều future và dùng queue để giữ CPU bận mà không làm quá tải bộ nhớ.  
- **Tích hợp với framework web**: Kết nối script này vào endpoint Flask hoặc FastAPI để cung cấp OCR theo yêu cầu như một dịch vụ.

---

### TL;DR

Bạn đã biết cách **trích xuất văn bản từ pdf hình ảnh** bằng một script Python tối thiểu chạy OCR bất đồng bộ, cho phép bạn **chuyển đổi tài liệu quét thành văn bản** trong khi chương trình vẫn phản hồi nhanh. Hãy thử nghiệm các cài đặt ngôn ngữ, kích thước batch, và các thủ thuật tiền xử lý để đạt độ chính xác tối đa.

Có cách tiếp cận nào bạn muốn chia sẻ—có thể là OCR trên ghi chú viết tay hoặc dịch vụ dựa trên đám mây? Hãy để lại bình luận, và chúc bạn lập trình vui vẻ!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích chi tiết từng bước, giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Images Using Aspose.OCR – Allowed Characters](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}