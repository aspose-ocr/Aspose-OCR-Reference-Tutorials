---
category: general
date: 2026-02-17
description: Học cách sử dụng OCR trong Java để nhận dạng văn bản từ các tệp hình
  ảnh, trích xuất văn bản từ biên lai PNG và chuyển đổi biên lai sang JSON với Aspose
  OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: vi
og_description: Hướng dẫn từng bước cách sử dụng OCR trong Java để nhận dạng văn bản
  từ hình ảnh, trích xuất văn bản từ biên lai PNG và chuyển biên lai sang JSON.
og_title: Cách sử dụng OCR trong Java – Nhận dạng văn bản từ hình ảnh
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Cách sử dụng OCR trong Java – Nhận dạng văn bản từ hình ảnh nhanh chóng
url: /vi/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

content.

Let's craft translation.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Sử Dụng OCR trong Java – Nhận Dạng Văn Bản từ Hình Ảnh Nhanh Chóng

Bạn đã bao giờ tự hỏi **cách sử dụng OCR** để lấy văn bản từ một bức ảnh biên lai chưa? Có thể bạn đã thử một vài công cụ trực tuyến, chỉ để nhận được các ký tự lộn xộn hoặc định dạng mà bạn không thể phân tích. Tin tốt là với một vài dòng mã Java, bạn có thể **nhận dạng văn bản từ hình ảnh**, **trích xuất văn bản từ PNG** biên lai, và thậm chí **chuyển biên lai sang JSON** để xử lý downstream.  

Trong tutorial này chúng ta sẽ đi qua toàn bộ quy trình — từ việc cấp phép thư viện Aspose OCR đến việc nhận được payload JSON sạch sẽ mà bạn có thể đưa vào cơ sở dữ liệu hoặc mô hình machine‑learning. Không có phần thừa, chỉ có một ví dụ thực tế, có thể chạy được mà bạn có thể sao chép‑dán vào IDE. Khi kết thúc, bạn sẽ có một chương trình tự chứa, nhận `receipt.png` và xuất ra một chuỗi JSON sẵn sàng sử dụng.

## Những Gì Bạn Cần

- **Java Development Kit (JDK) 8+** – bất kỳ phiên bản mới nào cũng hoạt động.  
- **Aspose OCR for Java** library (artifact Maven là `com.aspose:aspose-ocr`).  
- Một **tệp giấy phép Aspose OCR hợp lệ** (`Aspose.OCR.lic`). Bản dùng thử miễn phí hoạt động cho việc thử nghiệm, nhưng giấy phép chính thức sẽ loại bỏ các giới hạn đánh giá.  
- Một tệp hình ảnh (PNG, JPEG, v.v.) chứa văn bản bạn muốn đọc—gọi nó là `receipt.png` và đặt nó vào một thư mục đã biết.  
- IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, VS Code…) – bạn tự do lựa chọn.  

> **Pro tip:** Giữ tệp giấy phép của bạn ở ngoài thư mục nguồn và tham chiếu nó bằng đường dẫn tuyệt đối hoặc tương đối để tránh commit vào hệ thống kiểm soát phiên bản.

Bây giờ các điều kiện tiên quyết đã rõ, hãy đi sâu vào mã thực tế.

## Cách Sử Dụng OCR – Các Bước Cốt Lõi

Dưới đây là tổng quan cấp cao về các hành động chúng ta sẽ thực hiện:

1. **Tải thư viện Aspose OCR** và áp dụng giấy phép của bạn.  
2. **Tạo một instance `OcrEngine`** – đây là engine thực hiện phần việc nặng.  
3. **Chuẩn bị một đối tượng `OcrInput`** trỏ tới hình ảnh bạn muốn xử lý.  
4. **Gọi `recognize` với `ResultFormat.JSON`** để nhận được biểu diễn JSON của văn bản đã trích xuất.  
5. **Xử lý đầu ra JSON** – in ra, ghi vào file, hoặc phân tích thêm.

Mỗi bước sẽ được giải thích chi tiết trong các phần sau.

## Bước 1 – Cài Đặt Aspose OCR và Áp Dụng Giấy Phép Của Bạn

Đầu tiên, thêm dependency Aspose OCR vào `pom.xml` nếu bạn dùng Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Bây giờ, trong mã Java của bạn, tải giấy phép. Bước này rất quan trọng; nếu không, thư viện sẽ chạy ở chế độ đánh giá và có thể chèn watermark vào kết quả.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Tại sao lại quan trọng:** Đối tượng `License` thông báo cho engine OCR rằng bạn đã được ủy quyền sử dụng toàn bộ tính năng, bao gồm nhận dạng độ chính xác cao và xuất JSON. Bỏ qua bước này vẫn cho phép bạn **nhận dạng văn bản từ hình ảnh**, nhưng kết quả có thể bị giới hạn.

## Bước 2 – Tạo Instance Engine OCR

Lớp `OcrEngine` là điểm vào cho mọi thao tác OCR. Hãy nghĩ nó như “bộ não” đọc các pixel và quyết định ký tự tương ứng.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Bạn có thể tùy chỉnh engine (ví dụ: đặt ngôn ngữ, bật deskew) sau này nếu biên lai của bạn chứa script không phải Latin hoặc được quét ở góc nghiêng. Đối với hầu hết các biên lai ở Mỹ, các giá trị mặc định hoạt động tốt.

## Bước 3 – Tải Hình Ảnh Bạn Muốn Xử Lý

Bây giờ chúng ta sẽ trỏ engine OCR tới tệp chứa biên lai. Lớp `OcrInput` có thể chấp nhận nhiều hình ảnh, nhưng trong tutorial này chúng ta giữ đơn giản với một PNG duy nhất.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

Nếu bạn cần **trích xuất văn bản từ PNG** hàng loạt, chỉ cần gọi `input.add()` liên tục hoặc truyền danh sách các đường dẫn tệp.

## Bước 4 – Nhận Dạng Văn Bản và Chuyển Biên Lai Sang JSON

Đây là phần cốt lõi của tutorial. Chúng ta yêu cầu engine nhận dạng văn bản và trả về kết quả ở định dạng JSON. Cờ `ResultFormat.JSON` thực hiện toàn bộ công việc nặng cho chúng ta.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

Payload JSON bao gồm mỗi dòng đã nhận dạng, bounding box, điểm confidence và văn bản thô. Cấu trúc này giúp việc **chuyển biên lai sang JSON** và đưa vào bất kỳ API downstream nào trở nên đơn giản.

## Bước 5 – Gộp Tất Cả và Chạy Chương Trình

Dưới đây là lớp Java hoàn chỉnh, sẵn sàng chạy, kết nối mọi thứ lại với nhau. Lưu lại dưới tên `JsonExportDemo.java` (hoặc bất kỳ tên nào bạn muốn) và chạy từ IDE hoặc dòng lệnh.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Kết Quả Mong Đợi

Chạy chương trình sẽ in ra một chuỗi JSON tương tự như sau (nội dung cụ thể phụ thuộc vào biên lai của bạn):

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

Bây giờ bạn có thể đưa JSON này vào cơ sở dữ liệu, endpoint REST, hoặc pipeline phân tích dữ liệu. Bước **chuyển biên lai sang JSON** đã được thực hiện sẵn.

## Các Câu Hỏi Thường Gặp và Trường Hợp Cạnh

### Hình ảnh bị xoay thì sao?

Aspose OCR tự động phát hiện và chỉnh sửa các xoay nhẹ. Đối với hình ảnh nghiêng mạnh, hãy gọi `engine.getImagePreprocessingOptions().setDeskew(true)` trước khi nhận dạng.

### Làm sao để xử lý đa ngôn ngữ?

Sử dụng `engine.getLanguage()` để đặt ngôn ngữ mong muốn, ví dụ `engine.setLanguage(Language.FRENCH)`. Điều này hữu ích khi bạn cần **nhận dạng văn bản từ hình ảnh** chứa biên lai đa ngôn ngữ.

### Có thể xuất ra plain text thay vì JSON không?

Chắc chắn rồi. Thay `ResultFormat.JSON` bằng `ResultFormat.TEXT` và gọi `result.getText()`.

### Có cách nào để giới hạn OCR chỉ trong một vùng cụ thể không?

Có — dùng `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` để tập trung vào khu vực biên lai, giúp tăng tốc và độ chính xác.

## Pro Tips cho OCR Sẵn Sàng Sản Xuất

- **Cache đối tượng license** nếu bạn xử lý nhiều tệp trong vòng lặp; tạo lại liên tục sẽ gây overhead.  
- **Xử lý batch**: tải tất cả đường dẫn biên lai vào một `OcrInput` duy nhất và gọi `recognize` một lần. JSON sẽ chứa một mảng các trang, mỗi trang có các dòng riêng.  
- **Validate JSON**: sau khi nhận được chuỗi, phân tích bằng thư viện như Jackson để chắc chắn nó hợp lệ trước khi lưu.  
- **Theo dõi confidence**: JSON bao gồm trường `confidence` cho mỗi dòng. Lọc bỏ các dòng dưới ngưỡng (ví dụ 0.85) để tránh dữ liệu rác.  
- **Bảo mật giấy phép**: lưu `Aspose.OCR.lic` trong vault an toàn hoặc biến môi trường, đặc biệt trong triển khai cloud.

## Kết Luận

Chúng ta đã bao phủ **cách sử dụng OCR** trong Java để **nhận dạng văn bản từ hình ảnh**, **trích xuất văn bản từ PNG** biên lai, và **chuyển biên lai sang JSON** — tất cả bằng một ví dụ ngắn gọn, đầu‑tới‑cuối. Các bước rất rõ ràng, mã hoàn toàn chạy được, và đầu ra JSON cung cấp một cấu trúc sẵn sàng cho bất kỳ hệ thống downstream nào.

Tiếp theo, bạn có thể khám phá các kịch bản nâng cao: đưa JSON vào Apache Kafka để xử lý thời gian thực, áp dụng regex để lấy tổng các mục, hoặc tích hợp với dịch vụ OCR đám mây để mở rộng quy mô. Dù bạn chọn gì, những nguyên tắc cơ bản vừa học sẽ luôn hữu ích.

Có câu hỏi, hoặc gặp khó khăn khi thực hiện? Hãy để lại bình luận bên dưới, chúng mình sẽ cùng giải quyết. Chúc bạn lập trình vui vẻ, và tận hưởng việc biến những bức ảnh biên lai lộn xộn thành dữ liệu sạch, có thể tìm kiếm!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}