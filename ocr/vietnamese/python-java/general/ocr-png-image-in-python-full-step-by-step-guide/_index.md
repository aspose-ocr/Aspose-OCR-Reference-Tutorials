---
category: general
date: 2026-06-06
description: OCR ảnh PNG bằng Python – học cách trích xuất văn bản từ hình ảnh, chạy
  ví dụ OCR bằng Python và thậm chí dễ dàng đọc văn bản tiếng Hy Lạp cổ.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: vi
og_description: Giải thích OCR ảnh PNG trong Python. Hướng dẫn này chỉ cách trích
  xuất văn bản từ hình ảnh, chạy một ví dụ OCR bằng Python và đọc tiếng Hy Lạp cổ
  một cách dễ dàng.
og_title: OCR ảnh PNG trong Python – Hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR ảnh PNG trong Python – Hướng dẫn chi tiết từng bước
url: /vi/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image trong Python – Hướng Dẫn Chi Tiết Từng Bước

Bạn đã bao giờ tự hỏi làm thế nào để **OCR PNG image** các tệp trực tiếp từ một script Python? Có thể bạn có một thư mục đầy các bản sao quét của các bản thảo cổ và bạn cần **extract text from image** các tệp mà không phải gõ tay mọi thứ. Tin tốt là bạn không cần bằng tiến sĩ về thị giác máy tính—chỉ cần vài dòng code và thư viện phù hợp, và bạn sẽ đọc tiếng Hy Lạp cổ trong vài giây.

Trong hướng dẫn này, chúng ta sẽ đi qua một **python OCR example** nhận dạng văn bản từ một PNG, đặt ngôn ngữ thành Greek polytonic, và in kết quả. Khi kết thúc, bạn sẽ biết chính xác cách **recognize image text**, xử lý các vấn đề thường gặp, và điều chỉnh script cho các ngôn ngữ hoặc định dạng ảnh khác.

## Những Điều Bạn Sẽ Học

- Cài đặt và cấu hình một thư viện OCR cho Python (pytesseract + Tesseract OCR)
- Tạo một thể hiện OCR engine và tải một tệp PNG
- Đặt ngôn ngữ nhận dạng thành Greek polytonic để bạn có thể **read ancient greek**
- Xuất văn bản đã nhận dạng và khắc phục các vấn đề thường gặp
- Mở rộng script để xử lý hàng loạt nhiều PNG hoặc chuyển sang ngôn ngữ khác

### Yêu Cầu Trước

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Cú pháp hiện đại và gợi ý kiểu |
| `pytesseract` package | Lớp bao bọc nhẹ cho engine Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Engine thực tế thực hiện các tác vụ nặng |
| Greek language data (`grc.traineddata`) | Cần thiết để **read ancient greek** chính xác |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Đối tượng cho bản demo **ocr png image** |

Bạn có thể cài đặt phần Python bằng:

```bash
pip install pytesseract Pillow
```

Và trên Ubuntu/macOS bạn sẽ cài đặt engine:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Đừng quên tải dữ liệu đã được đào tạo cho Greek polytonic:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Đường dẫn có thể khác; điều chỉnh `TESSDATA_PREFIX` nếu cần.)*

## OCR PNG Image: Tạo Thể Hiện Engine

Điều đầu tiên chúng ta cần là một đối tượng giao tiếp với Tesseract. Trong `pytesseract` engine được truy cập thông qua các hàm ở mức module, nhưng để rõ ràng chúng ta sẽ bọc nó trong một lớp nhỏ. Điều này phản ánh khái niệm “engine” mà bạn đã thấy trong đoạn mã gốc.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Tại sao lại bọc nó?**  
- Giữ API công cộng giống hệt đoạn mã mẫu, giúp việc di chuyển dễ dàng.  
- Cho phép chúng ta thêm logging hoặc xử lý lỗi sau này mà không ảnh hưởng tới luồng chính.  
- Thể hiện thực hành OOP tốt—điều mà các nhà phát triển cấp cao đánh giá cao.

## Extract Text from Image: Đặt Ngôn Ngữ Thành Greek Polytonic

Bây giờ chúng ta đã có engine, chúng ta cần chỉ định ngôn ngữ mà nó sẽ nhận dạng. Greek polytonic sử dụng dấu phụ mà dữ liệu “greek” tiêu chuẩn không bao gồm, vì vậy chúng ta chỉ định Tesseract tới tệp `grc` đã được đào tạo.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Nếu bạn muốn **extract text from image** các tệp bằng ngôn ngữ khác, chỉ cần thay `"grc"` bằng `"eng"` cho tiếng Anh, `"fra"` cho tiếng Pháp, v.v. Dòng lệnh này hoạt động cho bất kỳ ngôn ngữ nào bạn đã cài đặt.

## Recognize Image Text: Chạy OCR trên PNG

Với ngôn ngữ đã được đặt, chúng ta đưa PNG vào engine. Ví dụ gốc sử dụng đường dẫn cứng; chúng ta sẽ làm cho linh hoạt hơn bằng cách sử dụng các đối tượng `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Mẹo & Trường Hợp Đặc Biệt**

- **File not found** – bọc lời gọi trong `try/except FileNotFoundError` để đưa ra thông báo thân thiện.  
- **Low‑resolution PNG** – cân nhắc tiền xử lý (ví dụ: thay đổi kích thước, nhị phân hoá) bằng Pillow trước khi OCR.  
- **Non‑Greek text** – Tesseract vẫn sẽ cố gắng giải mã, nhưng độ chính xác giảm đáng kể. Luôn luôn khớp ngôn ngữ.

## Xuất Văn Bản Đã Nhận Dạng

Cuối cùng, chúng ta in kết quả. Trong một dự án thực tế, bạn có thể ghi vào cơ sở dữ liệu, file CSV, hoặc thậm chí đưa vào quy trình dịch thuật.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Khi bạn chạy script trên một bản quét rõ ràng của một khắc văn Hy Lạp cổ, bạn sẽ thấy kết quả giống như:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Nếu đầu ra bị rối, hãy kiểm tra lại rằng tệp **greek.traineddata** nằm trong thư mục đúng và PNG không quá nhiễu.

## Ví Dụ Hoàn Chỉnh (Tất Cả Các Bước Trong Một Script)

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Lưu lại với tên `ocr_greek.py` và thực thi `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Expected output** (rút gọn để ngắn gọn):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Nếu bạn thấy các ký tự Hy Lạp đúng, chúc mừng—bạn đã thực hiện thành công một thao tác **ocr png image** trong Python!

## Câu Hỏi Thường Gặp & Mẹo Chuyên Nghiệp

### Làm sao để cải thiện độ chính xác trên PNG nhiễu?

- Chuyển ảnh sang thang xám: `img = img.convert('L')`
- Áp dụng ngưỡng nhị phân: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Mở rộng kích thước với `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Các bước này thường biến một cơn ác mộng **recognize image text** thành kết quả sạch sẽ.

### Tôi có thể xử lý toàn bộ thư mục PNG không?

Chắc chắn. Bọc lời gọi `recognize_image` trong một vòng lặp `for` qua `Path.glob("*.png")`. Lưu mỗi kết quả vào một dictionary hoặc ghi vào CSV để phân tích sau.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Nếu tôi chỉ cần trích xuất số?

Gửi một chuỗi **config** tùy chỉnh tới `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

Bằng cách đó bạn có thể **extract text from image** các tệp chứa bảng, số sê-ri, hoặc dấu thời gian.

### Có cách nào để lấy điểm tin cậy không?

Có—sử dụng `pytesseract.image_to_data` trả về một TSV với độ tin cậy cho mỗi từ. Bạn có thể lọc bỏ các token có độ tin cậy thấp trước khi ghép chuỗi cuối cùng.

## Mở Rộng Hướng Dẫn

Bây giờ bạn đã nắm vững các kiến thức cơ bản, hãy xem xét khám phá các chủ đề liên quan sau:

- **Batch OCR with multiprocessing** – tăng tốc xử lý khối lượng lớn PNG.  
- **Hybrid OCR + NLP pipelines** – tự động dịch tiếng Hy Lạp cổ đã trích xuất sang tiếng Anh hiện đại.  
- **Alternative engines** – thử `easyocr` hoặc các phương pháp dựa trên `opencv` cho các trường hợp sử dụng cụ thể.  
- **Cloud OCR services** – Google Vision, Azure Computer Vision, hoặc AWS Textract cho việc mở rộng không máy chủ.  

Mỗi mục này dựa trên **python ocr example** cốt lõi mà chúng ta vừa đề cập, vì vậy bạn sẽ cảm thấy tự tin khi khám phá sâu hơn.

## Kết Luận

Chúng ta đã lấy một đoạn mã đơn giản và biến nó thành một quy trình **ocr png image** mạnh mẽ trong Python. Bằng cách tạo một `OcrEngine`, đặt ngôn ngữ thành Greek polytonic, đưa PNG vào và in kết quả, bạn giờ đã biết cách **extract text from image** các tệp, **recognize image text**, và thậm chí **read ancient greek**.

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh bằng Aspose OCR – Hướng Dẫn Từng Bước](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Cách Đặt Giá Trị Ngưỡng trong Nhận Diện Hình ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Nhận dạng Văn bản ảnh với Aspose OCR cho Nhiều Ngôn ngữ](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}