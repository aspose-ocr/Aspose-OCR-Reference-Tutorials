---
category: general
date: 2026-06-06
description: Chạy OCR trên hình ảnh bằng Python và xem các điểm tin cậy. Tìm hiểu
  cách lọc các từ có độ tin cậy thấp, đặt ngưỡng và xử lý các trường hợp đặc biệt.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: vi
og_description: Chạy OCR trên hình ảnh bằng Python, kiểm tra mức độ tin cậy và lọc
  các từ có độ tin cậy thấp. Hướng dẫn này sẽ dẫn bạn qua một ví dụ hoàn chỉnh, có
  thể chạy được.
og_title: Chạy OCR trên hình ảnh bằng Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Chạy OCR trên hình ảnh bằng Python – Hướng dẫn chi tiết từng bước
url: /vi/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên Hình ảnh bằng Python – Hướng dẫn chi tiết từng bước

Bạn đã bao giờ cần **run OCR on image** nhưng không chắc làm sao để lấy văn bản đáng tin cậy từ chúng? Bạn không đơn độc—nhiều nhà phát triển gặp cùng một vấn đề khi các từ được trích xuất trông không ổn và điểm confidence là một bí ẩn.  

Trong hướng dẫn này, chúng ta sẽ đi thẳng vào một giải pháp hoạt động: bạn sẽ thấy cách **run OCR on image**, đọc confidence tổng thể, và lấy ra các từ có confidence thấp có thể cần xem xét thủ công. Khi kết thúc, bạn sẽ có một script có thể tái sử dụng, hiểu vì sao mỗi dòng quan trọng, và biết cách điều chỉnh ngưỡng confidence cho dự án của mình.

## Những gì hướng dẫn này bao gồm

Chúng ta sẽ đi qua toàn bộ quy trình—từ tải hình ảnh đến in ra báo cáo gọn gàng về các từ có confidence dưới mức 80 % confidence mark. Along the way we’ll discuss:

* Chọn một engine OCR vững chắc (chúng tôi sẽ sử dụng **EasyOCR**, một thư viện OCR Python phổ biến)  
* Giải thích thuộc tính `confidence` mà mọi kết quả OCR trả về  
* Lọc các từ bằng ngưỡng **OCR confidence threshold** tùy chỉnh  
* Mở rộng script cho xử lý hàng loạt hoặc các engine thay thế như **pytesseract**  

Không cần kinh nghiệm OCR trước, chỉ cần quen thuộc cơ bản với Python và môi trường làm việc (khuyến nghị Python 3.9+).  

Sẵn sàng biến các ảnh chụp mờ thành văn bản sạch, có thể tìm kiếm? Hãy bắt đầu.

---

## ## Cách chạy OCR trên hình ảnh bằng Python

Phần cốt lõi của hướng dẫn là đoạn mã ba bước phản ánh code bạn đã thấy. Dưới đây chúng tôi sẽ phân tích từng dòng, giải thích lý do, và cung cấp một script đầy đủ, sẵn sàng sao chép.

### Bước 1: Cài đặt và nhập Engine OCR

Đầu tiên, đảm bảo thư viện OCR đã sẵn sàng. **EasyOCR** hoạt động ngay lập tức cho nhiều ngôn ngữ và cung cấp điểm confidence cho mỗi từ.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Why EasyOCR?* It bundles a deep‑learning model that’s been trained on diverse datasets, so you typically get higher confidence values than the older Tesseract engine, especially on mixed‑quality images.

> **Pro tip:** If you’re on a constrained environment (e.g., a tiny Docker container), `pytesseract` might be lighter, but you’ll lose some of the modern accuracy EasyOCR provides.

### Bước 2: Chạy OCR trên hình ảnh

Bây giờ chúng ta thực sự **run OCR on image**. Phương thức `recognize_image` từ ví dụ gốc được thay thế bằng lời gọi `readtext` của EasyOCR, trả về một danh sách các tuple `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Mỗi mục trong `ocr_results` trông như sau:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Phần tử thứ ba (`0.92` trong ví dụ) là điểm confidence, giá trị từ 0 đến 1.

### Bước 3: Tổng hợp Confidence Tổng thể

Khác với đoạn mã trước đây chỉ in một thuộc tính `confidence` duy nhất, EasyOCR cung cấp confidence cho mỗi từ. Để có cái nhìn tổng thể, chúng ta sẽ tính trung bình chúng:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Why average?* It gives you a quick health check—if the overall confidence is below, say, 70 %, you probably need to improve the image (better lighting, preprocessing, etc.).

### Bước 4: Liệt kê các từ có Confidence thấp

Bây giờ là phần trả lời trực tiếp yêu cầu “liệt kê các từ có confidence dưới ngưỡng mong muốn”. Chúng ta sẽ đặt **OCR confidence threshold** mặc định là 0.80 (80 %), nhưng bạn có thể điều chỉnh.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Vòng lặp in ra mỗi từ không đạt ngưỡng, kèm theo confidence dưới dạng phần trăm. Đây là tương đương chính xác với vòng lặp gốc `for recognized_word in recognition_result.words`, nhưng bây giờ hoạt động với định dạng đầu ra của EasyOCR.

---

## ## Hiểu về Điểm Confidence trong OCR

Confidence không phải là một con số ma thuật; nó là ước lượng của mô hình về mức độ chắc chắn đối với một bản sao cụ thể. Dưới đây là một vài điểm cần lưu ý:

| Tình huống | Confidence điển hình | Cần làm gì |
|-----------|-------------------|------------|
| Quét rõ, độ phân giải cao | 0.95 – 1.00 | Không cần công việc bổ sung |
| Mờ nhẹ hoặc ánh sáng không đồng đều | 0.80 – 0.94 | Xem xét tiền xử lý nhẹ (tăng độ tương phản) |
| Nhiễu mạnh, văn bản bị quay | < 0.70 | Áp dụng tiền xử lý hình ảnh (điều chỉnh góc, giảm nhiễu) hoặc chuyển sang engine OCR khác |

> **Cảnh báo:** Một số ngôn ngữ (ví dụ, chữ viết tay cursive) tự nhiên cho điểm thấp hơn. Điều chỉnh ngưỡng cho phù hợp.

### Các trường hợp đặc biệt & Biến thể

1. **Xử lý hàng loạt** – Nếu bạn cần **run OCR on image** nhiều tệp, hãy bọc logic trên trong một vòng lặp duyệt qua thư mục.  
2. **Nhiều ngôn ngữ** – Truyền một danh sách như `['en', 'fr']` vào `easyocr.Reader` và engine sẽ phát hiện cả hai.  
3. **Engine thay thế** – Muốn thử **pytesseract**? Thay thế khối reader bằng:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Bạn sẽ cần tổng hợp confidence từng ký tự thành giá trị confidence cho mỗi từ—một chút công việc nhưng có thể thực hiện.

4. **Mẹo tiền xử lý** – Áp dụng các bộ lọc OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) có thể tăng confidence cho các bản quét nhiễu.  

---

## ## Script đầy đủ, sẵn sàng chạy

Dưới đây là file Python hoàn chỉnh bạn có thể đưa vào dự án. Lưu dưới tên `ocr_report.py` và chạy `python ocr_report.py`. Đảm bảo đường dẫn hình ảnh trỏ tới một tệp thực tế.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Kết quả mong đợi** (các số của bạn có thể khác):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Nếu mọi từ đều vượt qua ngưỡng 80 % bạn sẽ thấy thông báo thân thiện “All words meet the confidence threshold.” thay vì.

---

## ## Câu hỏi thường gặp (FAQ)

**Q: Điều này có hoạt động với PDF không?**  
A: Không trực tiếp. Chuyển mỗi trang PDF thành hình ảnh trước (ví dụ, bằng `pdf2image`) rồi đưa PNG/JPEG vào script.

**Q: Các số confidence của tôi đều thấp—tôi có thể làm gì?**  
A: Thử tiền xử lý hình ảnh: tăng độ tương phản, loại bỏ nhiễu nền, hoặc xoay ảnh thành chiều ngang. EasyOCR cũng chấp nhận tham số `contrast_ths` mà bạn có thể điều chỉnh.

**Q: Tôi có thể xuất kết quả ra CSV không?**  
A: Chắc chắn. Sau vòng lặp low‑confidence, ghi `ocr_results` vào một `csv.DictWriter` trong đó mỗi hàng chứa `text`, `confidence`, và tọa độ bounding‑box.

**Q: Có phiên bản tăng tốc bằng GPU không?**  
A: EasyOCR tự động sử dụng CUDA nếu có GPU tương thích và PyTorch được cài đặt. Kiểm tra bằng `torch.cuda.is_available()` trước khi chạy script.

---

## Kết luận

Chúng tôi vừa **run OCR on image** bằng Python, kiểm tra confidence tổng thể, và tách ra các từ có confidence thấp cần một

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách đặt giá trị ngưỡng trong nhận dạng OCR hình ảnh](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Cách sử dụng Aspose OCR để nhận kết quả JSON trong nhận dạng hình ảnh](/ocr/english/net/text-recognition/get-result-as-json/)
- [Trích xuất văn bản từ hình ảnh – Tối ưu hóa OCR với Aspose.OCR cho .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}