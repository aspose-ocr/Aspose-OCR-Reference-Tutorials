---
category: general
date: 2026-07-05
description: Cách chỉnh nghiêng ảnh nhanh chóng. Học cách tiền xử lý ảnh cho OCR,
  sửa góc quay của ảnh và chuyển đổi bản quét thành văn bản bằng Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: vi
og_description: Cách chỉnh nghiêng ảnh và tiền xử lý ảnh cho OCR. Hướng dẫn này chỉ
  ra cách sửa góc quay của ảnh và trích xuất văn bản từ ảnh bằng Python.
og_title: Cách chỉnh nghiêng ảnh – Tiền xử lý OCR từng bước
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Cách chỉnh nghiêng ảnh – Hướng dẫn toàn diện cho tiền xử lý OCR
url: /vi/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Hướng Lại Hình Ảnh – Hướng Dẫn Toàn Diện cho Tiền Xử Lý OCR

Bạn đã bao giờ tự hỏi **cách định hướng lại hình ảnh** khi chúng trông như được quét bằng một máy quét lệch? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, việc đầu tiên bạn phải làm trước khi **trích xuất văn bản từ hình ảnh** là làm thẳng những góc nghiêng đó.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực hành, từ đầu đến cuối, **tiền xử lý hình ảnh cho OCR**, sửa lỗi xoay, và cuối cùng **chuyển đổi bản quét thành văn bản** bằng một thư viện OCR Python. Không có những tham chiếu mơ hồ, chỉ có một script hoạt động mà bạn có thể sao chép‑dán, cùng với các mẹo về những lỗi thường gặp.  

## Những Điều Bạn Sẽ Đạt Được

Khi kết thúc hướng dẫn này, bạn sẽ có thể:

* Tải bất kỳ tệp JPEG hoặc PNG đã quét nào có độ nghiêng nhẹ.  
* Áp dụng bộ lọc định hướng lại và bước nhị phân hoá để tăng độ chính xác của OCR.  
* Chạy engine OCR và **trích xuất văn bản từ hình ảnh** một cách đáng tin cậy.  
* Hiểu vì sao **việc xoay hình ảnh đúng** lại quan trọng đối với quá trình trích xuất văn bản sau này.  

### Yêu Cầu Trước

* Python 3.9+ đã được cài đặt trên máy của bạn.  
* Một gói OCR có thể cài đặt qua pip và mô phỏng không gian tên `ocr` được dùng trong ví dụ (ví dụ: một wrapper nhẹ quanh Tesseract).  
* Kiến thức cơ bản về hàm Python và các khái niệm xử lý ảnh.  

Nếu bạn đã có những thứ trên, hãy bắt đầu.

![how to deskew image example](deskew_before_after.png){alt="cách định hướng lại hình ảnh – trước và sau khi chỉnh sửa"}

## Bước 1: Cài Đặt Engine OCR – Cách Định Hướng Lại Hình Ảnh Bằng Python

Điều đầu tiên cần làm: bạn cần một engine OCR có thể hiểu ngôn ngữ của tài liệu. Đoạn mã dưới đây cho thấy cách khởi tạo boilerplate tối thiểu để tạo engine và thông báo rằng bạn đang làm việc với văn bản tiếng Anh.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Tại sao điều này quan trọng:* Cài đặt ngôn ngữ của engine ảnh hưởng đến bộ ký tự và từ điển mà nó sử dụng. Bỏ qua bước này có thể khiến OCR hiểu sai các từ thông dụng, đặc biệt sau khi bạn **sửa lỗi xoay hình ảnh**.

## Bước 2: Tải Hình Ảnh Đã Quét Muốn Định Hướng Lại

Bây giờ chúng ta đưa tệp vào bộ nhớ. Thay `"YOUR_DIRECTORY/skewed_scan.jpg"` bằng đường dẫn tới hình ảnh của bạn.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

Nếu hình ảnh đã ở dạng mảng NumPy hoặc `Mat` của OpenCV, bạn có thể điều chỉnh loader cho phù hợp – điều quan trọng là đối tượng phải cung cấp phương thức `apply_filter` được sử dụng ở bước sau.

## Bước 3: Tiền Xử Lý Hình Ảnh cho OCR – Định Hướng Lại và Nhị Phân Hoá

Đây là nơi phép thuật xảy ra. Chúng ta sẽ xâu chuỗi hai bộ lọc:

1. **Deskew** – tự động phát hiện đường cơ sở văn bản chiếm ưu thế và xoay ảnh trở lại chiều ngang.  
2. **Binarize (Otsu)** – chuyển ảnh thành đen‑trắng thuần túy, giúp cải thiện đáng kể tỷ lệ nhận dạng.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Mẹo chuyên nghiệp:* Nếu bạn nhận thấy văn bản vẫn còn mờ sau khi nhị phân hoá, hãy thử điều chỉnh độ tương phản hoặc dùng phương pháp ngưỡng khác. Module `ocr.Filter` thường có sẵn `adaptive_threshold()` cho các trường hợp khó hơn.

## Bước 4: Chạy OCR – Trích Xuất Văn Bản Từ Hình Ảnh

Với một canvas sạch sẽ, thẳng hàng, chúng ta đưa ảnh cho engine. Đối tượng kết quả chứa chuỗi đã nhận dạng, điểm tin cậy, và thậm chí các bounding box nếu bạn cần dùng sau này.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Kết quả điển hình trông như sau:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Bạn có thấy các ngắt dòng khớp hoàn hảo không? Đó là lợi ích của **việc xoay hình ảnh đúng** – OCR không còn phải đoán hướng dòng nữa.

## Bước 5: Kết Hợp Tất Cả – Script Một File Để Chuyển Đổi Bản Quét Thành Văn Bản

Dưới đây là script đầy đủ, có thể chạy ngay, kết hợp mọi phần chúng ta đã thảo luận. Lưu lại dưới tên `deskew_ocr.py` và thực thi `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Tại Sao Cách Này Hoạt Động

* **Deskew trước** – xoay ảnh trước khi nhị phân hoá giúp thuật toán ngưỡng hoạt động trên một đường chân trời bằng phẳng.  
* **Binarize sau deskew** – phương pháp Otsu giả định một histogram nhị phân; một trang nghiêng sẽ phá vỡ giả định này.  
* **Mô hình ngôn ngữ tiếng Anh** – cho OCR biết những ký tự nào sẽ xuất hiện, giảm thiểu các kết quả sai.  

Nếu bạn cần hỗ trợ các ngôn ngữ khác, chỉ cần thay `ocr.Language.ENGLISH` bằng enum tương ứng.

## Câu Hỏi Thường Gặp & Trường Hợp Cạnh

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu bản quét bị lộn ngược?* | Bộ lọc `deskew()` thường phát hiện cả quay 180° nữa. Nếu không, gọi `apply_filter(ocr.Filter.rotate(180))` trước khi deskew. |
| *Tài liệu của tôi có đồ họa màu – việc nhị phân hoá có xóa chúng không?* | Có. Đối với nội dung hỗn hợp, hãy cân nhắc chỉ dùng `ocr.Filter.deskew()` rồi chạy OCR trên ảnh màu. Bạn vẫn có thể trích xuất văn bản trong khi giữ lại đồ họa. |
| *Tôi có thể xử lý một loạt tệp không?* | Đặt logic vào một vòng lặp, đọc mỗi đường dẫn tệp từ danh sách, và lưu `result.text` của mỗi tệp vào một file `.txt` riêng. |
| *Làm sao cải thiện độ chính xác trên các bản quét độ phân giải thấp?* | Phóng to ảnh bằng bộ lọc bicubic **trước** khi deskew, sau đó áp dụng bộ lọc làm nét. Nhiều pixel hơn giúp engine OCR có thêm thông tin. |

## Bonus: Kiểm Tra Thị Giác Việc Định Hướng Lại

Nếu bạn muốn xem trước‑sau cạnh nhau, thêm một đoạn mã Matplotlib nhanh:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Nhìn thấy sự căn chỉnh đã được sửa có thể rất an tâm, đặc biệt khi bạn đang gỡ lỗi một loạt bản quét khó khăn.

## Kết Luận

Chúng ta đã tìm hiểu **cách định hướng lại hình ảnh**, tại sao **tiền xử lý hình ảnh cho OCR** lại quan trọng, và cách **trích xuất văn bản từ hình ảnh** để cuối cùng **chuyển đổi bản quét thành văn bản**. Quy trình – tải → deskew → binarize → nhận dạng – đảm bảo OCR nhận được một trang sạch, thẳng, từ đó tăng độ chính xác và giảm thiểu các chỉnh sửa thủ công.

Bạn sẽ làm gì tiếp theo trong hành trình OCR? Hãy thử:

* Các gói ngôn ngữ khác (`ocr.Language.FRENCH`, v.v.).  
* Thêm bước phân tích bố cục để phát hiện cột hoặc bảng.  
* Xuất kết quả OCR ra PDF có thể tìm kiếm bằng một thư viện PDF.

Đừng ngại để lại bình luận nếu gặp khó khăn, hoặc chia sẻ các tùy chỉnh của bạn cho những bản quét đặc biệt cứng đầu. Chúc lập trình vui vẻ, và mong hình ảnh của bạn luôn thẳng hàng!

## Bạn Nên Học Gì Tiếp Theo?


Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ, cùng các giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}