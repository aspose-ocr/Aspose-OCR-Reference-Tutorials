---
date: 2026-06-24
description: Tìm hiểu cách OCR văn bản hình ảnh với lựa chọn ngôn ngữ bằng Aspose.OCR
  cho Java. Hướng dẫn từng bước này bao gồm trích xuất văn bản Java, OCR skew correction
  và nhiều hơn nữa.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Cách thực hiện chỉnh sửa độ nghiêng OCR và lựa chọn ngôn ngữ với Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Cách thực hiện chỉnh sửa độ nghiêng OCR và lựa chọn ngôn ngữ với Aspose.OCR
url: /vi/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Thực Hiện Sửa Độ Nghiêng OCR và Lựa Chọn Ngôn Ngữ với Aspose.OCR

## Giới thiệu

Việc trích xuất văn bản từ các tệp hình ảnh là một nhu cầu phổ biến, dù bạn đang số hoá tài liệu đã quét, xử lý biên lai, hay xây dựng kho lưu trữ có thể tìm kiếm. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ thực tế, đầy đủ, cho thấy **cách OCR văn bản hình ảnh** với cài đặt ngôn ngữ cụ thể, để bạn có thể tích hợp OCR đáng tin cậy vào các ứng dụng Java ngay hôm nay. Bạn cũng sẽ thấy cách xử lý **sửa độ nghiêng OCR** và nhận dạng dựa trên vùng để đạt độ chính xác tối ưu, giúp **cải thiện độ chính xác OCR** lên tới 30 % trên các bản quét có góc nghiêng.

## Câu trả lời nhanh
- **Thư viện nào hỗ trợ OCR trong Java?** Aspose.OCR for Java  
- **Cài đặt nào chọn ngôn ngữ?** `settings.setLanguage(Language.Eng)` (hoặc bất kỳ ngôn ngữ nào được hỗ trợ)  
- **Có cần giấy phép cho việc phát triển không?** Giấy phép dùng thử miễn phí hoạt động cho việc thử nghiệm; giấy phép thương mại cần thiết cho môi trường sản xuất.  
- **Có thể giới hạn OCR trong một vùng của hình ảnh không?** Có, sử dụng `RecognitionSettings.setRecognitionAreas()` với các hình chữ nhật.  
- **Thời gian chạy điển hình là bao lâu?** Vài giây cho mỗi trang trên một laptop tiêu chuẩn, tùy thuộc vào kích thước hình ảnh và độ phức tạp của ngôn ngữ.  

`Language` là một enumeration liệt kê các ngôn ngữ OCR được Aspose.OCR hỗ trợ, chẳng hạn như English, French, Spanish, v.v.

## Sửa Độ Nghiêng OCR là gì?

Sửa độ nghiêng OCR là quá trình phát hiện và làm thẳng các dòng văn bản bị nghiêng trước khi nhận dạng ký tự. Bằng cách căn chỉnh đường cơ sở của văn bản, engine OCR có thể áp dụng các mô hình ngôn ngữ một cách hiệu quả hơn, giảm thiểu các lỗi nhận dạng do quét góc nghiêng. Bước này cải thiện chất lượng hình ảnh đầu vào, cho phép các thuật toán nhận dạng tập trung vào hình dạng ký tự thực tế thay vì các biến dạng do xoay.

## Tại sao Sửa Độ Nghiêng OCR Cải Thiện Độ Chính Xác

Khi văn bản bị nghiêng, hình dạng ký tự bị biến dạng, dẫn đến tỷ lệ lỗi cao tới 20 %. Áp dụng **ocr skew correction** loại bỏ biến dạng đó, cho phép engine tập trung vào các glyph thực. Trong các bài kiểm tra chuẩn, Aspose.OCR đạt mức tăng 15‑30 % độ chính xác nhận dạng trên các tài liệu có góc quay 10‑15° sau khi áp dụng sửa độ nghiêng.

## Tại sao nên dùng Aspose.OCR với Lựa Chọn Ngôn Ngữ?

Việc chọn đúng ngôn ngữ của văn bản nguồn cho phép engine OCR sử dụng từ điển và mô hình ký tự riêng cho ngôn ngữ, nâng cao đáng kể độ chính xác nhận dạng và giảm thời gian xử lý. Ngoài ra, Aspose.OCR cung cấp kiểm soát tinh chỉnh cho việc sửa độ nghiêng, lựa chọn vùng và định dạng đầu ra, làm cho nó trở thành lựa chọn đa năng cho các pipeline xử lý tài liệu đa ngôn ngữ.

- **Hỗ trợ đa ngôn ngữ** – Chọn ngôn ngữ chính xác có trong hình ảnh để tăng độ chính xác.  
- **Kiểm soát tinh chỉnh** – Điều chỉnh độ nghiêng, định nghĩa vùng nhận dạng, và thiết lập hành vi tự động sửa độ nghiêng.  
- **API Java thuần** – Không phụ thuộc vào native, dễ tích hợp vào bất kỳ dự án Java nào.  
- **Dữ liệu kết quả phong phú** – Nhận văn bản thuần, JSON, các hình chữ nhật bao quanh và cảnh báo trong một lần gọi.  
- **Khả năng định lượng** – Aspose.OCR hỗ trợ **hơn 50** định dạng đầu vào và đầu ra và có thể xử lý **lô ảnh 500 trang** mà không cần tải toàn bộ tài liệu vào bộ nhớ.

## Yêu cầu trước

Trước khi bắt đầu, hãy chắc chắn rằng bạn đã có:

- **Java Development Kit (JDK)** được cài đặt (JDK 8 trở lên).  
- Thư viện **Aspose.OCR for Java** – tải về từ trang chính thức [tại đây](https://reference.aspose.com/ocr/java/).  
- Một tệp hình ảnh chứa văn bản bạn muốn trích xuất, ví dụ `p3.png`.  

## Nhập Gói

Các lệnh import sau cung cấp quyền truy cập vào các lớp OCR cốt lõi và các tiện ích chuẩn của Java.  
`import com.aspose.ocr.*;` – nhập engine OCR chính.  
`import com.aspose.ocr.config.*;` – chứa các đối tượng cấu hình như `RecognitionSettings`.  
`import java.awt.Rectangle;` – dùng để định nghĩa các vùng nhận dạng.  

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

## Cách Áp Dụng Sửa Độ Nghiêng OCR trong Java?

Tải hình ảnh, tắt chế độ phát hiện độ nghiêng tự động, và hoặc cung cấp góc đo được hoặc để engine tính toán bằng `settings.setAutoSkew(false)`. Engine OCR sẽ đầu tiên làm thẳng hình ảnh dựa trên góc đã cung cấp hoặc đã phát hiện, sau đó tiến hành nhận dạng ký tự. Cách tiếp cận hai bước này đảm bảo mọi độ nghiêng được loại bỏ trước khi áp dụng các mô hình ngôn ngữ, mang lại kết quả văn bản sạch hơn và giảm thiểu các lỗi nhận dạng.

## Hướng Dẫn Từng Bước

### Bước 1: Thiết Lập Thư Mục Tài Liệu

Tạo một đối tượng `File` trỏ tới thư mục chứa ảnh nguồn của bạn. Điều này giúp việc xử lý đường dẫn trở nên di động trên các hệ điều hành khác nhau.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Thay `"Your Document Directory"` bằng đường dẫn tuyệt đối nơi chứa `p3.png`.

### Bước 2: Định Nghĩa Đường Dẫn Ảnh

Khởi tạo một đối tượng `File` cho ảnh cụ thể bạn muốn xử lý. Sử dụng đối tượng `File` giúp bạn dễ dàng truy cập siêu dữ liệu của tệp nếu cần sau này.

```java
// The image path
String file = dataDir + "p3.png";
```

Đảm bảo biến `file` trỏ tới đúng ảnh bạn dự định xử lý.

### Bước 3: Tạo Instance API Aspose.OCR

Lớp `AsposeOCR` là điểm vào cho tất cả các thao tác OCR. Nó bao bọc engine, quản lý tài nguyên và cung cấp phương thức `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

Đối tượng `AsposeOCR` cho phép bạn truy cập vào mọi thao tác OCR.

### Bước 4: Đặt Tùy Chọn Nhận Dạng (Lựa Chọn Ngôn Ngữ)

`RecognitionSettings` là container cấu hình của Aspose.OCR, cho phép bạn tinh chỉnh quá trình OCR.  

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

1. Tắt auto‑skew vì chúng ta cung cấp giá trị nghiêng thủ công.  
2. Định nghĩa một vùng hình chữ nhật (`RecognitionAreas`) để giới hạn OCR chỉ ở phần ảnh thực sự chứa văn bản.  
3. Đặt **ngôn ngữ** thành tiếng Anh (`Language.Eng`). Thay đổi thành `Language.Fra`, `Language.Spa`, v.v., tùy vào ảnh nguồn của bạn.

### Bước 5: Thực Hiện OCR và Lấy Kết Quả

Gọi `recognizePage` sẽ chạy engine OCR sử dụng ảnh và các cài đặt bạn đã định nghĩa. Kết quả được lưu trong một đối tượng `RecognitionResult`, tổng hợp tất cả dữ liệu hữu ích.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Lệnh `RecognizePage` chạy engine OCR với ảnh và các cài đặt đã cung cấp. Kết quả được lưu trong đối tượng `RecognitionResult`.

### Bước 6: In và Sử Dụng Kết Quả

Đầu ra console hiển thị:

- Văn bản đã trích xuất đầy đủ (`recognitionText`).  
- Văn bản cho mỗi hình chữ nhật đã định nghĩa (`recognitionAreasText`).  
- Tọa độ các hình chữ nhật bao quanh.  
- Đại diện JSON để dễ dàng xử lý tiếp theo.  
- Góc nghiêng đã phát hiện và bất kỳ cảnh báo nào.

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

Đầu ra console hiển thị văn bản trích xuất đầy đủ, văn bản theo vùng, các bounding box, JSON, góc nghiêng và cảnh báo. Bạn có thể đưa `result.recognitionText` vào logic nghiệp vụ của mình — lưu trữ, lập chỉ mục, hoặc truyền cho dịch vụ khác.

## Các Vấn Đề Thường Gặp và Giải Pháp

| Vấn đề | Nguyên nhân | Giải pháp |
|-------|-------------|-----------|
| **Ký tự rác** | Ngôn ngữ được chọn không đúng | Đặt đúng enum `Language` (ví dụ, `Language.Fra` cho tiếng Pháp). |
| **Không có văn bản trả về** | Vùng nhận dạng không bao phủ văn bản | Điều chỉnh tọa độ `Rectangle` hoặc bỏ `RecognitionAreas` để xử lý toàn bộ ảnh. |
| **Hiệu năng chậm** | Ảnh quá lớn hoặc độ phân giải cao | Thu nhỏ ảnh trước khi OCR hoặc tăng bộ nhớ JVM. |
| **Cảnh báo định dạng không hỗ trợ** | Định dạng ảnh không được nhận dạng | Chuyển đổi ảnh sang PNG, JPEG hoặc TIFF trước khi xử lý. |

## Câu Hỏi Thường Gặp

**H: Có thể nhận dạng nhiều ngôn ngữ trong một lần gọi OCR không?**  
Đ: Có. Sử dụng `settings.setLanguage(Language.Eng | Language.Fra)` để bật nhận dạng đa ngôn ngữ.

**H: Aspose.OCR hỗ trợ những định dạng ảnh nào?**  
Đ: PNG, JPEG, BMP, TIFF, GIF và một số định dạng khác. Chỉ cần cung cấp đường dẫn tệp đúng.

**H: Có giới hạn kích thước ảnh không?**  
Đ: Không có giới hạn cứng, nhưng xử lý ảnh lớn hơn 10 MB có thể tăng mức sử dụng bộ nhớ và thời gian chạy. Nên thu nhỏ các tệp lớn.

**H: Làm sao để có giấy phép sản xuất?**  
Đ: Mua giấy phép từ trang web Aspose và áp dụng nó qua lớp `License` như trong tài liệu Aspose.

**H: Có thể trích xuất văn bản trực tiếp từ trang PDF không?**  
Đ: Không trực tiếp bằng Aspose.OCR. Cần chuyển trang PDF sang ảnh trước (ví dụ, dùng Aspose.PDF) rồi mới chạy OCR.

## Kết Luận

Bạn đã thấy cách **trích xuất văn bản từ hình ảnh** bằng Aspose.OCR cho Java, đồng thời lựa chọn ngôn ngữ phù hợp và áp dụng **sửa độ nghiêng OCR** để nâng cao độ tin cậy. Cách tiếp cận này mang lại OCR chính xác, hiệu suất cao, có thể nhúng vào bất kỳ quy trình làm việc nào dựa trên Java — từ hệ thống quản lý tài liệu đến pipeline thu thập dữ liệu. Hãy thử nghiệm các enum `Language` khác nhau, tinh chỉnh `RecognitionAreas`, và tích hợp đầu ra JSON vào phân tích downstream để có giải pháp thực sự đầu‑cuối‑đầu.

---

**Cập nhật lần cuối:** 2026-06-24  
**Kiểm thử với:** Aspose.OCR 24.11 for Java  
**Tác giả:** Aspose

## Các Hướng Dẫn Liên Quan

- [Cách tính góc nghiêng java bằng Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Cách OCR Văn Bản Hình Ảnh với Ngôn Ngữ Sử Dụng Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR Nhận Dạng Tài Liệu PDF trong Aspose.OCR cho Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}