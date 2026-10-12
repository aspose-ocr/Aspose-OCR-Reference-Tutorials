---
category: general
date: 2026-10-11
description: Tìm hiểu cách thực hiện OCR trên hình PNG trong Java, trích xuất văn
  bản từ hình ảnh và chuyển đổi hình ảnh thành văn bản bằng ví dụ OcrEngine đơn giản.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: vi
lastmod: 2026-10-11
og_description: Cách thực hiện OCR trên ảnh PNG bằng Java, trích xuất văn bản từ ảnh
  và chuyển ảnh thành văn bản bằng một ví dụ ngắn gọn, sẵn sàng chạy.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Cách thực hiện OCR trên hình PNG trong Java – hướng dẫn đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Cách thực hiện OCR trên hình ảnh PNG trong Java
url: /vi/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách thực hiện OCR trên ảnh PNG trong Java

Nếu bạn cần **perform OCR** trên một tệp hình ảnh, việc học **how to perform OCR** trong Java là cần thiết cho nhiều nhiệm vụ tự động hoá. Dù bạn đang số hoá biên lai, lập chỉ mục tài liệu đã quét, hoặc xây dựng một kho ảnh có thể tìm kiếm, khả năng **extract text from image** từ các tệp giúp tiết kiệm vô số giờ làm việc thủ công.

Hướng dẫn này cho bạn một giải pháp hoàn chỉnh, có thể chạy được, tải một PNG, chạy một engine OCR, và **recognize text from PNG**. Bạn cũng sẽ thấy cách **convert image to text** và xử lý các vấn đề thường gặp như đầu vào độ phân giải thấp hoặc ký tự không phải ASCII.

## Những gì bạn sẽ đạt được

* **load image java** code đọc một PNG từ đĩa,
* khởi tạo một engine OCR nhẹ,
* **extract text from image** và in kết quả ra console,
* điều chỉnh giải pháp cho các định dạng hình ảnh khác hoặc xử lý hàng loạt.

Không cần dịch vụ bên ngoài—chỉ cần một thư viện OCR mã nguồn mở duy nhất (Tess4J) và môi trường chạy Java SE.

---

## Yêu cầu trước

* Java 17 hoặc mới hơn (mã được biên dịch với JDK 17).
* Maven hoặc Gradle để quản lý phụ thuộc.
* Kiến thức cơ bản về dòng lệnh và IDE mà bạn chọn.
* Thư viện `tess4j` (một wrapper Java cho Tesseract). Thêm phụ thuộc Maven sau:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Nếu bạn dùng Gradle, tương đương là:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Bạn cũng cần các tệp dữ liệu Tesseract (`.traineddata`). Tải gói dữ liệu tiếng Anh từ kho chính thức và đặt vào thư mục có tên `tessdata` ở thư mục gốc của dự án.

## Bước 1: Tải ảnh trong Java

Việc tải một PNG rất đơn giản với lớp chuẩn `ImageIO`. Đoạn mã dưới đây minh họa **load image java** một cách an toàn, có xử lý ngoại lệ:

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Tại sao điều này quan trọng:** `ImageIO.read` tự động phát hiện định dạng ảnh, nhưng chúng ta kiểm tra `null` một cách rõ ràng để tránh lỗi im lặng khi PNG bị hỏng. Mẫu này là thực hành tốt khi bạn **load image java** cho OCR.

## Bước 2: Khởi tạo engine OCR

Tess4J bọc binary gốc của Tesseract, cung cấp một API Java đơn giản. Phương thức sau tạo một thể hiện `Tesseract`, chỉ tới thư mục `tessdata`, và cấu hình ngôn ngữ là tiếng Anh:

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Tại sao chúng ta làm như vậy:** Khởi tạo engine một lần và tái sử dụng cho nhiều ảnh giảm chi phí khởi động. Lệnh `setOcrEngineMode` chọn chế độ mặc định, hoạt động tốt cho hầu hết PNG. Nếu gặp ảnh quét nhiễu, bạn có thể thử các chế độ khác (ví dụ, `OEM_LSTM_ONLY`).

## Bước 3: Thực hiện OCR và **recognize text from PNG**

Bây giờ chúng ta kết hợp bộ tải ảnh và engine OCR. Phương thức dưới đây chạy OCR trên một `BufferedImage` và trả về chuỗi đã trích xuất:

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Ví dụ đầy đủ có thể chạy**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Kết quả mong đợi**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Console sẽ hiển thị các ký tự chính xác mà engine trích xuất từ `sample.png`. Nếu PNG chỉ chứa một từ duy nhất, kết quả sẽ là từ đó kèm theo một ký tự xuống dòng.

## Bước 4: Các biến thể phổ biến và trường hợp đặc biệt

### 4.1 Xử lý PNG độ phân giải thấp

Tesseract hoạt động tốt nhất trên ảnh có ít nhất 300 DPI. Nếu PNG nguồn của bạn nhỏ hơn, hãy phóng to trước khi OCR:

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Áp dụng `upscale(image, 2)` trước khi gọi `extractText` để cải thiện độ chính xác.

### 4.2 Trích xuất văn bản không phải tiếng Anh

Để **extract text from image** chứa các ngôn ngữ khác, tải các tệp `.traineddata` phù hợp và đặt mã ngôn ngữ:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Xử lý hàng loạt nhiều PNG

Nếu bạn cần **recognize text from PNG** trong một thư mục, lặp qua các tệp trong thư mục:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Xử lý lỗi OCR

Các lỗi OCR thường gặp bao gồm đọc nhầm `0` (số không) thành `O` hoặc `1` thành `l`. Xử lý hậu kỳ bằng biểu thức chính quy có thể làm sạch kết quả:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

## Mẹo chuyên nghiệp để OCR đáng tin cậy trong Java

| Tip | Reason |
|-----|--------|
| **Sử dụng PNG không mất dữ liệu** | Các artefact nén trong JPEG có thể làm rối engine. |
| **Cắt bỏ viền trắng** | Khoảng trắng thừa làm tăng thời gian xử lý và có thể gây kết quả dương tính giả. |
| **Đặt `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** chỉ khi bố cục không xác định; nếu không, chọn một chế độ cụ thể (ví dụ, `PSM_SINGLE_BLOCK`). | |
| **Lưu cache thể hiện `ITesseract`** | |

## Bạn nên học gì tiếp theo?

Các hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh có hướng dẫn từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}