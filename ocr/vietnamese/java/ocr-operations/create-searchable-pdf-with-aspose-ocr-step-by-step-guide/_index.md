---
category: general
date: 2026-01-02
description: Tạo PDF có thể tìm kiếm từ PDF hình ảnh đã quét bằng Aspose OCR. Tìm
  hiểu cách đặt ngôn ngữ OCR, nhúng lớp văn bản PDF và áp dụng các tùy chọn nén PDF
  cao.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: vi
og_description: Tạo PDF có thể tìm kiếm nhanh chóng. Hướng dẫn này chỉ cách chuyển
  PDF ảnh quét, nhúng lớp văn bản, thiết lập ngôn ngữ OCR và bật nén PDF cao.
og_title: Tạo PDF có thể tìm kiếm với Aspose OCR – Hướng dẫn đầy đủ
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Tạo PDF có thể tìm kiếm bằng Aspose OCR – Hướng dẫn từng bước
url: /vi/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm – Hướng dẫn lập trình đầy đủ

Bạn đã bao giờ cần **tạo file PDF có thể tìm kiếm** từ các ảnh đã quét nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất. Trong nhiều quy trình làm việc với tài liệu, một PDF chỉ chứa hình ảnh là một lối chết cho việc tìm kiếm và lập chỉ mục.  

Tin tốt là với Aspose OCR, bạn có thể **chuyển đổi PDF ảnh đã quét** thành một tài liệu có thể tìm kiếm hoàn toàn chỉ trong vài dòng Java. Hướng dẫn này sẽ dẫn bạn qua từng bước—khởi tạo engine OCR, cấu hình cài đặt PDF nén cao, nhúng lớp văn bản ẩn, và thậm chí chọn ngôn ngữ OCR phù hợp.

Khi hoàn thành, bạn sẽ có một chương trình chạy được tạo ra file PDF có thể tìm kiếm, một tệp bạn có thể đưa vào bất kỳ công cụ tìm kiếm hay hệ thống quản lý tài liệu nào mà không gặp rắc rối.

---

## Tạo PDF có thể tìm kiếm – Tổng quan

Trước khi đi vào code, hãy làm rõ “tạo PDF có thể tìm kiếm” thực sự có nghĩa là gì. Một PDF có thể tìm kiếm chứa hai lớp song song:

1. **Lớp hình ảnh** – ảnh quét gốc (hoặc trang đã được render).  
2. **Lớp văn bản** – các ký tự vô hình nhưng có thể đọc được bởi máy, được trích xuất bằng OCR.

Khi bạn mở PDF như vậy trong Adobe Reader và chọn văn bản, bạn thực sự đang tương tác với lớp văn bản ẩn, không phải với hình ảnh. Cách tiếp cận hai lớp này là điều cho phép chức năng **embed text layer PDF**.

---

## Chuyển đổi PDF ảnh đã quét bằng Aspose OCR

Điều đầu tiên bạn cần là một ảnh đã quét (PNG, JPEG, TIFF) mà bạn muốn biến thành PDF. Aspose OCR có thể đọc ảnh đó, chạy OCR và chuyển kết quả cho một trình ghi PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Tại sao cách này hoạt động:**  
- `setCreateSearchablePdf(true)` yêu cầu Aspose tạo lớp văn bản ẩn, đáp ứng yêu cầu **embed text layer pdf**.  
- `setCompressionLevel(9)` đưa tệp vào phạm vi **high compression pdf**, giảm kích thước cuối cùng mà không làm giảm độ chính xác OCR.  
- Tham số `RecognitionLanguage.ENGLISH` cho thấy cách **set OCR language**; bạn có thể đổi sang tiếng Pháp, tiếng Đức, v.v., tùy thuộc vào tài liệu nguồn.

---

## Cài đặt PDF nén cao

Các PDF quét lớn có thể nhanh chóng tăng lên hàng trăm megabyte. Aspose cung cấp một API nén đơn giản hoạt động ở mức PDF. Phương thức `setCompressionLevel` chấp nhận giá trị từ 0 (không nén) đến 9 (nén tối đa).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Một vài mẹo:

- **Sử dụng định dạng ảnh không mất dữ liệu** (PNG) cho các bản quét chứa nhiều văn bản; JPEG phù hợp hơn cho ảnh.  
- **Bật subsetting phông chữ** nếu bạn nhúng phông chữ tùy chỉnh—Aspose tự động làm việc này khi bạn tạo PDF có thể tìm kiếm.  
- **Kiểm tra kích thước đầu ra** sau mỗi thay đổi; đôi khi nén mức 8 có thể giảm kích thước 10 % mà chất lượng gần như không thay đổi so với mức 9.

---

## Nhúng lớp văn bản PDF để có thể tìm kiếm

Nếu bạn bỏ qua lời gọi `setCreateSearchablePdf(true)`, tệp kết quả sẽ trông ổn nhưng bạn sẽ không thể tìm kiếm nội dung của nó. Lớp văn bản ẩn được tạo bằng cách ánh xạ mỗi ký tự đã nhận dạng tới vị trí của nó trên trang.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Những điểm cần lưu ý:**  

- **Tài liệu đa ngôn ngữ** – bạn có thể cần chạy OCR hai lần, mỗi lần một ngôn ngữ, rồi hợp nhất các lớp văn bản.  
- **Bố cục phức tạp** (bảng, đa cột) – Aspose thực hiện khá tốt, nhưng hãy kiểm tra lại kết quả bằng một trình xem PDF có thể hiển thị văn bản ẩn (ví dụ, chế độ “Edit PDF” của Adobe Acrobat).

---

## Đặt ngôn ngữ OCR để nhận dạng chính xác

Độ chính xác của engine OCR phụ thuộc vào ngôn ngữ bạn chỉ định. Aspose đi kèm với một tập các ngôn ngữ tích hợp, và bạn cũng có thể thêm các gói ngôn ngữ tùy chỉnh.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Khi nào nên thay đổi ngôn ngữ:**  

- Tài liệu chứa **kịch bản không phải Latin** (Cyrillic, Arabic) – chuyển sang `RecognitionLanguage` phù hợp.  
- Các trang đa ngôn ngữ – bạn có thể gọi `recognizeImageAndSave` hai lần, mỗi lần với một ngôn ngữ khác nhau, rồi hợp nhất các PDF.

---

## Chạy ví dụ hoàn chỉnh

Dưới đây là chương trình đầy đủ, sẵn sàng chạy. Thay thế các đường dẫn placeholder bằng vị trí file thực tế, đảm bảo JAR Aspose OCR đã có trong classpath, và thực thi.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Kết quả mong đợi:** Khi chạy chương trình, console sẽ in:

```
Searchable PDF created.
```

Mở `searchable.pdf` bằng bất kỳ trình xem PDF nào, thử chọn văn bản và bạn sẽ thấy lớp vô hình hoạt động. Bạn đã **tạo PDF có thể tìm kiếm** thành công từ một ảnh đã quét.

---

![create searchable pdf example](image-placeholder.png "create searchable pdf example")

*Ảnh chụp màn hình trên (placeholder) thường sẽ hiển thị trình xem PDF với văn bản có thể chọn được trên một trang đã quét.*

---

## Kết luận

Chúng ta đã bao quát mọi thứ bạn cần để **tạo PDF có thể tìm kiếm** bằng Aspose OCR:

- Khởi tạo engine OCR.  
- **Chuyển đổi PDF ảnh đã quét** bằng cách đưa PNG/JPEG vào `recognizeImageAndSave`.  
- Sử dụng `setCreateSearchablePdf(true)` để **embed text layer PDF**.  
- Áp dụng `setCompressionLevel(9)` cho một **high compression PDF** nhẹ nhàng.  
- Chọn `RecognitionLanguage` phù hợp để **set OCR language** và đạt độ chính xác tối đa.

Từ đây, bạn có thể thử nghiệm xử lý hàng loạt, các ngôn ngữ khác nhau, hoặc thậm chí kết hợp nhiều trang quét thành một PDF có thể tìm kiếm duy nhất. Mẫu này cũng áp dụng cho các ngôn ngữ khác như tiếng Tây Ban Nha hay tiếng Nhật—chỉ cần đổi giá trị enum `RecognitionLanguage`.

Nếu gặp khó khăn, hãy để lại bình luận, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}