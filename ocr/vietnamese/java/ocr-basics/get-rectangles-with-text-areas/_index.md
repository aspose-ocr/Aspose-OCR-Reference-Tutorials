---
date: 2026-02-09
description: Học cách chuyển đổi hình ảnh thành văn bản và trích xuất các hình chữ
  nhật vùng văn bản bằng thư viện Aspose OCR Java. Hướng dẫn từng bước kèm ví dụ mã.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Chuyển đổi hình ảnh thành văn bản – Nhận dạng văn bản từ hình ảnh và lấy các
  hình chữ nhật vùng văn bản
url: /vi/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chuyển Đổi Hình Ảnh Thành Văn Bản – Nhận Diện Văn Bản Từ Hình Ảnh và Lấy Các Hình Chữ Nhật Vùng Văn Bản

## Giới thiệu

Nếu bạn cần **chuyển đổi hình ảnh thành văn bản** và **nhận diện văn bản từ các tệp hình ảnh** trong một ứng dụng Java, Aspose.OCR for Java cung cấp một cách nhanh chóng và chính xác để thực hiện. Trong hướng dẫn này, chúng ta sẽ đi qua các bước chính xác để trích xuất các đoạn văn từ một hình ảnh, lấy các hình chữ nhật bao quanh mỗi vùng văn bản, và in các tọa độ đó ra console. Khi hoàn thành, bạn sẽ hiểu vì sao cách tiếp cận này hoạt động, cách tích hợp thư viện, và nơi bạn có thể mở rộng nó cho các trường hợp sử dụng của riêng mình.

## Câu trả lời nhanh
- **“Nhận diện văn bản từ hình ảnh” có nghĩa là gì?** Nó có nghĩa là chuyển các ký tự hiển thị trong một bức ảnh thành dữ liệu chuỗi có thể chỉnh sửa.  
- **Thư viện nào thực hiện việc này trong Java?** Aspose.OCR for Java.  
- **Tôi có cần giấy phép cho việc phát triển không?** Một giấy phép tạm thời có sẵn để thử nghiệm; giấy phép đầy đủ cần thiết cho môi trường sản xuất.  
- **Tôi có thể trích xuất các đoạn văn thay vì các từ riêng lẻ không?** Có – sử dụng `AreasType.PARAGRAPHS` để lấy các hình chữ nhật ở mức đoạn văn.  
- **Mã có tương thích với Java 11+ không?** Chắc chắn, API hoạt động với Java 11 và các phiên bản sau.

## “Chuyển đổi hình ảnh thành văn bản” trong Aspose.OCR là gì?
Phương thức `RecognizePage` của Aspose.OCR phân tích bitmap, áp dụng các thuật toán OCR, và trả về chuỗi đã nhận diện. Khi bạn yêu cầu các vùng văn bản, thư viện cũng tính toán các tọa độ `Rectangle` chính xác cho mỗi khối văn bản, giúp bạn dễ dàng làm nổi bật hoặc xử lý các phần cụ thể sau này.

## Tại sao nên sử dụng **java ocr library** này?
- **Độ chính xác cao** – hỗ trợ nhiều ngôn ngữ và phông chữ phức tạp.  
- **Tích hợp dễ dàng** – một file JAR duy nhất cung cấp đầy đủ khả năng OCR.  
- **Đầu ra linh hoạt** – bạn có thể lấy văn bản thô, HTML định dạng, hoặc các hình chữ nhật vùng văn bản chính xác.  
- **An toàn đa luồng** – phù hợp cho môi trường máy chủ có lưu lượng cao.

## Yêu cầu trước

- **Bộ công cụ phát triển Java** (JDK 11 trở lên) đã được cài đặt trên máy của bạn.  
- Thư viện **Aspose.OCR for Java** – tải xuống từ trang chính thức [tại đây](https://releases.aspose.com/ocr/java/).  
- Một IDE hoặc công cụ xây dựng (Maven/Gradle) để quản lý phụ thuộc JAR.

## Nhập các gói

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

## Hướng dẫn từng bước

### Bước 1: Thiết lập dự án
Tạo một dự án Java mới (hoặc thêm vào dự án hiện có) và đặt file JAR Aspose.OCR vào classpath. Nếu bạn dùng Maven, thêm phụ thuộc như mô tả trong gói tải xuống.

### Bước 2: Định nghĩa thư mục tài liệu và đường dẫn hình ảnh
Chỉ định vị trí của hình ảnh mẫu:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Bước 3: Tạo thể hiện Aspose.OCR
Khởi tạo engine OCR:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Bước 4: Nhận diện văn bản trong hình ảnh
Gọi `RecognizePage` để chuyển ảnh thành văn bản thuần. Bước này minh họa khả năng **recognize text image java** cốt lõi:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Bước 5: Lấy các hình chữ nhật với vùng văn bản
Bây giờ lấy các hình chữ nhật bao quanh mỗi đoạn (hoặc các loại vùng khác). Đây là nơi bạn **extract paragraphs from image** và nhận được tọa độ của chúng:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Các vấn đề thường gặp & Khắc phục

| Triệu chứng | Nguyên nhân khả dĩ | Cách khắc phục |
|------------|---------------------|----------------|
| `IOException` khi gọi `RecognizePage` | Đường dẫn tệp không đúng hoặc thiếu quyền đọc | Kiểm tra `imagePath` trỏ tới file PNG/JPG tồn tại và ứng dụng có quyền truy cập hệ thống tệp. |
| Chuỗi kết quả rỗng | Hình ảnh chất lượng thấp hoặc ngôn ngữ không được hỗ trợ | Tiền xử lý ảnh (tăng độ tương phản, nhị phân hoá) hoặc chỉ định ngôn ngữ đúng bằng `api.setLanguage("eng")`. |
| Không có hình chữ nhật nào được trả về | Sử dụng sai `AreasType` (ví dụ `WORDS` khi mong muốn đoạn văn) | Chuyển sang `AreasType.PARAGRAPHS` hoặc `AreasType.LINES` tùy nhu cầu. |

## Câu hỏi thường gặp

**H: Aspose.OCR có tương thích với Java 11 không?**  
Đ: Có, Aspose.OCR hoạt động với Java 11 và các phiên bản sau.

**H: Tôi có thể dùng Aspose.OCR cho cả dự án cá nhân và thương mại không?**  
Đ: Có, bạn có thể sử dụng trong bất kỳ loại dự án nào. Để biết chi tiết giấy phép, truy cập [tại đây](https://purchase.aspose.com/buy).

**H: Làm sao để lấy giấy phép tạm thời để đánh giá?**  
Đ: Bạn có thể nhận giấy phép tạm thời [tại đây](https://purchase.aspose.com/temporary-license/).

**H: Tôi có thể tìm hỗ trợ cộng đồng hoặc trợ giúp chính thức ở đâu?**  
Đ: Đối với hỗ trợ và thảo luận, truy cập [diễn đàn Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**H: Aspose.OCR có hỗ trợ đa luồng không?**  
Đ: Có, thư viện an toàn đa luồng và có thể được sử dụng trong môi trường đồng thời để cải thiện hiệu năng.

## Kết luận

Trong **aspose ocr java tutorial** này, bạn đã học cách **chuyển đổi hình ảnh thành văn bản** bằng Aspose.OCR for Java, trích xuất các đoạn văn, và lấy các hình chữ nhật chính xác bao quanh mỗi khối văn bản. Những khả năng này cho phép bạn xây dựng PDF có thể tìm kiếm, làm nổi bật văn bản trong giao diện người dùng, hoặc đưa dữ liệu có cấu trúc vào các quy trình downstream. Hãy khám phá thêm API để tùy chỉnh cài đặt ngôn ngữ, xử lý các định dạng ảnh khác, hoặc tích hợp với lưu trữ đám mây.

---

**Cập nhật lần cuối:** 2026-02-09  
**Đã kiểm tra với:** Aspose.OCR 23.10 for Java  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}