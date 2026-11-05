---
category: general
date: 2026-02-19
description: Học cách chỉnh nghiêng ảnh và loại bỏ nhiễu cho OCR. Hướng dẫn này chỉ
  cách nhận dạng ảnh văn bản, sửa góc quay của ảnh và tiền xử lý ảnh OCR bằng Aspose
  OCR.
draft: false
keywords:
- how to deskew image
- recognize text image
- how to remove noise
- correct image rotation
- preprocess image ocr
language: vi
og_description: Cách chỉnh nghiêng ảnh và loại bỏ nhiễu để bạn có thể nhận dạng văn
  bản nhanh chóng. Hãy làm theo hướng dẫn này để sửa góc quay của ảnh và tiền xử lý
  OCR ảnh bằng Aspose.
og_title: Cách chỉnh nghiêng ảnh – Hướng dẫn xử lý trước OCR đầy đủ
tags:
- OCR
- Java
- Image Processing
title: Cách chỉnh nghiêng ảnh — Hướng dẫn tiền xử lý OCR từng bước
url: /vi/java/ocr-operations/how-to-deskew-image-step-by-step-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Deskew Image — Hướng Dẫn Xử Lý Trước OCR Toàn Diện

Bạn đã bao giờ tự hỏi **how to deskew image** các tệp ảnh trước khi đưa chúng vào một engine OCR chưa? Có thể bạn đã quét một loạt biên lai, và các trang trông như đang nghiêng một chút, hoặc bản quét bị điểm nhiễu ngẫu nhiên. Đó là một vấn đề phổ biến—các hình ảnh nghiêng, nhiễu làm cho việc nhận dạng văn bản gặp khó khăn.  

Tin tốt? Bạn có thể chỉnh thẳng (correct image rotation) và loại bỏ nhiễu (how to remove noise) chỉ với vài dòng Java bằng cách sử dụng Aspose.OCR. Trong hướng dẫn này, chúng tôi sẽ đi qua toàn bộ quy trình: từ việc tải một PNG bị nhiễu‑và‑xoay, áp dụng deskew + median denoise, cho đến **recognize text image** và in kết quả. Khi kết thúc, bạn sẽ có một đoạn mã có thể tái sử dụng và chèn vào bất kỳ dự án Java nào.

## Những Gì Bạn Cần

- **Java 17** hoặc mới hơn (mã sẽ biên dịch với các phiên bản cũ hơn, nhưng 17 là lựa chọn tối ưu).  
- **Aspose.OCR for Java** – bạn có thể tải JAR mới nhất từ Maven Central (`com.aspose:aspose-ocr`).  
- Một tệp ảnh vừa bị xoay vừa nhiễu (ví dụ, `noisy-rotated.png`).  
- Một IDE cơ bản (IntelliJ, Eclipse, hoặc thậm chí VS Code).  

Không cần công cụ xây dựng phức tạp; chỉ cần chạy đơn giản với `javac` + `java` là đủ.

## Bước 1 – Tạo Instance của OCR Engine  

Điều đầu tiên bạn làm là khởi tạo một `OcrEngine`. Hãy nghĩ nó như bộ não sẽ đọc các ký tự cho bạn.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Mẹo:** Giữ engine dưới dạng singleton nếu bạn đang xử lý nhiều ảnh; nó sẽ tái sử dụng bộ nhớ trong và tăng tốc độ.

## Bước 2 – Bật Deskew và Median Denoise (How to Remove Noise)

Bây giờ chúng ta yêu cầu engine **correct image rotation** và **how to remove noise**. Cả hai bộ lọc đều tùy chọn, nhưng khi kết hợp chúng sẽ cải thiện độ chính xác đáng kể.

```java
        // Turn on preprocessing filters
        ocrEngine.getPreprocessing().setDeskew(true);          // fixes rotation
        ocrEngine.getPreprocessing().setMedianDenoise(true);   // smooths out speckles
```

Tại sao lại dùng median denoise? Nó bảo tồn các cạnh (các đường nét xác định ký tự) trong khi loại bỏ các pixel riêng lẻ—đúng là những gì bạn cần cho OCR sạch sẽ.

## Bước 3 – Tải Ảnh Bạn Muốn Xử Lý  

Ở đây chúng ta chỉ định engine tới tệp cần làm sạch. `ImageStream.fromFile` đọc PNG vào bộ nhớ.

```java
        // Load the noisy‑rotated image
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/noisy-rotated.png"));
```

Nếu ảnh của bạn nằm trên máy chủ từ xa, chỉ cần cung cấp một `InputStream` thay thế—Aspose sẽ xử lý một cách mượt mà.

## Bước 4 – Chạy OCR và Lấy Văn Bản Được Nhận Diện  

Với tiền xử lý được bật, engine bây giờ sẽ đọc ảnh đã được chỉnh sửa. Lệnh `recognize()` trả về một `RecognitionResult` chứa chuỗi đã trích xuất.

```java
        // Perform OCR – the engine automatically applies deskew & denoise first
        String recognizedText = ocrEngine.recognize().getText();

        // Show the output
        System.out.println("=== Recognized Text ===");
        System.out.println(recognizedText);
    }
}
```

Bạn sẽ thấy văn bản sạch sẽ, dễ đọc trên console, ngay cả khi ảnh gốc bị nghiêng và nhiễu.

## Bước 5 – Xác Minh Kết Quả (What to Expect)

Khi mọi thứ hoạt động, console sẽ in ra một thứ gì đó như:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑02‑15
Total: $1,234.56
```

Nếu đầu ra vẫn chứa các ký tự rối, hãy kiểm tra lại:

- Độ phân giải ảnh (≥ 300 dpi là lý tưởng).  
- Đường dẫn tệp đúng.  
- Liệu các bộ lọc bổ sung (ví dụ, `setContrastStretch`) có hữu ích không.

## Tùy Chọn: Xác Nhận Bằng Hình Ảnh Ví Dụ  

Dưới đây là một bản xem trước nhỏ của một biên lai bị xoay và nhiễu. Hãy chú ý đến độ nghiêng—code của chúng tôi sẽ chỉnh thẳng cho bạn.

![ví dụ cách deskew image](deskew-demo.png "cách deskew image")

*Văn bản thay thế: cách deskew image – trước và sau khi xử lý.*

## Câu Hỏi Thường Gặp

### Điều này có hoạt động với PDF hay chỉ PNG/JPEG?  

Aspose.OCR có thể đọc PDF trực tiếp; chỉ cần thay thế `ImageStream.fromFile` bằng `ImageStream.fromPdf`. Các cờ tiền xử lý vẫn được áp dụng, vì vậy bạn vẫn nhận được **how to deskew image** và **how to remove noise**.

### Nếu tôi cần giữ nguyên hướng gốc cho các bước sau thì sao?  

Bạn có thể sao chép ảnh trước khi tiền xử lý:

```java
Image original = ocrEngine.getImage().clone();
ocrEngine.getPreprocessing().apply(); // modifies the internal copy
// Use original later if needed
```

### Tôi có thể thay đổi góc deskew thủ công không?  

Có—`setDeskewAngle(double degrees)` cho phép bạn ghi đè thuật toán tự động phát hiện. Hữu ích khi auto‑detect thất bại với các góc xoay cực đoan.

### Median denoise khác gì so với Gaussian blur?  

Bộ lọc median thay thế mỗi pixel bằng giá trị trung vị của các pixel lân cận, giúp bảo tồn các cạnh. Gaussian blur làm mờ mọi thứ, có thể làm mờ nét ký tự—do đó median là lựa chọn an toàn hơn cho OCR.

## Tổng Kết  

Trong tutorial này, chúng tôi đã đề cập đến **how to deskew image** các tệp, trình diễn **how to remove noise**, và cho bạn thấy cách **recognize text image** bằng việc sử dụng tiền xử lý tích hợp của Aspose OCR. Bằng cách bật `setDeskew(true)` và `setMedianDenoise(true)`, bạn tự động **correct image rotation** và loại bỏ các điểm nhiễu, biến một bản quét lộn xộn thành một chuỗi văn bản sạch.

Hãy thoải mái thử nghiệm: thử các chiến lược denoise khác nhau, đưa PDF vào, hoặc nối nhiều ảnh trong một vòng lặp. Mẫu giống nhau—engine → preprocess → recognize—áp dụng cho mọi tình huống, tạo nền tảng vững chắc cho bất kỳ pipeline OCR nào.

**Các bước tiếp theo** bạn có thể khám phá:

- **Xử lý hàng loạt** – lặp qua một thư mục ảnh và ghi mỗi kết quả vào tệp `.txt`.  
- **Gói ngôn ngữ** – tải từ điển ngôn ngữ cụ thể để tăng độ chính xác cho văn bản không phải tiếng Anh.  
- **Bộ lọc nâng cao** – như `setContrastStretch` hoặc `setBinarization` cho các bản quét có độ tương phản thấp.  

Có thêm câu hỏi? Để lại bình luận, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}