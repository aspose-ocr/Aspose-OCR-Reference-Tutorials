---
category: general
date: 2026-07-05
description: Tạo PDF có thể tìm kiếm trong Java bằng Aspose OCR. Tìm hiểu cách nén
  hình ảnh trong PDF, chuyển đổi ảnh quét sang PDF và tắt nhúng phông chữ trong PDF
  để giảm kích thước tệp.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm bằng Java với Aspose OCR. Hướng dẫn này cho
  thấy cách nén hình ảnh trong PDF, chuyển đổi ảnh quét sang PDF và tắt việc nhúng
  phông chữ trong PDF.
og_title: Tạo PDF có thể tìm kiếm trong Java – Hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Tạo PDF có thể tìm kiếm trong Java – Hướng dẫn toàn diện
url: /vi/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm trong Java – Hướng dẫn đầy đủ

Bạn đã bao giờ cần **create searchable PDF** từ một tài liệu đã quét nhưng lại bối rối ở phần “làm sao để thực hiện” chưa? Bạn không phải là người duy nhất. Trong nhiều dự án, việc chuyển đổi một TIFF hoặc JPEG thành PDF mà bạn thực sự có thể tìm kiếm là một tính năng *phải có*, đặc biệt khi bạn cũng muốn **compress images in PDF** để giữ kích thước tệp ở mức hợp lý.  

Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ thực hành sử dụng Aspose OCR cho Java. Khi kết thúc, bạn sẽ biết chính xác cách **convert scanned image to PDF**, điều chỉnh cài đặt **compress images in PDF** và thậm chí **disable font embedding PDF** để giảm thêm vài kilobyte. Không có phần thừa—chỉ có một giải pháp hoàn chỉnh, có thể chạy được mà bạn có thể đưa vào cơ sở mã của mình ngay hôm nay.

## Những gì bạn sẽ học

- Cài đặt engine Aspose OCR trong dự án Java.  
- Thực hiện OCR trên một tệp TIFF (hoặc bất kỳ hình ảnh raster nào).  
- Cấu hình `PdfSaveOptions` để **compress images in PDF** và **disable font embedding PDF**.  
- Lưu kết quả dưới dạng **searchable PDF** mà bạn có thể lập chỉ mục hoặc tìm kiếm ngay lập tức.  

**Prerequisites**  
- Java 8 hoặc mới hơn đã được cài đặt.  
- Maven hoặc Gradle để quản lý phụ thuộc (chúng tôi sẽ hiển thị đoạn mã Maven).  
- Một tệp hình ảnh đã quét (TIFF, PNG hoặc JPEG) sẵn sàng để xử lý.  

Nếu bạn đã có những thứ trên, hãy bắt đầu.

![Quy trình tạo PDF có thể tìm kiếm – Chuyển đổi OCR Java sang PDF](/images/create-searchable-pdf-workflow.png "Diagram showing the steps to create searchable PDF with Aspose OCR")

## Bước 1: Thêm phụ thuộc Aspose OCR

Đầu tiên, kéo thư viện Aspose OCR vào dự án của bạn. Với Maven, thêm đoạn này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Nếu bạn thích Gradle, tương đương là:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Mẹo chuyên nghiệp:** Hãy chú ý đến ghi chú phát hành của Aspose; các phiên bản mới thường mang lại cải thiện hiệu năng cho độ chính xác của OCR.

## Bước 2: Khởi tạo Engine OCR

Tạo một engine OCR đơn giản như việc khởi tạo `OcrEngine`. Đối tượng này sẽ xử lý mọi thứ từ tải hình ảnh đến trích xuất văn bản.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Tại sao chúng ta cần một engine riêng? Aspose tách phần xử lý nặng (tiền xử lý hình ảnh, mô hình ngôn ngữ) ra khỏi phần còn lại của ứng dụng, vì vậy bạn có thể tái sử dụng cùng một `engine` cho nhiều tệp mà không cần khởi tạo lại các tài nguyên nặng.

## Bước 3: Thực hiện OCR trên hình ảnh đã quét

Bây giờ chúng ta cung cấp cho engine một tệp đã quét. Phương thức `recognizeImage` trả về một `RecognitionResult` chứa văn bản đã trích xuất và thông tin bố cục.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Nếu hình ảnh không phải là TIFF thì sao?**  
> Aspose OCR tự động phát hiện các định dạng raster phổ biến, vì vậy bạn có thể chỉ tới một JPEG, PNG hoặc BMP mà không cần thay đổi mã.

## Bước 4: Cấu hình tùy chọn lưu PDF (Nén hình ảnh & Tắt nhúng phông chữ)

Đây là nơi các từ khóa phụ tỏa sáng. Chúng ta sẽ yêu cầu Aspose **compress images in PDF** và **disable font embedding PDF**. Cả hai cài đặt đều giảm kích thước tệp cuối cùng—rất hữu ích khi bạn phải gửi hàng chục tài liệu.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Tại sao nên nén hình ảnh?**  
Các trang quét thường có độ phân giải cao; nén chúng xuống chất lượng 80 % có thể giảm một PDF 10 trang từ 12 MB xuống dưới 3 MB mà không gây mất mát hình ảnh đáng chú ý.

**Tại sao tắt nhúng phông chữ?**  
Nếu engine OCR sử dụng các phông chữ hệ thống tiêu chuẩn (như Arial hoặc Times New Roman), việc nhúng chúng là thừa thãi. Tắt tính năng này sẽ giảm kích thước tệp hơn nữa, đặc biệt đối với các lô lớn.

## Bước 5: Lưu kết quả OCR dưới dạng PDF có thể tìm kiếm

Bước cuối cùng ghép nối mọi thứ lại: hình ảnh gốc, lớp văn bản đã trích xuất và các tùy chọn PDF chúng ta vừa thiết lập.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Khi bạn mở `document.pdf` trong Adobe Reader hoặc bất kỳ trình xem hiện đại nào, bạn sẽ thấy hình ảnh quét gốc **cộng** với một lớp văn bản vô hình. Gõ một từ vào ô tìm kiếm sẽ làm nổi bật các kết quả khớp—đúng như lời hứa của “create searchable pdf”.

### Kết quả mong đợi

Chạy chương trình với một TIFF hợp lệ sẽ cho ra kết quả giống như:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Mở PDF, nhấn `Ctrl+F`, gõ một từ xuất hiện trong trang quét, và xem nó nhảy tới vị trí đúng. Đó là dấu hiệu của một quy trình **create searchable pdf** thành công.

## Những lỗi thường gặp & Cách tránh

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **PDF trống** | `PdfSaveOptions` không được truyền vào `saveAsSearchablePdf`. | Đảm bảo bạn gọi phiên bản overload chấp nhận `PdfSaveOptions`. |
| **Ký tự rác** | Ngôn ngữ OCR không được đặt (mặc định là tiếng Anh). | Sử dụng `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` trước `recognizeImage`. |
| **Kích thước tệp quá lớn** | `setCompressImages(false)` hoặc `setEmbedFonts(true)`. | Giữ cả hai cờ như đã minh họa ở trên. |
| **Biến dạng hình ảnh** | `setImageQuality` được đặt quá thấp (<50). | Giữ mức 70‑90 để cân bằng tốt. |

## Mở rộng ví dụ

Bây giờ bạn đã có thể **convert scanned image to PDF** và kiểm soát kích thước, bạn có thể muốn:

- **Xử lý hàng loạt** một thư mục các bản quét bằng vòng lặp đơn giản `for(File f : folder.listFiles())`.  
- Thêm **watermarks** bằng Aspose PDF (`PdfDocument.addWatermarkText`).  
- Xuất văn bản OCR ra tệp **plain .txt** cho hệ thống lập chỉ mục (`result.getText().writeToFile("doc.txt")`).  

Tất cả các phần mở rộng này đều tái sử dụng cùng một thể hiện `OcrEngine`, giúp giảm mức sử dụng bộ nhớ.

## Mã đầy đủ, sẵn sàng chạy

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Sao chép‑dán đoạn này vào IDE của bạn, thay thế `YOUR_DIRECTORY` bằng đường dẫn thực tế, và chạy. Nếu mọi thứ được cấu hình đúng, bạn sẽ có một **searchable PDF** nhẹ nhõm nhờ nén hình ảnh và tắt nhúng phông chữ.

## Kết luận

Chúng tôi vừa trình bày mọi thứ bạn cần để **create searchable pdf** trong Java bằng Aspose OCR. Từ khởi tạo engine, thực hiện OCR, điều chỉnh **compress images in pdf**, và **disable font embedding pdf**, đến cuối cùng lưu tài liệu có thể tìm kiếm—mỗi bước đều được giải thích kèm lý do phía sau.

Sẵn sàng cho thử thách tiếp theo? Hãy thử thêm các gói ngôn ngữ OCR, xử lý hàng loạt toàn bộ thư mục, hoặc lớp PDF với chú thích. Những nền tảng bạn vừa nắm vững sẽ giúp các phần mở rộng này trở nên dễ dàng.

Có câu hỏi hoặc muốn chia sẻ mẹo của bạn? Để lại bình luận bên dưới, chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Nhận dạng văn bản PDF – Các thao tác OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-operations/)
- [OCR nhận dạng tài liệu PDF trong Aspose.OCR cho Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Cách OCR PDF trong .NET với Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}