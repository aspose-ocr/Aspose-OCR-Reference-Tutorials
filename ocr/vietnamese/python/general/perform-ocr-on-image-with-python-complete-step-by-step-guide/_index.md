---
category: general
date: 2026-07-05
description: Thực hiện OCR trên hình ảnh bằng Python. Học cách chuyển đổi hình ảnh
  thành văn bản bằng Python, tải hình ảnh cho OCR và trích xuất văn bản Cyrillic từ
  hình ảnh trong vài phút.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: vi
og_description: Thực hiện OCR trên hình ảnh bằng Python. Hướng dẫn này cho bạn cách
  chuyển đổi hình ảnh thành văn bản bằng Python, tải hình ảnh cho OCR và nhanh chóng
  trích xuất văn bản Cyrillic từ hình ảnh.
og_title: Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn chi tiết từng bước
url: /vi/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh bằng Python – Hướng dẫn chi tiết từng bước

Bạn đã bao giờ tự hỏi làm thế nào để **perform OCR on image** các tệp mà không phải chuyển chúng cho dịch vụ bên thứ ba? Bạn không phải là người duy nhất. Trong nhiều dự án—máy quét hộ chiếu, công cụ số hóa biên lai, hoặc phần mềm lưu trữ—việc lấy văn bản thô từ một bức ảnh là rào cản đầu tiên.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực tế mà **converts image to text python** kiểu, cho bạn thấy cách **load image for OCR**, và cuối cùng **extract Cyrillic text from image** bằng thư viện mã nguồn mở `aocr`. Khi kết thúc, bạn sẽ có thể **recognize Cyrillic text** trong bất kỳ bức ảnh nào bạn đưa vào.

> **Bạn sẽ nhận được:** một script sẵn sàng chạy, giải thích rõ ràng từng bước, và các mẹo để xử lý các vấn đề thường gặp (như ảnh mờ hoặc phông chữ không mong đợi). Không có API bên ngoài, chỉ Python thuần.

---

## Yêu cầu trước

- Python 3.8 hoặc mới hơn đã được cài đặt.
- Một terminal hoặc command prompt mà bạn cảm thấy thoải mái.
- Gói `aocr` (có thể cài đặt qua `pip install aocr`).
- Một tệp hình ảnh chứa ký tự Cyrillic (ví dụ: hộ chiếu Nga đã quét).  

Nếu bất kỳ mục nào trong số này nghe lạ, đừng lo lắng—mỗi điểm sẽ được giải thích ngắn gọn khi chúng ta tiến hành.

---

## Bước 1: Thực hiện OCR trên hình ảnh – Cài đặt môi trường

Điều đầu tiên chúng ta cần là một môi trường Python sạch sẽ nơi thư viện OCR được cài đặt. Sử dụng môi trường ảo giúp cô lập các phụ thuộc và ngăn ngừa xung đột phiên bản.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Tại sao?**  
Môi trường riêng biệt đảm bảo rằng gói `aocr` và các binary gốc của nó không gây xung đột với các dự án khác. Nó cũng làm cho việc tái tạo trở nên dễ dàng—ai đó có thể clone repo của bạn và chạy lệnh `pip install -r requirements.txt` giống nhau.

> **Mẹo chuyên nghiệp:** Đóng băng các phụ thuộc của bạn bằng `pip freeze > requirements.txt` để luôn biết chính xác phiên bản nào đã được sử dụng.

---

## Bước 2: Tải hình ảnh cho OCR – Nhập và chuẩn bị tệp

Bây giờ thư viện đã sẵn sàng, chúng ta cần **load image for OCR**. Phương thức `aocr.Image.from_file` xử lý hầu hết các định dạng phổ biến (PNG, JPEG, TIFF). Đây là cách thực hiện:

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Điều gì đang xảy ra ở đây?**  
`aocr.Image.from_file` đọc dữ liệu nhị phân, giải mã và lưu vào một đối tượng mà engine OCR có thể hiểu. Nếu không tìm thấy tệp, Python sẽ ném ra `FileNotFoundError`, bạn có thể bắt lỗi này sau nếu cần xử lý lỗi một cách mềm mại.

> **Trường hợp đặc biệt:** Một số máy quét xuất ra TIFF đa trang. Trong trường hợp đó, bạn cần tách các trang trước—`aocr` cung cấp `Image.from_tiff_pages()` để thực hiện.

---

## Bước 3: Cấu hình Engine OCR – Buộc nhận dạng Cyrillic

Mặc định, nhiều engine OCR cố gắng đoán ngôn ngữ, điều này có thể dẫn đến kết quả rối cho các script không phải Latin. Để **recognize Cyrillic text** một cách đáng tin cậy, chúng ta đặt ngôn ngữ thành “cyrillic” một cách rõ ràng.

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Tại sao phải buộc ngôn ngữ?**  
Các ký tự Cyrillic có hình dạng tương tự với chữ Latin (ví dụ, “A” vs “А”). Khi báo cho engine biết sẽ gặp Cyrillic, việc nhận dạng sai giảm đáng kể, đặc biệt trên các ảnh quét độ phân giải thấp.

---

## Bước 4: Thực hiện OCR trên hình ảnh – Chạy quá trình nhận dạng

Với hình ảnh đã được tải và engine đã được tinh chỉnh, cuối cùng chúng ta **perform OCR on image**. Phương thức `recognize` trả về một đối tượng `OcrResult` chứa văn bản đã trích xuất và điểm tin cậy.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**`ocr_result` cung cấp gì?**  
- `text`: chuỗi ký tự đã nhận dạng.  
- `confidence`: một số thực (0‑1) chỉ độ chắc chắn tổng thể.  
- `lines`: danh sách các đối tượng dòng nếu bạn cần kiểm soát chi tiết.  

> **Câu hỏi thường gặp:** *Nếu văn bản bị lộn ngược thì sao?*  
> `aocr` có thể tự động xoay ảnh; chỉ cần đặt `ocr_engine.auto_rotate = True` trước khi gọi `recognize`.

---

## Bước 5: Chuyển đổi hình ảnh sang văn bản Python – Xử lý hậu kỳ kết quả

Chuỗi thô có thể chứa khoảng trắng lẻ loi hoặc ký tự ngắt dòng không mong muốn. Để **convert image to text python** kiểu, chúng ta sẽ làm sạch nó bằng vài bước đơn giản:

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Tại sao cần làm điều này?**  
Kết quả đã được làm sạch dễ dàng hơn để đưa vào các pipeline tiếp theo—cho dù bạn lưu vào cơ sở dữ liệu, gửi tới API dịch thuật, hoặc thực hiện tìm kiếm regex cho số hộ chiếu.

---

## Bước 6: Trích xuất văn bản Cyrillic từ hình ảnh – Kết hợp mọi thứ

Hãy gói tất cả vào một hàm duy nhất, có thể tái sử dụng. Điều này làm cho **extract Cyrillic text from image** trở thành một dòng lệnh trong các dự án của bạn.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Kết quả bạn sẽ thấy (ví dụ):**

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Nếu hình ảnh rõ nét và phông chữ phù hợp với mô hình OCR, bạn sẽ nhận được bản sao gần như hoàn hảo.

---

## Khắc phục sự cố & Mẹo

| Vấn đề | Nguyên nhân có thể | Cách khắc phục |
|-------|-------------------|----------------|
| Ký tự bị rối | Cài đặt ngôn ngữ sai | Đảm bảo `ocr_engine.language = "cyrillic"` |
| Kết quả rỗng | Hình ảnh quá tối hoặc độ phân giải thấp | Tiền xử lý bằng `opencv` để tăng độ tương phản |
| Hướng sai | Hình ảnh bị quay 90° | Đặt `ocr_engine.auto_rotate = True` |
| Hiệu năng chậm | Hình ảnh lớn ( >5 MP ) | Thay đổi kích thước với `aocr.Image.resize(width=1024)` trước khi nhận dạng |

![ví dụ thực hiện OCR trên hình ảnh](ocr_example.png "ví dụ thực hiện OCR trên hình ảnh")

*Alt text: “ví dụ thực hiện OCR trên hình ảnh hiển thị mã Python trích xuất văn bản Cyrillic từ ảnh quét hộ chiếu.”*

---

## Kết luận

Chúng ta vừa **performed OCR on image** các tệp bằng Python thuần, đã học cách **load image for OCR**, buộc engine **recognize Cyrillic text**, và cuối cùng **extract Cyrillic text from image** bằng một hàm trợ giúp gọn gàng. Toàn bộ pipeline—từ cài đặt `aocr` đến làm sạch kết quả—chỉ cần vài chục dòng mã và có thể tích hợp vào bất kỳ dự án nào cần **convert image to text python** kiểu.

## Những gì tiếp theo?

- **Xử lý hàng loạt:** Lặp qua một thư mục các ảnh quét và lưu kết quả vào SQLite.
- **Phát hiện ngôn ngữ:** Kết hợp `langdetect` với `aocr` để tự động chuyển đổi giữa Cyrillic và Latin.
- **Tiền xử lý nâng cao:** Sử dụng `opencv` để chỉnh góc, giảm nhiễu, hoặc nhị phân hoá ảnh nhằm tăng độ chính xác.
- **Tích hợp với FastAPI:** Phơi bày hàm `extract_cyrillic_text` dưới dạng endpoint REST cho các ứng dụng web.

Hãy thoải mái thử nghiệm—đổi ngôn ngữ sang “latin” cho hộ chiếu tiếng Anh, hoặc thử một backend OCR khác hoàn toàn. Các khái niệm vẫn giống nhau, và mã đủ linh hoạt để thích nghi.

Chúc lập trình vui vẻ, và hy vọng hình ảnh của bạn luôn dễ đọc!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}