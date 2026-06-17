---
category: general
date: 2026-05-06
description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose OCR trong Java. Học cách
  chuyển đổi hình ảnh sang PDF, bật sửa lỗi chính tả và sử dụng OCR GPU để có kết
  quả nhanh chóng.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: vi
og_description: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Aspose OCR trong Java. Hướng
  dẫn này chỉ cách chuyển hình ảnh sang PDF, bật sửa lỗi chính tả và sử dụng OCR GPU.
og_title: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Java OCR
tags:
- OCR
- Java
- PDF
title: Tạo PDF có thể tìm kiếm từ hình ảnh bằng Java OCR
url: /vi/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm từ Hình ảnh với Java OCR

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một bức ảnh đã quét nhưng không biết bắt đầu từ đâu? Bạn không đơn độc—hầu hết các nhà phát triển đều gặp khó khăn này khi lần đầu tiên xử lý PDF dựa trên hình ảnh. May mắn là, với Aspose OCR for Java, bạn có thể **chuyển đổi hình ảnh sang PDF**, biến văn bản thành nội dung có thể chọn, và thậm chí thêm tính năng sửa lỗi chính tả để có kết quả hoàn hảo.

Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ hoàn chỉnh, sẵn sàng chạy, cho thấy cách **sử dụng OCR GPU** khi có sẵn, cách **xử lý OCR hình ảnh** một cách hiệu quả, và lý do tại sao việc bật sửa lỗi chính tả lại quan trọng cho việc tìm kiếm sau này. Khi kết thúc, bạn sẽ có một cách chỉ một cú nhấp chuột để tạo PDF có thể tìm kiếm mà bạn có thể phát hành cho người dùng hoặc lưu trữ để tuân thủ.

> **Mẹo chuyên nghiệp:** Nếu bạn đang chạy trên máy không có GPU, mã sẽ tự động chuyển sang CPU, vì vậy bạn không cần phải viết lại bất kỳ gì.

---

## Những gì bạn cần

- **Java 8+** (mã biên dịch với JDK 8 và mới hơn)
- **Thư viện Aspose OCR for Java** (tải JAR mới nhất từ trang Aspose)
- Một **hình ảnh đầu vào** (JPEG, PNG, TIFF, v.v.) mà bạn muốn chuyển thành PDF có thể tìm kiếm
- (Tùy chọn) Một **GPU** hỗ trợ CUDA nếu bạn muốn nhận dạng nhanh nhất có thể

Không cần framework bổ sung, không cần mánh khóe Maven/Gradle—chỉ cần một JAR duy nhất trên classpath và bạn đã sẵn sàng.

## Bước 1: Khởi tạo Engine OCR – Trái tim của quá trình  

Đầu tiên chúng ta tạo một thể hiện `OcrEngine` và chỉ đến tệp nguồn. Đối tượng này là công cụ chính sẽ đọc hình ảnh, chạy mạng nơ-ron, và trả lại cho chúng ta văn bản.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Tại sao điều này quan trọng:* Khởi tạo engine một lần và tái sử dụng nó tránh được chi phí tải lại các thư viện gốc—một lợi thế hiệu năng nhỏ nhưng tích lũy khi bạn xử lý hàng chục tệp cùng lúc.

## Bước 2: Chọn Thiết bị Xử lý – Sử dụng OCR GPU Khi Có Thể  

Nếu workstation của bạn có GPU tương thích, bạn có thể yêu cầu Aspose chạy các tác vụ nặng trên đó. Nếu không, engine sẽ tự động chuyển sang CPU.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Lợi ích là gì?* Tăng tốc GPU có thể giảm vài giây cho mỗi trang, đặc biệt với các bản quét độ phân giải cao. Cơ chế dự phòng đảm bảo cùng một mã hoạt động ở mọi nơi, vì vậy chúng tôi khuyên dùng **use OCR GPU** làm cài đặt mặc định.

## Bước 3: Tăng tốc Quét – Tận dụng Tất cả các Nhân CPU  

Ngay cả khi GPU đang bận, các bước tiền xử lý xung quanh vẫn có thể được thực hiện song song. Đặt số lượng luồng bằng số bộ xử lý có sẵn cho phép engine xử lý nhiều phần cùng lúc.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Lưu ý:* Trên laptop 4 nhân, sẽ khởi tạo bốn luồng; trên workstation 16 nhân bạn sẽ nhận được lợi ích đầy đủ. Chỉ cần nhớ rằng nhiều luồng hơn đồng nghĩa với việc sử dụng bộ nhớ cao hơn.

## Bước 4: Làm sạch Hình ảnh – Bộ lọc Tiền xử lý  

Một bản quét mờ hoặc nhiễu sẽ tạo ra văn bản rác. Thêm một vài bộ lọc tích hợp sẽ cải thiện độ chính xác đáng kể.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Tại sao lại dùng các bộ lọc này?* `DeskewFilter` sửa lỗi xoay thường xảy ra khi tài liệu được đưa qua máy quét ở góc nghiêng. `NoiseRemovalFilter` loại bỏ các pixel lẻ mà nếu không sẽ bị hiểu nhầm thành ký tự. Hãy nghĩ rằng bạn đang cung cấp cho engine OCR một tờ giấy sạch để đọc.

## Bước 5: Bật Các Tính năng Thông minh – Kích hoạt Sửa lỗi Chính tả & Phát hiện Ngôn ngữ Tự động  

Nếu bạn đang xử lý tài liệu đa ngôn ngữ, hoặc chỉ muốn giảm lỗi chính tả, hãy bật bộ kiểm tra chính tả tích hợp và để engine đoán ngôn ngữ.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Khi nào điều này hữu ích?* Giả sử bản quét của bạn chứa cả phần tiếng Anh và tiếng Tây Ban Nha. Tính năng tự động phát hiện sẽ chuyển đổi từ điển ngay lập tức, trong khi sửa lỗi chính tả sẽ làm sạch các ký tự đọc sai như “0” thay vì “O”. Bước này là thiết yếu để tạo ra một **PDF có thể tìm kiếm** thực sự trả về kết quả chính xác.

## Bước 6: Lưu Kết quả – Chuyển Đổi Hình ảnh sang PDF và Làm cho Nó có thể Tìm kiếm  

Cuối cùng chúng ta yêu cầu engine ghi ra một PDF trong đó hình ảnh gốc nằm phía sau một lớp văn bản vô hình. Đây là quy trình **chuyển đổi hình ảnh sang PDF** truyền thống, nhưng PDF hiện đã có thể tìm kiếm.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Tệp đầu ra (`output-searchable.pdf`) có thể mở bằng bất kỳ trình xem PDF nào; bạn sẽ có thể chọn, sao chép và tìm kiếm văn bản như một PDF gốc. Không cần công cụ bổ sung.

## Ví dụ Hoạt động Đầy đủ – Dán và Chạy  

Dưới đây là toàn bộ chương trình, sẵn sàng biên dịch. Thay thế `YOUR_DIRECTORY` bằng thư mục chứa `input.jpg`.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Kết quả mong đợi:** Khi bạn chạy chương trình, sẽ thấy dòng console *“Searchable PDF generated successfully.”* Mở `output-searchable.pdf` trong Adobe Reader cho phép bạn gõ một từ từ hình ảnh gốc vào ô tìm kiếm và ngay lập tức nhảy tới vị trí của nó.

## Câu hỏi Thường gặp & Trường hợp Cạnh  

- **Nếu GPU không được phát hiện thì sao?**  
  Lệnh `setDeviceType(OcrDeviceType.GPU)` không gây lỗi; nó chỉ hướng dẫn engine thử GPU trước. Nếu thất bại, engine sẽ tự động chuyển sang CPU một cách im lặng.

- **Tôi có thể xử lý nhiều hình ảnh trong một lần chạy không?**  
  Có. Đặt mã trong một vòng lặp, thay đổi tên tệp mỗi lần lặp, và tái sử dụng cùng một thể hiện `OcrEngine` để giữ mức sử dụng bộ nhớ thấp.

- **PDF của tôi quá lớn—làm sao giảm kích thước?**  
  Sau khi OCR, bạn có thể chạy các API tối ưu PDF của Aspose, hoặc đơn giản giảm độ phân giải của hình ảnh nguồn trước khi đưa vào engine (`ImageStream.fromFile(...).setResolution(150)` cho 150 DPI).

- **Tôi cần giữ nguyên độ phân giải hình ảnh gốc để tuân thủ pháp lý.**  
  Định dạng `PDF_SEARCHABLE` giữ nguyên bitmap gốc; lớp văn bản vô hình được thêm lên trên mà không làm thay đổi chất lượng hình ảnh.

## Tóm tắt bằng Hình ảnh  

![ví dụ tạo pdf có thể tìm kiếm](placeholder-image.png "ví dụ tạo pdf có thể tìm kiếm")

*Văn bản thay thế:* *ví dụ tạo pdf có thể tìm kiếm – Engine Java OCR chuyển một JPG đã quét thành PDF có thể tìm kiếm.*

## Kết luận  

Bây giờ bạn đã có một **giải pháp hoàn chỉnh, từ đầu đến cuối** để chuyển bất kỳ hình ảnh nào thành **PDF có thể tìm kiếm** bằng Aspose OCR cho Java. Bằng cách **chuyển đổi hình ảnh sang PDF**, **bật sửa lỗi chính tả**, và **sử dụng OCR GPU** khi có thể, bạn sẽ có kết quả nhanh, chính xác và có thể tìm kiếm, hoạt động trên mọi nền tảng.

Tiếp theo? Hãy thử nghiệm với:

- **Các định dạng đầu ra khác nhau** (`PDF`, `DOCX`, `HTML`) để xem cách lớp văn bản hoạt động.
- **Từ điển tùy chỉnh** nếu bạn đang xử lý thuật ngữ chuyên ngành.
- **Xử lý hàng loạt** để tự động xử lý hàng ngàn bản quét.

Bạn có thể tự do điều chỉnh số lượng luồng, thay đổi bộ lọc, hoặc tích hợp quy trình tiền xử lý của riêng mình. Mô hình cốt lõi vẫn như cũ: tải → tiền xử lý → cấu hình → OCR → lưu.

Chúc lập trình vui vẻ, và hy vọng các PDF của bạn luôn có thể tìm kiếm!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}