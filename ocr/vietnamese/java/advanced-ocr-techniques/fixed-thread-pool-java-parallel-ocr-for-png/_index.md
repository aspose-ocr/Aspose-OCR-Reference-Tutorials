---
category: general
date: 2026-02-17
description: Tìm hiểu cách sử dụng một fixed thread pool trong Java để trích xuất
  văn bản từ các ảnh PNG bằng xử lý OCR song song và tắt dịch vụ executor một cách
  đúng cách.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: vi
og_description: Khám phá cách một pool luồng cố định trong Java có thể trích xuất
  văn bản từ ảnh PNG một cách song song, chuyển đổi văn bản của các trang quét và
  tắt dịch vụ executor một cách an toàn.
og_title: fixed thread pool Java – OCR song song cho PNG
tags:
- java
- ocr
- multithreading
- aspose
title: bể luồng cố định Java – OCR song song cho PNG
url: /vi/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# fixed thread pool java – OCR song song cho PNG

Bạn đã bao giờ tự hỏi làm thế nào để tăng tốc OCR trên một loạt các tệp PNG bằng cách sử dụng **fixed thread pool java**? Trong hướng dẫn này, chúng ta sẽ thực hiện **extract text from PNG** các hình ảnh một cách song song, **convert scanned pages text** thành các chuỗi có thể chỉnh sửa, và an toàn **shut down executor service** khi công việc hoàn thành.

Nếu bạn từng nhìn chằm chằm vào một vòng lặp single‑threaded kéo dài trong nhiều phút, bạn sẽ hiểu cảm giác chờ đợi mỗi trang hoàn thành trước khi trang tiếp theo bắt đầu. Tin tốt là gì? Chỉ với vài dòng Java và Aspose OCR, bạn có thể khai thác sức mạnh của tất cả các lõi CPU, biến những trang quét thành văn bản có thể tìm kiếm, và giữ cho ứng dụng của bạn luôn phản hồi.

Dưới đây là một ví dụ hoàn chỉnh, sẵn sàng chạy, cùng với các giải thích tại sao mỗi phần lại quan trọng, những lỗi thường gặp, và các mẹo bạn có thể áp dụng cho bất kỳ thư viện OCR nào.

---

## Những gì bạn cần

- **Java 17** (hoặc bất kỳ JDK hiện đại nào) – mã sử dụng cú pháp hiện đại `var` một cách hạn chế, nhưng vẫn hoạt động trên các phiên bản cũ hơn.  
- Thư viện **Aspose.OCR for Java** – bạn có thể lấy nó từ Maven Central hoặc tải bản dùng thử từ Aspose.  
- Một tập hợp các tệp **PNG** bạn muốn xử lý – ví dụ như biên lai quét, trang sách, hoặc ảnh chụp màn hình.  
- Kiến thức cơ bản về đồng thời trong Java – không bắt buộc, nhưng sẽ hữu ích.

Đó là tất cả. Không cần dịch vụ bên ngoài, không cần Docker, chỉ cần Java thuần và một chút ma thuật đa luồng.

## Bước 1: Thêm phụ thuộc Aspose OCR & Giấy phép (Tùy chọn)

Đầu tiên, đảm bảo JAR Aspose OCR có trong classpath của bạn. Nếu bạn dùng Maven, thêm:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Nếu bạn không có giấy phép, thư viện sẽ chạy ở chế độ đánh giá; mã vẫn hoạt động như bình thường. Để tải giấy phép (được khuyến nghị cho môi trường production), đặt `Aspose.OCR.lic` vào thư mục resources và sử dụng:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Giữ file giấy phép ra ngoài hệ thống kiểm soát phiên bản để tránh việc lộ ra ngoài vô tình.

## Bước 2: Tạo một đối tượng `OcrEngine` Thread‑Safe

`OcrEngine` của Aspose OCR là thread‑safe miễn là bạn tái sử dụng cùng một thể hiện cho các tác vụ. Tạo nó một lần sẽ tiết kiệm bộ nhớ và tránh chi phí khởi tạo lại engine cho mỗi hình ảnh.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Tại sao nên tái sử dụng? Hãy tưởng tượng engine như một nhân viên nặng ký tải các mô hình ngôn ngữ vào bộ nhớ. Tạo một engine mới cho mỗi hình ảnh sẽ giống như thuê một chuyên gia mới cho mỗi công việc nhỏ – tốn kém và không cần thiết.

## Bước 3: Thiết lập Fixed Thread Pool Java

Bây giờ là phần trọng tâm: một **fixed thread pool java**. Chúng ta sẽ đặt kích thước bằng số bộ xử lý logic để mỗi lõi đều có công việc mà không bị quá tải.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Sử dụng một pool *fixed* (thay vì cached) giúp bạn dự đoán được việc sử dụng tài nguyên và ngăn ngừa các đợt “out‑of‑memory” khi hàng trăm hình ảnh đến cùng một lúc.

## Bước 4: Liệt kê các tệp PNG bạn muốn xử lý (Extract Text from PNG)

Thu thập các đường dẫn tới các hình ảnh bạn muốn OCR. Trong dự án thực tế bạn có thể quét một thư mục hoặc đọc từ cơ sở dữ liệu; ở đây chúng ta sẽ hard‑code một vài ví dụ.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Note:** Phần mở rộng tệp **png** là quan trọng vì Aspose OCR tự động phát hiện định dạng, nhưng bạn cũng có thể đưa JPEG hoặc TIFF vào.

## Bước 5: Gửi các tác vụ OCR – Xử lý OCR song song

Mỗi hình ảnh sẽ trở thành một callable trả về văn bản đã nhận dạng. Vì `OcrEngine` được chia sẻ, chúng ta chỉ cần truyền đường dẫn tệp vào tác vụ.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Tại sao lại bọc trong một `Future`? Nó cho phép chúng ta khởi chạy tất cả các công việc ngay lập tức, sau đó thu thập kết quả theo thứ tự đã gửi – hoàn hảo để giữ thứ tự trang khi **convert scanned pages text** trở lại một tài liệu.

## Bước 6: Lấy kết quả và hiển thị (Convert Scanned Pages Text)

Bây giờ chúng ta chờ mỗi `Future` hoàn thành và in ra kết quả. Lệnh `get()` chỉ chặn cho đến khi tác vụ cụ thể hoàn thành, không phải toàn bộ pool.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Kết quả console điển hình trông như sau:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Nếu bạn muốn ghi kết quả ra file, thay `System.out.println` bằng lệnh `Files.writeString`.

## Bước 7: Tắt dịch vụ Executor một cách sạch sẽ

Khi mọi tác vụ đã hoàn thành, việc **shut down executor service** là rất quan trọng; nếu không JVM có thể giữ các luồng non‑daemon sống, ngăn cản việc thoát ứng dụng một cách êm ái.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Mẫu `awaitTermination` cho phép pool có thời gian hoàn thành công việc đang chạy trước khi chúng ta buộc dừng. Bỏ qua bước này là nguyên nhân phổ biến gây rò rỉ bộ nhớ trong các ứng dụng chạy lâu dài.

## Ví dụ Hoạt động đầy đủ

Kết hợp tất cả lại, dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào `ParallelBatchDemo.java` và chạy:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}