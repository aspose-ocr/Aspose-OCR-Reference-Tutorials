---
category: general
date: 2026-09-16
description: Tìm hiểu cách bật GPU để tăng tốc OCR trong Java, nhận dạng văn bản từ
  các tệp hình ảnh và chuyển đổi hình ảnh thành văn bản bằng Aspose OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: vi
lastmod: 2026-09-16
og_description: Cách bật GPU cho OCR trong Java, nhận dạng văn bản từ các tệp hình
  ảnh và chuyển đổi hình ảnh thành văn bản với Aspose OCR – hướng dẫn chi tiết từng
  bước.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: Cách bật GPU và trích xuất văn bản từ hình ảnh trong Java
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Cách bật GPU và trích xuất văn bản từ hình ảnh trong Java
url: /vi/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách bật GPU và trích xuất văn bản từ hình ảnh trong Java

Nếu bạn cần **cách bật GPU** cho nhận dạng ký tự quang học, hướng dẫn này sẽ chỉ cho bạn các bước chính xác. Bằng cách bật tăng tốc GPU, bạn có thể **nhận dạng văn bản từ tệp hình ảnh** nhanh hơn nhiều lần so với chỉ dùng CPU. Ví dụ sử dụng Aspose OCR cho Java, nhưng các khái niệm áp dụng cho bất kỳ thư viện OCR nào hỗ trợ GPU.

Trong tutorial này bạn sẽ học cách:

* Bật tăng tốc GPU trong engine OCR.  
* Tải một hình ảnh và **trích xuất văn bản từ hình ảnh**.  
* **Chuyển đổi hình ảnh thành văn bản** chỉ với vài dòng code.  

Không cần dịch vụ bên ngoài—tất cả chạy cục bộ trên máy của bạn. Một môi trường phát triển Java cơ bản và thư viện Aspose OCR cho Java là những điều kiện tiên quyết duy nhất.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn bạn có:

| Yêu cầu | Phiên bản / Chi tiết |
|-------------|------------------|
| Java Development Kit (JDK) | 8 hoặc mới hơn |
| Maven hoặc Gradle (để quản lý phụ thuộc) | Bất kỳ phiên bản gần đây nào |
| GPU hỗ trợ CUDA (tùy chọn nhưng khuyến nghị) | GPU NVIDIA với driver ≥ 450 |
| Thư viện Aspose OCR cho Java | 23.9 hoặc mới hơn (tải từ trang web Aspose) |

Nếu bạn không có GPU, code vẫn hoạt động; nó sẽ chỉ chạy trên CPU.

## Bước 1: Thêm Aspose OCR vào dự án của bạn

Đối với Maven, thêm phụ thuộc sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Đối với Gradle, đặt đoạn này trong `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Các mục này sẽ tự động kéo engine OCR và các binary GPU gốc.

## Bước 2: Cách bật GPU cho engine OCR

Nhiệm vụ chính là thông báo cho `OcrEngine` sử dụng GPU. Aspose OCR cung cấp một flag đơn giản:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**Tại sao lại quan trọng:** Khi gọi `setGpuEnabled(true)`, thư viện sẽ tải các kernel dựa trên CUDA để song song hoá các giai đoạn tiền xử lý ảnh và phân đoạn ký tự. Trên một card NVIDIA hiện đại, bạn có thể thấy tốc độ tăng 2‑4× so với đường đi mặc định trên CPU.

> **Mẹo chuyên nghiệp:** Kiểm tra GPU của bạn có được phát hiện bằng cách chạy `SystemInfo.isCudaSupported()` trước khi bật flag. Nếu phương thức trả về `false`, engine sẽ tự động quay lại CPU.

## Bước 3: Tải hình ảnh bạn muốn xử lý

Bạn có thể đưa bất kỳ định dạng ảnh nào được Aspose hỗ trợ (JPEG, PNG, BMP, TIFF, v.v.) vào engine OCR. Dưới đây là cách tải một tệp JPEG:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**Trường hợp đặc biệt:** Nếu ảnh quá lớn (hơn 5 MB) hãy cân nhắc thu nhỏ trước để giảm tiêu thụ bộ nhớ. Engine OCR hoạt động tốt nhất với ảnh khoảng 300 dpi.

## Bước 4: Thực hiện OCR và **nhận dạng văn bản từ hình ảnh**

Khi engine đã được cấu hình và ảnh đã được tải, bạn có thể chạy nhận dạng:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

Phương thức `recognize()` trả về một `String` dạng văn bản thuần. Bên trong, engine thực hiện một số giai đoạn:

1. **Tiền xử lý** – chỉnh nghiêng, nhị phân hoá và tăng độ tương phản (tăng tốc bằng GPU).  
2. **Phân đoạn** – xác định các dòng văn bản, từ và ký tự.  
3. **Phân loại** – so sánh mỗi ký tự với mô hình ngôn ngữ tích hợp.

Vì GPU đang hoạt động, các bước 1 và 2 hưởng lợi nhiều nhất từ việc thực thi song song.

## Bước 5: Hiển thị hoặc lưu văn bản đã trích xuất

Cuối cùng, xuất kết quả ra console, tệp, hoặc bất kỳ bộ xử lý nào tiếp theo:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**Kết quả điển hình** (cho một ảnh mẫu chứa “Hello World”):

```
Recognized text:
Hello World
```

Nếu OCR không phát hiện ký tự nào, `recognizedText` sẽ là một chuỗi rỗng. Trong trường hợp đó, hãy kiểm tra lại chất lượng ảnh hoặc tắt GPU để so sánh hiệu năng.

## Xử lý các vấn đề thường gặp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------|-----|
| **GPU không được phát hiện** | Thiếu driver CUDA hoặc GPU không hỗ trợ | Cài đặt driver NVIDIA mới nhất và kiểm tra bằng `nvidia-smi`. |
| **Ký tự sai** | Độ tương phản thấp hoặc nền nhiễu | Tiền xử lý ảnh (ví dụ: tăng độ tương phản) trước khi đưa vào engine. |
| **Lỗi hết bộ nhớ** | Ảnh quá lớn trên GPU có bộ nhớ hạn chế | Thu nhỏ ảnh xuống ≤ 2000 px chiều rộng hoặc xử lý theo từng tile. |
| **Ngôn ngữ không khớp** | Mô hình ngôn ngữ mặc định là tiếng Anh nhưng văn bản ở ngôn ngữ khác | Gọi `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (hoặc enum phù hợp) trước `recognize()`. |

## Ví dụ đầy đủ, có thể chạy được

Dưới đây là một lớp Java tự chứa tất cả các bước. Lưu lại dưới tên `GpuEnabledOcrExample.java`, chỉnh đường dẫn ảnh, và chạy bằng `javac`/`java` hoặc qua IDE của bạn.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### Kết quả mong đợi

Chạy chương trình sẽ in văn bản đã trích xuất ra console và ghi cùng nội dung vào `recognized_output.txt`. Với GPU bật, thời gian thực thi tổng cho ảnh 2 MP thường dưới 200 ms trên NVIDIA RTX 3060, so với ~500 ms chỉ dùng CPU.

## Kết luận

Bạn đã biết **cách bật GPU** cho Aspose OCR trong Java, **nhận dạng văn bản từ hình ảnh** và **chuyển đổi hình ảnh thành văn bản** chỉ với vài dòng code đơn giản. Bằng cách tận dụng tăng tốc GPU, bạn đạt được xử lý nhanh hơn, rất cần thiết cho các ứng dụng batch‑oriented hoặc thời gian thực như quét hoá đơn, xử lý biên lai và số hoá tài liệu.

**Các bước tiếp theo**

* Thử nghiệm các mô hình ngôn ngữ khác (`ocrEngine.setLanguage`) để **trích xuất văn bản từ hình ảnh** bằng tiếng Pháp, Đức, hoặc Trung Quốc.  
* Kết hợp đầu ra OCR với Apache Tika để tự động lập chỉ mục nội dung đã trích xuất.  
* Khám phá streaming các PDF lớn trang‑theo‑trang nếu bạn cần **nhận dạng văn bản từ khung hình ảnh** bên trong tài liệu PDF.

Hãy tự do điều chỉnh mẫu, tích hợp vào dịch vụ của bạn, và chia sẻ kết quả. Chúc bạn lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ code hoàn chỉnh với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}