---
category: general
date: 2026-03-18
description: Tạo PDF có thể tìm kiếm từ các tệp đã quét của bạn bằng Aspose OCR. Tìm
  hiểu cách chuyển đổi PDF đã quét, trích xuất văn bản từ PDF và nhận dạng văn bản
  PDF nhanh chóng.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm ngay lập tức. Hãy làm theo hướng dẫn này để
  chuyển đổi PDF đã quét, trích xuất văn bản từ PDF và nhận dạng văn bản PDF bằng
  Aspose OCR.
og_title: Tạo PDF có thể tìm kiếm – Hướng dẫn từng bước với Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Tạo PDF có thể tìm kiếm – Chuyển đổi PDF đã quét bằng Aspose OCR
url: /vi/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm – Hướng dẫn từng bước  

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một đống các trang đã quét nhưng không biết bắt đầu từ đâu chưa? Bạn không đơn độc—hầu hết các nhà phát triển đều gặp khó khăn này khi lần quét đầu tiên được tải lên máy chủ.  

Tin tốt là với Aspose OCR, bạn có thể **chuyển đổi pdf đã quét** chỉ trong vài dòng mã, **trích xuất văn bản từ pdf** để xác thực, và thậm chí **nhận dạng văn bản pdf** ngay lập tức. Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình, từ cài đặt thư viện đến lưu tài liệu có thể tìm kiếm hoàn chỉnh, và kèm một vài mẹo để xử lý các trường hợp **chuyển đổi pdf ảnh** khó khăn.

## Những gì bạn sẽ đạt được  

Khi hoàn thành hướng dẫn này, bạn sẽ có thể:

* Tải một PDF đã quét (hoặc PDF chỉ chứa hình ảnh) vào Aspose OCR.  
* Chỉ định cho engine những trang nào cần xử lý – hữu ích khi bạn chỉ cần một phần của tài liệu.  
* Nhúng kết quả OCR trở lại file gốc để đầu ra là một **PDF có thể tìm kiếm** thực thụ.  
* Xác minh hoạt động bằng cách in số lượng trang và, nếu muốn, xuất văn bản đã trích xuất.  

Không có dịch vụ bên ngoài, không có phép màu ẩn—chỉ Python thuần và API của Aspose.

## Yêu cầu trước  

* Python 3.8 hoặc mới hơn.  
* Gói `aspose-ocr` – cài đặt bằng `pip install aspose-ocr`.  
* Một file PDF đã quét (hoặc PDF chỉ chứa hình ảnh).  
* Kiến thức cơ bản về lập trình Python.  

Nếu bạn đã có những thứ trên, tuyệt vời—cùng bắt đầu.

<img src="searchable-pdf-workflow.png" alt="Create searchable PDF workflow">  

*(Minh hoạ quy trình OCR – không bắt buộc cho mã nhưng giúp người học trực quan.)*

## Bước 1 – Khởi tạo OCR Engine  

Điều đầu tiên cần làm: bạn cần một thể hiện `OcrEngine`. Hãy nghĩ nó như bộ não sẽ đọc từng pixel và chuyển chúng thành ký tự Unicode.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Tại sao điều này quan trọng:** Không có engine, bạn không thể thiết lập tùy chọn hay chạy nhận dạng. Khởi tạo sớm cũng cho phép bạn gắn bất kỳ từ điển tùy chỉnh nào sau này.

## Bước 2 – Tải PDF nguồn của bạn  

Aspose OCR có thể đọc PDF trực tiếp, nghĩa là bạn không cần raster hoá từng trang thủ công. Chỉ cần chỉ đường cho engine tới file.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Mẹo chuyên nghiệp:* Nếu PDF rất lớn, hãy cân nhắc tải nó từ một stream để tránh khóa file trên đĩa.

## Bước 3 – Cấu hình tùy chọn nhận dạng PDF  

Đây là nơi các từ khóa phụ bắt đầu tỏa sáng. Bạn có thể yêu cầu engine **chuyển đổi pdf đã quét** chỉ trên một số trang nhất định, nhúng văn bản đã nhận dạng, hoặc thậm chí giữ nguyên hình ảnh gốc.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Tại sao điều này quan trọng:**  
* `setEmbedRecognisedText(True)` là chìa khóa để biến một PDF raster thành **PDF có thể tìm kiếm**.  
* `setPageRange` giúp bạn **chuyển đổi pdf ảnh** một cách chọn lọc—hữu ích cho tài liệu lớn mà bạn chỉ cần OCR một vài trang.  
* Bật trích xuất văn bản cho phép bạn sau này **trích xuất văn bản từ pdf** mà không cần mở trình xem.

## Bước 4 – Gắn tùy chọn vào Engine  

Bây giờ gắn các tùy chọn vào engine. Bước này dễ bị bỏ qua, nhưng nếu bỏ qua thì engine sẽ chạy với cài đặt mặc định (không có văn bản có thể tìm kiếm).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Bước 5 – Chạy OCR trên các trang đã chọn  

Khi mọi thứ đã được kết nối, việc nhận dạng thực tế chỉ là một lời gọi phương thức duy nhất.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Nếu bạn đang xử lý một tài liệu đa megabyte, có thể muốn bọc đoạn mã này trong khối try/except để bắt `OcrException` và ghi lại trang gây lỗi.

## Bước 6 – Xác minh kết quả  

Một kiểm tra nhanh là in ra số trang mà engine cho là đã xử lý. Bạn cũng có thể lấy văn bản thô nếu cần **trích xuất văn bản từ pdf** để phân tích sâu hơn.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Tại sao bạn cần quan tâm:** Nhìn thấy số lượng trang xác nhận rằng `setPageRange` đã hoạt động, và đoạn văn bản đã trích xuất chứng minh OCR thực sự nhận dạng được ký tự.

## Bước 7 – Lưu PDF có thể tìm kiếm  

Cuối cùng, ghi kết quả ra đĩa. Hằng số `ImageFormats.PDF` thông báo cho Aspose giữ file ở dạng PDF, nhưng đã được bổ sung văn bản có thể tìm kiếm.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Mở file kết quả bằng bất kỳ trình đọc PDF nào và thử tìm kiếm văn bản—voilà, bạn đã **tạo pdf có thể tìm kiếm**!

## Xử lý các trường hợp khó thường gặp  

### Khi nguồn là PDF *chỉ chứa hình ảnh*  

Nếu PDF đầu vào của bạn chỉ có hình ảnh (không có lớp văn bản), cùng một đoạn mã vẫn hoạt động—chỉ cần đảm bảo `setEmbedRecognisedText(True)` vẫn được bật. Bạn cũng có thể muốn tăng DPI để cải thiện độ chính xác:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Xử lý đa ngôn ngữ  

Aspose OCR hỗ trợ các gói ngôn ngữ. Tải ngôn ngữ trước khi gọi `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Tài liệu lớn  

Xử lý một PDF đã quét 500 trang có thể tốn nhiều bộ nhớ. Hãy chia công việc:

1. Lặp qua các phạm vi trang (`setPageRange(start, end)`).  
2. Lưu mỗi khối thành một PDF có thể tìm kiếm tạm thời.  
3. Gộp các khối lại bằng `PdfMerger` (một thành phần Aspose khác).

## Ví dụ hoàn chỉnh (Tất cả các bước cùng nhau)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Chạy script này sẽ cho bạn một **PDF có thể tìm kiếm** mà bạn có thể mở trong Adobe Reader, Chrome, hoặc bất kỳ trình đọc PDF nào và ngay lập tức tìm kiếm từ khóa.

## Kết luận  

Bây giờ bạn đã có một giải pháp toàn diện, từ đầu đến cuối, để **tạo PDF có thể tìm kiếm** bằng Aspose OCR. Từ việc tải nguồn, cấu hình các tùy chọn **chuyển đổi pdf đã quét**, trích xuất và xác minh văn bản, đến cuối cùng là lưu kết quả có thể tìm kiếm, mọi bước đều được bao phủ.  

Tiếp theo, bạn có thể khám phá các kịch bản **chuyển đổi pdf ảnh** khi nguồn là một loạt JPEG được đóng gói trong PDF, hoặc đi sâu hơn vào OCR theo ngôn ngữ để cải thiện độ chính xác cho tài liệu đa ngôn ngữ. Dù sao, quy trình vẫn giống nhau: thiết lập tùy chọn, chạy `recognize()`, và lưu lại.

Hãy thoải mái thử nghiệm—thay đổi phạm vi trang, điều chỉnh DPI, hoặc gắn một từ điển tùy chỉnh. Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc kiểm tra tài liệu chính thức của Aspose để nắm bắt các cập nhật API mới nhất. Chúc bạn OCR vui vẻ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}