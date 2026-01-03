---
category: general
date: 2026-01-02
description: Chuyển đổi hình ảnh thành văn bản bằng Java sử dụng Aspose OCR. Thành
  thạo xử lý OCR hàng loạt, đọc hình ảnh từ thư mục và lọc tệp theo phần mở rộng.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: vi
og_description: Chuyển đổi hình ảnh thành văn bản nhanh chóng với Java. Hướng dẫn
  này bao gồm xử lý OCR hàng loạt, đọc hình ảnh từ thư mục và lọc tệp theo phần mở
  rộng.
og_title: Chuyển đổi hình ảnh thành văn bản trong Java – Hướng dẫn OCR hàng loạt đầy
  đủ
tags:
- OCR
- Java
- Aspose
title: Chuyển Đổi Hình Ảnh Thành Văn Bản trong Java – Hướng Dẫn Xử Lý OCR Hàng Loạt
url: /vi/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển Đổi Hình Ảnh thành Văn Bản trong Java – Hướng Dẫn Xử Lý OCR Hàng Loạt

Bạn đã bao giờ cần **chuyển đổi hình ảnh thành văn bản** nhưng không biết cách xử lý hàng chục tệp cùng lúc? Bạn không phải là người duy nhất—các nhà phát triển luôn phải đấu tranh để trích xuất dữ liệu từ PNG, JPG và các bản scan khác. Tin tốt là gì? Với Aspose OCR, bạn có thể tạo một pipeline OCR hàng loạt trong vài phút, đọc hình ảnh từ cấu trúc thư mục, và thậm chí lọc tệp theo phần mở rộng để chỉ làm việc với những gì quan trọng.

Trong tutorial này, chúng ta sẽ xây dựng một chương trình Java tự chứa, duyệt một thư mục, chọn ra mọi tệp `.png` hoặc `.jpg`, gửi từng ảnh tới Aspose OCR một cách bất đồng bộ, và in ra văn bản đã trích xuất theo đúng thứ tự ban đầu. Khi hoàn thành, bạn sẽ có một đoạn mã có thể tái sử dụng trong bất kỳ dự án nào cần **chuyển đổi hình ảnh thành văn bản** ở quy mô lớn.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Những gì bạn sẽ xây dựng

- Một engine `AsposeOCR` duy nhất được chia sẻ giữa các luồng (hiệu quả và thread‑safe).  
- Một `ParallelRecognizer` chạy các job OCR song song, hoàn hảo cho **xử lý OCR hàng loạt**.  
- Logic **đọc hình ảnh từ thư mục** bằng `java.nio.file.Files`.  
- Bộ lọc đơn giản để **trích xuất văn bản từ tệp PNG** đồng thời vẫn xử lý JPG.  
- Đóng gọn sạch sẽ pool luồng nội bộ để tránh rò rỉ tài nguyên.

### Yêu cầu trước

- Java 17 (hoặc bất kỳ phiên bản LTS gần đây nào).  
- Maven hoặc Gradle để tải thư viện Aspose OCR.  
- Một thư mục chứa các ảnh PNG/JPG bạn muốn xử lý.  
- Kiến thức cơ bản về Java streams—không cần gì phức tạp.

> **Mẹo chuyên nghiệp:** Nếu bạn chưa có giấy phép, Aspose cung cấp một khóa tạm thời miễn phí để bạn có thể thử nghiệm.

---

## Bước 1 – Thiết lập dự án và thêm Aspose OCR

Đầu tiên, tạo một dự án Maven mới (hoặc Gradle, tùy bạn). Thêm dependency Aspose OCR vào `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Tại sao lại quan trọng:** Khai báo dependency ngay từ đầu giúp trình biên dịch nhận diện `AsposeOCR`, `ParallelRecognizer` và các lớp liên quan. Nó cũng đảm bảo cùng một phiên bản được sử dụng trên mọi máy, điều này rất quan trọng cho **xử lý OCR hàng loạt** có thể tái tạo.

Khi quá trình build hoàn tất, làm mới IDE và bạn sẽ thấy các package Aspose dưới `External Libraries`.

---

## Bước 2 – Chuyển Đổi Hình Ảnh thành Văn Bản – Khởi tạo Engine OCR

Chúng ta chỉ cần **một** thể hiện engine OCR cho toàn bộ quá trình. Chia sẻ nó giữa các luồng giúp tiết kiệm bộ nhớ và tăng tốc vì engine chỉ tải gói ngôn ngữ một lần.

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

> **Giải thích:** `ParallelRecognizer` bọc engine trong một thread‑pool. Khi bạn gửi nhiều tệp, mỗi tệp sẽ được xử lý bởi một worker thread riêng, cho phép thực hiện song song thực sự trên CPU đa nhân.

---

## Bước 3 – Đọc Hình Ảnh từ Thư Mục – Duyệt Cây Thư Mục

Bây giờ chúng ta cần **đọc hình ảnh từ thư mục** và thu thập mọi PNG hoặc JPG. API `Files.walk` cho phép làm điều này trong một dòng, nhưng chúng ta sẽ thêm bộ lọc để **trích xuất văn bản từ PNG** khi cần.

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

> **Tại sao lại lọc ở đây:** Sử dụng `filter` cho phép chúng ta **lọc tệp theo phần mở rộng** ngay từ đầu, giảm thiểu I/O không cần thiết sau này. Nó cũng giữ cho code sạch sẽ—không cần regex phức tạp.

---

## Bước 4 – Xử Lý OCR Hàng Loạt – Gửi Job Bất Đồng Bộ

Khi danh sách tệp đã sẵn sàng, chúng ta đẩy từng đường dẫn tới `ParallelRecognizer`. Phương thức `recognizeAsync` trả về một `Future<OcrResult>` mà chúng ta lưu lại để lấy kết quả sau.

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

> **Điều gì đang diễn ra phía sau?** Mỗi lời gọi đưa một task vào executor service nội bộ của recognizer. Các task chạy song song, vì vậy một thư mục chứa 100 ảnh có thể được xử lý trong một phần thời gian so với vòng lặp đơn luồng.

---

## Bước 5 – Lấy Kết Quả theo Thứ Tự Gốc – Giữ Trình Tự Tệp

Vì chúng ta lưu các `Future` theo cùng thứ tự với `imagePaths`, chỉ cần duyệt danh sách và gọi `get()`. Lệnh này sẽ chặn chỉ cho đến khi ảnh tương ứng hoàn thành, giữ nguyên thứ tự mà không cần quản lý phức tạp.

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

**Ví dụ đầu ra console** (rút gọn để tiện):

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

> **Xử lý trường hợp ngoại lệ:** Nếu một ảnh nào đó ném ra lỗi (tệp hỏng, định dạng không hỗ trợ), chúng ta bắt và tiếp tục xử lý các ảnh còn lại—một thói quen thiết yếu cho các pipeline **xử lý OCR hàng loạt** đáng tin cậy.

---

## Bước 6 – Dọn Dẹp – Đóng Recognizer

Đừng bao giờ quên tắt pool luồng nội bộ; nếu không JVM có thể treo khi thoát.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

Xong rồi! Chương trình bây giờ sẽ duyệt bất kỳ thư mục nào, lọc các tệp PNG/JPG, chạy OCR song song và in ra kết quả.

---

## Ví Dụ Hoàn Chỉnh

Dưới đây là lớp Java đầy đủ, sẵn sàng sao chép‑dán. Thay `"YOUR_DIRECTORY"` bằng đường dẫn tới thư mục ảnh của bạn và chạy từ IDE hoặc dòng lệnh.

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

Chạy lớp, quan sát console đầy các chuỗi đã trích xuất, và chúc mừng vì bạn vừa **chuyển đổi hình ảnh thành văn bản** mà không viết một vòng lặp nào chặn I/O.

---

## Câu Hỏi Thường Gặp (FAQs)

**Hỏi: Tôi có thể xử lý PDF hoặc TIFF không?**  
Đáp: Chắc chắn. Aspose OCR hỗ trợ nhiều định dạng—chỉ cần thêm các phần mở rộng tệp tương ứng vào bộ lọc ở Bước 2.

**Hỏi: Nếu tôi cần ngôn ngữ khác, chẳng hạn tiếng Tây Ban Nha?**  
Đáp: Thay `RecognitionLanguage.ENGLISH` bằng `RecognitionLanguage.SPANISH`. Đảm bảo gói ngôn ngữ đã được cài đặt (Aspose đã bao gồm hầu hết các ngôn ngữ chính).

**Hỏi: Thư mục của tôi có các thư mục con—chúng có được quét không?**  
Đáp: Có. `Files.walk` duyệt toàn bộ cây thư mục một cách đệ quy, vì vậy mọi PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}