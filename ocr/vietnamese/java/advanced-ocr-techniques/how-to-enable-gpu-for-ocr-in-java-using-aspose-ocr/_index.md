---
category: general
date: 2026-08-18
description: Cách bật GPU cho OCR trong Java và nhanh chóng nhận dạng văn bản ảnh,
  trích xuất văn bản JPG, thêm bộ lọc và thiết lập ngôn ngữ với Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: vi
lastmod: 2026-08-18
og_description: Cách bật GPU cho OCR trong Java và nhận dạng văn bản hình ảnh ngay
  lập tức, trích xuất văn bản JPG, thêm bộ lọc và thiết lập ngôn ngữ bằng Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Cách bật GPU cho OCR trong Java – hướng dẫn đầy đủ Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Cách bật GPU cho OCR trong Java bằng Aspose.OCR
url: /vi/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bật GPU cho OCR trong Java sử dụng Aspose.OCR

Nếu bạn cần **cách bật GPU** cho OCR trong Java, hướng dẫn này sẽ đưa bạn qua các bước chính xác. Kích hoạt tăng tốc GPU cho phép bạn **nhận dạng văn bản trong hình ảnh** nhanh hơn nhiều lần, điều này rất quan trọng khi bạn phải **trích xuất văn bản JPG** hàng loạt. Chúng tôi cũng sẽ đề cập đến **cách thêm bộ lọc**, **cách đặt ngôn ngữ**, và cách lấy kết quả cuối cùng.

Khi kết thúc tutorial này, bạn sẽ có một chương trình hoàn chỉnh, có thể chạy được mà:

* Khởi động engine Aspose.OCR với hỗ trợ GPU.  
* Cấu hình ngôn ngữ OCR (ví dụ: English).  
* Áp dụng bộ lọc giảm nhiễu để cải thiện độ chính xác.  
* Tải ảnh JPEG, thực hiện nhận dạng và in ra văn bản đã trích xuất.

> **Yêu cầu trước:** Java 17 hoặc mới hơn, Maven, và giấy phép Aspose.OCR cho Java (bản dùng thử miễn phí hoạt động cho mục đích đánh giá).

---

![How to enable GPU for OCR in Java](/images/ocr-gpu.png){alt="Cách bật GPU cho OCR trong Java"}

## Những gì bạn sẽ cần

| Item | Reason |
|------|--------|
| **Java Development Kit (JDK) 17+** | Cần thiết để biên dịch và chạy ví dụ. |
| **Maven** | Đơn giản hoá việc quản lý phụ thuộc cho Aspose.OCR. |
| **Aspose.OCR for Java** | Cung cấp lớp `OcrEngine` và hỗ trợ GPU. |
| **A sample JPEG image** (`sample.jpg`) | Được dùng để minh họa **trích xuất văn bản JPG**. |
| **GPU‑compatible hardware** (optional but recommended) | Kích hoạt tăng tốc hiệu năng mà chúng ta sẽ cấu hình. |

---

## Bước 1: Thiết lập dự án Maven

Tạo một dự án Maven mới (hoặc thêm vào dự án hiện có) và bao gồm phụ thuộc Aspose.OCR:

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **Mẹo:** Giữ phiên bản luôn cập nhật; các bản phát hành mới cải thiện việc xử lý GPU và thêm các gói ngôn ngữ.

---

## Bước 2: Khởi tạo engine OCR và **cách bật GPU**

Trái tim của giải pháp là `OcrEngine`. Việc khởi tạo nó rất đơn giản, nhưng bạn phải bật rõ ràng tăng tốc GPU:

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Tại sao bật GPU?**  
Khi gọi `setUseGpu(true)`, Aspose.OCR sẽ chuyển các kernel xử lý ảnh nặng sang card đồ họa. Trên một GPU NVIDIA/AMD hiện đại, tốc độ nhận dạng có thể tăng từ ~200 ms mỗi trang xuống < 80 ms, giảm đáng kể thời gian xử lý tổng cho các lô lớn.

---

## Bước 3: **Cách đặt ngôn ngữ** và **cách thêm bộ lọc**

### 3.1 Đặt ngôn ngữ OCR

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR đi kèm với các gói ngôn ngữ cho hơn 100 ngôn ngữ. Thay `ENGLISH` bằng `FRENCH`, `CHINESE_SIMPLIFIED`, v.v., để phù hợp với tài liệu nguồn của bạn.

### 3.2 Thêm bộ lọc tiền xử lý

Tiếng ồn, các artefact nén, hoặc ánh sáng không đồng đều có thể làm giảm độ chính xác. Thêm bộ lọc giảm nhiễu là cách **cách thêm bộ lọc** điển hình:

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

Các bộ lọc hữu ích khác bao gồm `FilterType.CONTRAST`, `FilterType.BRIGHTNESS`, và `FilterType.BINARIZE`. Bạn có thể chuỗi nhiều bộ lọc bằng cách gọi `addPreprocessFilter` nhiều lần.

---

## Bước 4: Tải ảnh – **trích xuất văn bản JPG**

Bây giờ chúng ta chỉ định engine tới file JPEG cần xử lý:

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Thay `YOUR_DIRECTORY` bằng đường dẫn thực tế nơi `sample.jpg` nằm. Aspose.OCR cũng hỗ trợ PNG, BMP, TIFF và PDF; cùng một lệnh sẽ hoạt động cho các định dạng đó.

---

## Bước 5: Thực hiện OCR và **nhận dạng văn bản trong hình ảnh**

Với engine đã được cấu hình, gọi quy trình nhận dạng:

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

Phương thức `recognize()` xử lý ảnh trên GPU (nếu đã bật) và điền vào bộ đệm văn bản nội bộ. `getText()` trả về một `String` dạng plain‑text, bạn có thể ghi vào file, cơ sở dữ liệu, hoặc truyền cho các pipeline NLP tiếp theo.

### Đầu ra dự kiến

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Nếu ảnh chứa nhiều dòng, chuỗi trả về sẽ bao gồm ký tự xuống dòng (`\n`) để giữ nguyên bố cục gốc.

---

## Bước 6: Xác minh việc sử dụng GPU (tùy chọn)

Để chắc chắn GPU thực sự được dùng, bật logging của Aspose:

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Kiểm tra `ocr-debug.log` sau khi chạy; bạn sẽ thấy các mục như `GPU device: NVIDIA GeForce RTX 3080` và `Processing time (GPU): 78 ms`. Nếu log đề cập đến **CPU**, hãy kiểm tra lại cài đặt driver và chắc chắn lệnh `setUseGpu(true)` đã có.

---

## Những lỗi thường gặp và cách tránh chúng

| Symptom | Likely cause | Fix |
|---------|--------------|-----|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Thiếu thư viện GPU gốc | Cài đặt driver GPU mới nhất và đảm bảo các binary gốc `aspose-ocr` có trong `java.library.path`. |
| **Poor accuracy on dark images** | Không có bộ lọc tiền xử lý | Thêm `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` hoặc tăng `FilterType.CONTRAST`. |
| **`OutOfMemoryError` on large batches** | Hết bộ nhớ GPU | Xử lý ảnh theo lô nhỏ hơn hoặc tắt GPU (`engine.setUseGpu(false)`) cho các độ phân giải rất lớn. |
| **Incorrect language output** | Đặt ngôn ngữ sai | Xác minh `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` khớp với văn bản nguồn. |

---

## Ví dụ đầy đủ, có thể chạy được

Dưới đây là lớp Java hoàn chỉnh bạn có thể sao chép‑dán vào `src/main/java/com/example/HelloWorldOcr.java`. Nó bao gồm tất cả các bước, xử lý lỗi, và logging tùy chọn.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Chạy chương trình**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Bạn sẽ thấy văn bản đã nhận dạng được in ra console và lưu trong `output.txt`. File `ocr-debug.log` sẽ xác nhận việc sử dụng GPU.

---

## Kết luận

Trong tutorial này chúng tôi đã trình bày **cách bật GPU** cho Aspose.OCR trong Java, cách **nhận dạng văn bản trong hình ảnh**, **trích xuất văn bản JPG**, **cách thêm bộ lọc**, và **cách đặt ngôn ngữ**—tất cả trong một chương trình tự chứa duy nhất. Khi bật GPU, bạn sẽ có tốc độ đáng kể, trong khi các bộ lọc và cài đặt ngôn ngữ đảm bảo độ chính xác cao trên nhiều nguồn ảnh khác nhau.

**Các bước tiếp theo**

* Thử nghiệm các bộ lọc bổ sung như `FilterType.BINARIZE` cho tài liệu quét.  
* Chuyển sang các ngôn ngữ khác (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) để mở rộng hỗ trợ đa ngôn ngữ.  
* Kết hợp pipeline OCR này với Apache PDFBox để trích xuất văn bản trực tiếp từ các trang PDF.  

Bạn có thể tùy chỉnh mã cho xử lý hàng loạt, tích hợp vào dịch vụ Spring Boot, hoặc kết nối với hàng đợi tin nhắn để thực hiện OCR thời gian thực. Chúc lập trình vui!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên đều bao gồm ví dụ mã đầy đủ với giải thích chi tiết từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Đọc Văn Bản từ Hình Ảnh trong Java Sử Dụng Aspose OCR – Hướng Dẫn Đầy Đủ](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Cách OCR Văn Bản Hình Ảnh với Ngôn Ngữ Sử Dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Tiền Xử Lý Ảnh OCR trong Java với Aspose OCR – Tăng Độ Chính Xác & Trích Xuất Văn Bản](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}