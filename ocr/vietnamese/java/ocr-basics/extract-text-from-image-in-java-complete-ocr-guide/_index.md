---
category: general
date: 2026-07-21
description: Trích xuất văn bản từ hình ảnh bằng Java OCR. Tìm hiểu cách chuyển đổi
  PNG sang văn bản, đọc văn bản từ PNG, tải hình ảnh cho OCR và thực hiện OCR trên
  hình ảnh chỉ trong vài bước.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: vi
lastmod: 2026-07-21
og_description: Trích xuất văn bản từ hình ảnh bằng Java. Hướng dẫn này chỉ cho bạn
  cách chuyển đổi PNG sang văn bản, đọc văn bản từ PNG, tải hình ảnh cho OCR và thực
  hiện OCR trên hình ảnh một cách hiệu quả.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Trích xuất văn bản từ hình ảnh trong Java – Hướng dẫn OCR từng bước
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Trích xuất văn bản từ hình ảnh trong Java – Hướng dẫn OCR toàn diện
url: /vi/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong Java – Hướng dẫn OCR toàn diện

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không chắc thư viện Java nào phù hợp? Bạn không đơn độc. Dù bạn đang số hoá biên lai, quét PDF, hay xây dựng một kho lưu trữ có thể tìm kiếm, việc lấy văn bản ra từ file PNG là một vấn đề thường gặp đối với nhiều lập trình viên.

Trong tutorial này, chúng ta sẽ thực hiện một giải pháp thực tế cho phép bạn **chuyển đổi PNG sang văn bản**, **đọc văn bản từ PNG**, **tải hình ảnh cho OCR**, và **thực hiện OCR trên hình ảnh**—tất cả chỉ với vài dòng mã Java sạch sẽ. Khi hoàn thành, bạn sẽ có một chương trình có thể chạy được và dễ dàng tích hợp vào bất kỳ dự án nào.

## Những gì bạn sẽ xây dựng

Chúng ta sẽ tạo một ứng dụng console Java nhỏ gọn có các chức năng:

1. Tải một file PNG từ đĩa.  
2. Gửi hình ảnh tới engine OCR (Tess4J, một wrapper Java cho Tesseract).  
3. In ra văn bản đã nhận dạng lên console.

Không có dịch vụ bên ngoài, không có phép màu—chỉ thuần Java và một engine OCR mã nguồn mở.

## Điều kiện tiên quyết

- **Java 17** trở lên (mã có thể biên dịch với các phiên bản cũ hơn, nhưng Java 17 cung cấp các tính năng ngôn ngữ mới nhất).  
- **Maven** hoặc **Gradle** để quản lý phụ thuộc.  
- Một file PNG mẫu có tên `sample.png` đặt trong thư mục bạn có thể tham chiếu (ví dụ: `src/main/resources`).  
- Kiến thức cơ bản về phương thức `main` của Java và xử lý ngoại lệ.

Nếu bất kỳ mục nào trên còn lạ, đừng lo—mỗi bước đều có phần tóm tắt nhanh.

## Bước 1: Thiết lập Dự án và Thêm Thư viện OCR

Đầu tiên, tạo một dự án Maven mới (hoặc Gradle nếu bạn thích). Thêm phụ thuộc Tess4J, thư viện sẽ tự tải các binary của Tesseract cho bạn.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Mẹo:** Nếu bạn dùng Gradle, dòng tương đương là `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Thêm thư viện này sẽ cung cấp lớp `Tesseract`, chịu trách nhiệm **thực hiện OCR trên hình ảnh**.

## Bước 2: Tải Hình ảnh cho OCR

Bây giờ chúng ta cần **tải hình ảnh cho OCR**. Tess4J làm việc với `java.awt.image.BufferedImage`, vì vậy chúng ta sẽ đọc PNG bằng `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Phương thức trên tách riêng logic **tải hình ảnh cho OCR**, giúp phần còn lại của mã dễ kiểm thử hơn. Lưu ý chú thích – nó phản ánh đoạn mã gốc đồng thời mở rộng để rõ ràng hơn.

## Bước 3: Thực hiện OCR trên Hình ảnh

Với hình ảnh đã có trong bộ nhớ, chúng ta có thể **thực hiện OCR trên hình ảnh**. Đối tượng `Tesseract` là engine của chúng ta; chúng ta sẽ cấu hình nó sử dụng dữ liệu ngôn ngữ tiếng Anh mặc định đi kèm với Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Ở đây chúng tôi đã gộp “Bước 1” và “Bước 4” gốc thành một phương thức duy nhất, vì việc tạo đối tượng `Tesseract` không tốn kém và giúp mã ngắn gọn hơn. Chú thích vẫn đề cập tới các bước gốc để dễ truy vết.

## Bước 4: Kết hợp Tất cả – Phương thức main

Cuối cùng, chúng ta đưa mọi thứ lại với nhau trong `main`. Đây là nơi bạn sẽ **đọc văn bản từ PNG** và xem kết quả được in ra console.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Khi chạy `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (hoặc lệnh tương đương của Gradle), bạn sẽ thấy đầu ra giống như:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Kết quả này chứng minh bạn đã **trích xuất văn bản từ hình ảnh**, **chuyển đổi PNG sang văn bản**, và **đọc văn bản từ PNG** trong một chương trình gọn gàng.

## Xử lý Các Trường hợp Thường gặp

### Hình ảnh Chất lượng Thấp

Nếu PNG bị mờ hoặc độ tương phản thấp, độ chính xác OCR sẽ giảm. Một cách khắc phục nhanh là tiền xử lý hình ảnh:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Hỗ trợ Đa Ngôn ngữ

Tess4J có thể xử lý nhiều ngôn ngữ. Chỉ cần tải file `.traineddata` phù hợp và đặt `tesseract.setLanguage("spa")` cho tiếng Tây Ban Nha, ví dụ.

### PDF Lớn hoặc Hình ảnh Nhiều Trang

Nếu bạn cần **trích xuất văn bản từ hình ảnh** nằm trong PDF, hãy tách mỗi trang thành PNG (sử dụng PDFBox) rồi đưa từng PNG vào quy trình OCR như trên.

## Ví dụ Hoàn chỉnh (Tất cả Mã trong Một File)

Dưới đây là lớp Java hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán vào `src/main/java/com/example/ocrdemo/OcrDemo.java` và bạn đã sẵn sàng.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Chạy lớp này sẽ in ra kết quả OCR, xác nhận bạn đã **thực hiện OCR trên hình ảnh** và biến PNG thành văn bản có thể chỉnh sửa.

## Tổng kết & Các Bước Tiếp Theo

Chúng ta đã bắt đầu bằng việc **trích xuất văn bản từ hình ảnh** bằng một môi trường Java nhẹ. Bây giờ bạn đã biết cách **tải hình ảnh cho OCR**, **thực hiện OCR trên hình ảnh**, và **đọc văn bản từ PNG**—những khối xây dựng thiết yếu cho bất kỳ quy trình số hoá tài liệu nào.

Muốn tiến xa hơn? Hãy thử các ý tưởng sau:

- **Xử lý hàng loạt:** Duyệt qua một thư mục PNG và ghi mỗi kết quả vào file `.txt`.  
- **Tích hợp với cơ sở dữ liệu:** Lưu trữ các chuỗi đã trích xuất cùng metadata để tạo kho lưu trữ có thể tìm kiếm.  
- **Kết hợp với NLP:** Đưa đầu ra OCR vào mô hình phân tích cảm xúc để nhanh chóng rút ra thông tin.  

Mỗi mở rộng đều dựa trên các khái niệm cốt lõi mà chúng ta đã học, vì vậy bạn đã sẵn sàng để thử nghiệm.

---

*Chúc lập trình vui vẻ! Nếu gặp bất kỳ khó khăn nào*


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ cùng các giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}