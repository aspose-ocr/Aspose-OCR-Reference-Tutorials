---
category: general
date: 2026-05-06
description: Cách sử dụng OCR để trích xuất văn bản từ hình ảnh trong Java. Tìm hiểu
  chuyển đổi hình ảnh sang văn bản bằng OCR, sửa lỗi OCR và tải hình ảnh cho OCR bằng
  Aspose OCR.
draft: false
keywords:
- how to use ocr
- extract text from image
- ocr image to text
- correct ocr errors
- load image for ocr
language: vi
og_description: Cách sử dụng OCR trong Java để trích xuất văn bản từ hình ảnh, sửa
  lỗi OCR và tải hình ảnh cho OCR bằng Aspose OCR.
og_title: Cách sử dụng OCR trong Java – Hướng dẫn toàn diện
tags:
- OCR
- Java
- Aspose
title: Cách sử dụng OCR trong Java – Trích xuất văn bản từ hình ảnh với chỉnh sửa
  chính tả
url: /vi/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách sử dụng OCR trong Java – Trích xuất văn bản từ hình ảnh với sửa lỗi chính tả

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để biến một bức ảnh biên lai mờ thành văn bản sạch, có thể tìm kiếm không? Bạn không phải là người duy nhất. Trong nhiều dự án—ứng dụng theo dõi chi phí, quy trình số hoá hoá đơn, hoặc thậm chí một script ghi chú nhanh—việc lấy văn bản đáng tin cậy từ hình ảnh là rào cản đầu tiên.  

Bài hướng dẫn này sẽ chỉ cho bạn cách sử dụng OCR trong Java, bao quát mọi thứ từ việc tải hình ảnh cho OCR đến việc sửa lỗi OCR sao cho kết quả trông như được gõ bởi con người. Khi hoàn thành, bạn sẽ có thể **trích xuất văn bản từ hình ảnh**, thực hiện chuyển đổi **OCR image to text**, và tự động sửa các lỗi nhận dạng phổ biến.

## Những gì bạn sẽ xây dựng

Chúng ta sẽ tạo một chương trình console Java nhỏ mà:

1. Tải một file PNG (hoặc bất kỳ định dạng nào được hỗ trợ) vào engine Aspose OCR.  
2. Kích hoạt tính năng sửa lỗi chính tả tích hợp để **sửa lỗi OCR**.  
3. Chạy quá trình nhận dạng và in ra văn bản đã được làm sạch.  

Không có dịch vụ bên ngoài, không có framework nặng—chỉ một file JAR duy nhất và vài dòng code.

### Yêu cầu trước

- Java Development Kit (JDK) 8 hoặc mới hơn.  
- Maven (hoặc bất kỳ công cụ xây dựng nào) để tải thư viện Aspose OCR.  
- Một file hình ảnh (ví dụ `receipt.png`) mà bạn muốn phân tích.  

Nếu bạn chưa có file JAR Aspose OCR, hãy thêm phụ thuộc này vào `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

> **Mẹo:** Phiên bản đánh giá miễn phí hoạt động cho việc thử nghiệm, nhưng giấy phép sẽ loại bỏ watermark đánh giá.

## Bước 1 – Khởi tạo Engine OCR (Từ khóa chính trong hành động)

Điều đầu tiên bạn cần làm là tạo một thể hiện của `OcrEngine`. Hãy nghĩ nó như bộ não sẽ đọc các pixel và chuyển chúng thành ký tự.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this is where we start using OCR
        OcrEngine ocrEngine = new OcrEngine();
```

*Tại sao điều này quan trọng:* Khởi tạo engine thiết lập các tài nguyên nội bộ (mô hình ngôn ngữ, từ điển, v.v.). Bỏ qua bước này sẽ gây ra `NullPointerException` sau này khi bạn cố tải một hình ảnh.

## Bước 2 – Tải hình ảnh cho OCR

Bây giờ chúng ta thực sự **tải hình ảnh cho OCR**. Aspose cung cấp một tiện ích `ImageStream.fromFile` thuận tiện, nhưng bạn cũng có thể cung cấp một `byte[]` nếu muốn.

```java
        // Load the image you want to analyse – replace the path with your own file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

*Cạm bẫy thường gặp:* Đường dẫn file phải là tuyệt đối hoặc tương đối so với thư mục làm việc. Nếu không tìm thấy hình ảnh, engine sẽ ném ra `IOException`. Hãy kiểm tra lại đường dẫn, đặc biệt khi chạy từ IDE so với một JAR đã đóng gói.

## Bước 3 – Bật sửa lỗi chính tả để **sửa lỗi OCR**

OCR mặc định có thể gây nhiễu—ví dụ “l0ve” thay vì “love” hoặc “0” thay cho “O”. Bật sửa lỗi chính tả sẽ yêu cầu engine thực hiện một bước xử lý hậu kỳ để sửa các lỗi thường gặp.

```java
        // Turn on the spell‑correction feature – this helps to correct OCR errors
        ocrEngine.getSettings().setEnableSpellCorrection(true);
```

*Tại sao bạn muốn điều này:* Nếu không có sửa lỗi chính tả, bạn có thể phải tự tay làm sạch đầu ra, điều này làm mất mục đích của tự động hoá. Từ điển tích hợp hoạt động tốt cho tiếng Anh và một số ngôn ngữ khác.

## Bước 4 – Thực hiện nhận dạng (**OCR Image to Text**)

Với hình ảnh đã được tải và sửa lỗi chính tả đã bật, cuối cùng chúng ta có thể yêu cầu engine nhận dạng văn bản.

```java
        // Run the OCR process – this converts the image to text
        OcrResult ocrResult = ocrEngine.recognize();
```

*Trường hợp đặc biệt:* Nếu hình ảnh có độ tương phản thấp hoặc nghiêng mạnh, kết quả vẫn có thể chứa các ký tự vô nghĩa. Hãy cân nhắc tiền xử lý (ví dụ, nhị phân hoá, chỉnh nghiêng) trước khi đưa vào engine.

## Bước 5 – Xuất văn bản đã được làm sạch

Bước cuối cùng chỉ đơn giản là in ra kết quả. Trong một ứng dụng thực tế bạn có thể ghi nó vào cơ sở dữ liệu hoặc file, nhưng đối với bản demo này `System.out` là đủ.

```java
        // Display the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Kết quả mong đợi

Giả sử `receipt.png` chứa danh sách mặt hàng rõ ràng, bạn có thể thấy kết quả như sau:

```
Corrected text:
Item           Qty   Price
Apple          2     $1.20
Banana         5     $0.75
Total               $5.55
```

Lưu ý cách “Qty” và “Price” được viết đúng ngay cả khi bản scan gốc có một ký tự “Qy” lạc.

## Ví dụ hoàn chỉnh hoạt động

Dưới đây là chương trình đầy đủ mà bạn có thể sao chép‑dán vào một file tên `SpellCorrectDemo.java`. Đảm bảo file JAR Aspose OCR có trong classpath của bạn.

```java
import com.aspose.ocr.*;

public class SpellCorrectDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Replace "YOUR_DIRECTORY/receipt.png" with the actual path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Enable spell correction to improve accuracy
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Step 4: Perform OCR recognition (OCR image to text)
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the corrected text
        System.out.println("Corrected text:");
        System.out.println(ocrResult.getText());
    }
}
```

Chạy nó bằng:

```bash
javac -cp "aspose-ocr-23.9.jar" SpellCorrectDemo.java
java -cp ".:aspose-ocr-23.9.jar" SpellCorrectDemo
```

Bây giờ bạn sẽ thấy văn bản đã được làm sạch được in ra console.

## Bonus: Điều chỉnh cài đặt để tăng độ chính xác

Mặc dù cấu hình mặc định hoạt động cho hầu hết tài liệu in, bạn có thể cần điều chỉnh một vài tham số cho các trường hợp đặc thù:

| Setting | What It Does | When to Change |
|---------|--------------|----------------|
| `setLanguage(OcrLanguage.English)` | Buộc sử dụng từ điển tiếng Anh (giảm kết quả dương tính giả) | Nếu hình ảnh của bạn chỉ chứa văn bản tiếng Anh. |
| `setResolution(300)` | Thông báo cho engine DPI của ảnh nguồn | Đối với các bản scan độ phân giải cao. |
| `setEnableAutoSkewCorrection(true)` | Tự động xoay các trang hơi nghiêng | Khi hình ảnh được chụp bằng điện thoại. |

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setEnableAutoSkewCorrection(true);
```

## Câu hỏi thường gặp

**Q: Điều này có hoạt động với PDF không?**  
A: Có. Chuyển mỗi trang PDF thành hình ảnh (ví dụ, dùng Aspose PDF) và đưa hình ảnh vào engine OCR.

**Q: Nếu ảnh của tôi ở định dạng BMP thì sao?**  
A: `ImageStream.fromFile` hỗ trợ PNG, JPEG, BMP, TIFF và GIF ngay từ đầu. Chỉ cần thay đổi phần mở rộng file.

**Q: Tôi có thể tắt sửa lỗi chính tả không?**  
A: Chắc chắn—đặt `setEnableSpellCorrection(false)` nếu bạn cần đầu ra OCR thô cho các bước xử lý tiếp theo.

## Kết luận

Bây giờ bạn đã biết **cách sử dụng OCR** trong Java để **trích xuất văn bản từ hình ảnh**, tự động **sửa lỗi OCR**, và đúng cách **tải hình ảnh cho OCR** bằng Aspose OCR. Quy trình năm bước—khởi tạo, tải, bật sửa lỗi chính tả, nhận dạng và xuất—bao phủ phần lớn các nhiệm vụ OCR hàng ngày.  

Từ đây, hãy cân nhắc kết hợp logic này với việc ghi lại vào cơ sở dữ liệu, một endpoint REST, hoặc một bộ xử lý batch để xử lý hàng chục biên lai cùng lúc. Thử nghiệm với bảng cài đặt bổ sung ở trên để tối ưu độ chính xác đến từng ký tự.

Chúc lập trình vui vẻ, và hy vọng kết quả OCR của bạn luôn sạch sẽ hơn cả những biên lai bị dơ cà phê! 

![how to use ocr diagram showing image → OCR engine → corrected text flow]

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}