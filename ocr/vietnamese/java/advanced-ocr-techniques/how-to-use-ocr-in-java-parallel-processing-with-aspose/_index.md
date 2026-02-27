---
category: general
date: 2026-02-27
description: Tìm hiểu cách sử dụng OCR trong Java để trích xuất văn bản hình ảnh từ
  các tệp TIFF và PDF bằng xử lý song song của Aspose OCR. Hướng dẫn nhanh, đơn giản.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: vi
og_description: Tìm hiểu cách sử dụng OCR trong Java để trích xuất văn bản từ hình
  ảnh trong các tệp TIFF và PDF bằng xử lý song song của Aspose OCR.
og_title: Cách sử dụng OCR trong Java – Xử lý song song với Aspose
tags:
- OCR
- Java
- Aspose
title: Cách sử dụng OCR trong Java – Xử lý song song với Aspose
url: /vi/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong Java – Xử Lý Song Song với Aspose

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để trích xuất văn bản từ tài liệu đã quét mà không gặp khó khăn chưa? Bạn không phải là người duy nhất. Các nhà phát triển thường gặp rào cản khi cần đọc văn bản từ hình ảnh—đặc biệt là TIFF và PDF—và đồng thời duy trì hiệu năng.

Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn một giải pháp hoàn chỉnh, sẵn sàng chạy, giúp **trích xuất văn bản hình ảnh trong Java** bằng Aspose OCR, bật xử lý song song, và thậm chí cho phép bạn giới hạn số lượng luồng. Khi kết thúc, bạn sẽ có một lớp duy nhất có thể **thực hiện OCR trên PDF** và **trích xuất văn bản từ TIFF** trong thời gian chỉ bằng một phần nhỏ so với cách tiếp cận đơn luồng.

> **Bạn sẽ nhận được**  
> * Giải thích rõ ràng tại sao OCR song song quan trọng.  
> * Một chương trình Java đầy đủ (không thiếu import).  
> * Mẹo điều chỉnh việc sử dụng luồng và xử lý các vấn đề thường gặp.  

## Yêu cầu trước

- Java 8 hoặc mới hơn (mã nguồn cũng biên dịch được với JDK 11).  
- Thư viện Aspose.OCR cho Java – bạn có thể tải JAR mới nhất từ Maven Central (`com.aspose:aspose-ocr`).  
- Một file ảnh (`.tif`, `.tiff`) hoặc PDF bạn muốn xử lý.  
- Một lượng RAM vừa phải—xử lý song song sẽ khởi tạo một vài luồng, nhưng Aspose tiết kiệm bộ nhớ.

Nếu bạn đã có những thứ này, hãy bắt đầu.

![Sơ đồ mô tả quy trình OCR – cách sử dụng OCR trong Java với xử lý song song](how-to-use-ocr-pipeline.png)

*Văn bản thay thế hình ảnh: sơ đồ ví dụ cách sử dụng OCR*

---

## Bước 1: Thiết lập Dự án và Thêm Aspose OCR

### Tại sao điều này quan trọng

Trước khi bạn có thể **thực hiện OCR trên PDF** hoặc bất kỳ hình ảnh nào, thư viện phải có trong classpath của bạn. Nếu không, trình biên dịch sẽ ném `ClassNotFoundException` và bạn sẽ bị kẹt ở bước hai.

### Cách thực hiện

Nếu bạn đang sử dụng Maven, thêm phụ thuộc:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Đối với Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Mẹo chuyên nghiệp:** Giữ số phiên bản đồng bộ với ghi chú phát hành của Aspose; các phiên bản mới thường bao gồm cải tiến hiệu năng cho xử lý song song.

---

## Bước 2: Tạo Engine OCR và Bật Xử Lý Song Song

### Tại sao điều này quan trọng

Mặc định, Aspose OCR chạy trên một luồng duy nhất. Khi bạn cung cấp cho nó một PDF đa trang hoặc một loạt TIFF, engine sẽ xử lý mỗi trang lần lượt—chậm và không hiệu quả. Bật xử lý song song cho phép CPU xử lý nhiều trang cùng lúc, giảm thời gian thực thi đáng kể.

### Code

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Giải thích các dòng quan trọng**

- `setUseParallelProcessing(true)`: cho Aspose biết chia tải công việc ra các lõi CPU có sẵn.  
- `setMaxThreads(...)`: bạn có thể giới hạn pool luồng nếu đang trên máy chủ chia sẻ hoặc muốn để chỗ cho các dịch vụ khác.  
- `processImage(inputPath)`: hoạt động cho cả file ảnh và tài liệu PDF, vì vậy cùng một lời gọi **thực hiện OCR trên PDF** và trên TIFF.

---

## Bước 3: Xử lý Các Loại Đầu Vào Khác Nhau – PDF vs. TIFF

### Tại sao điều này quan trọng

Mặc dù `processImage` chấp nhận một chuỗi đường dẫn, cách xử lý bên dưới lại khác nhau. PDF thường chứa nhiều trang, mỗi trang trở thành một công việc OCR riêng. TIFF có thể là một trang hoặc đa trang; Aspose coi mỗi khung ảnh là một trang.

### Những điểm cần lưu ý

| Đầu vào | Vấn đề thường gặp | Cách khắc phục đề xuất |
|------|----------------|-----------------|
| PDF | Các PDF lớn có thể làm cạn kiệt bộ nhớ nếu tất cả các trang được tải đồng thời. | Sử dụng `ocrEngine.getConfig().setMemoryOptimization(true);` (có sẵn trong các phiên bản mới). |
| Multi‑page TIFF | Một số TIFF cũ sử dụng nén không được hỗ trợ. | Chuyển đổi sang định dạng được hỗ trợ trước, hoặc sử dụng trợ giúp `TiffImage` của Aspose. |

Dưới đây là một đoạn mã nhanh cho thấy cách phát hiện loại file và ghi lại thông báo thân thiện:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Bước 4: Xác Minh Đầu Ra – Bạn Nên Nhìn Thấy Gì?

Khi chương trình kết thúc, bạn sẽ thấy văn bản đã trích xuất thô được in ra console. Đối với một hoá đơn quét đơn giản, đầu ra có thể trông như sau:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Nếu OCR gặp khó khăn với một trang cụ thể, Aspose sẽ chèn một dòng placeholder như `[Unrecognizable]`. Bạn có thể lọc chúng ra sau nếu cần dữ liệu sạch.

**Kiểm tra nhanh**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Bước 5: Tinh Chỉnh Hiệu Năng – Khi Nào Điều Chỉnh Số Lượng Luồng

### Tại sao điều này quan trọng

Nhiều luồng không phải luôn đồng nghĩa với kết quả nhanh hơn. Trên laptop 4‑core, khởi chạy 8 luồng có thể gây overhead chuyển đổi ngữ cảnh. Ngược lại, trên server 32‑core bạn có thể muốn khai thác toàn bộ sức mạnh.

### Cách tìm điểm cân bằng

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Chạy chương trình với các cài đặt khác nhau và đo thời gian:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Ghi lại thời gian, chọn cấu hình cho throughput tốt nhất, và cố định nó cho môi trường production.

---

## Bước 6: Mở Rộng Demo – Xử Lý Hàng Loạt Nhiều File

Nếu bạn cần **trích xuất văn bản hình ảnh java** từ toàn bộ thư mục, hãy bao bọc logic cốt lõi trong một vòng lặp:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Mẫu này mở rộng tốt vì engine đã chạy các trang của mỗi file song song. Vòng lặp bên ngoài chạy tuần tự, nhưng bạn cũng có thể gửi mỗi file tới một `ExecutorService` nếu cần khai thác tối đa một cụm CPU lớn.

---

## Những Cạm Bẫy Thông Thường & Cách Tránh Chúng

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|------------|-------------------|----------------|
| `OutOfMemoryError` | Quá nhiều trang được tải cùng lúc (đặc biệt với PDF lớn). | Bật tối ưu hoá bộ nhớ (`setMemoryOptimization(true)`) hoặc xử lý PDF trang‑theo‑trang bằng `processPage`. |
| Ký tự bị rối | Cấu hình ngôn ngữ/charset sai. | Gọi `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` hoặc enum ngôn ngữ phù hợp. |
| Hiệu năng chậm mặc dù đã bật cờ song song | Hệ điều hành giới hạn tạo luồng hoặc JVM chạy với heap nhỏ. | Tăng flag heap `-Xmx`, và kiểm tra giới hạn luồng OS (`ulimit -u`). |
| Kết quả trống | Độ phân giải ảnh đầu vào < 300 dpi. | Tăng độ phân giải ảnh trước OCR hoặc dùng máy quét xuất độ phân giải cao hơn. |

---

## Tóm Tắt – Những Điều Chúng Ta Đã Bao Quát

- **Cách sử dụng OCR** trong Java với `OcrEngine` của Aspose.  
- Bật **xử lý song song** để tăng tốc **thực hiện OCR trên PDF** và **trích xuất văn bản từ TIFF**.  
- Điều chỉnh số lượng luồng để đạt hiệu năng tối ưu.  
- Xử lý các trường hợp đặc biệt như PDF lớn, TIFF đa trang, và cài đặt ngôn ngữ.  
- Mở rộng demo một file thành bộ xử lý hàng loạt cho khối lượng công việc thực tế.

---

## Bước Tiếp Theo

Bây giờ bạn đã nắm vững các kiến thức cơ bản, hãy xem xét khám phá các chủ đề liên quan sau:

- **Trích xuất văn bản hình ảnh java** từ ghi chú viết tay (bật `setHandwritingRecognition(true)`).  
- Tích hợp đầu ra OCR với Apache Tika để trích xuất siêu dữ liệu.  
- Lưu kết quả vào Elasticsearch để lưu trữ tài liệu có thể tìm kiếm.  
- Sử dụng OCR của Aspose với các ngôn ngữ khác như Python hoặc .NET—nguyên tắc vẫn giống nhau.

Hãy thoải mái thử nghiệm với các giới hạn luồng khác nhau, định dạng ảnh và gói ngôn ngữ. Bạn càng thử nghiệm, bạn sẽ càng hiểu rõ các đánh đổi giữa tốc độ và độ chính xác.

---

### Chúc lập trình vui vẻ!

Nếu bạn gặp bất kỳ vấn đề nào hoặc có ý tưởng tối ưu hoá thêm, hãy để lại bình luận bên dưới. Tôi luôn sẵn sàng thảo luận về các mẹo OCR—không khó, chỉ cần code.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}