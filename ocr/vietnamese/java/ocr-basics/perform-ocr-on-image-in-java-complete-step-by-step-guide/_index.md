---
category: general
date: 2026-06-16
description: Học cách thực hiện OCR trên các tệp hình ảnh trong Java. Hướng dẫn này
  bao gồm nhận dạng văn bản từ PNG, trích xuất văn bản từ hình ảnh, chuyển đổi hình
  ảnh thành văn bản và tải hình ảnh cho OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: vi
og_description: Thực hiện OCR trên hình ảnh bằng Java. Hướng dẫn này chỉ cách nhận
  dạng văn bản từ PNG, trích xuất văn bản từ hình ảnh và chuyển đổi hình ảnh thành
  văn bản với một ví dụ sẵn sàng chạy.
og_title: Thực hiện OCR trên hình ảnh bằng Java – Hướng dẫn lập trình đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Thực hiện OCR trên hình ảnh trong Java – Hướng dẫn chi tiết từng bước
url: /vi/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Thực hiện OCR trên hình ảnh trong Java – Hướng dẫn chi tiết từng bước

Bạn đã bao giờ cần **perform OCR on image** trên các tệp hình ảnh nhưng không chắc thư viện Java nào nên chọn? Bạn không đơn độc. Cho dù bạn đang xây dựng một trình quét biên lai, một hệ thống lưu trữ tài liệu, hay chỉ tò mò về việc chuyển ảnh thành văn bản có thể tìm kiếm, việc học cách **perform OCR on image** với Java là một kỹ năng hữu ích.

Trong hướng dẫn này, chúng tôi sẽ đi qua mọi thứ bạn cần để **perform OCR on image** các tệp: tải hình ảnh, cấu hình engine, nhận dạng văn bản và cuối cùng in kết quả. Khi kết thúc, bạn sẽ có thể **recognize text from PNG** các tệp, **extract text from image** nguồn, và **convert image to text** chỉ với vài dòng mã.

## Yêu cầu trước

- Java 17 hoặc mới hơn (mã sẽ biên dịch với bất kỳ JDK gần đây nào)
- Maven đã cài đặt (hoặc công cụ xây dựng yêu thích của bạn)
- Kiến thức cơ bản về cú pháp Java
- Một tệp PNG bạn muốn thử (chúng tôi sẽ gọi nó là `hello.png`)

> **Mẹo chuyên nghiệp:** Nếu bạn không có sẵn tệp PNG, hãy tạo một tệp bằng cách chụp màn hình bất kỳ văn bản nào và lưu nó dưới tên `hello.png` trong thư mục có tên `resources`.

## Những gì chúng ta sẽ xây dựng

Một ứng dụng console nhỏ tên `OcrDemo` thực hiện:

1. **Loads image for OCR** – đọc một tệp PNG từ đĩa.
2. **Performs OCR on image** – sử dụng engine Tesseract qua Tess4J.
3. **Extracts text from image** – trả về một `String` chứa nội dung đã nhận dạng.
4. In kết quả ra console.

Hãy bắt đầu.

## Bước 1: Thiết lập dự án và thêm Tess4J

Đầu tiên, tạo một dự án Maven mới (hoặc Gradle nếu bạn thích). Thêm phụ thuộc Tess4J, nó bao bọc engine Tesseract OCR phổ biến.

```xml
<!-- pom.xml -->
<project>
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

> **Tại sao lại là Tess4J?** Nó được duy trì tích cực, hoạt động đa nền tảng và cung cấp cho bạn một API Java sạch sẽ cho các nhiệm vụ **perform OCR on image**.

## Bước 2: Chuẩn bị logic tải hình ảnh

Bây giờ chúng ta sẽ viết một phương thức trợ giúp để **load image for OCR**. Phương thức này sử dụng `ImageIO` của Java để đọc một PNG vào `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Lưu ý tên phương thức rõ ràng phản ánh ý định **load image for OCR**, giúp mã tự mô tả.

## Bước 3: Cấu hình engine OCR để **Perform OCR on Image**

Với hình ảnh đã sẵn sàng, chúng ta tạo một thể hiện `Tesseract`, bật phát hiện ngôn ngữ tự động và gọi `doOCR`. Đây là phần cốt lõi của cách chúng ta **perform OCR on image** dữ liệu.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Tại sao bật tự động phát hiện?** Nó cho phép engine chọn mô hình ngôn ngữ tốt nhất cho hình ảnh, rất hữu ích khi bạn **convert image to text** từ các nguồn có hỗn hợp tiếng Anh và các chữ viết khác.

## Bước 4: Kết hợp tất cả – Ứng dụng chính

Đây là điểm vào mà **recognize text from PNG**, **extract text from image**, và cuối cùng in kết quả. Đây là ví dụ đầy đủ, có thể chạy được.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Kết quả mong đợi

Nếu `hello.png` chứa cụm từ “Hello, OCR world!”, console sẽ hiển thị gì đó như sau:

```
=== Recognized Text ===
Hello, OCR world!
```

Kết quả chính xác có thể hơi khác nhau tùy vào chất lượng hình ảnh, nhưng bạn sẽ thấy văn bản bạn đã đặt trong PNG.

## Bước 5: Xử lý các trường hợp biên thường gặp

### 5.1 Xử lý hình ảnh độ phân giải thấp

Nếu PNG nguồn mờ, độ chính xác OCR giảm. Một cách nhanh là tăng kích thước hình ảnh trước khi đưa vào engine:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Gọi `upscale(image, 2)` trước `engine.recognize(image)` để cải thiện kết quả.

### 5.2 Tài liệu đa ngôn ngữ

Nếu bạn dự đoán có văn bản tiếng Pháp hoặc tiếng Đức, chỉ cần thêm mã ngôn ngữ vào `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Engine sẽ cố gắng **extract text from image** bằng cách sử dụng các mô hình ngôn ngữ kết hợp.

### 5.3 Bỏ qua các trang trống

Đôi khi một trang PDF đã quét hiển thị dưới dạng PNG trống. Phát hiện hình ảnh trống giúp tiết kiệm thời gian xử lý:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Bước 6: Đóng gói và chạy ứng dụng

1. **Compile:** `mvn clean compile`
2. **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Đảm bảo thư mục `tessdata` (chứa các tệp ngôn ngữ) nằm cạnh JAR đã biên dịch hoặc chỉ định đường dẫn tuyệt đối trong `OcrEngine`.

## Kết luận

Bạn giờ đã có một mẫu vững chắc, sẵn sàng cho sản xuất để **perform OCR on image** các tệp bằng Java. Từ **loading image for OCR** đến **recognize text from PNG**, chúng tôi đã đề cập cách **extract text from image**, **convert image to text**, và xử lý các tình huống khó như quét độ phân giải thấp hoặc nội dung đa ngôn ngữ.

Tiếp theo, bạn có thể khám phá:

- **Batch processing** – lặp qua một thư mục các PNG và ghi mỗi kết quả vào tệp `.txt`.
- **PDF generation** – nhúng văn bản đã trích xuất trở lại vào PDF có thể tìm kiếm.
- **Cloud OCR services** – so sánh hiệu năng Tesseract cục bộ với các API như Google Vision hoặc Azure Cognitive Services.

Hãy thoải mái thử nghiệm, điều chỉnh các tham số và chia sẻ kết quả của bạn. Chúc lập trình vui vẻ, và mong hình ảnh của bạn luôn chuyển thành văn bản sạch sẽ, có thể tìm kiếm!

![Diagram showing the OCR workflow to perform OCR on image](https://example.com/ocr-workflow.png "perform OCR on image example")

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn thành thạo các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [nhận dạng văn bản hình ảnh với Aspose OCR – Hướng dẫn OCR Java đầy đủ](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Chuyển hình ảnh thành văn bản trong Java bằng Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Trích xuất văn bản từ hình ảnh Java với Aspose.OCR chế độ phát hiện vùng](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}