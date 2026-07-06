---
category: general
date: 2026-03-28
description: Tìm hiểu cách nhận dạng văn bản trong hình ảnh bằng Java sử dụng Aspose
  OCR, trích xuất văn bản từ các tệp PNG và sử dụng tăng tốc GPU để OCR nhanh các
  hình ảnh lớn.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: vi
og_description: Khám phá cách nhận dạng văn bản trong hình ảnh bằng Java, trích xuất
  văn bản từ các tệp PNG và sử dụng tăng tốc GPU cho OCR các hình ảnh lớn.
og_title: Nhận dạng văn bản trong ảnh bằng Java OCR – Ví dụ tăng tốc GPU
tags:
- OCR
- Java
- GPU
title: Nhận dạng văn bản trong hình ảnh bằng Java OCR – Ví dụ tăng tốc bằng GPU
url: /vi/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# nhận dạng văn bản trong ảnh bằng Java OCR – Ví dụ tăng tốc GPU

Bạn đã bao giờ cần **nhận dạng văn bản trong ảnh** từ một tệp PNG khổng lồ nhưng phiên bản CPU lại chậm chạp? Bạn không phải là người duy nhất. Trong nhiều quy trình thực tế—như quét hoá đơn hoặc lưu trữ tài liệu lịch sử—kích thước ảnh có thể rất lớn, và engine OCR mặc định không thể bắt kịp.  

Tin tốt: Aspose OCR for Java cho phép bạn **sử dụng tăng tốc GPU** để tăng tốc quá trình, và mã nguồn lại rất ngắn gọn. Trong hướng dẫn này, bạn sẽ thấy một ví dụ Java OCR đầy đủ, có thể chạy ngay, **trích xuất văn bản từ tệp PNG**, tận dụng GPU hỗ trợ CUDA, và xử lý **ocr large image** chỉ với vài dòng code. Khi kết thúc, bạn sẽ biết cách tích hợp vào dự án Java của mình và hiểu tại sao mỗi thiết lập lại quan trọng.

## Những gì bạn sẽ học

- Cách thiết lập Aspose OCR trong dự án Maven hoặc Gradle.  
- Quy trình từng bước để **nhận dạng văn bản trong ảnh** trên GPU.  
- Tại sao việc cấu hình số lượng stream GPU có thể cải thiện thông lượng.  
- Cách kiểm tra đầu ra và khắc phục các vấn đề thường gặp.  

> **Yêu cầu trước** – Java 17 (hoặc mới hơn), GPU tương thích CUDA với driver mới nhất, và giấy phép Aspose OCR for Java hợp lệ (bản dùng thử miễn phí đủ cho việc đánh giá). Không cần thư viện bên ngoài nào khác.

---

## Bước 1: Thêm phụ thuộc Aspose OCR

Đầu tiên, đưa thư viện Aspose OCR vào dự án của bạn. Nếu bạn dùng **Maven**, thêm đoạn sau vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

Đối với **Gradle**, đặt đoạn này trong `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Mẹo:** Phiên bản mới nhất (tính đến tháng 3 2026) đã bao gồm các cải tiến hiệu năng cho tải công việc GPU, vì vậy luôn luôn kéo phiên bản mới nhất.

---

## Bước 2: Khởi tạo OCR Engine và bật GPU

Tạo một OCR engine rất đơn giản. Phần quan trọng là bật cờ GPU—nếu không, engine sẽ quay lại chế độ CPU.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### Tại sao phải bật GPU?

Khi bạn bật `setUseGpu(true)`, Aspose sẽ chuyển các phép tính mạng nơ-ron tích chập nặng nề sang card đồ họa. Điều này có thể giảm vài giây thời gian xử lý một **ocr large image**, đặc biệt khi ảnh vượt quá 4000 × 4000 px. Nếu môi trường của bạn không có GPU tương thích, lệnh này sẽ trở thành không thực hiện và engine sẽ tiếp tục chạy trên CPU—không gây lỗi, chỉ chậm hơn.

---

## Bước 3: Nhận dạng ảnh PNG và trích xuất văn bản

Bây giờ chỉ định engine tới tệp bạn muốn xử lý. Ví dụ sử dụng `sample-large.png`, nhưng bạn có thể thay bằng bất kỳ tệp PNG hoặc JPEG nào.

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Khi chạy chương trình, bạn sẽ thấy đầu ra giống như:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

Đầu ra này xác nhận thao tác **nhận dạng văn bản trong ảnh** đã thành công và bạn đã **trích xuất văn bản png** thành công.

---

## Bước 4: Kiểm tra việc sử dụng GPU (Tùy chọn nhưng hữu ích)

Nếu bạn muốn biết GPU thực sự có được sử dụng hay không, mở công cụ giám sát GPU của hệ thống (ví dụ `nvidia-smi` trên Linux). Khi quá trình Java đang chạy, bạn sẽ thấy một mức tăng nhẹ về bộ nhớ và mức sử dụng tính toán.

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

Nếu không thấy hoạt động nào, hãy kiểm tra lại:

1. Driver CUDA phù hợp với mẫu GPU.  
2. Lệnh `setUseGpu(true)` không bị ghi đè ở phần sau của mã.  
3. Tệp giấy phép của bạn (nếu có) không hạn chế việc sử dụng GPU.

---

## Bước 5: Xử lý các trường hợp đặc biệt thường gặp

### Ảnh lớn vượt quá bộ nhớ GPU

Khi ảnh quá lớn (ví dụ 8000 × 8000 px), GPU có thể hết bộ nhớ. Một cách khắc phục nhanh là giảm kích thước ảnh trước khi đưa vào Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

Sau đó truyền `"sample-resized.png"` vào `recognizeImage`. Cách này giữ độ chính xác OCR trong khi không vượt quá giới hạn GPU.

### PDF đa trang

Aspose OCR cũng có thể xử lý PDF theo từng trang. Lặp qua mỗi trang, chuyển nó thành ảnh, và đưa vào engine. Cờ **use gpu acceleration** vẫn được áp dụng, giúp bạn có một pipeline PDF‑to‑text nhanh chóng.

---

## Ví dụ hoàn chỉnh (Sẵn sàng sao chép‑dán)

Dưới đây là lớp Java đầy đủ, sẵn sàng biên dịch và chạy. Thay `YOUR_DIRECTORY` bằng đường dẫn tới tệp PNG của bạn.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Đầu ra mong đợi** – một chuỗi văn bản thuần thể hiện mọi nội dung engine có thể đọc được từ ảnh. Nếu ảnh chứa bảng, bạn sẽ nhận được nội dung các ô được nối bằng dấu xuống dòng; Aspose không giữ nguyên bố cục, nhưng bạn có thể xử lý chuỗi sau nếu cần.

---

## Câu hỏi thường gặp

| Question | Answer |
|----------|--------|
| **Do I need a paid license?** | Bản dùng thử hoạt động cho tới 200 trang và tắt watermark cho OCR. Đối với môi trường production, giấy phép sẽ loại bỏ giới hạn và mở khóa toàn bộ stack GPU. |
| **What if my GPU is older (e.g., GTX 750)?** | Các GPU cũ hơn vẫn có thể hoạt động nhưng tốc độ sẽ giảm; đảm bảo bạn có ít nhất Compute Capability 3.0. |
| **Can I process JPG or BMP files?** | Chắc chắn—`recognizeImage` chấp nhận bất kỳ định dạng nào được Java ImageIO hỗ trợ. |
| **Is there a way to batch‑process many images?** | Đặt lời gọi OCR trong một vòng lặp, và cân nhắc tăng `setGpuStreams` để phù hợp với số lượng stream đồng thời bạn muốn. |
| **What if I need to preserve layout?** | Sử dụng `LayoutOptions` của Aspose OCR để lấy các bounding box; phần này nằm ngoài phạm vi hướng dẫn nhanh nhưng được mô tả trong API. |

---

## Kết luận

Bạn đã có một **java ocr example** ngắn gọn, đầu‑cuối, có thể **nhận dạng văn bản trong ảnh**, **trích xuất văn bản png**, và **sử dụng tăng tốc GPU** để tăng tốc xử lý một **ocr large image**. Bằng cách điều chỉnh số lượng stream GPU và, nếu cần, giảm kích thước ảnh quá lớn, bạn có thể tùy chỉnh giải pháp cho hầu hết mọi cấu hình phần cứng.

Sẵn sàng cho bước tiếp theo? Hãy thử đưa một thư mục các biên lai đã quét vào cùng pipeline, hoặc khám phá API `TextRegion` của Aspose để giữ nguyên bố cục gốc. Nếu gặp khó khăn, diễn đàn Aspose và Javadoc là những nguồn tài nguyên tuyệt vời—chỉ cần nhớ các kiến thức cơ bản chúng ta đã đề cập ở đây.

Chúc lập trình vui vẻ, và chúc OCR của bạn chạy nhanh như chớp!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}