---
category: general
date: 2026-05-31
description: Tiền xử lý hình ảnh cho OCR nhằm cải thiện đáng kể độ chính xác của OCR
  bằng cách sử dụng Aspose OCR Java. Thực hiện theo hướng dẫn chi tiết từng bước.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: vi
og_description: Tiền xử lý hình ảnh cho OCR và tìm hiểu cách cải thiện độ chính xác
  của OCR bằng việc tiền xử lý trong Java sử dụng Aspose OCR.
og_title: Tiền xử lý ảnh cho OCR – Tăng độ chính xác với tiền xử lý
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Tiền xử lý hình ảnh cho OCR – Tăng độ chính xác với việc tiền xử lý
url: /vi/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý hình ảnh cho OCR – Tăng độ chính xác với tiền xử lý

Bạn đã bao giờ tự hỏi tại sao kết quả OCR của mình lại rối rắm mặc dù ảnh nguồn trông ổn? Trong hầu hết các trường hợp, nguyên nhân ẩn trong hình ảnh — nghiêng, nhiễu, độ tương phản thấp — những yếu tố làm rối ngay cả những bộ nhận dạng thông minh nhất. **Tiền xử lý hình ảnh cho OCR** và bạn sẽ thấy chất lượng tăng vọt.

Trong tutorial này, chúng tôi không chỉ chỉ cho bạn cách tiền xử lý hình ảnh cho OCR, mà còn giải thích **cách cải thiện độ chính xác OCR với tiền xử lý** bằng cách xây dựng một pipeline nhỏ nhưng mạnh mẽ với Aspose OCR cho Java. Khi hoàn thành, bạn sẽ có một chương trình sẵn sàng chạy, chuyển đổi PNG nhiễu, lệch thành văn bản sạch, dễ đọc.

## Những gì bạn sẽ học

- Tại sao tiền xử lý lại quan trọng đối với các engine OCR  
- Cách thiết lập Aspose OCR trong dự án Java  
- Mã từng bước **tiền xử lý hình ảnh cho OCR** bằng các bộ lọc deskew, denoise và contrast  
- Mẹo tinh chỉnh pipeline để **cải thiện độ chính xác OCR với tiền xử lý** trên bộ dữ liệu của riêng bạn  

Không có phần thừa, chỉ có một ví dụ hoàn chỉnh, có thể chạy và lý do cho từng dòng mã.

## Điều kiện tiên quyết

Trước khi bắt đầu, hãy chắc chắn bạn có:

| Yêu cầu | Lý do |
|-------------|--------|
| Java 8 hoặc mới hơn | Thư viện Aspose OCR Java hỗ trợ Java 8+ |
| Maven hoặc Gradle (tùy chọn) | Đơn giản hoá việc thêm phụ thuộc Aspose OCR |
| Tệp giấy phép Aspose OCR for Java (`Aspose.OCR.Java.lic`) | Cần thiết để mở khóa toàn bộ tính năng |
| Một hình mẫu (ví dụ, `noisy_skewed.png`) | Hình ảnh bạn sẽ *tiền xử lý hình ảnh cho OCR* |

Nếu thiếu bất kỳ mục nào, hãy dừng lại và chuẩn bị chúng — chạy mã mà không có giấy phép sẽ chỉ gây ra ngoại lệ.

## Bước 1: Áp dụng giấy phép Aspose OCR

Điều đầu tiên cần làm. Engine OCR sẽ không thực hiện gì hữu ích nếu không có giấy phép hợp lệ. Bước này **tiền xử lý hình ảnh cho OCR** một cách gián tiếp bằng cách mở khóa toàn bộ các bộ lọc ảnh.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Mẹo chuyên nghiệp:** Giữ tệp giấy phép ra khỏi hệ thống kiểm soát phiên bản. Sử dụng biến môi trường hoặc vault bảo mật trong môi trường production.

## Bước 2: Khởi tạo Engine OCR và tải ảnh nguồn

Bây giờ chúng ta tạo engine, chỉ định ngôn ngữ mong muốn và trỏ tới file mà chúng ta muốn *tiền xử lý hình ảnh cho OCR*.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

Tại sao phải đặt ngôn ngữ? Vì engine có thể áp dụng các heuristic riêng cho ngôn ngữ, điều này đã **cải thiện độ chính xác OCR với tiền xử lý** ngay trước khi chúng ta áp dụng các bộ lọc.

## Bước 3: Xây dựng Pipeline tiền xử lý

Đây là phần cốt lõi của tutorial. Ở đây chúng ta **tiền xử lý hình ảnh cho OCR** bằng cách chuỗi ba bộ lọc:

| Bộ lọc | Chức năng | Lý do quan trọng đối với độ chính xác |
|--------|--------------|-----------------------------|
| `AutoDeskew` | Phát hiện và chỉnh sửa góc quay | Các dòng văn bản nghiêng làm rối việc phân đoạn ký tự |
| `DenoiseMedian(3)` | Giảm nhiễu bằng bộ lọc trung vị (kernel = 3) | Loại bỏ các đốm nhiễu trông giống ký tự lẻ |
| `ContrastStretch` | Kéo dãn histogram để tăng độ tương phản | Nền tối trở nên đọc được, văn bản sáng nổi bật hơn |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

Lưu ý chúng ta không cần viết bất kỳ mã xử lý ảnh nào từ đầu — Aspose đã cung cấp các bộ lọc sẵn. Điều này **cải thiện độ chính xác OCR với tiền xử lý** một cách đáng kể trong khi vẫn giữ cho triển khai ngắn gọn.

## Bước 4: Chạy OCR trên ảnh đã tiền xử lý

Với pipeline đã sẵn sàng, engine sẽ tự động áp dụng các bộ lọc trước khi nhận dạng. Bạn chỉ cần một lời gọi duy nhất:

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

Ở phía sau, engine:

1. Tải PNG gốc.  
2. Đưa nó qua `AutoDeskew`, `DenoiseMedian` và `ContrastStretch`.  
3. Chạy bộ nhận dạng trên bitmap đã được làm sạch.  

Đó là phép màu của **tiền xử lý hình ảnh cho OCR** — công việc nặng được trừu tượng hoá.

## Bước 5: Xuất văn bản đã nhận dạng

Cuối cùng, in kết quả ra console hoặc ghi vào file. Đối với mục đích demo, một `System.out.println` đơn giản đã đủ.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

Nếu mọi thứ diễn ra tốt, bạn sẽ thấy các câu sạch, dễ đọc thay vì một mớ hỗn độn. Kết quả cụ thể phụ thuộc vào ảnh nguồn, nhưng bạn sẽ nhận thấy sự cải thiện rõ rệt so với việc chạy OCR trên file thô.

### Kết quả mong đợi (ví dụ)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

Nếu vẫn còn ký tự lạ, hãy kiểm tra lại thứ tự các bộ lọc — đôi khi áp dụng `ContrastStretch` *trước* `DenoiseMedian` cho kết quả tốt hơn trên các bản scan bị hư hỏng nặng.

## Trực quan hoá Pipeline (Tùy chọn)

Dưới đây là sơ đồ mô tả cách ảnh chảy qua từng bộ lọc. Nó có thể giúp bạn giải thích quy trình cho đồng nghiệp hoặc nhúng vào tài liệu.

![preprocess image for OCR pipeline diagram](pipeline.png "Diagram showing AutoDeskew → DenoiseMedian → ContrastStretch stages for preprocess image for OCR")

*Alt text:* *Sơ đồ tiền xử lý hình ảnh cho OCR minh hoạ ba bộ lọc được áp dụng trước khi nhận dạng.*

## Những lỗi thường gặp & Cách khắc phục

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|---------|--------------|-----|
| Văn bản vẫn mờ sau tiền xử lý | Bộ lọc contrast không đủ mạnh | Tăng hệ số kéo dãn hoặc thử `HistogramEqualization` |
| OCR ném `NullPointerException` | Đường dẫn tệp giấy phép sai | Kiểm tra lại đường dẫn và đảm bảo tệp có thể đọc được |
| Vẫn còn nghiêng | Góc quay ảnh > 15° (giới hạn AutoDeskew) | Xoay ảnh thủ công bằng `AffineTransform` trước pipeline |
| Quá nhiều kết quả sai | Mức độ nhiễu cao, kernel quá nhỏ | Tăng kernel trung vị (ví dụ, `new DenoiseMedian(5)`) |

Dự đoán trước các vấn đề này sẽ giúp bạn **cải thiện độ chính xác OCR với tiền xử lý** ngay cả trên những bản scan khó khăn nhất.

## Mở rộng Pipeline

Muốn kiểm soát nhiều hơn? Aspose OCR cho phép bạn thêm bộ lọc tùy chỉnh hoặc thay đổi thứ tự các bộ lọc hiện có. Một vài ý tưởng:

- **Binarization**: `preprocessor.addFilter(new BinarizeOtsu());` – ép ảnh thành đen‑trắng thuần túy, hữu ích cho tài liệu in.  
- **Resize**: `preprocessor.addFilter(new Scale(2.0));` – phóng to ảnh độ phân giải thấp, thường tăng độ chính xác.  
- **Sharpen**: `preprocessor.addFilter(new Sharpen());` – làm nổi bật các cạnh cho phông chữ nhỏ.

Nhớ rằng mỗi bộ lọc bổ sung sẽ tăng thời gian xử lý, vì vậy hãy benchmark trên phần cứng mục tiêu của bạn.

## Toàn bộ mã nguồn (Sẵn sàng sao chép)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

Lưu lại dưới tên `PreprocessDemo.java`, thêm JAR Aspose OCR vào classpath (hoặc khai báo trong Maven), và chạy:



## Bạn nên học gì tiếp theo?

- [Cách OCR Văn bản Hình ảnh với Ngôn ngữ Sử dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Trích xuất Văn bản từ Hình ảnh Java với Aspose.OCR Chế độ Phát hiện Khu vực](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Cách tính góc nghiêng java bằng Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}