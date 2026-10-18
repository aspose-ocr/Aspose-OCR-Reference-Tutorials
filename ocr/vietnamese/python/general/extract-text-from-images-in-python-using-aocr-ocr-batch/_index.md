---
category: general
date: 2026-06-25
description: Trích xuất văn bản từ hình ảnh bằng thư viện aocr của Python – học OCR
  hàng loạt, đặt chế độ nhận dạng là in, và thêm bộ xử lý hậu kỳ AI.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng thư viện aocr của Python. Hướng
  dẫn này trình bày OCR hàng loạt, chế độ nhận dạng văn bản in và bộ xử lý hậu kỳ
  AI tùy chọn.
og_title: Trích xuất văn bản từ hình ảnh bằng Python – Hướng dẫn đầy đủ aocr Batch
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Trích xuất văn bản từ hình ảnh trong Python bằng aocr OCR Batch
url: /vi/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong Python bằng aocr OCR Batch

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng cảm thấy choáng ngợp bởi hàng chục bước nhỏ? Bạn không phải là người duy nhất. Dù bạn đang số hoá các mẫu quét, lấy dữ liệu từ biên lai, hay xây dựng một kho lưu trữ có thể tìm kiếm, việc có được kết quả OCR đáng tin cậy ở quy mô lớn có thể giống như leo lên một ngọn đồi dốc.

Tin tốt? Với **thư viện aocr** bạn có thể tạo một **Python OCR batch** chỉ trong vài dòng code. Trong hướng dẫn này, chúng ta sẽ đi qua cách tạo một OCR batch, tải mọi hình ảnh được hỗ trợ từ một thư mục, chọn **chế độ nhận dạng printed** phù hợp, và thậm chí gắn một **AI postprocessor** để tăng độ chính xác. Khi hoàn thành, bạn sẽ có một script sẵn sàng chạy để trích xuất văn bản từ hình ảnh và báo cáo lượng văn bản đã thu thập cho mỗi tệp.

## Bạn sẽ học được gì

- Cách cài đặt và import gói `aocr`.
- Thiết lập một `OcrBatch` để tự động xử lý hàng ngàn tệp.
- Chọn chế độ nhận dạng tối ưu cho tài liệu in.
- (Tùy chọn) Kết nối một AI post‑processor để làm sạch kết quả nhiễu.
- Hiển thị đường dẫn tệp cùng với độ dài của văn bản đã trích xuất.
- Mẹo xử lý các trường hợp đặc biệt như định dạng không hỗ trợ hoặc trang trống.

### Yêu cầu trước

- Python 3.8 hoặc mới hơn đã được cài đặt trên máy của bạn.  
- Kiến thức cơ bản về lập trình Python (vòng lặp, import, v.v.).  
- Có sẵn một thư mục chứa các hình ảnh quét (PNG, JPG, TIFF, v.v.).  

Nếu đã có những thứ trên, hãy bắt đầu—không cần dịch vụ bên ngoài.

## Bước 1: Cài đặt Thư viện aocr

Đầu tiên, `aocr` không có trong thư viện chuẩn, vì vậy bạn cần tải nó từ PyPI.

```bash
pip install aocr
```

> **Mẹo chuyên nghiệp:** Sử dụng môi trường ảo (`python -m venv .venv`) để cô lập các phụ thuộc.  

Sau khi cài đặt, bạn có thể import các lớp cốt lõi.

```python
# core imports
import aocr
```

## Bước 2: Tạo một Instance của OCR Batch

`OcrBatch` là động cơ sẽ duyệt qua thư mục của bạn và theo dõi mọi tệp hình ảnh. Hãy tưởng tượng nó như một băng chuyền đưa ảnh vào engine OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Lúc này batch còn trống, nhưng chúng ta sẽ lấp đầy nó ở bước tiếp theo.

## Bước 3: Thêm Tất cả Các Hình ảnh Được Hỗ trợ từ Thư mục (Đệ quy)

Bạn có thể có cấu trúc thư mục lồng nhau—có thể mỗi thư mục con cho một khách hàng hoặc một tháng. Phương thức `add_folder` sẽ tự động duyệt cây thư mục, kéo vào mọi hình ảnh mà nó biết cách đọc.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Thay `"YOUR_DIRECTORY/scanned_forms/"` bằng đường dẫn thực tế trên hệ thống của bạn. Sau lệnh này, `ocr_batch.file_paths` sẽ chứa danh sách các tên tệp tuyệt đối, và batch sẽ biết chính xác có bao nhiêu mục sẽ được xử lý.

## Bước 4: Chọn Chế độ Nhận dạng cho Văn bản In

Engine `aocr` hỗ trợ một số chế độ (handwritten, printed, mixed). Vì chúng ta đang làm việc với các mẫu in sạch, hãy đặt chế độ cho phù hợp. Cờ nhỏ này có thể cải thiện đáng kể độ chính xác vì engine không cần áp dụng các heuristics nặng nề dành cho chữ viết tay.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Tại sao quan trọng:** Văn bản in có các đường cơ sở và hình dạng ký tự nhất quán, cho phép mô hình OCR áp dụng từ điển ký tự chặt chẽ hơn. Nếu để chế độ “auto”, bạn có thể nhận được nhiều nhiễu trên các bản quét độ phân giải thấp.

## Bước 5: (Tùy chọn) Gắn một AI Post‑Processor

Nếu các bản quét của bạn bị mờ, độ tương phản thấp, hoặc phông chữ lạ, một AI post‑processor có thể làm sạch đầu ra OCR thô trước khi chuyển sang các hệ thống downstream. Phương thức `set_ai_postprocessor` nhận một đối tượng thực hiện giao diện `process(text: str) -> str`.

Dưới đây là một ví dụ tối thiểu sử dụng lớp hư cấu `SimpleCleaner`. Trong thực tế, bạn có thể gắn một transformer của HuggingFace, một mô hình ngôn ngữ tùy chỉnh, hoặc thậm chí một bộ kiểm tra chính tả dựa trên quy tắc.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Nếu bỏ qua bước này, batch sẽ chỉ trả về các chuỗi OCR thô.

## Bước 6: Chạy OCR trên Toàn bộ Batch và Thu thập Kết quả

Bây giờ công việc nặng bắt đầu. Phương thức `run` lặp qua mọi tệp, chạy engine OCR, truyền đầu ra qua AI post‑processor (nếu có), và trả về một danh sách các chuỗi—một chuỗi cho mỗi hình ảnh.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Vì phương thức trả về một danh sách Python thuần, bạn có thể xử lý nó như bất kỳ collection nào khác—lưu, ghi vào CSV, hoặc đưa vào cơ sở dữ liệu.

## Bước 7: Hiển thị Đường dẫn Tệp và Độ dài Văn bản Đã Trích xuất

Một kiểm tra nhanh là in ra số ký tự đã trích xuất từ mỗi tệp. Nếu một trang trống hoặc OCR thất bại, bạn sẽ thấy độ dài `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Kết quả thường trông như sau:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Nhìn thấy một `0` ngay lập tức cho biết tệp nào cần xem xét lại (có thể bị hỏng hoặc không phải là hình ảnh).

## Xử lý Các Trường hợp Đặc biệt Thông thường

### 1. Kiểu Tệp Không Hỗ trợ

`aocr` sẽ bỏ qua lặng lẽ các tệp không thể giải mã. Nếu bạn nghi ngờ có PDF hoặc BMP trong thư mục, hãy lọc chúng trước:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Batch Lớn và Tiêu thụ Bộ nhớ

Chạy hàng ngàn bản quét độ phân giải cao có thể làm tăng đáng kể việc sử dụng bộ nhớ. Giảm thiểu bằng cách xử lý theo từng khối:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Trang Trống hoặc Độ Tương phản Thấp

Nếu một trang cho ra ít hơn 10 ký tự, bạn có thể muốn đánh dấu để kiểm tra thủ công:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Ví dụ Hoàn chỉnh

Kết hợp tất cả lại, đây là một script bạn có thể sao chép‑dán và chạy ngay. Lưu lại dưới tên `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Kết quả mong đợi** (rút gọn để ngắn gọn):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Chạy script bằng:

```bash
python batch_ocr.py
```

Nếu mọi thứ được thiết lập đúng, bạn sẽ thấy một dòng cho mỗi hình ảnh, mỗi dòng báo cáo số ký tự của văn bản đã trích xuất.

## Câu hỏi Thường gặp

**Q: Điều này có hoạt động trên PDF không?**  
A: Không có sẵn. `aocr` chỉ xử lý ảnh raster. Chuyển PDF sang PNG/TIFF trước (ví dụ, dùng `pdf2image`).

**Q: Tôi có thể đổi chế độ nhận dạng sang handwritten không?**  
A: Chắc chắn—chỉ cần thay `aocr.RecognitionMode.PRINTED` bằng `aocr.RecognitionMode.HANDWRITTEN`. Thời gian chạy sẽ chậm hơn nhưng kết quả sẽ tốt hơn với các ghi chú viết tay.

**Q: Nếu tôi cần hỗ trợ đa ngôn ngữ thì sao?**  
A: Thư viện đi kèm các gói ngôn ngữ. Cài đặt module ngôn ngữ mong muốn (`pip install aocr-lang-fr` cho tiếng Pháp, v.v.) và đặt `ocr_batch.language = "fr"` trước khi chạy.

## Các Bước Tiếp Theo và Chủ đề Liên quan

- **Xử lý song song:** Bao bọc việc thực thi batch trong một `concurrent.futures.ThreadPoolExecutor` để tận dụng nhiều lõi CPU.  
- **Lưu kết quả:** Ghi `ocr_results` vào CSV hoặc cơ sở dữ liệu SQLite cho các phân tích downstream.  
- **Tích hợp với AI đám mây:** Thay thế `SimpleCleaner` bằng một mô hình transformer từ HuggingFace để có khả năng sửa lỗi chính tả hiện đại.  
- **Fine‑tuning aocr:** Nếu bạn có bộ phông chữ tùy chỉnh, khám phá `aocr.Trainer` để cải thiện độ chính xác chế độ in.

---

Đó là tất cả—bây giờ bạn đã có một nền tảng vững chắc


## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}