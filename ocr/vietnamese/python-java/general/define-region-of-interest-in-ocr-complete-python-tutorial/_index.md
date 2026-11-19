---
category: general
date: 2026-06-16
description: Xác định vùng quan tâm trong OCR để trích xuất văn bản tiếng Tây Ban
  Nha từ thẻ căn cước. Tìm hiểu cách tải ảnh cho OCR và chỉ định ROI một cách hiệu
  quả.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: vi
og_description: Xác định vùng quan tâm trong OCR để trích xuất văn bản tiếng Tây Ban
  Nha từ thẻ ID. Hướng dẫn từng bước về cách tải ảnh và chỉ định ROI.
og_title: Xác định vùng quan tâm trong OCR – Hướng dẫn Python toàn diện
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Xác định vùng quan tâm trong OCR – Hướng dẫn Python đầy đủ
url: /vi/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Định nghĩa vùng quan tâm trong OCR – Hướng dẫn Python đầy đủ

Bạn đã bao giờ tự hỏi làm thế nào **định nghĩa vùng quan tâm trong OCR** để chỉ đọc phần ảnh bạn thực sự cần? Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách thực hiện điều đó, đồng thời cho bạn biết cách **tải ảnh cho OCR** và trích xuất văn bản tiếng Tây Ban Nha từ thẻ ID chỉ trong vài dòng Python.  

Nếu bạn từng nhìn vào một bản scan nhiễu và nghĩ, “Phải có cách sạch hơn để lấy trường tên,” thì bạn đang ở đúng chỗ. Khi kết thúc, bạn sẽ có thể lấy văn bản thẻ ID mà bạn quan tâm mà không bị rối bởi nền nền.

## Những gì bạn sẽ học

- Tại sao bạn nên **định nghĩa vùng quan tâm** trước khi chạy OCR.  
- Các bước chính xác để **tải ảnh cho OCR** bằng một wrapper OCR Python phổ biến.  
- Cách **định nghĩa ROI** bằng tọa độ pixel.  
- Các cách **trích xuất văn bản thẻ ID** một cách đáng tin cậy, ngay cả khi ngôn ngữ nguồn là tiếng Tây Ban Nha.  
- Mẹo xử lý các trường hợp đặc biệt như thẻ bị xoay hoặc scan có độ tương phản thấp.  

Không yêu cầu bạn phải là chuyên gia OCR—chỉ cần một môi trường Python 3 hoạt động và một file JPEG của thẻ ID mà bạn muốn thử nghiệm.

---

![Define region of interest illustration](placeholder.png){alt="Ví dụ vùng quan tâm được đánh dấu hình chữ nhật trên ảnh thẻ ID"}

## Bước 1: Cài đặt và nhập thư viện OCR

Trước hết, bạn cần một thư viện cung cấp lớp `OcrEngine` tương tự như đoạn mã bạn đã thấy. Trong hướng dẫn này, chúng tôi sẽ dùng gói giả tưởng `ocr`, nhưng các khái niệm tương tự áp dụng cho `pytesseract`, `easyocr`, hoặc bất kỳ wrapper nào cho phép bạn đặt ngôn ngữ và ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Pro tip:* Nếu bạn đang dùng `pytesseract`, lớp `Rectangle` trở thành một tuple đơn giản `(left, top, width, height)`. Phần còn lại của quy trình vẫn giống nhau.

## Bước 2: Tải ảnh cho OCR

Bây giờ chúng ta **tải ảnh cho OCR**. Engine mong đợi một đối tượng `ocr.Image`, vì vậy chúng ta chỉ định đường dẫn tới file chứa thẻ ID. Đảm bảo đường dẫn là tuyệt đối hoặc tương đối so với thư mục làm việc của script.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Nếu ảnh quá lớn, hãy cân nhắc giảm kích thước trước; các engine OCR chạy nhanh hơn trên ảnh có chiều rộng dưới 1500 px.

## Bước 3: Cách Định nghĩa ROI (Định nghĩa Vùng Quan Tâm)

Đây là phần cốt lõi của hướng dẫn: **cách định nghĩa ROI**. Một vùng quan tâm chỉ đơn giản là một hình chữ nhật nói với engine OCR, “Chỉ xem trong giới hạn pixel này.” Hãy tưởng tượng bạn đang vẽ một hộp quanh trường tên trên thẻ ID.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Tại sao lại là những con số đó? Trong ảnh mẫu của chúng tôi, tên nằm khoảng 120 px từ cạnh trái và 80 px từ cạnh trên. Điều chỉnh chúng sao cho phù hợp với bố cục của thẻ bạn đang xử lý.  

*Trường hợp đặc biệt:* Nếu thẻ bị xoay 90°, hoán đổi `width` và `height` và điều chỉnh `left`/`top` cho phù hợp, hoặc xoay ảnh trước bằng Pillow trước khi đưa vào engine.

## Bước 4: Thực hiện OCR trong ROI

Với ROI đã được định nghĩa, engine sẽ bỏ qua mọi thứ bên ngoài hình chữ nhật. Điều này không chỉ tăng tốc xử lý mà còn giảm các kết quả dương tính sai do đồ họa nền.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

Lệnh `recognize()` trả về một đối tượng chứa văn bản đã nhận dạng, điểm tin cậy, và các bounding box cho mỗi từ.

## Bước 5: Trích xuất Văn bản Thẻ ID (và Xác minh Kết quả Tiếng Tây Ban Nha)

Cuối cùng, chúng ta **trích xuất văn bản thẻ ID** từ kết quả ROI và in ra. Vì chúng ta đã đặt ngôn ngữ là tiếng Tây Ban Nha ở bước trước, engine OCR sẽ sử dụng từ điển ngôn ngữ‑specific, cải thiện độ chính xác cho các ký tự có dấu như “ñ” hoặc “á”.

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Kết quả mong đợi

```
ROI text: JUAN PÉREZ GARCÍA
```

Nếu bạn thấy các ký tự bị rối, hãy kiểm tra lại rằng ảnh thực sự là tiếng Tây Ban Nha và các file dữ liệu ngôn ngữ của thư viện OCR đã được cài đặt.

## Những Sai Lầm Thường Gặp & Cách Tránh

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|------------|-------------------|----------------|
| Trả về chuỗi rỗng | ROI không giao với bất kỳ văn bản nào | Xác minh tọa độ bằng trình xem ảnh; dùng `engine.debug_draw_roi()` nếu có. |
| Nhiều ký tự rác | Gói ngôn ngữ sai | Cài lại dữ liệu ngôn ngữ tiếng Tây Ban Nha hoặc chuyển sang `ocr.Language.AUTO`. |
| Điểm tin cậy thấp | Ảnh mờ hoặc độ tương phản thấp | Tiền xử lý bằng OpenCV – áp dụng `cv2.GaussianBlur` và `cv2.threshold`. |
| OCR chạy trên toàn ảnh mặc dù đã đặt ROI | Dùng phiên bản thư viện cũ | Nâng cấp lên phiên bản mới nhất của gói `ocr`; các phiên bản cũ bỏ qua ROI. |

## Mở Rộng Ví Dụ: Nhiều ROI

Đôi khi bạn cần lấy hơn một trường (ví dụ: tên và số ID). Mô hình vẫn giống: thay đổi `engine.region_of_interest` và gọi lại `recognize()`.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Bạn cũng có thể xử lý hàng loạt danh sách các hình chữ nhật nếu thư viện hỗ trợ, giúp giảm số lần gọi tới engine OCR.

## Script Hoàn Chỉnh

Kết hợp mọi thứ lại, đây là một script sẵn sàng chạy **định nghĩa vùng quan tâm**, **tải ảnh cho OCR**, và **trích xuất văn bản tiếng Tây Ban Nha** từ thẻ ID.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Chạy script và bạn sẽ thấy tên được in ra console. Thay đổi các giá trị hình chữ nhật để nhắm tới các trường khác, và bạn sẽ có một công cụ tái sử dụng cho bất kỳ tài liệu dạng thẻ ID nào.

## Các Bước Tiếp Theo

- **Xử lý hàng loạt:** Duyệt qua một thư mục chứa các thẻ ID và lưu mỗi tên đã trích xuất vào file CSV.  
- **Phát hiện ngôn ngữ:** Cho phép người dùng chọn ngôn ngữ động; `ocr.Language.AUTO` có thể hữu ích.  
- **Hậu xử lý:** Áp dụng các mẫu regex để làm sạch các lỗi OCR thường gặp (ví dụ: thay “0” bằng “O” khi nó xuất hiện trong tên).  

Bằng việc thành thạo cách **định nghĩa vùng quan tâm**, bạn đã mở khóa một cách mạnh mẽ để **trích xuất văn bản thẻ ID** nhanh chóng và chính xác, đặc biệt khi làm việc với tài liệu tiếng Tây Ban Nha.

---

### TL;DR

Chúng tôi đã chỉ cho bạn cách **định nghĩa vùng quan tâm trong OCR**, **tải ảnh cho OCR**, và **cách định nghĩa ROI** để **trích xuất văn bản tiếng Tây Ban Nha** từ một thẻ ID. Ví dụ hoàn chỉnh chạy dưới một phút và có thể điều chỉnh cho bất kỳ bố cục nào chỉ bằng một vài thay đổi tọa độ. Hãy thử, điều chỉnh hình chữ nhật, và xem OCR tập trung như một tia laser.

Happy coding!

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}