---
category: general
date: 2026-03-28
description: Tiền xử lý hình ảnh cho OCR và nhận dạng văn bản từ hình ảnh bằng Aspose
  OCR. Tìm hiểu cách trích xuất văn bản từ ảnh, cải thiện độ chính xác của OCR qua
  các bước tiền xử lý.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: vi
og_description: Tiền xử lý hình ảnh cho OCR và trích xuất văn bản từ ảnh bằng Aspose
  OCR Java. Hãy làm theo hướng dẫn này để cải thiện độ chính xác của OCR chỉ trong
  vài bước.
og_title: Tiền xử lý hình ảnh cho OCR – Hướng dẫn Java đầy đủ
tags:
- OCR
- Java
- Image Processing
title: Tiền xử lý hình ảnh cho OCR – Tăng độ chính xác trích xuất văn bản trong Java
url: /vi/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tiền xử lý ảnh cho OCR – Hướng dẫn Java đầy đủ

Bạn đã bao giờ **tiền xử lý ảnh cho OCR** mà vẫn nhận được kết quả rối rắm chưa? Bạn không phải là người duy nhất. Trong nhiều dự án thực tế, một bản scan thô hoặc một bức ảnh chụp bằng điện thoại chứa độ nghiêng, nhiễu hoặc độ tương phản thấp khiến ngay cả những engine nhận dạng thông minh nhất cũng gặp khó khăn. Tin tốt là gì? Một pipeline tiền xử lý ngắn gọn—giảm nghiêng, giảm nhiễu, nhị phân hoá—có thể cải thiện đáng kể **độ chính xác OCR khi tiền xử lý**.

Trong tutorial này, chúng ta sẽ đi qua một ví dụ thực hành cho thấy cách **nhận dạng văn bản từ ảnh** bằng Aspose OCR cho Java. Khi kết thúc, bạn sẽ có thể **trích xuất văn bản từ ảnh** với ít lỗi hơn, và hiểu tại sao mỗi bước tiền xử lý lại quan trọng.

> **Bạn sẽ thu được gì**  
> * Một chương trình Java chạy được đầy đủ, tải một bức ảnh nghiêng, áp dụng ba bộ lọc cổ điển, và in ra văn bản sạch.  
> * Hiểu sâu về “tại sao” của giảm nghiêng, giảm nhiễu và nhị phân hoá.  
> * Các mẹo xử lý các trường hợp đặc biệt—tệp lớn, định dạng ảnh khác nhau, và thứ tự bộ lọc tùy chỉnh.

## Yêu cầu trước

- Java 8 hoặc mới hơn đã được cài đặt (mã cũng biên dịch được với JDK 11).  
- Maven hoặc Gradle để kéo thư viện Aspose OCR.  
- Một ảnh mẫu (ví dụ: `angled-photo.jpg`) hơi xoay và có một chút nhiễu hình ảnh.  
- Kiến thức cơ bản về phương thức `main` của Java—không cần chuyên môn sâu về OCR.

Nếu bạn thiếu bất kỳ mục nào, chỉ cần tải JDK mới nhất từ Oracle hoặc OpenJDK và thêm dependency Maven sau vào file `pom.xml` của bạn:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

Bây giờ, chúng ta cùng khám phá mã nguồn.

## Bước 1 – Tạo thể hiện OCR Engine

Điều đầu tiên bạn cần là một đối tượng `OcrEngine`. Hãy nghĩ nó như bộ não sẽ đọc ảnh đã được xử lý sau này.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Tại sao điều này quan trọng:** Engine chứa các cài đặt nhận dạng, gói ngôn ngữ, và—điều quan trọng nhất đối với chúng ta—các tùy chọn tiền xử lý. Nếu không có nó, bạn sẽ phải tự xâu chuỗi các thư viện xử lý ảnh, điều này làm mất đi mục đích của một pipeline sạch sẽ.

## Bước 2 – Xây dựng Pipeline Tiền xử lý (giảm nghiêng → giảm nhiễu → nhị phân hoá)

Aspose OCR đi kèm với lớp `PreprocessingOptions` tích hợp sẵn, cho phép bạn xếp chồng các bộ lọc theo đúng thứ tự cần thiết. Ở đây chúng ta thêm ba bộ lọc:

1. **DE_SKEW** – làm thẳng văn bản bị xoay.  
2. **DENOISE** – làm mịn các pixel hạt giống có thể bị nhầm thành ký tự.  
3. **BINARIZE** – chuyển ảnh thành đen‑trắng thuần khiết, giúp engine OCR dễ dàng hơn.

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Mẹo chuyên nghiệp:** Thứ tự các bộ lọc rất quan trọng. Nếu bạn nhị phân hoá *trước* khi giảm nhiễu, nhiễu có thể biến thành các đốm đen sắc nét gây nhầm lẫn cho bộ nhận dạng. Giảm nghiêng trước tiên đảm bảo đường cơ sở của văn bản nằm ngang, cải thiện kết quả của cả giảm nhiễu và nhị phân hoá.

## Bước 3 – Đưa ảnh vào Engine

Bây giờ chúng ta chỉ định engine tới tệp ảnh muốn đọc. Đường dẫn có thể là tuyệt đối hoặc tương đối so với thư mục gốc dự án.

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **Nếu ảnh quá lớn thì sao?** Aspose OCR tự động thu nhỏ các ảnh có chiều dài lớn hơn 2000 px, nhưng bạn có thể ghi đè bằng cách gọi `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` nếu lo ngại về bộ nhớ.

## Bước 4 – Xuất Văn bản Đã Nhận dạng

Cuối cùng, chúng ta in chuỗi đã trích xuất ra console. Trong một ứng dụng thực tế, bạn có thể ghi nó vào cơ sở dữ liệu, tệp, hoặc đưa vào pipeline NLP tiếp theo.

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Kết quả dự kiến

Nếu `angled-photo.jpg` chứa câu *“The quick brown fox jumps over the lazy dog.”* bạn sẽ thấy đầu ra tương tự:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Chú ý rằng đầu ra rất sạch—không có ký tự lạ, không có dòng bị cắt. Đó là sức mạnh của **tiền xử lý ảnh cho OCR**.

## Bước 5 – Kiểm tra và Điều chỉnh (Tùy chọn)

Ngay cả với một pipeline vững chắc, bạn vẫn có thể gặp các trường hợp đặc biệt:

| Tình huống | Điều chỉnh đề xuất |
|-----------|--------------------|
| **Độ tương phản rất thấp** (ví dụ: tài liệu scan mờ) | Thêm bộ lọc `ContrastAdjustment` trước khi nhị phân hoá. |
| **Nền màu sắc** (ví dụ: biên lai có dấu màu) | Thêm bộ lọc `BackgroundRemoval` hoặc chuyển sang ảnh xám trước. |
| **PDF đa trang** | Lặp qua mỗi trang ảnh và tái sử dụng cùng một `preprocessingOptions`. |

Bạn có thể thử nghiệm bằng cách gọi `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` hoặc bất kỳ bộ lọc nào khác được liệt kê trong tài liệu API Aspose OCR.

## Ví dụ đầy đủ, có thể chạy

Dưới đây là chương trình hoàn chỉnh, sẵn sàng sao chép‑dán vào file có tên `PreprocessExample.java`. Đảm bảo dependency Maven đã được giải quyết trước khi biên dịch.

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing: de‑skew → denoise → binarize
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE);
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);

        // 3️⃣ Perform OCR on the chosen image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);

        // 4️⃣ Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Biên dịch và chạy:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

Bạn sẽ thấy văn bản sạch được in ra console, xác nhận rằng bạn đã thành công trong việc **tiền xử lý ảnh cho OCR** và **nhận dạng văn bản từ ảnh**.

## Câu hỏi thường gặp

**Q1: Có hoạt động với file PNG hoặc TIFF không?**  
Có—Aspose OCR hỗ trợ JPEG, PNG, BMP, TIFF và một số định dạng khác. Pipeline tiền xử lý giống hệt; thư viện tự động phát hiện định dạng.

**Q2: Nếu tôi cần trích xuất văn bản từ ảnh chụp bằng điện thoại thì sao?**  
Ảnh điện thoại thường gặp vấn đề ánh sáng không đồng đều. Thêm bộ lọc `LIGHTING_CORRECTION` trước khi nhị phân hoá có thể giúp. Thay đổi mã chỉ cần một dòng:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: Tôi có thể thay đổi ngôn ngữ của OCR không?**  
Chắc chắn. Sau khi tạo engine, đặt ngôn ngữ:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: Điều này cải thiện độ chính xác OCR như thế nào?**  
Mỗi bộ lọc giảm một loại nhiễu hình ảnh cụ thể. Giảm nghiêng căn chỉnh các dòng văn bản, giảm nhiễu loại bỏ các đốm ngẫu nhiên, và nhị phân hoá tạo ảnh độ tương phản cao. Khi kết hợp, chúng cung cấp cho thuật toán nhận dạng một tín hiệu sạch hơn, dẫn đến độ chính xác ký tự cao hơn—thường tăng 15‑30 % trên các đầu vào nhiễu.

## Các bước tiếp theo & Chủ đề liên quan

- **Xử lý hàng loạt:** Đặt logic cốt lõi trong một vòng lặp để xử lý toàn bộ thư mục ảnh.  
- **Thứ tự bộ lọc tùy chỉnh:** Thử nghiệm `BINARIZE` trước `DENOISE` cho các tài liệu đã có độ tương phản cao.  
- **Tối ưu hiệu năng:** Dùng `ocrEngine.getRecognitionSettings().setThreadCount(4)` để chạy đa luồng trên máy đa nhân.  
- **Thư viện thay thế:** So sánh Aspose OCR với Tesseract‑Java cho các trường hợp mở nguồn.  
- **Sau xử lý:** Áp dụng kiểm tra chính tả hoặc làm sạch bằng regex lên kết quả thô để có đầu ra sạch hơn nữa.

Bằng cách nắm vững workflow **tiền xử lý ảnh cho OCR**, bạn sẽ thấy việc trích xuất văn bản từ nguồn ảnh trở nên dự đoán được, lặp lại được, thay vì một thí nghiệm may‑rủi.

---

*Bạn đã sẵn sàng nâng cao pipeline OCR của mình? Tải mã nguồn, tùy chỉnh các bộ lọc, và quan sát độ chính xác tăng lên. Nếu gặp khó khăn, hãy để lại bình luận bên dưới—chúc bạn lập trình vui!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}