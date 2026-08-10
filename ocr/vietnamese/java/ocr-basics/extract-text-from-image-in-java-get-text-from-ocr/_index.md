---
category: general
date: 2026-05-25
description: Trích xuất văn bản từ hình ảnh trong Java bằng OCR. Tìm hiểu cách tải
  hình ảnh cho OCR, nhận dạng văn bản từ ảnh và lấy văn bản từ OCR với một ví dụ mã
  đơn giản.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: vi
og_description: Trích xuất văn bản từ hình ảnh trong Java với hướng dẫn từng bước.
  Học cách tải hình ảnh cho OCR, nhận dạng văn bản từ ảnh và lấy văn bản từ OCR một
  cách hiệu quả.
og_title: Trích xuất văn bản từ hình ảnh trong Java – Lấy văn bản bằng OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Trích xuất văn bản từ hình ảnh trong Java – Lấy văn bản từ OCR
url: /vi/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất Văn bản từ Hình ảnh trong Java – Lấy Văn bản từ OCR

Bạn đã bao giờ cần **trích xuất văn bản từ hình ảnh** nhưng không chắc nên chọn thư viện Java nào? Bạn không cô đơn. Dù bạn đang số hoá biên lai, lấy số sê-ri từ ảnh sản phẩm, hay chỉ đơn giản là thử nghiệm một dự án phụ thú vị, việc chuyển một bức ảnh thành văn bản có thể chỉnh sửa là một rào cản phổ biến.

Trong tutorial này, chúng tôi sẽ hướng dẫn qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho bạn thấy cách **load image for OCR**, cấu hình engine, và cuối cùng **recognize text from photo** để bạn có thể **get text from OCR** chỉ với vài dòng code. Không có tham chiếu mơ hồ—mọi thứ bạn cần đều có ở đây.

## Những gì bạn sẽ học

* Cách thiết lập một engine OCR nhẹ trong Java.  
* Các bước chính xác để **load image for OCR** và xử lý các đường dẫn tệp khác nhau.  
* Tại sao việc cấu hình ngôn ngữ lại quan trọng khi bạn muốn **extract text from image** không phải tiếng Anh.  
* Cách xuất kết quả một cách an toàn và cách xử lý khi engine không trả về gì.  
* Một vài mẹo chuyên nghiệp để tránh những lỗi thường gặp nhất.

Kết thúc hướng dẫn này, bạn sẽ có một chương trình tự chứa có thể đọc file JPEG (hoặc PNG) chứa các ký tự tiếng Ukraina và in chuỗi đã nhận dạng ra console. Hãy thoải mái thay đổi ngôn ngữ hoặc hình ảnh—mọi thứ đều được mô-đun hoá.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: Flow diagram of extract text from image process in Java.*

## Yêu cầu trước

* **Java Development Kit (JDK) 11+** – code sử dụng hệ thống module hiện đại, nhưng các phiên bản cũ hơn cũng hoạt động với một vài chỉnh sửa nhỏ.  
* **Maven hoặc Gradle** – để tải thư viện OCR (chúng ta sẽ dùng **Asprise OCR** như một lựa chọn nhẹ, miễn phí cho phát triển).  
* Một file ảnh mẫu (ví dụ: `ukrainian_sign.jpg`) được đặt ở vị trí mà chương trình của bạn có thể đọc được.  
* Kiến thức cơ bản về phương thức `main` của Java và xử lý ngoại lệ.

Nếu bạn đã có những thứ này, bạn đã sẵn sàng. Nếu chưa, hãy tải JDK từ Oracle hoặc AdoptOpenJDK và thiết lập một dự án Maven đơn giản—không cần gì phức tạp.

---

## Bước 1: Thêm Dependency OCR

Đầu tiên, thông báo cho công cụ build của bạn tải engine OCR. Đối với Maven, chèn đoạn này vào `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Nếu bạn thích Gradle, tương đương là:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Các coordinates này sẽ tải một JAR gọn gàng bao gồm `OcrEngine`, `OcrLanguage`, và các lớp trợ giúp mà chúng ta sẽ dùng. Không cần binary gốc bổ sung cho các script Latin và Cyrillic cơ bản.

---

## Bước 2: Tạo lớp Java để **Extract Text from Image**

Bây giờ chúng ta sẽ viết chương trình thực tế. Lưu đoạn sau dưới tên `ExtractTextDemo.java` trong `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Tại sao cấu trúc này hoạt động

* **Các khối được đánh số riêng** giúp luồng thực hiện dễ theo dõi, đặc biệt khi bạn đang tìm nơi **load image for OCR** hoặc **recognize text from photo**.  
* Khối `try/catch` quanh việc tải ảnh và nhận dạng đảm bảo chương trình thất bại một cách nhẹ nhàng—hữu ích khi đường dẫn file sai hoặc engine OCR không tìm thấy dữ liệu ngôn ngữ.  
* Đặt ngôn ngữ sớm (bước 2) cải thiện đáng kể độ chính xác cho các script không phải tiếng Anh. Nếu sau này bạn cần **java image to text** cho ngôn ngữ khác, chỉ cần thay `OcrLanguage.UKRAINIAN` bằng `OcrLanguage.ENGLISH`, `FRENCH`, v.v.

---

## Bước 3: Biên dịch và Chạy Chương trình

Từ thư mục gốc của dự án, thực hiện:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Hoặc, nếu bạn dùng Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Giả sử `ukrainian_sign.jpg` chứa văn bản *«Ласкаво просимо»* (tiếng Ukraina có nghĩa “Welcome”), bạn sẽ thấy đầu ra tương tự:

```
=== OCR Result ===
Ласкаво просимо
```

Đầu ra này xác nhận bạn đã **extract text from image** và **get text from OCR** thành công trong một lần chạy.

---

## Bước 4: Điều chỉnh Quy trình – Từ **Java Image to Text** trong Dự án Thực tế

Mặc dù demo này tối giản, các ứng dụng thực tế thường cần một vài bổ sung:

| Scenario | What to Adjust | Reason |
|----------|----------------|--------|
| **Batch processing** | Loop over a `List<Path>` and store each result in a database. | Giảm công việc thủ công khi bạn có hàng trăm bức ảnh. |
| **Different image formats** | Use `ImageIO.read(new File(path))` to pre‑process, then pass the `BufferedImage` to `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Xử lý PNG, BMP, hoặc thậm chí PDF sau khi chuyển đổi. |
| **Performance tuning** | Call `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)` if you’re okay with slightly lower accuracy. | Tăng tốc nhận dạng trên phần cứng yếu. |
| **Post‑processing** | Trim whitespace, replace common OCR mis‑reads (`0` → `O`, `1` → `I`). | Cải thiện chất lượng dữ liệu downstream. |

Những biến thể này giữ nguyên ý tưởng cốt lõi—**recognize text from photo**—trong khi cung cấp sự linh hoạt cho các khối lượng công việc sản xuất.

---

## Những Sai Lầm Thường Gặp & Mẹo Chuyên Nghiệp

1. **Cài đặt ngôn ngữ sai** – Nếu bạn bỏ qua bước 2, engine sẽ mặc định tiếng Anh, biến các ký tự Cyrillic thành mớ chữ vô nghĩa. Luôn kiểm tra lại mã ngôn ngữ.  
2. **Chất lượng ảnh quan trọng** – Ảnh độ phân giải thấp hoặc mờ sẽ làm giảm độ chính xác. Tiền xử lý bằng tăng độ tương phản hoặc nhị phân hoá nếu cần.  
3. **Quirks đường dẫn file** – Trên Windows, dấu gạch chéo ngược cần escape (`C:\\images\\file.jpg`). Sử dụng `Path.of(...)` từ `java.nio.file` sẽ tránh vấn đề này.  
4. **Rò rỉ bộ nhớ** – `OcrEngine` giữ tài nguyên gốc. Gọi `ocrEngine.dispose()` khi hoàn thành, đặc biệt trong các dịch vụ chạy lâu.  
5. **An toàn đa luồng** – Engine không thread‑safe theo mặc định. Tạo một instance riêng cho mỗi luồng hoặc đồng bộ hoá truy cập.

---

## Ví dụ Hoàn chỉnh (Tất cả trong Một File)

Dưới đây là một file duy nhất bạn có thể copy‑paste vào bất kỳ IDE nào. Nó bao gồm lời gọi `dispose()` và một phương thức trợ giúp nhỏ để làm code gọn hơn.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Chạy chương trình này sẽ cho ra cùng một đầu ra console như đã trình bày ở trên. Bạn có thể thay `OcrLanguage.UKRAINIAN` bằng `OcrLanguage.ENGLISH` hoặc bất kỳ ngôn ngữ hỗ trợ nào khác để xem engine thích nghi như thế nào.

---

## Kết luận

Chúng ta đã đi qua mọi thứ bạn cần để **extract text from image** bằng Java: từ việc thêm dependency OCR, đến **load image for OCR**,  

## Các Tutorial Liên quan

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}