---
category: general
date: 2026-02-22
description: Cách sử dụng OCR trong Java để trích xuất văn bản từ hình ảnh, cải thiện
  độ chính xác của OCR và tải hình ảnh cho OCR với các ví dụ mã thực tế.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: vi
og_description: Cách sử dụng OCR trong Java để trích xuất văn bản từ hình ảnh và cải
  thiện độ chính xác của OCR. Hãy theo dõi hướng dẫn này để có một ví dụ sẵn sàng
  chạy.
og_title: Cách sử dụng OCR trong Java – Hướng dẫn chi tiết từng bước
tags:
- OCR
- Java
- Image Processing
title: Cách sử dụng OCR trong Java – Hướng dẫn chi tiết từng bước
url: /vi/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong Java – Hướng Dẫn Toàn Diện Từng Bước

Bạn đã bao giờ cần **cách sử dụng OCR** trên một ảnh chụp màn hình bị nghiêng và tự hỏi tại sao kết quả lại giống như một mớ hỗn độn? Bạn không phải là người duy nhất. Trong nhiều ứng dụng thực tế—quét biên lai, số hoá biểu mẫu, hoặc lấy văn bản từ meme—đạt được kết quả đáng tin cậy phụ thuộc vào một vài cài đặt đơn giản.

Trong hướng dẫn này, chúng tôi sẽ trình bày **cách sử dụng OCR** để *trích xuất văn bản từ tệp hình ảnh*, cho bạn biết cách **cải thiện độ chính xác của OCR**, và minh họa cách **tải hình ảnh cho OCR** một cách đúng đắn bằng một thư viện OCR phổ biến cho Java. Khi kết thúc, bạn sẽ có một chương trình tự chứa có thể đưa vào bất kỳ dự án nào.

## Những Điều Bạn Sẽ Học

- Mã chính xác bạn cần để **load image for OCR** (không có phụ thuộc ẩn).
- Các cờ tiền xử lý nào tăng **improve OCR accuracy** và tại sao chúng quan trọng.
- Cách đọc kết quả OCR và in ra console.
- Các lỗi thường gặp—như quên thiết lập vùng quan tâm (region of interest) hoặc bỏ qua giảm nhiễu—và cách tránh chúng.

### Yêu Cầu Trước

- Java 17 hoặc mới hơn (mã sẽ biên dịch với bất kỳ JDK nào gần đây).
- Một thư viện OCR cung cấp các lớp `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput`, và `OcrResult` (ví dụ, gói giả `com.example.ocr` được dùng trong đoạn mã). Thay thế bằng thư viện thực tế bạn đang sử dụng.
- Một hình ảnh mẫu (`skewed_noisy.png`) được đặt trong thư mục bạn có thể tham chiếu.

> **Mẹo chuyên nghiệp:** Nếu bạn đang sử dụng SDK thương mại, hãy chắc chắn tệp giấy phép nằm trong classpath của bạn; nếu không, engine sẽ ném lỗi khởi tạo.

---

## Bước 1: Tạo Một Instance của OCR Engine – **how to use OCR** hiệu quả

Điều đầu tiên bạn cần là một đối tượng `OcrEngine`. Hãy nghĩ nó như bộ não sẽ giải mã các pixel.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Tại sao điều này quan trọng:* Nếu không có engine, bạn sẽ không có ngữ cảnh cho các mô hình ngôn ngữ, bộ ký tự, hoặc các heuristics hình ảnh. Khởi tạo sớm cũng cho phép bạn gắn các tùy chọn tiền xử lý sau này.

---

## Bước 2: Cấu Hình Tiền Xử Lý Hình Ảnh – **improve OCR accuracy**

Tiền xử lý là công thức bí mật biến một bản quét nhiễu thành văn bản sạch, có thể đọc được bởi máy. Dưới đây chúng tôi bật deskew, giảm nhiễu mức cao, tự động tăng tương phản, và một vùng quan tâm (ROI) để tập trung vào phần hình ảnh liên quan.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Tại sao điều này quan trọng:*  
- **Deskew** căn chỉnh văn bản bị xoay, điều này rất cần thiết khi quét biên lai không hoàn toàn phẳng.  
- **Noise reduction** loại bỏ các pixel lẻ lùng mà nếu không sẽ bị hiểu là ký tự.  
- **Auto‑contrast** mở rộng dải tông, làm cho các ký tự mờ nổi bật hơn.  
- **ROI** chỉ cho engine bỏ qua các viền không liên quan, tiết kiệm thời gian và bộ nhớ.

Nếu bạn bỏ qua bất kỳ mục nào trong số này, bạn có thể sẽ thấy giảm hiệu suất **improve OCR accuracy**.

---

## Bước 3: Tải Hình Ảnh cho OCR – **load image for OCR** đúng cách

Bây giờ chúng ta thực sự chỉ định engine tới tệp mà chúng ta muốn đọc. Lớp `OcrInput` có thể chấp nhận nhiều hình ảnh, nhưng trong ví dụ này chúng tôi giữ cho nó đơn giản.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Tại sao điều này quan trọng:* Đường dẫn phải là tuyệt đối hoặc tương đối so với thư mục làm việc; nếu không engine sẽ ném `FileNotFoundException`. Ngoài ra, lưu ý rằng tên phương thức `add` gợi ý bạn có thể xếp hàng nhiều hình ảnh—rất hữu ích cho xử lý hàng loạt.

---

## Bước 4: Thực Hiện OCR và Xuất Văn Bản Được Nhận Diện – **how to use OCR** từ đầu tới cuối

Cuối cùng, chúng ta yêu cầu engine nhận dạng văn bản và in ra. Đối tượng `OcrResult` chứa chuỗi thô, điểm tin cậy, và siêu dữ liệu từng dòng (nếu bạn cần sau này).

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Kết quả mong đợi** (giả sử hình mẫu chứa “Hello, OCR World!”):

```
=== OCR Output ===
Hello, OCR World!
```

Nếu kết quả trông rối rắm, hãy quay lại Bước 2 và điều chỉnh các tùy chọn tiền xử lý—có thể giảm mức giảm nhiễu hoặc điều chỉnh hình chữ nhật ROI.

---

## Ví Dụ Đầy Đủ, Có Thể Chạy

Dưới đây là một chương trình Java hoàn chỉnh mà bạn có thể sao chép‑dán vào tệp có tên `OcrDemo.java`. Nó kết hợp mọi bước chúng ta đã thảo luận.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Lưu tệp, biên dịch bằng `javac OcrDemo.java`, và chạy `java OcrDemo`. Nếu mọi thứ được cấu hình đúng, bạn sẽ thấy văn bản đã trích xuất được in ra console.

---

## Câu Hỏi Thường Gặp & Trường Hợp Đặc Biệt

| Câu hỏi | Trả lời |
|----------|--------|
| **Nếu hình ảnh của tôi ở định dạng JPEG thì sao?** | Phương thức `OcrInput.add()` chấp nhận bất kỳ định dạng raster nào được hỗ trợ—PNG, JPEG, BMP, TIFF. Chỉ cần thay đổi phần mở rộng tệp trong đường dẫn. |
| **Tôi có thể xử lý nhiều trang cùng lúc không?** | Chắc chắn. Gọi `ocrInput.add()` cho mỗi tệp, sau đó truyền cùng một `ocrInput` vào `recognize()`. Engine sẽ trả về một `OcrResult` đã được nối lại. |
| **Nếu kết quả OCR rỗng thì sao?** | Kiểm tra lại xem ROI thực sự có chứa văn bản không. Cũng đảm bảo `setDeskewEnabled(true)` được bật; một góc quay 90° sẽ khiến engine nghĩ hình ảnh là trống. |
| **Làm sao để thay đổi mô hình ngôn ngữ?** | Hầu hết các thư viện cung cấp phương thức `setLanguage(String)` trên `OcrEngine`. Gọi nó trước `recognize()`, ví dụ `ocrEngine.setLanguage("eng")`. |
| **Có cách nào để lấy điểm tin cậy không?** | Có, `OcrResult` thường cung cấp `getConfidence()` cho mỗi dòng hoặc mỗi ký tự. Sử dụng nó để lọc các kết quả có độ tin cậy thấp. |

---

## Kết Luận

Chúng tôi đã trình bày **cách sử dụng OCR** trong Java từ đầu đến cuối: tạo engine, cấu hình tiền xử lý để **cải thiện độ chính xác của OCR**, **tải hình ảnh cho OCR** đúng cách, và cuối cùng in ra văn bản đã trích xuất. Đoạn mã hoàn chỉnh đã sẵn sàng chạy, và các giải thích trả lời câu hỏi “tại sao” cho mỗi dòng.

Sẵn sàng cho bước tiếp theo? Hãy thử thay đổi hình chữ nhật ROI để tập trung vào các phần khác nhau của hình ảnh, thử nghiệm với `NoiseReduction.MEDIUM`, hoặc tích hợp đầu ra vào PDF có thể tìm kiếm. Bạn cũng có thể khám phá các chủ đề liên quan như **extract text from image** bằng dịch vụ đám mây, hoặc xử lý hàng nghìn tệp theo lô với hàng đợi đa luồng.

Có thêm câu hỏi nào về OCR, tiền xử lý hình ảnh, hoặc tích hợp Java không? Hãy để lại bình luận, và chúc bạn lập trình vui vẻ! 

![Ví dụ cách sử dụng OCR](/images/ocr-demo.png "cách sử dụng OCR – Ví dụ Java hiển thị tiền xử lý và kết quả")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}