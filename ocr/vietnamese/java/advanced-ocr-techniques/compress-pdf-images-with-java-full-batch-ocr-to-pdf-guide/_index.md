---
category: general
date: 2026-07-05
description: Nén hình ảnh PDF khi chuyển PNG sang PDF bằng Java. Tìm hiểu tiền xử
  lý hình ảnh cho OCR, nhận dạng văn bản JPG và thực hiện OCR hàng loạt sang PDF trong
  một hướng dẫn.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: vi
og_description: Nén hình ảnh PDF và chuyển PNG sang PDF bằng Java. Hướng dẫn này bao
  gồm tiền xử lý hình ảnh cho OCR, nhận dạng văn bản JPG và OCR hàng loạt sang PDF.
og_title: Nén ảnh PDF bằng Java – Hướng dẫn OCR hàng loạt đầy đủ
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Nén hình ảnh PDF bằng Java – Hướng dẫn OCR hàng loạt đầy đủ sang PDF
url: /vi/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nén Hình Ảnh PDF với Java – Hướng Dẫn Toàn Bộ Batch OCR sang PDF

Bạn đã bao giờ cần **nén hình ảnh PDF** trong khi chuyển một thư mục PNG thành các PDF có thể tìm kiếm chưa? Bạn không phải là người duy nhất. Trong nhiều quy trình tự động, vấn đề lớn nhất là cân bằng chất lượng hình ảnh, độ chính xác OCR và kích thước PDF cuối cùng—tất cả cùng một lúc.  

Trong tutorial này chúng ta sẽ đi qua một giải pháp thực tế giúp **chuyển PNG sang PDF**, áp dụng **image preprocessing for OCR**, và cuối cùng **nén hình ảnh PDF** để đầu ra vẫn nhẹ. Khi kết thúc, bạn sẽ biết cách **recognize text JPG** các tệp, thiết lập quy trình **batch OCR to PDF**, và giữ các PDF của mình gọn gàng.

## Những Điều Bạn Sẽ Học

- Cài đặt Aspose OCR cho Java và áp dụng giấy phép.
- Cấu hình engine cho đa luồng, tăng tốc GPU và sửa lỗi chính tả.
- Xây dựng một pipeline **image preprocessing for OCR** có thể tái sử dụng (loại bỏ nhiễu, tăng độ tương phản, nhị phân hoá).
- Sử dụng **PdfSaveOptions** để **compress PDF images** mà không làm giảm khả năng đọc.
- Duyệt qua một thư mục để **convert PNG to PDF** và **recognize text JPG** hàng loạt.
- Một chương trình Java hoàn chỉnh, sẵn sàng chạy mà bạn có thể đưa vào bất kỳ dự án nào.

> **Prerequisites**: Java 8+, Maven hoặc Gradle, giấy phép Aspose OCR cho Java, và một thư mục chứa các ảnh PNG/JPG bạn muốn xử lý.

---

## Bước 1: Áp Dụng Giấy Phép Aspose OCR (Cần Thiết cho Môi Trường Sản Xuất)

Trước khi bạn có thể gọi bất kỳ API OCR nào, bạn phải tải một giấy phép hợp lệ; nếu không bạn sẽ bị giới hạn bởi phiên bản dùng thử.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Lý do quan trọng*: Một engine có giấy phép sẽ mở khóa hỗ trợ GPU, độ chính xác cao hơn, và loại bỏ watermark mà nếu không sẽ làm tăng kích thước PDF của bạn.

---

## Bước 2: Cấu Hình Engine OCR – Luồng, GPU, và Sửa Lỗi Chính Tả

Một engine OCR nhanh là nền tảng của bất kỳ công việc **batch OCR to PDF** nào. Chúng ta sẽ khởi tạo số luồng tối đa mà CPU có thể xử lý, bật tăng tốc GPU (nếu bạn có card tương thích), và tăng cường sửa lỗi chính tả để làm sạch các lỗi OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro tip*: Nếu bạn đang chạy trên server không có giao diện (headless) và không có GPU, chỉ cần đặt `gpu.setEnabled(false)` – mã vẫn hoạt động, chỉ chậm hơn một chút.

---

## Bước 3: Xây Dựng Pipeline Tiền Xử Lý Ảnh

Các bản scan thô thường bị nhiễu, độ tương phản thấp, hoặc ánh sáng không đồng đều. **Image preprocessing for OCR** cải thiện đáng kể tỷ lệ nhận dạng, đặc biệt trong các trường hợp **recognize text JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Vì sao chúng ta xâu chuỗi các bước này*: Loại bỏ nhiễu trước sẽ ngăn bộ nhị phân hoá làm tăng các đốm nhiễu; tăng độ tương phản sau đó giúp các ký tự nổi bật; cuối cùng, nhị phân hoá cung cấp cho engine OCR một hình ảnh nhị phân sạch sẽ để làm việc.

---

## Bước 4: Chuẩn Bị PdfSaveOptions – **Compress PDF Images** Một Cách Hiệu Quả

Aspose cho phép bạn tinh chỉnh đầu ra PDF. Chúng ta sẽ bật nén hình ảnh và đặt mức chất lượng cân bằng giữa kích thước và độ rõ nét.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Kết quả*: Mỗi PDF có thể tìm kiếm sẽ nhỏ hơn đáng kể—lý tưởng cho việc lưu trữ hoặc gửi qua email.

---

## Bước 5: Xử Lý Thư Mục – **Convert PNG to PDF** và **Recognize Text JPG** Trong Một Vòng Lặp

Bây giờ chúng ta kết hợp mọi thứ lại. Vòng lặp sẽ duyệt qua thư mục đầu vào, thực hiện OCR trên mỗi PNG hoặc JPG, và ghi một PDF có thể tìm kiếm vào thư mục đầu ra. Tên PDF sẽ giống với tên ảnh nguồn.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Kết Quả Dự Kiến

Chạy chương trình sẽ in ra một dòng cho mỗi ảnh, ví dụ:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Mở bất kỳ PDF nào được tạo ra trong trình xem và bạn sẽ thấy văn bản có thể chọn, tìm kiếm được, trong khi kích thước tệp thường **nhỏ hơn 30‑50 %** so với phiên bản không nén.

---

## Các Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

### Nếu server của tôi không có GPU thì sao?
Chỉ cần đặt `gpuSettings.setEnabled(false)`. Phần còn lại của pipeline không thay đổi, và bạn vẫn nhận được xử lý đa luồng trên CPU.

### PDF của tôi vẫn quá lớn—có thể giảm chất lượng hơn không?
Có. Điều chỉnh `options.setImageQuality(70)` hoặc thậm chí `50`. Giá trị thấp hơn sẽ giảm kích thước mạnh hơn nhưng có thể làm mờ các glyph nhỏ. Hãy thử nghiệm với một mẫu đại diện.

### Làm sao xử lý các định dạng ảnh khác (TIFF, BMP)?
Thêm các phần mở rộng vào lambda lọc:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Pipeline tiền xử lý giống nhau sẽ hoạt động cho hầu hết các định dạng raster.

### Tôi có muốn giữ lại ảnh màu gốc thay vì nhị phân hoá không?
Thay `.addBinarize()` bằng `.addGrayscale()` trong builder của preprocessor nếu bạn cần giữ màu cho các phân tích tiếp theo.

---

## Mẹo Chuyên Gia cho Batch OCR Sẵn Sàng Sản Xuất

- **Quản lý bộ nhớ**: Tái sử dụng một đối tượng `OcrEngine` duy nhất (như trong ví dụ) để tránh tốn kém khi tạo/hủy đối tượng cho mỗi ảnh.
- **Xử lý lỗi**: Bao bọc khối xử lý từng tệp trong `try/catch` để ghi log lỗi mà không dừng toàn bộ batch.
- **Ghi log**: Sử dụng framework ghi log chuẩn (SLF4J, Log4j) thay vì `System.out.println` cho các giải pháp quy mô lớn.
- **Song song**: Đối với thư mục rất lớn, cân nhắc xử lý các thư mục con bằng parallel streams, nhưng cần chú ý tới việc tranh chấp GPU.
- **Bảo mật**: Lưu file giấy phép ra ngoài repository và bảo vệ bằng quyền truy cập hệ thống tập tin.

---

## Kết Luận

Chúng ta vừa chứng minh cách **compress PDF images** đồng thời thực hiện chuyển đổi **batch OCR to PDF** bao gồm **convert PNG to PDF**, **recognize text JPG**, và áp dụng một pipeline **image preprocessing for OCR** mạnh mẽ. Toàn bộ chương trình Java được đóng gói, chạy trên bất kỳ JDK hiện đại nào, và tạo ra các PDF có thể tìm kiếm, nhẹ nhàng, sẵn sàng lưu trữ hoặc phân tích tiếp theo.

Bước tiếp theo? Thử nghiệm các tham số tiền xử lý khác nhau, dùng các ngôn ngữ OCR ngoài tiếng Anh, hoặc tích hợp workflow vào một microservice Spring Boot giám sát thư mục và xử lý tệp ngay khi chúng xuất hiện. Các khái niệm cốt lõi—tải giấy phép, cấu hình engine, tiền xử lý, và nén PDF—vẫn giống nhau, mang lại nền tảng vững chắc cho bất kỳ dự án nào dựa trên OCR.

Có câu hỏi hoặc muốn chia sẻ các tùy chỉnh của bạn? Để lại bình luận bên dưới, chúc bạn lập trình vui vẻ!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")


## Bạn Nên Học Gì Tiếp Theo?


Các tutorial sau đây đề cập đến các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm mã nguồn đầy đủ, ví dụ hoạt động và giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}