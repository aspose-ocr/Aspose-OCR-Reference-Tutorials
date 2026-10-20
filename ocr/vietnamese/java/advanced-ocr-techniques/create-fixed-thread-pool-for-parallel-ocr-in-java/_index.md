---
category: general
date: 2026-05-03
description: Tạo pool luồng cố định trong Java để nhanh chóng trích xuất văn bản từ
  hình ảnh. Tìm hiểu cách chạy OCR, chuyển đổi hình ảnh thành văn bản và tăng hiệu
  suất với xử lý OCR song song.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: vi
og_description: Tạo pool luồng cố định trong Java để nhanh chóng trích xuất văn bản
  từ hình ảnh. Tìm hiểu cách chạy OCR, chuyển đổi hình ảnh thành văn bản và tăng hiệu
  suất với xử lý OCR song song.
og_title: Tạo Fixed Thread Pool cho OCR song song trong Java
tags:
- Java
- OCR
- Multithreading
title: Tạo Pool Luồng Cố Định cho OCR Song Song trong Java
url: /vi/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo Fixed Thread Pool cho OCR Song Song trong Java

Bạn đã bao giờ cần **create fixed thread pool** để tăng tốc các công việc OCR, nhưng không biết bắt đầu từ đâu? Bạn không phải là người duy nhất. Trong nhiều dự án có nhiều hình ảnh, nút thắt là lời gọi OCR đơn luồng, và giải pháp lại đơn giản bất ngờ: khởi tạo một pool các luồng làm việc và để chúng xử lý các tệp song song.  

Trong hướng dẫn này, bạn sẽ học cách **extract text from images** bằng Aspose OCR, cách **run OCR** một cách hiệu quả, và cách **convert image to text** mà không làm quá tải CPU của bạn. Khi kết thúc, bạn sẽ có một chương trình Java sẵn sàng chạy, minh họa **parallel OCR processing** trên một vài hình mẫu.

## Những gì bạn sẽ xây dựng

Chúng ta sẽ tạo một ứng dụng console nhỏ mà:

* Đọc danh sách các đường dẫn hình ảnh (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** có kích thước bằng số lõi CPU.
* Gửi một tác vụ OCR cho mỗi hình ảnh.
* Thu thập văn bản đã nhận dạng và in ra console.
* Tắt executor một cách sạch sẽ.

Không cần công cụ xây dựng bên ngoài, không có framework phức tạp—chỉ cần Java thuần và thư viện Aspose OCR. Nếu bạn có Java 8+ và một IDE tốt, bạn đã sẵn sàng.

## Yêu cầu trước

* **Java Development Kit (JDK) 8 or newer** – code sử dụng lambda, vì vậy các phiên bản cũ sẽ không biên dịch được.  
* **Aspose OCR for Java** – tải JAR từ trang web Aspose hoặc lấy qua Maven (`com.aspose:aspose-ocr`).  
* Một thư mục chứa một vài hình ảnh thử nghiệm (code trỏ tới `YOUR_DIRECTORY`).  
* Kiến thức cơ bản về đồng thời trong Java (chúng tôi sẽ giải thích phần còn lại).  

> *Mẹo:* Nếu bạn đang sử dụng Maven, thêm phụ thuộc vào `pom.xml` và để IDE xử lý classpath.  

---

## Bước 1: Thêm các Import cần thiết

Đầu tiên, đưa các lớp cần thiết vào phạm vi. Đây không chỉ là phần mã mẫu; mỗi import cho JVM biết nơi tìm engine OCR, các tiện ích xử lý hình ảnh, và các công cụ đồng thời cho phép chúng ta **create fixed thread pool**.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – API OCR cốt lõi.  
* `java.util.*` – các collection để lưu trữ đường dẫn hình ảnh và kết quả.  
* `java.util.concurrent.*` – gói đồng thời chứa `ExecutorService` và `Future`.

## Bước 2: Xác định các hình ảnh cần xử lý

Tiếp theo, chúng ta liệt kê các tệp mà chúng ta muốn **extract text from images**. Sử dụng `Arrays.asList` giúp mã ngắn gọn và cho phép chúng ta thay đổi thư mục của bạn mà không cần chỉnh sửa phần còn lại của logic.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Bạn có thể tự do thêm nhiều mục; thread pool sẽ tự động mở rộng dựa trên số lõi CPU bạn có.

## Bước 3: **Create Fixed Thread Pool** phù hợp với số lõi CPU

Đây là phần cốt lõi của hướng dẫn. Chúng ta hỏi runtime có bao nhiêu lõi khả dụng và yêu cầu nhà máy `Executors` cung cấp một pool có đúng kích thước đó. Tại sao lại là fixed? Bởi vì số lượng luồng dự đoán được ngăn ngừa hiện tượng “thread explosion” gây thiếu tài nguyên cho hệ điều hành.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` trả về số lõi logic (bao gồm cả hyper‑threads).  
* `newFixedThreadPool(coreCount)` đảm bảo chúng ta không bao giờ vượt quá khả năng của CPU, đây là cách an toàn nhất để **run OCR** song song.

## Bước 4: Gửi một tác vụ OCR cho mỗi hình ảnh

Bây giờ chúng ta chuyển mỗi đường dẫn tệp thành một callable mà **runs OCR**, nhận dạng văn bản và trả về kết quả. Lưu ý chúng ta tạo một `OcrEngine` mới trong lambda—điều này tránh việc chia sẻ trạng thái engine không an toàn giữa các luồng.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Mỗi lời gọi `submit` đưa lambda cho pool, pool sẽ lên lịch trên một luồng rảnh.  
* Các đối tượng `Future<String>` cho phép chúng ta lấy lại văn bản đã nhận dạng sau này, giữ nguyên thứ tự nếu cần.

## Bước 5: Lấy và Hiển thị Văn bản Đã Nhận dạng

Khi tất cả các tác vụ đã được đưa vào hàng đợi, chúng ta chỉ cần duyệt qua danh sách `Future`, gọi `get()` để chặn cho tới khi mỗi công việc OCR hoàn thành. Đây là bước **convert image to text** hiện ra: lời gọi `engine.getText()` trả về chuỗi thô.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Kết quả console điển hình trông như sau:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Nếu một tệp thất bại (có thể bị hỏng), bạn sẽ thấy một dòng bắt đầu bằng `Failed:` tiếp theo là đường dẫn—rất hữu ích để gỡ lỗi nhanh.

## Bước 6: Dọn dẹp Executor Service

Đừng bao giờ quên tắt pool; nếu không JVM có thể vẫn chạy, nghĩ rằng còn công việc. Một việc tắt một cách nhẹ nhàng cho phép các tác vụ đang chạy hoàn thành trước khi tiến trình kết thúc.

```java
executor.shutdown();
```

Bạn cũng có thể gọi `awaitTermination` nếu cần áp đặt thời gian chờ, nhưng đối với hầu hết các tiện ích dòng lệnh, `shutdown()` đơn giản là đủ.

## Ví dụ Hoạt động Đầy đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán vào một tệp có tên `ParallelOcrTutorial.java`, điều chỉnh các đường dẫn hình ảnh, và chạy `javac` + `java` như bình thường.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Kết quả mong đợi:** nội dung văn bản của mỗi hình ảnh được in ra console, theo cùng thứ tự với danh sách `imagePaths`. Nếu bất kỳ hình ảnh nào không thể xử lý, bạn sẽ thấy thông báo lỗi thay vì dòng trống.

## Câu hỏi Thường gặp & Trường hợp Cạnh

### Nếu tôi có nhiều hình ảnh hơn số luồng?

Fixed thread pool sẽ tự động đưa các tác vụ dư thừa vào hàng đợi. Ngay khi một luồng hoàn thành công việc OCR hiện tại, nó sẽ lấy tác vụ tiếp theo. Hành vi hàng đợi này là bản chất của **parallel OCR processing**—bạn đạt được lưu lượng tối đa mà không làm quá tải CPU.

### Tôi có thể thay đổi ngôn ngữ không?

Chắc chắn. Thay thế `engine.getLanguage().setEnglish(true);` bằng cờ ngôn ngữ phù hợp, ví dụ `setFrench(true)` hoặc bật nhiều ngôn ngữ bằng cách gọi nhiều setter trước `recognize()`.

### Làm sao để xử lý các hình ảnh rất lớn?

Các tệp lớn có thể tiêu tốn nhiều bộ nhớ cho mỗi luồng. Nếu bạn gặp `OutOfMemoryError`, hãy cân nhắc giảm kích thước hình ảnh trước khi đưa vào engine, hoặc tăng kích thước heap bằng `-Xmx`. Một cách tiếp cận khác là sử dụng **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}