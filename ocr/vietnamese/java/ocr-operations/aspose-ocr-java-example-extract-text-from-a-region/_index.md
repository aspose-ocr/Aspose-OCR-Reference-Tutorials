---
category: general
date: 2026-05-03
description: Ví dụ Aspose OCR Java cho thấy cách tải hình ảnh để OCR và trích xuất
  văn bản từ một vùng chỉ trong vài dòng mã.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: vi
og_description: Ví dụ Aspose OCR Java minh họa việc tải hình ảnh để OCR và trích xuất
  văn bản từ một vùng cụ thể, rất phù hợp cho việc xử lý hoá đơn.
og_title: Ví dụ Aspose OCR Java – Trích xuất văn bản theo vùng
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Ví dụ Aspose OCR Java: Trích xuất văn bản từ một vùng'
url: /vi/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Example: Trích xuất Văn bản từ một Vùng

Bạn đang tìm một **ví dụ Aspose OCR Java** cho phép bạn lấy chỉ phần cần thiết từ một hình ảnh? Trong hướng dẫn này, chúng ta sẽ đi qua **tải hình ảnh để OCR** và **trích xuất văn bản từ một vùng**, hoàn hảo cho số hóa đơn, trường biểu mẫu, hoặc bất kỳ dữ liệu nào ẩn trong một bức ảnh lớn hơn.

Bạn có thể tự hỏi tại sao lại giới hạn OCR trong một hình chữ nhật thay vì quét toàn bộ trang. Câu trả lời ngắn gọn: tốc độ và độ chính xác. Khi engine chỉ nhìn vào một phần đã định nghĩa, nó bỏ qua tiếng ồn không liên quan, chạy nhanh hơn và thường cho ra kết quả sạch hơn. Khi kết thúc tutorial này, bạn sẽ có một chương trình Java tự chứa thực hiện đúng điều đó, cùng một vài mẹo để tránh những bẫy thường gặp khiến người mới bối rối.

## Những gì bạn cần

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **Java Development Kit (JDK) 11** trở lên đã được cài đặt.
- Thư viện **Aspose.OCR for Java** (bạn có thể tải JAR mới nhất từ Maven Central hoặc cổng tải xuống của Aspose).
- Một tệp hình ảnh chứa văn bản bạn muốn đọc – trong demo chúng ta sẽ dùng `invoice.png`, trong đó có số hóa đơn ở góc trên‑phải.
- Một IDE yêu thích hoặc một trình soạn thảo văn bản đơn giản cộng với terminal; bất kỳ công cụ xây dựng nào (Maven, Gradle, hoặc chỉ `javac`) đều được.

Đó là tất cả. Không cần engine OCR bổ sung, không có binary gốc, chỉ Java thuần và Aspose.

![Ví dụ Aspose OCR Java](/images/aspose-ocr-java-example.png "Aspose OCR Java ví dụ hiển thị việc trích xuất vùng")

## Aspose OCR Java Example – Khởi tạo Engine OCR

Điều đầu tiên bất kỳ quy trình OCR nào cần là một thể hiện engine. Aspose cung cấp lớp nhẹ `OcrEngine` xử lý mọi thứ từ tải hình ảnh đến lựa chọn ngôn ngữ.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Tại sao điều này quan trọng:** Tạo engine ngay từ đầu cho bạn một đối tượng sạch để cấu hình. Bạn có thể tái sử dụng cùng một `OcrEngine` cho nhiều hình ảnh nếu đang xử lý một lô, giúp tiết kiệm bộ nhớ và thời gian khởi tạo.

## Tải Hình ảnh cho OCR

Tiếp theo, chúng ta chỉ cho engine biết hình nào sẽ được quét. Aspose cung cấp trợ giúp `ImageStream.fromFile`, giúp trừu tượng hoá việc tạo `FileInputStream` thủ công.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**Mẹo:** Thay `YOUR_DIRECTORY` bằng đường dẫn tuyệt đối hoặc tương đối tới nơi bạn lưu `invoice.png`. Nếu tệp không tìm thấy, Aspose sẽ ném `IOException`, vì vậy bạn có thể muốn bọc đoạn này trong khối try‑catch cho mã production.

## Định nghĩa và Trích xuất Văn bản từ một Vùng

Bây giờ là phần trọng tâm: hình chữ nhật chỉ cho engine biết nơi cần nhìn. Hàm khởi tạo `java.awt.Rectangle` nhận `(x, y, width, height)` – tất cả tính bằng pixel.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Cách hoạt động:** Bằng cách gọi `setRegion`, bạn giới hạn việc quét OCR trong một dải rộng 300 pixel, bắt đầu 120 pixel từ cạnh trái và 250 pixel từ trên. Điều chỉnh các số này để phù hợp với bố cục của bạn; cách nhanh để tìm chúng là mở hình ảnh trong bất kỳ trình chỉnh sửa đồ họa nào hiển thị tọa độ pixel.

## Bật Ngôn ngữ và Chạy Nhận dạng

Aspose OCR hỗ trợ hàng chục ngôn ngữ, nhưng đối với số hóa đơn chúng ta chỉ cần tiếng Anh. Bật ngôn ngữ đúng sẽ giảm đáng kể các kết quả sai.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Tại sao chỉ bật tiếng Anh?** Engine OCR sẽ cố gắng khớp ký tự từ mọi ngôn ngữ đã bật, điều này có thể gây nhầm lẫn khi văn bản chỉ là các ký tự chữ và số đơn giản. Hạn chế phạm vi ngôn ngữ cải thiện cả tốc độ và độ chính xác.

### Kết quả Dự kiến

Khi mọi thứ khớp nhau, bạn sẽ thấy đầu ra giống như:

```
Extracted region text: INV-12345
```

Nếu hình chữ nhật lệch vài pixel, đầu ra có thể bị rối hoặc trống. Đó là một kiểm tra nhanh: chạy chương trình, xem console và xác nhận văn bản khớp với những gì bạn thấy trong hình ảnh.

## Chạy Mã và Xác minh Kết quả

Giả sử bạn dùng Maven, thêm phụ thuộc Aspose OCR vào `pom.xml` của mình:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Biên dịch và thực thi:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Hoặc, nếu bạn thích dùng `javac` thuần:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

Bạn sẽ thấy dòng **Extracted region text** được in ra console. Nếu nhận được “OCR recognition failed”, hãy kiểm tra lại đường dẫn tệp và chắc chắn rằng vùng thực sự chứa các ký tự có thể đọc được.

## Các Trường hợp Đặc biệt & Biến thể Thông thường

| Tình huống | Cần Thay Đổi |
|-----------|--------------|
| **Nhiều ngôn ngữ** (ví dụ: Tiếng Anh + Tiếng Tây Ban Nha) | Gọi `ocrEngine.getLanguage().setSpanish(true);` cùng với tiếng Anh. |
| **Vùng nằm ngoài giới hạn hình ảnh** | Aspose sẽ tự động cắt hình chữ nhật, nhưng bạn sẽ mất dữ liệu. Sử dụng `ImageInfo` (`ocrEngine.getImage().getWidth()`) để kiểm tra kích thước trước khi đặt vùng. |
| **Hóa đơn động** (bố cục khác nhau) | Xem xét chạy một quét sơ bộ nhẹ trên toàn hình để tìm từ khóa như “Invoice #” rồi tính toán hình chữ nhật một cách lập trình. |
| **Hình ảnh DPI cao** | Tăng `ocrEngine.getImage().setResolution(300);` để cải thiện độ chính xác trên tài liệu quét. |
| **Tinh chỉnh hiệu năng** | Tắt các ngôn ngữ không cần thiết, giữ vùng càng nhỏ càng tốt, và tái sử dụng một thể hiện `OcrEngine` duy nhất cho nhiều tệp. |

## Mẹo Chuyên Gia Từ Trải Nghiệm Thực Tế

- **Mẹo pro:** Nếu bạn chỉ cần các chữ số (thường cho số hóa đơn), bật chế độ số bằng `ocrEngine.getLanguage().setDigits(true);`. Điều này loại bỏ tiếng ồn chữ cái.
- **Cẩn thận với:** PNG trong suốt. Aspose đôi khi hiểu sai kênh alpha; chuyển hình ảnh sang JPEG nền đặc trước có thể giải quyết các đầu ra trống lạ.
- **Nhớ:** Hình chữ nhật sử dụng hệ tọa độ gốc của hình ảnh, không phải bất kỳ tỉ lệ UI nào bạn có thể thấy trên màn hình. Luôn thử nghiệm với tệp chính xác mà bạn sẽ xử lý trong môi trường production.

## Tiếp Theo?

Bây giờ bạn đã có một **ví dụ Aspose OCR Java** vững chắc cho việc trích xuất dựa trên vùng, bạn có thể mở rộng nó theo một số hướng hữu ích:

- **Xử lý batch:** Lặp qua một thư mục các hóa đơn, tái sử dụng cùng một `OcrEngine` để tăng thông lượng.
- **Xác thực dữ liệu:** Đưa văn bản đã trích xuất qua regex như `INV-\\d{5}` để chắc chắn bạn đã nắm bắt được số hóa đơn hợp lệ.
- **Tích hợp với PDF:** Dùng Aspose.PDF để chèn lại văn bản đã trích xuất lên tài liệu gốc, tạo chuỗi kiểm toán.
- **Triển khai trên cloud:** Đóng gói mã trong một dịch vụ REST nhẹ (Spring Boot) để các hệ thống khác có thể gọi khi cần.

Mỗi bước này đều dựa trên các khái niệm cốt lõi—**tải hình ảnh cho OCR**, **trích xuất văn bản từ một vùng**, và xử lý kết quả—do đó bạn sẽ thấy việc chuyển đổi rất dễ dàng.

---

*Chúc bạn lập trình vui vẻ! Nếu gặp khó khăn, hãy để lại bình luận bên dưới hoặc truy cập diễn đàn Aspose, nơi cộng đồng chia sẻ các tinh chỉnh thực tế cho các bố cục khó khăn.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}