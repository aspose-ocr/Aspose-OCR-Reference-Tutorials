---
category: general
date: 2026-04-29
description: Trích xuất văn bản từ PDF bằng Aspose OCR trong Python. Tìm hiểu xử lý
  OCR PDF hàng loạt, chuyển đổi văn bản PDF đã quét và xử lý các trang có độ tin cậy
  thấp.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: vi
og_description: Trích xuất văn bản từ PDF bằng Aspose OCR trong Python. Hướng dẫn
  này trình bày xử lý OCR PDF hàng loạt, chuyển đổi văn bản PDF đã quét và xử lý kết
  quả có độ tin cậy thấp.
og_title: Trích xuất văn bản từ PDF – OCR PDF bằng Python
tags:
- OCR
- Python
- PDF processing
title: Trích xuất văn bản từ PDF – OCR PDF bằng Python
url: /vi/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ PDF – OCR PDF với Python

Bạn đã bao giờ cần **trích xuất văn bản từ PDF** nhưng tệp chỉ là hình ảnh đã được quét? Bạn không đơn độc—nhiều nhà phát triển gặp phải rào cản này khi muốn chuyển PDF thành dữ liệu có thể tìm kiếm. Tin tốt là gì? Với Aspose OCR cho Python, bạn có thể chuyển đổi văn bản PDF đã quét chỉ trong vài dòng code, và thậm chí thực hiện **xử lý OCR PDF hàng loạt** khi có hàng chục tệp cần xử lý.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: cài đặt thư viện, chạy OCR trên một PDF đơn, mở rộng thành batch, và xử lý các trang có độ tin cậy thấp để bạn biết khi nào cần kiểm tra thủ công. Khi kết thúc, bạn sẽ có một script sẵn sàng chạy để trích xuất văn bản từ bất kỳ PDF đã quét nào, và bạn sẽ hiểu lý do đằng sau mỗi bước.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

- Python 3.8 hoặc mới hơn (code sử dụng f‑strings, vì vậy 3.6+ cũng hoạt động, nhưng khuyến nghị 3.8+)
- Giấy phép Aspose OCR cho Python hoặc khóa dùng thử miễn phí (bạn có thể lấy từ trang web Aspose)
- Một thư mục chứa một hoặc nhiều PDF đã quét mà bạn muốn xử lý
- Một lượng không gian đĩa vừa đủ cho các báo cáo *.txt* được tạo ra

Đó là tất cả—không cần phụ thuộc bên ngoài nặng, không cần OpenCV. Engine OCR của Aspose sẽ thực hiện phần việc nặng cho bạn.

## Cài đặt môi trường

Đầu tiên, cài đặt gói Aspose OCR từ PyPI:

```bash
pip install aspose-ocr
```

Nếu bạn có tệp giấy phép (`Aspose.OCR.lic`), đặt nó vào thư mục gốc dự án và kích hoạt như sau:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Mẹo chuyên nghiệp:** Giữ tệp giấy phép ra khỏi hệ thống kiểm soát phiên bản; thêm nó vào `.gitignore` để tránh lộ ngoài ý muốn.

## Thực hiện OCR trên một PDF đơn

Bây giờ hãy trích xuất văn bản từ một PDF đã quét duy nhất. Các bước chính là:

1. Tạo một thể hiện `OcrEngine`.
2. Chỉ định tệp PDF cho nó.
3. Lấy một `OcrResult` cho mỗi trang.
4. Ghi kết quả văn bản thuần vào đĩa.
5. Giải phóng engine để giải phóng tài nguyên gốc.

Dưới đây là script đầy đủ, có thể chạy ngay:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Bạn sẽ thấy gì:** Đối với mỗi trang, script sẽ in ra một dòng như `Page 1: confidence 97.45%`. Nếu một trang có độ tin cậy dưới ngưỡng 80 %, một cảnh báo sẽ xuất hiện, cho bạn biết OCR có thể đã bỏ sót ký tự.

### Tại sao cách này hoạt động

- **`OcrEngine`** là cổng vào thư viện OCR gốc của Aspose; nó xử lý mọi thứ từ tiền xử lý hình ảnh đến nhận dạng ký tự.
- **`extract_from_pdf`** tự động raster hoá mỗi trang PDF, vì vậy bạn không cần tự chuyển PDF sang hình ảnh.
- **Điểm tin cậy** cho phép bạn tự động kiểm tra chất lượng—rất quan trọng khi xử lý tài liệu pháp lý hoặc y tế, nơi độ chính xác là yếu tố then chốt.

## Xử lý OCR PDF hàng loạt với Python

Hầu hết các dự án thực tế liên quan đến hơn một tệp. Hãy mở rộng script đơn thành một **pipeline xử lý OCR PDF hàng loạt** đi qua một thư mục, xử lý mỗi PDF và lưu kết quả vào một thư mục con tương ứng.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Lợi ích của cách này

- **Khả năng mở rộng:** Hàm duyệt thư mục một lần, tạo thư mục đầu ra riêng cho mỗi PDF. Giúp giữ mọi thứ gọn gàng khi bạn có hàng chục tài liệu.
- **Tái sử dụng:** `ocr_pdf_file` có thể được gọi từ các script khác (ví dụ, một dịch vụ web) vì nó là một hàm thuần.
- **Xử lý lỗi:** Script in ra thông báo thân thiện nếu thư mục đầu vào rỗng, tránh việc thất bại im lặng.

## Chuyển đổi văn bản PDF đã quét – Xử lý các trường hợp đặc biệt

Mặc dù code trên hoạt động với hầu hết các PDF, bạn có thể gặp một số tình huống đặc biệt:

| Tình huống | Nguyên nhân | Cách khắc phục |
|-----------|-------------|----------------|
| **PDF được mã hoá** | PDF được bảo vệ bằng mật khẩu. | Truyền mật khẩu vào `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Tài liệu đa ngôn ngữ** | Aspose OCR mặc định là tiếng Anh. | Đặt `ocr_engine.language = "spa"` cho tiếng Tây Ban Nha, hoặc cung cấp danh sách cho các ngôn ngữ hỗn hợp. |
| **PDF rất lớn (>500 trang)** | Tiêu thụ bộ nhớ tăng vì mỗi trang được tải vào RAM. | Xử lý PDF theo từng khối bằng `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` và lặp lại. |
| **Chất lượng quét kém** | DPI thấp hoặc nhiễu mạnh làm giảm độ tin cậy. | Tiền xử lý PDF với `engine.image_preprocessing = True` hoặc tăng DPI bằng `engine.dpi = 300`. |

> **Lưu ý:** Bật tiền xử lý hình ảnh có thể làm tăng thời gian CPU đáng kể. Nếu bạn chạy batch vào ban đêm, hãy lên lịch đủ thời gian hoặc khởi động một worker riêng.

## Kiểm tra kết quả

Sau khi script hoàn thành, bạn sẽ thấy cấu trúc thư mục như sau:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Mở bất kỳ tệp `.txt` nào; bạn sẽ thấy văn bản sạch, mã hoá UTF‑8, phản ánh nội dung đã quét gốc. Nếu gặp ký tự lộn xộn, hãy kiểm tra lại cài đặt ngôn ngữ của PDF và đảm bảo các gói phông chữ phù hợp đã được cài trên máy.

## Dọn dẹp tài nguyên

Aspose OCR dựa vào các DLL gốc, vì vậy cần gọi `engine.dispose()` một khi công việc xong. Bỏ qua bước này có thể gây rò rỉ bộ nhớ, đặc biệt trong các job batch chạy lâu.

```python
# Always the last line of your script
engine.dispose()
```

## Ví dụ hoàn chỉnh từ đầu đến cuối

Kết hợp mọi thứ lại, dưới đây là một script duy nhất

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}