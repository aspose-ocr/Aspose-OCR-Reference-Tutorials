---
category: general
date: 2026-06-22
description: Tạo PDF có thể tìm kiếm bằng OCR trong Java. Tìm hiểu cách tắt nén và
  chuyển đổi nhanh PDF ảnh quét sang PDF có thể tìm kiếm.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: vi
og_description: Tạo PDF có thể tìm kiếm bằng OCR trong Java. Hướng dẫn này chỉ cách
  tắt nén, chuyển đổi PDF ảnh đã quét và tạo PDF không nén.
og_title: Tạo PDF có thể tìm kiếm với OCR – Hướng dẫn Java đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: Tạo PDF có thể tìm kiếm với OCR – Hướng dẫn đầy đủ
url: /vi/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm với OCR – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một loạt ảnh đã quét nhưng không chắc phải bật/tắt những cài đặt nào? Bạn không phải là người duy nhất—hầu hết các nhà phát triển đều gặp khó khăn khi kết quả ra thành một khối dữ liệu khổng lồ, không thể đọc được.  

Trong tutorial này chúng ta sẽ đi qua một ví dụ sạch sẽ, từ đầu đến cuối, cho bạn thấy cách **tạo PDF có thể tìm kiếm** bằng một engine OCR Java, **chuyển đổi PDF ảnh đã quét**, và quan trọng nhất, **cách tắt nén** để file kết quả giữ nguyên kích thước gốc. Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng chạy và hiểu rõ tại sao mỗi cấu hình lại quan trọng.

## Những gì bạn sẽ học

* Cách cấu hình engine OCR để **ocr to searchable pdf**.  
* Lý do cần tắt nén PDF và cách có được **pdf without compression**.  
* Một chương trình Java hoàn chỉnh lấy ảnh đã quét, chạy OCR và lưu **searchable PDF**.  
* Mẹo xử lý các trường hợp đặc biệt như quét đa trang hoặc nguồn ảnh độ phân giải thấp.  

**Prerequisites** – Java 8+ đã được cài đặt, một OCR SDK tương thích (mã mẫu sử dụng ABBYY FineReader Engine API, nhưng các khái niệm áp dụng cho bất kỳ thư viện nào có `setOutputFormat` và `setPdfCompression`). Một IDE như IntelliJ IDEA hoặc Eclipse sẽ giúp công việc dễ dàng hơn, nhưng một trình soạn thảo văn bản đơn giản cũng đủ.

---

![Tạo quy trình PDF có thể tìm kiếm](image-placeholder.png "Sơ đồ mô tả quy trình tạo PDF có thể tìm kiếm từ ảnh đã quét đến PDF cuối cùng")

## Bước 1: Đặt Engine OCR thành **Create Searchable PDF**

Điều đầu tiên bạn cần nói với engine OCR là loại đầu ra bạn mong muốn. Mặc định nhiều SDK sẽ xuất ra văn bản thuần hoặc PDF raster, không thể tìm kiếm. Thay đổi định dạng sẽ thực hiện phần việc nặng cho bạn.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Lý do quan trọng*: Cờ `PDF_SEARCHABLE` chỉ thị cho engine nhúng một lớp văn bản vô hình phía dưới ảnh đã quét. Các công cụ tìm kiếm sau đó có thể lập chỉ mục tài liệu, khiến nó hoạt động như bất kỳ PDF gốc nào bạn mở trong Adobe Reader.

## Bước 2: Tắt Nén – **How to Disable Compression** đúng cách

Nếu bỏ qua bước này, engine sẽ nén mỗi trang để tiết kiệm không gian, nhưng việc nén có thể làm mờ chi tiết tinh vi—đặc biệt gây vấn đề khi bạn cần trích xuất ảnh độ phân giải cao sau này.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro tip**: Tắt nén là điều thiết yếu khi bạn dự định lưu trữ tài liệu pháp lý hoặc ảnh y tế, nơi mỗi pixel đều quan trọng. File kết quả có thể lớn hơn, nhưng bạn giữ nguyên kích thước và độ rõ gốc.

## Bước 3: Thực hiện OCR và nhận Document kết quả

Bây giờ engine đã biết phải xuất gì và xử lý ảnh như thế nào, bạn có thể chạy nhận dạng. Lệnh trả về một đối tượng `PdfDocument` sẵn sàng lưu hoặc tiếp tục xử lý.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Điều gì đang diễn ra bên trong?* Engine xử lý từng trang đầu vào, thực hiện nhận dạng ký tự, và ghép lớp văn bản ẩn lên ảnh. Nếu có nhiều trang, chúng sẽ tự động được nối lại.

## Bước 4: Lưu **Searchable PDF** vào Đĩa

Cuối cùng, ghi PDF trong bộ nhớ ra file. Chọn một vị trí bạn có quyền ghi, và đặt tên file có ý nghĩa.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

Khi bạn mở `searchable.pdf` trong trình xem, bạn sẽ thấy có thể chọn và tìm kiếm văn bản—mặc dù nội dung hiển thị vẫn là ảnh quét gốc.

### Ví dụ Hoạt động Đầy đủ

Dưới đây là một lớp Java tự chứa, kết hợp cả bốn bước lại với nhau. Bạn có thể sao chép‑dán, điều chỉnh đường dẫn đầu vào, và chạy ngay.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Kết quả mong đợi** – Sau khi chạy chương trình, bạn sẽ thấy thông báo console ở trên, và file `searchable.pdf` sẽ xuất hiện trong `YOUR_DIRECTORY`. Mở nó bằng bất kỳ trình đọc PDF nào, bạn sẽ có thể:

* Đánh dấu văn bản.  
* Sử dụng chức năng tìm kiếm tích hợp (Ctrl + F) để định vị từ.  
* Xuất lớp văn bản ẩn nếu cần.

---

## Tại sao cần Tắt Nén? Hiểu về **PDF Without Compression**

Bạn có thể tự hỏi, “Nén không phải luôn luôn tốt sao?” Câu trả lời có phần phức tạp:

| Tình huống | Giữ Nén (`NORMAL`) | Tắt Nén (`NONE`) |
|-----------|--------------------|------------------|
| Lưu trữ hợp đồng pháp lý | ❌ Có thể làm thay đổi độ chính xác pixel | ✅ Đảm bảo hình ảnh gốc |
| Lô lớn ảnh độ phân giải thấp | ✅ Tiết kiệm dung lượng | ❌ Tăng kích thước mà không có lợi ích |
| Cần độ chính xác OCR trên phông chữ siêu nhỏ | ❌ Làm mờ chi tiết | ✅ Bảo toàn mọi nét chữ |

Tóm lại, **how to disable compression** là sự cân bằng giữa lưu trữ và độ trung thực. Đối với hầu hết quy trình PDF có thể tìm kiếm, nơi bạn chỉ cần tìm văn bản chứ không cần in lại ảnh, tắt nén là lựa chọn an toàn nhất.

## Chuyển Đổi **Scanned Image PDF** Trực Tiếp

Đôi khi bạn đã có một PDF chứa ảnh đã quét (PDF “chỉ ảnh”). Để **convert scanned image pdf** thành phiên bản có thể tìm kiếm, bạn có thể đưa toàn bộ PDF cho engine thay vì từng ảnh riêng lẻ:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Các cờ cấu hình giống nhau (`PDF_SEARCHABLE` và `PdfCompression.NONE`) vẫn được áp dụng, vì vậy bạn sẽ nhận được **pdf without compression** ngay cả khi bắt đầu từ một container PDF.

## Những Sai Lầm Thường Gặp & Cách Tránh

* **Quên đặt định dạng đầu ra** – Engine mặc định tạo PDF raster, không thể tìm kiếm. Luôn gọi `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` trước `recognizeToPdf()`.  
* **Hết bộ nhớ khi xử lý lô lớn** – Tải và xử lý các trang theo lô, hoặc dùng API streaming nếu SDK hỗ trợ.  
* **Đường dẫn file không đúng** – Dùng đường dẫn tuyệt đối hoặc đảm bảo thư mục làm việc được đặt đúng; nếu không `pdf.save()` sẽ ném `IOException`.  
* **Giấy phép chưa kích hoạt** – Hầu hết các OCR SDK thương mại yêu cầu giấy phép hợp lệ; engine sẽ ném ngoại lệ runtime nếu thiếu.

---

## Kết luận

Bạn đã có một giải pháp hoàn chỉnh, sẵn sàng chạy, cho thấy **how to create searchable PDF** từ ảnh đã quét, cách **convert scanned image PDF**, và chính xác **how to disable compression** để tạo **pdf without compression**. Các bước chính là:

1. Đặt định dạng đầu ra thành `PDF_SEARCHABLE`.  
2. Tắt nén PDF bằng `PdfCompression.NONE`.  
3. Chạy OCR và lấy `PdfDocument`.  
4. Lưu file ra đĩa.

Từ đây bạn có thể thử nghiệm với phông chữ, thêm watermark, hoặc xử lý hàng loạt toàn bộ thư mục. Nếu bạn muốn tìm hiểu thêm về gói ngôn ngữ OCR, xử lý TIFF đa trang, hoặc tích hợp quy trình này vào dịch vụ web, hãy xem các tutorial sắp tới của chúng tôi về “OCR language selection in Java” và “Streaming OCR for large document sets”.

Có câu hỏi, hoặc gặp vấn đề? Để lại bình luận bên dưới—chúc bạn lập trình vui vẻ và tận hưởng các PDF mới có thể tìm kiếm!

## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã mẫu đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}