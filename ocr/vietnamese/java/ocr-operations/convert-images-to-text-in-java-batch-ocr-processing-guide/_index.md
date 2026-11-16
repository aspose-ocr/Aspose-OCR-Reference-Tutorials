---
category: general
date: 2026-08-28
description: Tìm hiểu cách trích xuất văn bản từ các hình ảnh png trong Java bằng
  Aspose OCR. Hướng dẫn này bao gồm xử lý OCR hàng loạt, đọc ảnh từ một thư mục, và
  lọc tệp theo phần mở rộng.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Tìm hiểu cách trích xuất văn bản từ các hình ảnh png trong Java bằng
  Aspose OCR. Hướng dẫn này bao gồm xử lý OCR hàng loạt, đọc ảnh từ một thư mục, và
  lọc tệp theo phần mở rộng.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Cách trích xuất văn bản từ png trong Java – hướng dẫn OCR hàng loạt
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Cách trích xuất văn bản từ png trong Java – hướng dẫn OCR hàng loạt
url: /vi/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách trích xuất văn bản từ png trong Java – hướng dẫn OCR hàng loạt

Nếu bạn từng cần **trích xuất văn bản từ png** nhưng không chắc cách mở rộng quy mô vượt qua một vài hình ảnh, bạn đang ở đúng nơi. Nhiều nhà phát triển bắt đầu với một lời gọi OCR cho một ảnh duy nhất và nhanh chóng gặp giới hạn hiệu năng khi thư mục tăng lên hàng chục hoặc hàng trăm tệp. Với Aspose OCR cho Java, bạn có thể tạo một quy trình OCR hàng loạt mạnh mẽ, duyệt qua thư mục, lọc chỉ các loại ảnh bạn quan tâm, thực hiện nhận dạng song song và trả về kết quả theo cùng thứ tự với các tệp nguồn. Khi kết thúc hướng dẫn này, bạn sẽ có một đoạn mã Java sẵn sàng sử dụng, xử lý **xử lý OCR hàng loạt** một cách đáng tin cậy và hiệu quả.

![Ví dụ chuyển ảnh thành văn bản](https://example.com/convert-images-to-text.png "Ảnh chụp màn hình đầu ra console Java hiển thị văn bản đã chuyển đổi từ các tệp PNG")

## Câu trả lời nhanh
- **Thư viện nào xử lý OCR?** Aspose OCR for Java.
- **Tôi có thể xử lý PNG và JPG cùng lúc không?** Có – mẫu lọc cả hai phần mở rộng.
- **Engine OCR có an toàn với đa luồng không?** Một thể hiện `AsposeOCR` chia sẻ duy nhất là an toàn cho việc sử dụng đồng thời.
- **Tôi có cần giấy phép để thử nghiệm không?** Một khóa tạm thời miễn phí có sẵn từ Aspose.
- **Các thư mục con sẽ được quét tự động không?** `Files.walk` duyệt toàn bộ cây thư mục một cách đệ quy.

## Trích xuất văn bản từ png là gì?
`extract text from png` đề cập đến quá trình áp dụng nhận dạng ký tự quang học (OCR) lên các tệp Portable Network Graphics để các ký tự hiển thị trở thành các chuỗi có thể tìm kiếm, chỉnh sửa. Engine của Aspose OCR đọc dữ liệu pixel, xác định hình dạng glyph và trả về văn bản Unicode trong một lời gọi phương thức duy nhất.

## Tại sao nên sử dụng Aspose OCR cho Java?
Aspose OCR hỗ trợ **hơn 30 ngôn ngữ**, xử lý lên tới **500 ảnh mỗi phút** trên máy chủ tiêu chuẩn 8‑core, và có thể xử lý các tệp lên tới **200 MB** mà không cần tải toàn bộ ảnh vào bộ nhớ. Những khả năng được định lượng này cho phép bạn chạy các công việc hàng loạt quy mô lớn trên phần cứng thông thường mà không gặp giới hạn bộ nhớ.

## Yêu cầu trước
- Java 17 (hoặc bất kỳ phiên bản LTS gần đây nào).
- Maven hoặc Gradle để quản lý phụ thuộc.
- Một thư mục chứa các ảnh PNG/JPG bạn muốn xử lý.
- Kiến thức cơ bản về Java streams và gói `java.nio.file`.
- (Tùy chọn) Khóa giấy phép tạm thời Aspose OCR để đánh giá.

> **Mẹo:** Khóa tạm thời miễn phí hết hạn sau 30 ngày, nhưng nó cung cấp cho bạn quyền truy cập đầy đủ API để thử nghiệm.

## Quy trình OCR hàng loạt duy trì thứ tự như thế nào?
`Future<OcrResult>` đại diện cho một kết quả OCR đang chờ có thể được lấy khi quá trình xử lý hoàn tất. Quy trình duy trì thứ tự tệp gốc bằng cách lưu các đối tượng `Future<OcrResult>` trong một danh sách phản ánh thứ tự của bộ sưu tập `Path` đầu vào. Khi bạn lặp qua các future và gọi `get()`, mỗi lời gọi chỉ chặn cho ảnh tương ứng, vì vậy chuỗi đầu ra khớp với chuỗi đầu vào mà không cần logic sắp xếp thêm.

## Aspose OCR cho Java là gì?
`AsposeOCR` là lớp cốt lõi của thư viện Aspose OCR, bao gồm tất cả các gói ngôn ngữ, cài đặt nhận dạng và tài nguyên native nội bộ. Nó được thiết kế để khởi tạo một lần duy nhất trong vòng đời ứng dụng và có thể chia sẻ an toàn giữa nhiều luồng. Vì nó chỉ tải dữ liệu ngôn ngữ một lần, việc tái sử dụng cùng một thể hiện giảm thiểu chi phí khởi tạo và cải thiện thông lượng cho các thao tác hàng loạt.

## Cách thiết lập dự án và thêm Aspose OCR
Đầu tiên, tạo một dự án Maven (hoặc Gradle) và thêm phụ thuộc Aspose OCR vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Tại sao điều này quan trọng:** Khai báo phụ thuộc ngay từ đầu đảm bảo trình biên dịch có thể nhìn thấy `AsposeOCR`, `ParallelRecognizer` và các lớp liên quan. Nó cũng đảm bảo cùng một phiên bản được sử dụng trên mọi máy, điều này rất quan trọng cho **xử lý OCR hàng loạt** có thể tái tạo.

Làm mới IDE của bạn sau khi quá trình xây dựng hoàn tất; bây giờ bạn sẽ thấy các gói Aspose dưới **External Libraries**.

## Cách khởi tạo engine OCR – chia sẻ một thể hiện duy nhất
`AsposeOCR` là lớp engine OCR chính được cung cấp bởi thư viện Aspose OCR. Chúng ta chỉ cần **một** thể hiện engine OCR cho toàn bộ quá trình. Chia sẻ nó giữa các luồng giúp tiết kiệm bộ nhớ và tăng tốc vì engine chỉ tải các gói ngôn ngữ một lần.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` an toàn với đa luồng, vì vậy bạn có thể an tâm truyền nó cho một `ParallelRecognizer` sẽ quản lý một pool các luồng làm việc.

> **Giải thích:** `ParallelRecognizer` bọc engine trong một thread‑pool. Khi bạn gửi nhiều tệp, mỗi tệp sẽ có một luồng làm việc riêng, cho phép thực hiện song song thực sự trên CPU đa nhân.

## Cách đọc ảnh từ thư mục – duyệt cây thư mục
`Files.walk` là phương thức Java NIO duyệt đệ quy một cây thư mục và trả về một stream các đối tượng `Path`. Bây giờ chúng ta cần **đọc ảnh từ thư mục** và thu thập mọi PNG hoặc JPG. API `Files.walk` cho phép thực hiện điều này trong một dòng lệnh, nhưng chúng ta sẽ thêm bộ lọc để **trích xuất văn bản từ png** chỉ khi cần.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Tại sao chúng tôi lọc ở đây:** Sử dụng `filter` cho phép chúng ta **lọc tệp theo phần mở rộng** sớm, giảm thiểu I/O không cần thiết sau này. Nó cũng giữ cho mã dễ đọc—không cần regex phức tạp.

## Cách gửi công việc OCR bất đồng bộ
`recognizeAsync` gửi một ảnh tới engine OCR để xử lý bất đồng bộ và trả về một `Future<OcrResult>` đại diện cho kết quả đang chờ. Với danh sách các tệp đã sẵn sàng, chúng ta đẩy mỗi đường dẫn tới `ParallelRecognizer`. Phương thức `recognizeAsync` trả về một `Future<OcrResult>` mà chúng ta lưu lại để lấy sau.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Điều gì đang diễn ra phía sau?** Mỗi lời gọi đưa một tác vụ vào service executor nội bộ của recognizer. Các tác vụ chạy song song, vì vậy một thư mục chứa 100 ảnh có thể được xử lý trong một phần nhỏ thời gian so với vòng lặp đơn luồng.

## Cách lấy kết quả trong khi giữ nguyên thứ tự tệp
`Future<OcrResult>` chứa kết quả của một tác vụ OCR bất đồng bộ và cung cấp phương thức `get()` để lấy văn bản đã nhận dạng. Vì chúng ta đã lưu các future theo cùng thứ tự với `imagePaths`, chúng ta chỉ cần lặp qua danh sách và gọi `get()`. Lời gọi chỉ chặn cho đến khi ảnh cụ thể đó hoàn thành, duy trì thứ tự mà không cần ghi chép bổ sung.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Kết quả console mẫu** (rút gọn để ngắn gọn):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Xử lý trường hợp biên:** Nếu một ảnh nào đó gây ra ngoại lệ (tệp hỏng, định dạng không hỗ trợ), chúng ta bắt lỗi và tiếp tục xử lý các ảnh còn lại—một thói quen cần thiết cho các **quy trình OCR hàng loạt** đáng tin cậy.

## Cách dọn dẹp tài nguyên – tắt recognizer
`ParallelRecognizer.shutdown()` dừng thread‑pool nội bộ, đảm bảo mọi tác vụ OCR hoàn thành trước khi ứng dụng kết thúc. Đừng quên tắt thread‑pool nội bộ; nếu không JVM có thể treo khi thoát.

```java
recognizer.shutdown();
```

Xong rồi! Chương trình giờ có thể duyệt bất kỳ thư mục nào, lọc các tệp PNG/JPG, chạy OCR song song và in kết quả theo thứ tự gốc.

---

## Ví dụ hoàn chỉnh (sao chép và dán)

Dưới đây là lớp Java đầy đủ, sẵn sàng chạy. Thay `"YOUR_DIRECTORY"` bằng đường dẫn tới thư mục ảnh của bạn và chạy từ IDE hoặc dòng lệnh.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Chạy lớp, quan sát console đầy các chuỗi đã trích xuất, và chúc mừng vì bạn vừa **chuyển ảnh thành văn bản** mà không viết một vòng lặp nào chặn I/O.

---

## Câu hỏi thường gặp (FAQs)

**Q: Tôi có thể xử lý PDF hoặc TIFF cũng được không?**  
A: Chắc chắn. Aspose OCR hỗ trợ hơn 30 định dạng—bao gồm PDF, TIFF, BMP và GIF—vì vậy chỉ cần thêm các phần mở rộng mong muốn vào bộ lọc trong bước duyệt thư mục.

**Q: Nếu tôi cần một ngôn ngữ khác ngoài tiếng Anh, chẳng hạn tiếng Tây Ban Nha?**  
A: Thay `RecognitionLanguage.ENGLISH` bằng `RecognitionLanguage.SPANISH` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ). Các gói ngôn ngữ đã được đóng gói cùng thư viện, không cần tải thêm.

**Q: Thư mục của tôi chứa các thư mục con—chúng có được quét không?**  
A: Có. `Files.walk` duyệt toàn bộ cây thư mục một cách đệ quy, vì vậy mọi PNG/J

**Q: Làm sao để xử lý các ảnh cực lớn vượt quá 200 MB?**  
A: Bật chế độ streaming bằng cách gọi `ocrEngine.setUseStreaming(true)`. Điều này khiến engine đọc ảnh theo từng khối, giảm đáng kể mức sử dụng bộ nhớ tối đa.

**Q: Có cách nào để giới hạn số luồng OCR đồng thời không?**  
A: Có. Khi khởi tạo `ParallelRecognizer`, truyền số lượng luồng tối đa mong muốn làm đối số thứ hai (ví dụ, `new ParallelRecognizer(ocrEngine, 4)`).

---

**Cập nhật lần cuối:** 2026-08-28  
**Kiểm tra với:** Aspose OCR for Java 24.10  
**Tác giả:** Aspose  






```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Hướng dẫn liên quan

- [Chuyển ảnh thành văn bản trong Java – Hướng dẫn xử lý OCR hàng loạt](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Đọc văn bản từ ảnh trong Java – Hướng dẫn Aspose OCR đầy đủ](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Trích xuất văn bản từ ảnh bằng Aspose.OCR – Ký tự cho phép](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}