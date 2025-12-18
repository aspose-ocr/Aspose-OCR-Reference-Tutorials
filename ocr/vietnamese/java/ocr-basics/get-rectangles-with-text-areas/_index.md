---
date: 2025-12-10
description: Tìm hiểu cách nhận dạng văn bản từ hình ảnh và trích xuất các đoạn văn
  từ hình ảnh bằng Aspose.OCR cho Java. Hướng dẫn từng bước kèm ví dụ mã.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Nhận dạng văn bản từ hình ảnh và truy xuất các hình chữ nhật vùng văn bản
url: /vi/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Nhận dạng Văn bản từ Hình ảnh và Lấy Các Hình chữ nhật Vùng Văn bản

## Giới thiệu

Nếu bạn cần **nhận dạng văn bản từ hình ảnh** trong một ứng dụng Java, Aspose.OCR for Java cung cấp cách nhanh chóng và chính xác để thực hiện. Trong hướng dẫn này, chúng ta sẽ đi qua các bước cần thiết để trích xuất các đoạn văn từ một hình ảnh, lấy các hình chữ nhật bao quanh mỗi vùng văn bản, và in các tọa độ đó ra console. Khi hoàn thành, bạn sẽ hiểu tại sao cách tiếp cận này hoạt động, cách tích hợp thư viện, và nơi bạn có thể mở rộng nó cho các trường hợp sử dụng của riêng mình.

## Trả lời nhanh
- **“Nhận dạng văn bản từ hình ảnh” có nghĩa là gì?** Nó có nghĩa là chuyển các ký tự hiển thị trong một bức ảnh thành dữ liệu chuỗi có thể chỉnh sửa.  
- **Thư viện nào thực hiện việc này trong Java?** Aspose.OCR for Java.  
- **Tôi có cần giấy phép cho việc phát triển không?** Một giấy phép tạm thời có sẵn để thử nghiệm; giấy phép đầy đủ cần thiết cho môi trường sản xuất.  
- **Tôi có thể trích xuất các đoạn văn thay vì các từ riêng lẻ không?** Có – sử dụng `AreasType.PARAGRAPHS` để lấy các hình chữ nhật ở mức đoạn văn.  
- **Mã có tương thích với Java 11+ không?** Hoàn toàn, API hoạt động với Java 11 và các phiên bản sau.

## “Nhận dạng văn bản từ hình ảnh” trong Aspose.OCR là gì?
Phương thức `RecognizePage` của Aspose.OCR phân tích bitmap, áp dụng các thuật toán OCR, và trả về chuỗi đã nhận dạng. Khi bạn yêu cầu các vùng văn bản, thư viện cũng tính toán các tọa độ `Rectangle` chính xác cho mỗi khối văn bản, giúp dễ dàng làm nổi bật hoặc xử lý các phần cụ thể sau này.

## Tại sao nên dùng Aspose.OCR cho Java?
- **Độ chính xác cao** – hỗ trợ nhiều ngôn ngữ và phông chữ phức tạp.  
- **Tích hợp dễ dàng** – một file JAR duy nhất cung cấp đầy đủ khả năng OCR.  
- **Đầu ra linh hoạt** – bạn có thể lấy văn bản thô, HTML định dạng, hoặc các hình chữ nhật vùng văn bản chính xác.  
- **An toàn đa luồng** – phù hợp cho môi trường máy chủ có lưu lượng cao.

## Yêu cầu trước

- **Bộ công cụ phát triển Java** (JDK 11 hoặc mới hơn) đã được cài đặt trên máy của bạn.  
- Thư viện **Aspose.OCR for Java** – tải về từ trang chính thức [tại đây](https://releases.aspose.com/ocr/java/).  
- Một IDE hoặc công cụ xây dựng (Maven/Gradle) để quản lý phụ thuộc JAR.

## Nhập các Gói

Trong dự án Java của bạn, nhập các lớp cần thiết:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Hướng dẫn Từng Bước

### Bước 1: Thiết lập Dự án
Tạo một dự án Java mới (hoặc thêm vào dự án hiện có) và đặt file JAR Aspose.OCR vào classpath. Nếu bạn dùng Maven, thêm phụ thuộc như mô tả trong gói tải về.

### Bước 2: Định nghĩa Thư mục Tài liệu và Đường dẫn Ảnh
Chỉ định vị trí của ảnh mẫu:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Bước 3: Tạo Instance Aspose.OCR
Khởi tạo engine OCR:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Bước 4: Nhận dạng Văn bản trong Ảnh
Gọi `RecognizePage` để chuyển ảnh thành văn bản thuần. Bước này minh họa khả năng **nhận dạng văn bản từ hình ảnh** cốt lõi:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Bước 5: Lấy Các Hình chữ nhật với Vùng Văn bản
Bây giờ lấy các hình chữ nhật bao quanh mỗi đoạn (hoặc các loại vùng khác). Đây là nơi bạn **trích xuất các đoạn văn từ ảnh** và nhận được tọa độ của chúng:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Các Vấn đề Thường gặp & Khắc phục

| Triệu chứng | Nguyên nhân có thể | Cách khắc phục |
|------------|--------------------|----------------|
| `IOException` khi gọi `RecognizePage` | Đường dẫn tệp không đúng hoặc thiếu quyền đọc | Kiểm tra `imagePath` có trỏ tới file PNG/JPG tồn tại và ứng dụng có quyền truy cập hệ thống tệp. |
| Chuỗi kết quả rỗng | Ảnh chất lượng thấp hoặc ngôn ngữ không được hỗ trợ | Tiền xử lý ảnh (tăng độ tương phản, nhị phân hoá) hoặc chỉ định ngôn ngữ đúng bằng `api.setLanguage("eng")`. |
| Không có hình chữ nhật nào được trả về | Sử dụng sai `AreasType` (ví dụ: `WORDS` khi mong muốn đoạn văn) | Chuyển sang `AreasType.PARAGRAPHS` hoặc `AreasType.LINES` tùy nhu cầu. |

## Câu hỏi Thường gặp

**H: Aspose.OCR có tương thích với Java 11 không?**  
Đ: Có, Aspose.OCR hoạt động với Java 11 và các phiên bản sau.

**H: Tôi có thể dùng Aspose.OCR cho cả dự án cá nhân và thương mại không?**  
Đ: Có, bạn có thể sử dụng trong bất kỳ loại dự án nào. Để biết chi tiết giấy phép, truy cập [tại đây](https://purchase.aspose.com/buy).

**H: Làm sao để lấy giấy phép tạm thời để đánh giá?**  
Đ: Bạn có thể lấy giấy phép tạm thời [tại đây](https://purchase.aspose.com/temporary-license/).

**H: Tôi có thể tìm hỗ trợ cộng đồng hoặc trợ giúp chính thức ở đâu?**  
Đ: Để được hỗ trợ và thảo luận, truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**H: Aspose.OCR có hỗ trợ đa luồng không?**  
Đ: Có, thư viện an toàn đa luồng và có thể được sử dụng trong môi trường đồng thời để cải thiện hiệu năng.

## Kết luận

Trong hướng dẫn này, bạn đã học cách **nhận dạng văn bản từ hình ảnh** bằng Aspose.OCR for Java, trích xuất các đoạn văn, và lấy các hình chữ nhật chính xác bao quanh mỗi khối văn bản. Những khả năng này cho phép bạn xây dựng PDF có thể tìm kiếm, làm nổi bật văn bản trong giao diện người dùng, hoặc đưa dữ liệu có cấu trúc vào các quy trình downstream. Hãy khám phá thêm API để tùy chỉnh cài đặt ngôn ngữ, xử lý các định dạng ảnh khác, hoặc tích hợp với lưu trữ đám mây.

---

**Cập nhật lần cuối:** 2025-12-10  
**Kiểm thử với:** Aspose.OCR 23.10 for Java  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}