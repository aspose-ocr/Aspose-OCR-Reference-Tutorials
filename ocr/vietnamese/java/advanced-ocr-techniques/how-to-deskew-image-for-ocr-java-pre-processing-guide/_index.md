---
category: general
date: 2026-03-18
description: Cách chỉnh nghiêng ảnh nhanh chóng bằng Aspose OCR Java. Tìm hiểu cách
  tiền xử lý ảnh cho OCR, làm sạch ảnh quét và cải thiện độ chính xác của OCR chỉ
  trong vài bước.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: vi
og_description: Cách chỉnh nghiêng ảnh bằng Aspose OCR Java, tiền xử lý ảnh cho OCR,
  làm sạch ảnh quét và cải thiện độ chính xác của OCR.
og_title: Cách loại bỏ nghiêng ảnh cho OCR – Hướng dẫn Java
tags:
- OCR
- Java
- Image Processing
title: Cách loại bỏ độ nghiêng của ảnh cho OCR – Hướng dẫn tiền xử lý Java
url: /vi/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Khử (Deskew) Hình Ảnh cho OCR – Hướng Dẫn Tiền Xử Lý Java

Bạn đã bao giờ tự hỏi **cách định khử (deskew) hình ảnh** khi chúng được quét ra với góc lệch lạ không? Bạn không phải là người duy nhất—nhiều nhà phát triển gặp phải vấn đề này khi cố gắng trích xuất văn bản từ các tài liệu chứa nhiều hình ảnh. Tin tốt là gì? Chỉ với vài dòng Java và Aspose OCR, bạn có thể làm thẳng, giảm nhiễu và lấy được văn bản sạch sẽ mà không tốn công sức.

Trong hướng dẫn này, chúng ta sẽ đi qua toàn bộ quy trình: tải một bản quét nhiễu, bị xoay, áp dụng bộ lọc deskew, loại bỏ nhiễu hình ảnh, và cuối cùng **trích xuất văn bản từ hình ảnh**. Khi kết thúc, bạn sẽ biết cách **tiền xử lý hình ảnh cho OCR**, **làm sạch hình ảnh đã quét**, và **cải thiện độ chính xác OCR** cho bất kỳ dự án nào cần trích xuất văn bản đáng tin cậy.

## Những Gì Bạn Cần

- Java 17 (hoặc bất kỳ JDK nào mới) – mã sử dụng các tính năng chuẩn của ngôn ngữ.
- Thư viện Aspose OCR cho Java (bản dùng thử miễn phí hoạt động tốt cho việc thử nghiệm).
- Một hình mẫu vừa nhiễu vừa bị xoay (ví dụ: `noisy-rotated.png`).
- IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, VS Code…) – bất kỳ công cụ nào có thể biên dịch Java.

Không cần framework bổ sung, không cần thủ thuật Maven/Gradle; các câu lệnh import duy nhất là những gì được hiển thị bên dưới.

---

## Cách Định Khử (Deskew) Hình Ảnh với Aspose OCR

Điều đầu tiên cần giải quyết là độ nghiêng của hình ảnh. Nếu các dòng văn bản không nằm ngang, engine OCR sẽ đọc sai ký tự. `DeskewFilter` thực hiện phần công việc nặng.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Tại sao điều này quan trọng:** `DeskewFilter` phân tích hình học của ảnh, ước tính góc quay và xoay bitmap trở lại vị trí ngang. Nếu bỏ qua bước này, hầu hết các engine OCR sẽ coi các ký tự nghiêng như những glyph hoàn toàn khác, làm giảm nỗ lực **cải thiện độ chính xác OCR** của bạn.

> **Mẹo chuyên nghiệp:** Nếu bạn làm việc với các tài liệu có thể bị lộn ngược, hãy bật cờ `setAutoRotate` trên `DeskewFilter` (có sẵn trong các phiên bản Aspose mới). Nó sẽ tự động lật 180° khi cần.

![Sơ đồ hiển thị trước và sau khi quay – cách định khử (deskew) hình ảnh](https://example.com/deskew-diagram.png "ví dụ cách định khử (deskew) hình ảnh")

*Văn bản thay thế hình ảnh: ví dụ cách định khử (deskew) hình ảnh*

---

## Tiền Xử Lý Hình Ảnh cho OCR – Giảm Nhiễu và Làm Sạch

Khi hình ảnh đã thẳng, rào cản tiếp theo là nhiễu hình ảnh—những đốm, hiện tượng nén, hoặc các mẫu nền mờ gây rối cho engine OCR. `DenoiseFilter` áp dụng thuật toán làm mịn nhẹ nhàng, giữ lại các cạnh (các ký tự) đồng thời loại bỏ hạt nhiễu.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Khi Nào Điều Chỉnh Cài Đặt Giảm Nhiễu

- **Quét rất tối:** Tăng độ mạnh của bộ lọc (`denoiseFilter.setStrength(2)`) để loại bỏ bóng nền.
- **Phông chữ in mảnh:** Giảm độ mạnh để tránh làm mờ các nét serif nhỏ.
- **Tài liệu màu:** Chuyển sang thang độ xám trước (`scannedImage = scannedImage.toGrayscale();`)—engine OCR hoạt động tốt nhất trên ảnh đơn kênh.

Những điều chỉnh này là một phần của các thực hành tốt **làm sạch hình ảnh đã quét**; bitmap sạch hơn sẽ trực tiếp mang lại điểm tin cậy cao hơn từ engine OCR.

---

## Trích Xuất Văn Bản từ Hình Ảnh – Chạy Engine OCR

Bây giờ hình ảnh đã thẳng và sạch sẽ, đã đến lúc **trích xuất văn bản từ hình ảnh**. Lớp `OcrEngine` xử lý mọi thứ phía sau: phân đoạn, phân loại ký tự và mô hình ngôn ngữ.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Kết Quả Dự Kiến

Nếu tệp nguồn của bạn chứa dòng “**Invoice # 12345**”, console sẽ in ra một thứ gì đó như:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Nếu kết quả xuất ra bị rối, hãy kiểm tra lại các bước trước—đặc biệt là việc định khử (deskew). Ngay cả độ nghiêng 1 độ cũng có thể làm hỏng số và ký hiệu.

---

## Những Cạm Bẫy Thường Gặp & Mẹo Để **Cải Thiện Độ Chính Xác OCR**

| Vấn đề | Tại sao ảnh hưởng đến độ chính xác | Cách khắc phục nhanh |
|--------|-----------------------------------|----------------------|
| **Xoay dư** | OCR mong đợi các đường cơ sở nằm ngang. | Kiểm tra bằng `deskewFilter.getAngle()` và ghi lại giá trị. |
| **Giảm nhiễu quá mức** | Làm mờ các nét mỏng, biến “i” thành “l”. | Sử dụng `setStrength(0.5)` cho phông chữ mỏng. |
| **Định dạng ảnh sai** | Nén JPEG tạo ra các hiện tượng nhiễu. | Ưu tiên PNG hoặc TIFF để lưu trữ không mất dữ liệu. |
| **Ngôn ngữ không đúng** | Engine mặc định tiếng Anh; các bảng chữ cái khác cần thiết lập rõ ràng. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **DPI thấp (≤150)** | Không đủ dữ liệu pixel để phân đoạn đáng tin cậy. | Làm lại mẫu ở 300 DPI trước khi xử lý (`scannedImage = scannedImage.resample(300);`). |

### Thêm: Xử Lý Hàng Loạt

Nếu bạn có một thư mục chứa các bản quét, hãy bao quanh demo trong một vòng lặp:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Mẫu này cho phép bạn **tiền xử lý hình ảnh cho OCR** ở quy mô lớn, giữ cho mã nguồn gọn gàng và hiệu năng dự đoán được.

---

## Tóm Tắt & Các Bước Tiếp Theo

Chúng ta đã đề cập tới **cách định khử (deskew) hình ảnh** files, **tiền xử lý hình ảnh cho OCR**, và cuối cùng **trích xuất văn bản từ hình ảnh** bằng Aspose OCR Java. Bằng cách làm thẳng bản quét, loại bỏ nhiễu và cung cấp một bitmap sạch sẽ cho engine, bạn sẽ **cải thiện độ chính xác OCR** một cách đáng kể trên mọi dự án.

Tiếp theo? Hãy cân nhắc các mở rộng sau:

- **Phát hiện ngôn ngữ** – chuyển `ocrEngine.setLanguage` dựa trên script được phát hiện.
- **Xuất PDF** – đưa văn bản đã nhận dạng vào trình tạo PDF để tạo tài liệu có thể tìm kiếm.
- **Xử lý hậu kỳ bằng Machine‑learning** – chạy kiểm tra chính tả hoặc từ điển tùy chỉnh trên kết quả OCR.

Hãy thử những ý tưởng này, thí nghiệm với các mức độ mạnh của bộ lọc khác nhau, và bạn sẽ sớm có một quy trình vững chắc cho bất kỳ dự án số hoá tài liệu nào.

---

*Chúc lập trình vui vẻ! Nếu gặp khó khăn, hãy để lại bình luận bên dưới—tôi sẽ giúp bạn tinh chỉnh các tham số deskew và denoise.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}