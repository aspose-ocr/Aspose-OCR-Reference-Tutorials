---
category: general
date: 2026-06-22
description: Tiền xử lý hình ảnh cho OCR để trích xuất văn bản từ hình ảnh và cải
  thiện độ chính xác của OCR bằng Aspose OCR trong Python. Bao gồm ví dụ đầy đủ, có
  thể chạy được.
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: vi
og_description: Tiền xử lý hình ảnh cho OCR, trích xuất văn bản từ hình ảnh và cải
  thiện độ chính xác của OCR với Aspose OCR. Tìm hiểu quy trình làm việc đầy đủ bằng
  Python.
og_title: Tiền xử lý ảnh cho OCR – Hướng dẫn Python đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Python từng bước
url: /vi/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý hình ảnh cho OCR – Hướng dẫn Python toàn diện

Nếu bạn cần **preprocess image for OCR**, có lẽ bạn đã gặp phải các bản scan nhiễu, trang bị lệch, hoặc ảnh có độ tương phản thấp không hợp tác. Đã bao giờ bạn cố gắng trích xuất văn bản từ hình ảnh mà chỉ nhận được một mớ hỗn độn? Đó là lúc một chuỗi tiền xử lý vững chắc có thể tạo ra sự khác biệt giữa một vài từ có thể đọc được và một cơn ác mộng sao chép toàn bộ.

Trong hướng dẫn này chúng tôi sẽ đi qua một ví dụ hoàn chỉnh, từ đầu đến cuối mà **extracts text from image** đồng thời chỉ cho bạn cách **improve OCR accuracy** bằng Aspose OCR cho Python. Không có tham chiếu mơ hồ—chỉ có mã bạn có thể sao chép‑dán, lý do đằng sau mỗi dòng, và các mẹo cho các trường hợp thực tế.

## Những gì bạn sẽ nhận được

- Một script Python sẵn sàng chạy, tải tài liệu nhiễu, làm sạch và in ra văn bản đã nhận dạng.  
- Hiểu tại sao mỗi bộ lọc tiền xử lý quan trọng và cách điều chỉnh các tham số của chúng.  
- Các chiến lược xử lý các vấn đề thường gặp như nhiễu hạt mạnh, xoay nghiêng cực độ, hoặc scan độ tương phản thấp.  

### Yêu cầu trước

| Yêu cầu | Lý do quan trọng |
|-------------|----------------|
| Python 3.8+ | Các gói wheels của Aspose OCR nhắm vào các trình thông dịch hiện đại. |
| `aspose-ocr` package (`pip install aspose-ocr`) | Cung cấp `OcrEngine`, `ImagePreprocessor`, và các lớp filter. |
| A sample image (e.g., `noisy-document.jpg`) | Chúng tôi sẽ sử dụng một bức ảnh cố ý lộn xộn để minh họa lợi ích của tiền xử lý. |
| Basic familiarity with Python functions | Giúp bạn điều chỉnh script cho quy trình của riêng mình. |

> **Mẹo chuyên nghiệp:** Nếu bạn đang dùng Windows, chạy script trong môi trường ảo để tránh xung đột phiên bản.

## Tiền xử lý hình ảnh cho OCR với Aspose OCR (Python)

Dưới đây là phần cốt lõi của tutorial—phân tích từng bước mã bạn sẽ cần. Mỗi phần giải thích **what** chúng ta đang làm *và* **why** chúng ta làm, để bạn có thể tinh chỉnh pipeline sau này mà không phải đoán mò.

![preprocess image for OCR example](ocr-preprocess.png){alt="ví dụ tiền xử lý hình ảnh cho OCR"}

### Bước 1 – Khởi tạo OCR Engine và tải hình ảnh nguồn của bạn

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **Why** an `OcrEngine`? Nó bao gói bộ nhận dạng, cài đặt ngôn ngữ, và (sau này) preprocessor.  
- **Why** `ImageStream.from_file`? Nó trừu tượng hoá việc xử lý loại file, vì vậy bạn có thể thay JPEG bằng PNG mà không cần thay đổi mã.

### Bước 2 – Xây dựng chuỗi tiền xử lý để làm sạch hình ảnh

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**Cách các filter này tăng độ chính xác OCR:**  
- **Deskew** loại bỏ vấn đề “trang nghiêng” phổ biến khiến việc phân đoạn ký tự bị rối.  
- **Despeckle** nhắm vào các hạt nhiễu do máy quét chất lượng thấp tạo ra; độ mạnh cao hơn loại bỏ nhiều nhiễu hơn nhưng có thể làm mòn chi tiết mỏng.  
- **ContrastBoost** làm cho văn bản tối nổi bật hơn trên nền sáng, một lợi thế cổ điển cho hầu hết các engine OCR.

> **Edge case:** Nếu tài liệu của bạn đã thẳng hoàn hảo, bạn có thể bỏ qua `Deskew()` để tiết kiệm vài mili giây.

### Bước 3 – Gắn Preprocessor vào Engine

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

Bây giờ mỗi khi `ocr_engine.recognize()` chạy, nó sẽ đầu tiên chạy ba filter theo đúng thứ tự chúng ta đã định nghĩa. Thứ tự quan trọng: bạn muốn **deskew before despeckling**, nếu không filter despeckle có thể hiểu sai các cạnh đã xoay thành nhiễu.

### Bước 4 – Chạy OCR và Trích xuất Văn bản từ Hình ảnh

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- Lệnh `recognize()` trả về một đối tượng `RecognitionResult` chứa không chỉ văn bản thô mà còn điểm tin cậy, hộp bao và thông tin ngôn ngữ.  
- Ở đây chúng ta chỉ cần chuỗi thuần, nhưng bạn có thể khám phá `recognition_result.get_confidence()` để kiểm tra nhanh **improve OCR accuracy**.

### Bước 5 – Xác minh Kết quả và Tinh chỉnh để Độ chính xác Tốt hơn

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

Nếu kết quả vẫn còn chứa các ký tự rối, hãy cân nhắc các điều chỉnh sau:

| Vấn đề | Giải pháp đề xuất |
|-------|-------------------|
| Văn bản vẫn mờ | Tăng `ContrastBoost(level)` lên 2.0 hoặc thêm `ocr.Filters.GaussianBlur(radius=1)` trước despeckling. |
| Quá nhiều ký tự lẻ | Tăng `Despeckle(strength)` lên 3, hoặc chèn `ocr.Filters.RemoveLines()` để loại bỏ các đường ngang. |
| Vẫn còn nghiêng | Gọi `ocr.Filters.Deskew(max_angle=5)` để giới hạn sửa chữa chỉ ở các góc nhẹ. |

## Script Đầy đủ, Có thể Chạy

Sao chép khối dưới đây vào một file có tên `ocr_preprocess.py`. Thay `YOUR_DIRECTORY/noisy-document.jpg` bằng đường dẫn thực tế tới hình ảnh của bạn, sau đó chạy `python ocr_preprocess.py`.

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

Chạy script này trên một file JPEG nhiễu, hơi xoay sẽ cho ra văn bản sạch, dễ đọc—điểm chứng cách một chuỗi tiền xử lý được thiết kế tốt **improves OCR accuracy** một cách đáng kể.

## Câu hỏi Thường gặp & Trả lời

**Q: Does this work with multi‑page PDFs?**  
A: Có. Chuyển mỗi trang thành một hình ảnh (ví dụ, dùng `pdf2image`) và đưa vào cùng một pipeline trong một vòng lặp. Các bước `preprocess image for OCR` vẫn áp dụng cho mỗi trang.

**Q: What if my document is in a language other than English?**  
A: Đặt ngôn ngữ trước khi nhận dạng: `engine.set_language(ocr.Language.FRENCH)`. Các filter tiền xử lý vẫn giữ nguyên; chỉ mô hình ngôn ngữ thay đổi.

**Q: Can I chain more filters?**  
A: Chắc chắn rồi. `ImagePreprocessor` có thể mở rộng—chỉ cần gọi `add_filter` lần nữa. Đối với nền có nhiều chấm, `ocr.Filters.MedianFilter(kernel=3)` có thể hữu ích.

## Tổng kết

Chúng ta vừa **preprocess image for OCR**, chạy engine của Aspose, và **extract text from image** đồng thời giới thiệu một số mẹo để **improve OCR accuracy**. Ví dụ hoàn chỉnh đã sẵn sàng để đưa vào bất kỳ dự án nào, và thiết kế filter mô-đun cho phép bạn thay đổi, thêm hoặc bỏ bớt các bước tùy theo dữ liệu.

Tiếp theo, bạn có thể khám phá:

- **Batch processing** hàng chục bản scan với `concurrent.futures`.  
- **Post‑processing** bằng các thư viện kiểm tra chính tả (ví dụ, `pyspellchecker`) để làm sạch các lỗi chính tả do OCR tạo ra.  
- **Integrating** script vào một dịch vụ web dùng Flask hoặc FastAPI, biến nó thành một micro‑service OCR theo yêu cầu.

Hãy thử, điều chỉnh độ mạnh của các filter, và quan sát tỉ lệ nhận dạng của bạn tăng lên. Nếu gặp khó khăn, để lại bình luận—chúc bạn lập trình vui! 

## Bạn Nên Học Gì Tiếp Theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh với Aspose OCR – Hướng dẫn Chi Tiết](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách sử dụng AspOCR: Bộ lọc Tiền xử lý Hình ảnh OCR cho .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Trích xuất Văn bản từ Hình ảnh – Tối ưu OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}