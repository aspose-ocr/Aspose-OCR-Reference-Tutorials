---
category: general
date: 2026-02-22
description: Tạo PDF có thể tìm kiếm từ PDF đã quét bằng Aspose OCR trong Java. Học
  cách chuyển đổi PDF đã quét, nén hình ảnh PDF và nhận dạng OCR cho PDF một cách
  hiệu quả.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: vi
og_description: Tạo PDF có thể tìm kiếm từ PDF đã quét bằng Aspose OCR trong Java.
  Hướng dẫn từng bước này chỉ cách chuyển đổi PDF đã quét, nén hình ảnh PDF và nhận
  dạng OCR cho PDF.
og_title: Tạo PDF có thể tìm kiếm – Hướng dẫn Java để chuyển đổi PDF đã quét
tags:
- Java
- OCR
- PDF
- Aspose
title: Tạo PDF có thể tìm kiếm – Hướng dẫn Java để chuyển đổi PDF đã quét
url: /vi/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tạo PDF có thể tìm kiếm – Hướng dẫn Java để Chuyển đổi PDF đã quét

Bạn đã bao giờ cần **tạo PDF có thể tìm kiếm** từ một đống tài liệu đã quét chưa? Đó là một vấn đề phổ biến—các PDF của bạn trông ổn, nhưng bạn không thể nhấn *Ctrl + F* để tìm bất cứ thứ gì. Tin tốt là gì? Với vài dòng Java và Aspose OCR, bạn có thể biến những PDF chỉ chứa hình ảnh thành các tệp có thể tìm kiếm hoàn toàn, **convert scanned PDF** sang văn bản, và thậm chí giảm kích thước kết quả bằng cách **compressing PDF images**.  

Trong tutorial này, chúng tôi sẽ hướng dẫn qua một ví dụ đầy đủ, có thể chạy được, giải thích lý do mỗi cài đặt quan trọng, và cho bạn thấy cách điều chỉnh quy trình cho các trường hợp đặc biệt như quét đa trang hoặc hình ảnh độ phân giải thấp. Khi kết thúc, bạn sẽ có một đoạn mã vững chắc, sẵn sàng cho sản xuất, mà **recognize pdf ocr** một cách đáng tin cậy và tạo ra một tài liệu có thể tìm kiếm gọn gàng.

---

## Những gì bạn cần

- **Java 17** (hoặc bất kỳ JDK gần đây nào; API không phụ thuộc vào JDK)  
- Thư viện **Aspose.OCR for Java** – bạn có thể lấy nó từ Maven Central (`com.aspose:aspose-ocr`)  
- Một PDF đã quét (chỉ hình ảnh) mà bạn muốn làm có thể tìm kiếm  
- Một IDE hoặc trình soạn thảo văn bản mà bạn cảm thấy thoải mái (IntelliJ, VS Code, Eclipse…)

Không có khung công tác nặng, không có dịch vụ bên ngoài—chỉ Java thuần và một JAR của bên thứ ba duy nhất.  

---

![tạo pdf có thể tìm kiếm ví dụ](placeholder-image.png "Minh họa PDF có thể tìm kiếm được tạo từ tài liệu đã quét")

*Văn bản thay thế hình ảnh:* **create searchable pdf** illustration showing before‑and‑after of a scanned PDF turned into searchable text.

---

## Bước 1 – Khởi tạo Engine OCR  

Điều đầu tiên bạn phải làm là khởi tạo một thể hiện `OcrEngine`. Hãy nghĩ nó như bộ não sẽ phân tích từng bitmap trong PDF và tạo ra các ký tự Unicode.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Pro tip:** Nếu bạn dự định xử lý nhiều PDF liên tiếp, hãy tái sử dụng cùng một `OcrEngine` thay vì tạo mới mỗi lần. Điều này tiết kiệm vài mili giây và giảm việc tiêu tốn bộ nhớ.

---

## Bước 2 – Cấu hình tùy chọn OCR cho PDF  

Aspose cho phép bạn tinh chỉnh cách PDF đầu ra được tạo. Ba cài đặt dưới đây là những yếu tố có ảnh hưởng lớn nhất tới **compress pdf images** trong khi vẫn giữ khả năng tìm kiếm.  

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi là mức cân bằng tốt; giá trị thấp hơn sẽ tăng tốc nhưng có thể bỏ lỡ các phông chữ nhỏ.  
- **CompressImages** – kích hoạt nén PNG không mất dữ liệu; PDF có thể tìm kiếm vẫn sắc nét nhưng nhẹ hơn.  
- **EmbedOriginalImages** – nếu không bật cờ này, engine sẽ loại bỏ raster gốc, chỉ để lại văn bản ẩn. Giữ lại hình ảnh đảm bảo PDF trông giống hệt bản quét, điều mà nhiều nhóm tuân thủ yêu cầu.

---

## Bước 3 – Tải PDF đã quét của bạn vào `OcrInput`  

Aspose đọc tệp nguồn thông qua một lớp bao `OcrInput`. Bạn có thể thêm nhiều tệp, nhưng trong bản demo này chúng ta tập trung vào một **image PDF** duy nhất.  

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Why not just pass a `File`?** Sử dụng `OcrInput` mang lại cho bạn khả năng nối nhiều PDF hoặc thậm chí trộn các tệp hình ảnh (PNG, JPEG) trước khi OCR. Đây là mẫu được khuyến nghị khi bạn **convert scanned pdf** có thể được chia thành nhiều nguồn.

---

## Bước 4 – Thực hiện OCR và nhận PDF có thể tìm kiếm dưới dạng mảng byte  

Bây giờ phép màu xảy ra. Engine phân tích từng trang, chạy OCR và tạo một PDF mới chứa cả hình ảnh gốc và lớp văn bản ẩn.  

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Nếu bạn cần văn bản thô cho các mục đích khác (ví dụ: lập chỉ mục), bạn cũng có thể gọi `ocrEngine.recognize(ocrInput)` để nhận về một `String`. Nhưng đối với mục tiêu **create searchable pdf**, mảng byte là thứ bạn sẽ ghi ra đĩa.

---

## Bước 5 – Lưu PDF có thể tìm kiếm ra đĩa  

Cuối cùng, ghi mảng byte vào một tệp. NIO của Java giúp việc này chỉ cần một dòng.  

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Khi bạn mở `searchable_output.pdf` trong Adobe Acrobat hoặc bất kỳ trình xem hiện đại nào, bạn sẽ nhận thấy giờ có thể chọn, sao chép và tìm kiếm văn bản—đúng như lời hứa của quá trình chuyển đổi **image pdf to text**.

---

## Chuyển đổi PDF đã quét sang Văn bản với OCR (Tùy chọn)

Đôi khi bạn chỉ cần văn bản thuần đã trích xuất, không phải PDF mới. Bạn có thể tái sử dụng cùng một engine:  

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Đoạn mã này minh họa cách dễ dàng **recognize pdf ocr** cho các quy trình tiếp theo như đưa vào chỉ mục tìm kiếm hoặc thực hiện phân tích ngôn ngữ tự nhiên.

---

## Nén hình ảnh PDF để có tệp nhỏ hơn  

Nếu các bản quét nguồn của bạn rất lớn (ví dụ: quét màu 600 dpi), PDF có thể tìm kiếm kết quả vẫn có thể nặng. Ngoài cờ `setCompressImages(true)`, bạn có thể giảm độ phân giải thủ công trước khi OCR:  

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

Giảm DPI sẽ giảm kích thước tệp khoảng một nửa, nhưng hãy kiểm tra độ đọc được—một số phông chữ sẽ không đọc được dưới 150 dpi. Sự cân bằng giữa **compress pdf images** và độ chính xác OCR là điều bạn sẽ quyết định dựa trên hạn chế lưu trữ.

---

## Giải thích các cài đặt OCR cho PDF  

| Cài đặt                | Ảnh hưởng tới đầu ra                         | Trường hợp sử dụng điển hình                                   |
|------------------------|----------------------------------------------|--------------------------------------------------------------|
| `setOutputDpi(int)`    | Điều khiển độ phân giải raster của đầu ra OCR | Lưu trữ chất lượng cao (300 dpi) so với PDF web nhẹ (150 dpi) |
| `setCompressImages`    | Kích hoạt nén PNG                            | Khi bạn cần gửi PDF qua email hoặc lưu trữ trên đám mây       |
| `setEmbedOriginalImages`| Giữ nguyên bản quét hiển thị                 | Tài liệu pháp lý hoặc tuân thủ cần giữ nguyên hình ảnh gốc    |
| `setLanguage` (optional) | Buộc mô hình ngôn ngữ (ví dụ: "eng")        | Tập dữ liệu đa ngôn ngữ mà phát hiện tự động mặc định có thể sai |

Hiểu các tùy chọn này giúp bạn **recognize pdf ocr** một cách thông minh hơn và tránh bẫy “văn bản mờ”.

---

## Image PDF to Text – Những khó khăn thường gặp và Cách tránh  

1. **Low‑resolution scans** – Độ chính xác OCR giảm mạnh dưới 150 dpi. Tăng độ phân giải nguồn trước khi đưa vào Aspose, hoặc yêu cầu DPI cao hơn từ máy quét.  
2. **Rotated pages** – Nếu các trang được quét nghiêng, bật tự động xoay: `pdfOcrOptions.setAutoRotate(true);`.  
3. **Encrypted PDFs** – Engine không thể đọc các tệp được bảo vệ bằng mật khẩu; hãy giải mã trước bằng `PdfDocument` từ Aspose.PDF.  
4. **Mixed raster and text** – Một số PDF đã chứa lớp văn bản ẩn. Chạy OCR lại có thể tạo trùng lặp văn bản. Sử dụng `PdfOcrOptions.setSkipExistingText(true);` để giữ nguyên lớp gốc.  

Giải quyết những vấn đề này đảm bảo quy trình **create searchable pdf** của bạn mạnh mẽ trong các bộ sưu tập tài liệu thực tế.

---

## Ví dụ Hoạt động đầy đủ (Tất cả các bước trong một tệp)

Dưới đây là lớp Java hoàn chỉnh mà bạn có thể sao chép‑dán vào IDE. Thay `YOUR_DIRECTORY` bằng đường dẫn thư mục thực tế.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}