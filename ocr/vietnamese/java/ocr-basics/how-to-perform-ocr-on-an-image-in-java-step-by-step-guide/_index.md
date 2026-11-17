---
category: general
date: 2026-11-17
description: Tìm hiểu cách thực hiện OCR trên hình ảnh trong Java và trích xuất văn
  bản từ ảnh bằng một ví dụ mã đơn giản. Bao gồm các mẹo đọc ảnh trong Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: vi
lastmod: 2026-11-17
og_description: Cách thực hiện OCR trên hình ảnh trong Java và trích xuất văn bản
  nhanh chóng. Hãy theo hướng dẫn này để đọc hình ảnh bằng Java và chuyển đổi hình
  ảnh thành văn bản với một ví dụ đã sẵn sàng chạy.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Cách thực hiện OCR trên hình ảnh trong Java – hướng dẫn từng bước
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Cách thực hiện OCR trên hình ảnh trong Java – hướng dẫn từng bước
url: /vi/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR trên hình ảnh trong Java – hướng dẫn từng bước

Nếu bạn cần **cách thực hiện OCR** trên một bức ảnh, hướng dẫn này sẽ cho bạn một giải pháp hoàn chỉnh, có thể chạy được trong Java. Bạn sẽ thấy cách đọc file ảnh, cấu hình engine OCR và trích xuất văn bản mà engine nhận dạng.

Làm việc với tài liệu đã quét, biên lai hoặc ảnh chụp màn hình thường đòi hỏi chuyển đổi nội dung hình ảnh thành văn bản có thể tìm kiếm. Hướng dẫn này sẽ dẫn bạn qua mọi bước, từ tải ảnh đến in ra văn bản đã trích xuất, đồng thời đề cập đến các vấn đề thường gặp như định dạng file không được hỗ trợ và kết quả null.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn có:

* Java Development Kit (JDK) 8 hoặc mới hơn đã được cài đặt.
* Công cụ xây dựng (Maven hoặc Gradle) để tải thư viện OCR.
* Một file ảnh (JPEG, PNG, BMP) mà bạn muốn xử lý.

Mã nguồn sử dụng **thư viện OCR từ gói `com.asprise.ocr`** vì nó chỉ cần một JAR duy nhất và hoạt động trên mọi nền tảng chính. Bạn có thể thay thế bằng nhà cung cấp khác (Tesseract, Google Vision, v.v.) bằng cách đổi các câu lệnh import và mã khởi tạo engine.

## Bước 1: Thêm phụ thuộc OCR

Nếu bạn dùng Maven, thêm phụ thuộc sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Đối với Gradle, đặt dòng này trong `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Các dòng này đảm bảo rằng mã **read image Java** có thể biên dịch và engine OCR sẽ có sẵn tại thời gian chạy.

## Bước 2: Đọc ảnh bằng Java

Đọc một file ảnh là bước cụ thể đầu tiên trong bất kỳ quy trình **extract text image** nào. Lớp `ImageIO` tích hợp sẵn của Java xử lý hầu hết các định dạng phổ biến.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Tại sao điều này quan trọng:** `ImageIO.read` trả về `null` đối với các định dạng không được hỗ trợ hoặc file bị hỏng. Phương thức trên ghi lại vấn đề và trả về `null` để bước tiếp theo có thể xử lý một cách mềm dẻo.

## Bước 3: Tạo và cấu hình engine OCR

Engine OCR cần biết ngôn ngữ nào sẽ được nhận dạng. Đặt ngôn ngữ sẽ cải thiện độ chính xác đáng kể, đặc biệt với các tài liệu không phải tiếng Anh.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Tại sao điều này quan trọng:** Khởi động engine là một thao tác tương đối nặng, vì vậy bạn nên tạo một lần và tái sử dụng cho nhiều ảnh nếu ứng dụng của bạn xử lý hàng loạt.

## Bước 4: Thực hiện OCR và chuyển đổi ảnh thành văn bản

Khi ảnh đã được tải và engine đã sẵn sàng, bạn có thể chạy bước nhận dạng. Đây là phần cốt lõi của **cách thực hiện OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Xử lý trường hợp biên:** Nếu ảnh là `null`, phương thức trả về một chuỗi rỗng thay vì ném `NullPointerException`. Điều này làm cho mã xung quanh trở nên vững chắc hơn khi làm việc với các file do người dùng cung cấp.

## Bước 5: Hiển thị văn bản đã trích xuất

Cuối cùng, in kết quả ra console hoặc chuyển nó tới thành phần khác (ví dụ: cơ sở dữ liệu hoặc widget UI).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Khi bạn chạy chương trình với `java OcrDemo sample.jpg`, console sẽ hiển thị các ký tự đã được nhận dạng. Điều này hoàn thành chu trình **convert image to text**.

### Kết quả mong đợi

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Nếu ảnh không chứa ký tự nào có thể đọc được, chương trình sẽ in `(no text detected)`.

## Các biến thể phổ biến và cách điều chỉnh chúng

| Biến thể | Thay đổi gì | Khi nào sử dụng |
|-----------|--------------|-----------------|
| **Ngôn ngữ khác** | Thay `"eng"` bằng `"spa"` cho tiếng Tây Ban Nha, `"fra"` cho tiếng Pháp, v.v. | Tài liệu viết bằng ngôn ngữ không phải tiếng Anh |
| **Xử lý hàng loạt** | Lặp qua danh sách các đường dẫn file, tái sử dụng cùng một instance `Ocr`. | Tập hợp lớn các trang đã quét |
| **Độ chính xác cao hơn** | Dùng `Ocr.SPEED_SLOW` hoặc bật `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` cho các bản quét chỉ chứa số. | Khi chất lượng OCR là yếu tố quan trọng (ví dụ: số hóa đơn) |
| **Thay thế bằng Tesseract** | Đổi import thành `net.sourceforge.tess4j.Tesseract` và điều chỉnh mã khởi tạo. | Dự án đã phụ thuộc vào Tesseract |

## Mẹo chuyên nghiệp

* **Thu nhỏ ảnh lớn** trước khi đưa vào engine; tốc độ OCR tỷ lệ với số pixel.
* **Tiền xử lý** ảnh (đen trắng, tăng độ tương phản) bằng các thư viện như OpenCV nếu nguồn ảnh có nhiễu.
* **Lưu cache engine OCR** nếu bạn gọi nó nhiều lần trong thời gian ngắn—khởi động và dừng engine tốn tài nguyên.
* **Xác thực kết quả** bằng biểu thức chính quy khi bạn mong đợi định dạng cụ thể (ví dụ: ngày tháng, số điện thoại).

## Kết luận

Bạn đã biết **cách thực hiện OCR** trên một ảnh trong Java, từ việc đọc file đến hiển thị văn bản đã trích xuất. Hướng dẫn đã đề cập đến các kỹ thuật **read image Java**, **extract text image**, **convert image to text**, và **image to text java**, đồng thời cung cấp các mẹo thực tiễn cho các tình huống thực tế.  

Từ đây bạn có thể:

* Tích hợp bước OCR vào một dịch vụ web nhận tải lên.
* Kết hợp đầu ra với chỉ mục tìm kiếm để thực hiện tìm kiếm toàn văn trên tài liệu đã quét.
* Khám phá các tùy chọn OCR nâng cao như hỗ trợ đa ngôn ngữ hoặc bộ ký tự tùy chỉnh.

Chúc lập trình vui vẻ, và tận hưởng việc biến ảnh thành văn bản có thể tìm kiếm!

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều có mã mẫu hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}