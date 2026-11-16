---
category: general
date: 2026-03-18
description: Chạy OCR trên hình ảnh nhanh chóng với Python. Tìm hiểu cách nhận dạng
  văn bản từ PNG, tải hình ảnh cho OCR và trích xuất từ ngữ từ hình ảnh trong hướng
  dẫn từng bước.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: vi
og_description: Chạy OCR trên hình ảnh bằng Python. Hướng dẫn này cho thấy cách nhận
  dạng văn bản từ PNG, tải hình ảnh cho OCR và trích xuất từ ngữ từ hình ảnh với một
  ví dụ mã đầy đủ.
og_title: Chạy OCR trên hình ảnh – Hướng dẫn Python
tags:
- OCR
- Python
- Image Processing
title: Chạy OCR trên hình ảnh – Ví dụ hoàn chỉnh OCR bằng Python
url: /vi/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên Hình ảnh – Ví dụ Python OCR Hoàn chỉnh

Bạn đã bao giờ cần **chạy OCR trên các tệp hình ảnh** nhưng không biết bắt đầu từ đâu? Bạn không cô đơn; nhiều nhà phát triển gặp khó khăn này khi lần đầu tiên xử lý việc trích xuất văn bản từ tài liệu đã quét. Trong hướng dẫn này, chúng ta sẽ đi qua một **ví dụ Python OCR** cho phép bạn **nhận dạng văn bản từ PNG**, **tải hình ảnh cho OCR**, và **trích xuất các từ từ hình ảnh** kèm theo điểm tin cậy—tất cả chỉ trong vài dòng code.

Chúng ta sẽ bao phủ mọi thứ bạn cần: thư viện yêu cầu, cách thiết lập engine, lý do mỗi bước quan trọng, và kết quả đầu ra trông như thế nào. Khi kết thúc, bạn sẽ có thể chèn đoạn mã này vào dự án của mình và bắt đầu lấy văn bản từ bất kỳ hình ảnh nào ngay lập tức. Không có phần thừa, chỉ có giải pháp thực tế, có thể chạy ngay.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- Python 3.8 hoặc mới hơn được cài đặt  
- Gói `ocrengine` (hoặc bất kỳ thư viện nào cung cấp lớp `OcrEngine`). Bạn có thể cài đặt bằng `pip install ocrengine` – điều chỉnh tên nếu bạn đang dùng thư viện OCR khác như `pytesseract`.  
- Một tệp hình ảnh (PNG, JPG, v.v.) mà bạn muốn xử lý – trong hướng dẫn này chúng ta sẽ dùng `invoice.png`.  

Đó là tất cả. Không có phụ thuộc nặng, không có dịch vụ bên ngoài, chỉ thuần Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: ví dụ chạy OCR trên hình ảnh – hoá đơn đã quét đang được xử lý*

## Bước 1 – Cài đặt và Import Thư viện OCR

Đầu tiên, hãy đưa engine OCR vào môi trường và import nó. Nếu bạn đang dùng gói giả định `ocrengine`, cách import sẽ như sau:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Tại sao lại quan trọng:** Import lớp đúng sẽ cho phép bạn truy cập các phương thức chúng ta sẽ gọi sau này, như `setImageFromFile` và `recognize`. Nếu bỏ qua bước này, Python sẽ ném ra `ModuleNotFoundError`, và bạn sẽ bị kẹt trước khi thậm chí tải hình ảnh.

## Bước 2 – Tạo một Instance của OCR Engine

Bây giờ thư viện đã sẵn sàng, chúng ta cần một đối tượng engine sẽ giữ cấu hình và trạng thái cho quá trình nhận dạng.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* Một số engine OCR cho phép bạn tinh chỉnh mô hình ngôn ngữ hoặc cài đặt DPI ở bước này. Đối với một **python OCR example** cơ bản, các giá trị mặc định hoạt động tốt, nhưng nếu bạn đang xử lý các bản quét độ phân giải thấp, hãy cân nhắc điều chỉnh chúng ở đây.

## Bước 3 – Tải Hình ảnh Bạn Muốn Xử lý

Bước hợp lý tiếp theo là **tải hình ảnh cho OCR**. Bạn chỉ định đường dẫn tệp PNG (hoặc bất kỳ định dạng hỗ trợ nào) mà bạn muốn phân tích.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Điều gì đang diễn ra phía sau?** Engine đọc dữ liệu pixel, chuyển đổi chúng thành định dạng mà thuật toán nhận dạng có thể hiểu, và lưu trữ nội bộ. Nếu đường dẫn tệp sai, bạn sẽ nhận được `FileNotFoundError`, vì vậy hãy kiểm tra kỹ xem hình ảnh có tồn tại không.

## Bước 4 – Chạy Thuật toán Nhận dạng

Với hình ảnh đã được tải, chúng ta cuối cùng **chạy OCR trên hình ảnh** để trích xuất nội dung văn bản.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

Tại thời điểm này, engine quét bitmap, áp dụng so khớp mẫu, và trả về một đối tượng chứa mọi từ, dòng và chỉ số tin cậy đã được phát hiện.

## Bước 5 – Duyệt Các Từ Được Nhận dạng và Hiển thị Độ Tin Cậy

Phần hữu ích nhất của bất kỳ quy trình OCR nào là xem **độ tin cậy** cho mỗi token đã trích xuất. Nó cho biết engine chắc chắn đến mức nào về mỗi từ, giúp bạn lọc bỏ các kết quả có độ tin cậy thấp nếu cần.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Kết quả mong đợi** (ví dụ):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Bây giờ bạn có thể thấy chính xác **những từ nào đã được trích xuất từ hình ảnh** và mức độ tin cậy của mỗi phát hiện. Đây là cốt lõi của bất kỳ **pipeline extract words from image** nào.

## Xử lý các Trường hợp Đặc biệt Thường Gặp

### Nếu Hình ảnh Là Đen‑trắng?

Một số engine OCR hoạt động tốt hơn với hình ảnh màu. Nếu bạn nhận thấy độ tin cậy thấp trên toàn bộ, hãy thử chuyển PNG sang phiên bản đen‑trắng có độ tương phản cao hơn trước khi đưa vào engine. Pillow có thể giúp:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Xử lý Nhiều Ngôn ngữ

Nếu tài liệu của bạn chứa cả tiếng Anh và tiếng Tây Ban Nha, bạn sẽ muốn **nhận dạng văn bản từ PNG** bằng mô hình đa ngôn ngữ. Hầu hết các engine cho phép bạn đặt danh sách ngôn ngữ khi khởi tạo:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Lọc Các Từ Có Độ Tin Cậy Thấp

Đôi khi bạn chỉ cần các từ có độ tin cậy trên, ví dụ, 90 %. Một bộ lọc nhanh như sau:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Kịch bản Đầy đủ, Sẵn sàng Chạy

Kết hợp mọi thứ lại, đây là một script đơn lẻ bạn có thể sao chép‑dán và chạy ngay (chỉ cần thay đổi đường dẫn tới PNG của bạn).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Chạy nó bằng:

```bash
python run_ocr_on_image.py
```

Bạn sẽ thấy danh sách các từ và phần trăm độ tin cậy được in ra console, giống như đã trình bày ở trên.

## Câu hỏi Thường gặp

**Điều này có hoạt động với tệp JPG hoặc TIFF không?**  
Chắc chắn. Phương thức `setImageFromFile` chấp nhận bất kỳ định dạng nào mà thư viện nền có thể giải mã, vì vậy bạn có thể **chạy OCR trên các tệp hình ảnh** loại JPG, TIFF, BMP, v.v.

**Tôi có thể xử lý nhiều hình ảnh trong một vòng lặp không?**  
Có thể. Đặt các bước tải và nhận dạng bên trong một vòng `for` qua danh sách các đường dẫn tệp. Chỉ cần nhớ khởi tạo lại engine nếu thư viện yêu cầu một instance mới cho mỗi hình ảnh.

**Nếu tôi cần văn bản dưới dạng một chuỗi duy nhất thay vì từng từ?**  
Hầu hết các đối tượng kết quả OCR cung cấp phương thức `getText()` trả về toàn bộ tài liệu. Ví dụ:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Các Bước Tiếp Theo và Chủ Đề Liên Quan

Bây giờ bạn đã biết cách **chạy OCR trên hình ảnh**, hãy xem xét khám phá:

- **Xử lý hậu kỳ**: Sử dụng biểu thức chính quy để làm sạch ngày tháng, số tiền, hoặc ID được trích xuất từ hoá đơn.  
- **Xử lý hàng loạt**: Kết hợp script với `os.listdir()` để xử lý toàn bộ thư mục tài liệu đã quét.  
- **Thư viện thay thế**: `pytesseract` là một lựa chọn mã nguồn mở phổ biến; quy trình làm việc tương tự—chỉ cần thay thế các lời gọi engine.  
- **Xuất kết quả**: Ghi các từ đã trích xuất và điểm tin cậy vào CSV để phân tích tiếp theo.

Mỗi phần mở rộng này dựa trực tiếp trên nền tảng chúng ta đã xây dựng, giúp bạn biến dữ liệu OCR thô thành thông tin có thể hành động.

---

### TL;DR

Chúng tôi đã trình bày một **python OCR example** ngắn gọn, thể hiện cách **tải hình ảnh cho OCR**, **chạy OCR trên hình ảnh**, và **trích xuất các từ từ hình ảnh** đồng thời báo cáo độ tin cậy. Toàn bộ script đã sẵn sàng chạy, và bạn hiện đã có kiến thức để tùy chỉnh nó cho bất kỳ dự án nào cần **nhận dạng văn bản từ PNG** (hoặc các định dạng khác). Hãy thử, điều chỉnh ngưỡng tin cậy, và xem ứng dụng của bạn trở nên nhận thức được văn bản trong vài phút. Chúc lập trình vui!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}