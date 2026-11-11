---
category: general
date: 2026-06-22
description: 'Cách chỉnh nghiêng ảnh cho OCR: tìm hiểu các bước tiền xử lý ảnh OCR,
  loại bỏ nhiễu muối tiêu và nâng cao độ chính xác.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: vi
og_description: Cách chỉnh nghiêng ảnh cho OCR, loại bỏ nhiễu muối tiêu và áp dụng
  các kỹ thuật tiền xử lý ảnh OCR trong một ví dụ Java hoàn chỉnh.
og_title: Cách chỉnh nghiêng ảnh – Hướng dẫn tiền xử lý ảnh OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: Cách chỉnh nghiêng ảnh – Hướng dẫn tiền xử lý ảnh OCR
url: /vi/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cách Định Hướng Lại Hình Ảnh – Hướng Dẫn Tiền Xử Lý Ảnh OCR

Bạn đã bao giờ tự hỏi **cách định hướng lại hình ảnh** để công cụ OCR của bạn thực sự đọc được văn bản chưa? Bạn không phải là người duy nhất. Một bản scan nghiêng có thể biến một tài liệu hoàn hảo thành một mớ hỗn độn, và hầu hết các nhà phát triển đều gặp phải vấn đề này ít nhất một lần.

Trong hướng dẫn này, chúng ta sẽ đi qua một quy trình **image preprocessing OCR** đầy đủ, không chỉ chỉnh sửa góc quay mà còn **loại bỏ nhiễu muối tiêu** và tăng độ tương phản — về cơ bản là mọi thứ bạn cần để **preprocess images OCR**‑style trước khi đưa vào engine. Khi kết thúc, bạn sẽ có một đoạn mã Java sẵn sàng chạy và một mô hình tư duy rõ ràng về lý do mỗi bước quan trọng.

## Cách Định Hướng Lại Hình Ảnh – Xây Dựng Quy Trình Tiền Xử Lý

Trọng tâm của bất kỳ quy trình làm việc thân thiện với OCR nào là một đối tượng **preprocess options** nối tiếp một loạt các bộ lọc. Hãy nghĩ nó như một băng chuyền: mỗi bộ lọc thực hiện một công việc, sau đó chuyển ảnh sang bộ lọc tiếp theo. Dưới đây là một ví dụ tối thiểu nhưng đầy đủ sử dụng một thư viện OCR giả định có sẵn `DeskewFilter`, `DenoiseFilter`, và `ContrastBoostFilter`.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### Tại sao cách này hoạt động

* **DeskewFilter** phân tích các dòng văn bản chiếm ưu thế trong ảnh, ước tính góc và xoay bitmap trở lại vị trí ngang. Hầu hết các thư viện giới hạn việc chỉnh sửa ở ±15° vì góc lớn hơn thường cho thấy một trang được scan kém cần can thiệp thủ công.
* **DenoiseFilter** nhắm vào mẫu *salt‑and‑pepper* cổ điển — những pixel đen hoặc trắng cô lập giống như nhiễu tĩnh trên TV. Việc loại bỏ chúng ngăn công cụ OCR nhầm lẫn nhiễu thành ký tự.
* **ContrastBoostFilter** kéo dài histogram, làm cho các nét mờ trở nên nổi bật. Hệ số `1.5f` là giá trị mặc định an toàn; bạn có thể tăng lên nếu bản scan của bạn đặc biệt nhạt.

> **Mẹo chuyên nghiệp:** Nếu bạn biết tài liệu của mình không bao giờ nghiêng quá 10°, hãy truyền giới hạn nhỏ hơn đó cho `DeskewFilter` — thuật toán sẽ chạy nhanh hơn và ít khả năng chỉnh sửa quá mức.

## Image Preprocessing OCR: Thêm Bộ Lọc Theo Thứ Tự Đúng

Thứ tự rất quan trọng. Hãy tưởng tượng bạn thực hiện denoise *trước* khi deskew; nhiễu có thể làm lệch việc phát hiện góc, dẫn đến kết quả lệch hướng. Ngược lại, áp dụng tăng độ tương phản *sau* khi deskew sẽ đảm bảo việc xoay không tạo ra nhiễu mới.

Dưới đây là một danh sách kiểm tra nhanh mà bạn có thể sao chép‑dán vào bất kỳ dự án nào:

| Bước | Bộ lọc | Lý do |
|------|--------|--------|
| 1 | `DeskewFilter` | Căn chỉnh đường cơ sở văn bản |
| 2 | `DenoiseFilter` | Loại bỏ nhiễu pixel cô lập |
| 3 | `ContrastBoostFilter` | Tăng khả năng đọc cho OCR |

Nếu bạn cần chèn các bước bổ sung — ví dụ, một bộ lọc **binarization** cho OCR nhị phân — bạn sẽ đặt nó **sau** khi tăng độ tương phản, vì một ảnh sạch, độ tương phản cao sẽ chuyển đổi nhị phân chính xác hơn.

## Loại Bỏ Nhiễu Muối Tiêu với DenoiseFilter

Nhiễu *salt‑and‑pepper* nổi tiếng trong các bản scan chất lượng thấp, đặc biệt là những ảnh chụp bằng camera điện thoại giá rẻ. `DenoiseFilter` trong thư viện của chúng tôi thực hiện một kernel median‑filter, thay thế mỗi pixel bằng giá trị trung vị của các pixel xung quanh. Hiệu quả? Những đốm này biến mất mà không làm mờ các ký tự thực tế.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*Khi nào nên tăng kích thước kernel?* Nếu ảnh nguồn của bạn bị đầy các đốm lớn, một kernel lớn hơn sẽ làm sạch chúng, nhưng hãy cẩn thận: quá lớn có thể bắt đầu xóa các nét mảnh trong phông chữ nhỏ.

## Preprocess Images OCR – Áp Dụng Quy Trình

Khi bạn đã lắp ráp chuỗi bộ lọc, việc gắn nó vào engine chỉ cần một dòng lệnh (`engine.setPreprocessOptions`). Từ thời điểm đó, mọi lời gọi tới `recognizeText` sẽ tự động chạy qua quy trình. Không cần gọi từng bộ lọc thủ công — mã của bạn sẽ gọn gàng, và các thay đổi trong tương lai (thêm bộ lọc mới, điều chỉnh tham số) sẽ được tập trung.

Đây là kết quả của một lần chạy thành công với một bản scan mẫu ban đầu có góc nghiêng 12° và nhiễu pepper đáng chú ý:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

Chú ý cách văn bản trở nên sạch sẽ, được căn chỉnh đúng, và không còn các ký tự lẻ tẻ mà nếu không sẽ xuất hiện như “I n v o i c e” hoặc “$‑‑‑”.

## Trường Hợp Cạnh & Những Cạm Bẫy Thông Thường

| Tình huống | Cần chú ý | Giải pháp đề xuất |
|-----------|-----------|-------------------|
| Xoay > 15° | DeskewFilter có thể bỏ qua | Xoay trước bằng tay hoặc sử dụng bộ lọc có phạm vi cao hơn |
| Độ phân giải cực thấp ( < 100 dpi ) | Tăng độ tương phản không thể khôi phục chi tiết | Làm lại mẫu ảnh trước (ví dụ, `ResampleFilter`) |
| Nhiễu hỗn hợp (Gaussian + salt‑pepper) | Chỉ dùng DenoiseFilter không đủ | Xâu chuỗi `GaussianBlurFilter` trước `DenoiseFilter` |
| Scan màu với văn bản màu | Cần chuyển sang thang xám | Chèn `GrayscaleFilter` trước khi tăng độ tương phản |

Bằng cách dự đoán các kịch bản này, bạn sẽ tiết kiệm hàng giờ gỡ lỗi sau này.

## Ví Dụ Hoàn Chỉnh (Tất Cả Trong Một)

Dưới đây là một lớp Java tự chứa mà bạn có thể đưa vào bất kỳ dự án Maven hoặc Gradle nào có phụ thuộc `com.example.ocr`. Nó minh họa **cách định hướng lại hình ảnh**, **loại bỏ nhiễu muối tiêu**, và **tiền xử lý ảnh OCR**‑style.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**Kết quả mong đợi** (giả sử `scanned-document.png` chứa một hoá đơn rõ ràng):

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

Nếu bạn thay thế ảnh bằng một ảnh đã được căn chỉnh hoàn hảo, bạn sẽ thấy quy trình vẫn chạy — không có gì bị lỗi, và độ chính xác OCR vẫn cao.

## Kết Luận

Bây giờ bạn đã nắm vững **cách định hướng lại hình ảnh** và lý do mỗi bước tiền xử lý — **image preprocessing OCR**, **remove salt pepper**, và **preprocess images OCR** — đóng vai trò quan trọng trong việc cung cấp văn bản sạch, có thể tìm kiếm được. Ví dụ trên là một bản đầy đủ,

## Bạn Nên Học Gì Tiếp Theo?

Các hướng dẫn sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn thành thạo các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách Sử Dụng AspOCR: Bộ Lọc Tiền Xử Lý Ảnh OCR cho .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Tính Góc Nghiêng cho Tiền Xử Lý Ảnh OCR](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [Cách Đặt Giá Trị Ngưỡng trong Nhận Diện Ảnh OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}