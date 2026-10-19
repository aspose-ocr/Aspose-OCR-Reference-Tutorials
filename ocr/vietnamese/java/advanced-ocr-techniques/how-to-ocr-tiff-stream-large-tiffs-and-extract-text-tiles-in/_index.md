---
category: general
date: 2026-04-29
description: Học cách OCR các tệp TIFF bằng chế độ streaming của Aspose OCR. Hướng
  dẫn này chỉ cho bạn cách trích xuất các ô văn bản từ các ảnh TIFF dạng lưới một
  cách hiệu quả.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: vi
og_description: cách OCR tiff bằng Aspose OCR streaming. Mã từng bước để trích xuất
  các khối văn bản từ các ảnh TIFF lớn.
og_title: Cách OCR TIFF – Hướng Dẫn Streaming Toàn Diện
tags:
- OCR
- Java
- Aspose
- TIFF
title: Cách OCR TIFF – Xử lý luồng các tệp TIFF lớn và trích xuất các ô văn bản trong
  Java
url: /vi/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# cách ocr tiff – Xử lý luồng các TIFF lớn và Trích xuất các khối văn bản trong Java

Bạn đã bao giờ tự hỏi **cách ocr tiff** các tệp quá lớn để tải vào bộ nhớ cùng một lúc chưa? Bạn không phải là người duy nhất. Nhiều nhà phát triển gặp khó khăn khi các ảnh TIFF của họ được chia thành hàng chục khối, và lệnh `ocrEngine.recognize()` thông thường chỉ “đơ”.  

Tin tốt? Chế độ streaming của Aspose OCR cho phép bạn cung cấp mỗi khối dưới dạng một luồng riêng, vì vậy bạn có thể **trích xuất các khối văn bản** mà không làm tràn heap. Trong hướng dẫn này, chúng tôi sẽ đi qua một ví dụ Java hoàn chỉnh, sẵn sàng chạy, giải thích lý do mỗi dòng quan trọng, và chỉ ra những bẫy cần tránh.

> **Bạn sẽ nhận được:** một chương trình có thể chạy được, ghép các TIFF dạng khối ngay khi đọc, in ra văn bản đã kết hợp, và cho bạn biết cách điều chỉnh mã cho các ngôn ngữ hoặc định dạng ảnh khác.

---

## Các yêu cầu trước

- **Java 17** trở lên (mã sử dụng try‑with‑resources, vì vậy JDK 8+ cũng hoạt động, nhưng JDK 17 là LTS hiện tại).
- Thư viện **Aspose.OCR for Java** (v23.10 trở lên). Thêm qua Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Một thư mục chứa các khối TIFF riêng lẻ (ví dụ: `tile_0.tif`, `tile_1.tif`, …).  
- Tùy chọn: một IDE như IntelliJ IDEA hoặc VS Code – nhưng một trình soạn thảo văn bản đơn giản cũng đủ.

---

## Bước 1 – Chuẩn bị đường dẫn các khối (Tại sao quan trọng)

Trước khi engine OCR có thể làm bất cứ việc gì, nó cần biết mỗi phần ảnh nằm ở đâu. Việc hard‑code các đường dẫn là ổn cho bản demo, nhưng trong môi trường thực tế bạn có thể quét một thư mục hoặc đọc từ file manifest.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Mẹo chuyên nghiệp:** giữ các khối theo thứ tự từ điển (0, 1, 2…) vì engine sẽ nối văn bản đã nhận dạng theo cùng một thứ tự mà bạn cung cấp các luồng.

---

## Bước 2 – Bật chế độ Streaming trên OCR Engine (Từ khóa chính)

Bây giờ chúng ta tạo thể hiện `OcrEngine` và bật streaming. Đây là phần cốt lõi của **cách ocr tiff** mà không cần tải toàn bộ ảnh vào RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Tại sao cần streaming?**  
Khi gọi `setEnableStreaming(true)`, engine coi mỗi `ImageStream` đến như là phần tiếp nối của luồng trước. Nó xây dựng một canvas ảo nội bộ, ghép các khối lại một cách ảo, và thực hiện OCR một lần duy nhất ở cuối. Điều này tránh lỗi “OutOfMemoryError” sẽ xảy ra nếu bạn cố gắng tải một TIFF đa gigabyte trong một lần.

---

## Bước 3 – Thêm mỗi khối dưới dạng Input Stream (Từ khóa phụ)

Đây là vòng lặp đưa mỗi khối vào engine. Khối `try‑with‑resources` đảm bảo handle file được đóng ngay, điều này rất quan trọng khi bạn phải xử lý hàng chục file.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Lưu ý cụm từ **extract text tiles** được nhúng tự nhiên: mỗi vòng lặp *trích xuất* văn bản từ một khối và thêm vào tập kết quả đang tăng dần.

---

## Bước 4 – Thực hiện nhận dạng và xuất văn bản đã kết hợp (Từ khóa chính)

Sau khi tất cả các khối đã được đưa vào hàng đợi, một lời gọi duy nhất thực hiện OCR trên ảnh ảo. Kết quả chứa toàn bộ văn bản, giống như khi bạn có một TIFF khổng lồ duy nhất.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Kết quả mong đợi** (giả sử các khối chứa cụm từ “Hello World” được chia ra):

```
=== OCR Output ===
Hello World
```

Nếu các khối của bạn có nhiều dòng hơn, chúng sẽ xuất hiện theo cùng thứ tự bạn cung cấp. Bạn cũng có thể ghi `ocrResult.getText()` ra file để xử lý tiếp.

---

## Bước 5 – Ví dụ đầy đủ, có thể chạy (Tất cả các bước trong một nơi)

Dưới đây là chương trình hoàn chỉnh mà bạn có thể sao chép‑dán vào `StreamingExample.java`. Nó bao gồm mọi import, chú thích và xử lý lỗi.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Lưu, biên dịch và chạy:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Bạn sẽ thấy văn bản OCR đã được nối in ra console.

---

## Mẹo nâng cao & Những bẫy thường gặp (Tại sao cách này hoạt động)

| Vấn đề | Nguyên nhân | Cách khắc phục / Tối ưu |
|-------|-------------|------------------------|
| **Lỗi out‑of‑memory** | Tải một TIFF kích thước đầy đủ vào `BufferedImage` tiêu tốn toàn bộ heap. | Sử dụng chế độ streaming (`setEnableStreaming(true)`) – engine không bao giờ tạo ra toàn bộ ảnh. |
| **Thứ tự khối không khớp** | Các file được sắp xếp theo thứ tự chữ cái thay vì số (ví dụ, `tile_10.tif` trước `tile_2.tif`). | Đặt số có độ dài cố định (`tile_00.tif`, `tile_01.tif`) hoặc sắp xếp bằng chương trình sử dụng `Comparator`. |
| **Ngôn ngữ sai** | OCR mặc định là tiếng Anh; văn bản không phải tiếng Anh sẽ bị rối. | Gọi `ocrEngine.getLanguageSettings().setLanguage("fr")` (hoặc bất kỳ mã ISO nào được hỗ trợ). |
| **Lỗi một khối** | Một khối bị hỏng làm dừng toàn bộ quá trình. | Bắt `IOException` cho mỗi khối, ghi log, và quyết định tiếp tục hay dừng. |
| **Nút cổ chai hiệu năng** | Đọc nhiều file nhỏ gây I/O chiếm ưu thế. | Gộp các khối vào một ZIP và stream từ bộ nhớ, hoặc dùng SSD nhanh. |

---

## Khi nào nên dùng Streaming vs. OCR ảnh đơn

- **Streaming** phù hợp cho:
  - TIFF đa trang hoặc ảnh gigapixel.
  - Các trường hợp bộ nhớ hạn chế (ví dụ, container Docker, thiết bị di động).
  - Các pipeline đã nhận được các đoạn ảnh (ví dụ, luồng camera).

- **OCR ảnh đơn** vẫn ổn cho:
  - Các file PNG/JPEG nhỏ (< 5 MB).
  - Các lần quét một lần, nơi sự đơn giản quan trọng hơn hiệu năng.

---

## Kết luận

Bây giờ bạn đã nắm vững **cách ocr tiff** bằng khả năng streaming của Aspose OCR, và biết cách **trích xuất các khối văn bản** một cách hiệu quả. Giải pháp hoàn chỉnh — khởi tạo engine, bật streaming, thêm từng khối, và cuối cùng thực hiện nhận dạng trên canvas ảo — bao gồm “cái gì”, “tại sao” và “cách làm” cần thiết cho mã sẵn sàng sản xuất.

Bước tiếp theo? Thử thay `"en"` bằng ngôn ngữ khác, hoặc thử nghiệm với các định dạng ảnh khác (`.png`, `.jpg`). Bạn cũng có thể đưa kết quả OCR trực tiếp vào một chỉ mục tìm kiếm hoặc trình tạo PDF. Mô hình vẫn giữ nguyên: stream, stitch, recognize.

Có câu hỏi về việc mở rộng lên hàng trăm khối, hoặc cần trợ giúp về xử lý lỗi? Hãy để lại bình luận bên dưới, và chúc bạn lập trình vui vẻ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}