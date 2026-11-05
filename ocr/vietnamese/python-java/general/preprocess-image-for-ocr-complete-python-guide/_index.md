---
category: general
date: 2026-06-28
description: Tiền xử lý hình ảnh cho OCR bằng Python để tăng độ chính xác. Học quy
  trình tiền xử lý hình ảnh toàn diện, cải thiện kết quả OCR và trích xuất văn bản
  từ hình ảnh Cyrillic.
draft: false
keywords:
- preprocess image for OCR
- how to improve OCR accuracy
- python OCR with preprocessing
- image preprocessing pipeline python
- extract text from Cyrillic image
language: vi
og_description: Tiền xử lý hình ảnh cho OCR bằng Python và học cách cải thiện độ chính
  xác của OCR. Hướng dẫn này sẽ đưa bạn qua quy trình tiền xử lý hoàn chỉnh và trích
  xuất văn bản từ các hình ảnh Cyrillic.
og_title: Tiền xử lý ảnh cho OCR – Hướng dẫn Python đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  headline: Preprocess Image for OCR – Complete Python Guide
  type: TechArticle
- description: Preprocess image for OCR with Python to boost accuracy. Learn a full
    image preprocessing pipeline, improve OCR results, and extract text from Cyrillic
    images.
  name: Preprocess Image for OCR – Complete Python Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the code works on 3.10+ as well). - Basic familiarity
      with Python packages and virtual environments. - An OCR library that provides
      `OcrEngine`, `Language`, and `ImagePreprocessor` classes (e.g., a wrapper around
      Tesseract or a commercial SDK). - A sample Cyrillic image (`cyri'
  - name: Why These Three Steps?
    text: 1. **Deskew** – OCR engines assume left‑to‑right (or top‑to‑bottom) alignment.
      A few degrees of rotation can drop accuracy by 30 % or more. 2. **Binarize**
      – Converting to a binary image reduces the data the OCR engine must analyze,
      sharpening character edges. 3. **Denoise** – Small specks or compre
  - name: How This Improves OCR Accuracy
    text: '- By feeding a **clean, deskewed, binarized** image, the engine can focus
      on character shapes rather than fighting noise. - Specifying `Language.Cyrillic`
      activates the correct character set and language model, which is a key factor
      in **how to improve OCR accuracy** for non‑Latin scripts.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Python toàn diện
url: /vi/python-java/general/preprocess-image-for-ocr-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý ảnh cho OCR – Hướng dẫn Python đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào để **tiền xử lý ảnh cho OCR** sao cho văn bản trở nên trong suốt? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp khó khăn khi engine OCR trả về các ký tự lộn xộn, đặc biệt với các bản quét Cyrillic bị nghiêng hoặc nhiễu. Tin tốt là gì? Một pipeline tiền xử lý ảnh được thiết kế tốt có thể tăng đáng kể tỷ lệ nhận dạng.

Trong hướng dẫn này, chúng ta sẽ ngay lập tức đi sâu vào giải pháp **Python OCR với tiền xử lý** giải quyết việc chỉnh nghiêng, nhị phân hoá và giảm nhiễu, sau đó chỉ cho bạn cách **trích xuất văn bản từ ảnh Cyrillic**. Khi kết thúc, bạn sẽ có một script có thể tái sử dụng, hiểu **cách cải thiện độ chính xác OCR**, và sẵn sàng điều chỉnh pipeline cho bất kỳ ngôn ngữ hay nguồn ảnh nào.

## Những gì bạn sẽ học

- Lý do đằng sau mỗi bước tiền xử lý và tại sao chúng quan trọng đối với OCR.
- Cách xây dựng một **image preprocessing pipeline python** có thể tái sử dụng trong nhiều dự án.
- Một ví dụ hoàn chỉnh, có thể chạy được, tạo engine OCR, tiền xử lý ảnh Cyrillic và in ra văn bản đã nhận dạng.
- Mẹo xử lý các trường hợp biên như nghiêng quá mức, độ tương phản thấp, hoặc tài liệu đa ngôn ngữ.
- Các ý tưởng bước tiếp theo như xử lý hàng loạt, gói ngôn ngữ tùy chỉnh, và tích hợp với các dịch vụ OCR đám mây.

### Yêu cầu trước

- Python 3.8 hoặc mới hơn (mã cũng chạy trên 3.10+).
- Kiến thức cơ bản về các package Python và môi trường ảo.
- Thư viện OCR cung cấp các lớp `OcrEngine`, `Language`, và `ImagePreprocessor` (ví dụ: một wrapper quanh Tesseract hoặc SDK thương mại).  
- Một ảnh mẫu Cyrillic (`cyrillic_skewed.jpg`) được đặt trong thư mục bạn kiểm soát.

> **Mẹo chuyên nghiệp:** Nếu bạn chưa có wrapper OCR sẵn có, hãy xem xét gói mã nguồn mở `pytesseract` và kết hợp nó với `opencv-python`. Các khái niệm trong hướng dẫn này có thể áp dụng trực tiếp.

---

## Bước 1: Cài đặt và nhập các package cần thiết

Đầu tiên, hãy giải quyết các phụ thuộc. Chúng ta sẽ sử dụng một `ocr_lib` giả định, bao gồm engine và các tiện ích tiền xử lý. Nếu bạn dùng `pytesseract` + OpenCV, hãy thay đổi các import cho phù hợp.

```python
# Install the (fictional) OCR library – replace with your actual package manager command
# pip install ocr-lib

from ocr_lib import OcrEngine, Language, ImagePreprocessor
import os
```

> **Tại sao điều này quan trọng:** Việc nhập đúng các lớp đảm bảo chúng ta có sự tách biệt rõ ràng giữa engine OCR (nhận dạng) và bộ tiền xử lý ảnh (cải thiện). Kết hợp chúng có thể dẫn đến mã rối rắm, khó gỡ lỗi.

---

## Bước 2: Xây dựng một **Preprocess Image for OCR** Pipeline

Bây giờ chúng ta sẽ tạo phần cốt lõi của hướng dẫn: một pipeline thực hiện chỉnh nghiêng, nhị phân hoá và giảm nhiễu đầu vào. Mỗi chuyển đổi nhắm vào một điểm yếu cụ thể của các engine OCR.

```python
# Step 2: Initialise the pre‑processing chain
preprocessor = ImagePreprocessor()

# Deskew – correct rotation so text lines are horizontal
preprocessor = preprocessor.deskew()

# Binarize – convert to pure black‑and‑white using a threshold (180 works well for most scans)
preprocessor = preprocessor.binarize(threshold=180)

# Remove noise – apply a mild median filter (strength=2) to smooth speckles
preprocessor = preprocessor.removeNoise(strength=2)
```

### Tại sao lại có ba bước này?

1. **Deskew** – Các engine OCR giả định sự căn chỉnh từ trái sang phải (hoặc từ trên xuống dưới). Một vài độ xoay có thể làm giảm độ chính xác tới 30 % hoặc hơn.  
2. **Binarize** – Chuyển đổi sang ảnh nhị phân giảm lượng dữ liệu mà engine OCR phải phân tích, làm nét hơn các cạnh ký tự.  
3. **Denoise** – Các đốm nhỏ hoặc artefact nén có thể bị nhầm thành dấu câu hoặc dấu phụ, đặc biệt trong Cyrillic nơi nhiều chữ có hình dạng tương tự.

> **Lưu ý trường hợp biên:** Nếu ảnh nguồn của bạn đã sạch, bạn có thể bỏ qua `removeNoise` hoặc giảm tham số `strength`. Việc giảm nhiễu quá mạnh có thể xóa bỏ các chi tiết mỏng như dấu phụ.

---

## Bước 3: Tải ảnh và áp dụng pipeline

Khi pipeline đã sẵn sàng, chúng ta cung cấp cho nó một đường dẫn tệp. Phương thức `apply` trả về một đối tượng ảnh đã xử lý mà engine OCR có thể tiêu thụ trực tiếp.

```python
# Path to the original Cyrillic image (adjust as needed)
image_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")

# Run the preprocessing pipeline
processed_image = preprocessor.apply(image_path)
```

Nếu bạn cần xem trước kết quả, có thể ghi nó ra đĩa:

```python
# Optional: save the preprocessed image for visual verification
processed_image.save("preprocessed_cyrillic.jpg")
print("Preprocessed image saved – check the file to confirm deskewing and binarization.")
```

> **Tại sao cần xem trước?** Nhìn thấy ảnh đã biến đổi giúp bạn tinh chỉnh ngưỡng. Đôi khi ngưỡng 180 quá mạnh; giảm xuống 150 có thể giữ lại các nét mỏng.

---

## Bước 4: Cài đặt engine OCR và nhận dạng văn bản

Bây giờ chúng ta chuyển sang phần OCR thực tế. Chúng ta sẽ cấu hình engine để sử dụng gói ngôn ngữ Cyrillic, điều này cần thiết để **trích xuất văn bản từ ảnh Cyrillic**.

```python
# Initialise the OCR engine
engine = OcrEngine()

# Tell the engine we’re working with Cyrillic text
engine.setLanguage(Language.Cyrillic)

# Perform recognition on the preprocessed image
ocr_result = engine.recognizeImage(processed_image)

# Extract plain text from the OCR result object
recognized_text = ocr_result.getText()
print("=== Recognized Text ===")
print(recognized_text)
```

### Cách cách này cải thiện độ chính xác OCR

- Bằng cách cung cấp một ảnh **sạch, đã chỉnh nghiêng, đã nhị phân hoá**, engine có thể tập trung vào hình dạng ký tự thay vì đấu tranh với nhiễu.  
- Đặt `Language.Cyrillic` kích hoạt bộ ký tự và mô hình ngôn ngữ đúng, là yếu tố then chốt trong **cách cải thiện độ chính xác OCR** cho các script không phải Latin.

---

## Bước 5: Đóng gói mọi thứ vào một hàm có thể tái sử dụng (Tùy chọn)

Nếu bạn dự định xử lý nhiều tệp, việc đóng gói logic sẽ làm cho mã của bạn sạch hơn và dễ bảo trì hơn.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Preprocess an image and extract Cyrillic text using the OCR engine.

    Parameters
    ----------
    image_path : str
        Full path to the source image.

    Returns
    -------
    str
        Recognized Cyrillic text.
    """
    # Build the preprocessing pipeline (could be cached for performance)
    preprocessor = (ImagePreprocessor()
                    .deskew()
                    .binarize(threshold=180)
                    .removeNoise(strength=2))

    processed = preprocessor.apply(image_path)

    engine = OcrEngine()
    engine.setLanguage(Language.Cyrillic)

    result = engine.recognizeImage(processed)
    return result.getText()


# Example usage
if __name__ == "__main__":
    sample_path = os.path.join("YOUR_DIRECTORY", "cyrillic_skewed.jpg")
    text = extract_cyrillic_text(sample_path)
    print("Extracted Cyrillic text:")
    print(text)
```

> **Tại sao lại dùng hàm?** Nó tách biệt logic tiền xử lý, giúp dễ dàng thay đổi ngôn ngữ khác hoặc điều chỉnh tham số mà không cần viết lại toàn bộ script.

---

## Những khó khăn thường gặp và cách khắc phục

| Issue | Symptom | Fix |
|-------|----------|-----|
| **Nghiêng quá mức (>15°)** | Văn bản xuất hiện lộn xộn hoặc thiếu | Tăng độ bền của `deskew()` hoặc tự quay trước bằng cách sử dụng `getRotationMatrix2D` của OpenCV. |
| **Độ tương phản thấp** | Nhị phân hoá làm mọi thứ trở nên trắng | Giảm giá trị `threshold` hoặc áp dụng bước kéo dài độ tương phản trước khi `binarize()`. |
| **Kích thước phông chữ nhỏ** | Các ký tự bị hợp lại sau khi nhị phân hoá | Sử dụng ảnh nguồn có độ phân giải cao hơn hoặc áp dụng một chút Gaussian blur trước khi ngưỡng. |
| **Nhiều ngôn ngữ** | Các chữ Cyrillic trở nên không đọc được | Đặt `engine.setLanguage([Language.Cyrillic, Language.English])` nếu thư viện hỗ trợ chế độ đa ngôn ngữ. |
| **Định dạng ảnh không được hỗ trợ** | `apply()` gây ra lỗi | Chuyển đổi ảnh sang PNG hoặc JPEG trước bằng Pillow (`Image.open().convert('RGB')`). |

## Mở rộng cách tiếp cận **Image Preprocessing Pipeline Python**

1. **Batch Processing** – Lặp qua một thư mục ảnh, lưu mỗi kết quả vào file CSV.  
2. **Parallel Execution** – Sử dụng `concurrent.futures.ThreadPoolExecutor` để tăng tốc các công việc lớn.  
3. **Custom Filters** – Thêm các phép biến đổi hình thái (`erode`, `dilate`) cho các mẫu in.  
4. **Cloud OCR Integration** – Thay thế `OcrEngine` bằng một client API (Google Vision, Azure Computer Vision) trong khi vẫn giữ các bước tiền xử lý giống nhau.

```python
# Example of batch processing with ThreadPoolExecutor
from concurrent.futures import ThreadPoolExecutor, as_completed

def batch_extract(folder: str):
    files = [os.path.join(folder, f) for f in os.listdir(folder) if f.lower().endswith('.jpg')]
    results = {}

    with ThreadPoolExecutor(max_workers=4) as executor:
        future_to_file = {executor.submit(extract_cyrillic_text, f): f for f in files}
        for future in as_completed(future_to_file):
            file_path = future_to_file[future]
            try:
                results[file_path] = future.result()
            except Exception as exc:
                results[file_path] = f"Error: {exc}"
    return results
```

## Tóm tắt bằng hình ảnh

![ví dụ tiền xử lý ảnh cho OCR](/images/ocr_preprocess_example.png "Sơ đồ mô tả pipeline tiền xử lý ảnh cho OCR: deskew → binarize → denoise → OCR engine")

*Sơ đồ minh họa mỗi giai đoạn của quy trình **preprocess image for OCR**, từ bản quét thô đến đầu ra văn bản cuối cùng.*

---

## Kết luận

Chúng ta đã đi qua một giải pháp **preprocess image for OCR** hoàn chỉnh bằng Python, bao gồm mọi thứ từ cài đặt các package phù hợp đến xây dựng một **image preprocessing pipeline python** mạnh mẽ và cuối cùng **trích xuất văn bản từ ảnh Cyrillic**. Bằng cách áp dụng chỉnh nghiêng, nhị phân hoá và giảm nhiễu trước khi đưa ảnh vào engine OCR, bạn sẽ thấy sự cải thiện đáng kể trong **cách cải thiện độ chính xác OCR**, đặc biệt với các script Cyrillic khó khăn.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thay đổi mô hình ngôn ngữ sang Arabic, thử nghiệm ngưỡng thích ứng, hoặc kết nối pipeline vào một API Flask để xử lý tài liệu thời gian thực. Không gì là không thể, và với nền tảng này bạn đã sẵn sàng biến các bản quét lộn xộn thành văn bản sạch, có thể tìm kiếm.

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn trong suốt!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, dựa trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên đều có ví dụ mã hoàn chỉnh, hoạt động, kèm theo giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất văn bản từ ảnh bằng Aspose OCR – Hướng dẫn từng bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tính góc nghiêng cho tiền xử lý ảnh OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Cách đặt giá trị ngưỡng trong nhận dạng ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}