---
category: general
date: 2026-04-26
description: cách sử dụng OCR trên PDF đã quét, trích xuất văn bản từ PDF, chạy OCR
  trên PDF và chuyển PDF đã quét thành các tệp có thể tìm kiếm trong vài bước.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: vi
og_description: 'cách sử dụng OCR trong Python: học cách trích xuất văn bản từ PDF,
  chạy OCR trên PDF và chuyển PDF đã quét thành tài liệu có thể tìm kiếm.'
og_title: cách sử dụng OCR – Hướng dẫn nhanh để trích xuất văn bản từ PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Cách sử dụng OCR – Trích xuất văn bản từ PDF bằng Python
url: /vi/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách sử dụng OCR – Trích xuất Văn bản từ PDF với Python

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy văn bản từ một hợp đồng, biên lai hoặc ebook đã được quét chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, PDF bạn nhận được chỉ là một hình ảnh, và nếu không có OCR bạn không thể tìm kiếm, lập chỉ mục hoặc phân tích nội dung của nó.  

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, cho thấy **cách sử dụng OCR**, cách **trích xuất văn bản từ PDF**, và lý do tại sao bạn có thể muốn **chuyển đổi PDF đã quét** thành các tài liệu có thể tìm kiếm. Chúng ta cũng sẽ đề cập đến nghệ thuật tinh tế của **tải PDF dưới dạng hình ảnh** để engine OCR có thể nhìn thấy mỗi trang một cách rõ ràng.

> **Xem nhanh:** Khi kết thúc, bạn sẽ có một script tải một PDF đa trang, chạy OCR trên mỗi trang và in ra văn bản đã nhận dạng – không cần dịch vụ bên ngoài.

## Những gì bạn cần

- Python 3.9+ (bất kỳ phiên bản gần đây nào cũng được)
- Gói `aocr` (hoặc bất kỳ thư viện OCR tương thích nào cung cấp `OcrEngine` và `Image.load`)
- Một file PDF đã quét mà bạn muốn xử lý (ví dụ: `contract.pdf`)
- Một lượng RAM vừa phải (≈ 200 MB cho mỗi 100 trang PDF thường là đủ)

Nếu bạn chưa cài đặt thư viện OCR, chạy:

```bash
pip install aocr
```

> **Mẹo chuyên nghiệp:** Sử dụng môi trường ảo để giữ các phụ thuộc của bạn gọn gàng.

## Bước 1: Tải PDF dưới dạng Hình ảnh – Mảnh ghép đầu tiên của Bức tranh

Trước khi OCR có thể thực hiện, PDF phải được biểu diễn dưới dạng hình ảnh. Đây là nơi từ khóa phụ **load pdf as image** phát huy vai trò.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Lý do quan trọng:* `aocr.Image.load` nội bộ raster hoá mỗi trang PDF thành bitmap mà engine OCR có thể hiểu. Nếu bạn bỏ qua bước này và đưa PDF thô vào, engine sẽ báo lỗi vì nó mong đợi dữ liệu pixel, không phải dữ liệu vector.

> **Lưu ý:** Đường dẫn có thể là tuyệt đối hoặc tương đối. Đảm bảo file có thể đọc được; nếu không sẽ gặp `FileNotFoundError`.

## Bước 2: Chạy OCR trên PDF – Biến Pixel thành Ký tự

Bây giờ PDF đã tồn tại dưới dạng hình ảnh, chúng ta cuối cùng có thể **run OCR on PDF**. Đoạn mã sau xử lý mọi trang trong một lần:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Điều gì đang diễn ra phía sau?* `process_all_pages` lặp qua các trang đã raster, áp dụng mô hình OCR và trả về một danh sách các đối tượng kết quả — một cho mỗi trang. Mỗi kết quả chứa văn bản đã nhận dạng, điểm tin cậy và các hộp bao (nếu bạn cần chúng sau này).

## Bước 3: Trích xuất Văn bản từ PDF – Lấy Chuỗi Văn bản ra

Với kết quả OCR trong tay, việc trích xuất văn bản thuần trở nên đơn giản. Chúng ta sẽ duyệt qua các trang và in ra đầu ra, minh họa từ khóa phụ **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Kết quả mong đợi** (rút gọn để ngắn gọn):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Nếu bạn cần văn bản dưới dạng một chuỗi duy nhất, chỉ cần nối lại:

```python
full_text = "\n".join(r.text for r in page_results)
```

Bây giờ bạn đã **trích xuất văn bản từ PDF** thành công bằng OCR.

## Bước 4: Chuyển đổi PDF đã Quét – Tạo PDF có thể Tìm kiếm

Nhiều công cụ hạ nguồn (như Elasticsearch hoặc SharePoint) yêu cầu một PDF có thể tìm kiếm thay vì một bản dump văn bản thuần. Bạn có thể nhúng kết quả OCR trở lại PDF gốc, thực chất **convert scanned PDF** thành phiên bản có thể tìm kiếm.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Tại sao lại làm như vậy?* Một PDF có thể tìm kiếm giữ nguyên bố cục và hình ảnh gốc đồng thời cho phép chọn văn bản và lập chỉ mục — một thắng lợi cho cả con người và máy móc.

## Những Cạm Bẫy Thường Gặp & Các Trường Hợp Đặc Biệt

### PDF Đa Trang Lớn Hơn Bộ Nhớ

Nếu PDF của bạn có hàng trăm trang, việc tải toàn bộ cùng một lúc có thể làm cạn kiệt RAM. Thư viện `aocr` hỗ trợ tải lười:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Sau đó xử lý các trang từng cái một:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Quét Chất Lượng Thấp

Độ chính xác OCR giảm đáng kể trên các bản quét mờ hoặc độ tương phản thấp. Trước khi đưa hình ảnh vào engine, hãy cân nhắc tiền xử lý:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Hỗ trợ Ngôn ngữ

Mặc định engine giả định tiếng Anh. Để **run OCR on PDF** bằng ngôn ngữ khác, đặt mã ngôn ngữ:

```python
ocr_engine.language = "spa"  # Spanish
```

Đảm bảo mô hình ngôn ngữ tương ứng đã được cài đặt.

## Ví dụ Hoàn chỉnh

Kết hợp mọi thứ lại, đây là một script tự chứa mà bạn có thể lưu vào file `ocr_pdf.py` và chạy ngay:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Chạy nó như sau:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Bạn sẽ thấy văn bản được in ra console, và nếu bạn cung cấp tùy chọn `-o`, một PDF có thể tìm kiếm sẽ xuất hiện bên cạnh file gốc.

## Mẹo Chuyên Nghiệp & Thực Hành Tốt

- **Xử lý hàng loạt:** Khi xử lý hàng chục PDF, bao gói logic trên trong một vòng lặp và ghi log thành công/thất bại cho mỗi file.
- **Lọc theo độ tin cậy:** Mỗi `page_result` bao gồm một chỉ số tin cậy. Loại bỏ hoặc đánh dấu các trang có độ tin cậy thấp để xem xét thủ công.
- **Song song:** Nếu CPU của bạn có nhiều lõi, cân nhắc sử dụng `concurrent.futures` để xử lý các trang song song — chỉ cần chú ý tới việc sử dụng bộ nhớ.
- **Khóa phiên bản:** API `aocr` có thể thay đổi. Ghim phiên bản trong `requirements.txt` (ví dụ: `aocr==2.3.1`) để tránh các thay đổi gây lỗi.

## Kết luận

Chúng ta đã đi qua **cách sử dụng OCR** để **trích xuất văn bản từ PDF**, **run OCR on PDF**, **load PDF as image**, và thậm chí **convert scanned PDF** thành định dạng có thể tìm kiếm. Mã nguồn đã hoàn chỉnh, các giải thích bao phủ cả *cái gì* và *tại sao*, và bạn giờ đã có một mẫu có thể tái sử dụng cho bất kỳ dự án nào liên quan tới PDF dựa trên hình ảnh.

Tiếp theo là gì? Hãy thử đưa văn bản đã trích xuất vào một pipeline xử lý ngôn ngữ tự nhiên, lập chỉ mục các PDF có thể tìm kiếm bằng Elasticsearch, hoặc thử nghiệm các backend OCR khác như Tesseract hoặc Azure Computer Vision. Bầu trời là giới hạn, và các công cụ đã sẵn sàng trong tay bạn.

Chúc lập trình vui vẻ, và chúc các PDF của bạn luôn có thể tìm kiếm được! 

![ví dụ cách sử dụng OCR](/images/ocr_workflow.png "cách sử dụng OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}