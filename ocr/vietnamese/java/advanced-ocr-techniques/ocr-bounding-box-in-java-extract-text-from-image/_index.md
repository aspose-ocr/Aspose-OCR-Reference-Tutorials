---
category: general
date: 2026-06-16
description: Bài hướng dẫn bounding box OCR trong Java cho thấy cách trích xuất văn
  bản từ hình ảnh, đọc văn bản từ hình ảnh và lấy điểm tin cậy OCR cho các tệp JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: vi
og_description: OCR bounding box trong Java cho phép bạn nhận dạng văn bản từ các
  tệp JPG, trích xuất văn bản từ hình ảnh và xem điểm tin cậy OCR — tất cả trong một
  ví dụ mã đơn giản.
og_title: Hộp bao OCR trong Java – Trích xuất văn bản từ ảnh
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Hộp giới hạn OCR trong Java – Trích xuất văn bản từ hình ảnh
url: /vi/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box trong Java – Extract Text from Image

Bạn đã bao giờ tự hỏi làm thế nào để lấy **ocr bounding box** cho mỗi đoạn văn bản trong một hình ảnh Java chưa? Trong hướng dẫn này, chúng tôi sẽ chỉ cho bạn cách **extract text from image** files, **read text from image**, và thậm chí xem **ocr confidence score** khi bạn **recognize text from jpg** files. Câu trả lời ngắn gọn? Một vài dòng mã sử dụng một thư viện OCR hiện đại, cộng với một chút giải thích tại sao mỗi lời gọi lại quan trọng.

Bạn sẽ tìm thấy dưới đây một ví dụ hoàn chỉnh, sẵn sàng chạy, phân tích từng bước, và một vài mẹo thực tế mà bạn có thể sao chép ngay vào dự án của mình. Khi kết thúc, bạn sẽ có thể xuất ra một thứ gì đó giống như:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Những gì bạn cần

- **Java 11** hoặc mới hơn (cú pháp dưới đây sử dụng từ khóa `var` để ngắn gọn, nhưng bạn có thể bỏ nó cho các JDK cũ hơn).  
- Một thư viện OCR cung cấp API Java – trong hướng dẫn này chúng tôi sẽ sử dụng **[Tesseract4J](https://github.com/nguyenq/tess4j)**, một lớp bao bọc nhẹ quanh engine Tesseract phổ biến.  
- Một ảnh JPEG (`.jpg`) chứa văn bản in rõ ràng.  
- IDE yêu thích của bạn (IntelliJ IDEA, Eclipse, VS Code…) – bất kỳ cái nào cũng được.

Nếu bạn chưa có thư viện, chỉ cần thêm phụ thuộc Maven này:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Bây giờ chúng ta cùng bắt đầu.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Cài đặt Engine

Điều đầu tiên bạn phải làm là tạo một thể hiện của engine OCR. Hãy nghĩ nó như việc bật máy quét sẽ sau này đọc các pixel.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Tại sao điều này quan trọng:**  
Không thiết lập `datapath`, Tesseract sẽ không biết vị trí các gói ngôn ngữ và bạn sẽ nhận được lỗi “Failed loading language” khó hiểu. Lệnh `setLanguage` là tùy chọn nếu bạn chỉ cần gói tiếng Anh mặc định, nhưng việc chỉ định rõ ràng làm cho mã dễ hiểu hơn cho những người đọc sau.

## Tải ảnh bạn muốn xử lý

Tiếp theo, cung cấp cho engine ảnh JPEG bạn muốn phân tích. Thư viện chấp nhận một `File` hoặc `BufferedImage`; chúng ta sẽ dùng `File` để đơn giản.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Mẹo chuyên nghiệp:**  
Nếu ảnh của bạn nằm trong resources (ví dụ, bên trong một JAR), hãy sử dụng `getResourceAsStream` và bọc nó bằng `ImageIO.read`. Như vậy hướng dẫn sẽ hoạt động cả khi chạy cục bộ và trong ứng dụng đã đóng gói.

## Thực hiện nhận dạng OCR

Bây giờ chúng ta thực sự yêu cầu engine đọc hình ảnh. Kết quả là một chuỗi văn bản thuần, nhưng chúng ta cũng muốn **ocr confidence score** và **ocr bounding box** cho mỗi dòng.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Tại sao chúng ta dùng `getWords` thay vì `doOCR` đơn giản:**  
`doOCR` cung cấp cho bạn chuỗi thô nhưng bỏ qua thông tin không gian. Bằng cách gọi `getWords` với `RIL_WORD` (hoặc `RIL_TEXTLINE` nếu bạn muốn hộp mức dòng), chúng ta nhận được một danh sách các đối tượng `Word` mà mỗi đối tượng chứa văn bản, độ tin cậy và hình chữ nhật bao quanh. Đó là cốt lõi của tính năng **ocr bounding box**.

## Hiểu đầu ra

Chạy đoạn mã trên với một ảnh JPEG sạch sẽ sẽ cho ra đầu ra tương tự như:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – các ký tự đã được nhận dạng.  
- **Confidence** – giá trị số thực từ 0 đến 1; càng cao nghĩa là engine càng chắc chắn.  
- **Box** – hình chữ nhật bao quanh từ trong tọa độ pixel (x, y, width, height).  

Bây giờ bạn có thể **read text from image** và cũng biết chính xác vị trí của mỗi đoạn trên canvas — hoàn hảo cho việc tô sáng, cắt, hoặc đưa vào các pipeline NLP tiếp theo.

## Các trường hợp góc cạnh & Những bẫy thường gặp

| Tình huống | Cần chú ý | Cách khắc phục / Giải pháp |
|-----------|-----------|----------------------------|
| Hình ảnh mờ hoặc độ tương phản thấp | Điểm tin cậy giảm mạnh (thường dưới 0.6). | Tiền xử lý bằng OpenCV: tăng độ tương phản, áp dụng ngưỡng. |
| JPEG chứa văn bản xoay | Các bounding box bị lệch hoặc thiếu. | Sử dụng `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` để Tesseract tự động phát hiện hướng. |
| Ảnh lớn gây OutOfMemoryError | Bộ nhớ heap Java đầy khi tải ảnh lớn. | Thu nhỏ ảnh trước khi OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Bạn cần hộp mức dòng thay vì mức từ | `RIL_WORD` trả về hộp theo từ. | Chuyển sang `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Ký tự không phải tiếng Anh hiển thị thành � | Dữ liệu ngôn ngữ chưa được tải. | Tải file `.traineddata` phù hợp và chỉ định `setDatapath` tới thư mục chứa nó. |

Giải quyết những vấn đề này sớm sẽ tiết kiệm cho bạn hàng giờ gỡ lỗi sau này.

## Ví dụ Hoạt động đầy đủ (Tất cả các bước trong một file)

Dưới đây là một lớp Java tự chứa mà bạn có thể sao chép‑dán vào thư mục `src/main/java` và chạy bằng `mvn exec:java`. Nó tập hợp mọi thứ chúng ta đã thảo luận.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Bạn nên học gì tiếp theo?

Những hướng dẫn sau đây bao gồm các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật đã trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoàn chỉnh với giải thích từng bước để giúp bạn nắm vững các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Trích xuất Văn bản từ Hình ảnh Java với Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Trích xuất Văn bản Hình ảnh – Cơ bản OCR với Aspose.OCR cho Java](/ocr/english/java/ocr-basics/)
- [Cách OCR Văn bản Hình ảnh với Ngôn ngữ Sử dụng Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}