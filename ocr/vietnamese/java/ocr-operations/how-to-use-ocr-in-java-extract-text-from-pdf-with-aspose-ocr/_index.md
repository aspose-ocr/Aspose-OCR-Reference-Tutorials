---
category: general
date: 2026-02-17
description: Cách sử dụng OCR trong Java để trích xuất văn bản từ PDF, chuyển PDF
  thành hình ảnh và thực hiện OCR trên các tệp PDF đã quét bằng Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- convert pdf to images
- perform OCR on pdf
- recognize scanned pdf
language: vi
og_description: Cách sử dụng OCR trong Java để trích xuất văn bản từ các tệp PDF.
  Tìm hiểu cách chuyển PDF thành hình ảnh và nhận dạng PDF đã quét với Aspose.OCR.
og_title: Cách sử dụng OCR trong Java – Hướng dẫn đầy đủ
tags:
- OCR
- Java
- Aspose
title: Cách sử dụng OCR trong Java – Trích xuất văn bản từ PDF với Aspose.OCR
url: /vi/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong Java – Trích Xuất Văn Bản từ PDF với Aspose.OCR

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để biến một PDF đã quét thành văn bản có thể tìm kiếm chưa? Bạn không phải là người duy nhất. Hầu hết các nhà phát triển gặp khó khăn khi một PDF xuất hiện dưới dạng một loạt các hình ảnh, và các công cụ trích xuất văn bản thông thường chỉ trả về rỗng. Tin tốt là gì? Chỉ với vài dòng Java và Aspose.OCR, bạn có thể **trích xuất văn bản từ PDF**, **chuyển PDF thành hình ảnh**, và **nhận dạng PDF đã quét** trong một quy trình đơn giản, không đau đầu.

Trong hướng dẫn này, chúng ta sẽ đi qua mọi thứ bạn cần biết — từ cấp phép thư viện đến việc in kết quả cuối cùng. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy, có thể lấy văn bản thuần từ bất kỳ báo cáo, hoá đơn, hoặc ebook đã quét nào. Không cần dịch vụ bên ngoài, không có phép màu — chỉ có mã Java thuần túy mà bạn kiểm soát.

## Những Gì Bạn Cần

- **Java Development Kit (JDK) 8+** – bất kỳ phiên bản mới nào cũng được.
- **Aspose.OCR for Java** JAR (tải về từ trang web Aspose).  
- Một **tệp giấy phép Aspose.OCR hợp lệ** (`Aspose.OCR.lic`). Bản dùng thử miễn phí hoạt động, nhưng giấy phép sẽ mở khóa độ chính xác đầy đủ.
- Một **PDF đã quét mẫu** (ví dụ: `scanned-report.pdf`).  
- Một IDE hoặc trình soạn thảo văn bản đơn giản cộng với terminal.

Đó là tất cả. Không cần Maven, không cần Gradle, không có phụ thuộc bổ sung — chỉ cần JAR Aspose.OCR nằm trong classpath của bạn.

![cách sử dụng OCR ví dụ](image-placeholder.png "cách sử dụng OCR ví dụ")

## Bước 1 – Tải Bản Quyền Aspose.OCR của Bạn (Tại Sao Điều Này Quan Trọng)

Trước khi engine có thể chạy ở tốc độ tối đa, bạn phải cho nó biết vị trí tệp giấy phép. Bỏ qua bước này sẽ buộc thư viện vào chế độ đánh giá, khiến đầu ra có watermark và có thể giới hạn độ chính xác.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the license – required for unrestricted OCR
        License license = new License();
        license.setLicense("Aspose.OCR.lic");
```

**Tại sao cách này hoạt động:** Lớp `License` đọc tệp `.lic` và đăng ký nó toàn cục. Khi đã thiết lập, mọi `OcrEngine` bạn tạo sẽ tự động sử dụng các tính năng có giấy phép.

## Bước 2 – Tạo Engine OCR (Trí Tuệ Đằng Sau Phép Màu)

Một thể hiện `OcrEngine` là bộ máy thực hiện việc quét hình ảnh và xuất ra văn bản. Hãy nghĩ nó như bộ não giải mã các mẫu pixel.

```java
        // Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Mẹo chuyên nghiệp:** Bạn có thể điều chỉnh ngôn ngữ, ngưỡng độ tin cậy, hoặc thậm chí bật tăng tốc GPU thông qua các thuộc tính của engine. Đối với hầu hết các PDF tiếng Anh, các giá trị mặc định là đủ.

## Bước 3 – Chuẩn Bị Đầu Vào: Thêm PDF Của Bạn (Chuyển PDF Thành Hình Ảnh Bên Trong)

Aspose.OCR coi mỗi trang của PDF như một hình ảnh. Khi bạn gọi `addPdf`, thư viện âm thầm raster hoá mỗi trang, chính xác là những gì bạn cần để **chuyển PDF thành hình ảnh** trước khi nhận dạng.

```java
        // Prepare OCR input – each PDF page becomes an image internally
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");
```

**Điều gì đang xảy ra:**  
- PDF được mở.  
- Mỗi trang được render ở 300 dpi (mặc định) để bảo toàn chi tiết ký tự.  
- Các đối tượng bitmap đã render được lưu trong bộ sưu tập `OcrInput`.

Nếu bạn cần hình ảnh thô (để gỡ lỗi hoặc tiền xử lý tùy chỉnh), hãy gọi `ocrInput.getPages()` sau bước này.

## Bước 4 – Chạy Quy Trình OCR (Thực Hiện OCR trên PDF)

Bây giờ công việc nặng bắt đầu. Phương thức `recognize` lặp qua từng hình ảnh, chạy thuật toán nhận dạng, và tổng hợp kết quả vào một `OcrResult`.

```java
        // Run OCR on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Tại sao bạn nên quan tâm:** `OcrResult` không chỉ chứa văn bản thuần mà còn có điểm tin cậy, hộp bao, và tham chiếu tới hình ảnh gốc. Đối với hầu hết các trường hợp, bạn chỉ cần `getText()`.

## Bước 5 – Lấy và Hiển Thị Văn Bản Đã Trích Xuất

Cuối cùng, lấy chuỗi văn bản thuần từ kết quả và in ra. Bạn cũng có thể ghi nó vào tệp, đưa vào chỉ mục tìm kiếm, hoặc truyền vào pipeline NLP tiếp theo.

```java
        // Output the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

### Kết Quả Dự Kiến

Nếu `scanned-report.pdf` chứa một đoạn văn đơn giản, bạn sẽ thấy thứ gì đó như:

```
Extracted text:
Quarterly Sales Report
Region: North America
Total Revenue: $4,527,000
...
```

Định dạng chính xác sẽ phản ánh bố cục gốc, giữ lại các ngắt dòng nếu có thể.

## Xử Lý Các Trường Hợp Đặc Biệt Thông Thường

### 1. PDF Đa Ngôn Ngữ

Nếu tài liệu của bạn chứa văn bản tiếng Pháp hoặc Tây Ban Nha, hãy đặt ngôn ngữ trước khi gọi `recognize`:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.FRENCH);
```

Bạn có thể cung cấp một mảng các ngôn ngữ để engine tự động phát hiện.

### 2. Quét Ảnh Độ Phân Giải Thấp

Khi làm việc với các bản quét 150 dpi, tăng DPI render nội bộ:

```java
ocrInput.addPdf("low-res.pdf", 600); // render at 600 dpi for better accuracy
```

DPI cao hơn cải thiện độ rõ nét của ký tự nhưng tiêu tốn nhiều bộ nhớ hơn.

### 3. PDF Lớn (Quản Lý Bộ Nhớ)

Đối với PDF có hàng chục trang, hãy xử lý chúng theo lô:

```java
int batchSize = 10;
for (int i = 0; i < ocrInput.getPages().size(); i += batchSize) {
    List<OcrPage> batch = ocrInput.getPages().subList(i, Math.min(i + batchSize, ocrInput.getPages().size()));
    OcrInput batchInput = new OcrInput();
    batchInput.getPages().addAll(batch);
    OcrResult batchResult = ocrEngine.recognize(batchInput);
    // Append batchResult.getText() to your final output
}
```

Cách tiếp cận này giúp ngăn heap JVM bị bùng nổ.

## Ví Dụ Đầy Đủ, Sẵn Sàng Chạy

Dưới đây là chương trình hoàn chỉnh — bao gồm các import và xử lý giấy phép — để bạn có thể sao chép và chạy ngay lập tức.

```java
import com.aspose.ocr.*;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (required for full functionality)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // Step 2: Create an OCR engine instance that will perform the recognition
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Prepare the OCR input by adding the PDF file.
        // Each page of the PDF is internally converted to an image.
        OcrInput ocrInput = new OcrInput();
        ocrInput.addPdf("YOUR_DIRECTORY/scanned-report.pdf");

        // Step 4: Run the OCR process on the prepared input
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // Step 5: Display the extracted text
        System.out.println("Extracted text:\n" + ocrResult.getText());
    }
}
```

Chạy nó với:

```bash
javac -cp "path/to/aspose-ocr.jar" PdfOcrDemo.java
java -cp ".:path/to/aspose-ocr.jar" PdfOcrDemo
```

Bạn sẽ thấy văn bản đã trích xuất được in ra console.

## Tóm Tắt – Những Điều Chúng Ta Đã Bao Quát

- **Cách sử dụng OCR** trong Java với Aspose.OCR.  
- Quy trình **trích xuất văn bản từ PDF**.  
- Nội bộ, thư viện **chuyển PDF thành hình ảnh** trước khi nhận dạng ký tự.  
- Các mẹo **thực hiện OCR trên PDF** với đa ngôn ngữ, quét độ phân giải thấp, và tài liệu lớn.  
- Một mẫu mã hoàn chỉnh, có thể chạy ngay mà bạn có thể đưa vào bất kỳ dự án Java nào.

## Bước Tiếp Theo & Các Chủ Đề Liên Quan

Bây giờ bạn đã có thể **nhận dạng PDF đã quét**, hãy cân nhắc các ý tưởng tiếp theo sau:

- **Tạo PDF Tìm Kiếm Được** – chồng lại văn bản OCR lên PDF gốc để tạo tài liệu có thể tìm kiếm.  
- **Dịch Vụ Xử Lý Hàng Loạt** – gói mã vào một microservice Spring Boot nhận PDF qua REST.  
- **Tích Hợp với Elasticsearch** – lập chỉ mục văn bản đã trích xuất để tìm kiếm toàn văn nhanh chóng trong kho tài liệu của bạn.  
- **Tiền Xử Lý Hình Ảnh** – sử dụng OpenCV để chỉnh góc hoặc giảm nhiễu trang trước khi OCR, nâng cao độ chính xác hơn nữa.

Mỗi chủ đề này dựa trên các khái niệm cốt lõi mà chúng ta đã khám phá, vì vậy hãy tự do thử nghiệm và để engine OCR thực hiện phần việc nặng.

---

*Chúc lập trình vui vẻ! Nếu bạn gặp bất kỳ trục trặc nào — như lỗi giấy phép hoặc kết quả null không mong muốn — hãy để lại bình luận bên dưới. Tôi luôn sẵn sàng hỗ trợ gỡ lỗi.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}