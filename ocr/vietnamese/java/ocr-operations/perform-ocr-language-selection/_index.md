---
date: 2026-02-12
description: Học cách OCR văn bản hình ảnh với lựa chọn ngôn ngữ bằng Aspose.OCR cho
  Java. Hướng dẫn từng bước này bao gồm trích xuất văn bản Java, chỉnh sửa độ nghiêng
  OCR và nhiều hơn nữa.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Cách OCR Văn bản Hình ảnh với Ngôn ngữ Sử dụng Aspose.OCR
url: /vi/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách OCR Văn bản Hình ảnh với Ngôn ngữ Sử dụng Aspose.OCR

## Giới thiệu

Việc trích xuất văn bản từ các tệp hình ảnh là một nhu cầu phổ biến, dù bạn đang số hoá tài liệu đã quét, xử lý biên lai, hay xây dựng kho lưu trữ có thể tìm kiếm. Trong hướng dẫn này, chúng ta sẽ đi qua một ví dụ thực tế, đầy đủ, cho thấy **cách OCR văn bản hình ảnh** với cài đặt ngôn ngữ cụ thể, để bạn có thể tích hợp OCR đáng tin cậy vào các ứng dụng Java ngay hôm nay. Bạn cũng sẽ thấy cách xử lý hiệu chỉnh nghiêng (skew) và nhận dạng dựa trên vùng để đạt độ chính xác tối ưu.

## Câu trả lời nhanh
- **Thư viện nào hỗ trợ OCR trong Java?** Aspose.OCR for Java  
- **Cài đặt nào chọn ngôn ngữ?** `settings.setLanguage(Language.Eng)` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ)  
- **Có cần giấy phép cho việc phát triển không?** Giấy phép dùng thử miễn phí đủ cho việc thử nghiệm; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Có thể giới hạn OCR trong một vùng của hình ảnh không?** Có, sử dụng `RecognitionSettings.setRecognitionAreas()` với các hình chữ nhật.  
- **Thời gian chạy điển hình là bao lâu?** Vài giây cho mỗi trang trên một laptop tiêu chuẩn, tùy thuộc vào kích thước hình ảnh và độ phức tạp của ngôn ngữ.

## Cách OCR Văn bản Hình ảnh với Lựa chọn Ngôn ngữ
Trong phần này, chúng ta trả lời câu hỏi cốt lõi **cách OCR** một hình ảnh khi bạn biết ngôn ngữ của văn bản. Việc chọn đúng ngôn ngữ sẽ cải thiện đáng kể độ chính xác nhận dạng vì engine OCR có thể áp dụng các từ điển và mô hình ký tự riêng cho ngôn ngữ đó.

### Tại sao điều này quan trọng
- **Độ chính xác cao hơn** – các mô hình riêng cho ngôn ngữ giảm thiểu lỗi nhận dạng.  
- **Tăng hiệu suất** – engine bỏ qua các kiểm tra ngôn ngữ không cần thiết.  
- **Xử lý dấu phụ tốt hơn** – tiếng Pháp, Tây Ban Nha, Đức, v.v. được nhận dạng chính xác khi sử dụng enum `Language` phù hợp.

## “Trích xuất văn bản từ hình ảnh” là gì?
Việc trích xuất văn bản từ hình ảnh (OCR) chuyển đổi biểu diễn trực quan của các ký tự thành chuỗi có thể đọc được bởi máy. Điều này cho phép tìm kiếm, phân tích và quy trình trích xuất dữ liệu mà nếu không sẽ phải thực hiện bằng cách nhập liệu thủ công.

## Tại sao sử dụng Aspose.OCR với lựa chọn ngôn ngữ?
- **Hỗ trợ đa ngôn ngữ** – Chọn chính xác ngôn ngữ (các) có trong hình ảnh để tăng độ chính xác.  
- **Kiểm soát chi tiết** – Điều chỉnh nghiêng, định nghĩa vùng nhận dạng, và thiết lập hành vi tự động nghiêng.  
- **API thuần Java** – Không phụ thuộc vào native, dễ tích hợp vào bất kỳ dự án Java nào.  
- **Dữ liệu kết quả phong phú** – Nhận văn bản thuần, JSON, các hình chữ nhật bao quanh và cảnh báo trong một lần gọi.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **Java Development Kit (JDK)** được cài đặt (JDK 8 trở lên).  
- **Thư viện Aspose.OCR for Java** – tải về từ trang chính thức [here](https://reference.aspose.com/ocr/java/).  
- Một tệp hình ảnh chứa văn bản bạn muốn trích xuất, ví dụ `p3.png`.

## Nhập Gói

Trong file nguồn Java của bạn, bao gồm các lớp Aspose.OCR cần thiết và các tiện ích chuẩn của Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Hướng dẫn từng bước

### Bước 1: Thiết lập Thư mục Tài liệu của Bạn

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Thay `"Your Document Directory"` bằng đường dẫn tuyệt đối nơi chứa `p3.png`.

### Bước 2: Xác định Đường dẫn Hình ảnh

```java
// The image path
String file = dataDir + "p3.png";
```

Đảm bảo biến `file` trỏ tới đúng hình ảnh bạn muốn xử lý.

### Bước 3: Tạo Instance API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Đối tượng `AsposeOCR` cung cấp quyền truy cập vào tất cả các thao tác OCR.

### Bước 4: Đặt tùy chọn Nhận dạng (Lựa chọn Ngôn ngữ)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Ở đây chúng ta:

1. Tắt tính năng tự động nghiêng vì chúng ta sẽ cung cấp giá trị nghiêng thủ công.  
2. Định nghĩa một vùng hình chữ nhật (`RecognitionAreas`) để giới hạn OCR chỉ trong phần hình ảnh thực sự chứa văn bản.  
3. Đặt **ngôn ngữ** thành tiếng Anh (`Language.Eng`). Thay thành `Language.Fra`, `Language.Spa`, v.v., tùy vào hình ảnh nguồn của bạn.

### Bước 5: Thực hiện OCR và Lấy Kết quả

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Lệnh `RecognizePage` chạy engine OCR sử dụng hình ảnh và các cài đặt bạn đã định nghĩa. Kết quả được lưu trong một đối tượng `RecognitionResult`.

### Bước 6: In và Sử dụng Kết quả

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

Đầu ra trên console hiển thị:

- Toàn bộ văn bản đã trích xuất (`recognitionText`).  
- Văn bản cho mỗi hình chữ nhật đã định nghĩa (`recognitionAreasText`).  
- Tọa độ của các hình chữ nhật bao quanh.  
- Đại diện JSON để dễ dàng xử lý tiếp theo.  
- Góc nghiêng được phát hiện và bất kỳ cảnh báo nào.

Bây giờ bạn có thể đưa `result.recognitionText` vào logic nghiệp vụ của mình — lưu trữ, lập chỉ mục, hoặc truyền cho dịch vụ khác.

## Các vấn đề thường gặp và Giải pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|----------|
| **Ký tự rác** | Chọn sai ngôn ngữ | Đặt enum `Language` đúng (ví dụ `Language.Fra` cho tiếng Pháp). |
| **Không trả về văn bản** | Vùng nhận dạng không bao phủ văn bản | Điều chỉnh tọa độ `Rectangle` hoặc loại bỏ `RecognitionAreas` để xử lý toàn bộ hình ảnh. |
| **Hiệu suất chậm** | Hình ảnh quá lớn hoặc độ phân giải cao | Thu nhỏ hình ảnh trước khi OCR hoặc tăng bộ nhớ cấp phát cho JVM. |
| **Cảnh báo định dạng không hỗ trợ** | Định dạng hình ảnh không được nhận dạng | Chuyển đổi hình ảnh sang PNG, JPEG hoặc TIFF trước khi xử lý. |

## Câu hỏi thường gặp

**H: Có thể nhận dạng nhiều ngôn ngữ trong một lần gọi OCR không?**  
Đ: Có. Sử dụng `settings.setLanguage(Language.Eng | Language.Fra)` để bật nhận dạng đa ngôn ngữ.

**H: Aspose.OCR hỗ trợ những định dạng hình ảnh nào?**  
Đ: PNG, JPEG, BMP, TIFF, GIF và một số định dạng khác. Chỉ cần cung cấp đường dẫn tệp đúng.

**H: Có giới hạn kích thước cho hình ảnh không?**  
Đ: Không có giới hạn cứng, nhưng hình ảnh quá lớn sẽ tăng mức sử dụng bộ nhớ và thời gian xử lý. Nên cân nhắc giảm kích thước các tệp lớn.

**H: Làm sao để có giấy phép sản xuất?**  
Đ: Mua giấy phép từ trang web Aspose và áp dụng nó qua lớp `License` như trong tài liệu Aspose.

**H: Có thể trích xuất văn bản trực tiếp từ trang PDF không?**  
Đ: Không trực tiếp bằng Aspose.OCR. Cần chuyển trang PDF sang hình ảnh trước (ví dụ dùng Aspose.PDF) rồi mới chạy OCR.

## Kết luận

Bạn đã thấy cách **trích xuất văn bản từ hình ảnh** bằng Aspose.OCR cho Java đồng thời lựa chọn ngôn ngữ phù hợp và giới hạn nhận dạng trong các vùng cụ thể. Cách tiếp cận này mang lại OCR chính xác, hiệu suất cao và có thể nhúng vào bất kỳ quy trình làm việc nào dựa trên Java — từ hệ thống quản lý tài liệu đến các pipeline thu thập dữ liệu. Sẵn sàng tiến bước? Hãy thử thay đổi enum ngôn ngữ, khám phá các vùng nhận dạng khác nhau, và tích hợp kết quả vào logic ứng dụng của bạn.

---

**Cập nhật lần cuối:** 2026-02-12  
**Kiểm tra với:** Aspose.OCR 24.11 for Java  
**Tác giả:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}