---
category: general
date: 2026-02-14
description: Trích xuất văn bản từ hình ảnh bằng Aspose OCR. Tìm hiểu cách tải hình
  ảnh cho OCR, đọc văn bản từ hình chữ nhật và làm theo hướng dẫn Aspose OCR này trong
  vài phút.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: vi
og_description: Trích xuất văn bản từ hình ảnh ngay lập tức. Hướng dẫn này chỉ cách
  tải hình ảnh cho OCR, đọc văn bản từ hình chữ nhật và hoàn thành một bài hướng dẫn
  OCR của Aspose.
og_title: Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Hướng dẫn nhanh
tags:
- Aspose
- OCR
- Java
title: Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Demo từng bước
url: /vi/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trích xuất văn bản từ hình ảnh bằng Aspose OCR – Demo từng bước

Bạn đã bao giờ cần **extract text from image** nhưng không chắc bắt đầu từ đâu? Bạn không đơn độc—nhiều nhà phát triển gặp khó khăn này khi lần đầu tiên thực hiện quét biên lai hoặc xác thực CMND. Tin tốt? Với Aspose OCR, bạn có thể tải một hình ảnh, xác định vùng chính xác chứa văn bản, và lấy các ký tự ra chỉ trong vài dòng.

Trong **aspose ocr tutorial** này, chúng ta sẽ đi qua mọi thứ bạn cần: tải hình ảnh cho OCR, thiết lập một hình chữ nhật chỉ cho engine biết nơi cần tìm, và cuối cùng đọc văn bản đã trích xuất. Khi kết thúc, bạn sẽ có một chương trình Java có thể chạy được, in văn bản ROI ra console—không có bí ẩn, chỉ là một giải pháp rõ ràng, hoạt động.

## Những gì bạn cần

| Prerequisite | Why it matters |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR được cung cấp dưới dạng thư viện Java; bất kỳ JDK hiện đại nào cũng được. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Cung cấp các lớp `OcrEngine`, `ImageStream`, và các lớp liên quan. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | Chúng ta sẽ chỉ định engine tới một hình chữ nhật bên trong tệp này. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Giúp bạn biên dịch và chạy mẫu nhanh chóng. |

Nếu bạn đang sử dụng Maven, thêm phụ thuộc này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Mẹo chuyên nghiệp:** Số phiên bản ở trên là hiện tại tính đến tháng 2 2026. Cập nhật lên phiên bản mới nhất sẽ đảm bảo bạn nhận được các bản sửa lỗi và cải thiện hiệu năng.

## Bước 1 – Khởi tạo OCR Engine

Điều đầu tiên cần làm: bạn cần một thể hiện của `OcrEngine`. Hãy nghĩ nó như bộ não sẽ phân tích các pixel.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Tại sao tạo như vậy? Aspose tách engine (nơi chứa cấu hình) ra khỏi dữ liệu hình ảnh, cho phép bạn linh hoạt tái sử dụng cùng một engine cho nhiều hình ảnh nếu muốn.

## Bước 2 – Tải hình ảnh cho OCR

Bây giờ chúng ta thực sự **load image for OCR**. Trợ giúp `ImageStream.fromFile` đọc tệp vào một stream mà Aspose có thể hiểu.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Nếu không tìm thấy tệp, engine sẽ ném một ngoại lệ, vì vậy bạn có thể muốn bọc đoạn này trong khối try‑catch trong mã sản xuất. Đối với demo này, chúng tôi để ngoại lệ lan lên—giữ ví dụ gọn gàng.

## Bước 3 – Định nghĩa Hình chữ nhật (Read Text from Rectangle)

Đây là nơi phần **read text from rectangle** tỏa sáng. Bạn chỉ định cho engine chính xác nơi cần tìm, giúp tăng tốc xử lý và giảm kết quả sai.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Tại sao lại là hình chữ nhật?**  
> Hầu hết tài liệu có bố cục dự đoán được—ví dụ một biên lai, số tiền luôn xuất hiện gần đáy. Bằng cách tập trung vào phần đó, OCR engine bỏ qua các đồ họa không liên quan và tăng độ chính xác.

**Trường hợp biên:** Nếu hình chữ nhật vượt quá giới hạn của hình ảnh, Aspose sẽ tự động cắt, nhưng bạn sẽ mất dữ liệu. Một kiểm tra nhanh có thể ngăn điều này:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Bước 4 – Xử lý hình ảnh

Khi mọi thứ đã sẵn sàng, chúng ta yêu cầu engine thực hiện phép màu của nó.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

Lệnh `process()` trả về một đối tượng `OcrResult` chứa văn bản đã trích xuất, điểm tin cậy, và thậm chí các hộp bao quanh cho mỗi từ nếu bạn cần sau này.

## Bước 5 – Xuất văn bản đã trích xuất

Cuối cùng, in kết quả. Trong một ứng dụng thực tế, bạn có thể lưu vào cơ sở dữ liệu hoặc truyền cho dịch vụ khác, nhưng cho tutorial này, việc in ra console là đủ.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Kết quả mong đợi** (giả sử hình chữ nhật đã bắt được tổng số tiền trên biên lai):

```
ROI text:
$12.34
```

Nếu ROI trống hoặc hình ảnh mờ, bạn sẽ thấy một chuỗi rỗng hoặc ký tự rối. Điều chỉnh hình chữ nhật, cải thiện chất lượng ảnh, hoặc bật các tùy chọn tiền xử lý của Aspose (ví dụ, `setAutoSkewCorrection(true)`).

## Ví dụ Hoạt động đầy đủ

Dưới đây là chương trình hoàn chỉnh, sẵn sàng chạy. Sao chép‑dán vào một tệp có tên `RoiDemo.java`, điều chỉnh đường dẫn ảnh, và chạy `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Xác minh kết quả:** Sau khi chạy, so sánh đầu ra console với văn bản thực tế bên trong hình chữ nhật. Nếu khớp, bạn đã thành công **extract text from image** bằng Aspose OCR.

## Câu hỏi thường gặp & Mẹo

### Nếu tôi cần xử lý nhiều ROI trong cùng một hình ảnh thì sao?

Tạo một `Rectangle` mới cho mỗi khu vực, gọi lại `setRegionOfInterest`, và chạy lại `process()`. Engine sẽ tái sử dụng cùng dữ liệu hình ảnh, vì vậy hiệu năng vẫn nhanh.

### Aspose xử lý các ngôn ngữ hoặc phông chữ khác nhau như thế nào?

Bạn có thể chuyển mô hình ngôn ngữ bằng `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Đối với các script không phải Latin, tải gói ngôn ngữ phù hợp (có sẵn trên trang tải xuống của Aspose).

### Thư viện có hỗ trợ đầu vào PDF không?

Có—Aspose OCR có thể nhận trực tiếp các stream PDF. Chỉ cần thay `ImageStream.fromFile` bằng `ImageStream.fromPdfFile("doc.pdf")` và tùy chọn chỉ định số trang.

### Tôi có thể cải thiện độ chính xác trên các bản quét chất lượng thấp không?

Bật tiền xử lý:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Kết luận

Chúng ta vừa đi qua một **aspose ocr tutorial** hoàn chỉnh, cho thấy cách **extract text from image**, **load image for OCR**, và **read text from rectangle** bằng Java. Các bước chính là khởi tạo engine, cung cấp một hình ảnh, định nghĩa vùng quan tâm, xử lý, và cuối cùng in kết quả.

Từ đây bạn có thể khám phá:

* **Batch processing** – lặp qua một thư mục các biên lai và lưu mỗi tổng vào cơ sở dữ liệu.  
* **Dynamic ROI detection** – sử dụng các thư viện xử lý ảnh (OpenCV) để tự động xác định các khối văn bản.  
* **Post‑processing** – áp dụng regex hoặc fuzzy matching để làm sạch các lỗi OCR.

Hãy thử những ý tưởng này, điều chỉnh hình chữ nhật cho phù hợp với tài liệu của bạn, và bạn sẽ có một pipeline trích xuất văn bản mạnh mẽ trong thời gian ngắn. Chúc lập trình vui!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}