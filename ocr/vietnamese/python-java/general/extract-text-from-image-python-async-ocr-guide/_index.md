---
category: general
date: 2026-01-12
description: Trích xuất văn bản từ hình ảnh bằng Python sử dụng Aspose OCR. Tìm hiểu
  cách chuyển đổi hình ảnh đã quét thành văn bản với mã bất đồng bộ chỉ trong vài
  phút.
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: vi
og_description: Trích xuất văn bản từ hình ảnh Python với Aspose OCR. Hướng dẫn này
  cho thấy cách chuyển đổi hình ảnh đã quét thành văn bản bằng các hàm bất đồng bộ.
og_title: Trích xuất văn bản từ ảnh bằng Python – Hướng dẫn OCR bất đồng bộ
tags:
- python
- ocr
- async
title: Trích xuất văn bản từ hình ảnh bằng Python – Hướng dẫn OCR bất đồng bộ
url: /vi/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh Python – Hướng dẫn OCR bất đồng bộ

Bạn đã bao giờ cần **extract text from image Python** trong các script nhưng gặp khó khăn ở phần OCR chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp trở ngại khi có một tài liệu đã quét và muốn chuyển nó thành văn bản có thể tìm kiếm mà không phải đau đầu.

Trong hướng dẫn này, chúng tôi sẽ hướng dẫn qua một ví dụ hoàn chỉnh, có thể chạy được, cho bạn thấy cách **convert scanned image to text** bằng API bất đồng bộ của Aspose OCR. Khi kết thúc, bạn sẽ có một hàm duy nhất có thể chèn vào bất kỳ dự án nào, và bạn sẽ hiểu tại sao xử lý bất đồng bộ có thể giữ cho ứng dụng của bạn phản hồi nhanh ngay cả khi OCR mất vài giây.

## Yêu cầu trước

- Python 3.8+ đã được cài đặt (các tính năng async yêu cầu ít nhất 3.7)
- Gói `asposeocr` (`pip install asposeocr`) – đây là thư viện chúng tôi sẽ sử dụng
- Tệp hình ảnh đã quét (TIFF, PNG, JPEG – bất kỳ định dạng nào Aspose OCR hỗ trợ)
- Kiến thức cơ bản về `asyncio` (nếu chưa, đừng lo – chúng tôi sẽ giải thích từng bước)

Không cần phụ thuộc hệ thống bổ sung nào; Aspose OCR đã gói mọi thứ bạn cần.

![Diagram showing async OCR flow – extract text from image python](https://example.com/async-ocr-diagram.png "async OCR flow – extract text from image python")

## Bước 1 – Thiết lập hàm trợ giúp bất đồng bộ  

Trọng tâm của giải pháp là một hàm `async` tải hình ảnh, khởi động OCR, và sau đó chờ kết quả. Giữ hàm này bất đồng bộ có nghĩa là bạn có thể chạy các coroutine khác (ví dụ: tải xuống thêm tệp) trong khi engine OCR hoạt động ở nền.

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**Tại sao điều này quan trọng:** Bằng cách trả về một `Future`, Aspose OCR thực hiện công việc nặng trên một pool thread riêng. `await` giải phóng event loop, vì vậy ứng dụng của bạn vẫn phản hồi nhanh. Nếu bạn cần xử lý nhiều hình ảnh đồng thời, bạn có thể lên lịch nhiều lời gọi `async_ocr` bằng `asyncio.gather`.

## Bước 2 – Chạy Coroutine trong Event Loop  

Bây giờ chúng ta đã có hàm trợ giúp, chúng ta cần thực thi nó. `asyncio.run` tạo một event loop mới, chạy coroutine, và tắt mọi thứ một cách sạch sẽ.

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**Mẹo chuyên nghiệp:** Nếu bạn tích hợp điều này vào một ứng dụng async lớn hơn (ví dụ: FastAPI), bạn sẽ gọi `await async_ocr(...)` trực tiếp thay vì `asyncio.run`.

## Bước 3 – Xác minh đầu ra  

Khi bạn chạy script, bạn sẽ thấy một kết quả tương tự như:

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

Nếu đầu ra bị rối, hãy kiểm tra lại rằng:

1. Hình ảnh rõ ràng và không bị nén quá mức.  
2. Bạn đã chọn ngôn ngữ đúng (`ocr.Language.ENGLISH` hoạt động cho hầu hết các văn bản dựa trên Latin).  
3. Đường dẫn tệp đúng và tệp có thể đọc được.

## Bước 4 – Xử lý các trường hợp đặc biệt  

### Nhiều ngôn ngữ  

Nếu bạn cần **convert scanned image to text** bằng ngôn ngữ khác ngoài tiếng Anh, chỉ cần thay đổi thuộc tính ngôn ngữ:

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### Tệp lớn  

Đối với các tệp TIFF rất lớn, hãy cân nhắc thay đổi kích thước hoặc chuyển đổi sang PNG có độ phân giải thấp hơn trước khi đưa vào OCR. Điều này giảm áp lực bộ nhớ và tăng tốc xử lý.

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### Xử lý lỗi  

Bao quanh lời gọi OCR bằng khối `try/except` để bắt các lỗi liên quan đến mạng hoặc giấy phép.

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## Bước 5 – Mở rộng: Xử lý nhiều hình ảnh đồng thời  

Vì hàm này là async, bạn có thể khởi chạy hàng chục công việc OCR cùng lúc:

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

Mẫu này giữ CPU bận rộn trong khi engine OCR hoạt động song song, giảm đáng kể thời gian xử lý tổng cộng.

## Kết luận  

Bây giờ bạn đã có một giải pháp **extract text from image Python** vững chắc, tận dụng API bất đồng bộ của Aspose OCR. Ví dụ hoàn chỉnh cho thấy cách:

1. Khởi tạo engine OCR và chọn ngôn ngữ.  
2. Khởi chạy OCR bất đồng bộ với `process_async`.  
3. Chờ kết quả mà không chặn event loop.  
4. Xử lý các vấn đề thường gặp như tệp lớn và hỗ trợ đa ngôn ngữ.

Bạn có thể tự do điều chỉnh mã cho các pipeline của mình—cho dù bạn đang xây dựng hệ thống quản lý tài liệu, công cụ lập chỉ mục tìm kiếm, hoặc tiện ích dòng lệnh đơn giản. Các bước tiếp theo có thể bao gồm:

- Lưu trữ văn bản đã trích xuất vào cơ sở dữ liệu để tìm kiếm toàn văn.  
- Thêm tạo PDF (ví dụ: sử dụng `PyPDF2`) để tạo PDF có thể tìm kiếm.  
- Tích hợp với framework web như FastAPI để cung cấp dịch vụ OCR dạng RESTful.

Chúc lập trình vui vẻ, và tận hưởng việc biến những hình ảnh đã quét thành văn bản có thể tìm kiếm và chỉnh sửa!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}