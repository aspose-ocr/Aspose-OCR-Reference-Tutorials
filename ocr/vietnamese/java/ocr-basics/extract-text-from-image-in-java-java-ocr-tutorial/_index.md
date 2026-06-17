---
category: general
date: 2026-03-07
description: Trích xuất văn bản từ hình ảnh bằng Java OCR. Tìm hiểu cách tải hình
  ảnh cho OCR, cấu hình ngôn ngữ và thực hiện một hướng dẫn Java OCR đầy đủ trong
  vài phút.
draft: false
keywords:
- extract text from image
- load image for ocr
- use OCR in java
- java ocr tutorial
language: vi
og_description: Trích xuất văn bản từ hình ảnh bằng Java OCR. Hướng dẫn này chỉ cách
  tải hình ảnh cho OCR, cấu hình ngôn ngữ và thực hiện tutorial Java OCR từng bước.
og_title: Trích xuất văn bản từ hình ảnh trong Java – Hướng dẫn OCR toàn diện
tags:
- OCR
- Java
- Image Processing
title: Trích xuất văn bản từ hình ảnh trong Java – Hướng dẫn OCR Java
url: /vi/java/ocr-basics/extract-text-from-image-in-java-java-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong Java – Hướng dẫn OCR toàn diện

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không chắc bắt đầu từ đâu trong Java? Bạn không phải là người duy nhất—các nhà phát triển thường gặp khó khăn này khi chuyển các biển hiệu, biên lai hoặc ghi chú viết tay đã quét thành các chuỗi có thể tìm kiếm.  

Tin tốt? Chỉ trong vài phút, bạn có thể có một pipeline OCR hoạt động, có khả năng đọc Kannada, tiếng Anh hoặc bất kỳ ngôn ngữ nào được hỗ trợ. Trong hướng dẫn này, chúng tôi sẽ **tải hình ảnh cho OCR**, cấu hình engine, và đi qua một **hướng dẫn OCR Java** mà bạn có thể sao chép‑dán và chạy ngay hôm nay.

## Những gì Hướng dẫn này Bao gồm

Chúng tôi sẽ bắt đầu bằng cách liệt kê các công cụ bạn cần, sau đó ngay lập tức thực hiện một triển khai **bước‑bước**. Khi kết thúc, bạn sẽ có thể:

* Tải một tệp hình ảnh vào `ImageInputStream` của Java.
* Cấu hình một engine OCR để nhận dạng một ngôn ngữ cụ thể (Kannada trong ví dụ của chúng tôi).
* Chạy quá trình nhận dạng và in ra văn bản đã trích xuất.
* Tinh chỉnh cài đặt để tăng độ chính xác và xử lý các lỗi thường gặp.

Không cần tài liệu bên ngoài—mọi thứ bạn cần đều có ở đây.  

**Yêu cầu trước**: Java 17 hoặc mới hơn, công cụ xây dựng như Maven hoặc Gradle, và một thư viện OCR cung cấp lớp `OcrEngine` (ví dụ, SDK *SimpleOCR* giả định). Nếu bạn dùng Maven, thêm phụ thuộc như được hiển thị phía sau.

---

## Bước 1 – Thiết lập Dự án và Thêm Thư viện OCR

Trước khi viết bất kỳ mã nào, hãy chắc chắn dự án của bạn có thể nhìn thấy các lớp OCR. Với Maven, chèn đoạn mã này vào `pom.xml` của bạn:

```xml
<!-- Maven dependency for SimpleOCR (replace with your actual OCR SDK) -->
<dependency>
    <groupId>com.example</groupId>
    <artifactId>simple-ocr</artifactId>
    <version>1.4.2</version>
</dependency>
```

Nếu bạn thích Gradle, tương đương là:

```gradle
implementation 'com.example:simple-ocr:1.4.2'
```

> **Mẹo chuyên nghiệp:** Giữ phiên bản thư viện luôn cập nhật; các bản phát hành mới thường bao gồm cải tiến mô hình ngôn ngữ giúp tăng độ chính xác.

Khi phụ thuộc đã được giải quyết, làm mới IDE của bạn và bạn đã sẵn sàng để viết mã.

## Bước 2 – Nhập các Lớp Cần Thiết

Dưới đây là danh sách đầy đủ các import bạn sẽ cần cho ví dụ. Chúng được giữ tối giản để bạn có thể thấy chính xác mỗi lớp làm gì.

```java
import com.example.ocr.OcrEngine;      // Main OCR engine
import com.example.ocr.OcrResult;      // Holds recognition result
import com.example.io.ImageInputStream; // Wrapper for image files
import java.nio.file.Paths;             // Convenient path handling
import java.io.IOException;             // For proper exception handling
```

> **Tại sao lại import những thứ này?** `OcrEngine` và `OcrResult` là trái tim của quá trình OCR, trong khi `ImageInputStream` trừu tượng hoá phần đọc file. Sử dụng `java.nio.file.Paths` giúp mã không phụ thuộc vào hệ điều hành.

## Bước 3 – Tải Hình ảnh cho OCR

Bây giờ là phần thường làm người dùng bối rối: cung cấp định dạng hình ảnh đúng cho engine. SDK OCR yêu cầu một `ImageInputStream`, mà bạn có thể lấy từ bất kỳ tệp nào trên đĩa.

```java
// Step 3: Load the image that contains the text you want to extract
String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));
```

> **Trường hợp biên:** Nếu hình ảnh bị hỏng hoặc ở định dạng không được hỗ trợ (ví dụ, GIF), hàm khởi tạo sẽ ném `IOException`. Hãy bao quanh lời gọi bằng khối try‑catch hoặc kiểm tra tệp trước.

## Bước 4 – Cấu hình Engine để Nhận dạng Ngôn ngữ Cụ thể

Hầu hết các engine OCR đều hỗ trợ đa ngôn ngữ. Để cải thiện độ chính xác, bạn nên cho engine biết chính xác ngôn ngữ cần nhận dạng. Trong trường hợp của chúng tôi, chúng tôi dùng mã ngôn ngữ `"kn"` cho Kannada.

```java
// Step 4: Create and configure the OCR engine for Kannada
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setLanguage("kn"); // 'kn' = Kannada
```

> **Tại sao phải đặt ngôn ngữ?** Giới hạn bộ ký tự giúp giảm các kết quả sai, đặc biệt khi làm việc với các chữ viết có nhiều glyph tương tự.

Nếu bạn cần chuyển đổi ngôn ngữ, chỉ cần thay đổi chuỗi mã—không cần thay đổi gì khác.

## Bước 5 – Chạy Quy trình OCR và Trích xuất Văn bản

Với hình ảnh đã được tải và engine đã được cấu hình, việc nhận dạng thực tế chỉ là một lời gọi phương thức. Đối tượng kết quả cung cấp cho bạn văn bản thuần và, tùy chọn, điểm tin cậy.

```java
// Step 5: Run OCR and retrieve the recognized text
OcrResult ocrResult = ocrEngine.recognize(imageStream);
String extractedText = ocrResult.getText();
```

> **Câu hỏi thường gặp:** *Nếu OCR trả về một chuỗi rỗng thì sao?*  
> Thông thường điều này có nghĩa là chất lượng hình ảnh quá thấp (mờ, độ tương phản thấp) hoặc ngôn ngữ chưa được đặt đúng. Hãy thử tiền xử lý hình ảnh (tăng độ tương phản, nhị phân hoá) hoặc kiểm tra lại mã ngôn ngữ.

## Bước 6 – Hiển thị Kết quả

Cuối cùng, in kết quả ra console. Trong một ứng dụng thực tế, bạn có thể lưu nó vào cơ sở dữ liệu hoặc đưa vào chỉ mục tìm kiếm.

```java
// Step 6: Output the recognized Kannada text
System.out.println("Extracted text:");
System.out.println(extractedText);
```

### Kết quả Dự kiến

Nếu hình ảnh nguồn chứa cụm từ Kannada “ಕರ್ನಾಟಕ” (Karnataka), console sẽ hiển thị:

```
Extracted text:
ಕರ್ನಾಟಕ
```

Xong rồi—một quy trình **sử dụng OCR trong Java** hoàn chỉnh mà bạn có thể điều chỉnh cho bất kỳ ngôn ngữ hoặc nguồn hình ảnh nào.

---

## Ví dụ Hoạt động Đầy đủ

Dưới đây là toàn bộ chương trình, sẵn sàng biên dịch. Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế tới tệp hình ảnh của bạn.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrResult;
import com.example.io.ImageInputStream;
import java.nio.file.Paths;
import java.io.IOException;

public class KannadaOcrExample {
    public static void main(String[] args) {
        try {
            // Create OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();

            // Configure for Kannada (language code "kn")
            ocrEngine.getConfig().setLanguage("kn");

            // Load the image you want to extract text from
            String imagePath = "YOUR_DIRECTORY/kannada_sign.jpg";
            ImageInputStream imageStream = new ImageInputStream(Paths.get(imagePath));

            // Run the OCR process
            OcrResult ocrResult = ocrEngine.recognize(imageStream);

            // Print the extracted text
            System.out.println("Extracted text:");
            System.out.println(ocrResult.getText());
        } catch (IOException e) {
            System.err.println("Failed to load image or run OCR: " + e.getMessage());
        } catch (Exception e) {
            System.err.println("Unexpected error during OCR: " + e.getMessage());
        }
    }
}
```

> **Mẹo:** Đối với mã sản xuất, hãy cân nhắc tái sử dụng một thể hiện `OcrEngine` duy nhất cho nhiều hình ảnh; việc tạo lại liên tục có thể tốn kém.

---

## Câu hỏi Thường gặp & Trường hợp Biên

### Làm sao cải thiện độ chính xác trên ảnh nhiễu?

- **Tiền xử lý** hình ảnh: chuyển sang thang xám, áp dụng lọc trung vị, hoặc tăng độ tương phản.  
- **Thay đổi kích thước** hình ảnh ít nhất 300 DPI; hầu hết các engine OCR yêu cầu độ phân giải này.  
- **Đặt danh sách trắng** các ký tự nếu bạn biết đầu ra mong muốn (ví dụ, chỉ số).

### Tôi có thể dùng cách này cho PDF không?

Có. Trích xuất mỗi trang thành hình ảnh (sử dụng PDFBox hoặc iText), sau đó đưa các hình ảnh đó vào cùng pipeline. Mã vẫn giống nhau; chỉ nguồn hình ảnh thay đổi.

### Nếu tôi cần nhận dạng nhiều ngôn ngữ trong một hình ảnh thì sao?

Hầu hết các SDK cho phép bạn truyền danh sách ngăn cách bằng dấu phẩy, như `"en,kn"`. Engine sẽ cố gắng khớp với bất kỳ script nào trong danh sách.

### Có cách nào để lấy điểm tin cậy không?

`OcrResult` thường bao gồm phương thức `getConfidence()` trả về một float từ 0 đến 1 cho mỗi dòng. Sử dụng nó để lọc các kết quả có độ tin cậy thấp.

---

## Bước Tiếp theo

Bây giờ bạn đã có thể **trích xuất văn bản từ hình ảnh** bằng Java, bạn có thể khám phá:

* **Xử lý hàng loạt** – lặp qua một thư mục hình ảnh và ghi kết quả vào CSV.  
* **Tích hợp với Apache Tika** – kết hợp OCR với việc phân tích tài liệu để tạo chỉ mục tìm kiếm thống nhất.  
* **API phía máy chủ** – cung cấp logic OCR qua endpoint REST (Spring Boot làm cho việc này đơn giản).  
* **Thư viện thay thế** – thử Tesseract qua `tess4j` nếu bạn cần giải pháp mã nguồn mở.  

Mỗi chủ đề này dựa trên các khái niệm cốt lõi trong **hướng dẫn OCR java** này, vì vậy hãy tự do thử nghiệm và mở rộng mã.

---

## Kết luận

Chúng tôi đã đi qua một ví dụ Java hoàn chỉnh mà **trích xuất văn bản từ hình ảnh**, cho thấy chính xác cách **tải hình ảnh cho OCR**, cấu hình cài đặt ngôn ngữ, và **sử dụng OCR trong Java** để lấy các chuỗi có thể đọc được. Đoạn mã tự chứa, xử lý lỗi một cách nhẹ nhàng, và có thể được chèn vào bất kỳ dự án Java nào mà không gặp rắc rối.  

Hãy thử nghiệm, điều chỉnh mã ngôn ngữ, và sớm bạn sẽ biến các tài liệu đã quét thành dữ liệu có thể tìm kiếm mà không hề khó khăn. Chúc lập trình vui!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}