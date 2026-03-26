---
category: general
date: 2026-03-26
description: Tạo PDF có thể tìm kiếm bằng Aspose.OCR Java – học cách tải ảnh OCR,
  đặt ngôn ngữ chính, trích xuất văn bản từ ảnh và lưu PDF OCR.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: vi
og_description: Tạo PDF có thể tìm kiếm bằng Aspose.OCR Java. Hướng dẫn từng bước
  để tải ảnh OCR, đặt ngôn ngữ chính, trích xuất văn bản từ ảnh và lưu PDF OCR.
og_title: Tạo PDF có thể tìm kiếm với Aspose.OCR – Hướng dẫn Java
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Tạo PDF có thể tìm kiếm bằng Aspose.OCR – Hướng dẫn Java
url: /vi/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm với Aspose.OCR – Hướng dẫn Java

Bạn đã bao giờ cần **tạo pdf có thể tìm kiếm** từ một tài liệu đã quét nhưng không biết bắt đầu từ đâu? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn này khi lần đầu tiên làm việc với OCR trong Java. Tin tốt là Aspose.OCR làm cho toàn bộ quy trình—từ tải ảnh, thiết lập ngôn ngữ chính và cuối cùng lưu PDF có hỗ trợ OCR—rất dễ dàng. Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, có thể chạy được, **trích xuất văn bản từ ảnh**, cho phép bạn **đặt ngôn ngữ chính**, và kết thúc bằng **lưu pdf OCR** mà bạn có thể mở bằng bất kỳ trình đọc nào.

Chúng ta cũng sẽ đề cập một vài mẹo thực tiễn, như bật tăng tốc GPU để xử lý nhanh hơn và xử lý tài liệu đa ngôn ngữ (Tamil + English trong ví dụ). Khi kết thúc, bạn sẽ có một đoạn mã sẵn sàng cho môi trường production mà có thể chèn vào dự án của mình.

## Những gì bạn cần

- **Java 17** (hoặc bất kỳ JDK mới nào; Aspose.OCR hỗ trợ Java 8+)
- Thư viện **Aspose.OCR for Java** (tải từ trang chính thức hoặc thêm qua Maven)
- Một **file giấy phép** (hoặc bản dùng thử 30 ngày)
- Một file ảnh chứa văn bản (bản demo sử dụng `sample-mixed-tamil-eng.jpg`)

Không cần framework phụ, không cần phụ thuộc native—chỉ cần Java thuần và các file JAR của Aspose.

---

## Bước 1: Tạo PDF có thể tìm kiếm – Thiết lập dự án

Trước khi đi vào code, hãy chắc chắn dự án đã sẵn sàng để **tạo pdf có thể tìm kiếm**.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Giữ phiên bản cập nhật; các bản phát hành mới thường bao gồm các bản sửa lỗi hiệu năng cho việc sử dụng GPU.

Bây giờ tạo một lớp Java đơn giản có tên `RecentFeaturesDemo`. Lớp này sẽ chứa toàn bộ logic cần **tải ảnh OCR**, cấu hình cài đặt ngôn ngữ, và cuối cùng **lưu pdf OCR**.

---

## Bước 2: Tải ảnh OCR và Khởi tạo Engine

Bước thực tế đầu tiên trong quy trình là **tải ảnh OCR**. Điều này cho Aspose.OCR biết file nào sẽ được phân tích.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Tại sao lại quan trọng:** Bật GPU (`setUseGpu(true)`) có thể giảm thời gian xử lý tới 70 % trên phần cứng hiện đại, trong khi xử lý song song đảm bảo CPU không bị nhàn rỗi khi GPU đang bận.

---

## Bước 3: Đặt Ngôn ngữ Chính (và Ngôn ngữ phụ)

Nếu bỏ qua bước này, Aspose.OCR sẽ cố gắng đoán ngôn ngữ, khiến quá trình chậm hơn và kém chính xác. Dưới đây là cách **đặt ngôn ngữ chính** là Tamil và thêm English làm dự phòng.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Giải thích:** Ngôn ngữ chính ảnh hưởng đến bộ ký tự và từ điển được sử dụng trong quá trình nhận dạng. Thêm ngôn ngữ phụ là rất quan trọng cho các tài liệu đa script (ví dụ: một hoá đơn có cả văn bản Tamil và English).  
> **Trường hợp đặc biệt:** Nếu tài liệu của bạn chứa hơn hai ngôn ngữ, bạn có thể gọi `addAdditionalLanguage(...)` cho mỗi ngôn ngữ bổ sung.

---

## Bước 4: Tiền xử lý ảnh – Cân chỉnh & Loại bỏ nhiễu

Ảnh quét thường bị xoay hoặc có nhiễu nền. Tiền xử lý giúp engine OCR **trích xuất văn bản từ ảnh** một cách đáng tin cậy hơn.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Mẹo:** Nếu bạn biết ảnh đã sạch sẽ, có thể bỏ qua `setDenoise(true)` để giảm vài mili giây.

---

## Bước 5: Tải File Ảnh

Bây giờ engine đã sẵn sàng, chúng ta chỉ cần chỉ định file muốn phân tích.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Nếu đường dẫn sai thì sao?** Aspose.OCR sẽ ném ra một `FileNotFoundException` rõ ràng. Hãy bọc lệnh trong try‑catch nếu cần xử lý lỗi mềm mại.

---

## Bước 6: Chạy OCR và Trích xuất Văn bản từ Ảnh

Với mọi thứ đã được cấu hình, đã đến lúc thực sự chạy nhận dạng. Bước này vừa **trích xuất văn bản từ ảnh** vừa chuẩn bị dữ liệu cần thiết cho việc tạo PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Kết quả console điển hình cho ảnh demo trông như sau:

```
வணக்கம் World
This is a mixed language sample.
```

Bạn sẽ thấy dòng Tamil được hiển thị đúng, tiếp theo là tiếng Anh. Đó là kết quả của việc **đặt ngôn ngữ chính** một cách chính xác.

---

## Bước 7: Lưu PDF OCR – Phần cuối cùng

Phần cuối cùng của quy trình là **lưu pdf OCR**. Aspose.OCR có thể nhúng một lớp văn bản vô hình lên trên ảnh gốc, khiến PDF có thể tìm kiếm.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Mở `searchable.pdf` trong Adobe Reader, nhấn **Ctrl + F**, và bạn có thể tìm kiếm cả từ Tamil và English—đúng như một quy trình **tạo pdf có thể tìm kiếm** hứa hẹn.

---

## Ví dụ Hoàn chỉnh (Sao chép‑Dán)

Dưới đây là chương trình đầy đủ mà bạn có thể biên dịch và chạy ngay. Thay các đường dẫn placeholder bằng thư mục của bạn.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Chạy bằng lệnh:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Bạn sẽ thấy văn bản đã trích xuất được in ra console, tiếp theo là xác nhận rằng **pdf có thể tìm kiếm** đã được ghi vào đĩa.

---

## Câu hỏi Thường gặp & Trường hợp Đặc biệt

### Nếu tôi cần **tải ảnh OCR** từ một mảng byte thì sao?

Bạn có thể thay `ImageStream.fromFile(imagePath)` bằng `ImageStream.fromBytes(byteArray)`. Điều này hữu ích khi ảnh đến từ cơ sở dữ liệu hoặc dịch vụ web.

### Làm thế nào để xử lý các PDF đã chứa ảnh?

Aspose.OCR có thể làm việc trực tiếp trên các trang PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Engine sẽ rasterize mỗi trang nội bộ trước khi nhận dạng.

### GPU của tôi không được phát hiện—có nên giữ `setUseGpu(true)` không?

Nếu `setUseGpu(true)` thất bại, Aspose.OCR sẽ tự động chuyển sang CPU. Bạn có thể kiểm tra `ocrEngine.getEngineSettings().isGpuAvailable()` trước khi bật.

### Tôi có thể **lưu pdf OCR** với siêu dữ liệu tùy chỉnh không?

Có. Sau khi nhận dạng, dùng `ocrEngine.getPdfSaveOptions().setTitle("My Document")` hoặc `setAuthor("John Doe")` trước khi gọi `save`.

---

## Mẹo Hiệu năng cho Lô lớn

- **Xử lý batch:** Tái sử dụng cùng một đối tượng `OcrEngine` cho nhiều ảnh. Chỉ cần gọi `ocrEngine.clear()` giữa các lần chạy.
- **Pool luồng:** Đóng gói mỗi tác vụ ảnh trong một `Callable` và submit tới `ExecutorService`. Vì đã bật xử lý song song, mỗi luồng sẽ hưởng lợi từ đa lõi.
- **Quản lý bộ nhớ:** Đối với ảnh gig‑pixel, cân nhắc giảm kích thước bằng `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)` để giữ RAM ở mức hợp lý.

---

## Kết luận

Chúng ta vừa đi qua toàn bộ quy trình **tạo pdf có thể tìm kiếm** bằng Aspose.OCR cho Java. Bắt đầu từ **tải ảnh OCR**, chúng ta đã:

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}