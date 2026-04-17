---
category: general
date: 2026-03-26
description: Học cách chạy OCR trên các ảnh PNG tiếng Ả Rập và trích xuất văn bản
  tiếng Ả Rập nhanh chóng. Hướng dẫn này trình bày cách chuyển đổi hình ảnh thành
  văn bản với mã Python từng bước.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: vi
og_description: Cách chạy OCR trên các hình PNG tiếng Ả Rập? Hãy theo dõi hướng dẫn
  đầy đủ này để trích xuất văn bản tiếng Ả Rập, nhận dạng văn bản tiếng Ả Rập và chuyển
  đổi hình ảnh thành văn bản bằng Python.
og_title: Cách thực hiện OCR trên PNG tiếng Ả Rập – Trích xuất văn bản từ hình ảnh
tags:
- OCR
- Python
- Arabic
title: Cách thực hiện OCR trên PNG tiếng Ả Rập – Trích xuất văn bản từ hình ảnh
url: /vi/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Chạy OCR trên PNG Tiếng Ả Rập – Trích Xuất Văn Bản Từ Hình Ảnh

Bạn đã bao giờ tự hỏi **cách chạy OCR** trên một hình ảnh chứa chữ viết tiếng Ả Rập chưa? Có thể bạn có một biên lai đã quét, một bản thảo lịch sử, hoặc chỉ đơn giản là một ảnh chụp màn hình của một bài đăng trên mạng xã hội và bạn cần văn bản ở định dạng có thể tìm kiếm. Bạn không đơn độc—các nhà phát triển trên toàn thế giới đều gặp khó khăn này khi làm việc với các ngôn ngữ viết từ phải sang trái.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **cách chạy OCR** trên một file PNG, trích xuất văn bản tiếng Ả Rập và in kết quả ra console. Không có những liên kết mơ hồ “xem tài liệu”; chỉ có mã bạn có thể sao chép‑dán, cùng với giải thích tại sao mỗi dòng lại quan trọng. Khi kết thúc, bạn sẽ có thể **chuyển đổi hình ảnh thành văn bản** một cách đáng tin cậy, ngay cả khi nguồn là một PNG tiếng Ả Rập khó xử lý.

> **Bạn sẽ học được**
> - Cài đặt một Python OCR engine cho tiếng Ả Rập  
> - Tải một ảnh PNG và xử lý các vấn đề thường gặp  
> - Nhận dạng văn bản tiếng Ả Rập và xác minh kết quả  
> - Mẹo để **trích xuất văn bản tiếng Ả Rập** từ các chất lượng ảnh khác nhau  

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã cài đặt Python 3.8+ và một phiên bản mới của thư viện `ocr` (thư viện được dùng trong đoạn mã). Nếu bạn đang dùng môi trường ảo, hãy kích hoạt nó ngay—điều này giúp quản lý các phụ thuộc gọn gàng.

## Prerequisites

- Python 3.8 hoặc mới hơn  
- Gói `ocr` (`pip install ocr‑engine` – thay bằng tên gói thực tế)  
- Một ảnh PNG tiếng Ả Rập (`arabic_doc.png`) được đặt ở vị trí bạn có thể tham chiếu  
- Kiến thức cơ bản về hàm và lớp trong Python  

Đó là tất cả. Không cần framework nặng, không cần Docker container—chỉ cần Python thuần.

## Step 1: Install and Import the OCR Library

Đầu tiên, chúng ta cần chính engine OCR. Thư viện chúng ta sẽ dùng cung cấp một lớp `OcrEngine` với API đơn giản.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Tại sao lại import `Imaging` riêng?* Submodule `Imaging` cung cấp phương thức `Image.load` tiện lợi, hiểu ngay các định dạng PNG, JPEG và TIFF. Bỏ qua bước này sẽ buộc bạn phải tự xử lý raw bytes, điều không cần thiết cho hầu hết các trường hợp sử dụng.

## Step 2: Create the OCR Engine Instance

Bây giờ chúng ta tạo một instance của engine. Hãy nghĩ đối tượng này như “bộ não” sẽ xử lý ảnh.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** Nếu bạn dự định xử lý nhiều ảnh liên tiếp, hãy tái sử dụng cùng một instance `ocr_engine`. Nó sẽ cache các mô hình ngôn ngữ, giúp tăng tốc các lần nhận dạng tiếp theo.

## Step 3: Set the Language to Arabic

Tiếng Ả Rập không phải là Latin; nó có bộ ký tự riêng, hướng viết từ phải sang trái và cách hình thành ký tự ngữ cảnh. Vì vậy chúng ta phải chỉ định rõ cho engine mô hình ngôn ngữ nào sẽ được tải.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Nếu bạn quên dòng này, engine sẽ mặc định tiếng Anh và bạn sẽ nhận được kết quả rối loạn—điều tôi đã thấy xảy ra quá thường xuyên.

## Step 4: Load Your PNG Image

Đây là nơi phần **chuyển đổi hình ảnh thành văn bản** thực sự bắt đầu. Chúng ta sẽ tải file PNG chứa chữ viết tiếng Ả Rập.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Common Edge Cases

| Issue | Symptom | Fix |
|-------|---------|-----|
| Hình ảnh quá tối | Kết quả chứa nhiều khoảng trống | Tiền xử lý bằng Pillow (`ImageEnhance.Brightness`) |
| PNG có kênh alpha | Một số engine OCR đọc sai các pixel trong suốt | Chuyển sang RGB (`image.convert("RGB")`) trước khi tải |
| Văn bản bị xoay | Văn bản nhận dạng bị lộn ngược | Xoay hình ảnh (`image.rotate(90, expand=True)`) trước khi đưa vào engine |

## Step 5: Run the Recognition Process

Với mọi thứ đã sẵn sàng, cuối cùng chúng ta yêu cầu engine thực hiện công việc.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

Phương thức `recognize` trả về một đối tượng chứa chuỗi Unicode thô, điểm tin cậy và các bounding box. Đối với hầu hết các nhà phát triển, văn bản thuần là những gì bạn cần.

## Step 6: Output the Recognized Arabic Text

Bây giờ chúng ta in kết quả. Trong một ứng dụng thực tế, bạn có thể ghi vào file, cơ sở dữ liệu, hoặc đưa vào một API dịch.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Khi chạy script, bạn sẽ thấy các ký tự tiếng Ả Rập hiển thị trong console (đảm bảo terminal của bạn hỗ trợ Unicode). Nếu bạn thấy dấu hỏi hoặc chuỗi rỗng, hãy kiểm tra lại cài đặt ngôn ngữ và chất lượng ảnh.

### Expected Output

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Nếu đầu ra trông giống như dòng trên, chúc mừng—bạn đã **trích xuất văn bản tiếng Ả Rập** thành công từ một PNG!

## Full Working Example

Dưới đây là toàn bộ script, sẵn sàng để sao chép‑dán. Thay `YOUR_DIRECTORY/arabic_doc.png` bằng đường dẫn tới file của bạn.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Chạy nó với `python run_ocr.py` (hoặc tên file bạn đặt). Nếu mọi thứ đã được cài đặt đúng, bạn sẽ thấy câu tiếng Ả Rập được in ra console.

## How to Run OCR on Different Image Formats

Cùng một đoạn mã này cũng hoạt động với JPEG, TIFF hoặc BMP—chỉ cần thay đổi phần mở rộng file. Phương thức `Image.load` tự động phát hiện định dạng, vì vậy bạn có thể **chuyển đổi hình ảnh thành văn bản** mà không cần thêm mã nào.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Nhớ rằng, chất lượng của ảnh nguồn ảnh hưởng mạnh đến độ chính xác của bước **nhận dạng văn bản tiếng Ả Rập**. Ảnh độ phân giải cao, nén thấp sẽ cho kết quả tốt nhất.

## Extract Text from PNG: Tips for Better Accuracy

1. **DPI Matters** – Nhắm tới ít nhất 300 dpi. DPI thấp thường dẫn đến việc bỏ sót ký tự.  
2. **Contrast is King** – Sử dụng công cụ xử lý ảnh (ví dụ OpenCV) để tăng độ tương phản trước khi đưa ảnh vào OCR engine.  
3. **Noise Removal** – Các điểm nhiễu nhỏ có thể làm rối mô hình; lọc trung vị giúp cải thiện.  

Dưới đây là một đoạn mã nhanh dùng Pillow để cải thiện PNG trước khi OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Frequently Asked Questions

**Q: Điều này có hoạt động với các ngôn ngữ viết từ phải sang trái khác tiếng Ả Rập không?**  
A: Chắc chắn. Chỉ cần thay đổi mã ngôn ngữ (`"ar"` → `"he"` cho Hebrew, `"fa"` cho Persian) và engine sẽ tải mô hình phù hợp.

**Q: Nếu tôi cần trích xuất văn bản từ nhiều PNG trong một thư mục thì sao?**  
A: Duyệt qua các file, tái sử dụng cùng một instance `ocr_engine`, và lưu kết quả vào danh sách hoặc ghi mỗi file ra một `.txt` riêng.

**Q: Tôi có thể lấy điểm tin cậy cho mỗi từ không?**  
A: Có. `ocr_result` thường cung cấp phương thức `get_confidences()`. Ghép mỗi điểm tin cậy với từ tương ứng để kiểm soát chất lượng.

## Next Steps

Bây giờ bạn đã biết **cách chạy OCR** trên PNG tiếng Ả Rập, hãy cân nhắc các ý tưởng tiếp theo:

- **Xử lý batch:** Kết hợp script với `os.listdir` để **trích xuất văn bản tiếng Ả Rập** từ toàn bộ thư mục.  
- **Post‑processing:** Sử dụng các thư viện `arabic_reshaper` và `python-bidi` để hiển thị đúng hướng từ phải sang trái trong PDF.  
- **Tích hợp:** Đưa văn bản đã trích xuất vào một chỉ mục tìm kiếm (ví dụ Elasticsearch) để làm cho tài liệu đã quét có thể tìm kiếm được.  

Mỗi chủ đề này dựa trên những nền tảng đã được trình bày ở trên, và sẽ giúp bạn biến một script **chuyển đổi hình ảnh thành văn bản** đơn giản thành một pipeline sẵn sàng cho sản xuất.

---

![cách chạy OCR trên PNG tiếng Ả Rập](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}