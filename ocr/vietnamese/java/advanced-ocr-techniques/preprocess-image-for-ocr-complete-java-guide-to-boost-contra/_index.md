---
category: general
date: 2026-02-17
description: Tiền xử lý hình ảnh cho OCR với Aspose OCR trong Java. Học cách tăng
  độ tương phản của hình ảnh, đặt mức độ tương phản và nhận dạng văn bản từ hình ảnh
  chỉ trong vài phút.
draft: false
keywords:
- preprocess image for ocr
- boost image contrast
- recognize text from image
- extract text using OCR
- set contrast level
language: vi
og_description: Tiền xử lý hình ảnh cho OCR bằng Aspose OCR Java. Hướng dẫn này cho
  thấy cách tăng độ tương phản của hình ảnh, thiết lập mức độ tương phản và nhận dạng
  văn bản từ hình ảnh một cách nhanh chóng.
og_title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Java để tăng độ tương phản & trích
  xuất văn bản
tags:
- Java
- OCR
- Image Processing
title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Java toàn diện để tăng độ tương phản
  & trích xuất văn bản
url: /vi/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý ảnh cho OCR – Hướng dẫn Java đầy đủ

Bạn đã bao giờ cần **tiền xử lý ảnh cho OCR** nhưng không chắc những cài đặt nào thực sự tạo ra sự khác biệt? Bạn không đơn độc. Hầu hết các nhà phát triển chỉ đưa một ảnh vào engine OCR và hy vọng phép màu sẽ xảy ra, nhưng kết quả lại rối rắm. Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực tế, từ đầu đến cuối, **tăng độ tương phản của ảnh**, điều chỉnh **mức độ tương phản**, và cuối cùng **nhận dạng văn bản từ ảnh** bằng Aspose OCR cho Java.

Khi hoàn thành, bạn sẽ có một đoạn mã có thể tái sử dụng để **trích xuất văn bản bằng OCR** một cách đáng tin cậy, ngay cả trên các bản quét nhiễu. Không có thủ thuật ẩn, chỉ có các bước rõ ràng và lý do đằng sau mỗi bước.

## Những gì bạn cần

- Java 17 hoặc mới hơn (mã sẽ biên dịch với bất kỳ JDK nào gần đây)
- Thư viện Aspose OCR cho Java (tải về từ trang chính thức của Aspose)
- Tệp giấy phép Aspose OCR hợp lệ (`Aspose.OCR.lic`)
- Ảnh đầu vào (`input.jpg`) mà bạn muốn đọc
- IDE yêu thích hoặc môi trường dòng lệnh đơn giản

Nếu bạn đã có những thứ này, tuyệt vời—hãy bắt đầu ngay.

## Bước 1: Tải giấy phép Aspose OCR (Cài đặt chính)

Trước khi engine OCR làm bất kỳ việc gì, nó cần biết rằng bạn đã có giấy phép. Nếu không, bạn sẽ gặp watermark bản dùng thử.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Tại sao điều này quan trọng:** Không có giấy phép hợp lệ, engine sẽ chạy ở chế độ đánh giá, có thể cắt ngắn kết quả hoặc thêm watermark. Đặt giấy phép ngay từ đầu cũng đảm bảo rằng mọi tùy chọn tiền xử lý sau này được áp dụng trong chế độ đầy đủ tính năng.

## Bước 2: Khởi tạo OCR Engine

Tạo một thể hiện `OcrEngine` sẽ cho bạn quyền truy cập cả vào pipeline nhận dạng và tiền xử lý.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**Mẹo chuyên nghiệp:** Giữ engine dưới dạng singleton nếu bạn dự định xử lý nhiều ảnh trong một batch; nó sẽ cache các tài nguyên nội bộ và tăng tốc các lần gọi tiếp theo.

## Bước 3: Cấu hình tiền xử lý – Độ nghiêng, Khử nhiễu và Tăng cường Độ tương phản

Đây là nơi chúng ta **tiền xử lý ảnh cho OCR**. Ba nút chúng ta sẽ điều chỉnh là:

1. **Deskew** – sửa các góc quay nhẹ.
2. **Denoise** – loại bỏ các điểm nhiễu gây rối việc phân đoạn ký tự.
3. **Contrast enhancement** – làm cho văn bản tối nổi bật hơn so với nền.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Tại sao cần điều chỉnh Mức độ tương phản?

Tăng mức độ tương phản sẽ kéo dài histogram của ảnh, làm cho các pixel tối trở nên tối hơn và các pixel sáng trở nên sáng hơn. Trong thực tế, **mức độ tương phản** `1.3f` thường cho cân bằng tốt nhất cho tài liệu in, trong khi giá trị trên `1.5f` có thể làm quá sáng các nét mỏng. Hãy thoải mái thử nghiệm; cài đặt này thay đổi nhanh và có thể cải thiện đáng kể tỷ lệ **nhận dạng văn bản từ ảnh**.

## Bước 4: Chuẩn bị Ảnh Đầu vào

Lớp `OcrInput` trừu tượng hoá việc xử lý tệp. Bạn có thể thêm nhiều ảnh nếu cần xử lý batch.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Trường hợp biên:** Nếu ảnh của bạn ở định dạng không chuẩn (ví dụ, TIFF có nhiều trang), bạn có thể tải từng trang riêng biệt hoặc chuyển đổi sang PNG/JPEG trước.

## Bước 5: Thực hiện Nhận dạng

Bây giờ engine sẽ chạy pipeline tiền xử lý mà chúng ta vừa cấu hình, sau đó chuyển ảnh đã được làm sạch cho thuật toán OCR cốt lõi.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Điều gì đang diễn ra phía sau?** Aspose OCR đầu tiên áp dụng phép biến đổi deskew, sau đó chạy bộ lọc denoise, và cuối cùng điều chỉnh độ tương phản trước khi đưa ảnh vào bộ nhận dạng dựa trên mạng nơ-ron. Thứ tự này được thiết kế cố ý; thay đổi nó có thể dẫn đến kết quả không tối ưu.

## Bước 6: Xuất Văn bản Đã Nhận dạng

Cuối cùng, chúng ta in chuỗi đã trích xuất ra console. Trong một ứng dụng thực tế, bạn có thể ghi nó vào tệp hoặc gửi qua mạng.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Kết quả Dự kiến

Nếu `input.jpg` chứa cụm từ “Hello World!”, console sẽ hiển thị:

```
Hello World!
```

Nếu đầu ra bị rối, hãy kiểm tra lại các giá trị tiền xử lý—đặc biệt là **mức độ tương phản** và **chế độ denoise**—và thử một định dạng ảnh khác.

## Bonus: Visualising the Pre‑Processed Image (Optional)

Đôi khi bạn muốn xem engine nhìn thấy gì sau khi đã deskew, denoise và tăng cường độ tương phản. Aspose OCR cho phép bạn xuất bitmap trung gian:

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

Mở `processed.png` cạnh nhau với ảnh gốc; bạn sẽ nhận thấy đường chân trời thẳng hơn và văn bản sắc nét hơn. Bước này hữu ích khi bạn đang khắc phục lý do một bản quét cụ thể thất bại.

![ví dụ tiền xử lý ảnh cho OCR](/images/ocr-preprocess-example.png "tiền xử lý ảnh cho OCR – trước và sau khi tăng độ tương phản")

*Hình ảnh trên minh họa cách tăng độ tương phản và khử nhiễu biến một bản quét mờ thành một bức ảnh sạch, sẵn sàng cho OCR.*

## Những Sai Lầm Thường Gặp & Cách Tránh

| Sai lầm | Tại sao xảy ra | Cách khắc phục |
|---------|----------------|----------------|
| **Quá tăng độ tương phản** (`setContrastLevel` quá cao) | Nền sáng trở nên trắng, xóa bỏ các ký tự mờ | Giữ mức giữa 1.1 và 1.4 cho hầu hết văn bản in |
| **Độ dung sai deskew quá thấp** | Các góc quay nhỏ không được chỉnh sửa | Tăng `setDeskewAngleTolerance` lên 0.2 hoặc 0.3 cho sách quét |
| **Dùng GAUSSIAN denoise trên ảnh nhị phân** | Làm mờ các cạnh, gộp ký tự | Dùng `DenoiseMode.MEDIAN` cho ảnh đen‑trắng |
| **Thiếu giấy phép** | Engine chuyển sang chế độ dùng thử, cắt ngắn đầu ra | Kiểm tra đường dẫn tới `Aspose.OCR.lic` và đảm bảo tệp có thể đọc được |

## Các Bước Tiếp Theo: Vượt Qua Tiền Xử Lý Cơ Bản

Bây giờ bạn đã có thể **tiền xử lý ảnh cho OCR** và **trích xuất văn bản bằng OCR**, hãy cân nhắc các mở rộng sau:

- **Gói ngôn ngữ** – tải các từ điển ngôn ngữ cụ thể để cải thiện độ chính xác cho văn bản không phải tiếng Anh.
- **Cắt vùng quan tâm (ROI)** – tập trung vào một phần của ảnh nếu bạn chỉ cần một đoạn của trang.
- **Xử lý batch** – lặp qua một thư mục ảnh, tái sử dụng cùng một thể hiện `OcrEngine` để tăng tốc.
- **Tích hợp với PDF** – kết hợp Aspose OCR với Aspose PDF để chuyển PDF quét thành PDF có thể tìm kiếm trong một pipeline duy nhất.

Mỗi chủ đề này tự nhiên sẽ bao gồm các từ khóa phụ của chúng ta: bạn vẫn sẽ **tăng độ tương phản ảnh**, **đặt mức độ tương phản**, và tiếp tục **nhận dạng văn bản từ ảnh** trong nhiều kịch bản.

## Kết luận

Chúng ta đã bao quát mọi thứ cần thiết để **tiền xử lý ảnh cho OCR** bằng Aspose OCR cho Java: tải giấy phép, cấu hình deskew, denoise và tăng cường độ tương phản, đưa ảnh vào và cuối cùng **nhận dạng văn bản từ ảnh**. Với ví dụ hoàn chỉnh, có thể chạy ngay, bạn giờ có thể **trích xuất văn bản bằng OCR** trên bất kỳ ảnh đã được chuẩn bị phù hợp nào.

Hãy chạy thử mã, điều chỉnh **mức độ tương phản**, và quan sát độ chính xác tăng lên. Khi đã sẵn sàng, khám phá các mô hình ngôn ngữ riêng hoặc pipeline batch để biến demo ảnh đơn thành giải pháp cấp sản xuất.

*Chúc lập trình vui vẻ, và mong các bản quét của bạn luôn sắc nét!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}