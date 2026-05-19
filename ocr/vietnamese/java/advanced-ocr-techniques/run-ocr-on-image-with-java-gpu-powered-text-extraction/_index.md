---
category: general
date: 2026-03-07
description: Thực hiện OCR trên hình ảnh bằng Java. Tìm hiểu cách nhận dạng văn bản
  từ PNG, trích xuất văn bản từ biên lai và tải hình ảnh để OCR với một ví dụ Java
  OCR hoàn chỉnh.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: vi
og_description: Chạy OCR trên hình ảnh bằng Java. Hướng dẫn này chỉ cách nhận dạng
  văn bản từ PNG, trích xuất văn bản từ biên lai và tải hình ảnh để OCR bằng một ví
  dụ OCR Java đầy đủ.
og_title: Chạy OCR trên hình ảnh bằng Java – Trích xuất văn bản bằng GPU
tags:
- OCR
- Java
- GPU
- Image Processing
title: Chạy OCR trên hình ảnh bằng Java – Trích xuất văn bản sử dụng GPU
url: /vi/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Chạy OCR trên Hình ảnh bằng Java – Trích xuất Văn bản Tăng tốc GPU

Bạn đã bao giờ cần **chạy OCR trên các tệp hình ảnh** nhưng không biết bắt đầu từ đâu trong Java? Bạn không đơn độc—nhiều nhà phát triển gặp cùng một rào cản khi lần đầu tiên cố gắng trích xuất văn bản từ một biên lai quét hoặc ảnh chụp màn hình PNG.  

Trong hướng dẫn này, chúng tôi sẽ dẫn bạn qua một **ví dụ Java OCR hoàn chỉnh** không chỉ **nhận dạng văn bản từ PNG** mà còn cho thấy cách **trích xuất văn bản từ biên lai**, đồng thời tận dụng tăng tốc GPU để đạt tốc độ nhanh hơn. Khi kết thúc, bạn sẽ có một chương trình sẵn sàng chạy, tải hình ảnh để OCR, xử lý và in kết quả văn bản thuần.

## Những gì bạn sẽ học

- Cách **tải hình ảnh cho OCR** bằng một `ImageInputStream` đơn giản.  
- Kích hoạt hỗ trợ GPU để engine chạy nhanh hơn trên phần cứng hiện đại.  
- Các bước chính để **nhận dạng văn bản từ PNG** và lấy các chuỗi hữu ích từ biên lai.  
- Các bẫy thường gặp (ví dụ: ID thiết bị GPU sai) và mẹo thực hành tốt.  
- Một đoạn mã đầy đủ, có thể chạy được mà bạn có thể sao chép‑dán vào IDE.

**Tiền đề**

- Java 17 trở lên (mã sử dụng từ khóa `var` để ngắn gọn, nhưng bạn có thể thay bằng kiểu dữ liệu cụ thể nếu đang dùng Java 8).  
- Thư viện OCR cung cấp các lớp `OcrEngine`, `ImageInputStream`, và `OcrResult` (ví dụ, SDK *FastOCR* giả tưởng; hãy thay bằng thư viện thực tế bạn đang dùng).  
- Một máy có GPU nếu bạn muốn tăng hiệu năng (không bắt buộc nhưng được khuyến nghị).

---

## Bước 1: Chạy OCR trên Hình ảnh – Kích hoạt Tăng tốc GPU

Điều đầu tiên cần làm là tạo engine OCR và chỉ định sử dụng GPU. Bước này rất quan trọng vì nếu không có hỗ trợ GPU, engine sẽ quay lại CPU, khiến quá trình xử lý biên lai độ phân giải cao chậm đáng kể.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Tại sao lại quan trọng:**  
Tăng tốc GPU giảm tải các phép tính ma trận nặng mà các engine OCR thực hiện. Nếu bạn có nhiều GPU, có thể chọn GPU có bộ nhớ lớn nhất bằng cách thay đổi giá trị `setGpuDeviceId`. Quên bật GPU là nguyên nhân phổ biến gây ra các phàn nàn “tại sao OCR của tôi lại chậm?”.

> **Mẹo chuyên nghiệp:** Nếu máy của bạn không có GPU tương thích, lệnh `setUseGpu(true)` sẽ chỉ bị bỏ qua—không gây lỗi, chỉ chậm hơn.

---

## Bước 2: Tải Hình ảnh cho OCR

Khi engine đã sẵn sàng, chúng ta cần cung cấp cho nó một hình ảnh. Ví dụ dưới đây cho thấy cách tải biên lai PNG lưu trên đĩa. Bạn có thể thay đổi đường dẫn thành bất kỳ định dạng hình ảnh nào mà thư viện OCR của bạn hỗ trợ.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Trường hợp biên:**  
Nếu tệp không tồn tại hoặc đường dẫn sai, `ImageInputStream` sẽ ném ra `IOException`. Hãy bao quanh lời gọi bằng khối try‑catch và ghi lại thông báo hữu ích:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Bước 3: Nhận dạng Văn bản từ PNG

Sau khi hình ảnh đã được tải, engine OCR có thể thực hiện “ma thuật”. Bước này thực sự **nhận dạng văn bản từ PNG** (hoặc bất kỳ định dạng hỗ trợ nào) và trả về một đối tượng `OcrResult`.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Điều gì đang diễn ra phía sau?**  
Engine thực hiện tiền xử lý (điều chỉnh góc, nhị phân hoá), chạy mạng nơ‑ron để phát hiện ký tự, rồi ghép chúng thành các dòng văn bản. Vì chúng ta đã bật GPU ở bước trước, các phép tính mạng nơ‑ron này diễn ra trên card đồ họa, giúp rút ngắn vài giây so với chạy trên CPU.

---

## Bước 4: Trích xuất Văn bản từ Biên lai

Sau khi nhận dạng, bạn thường chỉ cần văn bản thô. Lớp `OcrResult` thường cung cấp phương thức `getText()` trả về một `String` duy nhất. Bạn có thể tiếp tục xử lý (ví dụ, dùng regex để lấy tổng tiền, ngày tháng, v.v.).

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Kết quả biên lai mẫu:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Bây giờ bạn có thể đưa chuỗi này vào bộ phân tích riêng của mình để lấy tổng tiền, các mục hàng, hoặc thông tin thuế.

---

## Bước 5: Ví dụ Java OCR Đầy đủ – Sẵn sàng Chạy

Kết hợp tất cả lại, đây là **ví dụ Java OCR hoàn chỉnh** mà bạn có thể đặt vào tệp `Main.java`. Đảm bảo thư viện OCR đã được thêm vào classpath.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Kết quả console dự kiến** (giả sử biên lai mẫu ở trên):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Nếu kết quả trông rối mắt, hãy kiểm tra lại hình ảnh có rõ ràng (DPI cao) và gói ngôn ngữ OCR khớp với ngôn ngữ của biên lai.

---

## Câu hỏi Thường gặp & Những Điều Cần Lưu ý

| Câu hỏi | Trả lời |
|----------|--------|
| *Nếu GPU của tôi không được phát hiện thì sao?* | Engine sẽ tự động chuyển sang CPU. Kiểm tra driver và đảm bảo `setGpuDeviceId` trùng với thiết bị hiện có (`nvidia-smi` trên Linux có thể giúp). |
| *Tôi có thể xử lý các tệp JPEG hoặc TIFF không?* | Có—chỉ cần thay đổi phần mở rộng tệp trong `ImageInputStream`. Thư viện OCR thường tự động nhận dạng định dạng. |
| *Có cách để xử lý hàng loạt nhiều biên lai không?* | Đặt mã nhận dạng trong một vòng lặp và tái sử dụng cùng một thể hiện `OcrEngine`; khởi tạo lại cho mỗi ảnh sẽ lãng phí bộ nhớ GPU. |
| *Làm sao cải thiện độ chính xác trên biên lai có độ tương phản thấp?* | Tiền xử lý hình ảnh (tăng độ tương phản, chuyển sang grayscale) trước khi đưa vào engine OCR. Một số thư viện cung cấp API `preprocess`. |

---

## Kết luận

Bạn đã biết **cách chạy OCR trên hình ảnh** bằng Java, từ việc tải ảnh đến trích xuất văn bản sạch từ biên lai. Hướng dẫn đã bao gồm **nhận dạng văn bản từ PNG**, **trích xuất văn bản từ biên lai**, và trình bày một **ví dụ Java OCR** mà bạn có thể tùy biến cho bất kỳ dự án nào.  

Bước tiếp theo? Hãy thử tắt cờ GPU để so sánh hiệu năng, thử nghiệm với các độ phân giải ảnh khác nhau, hoặc tích hợp bộ phân tích dựa trên regex để tự động lấy tổng tiền. Nếu muốn khám phá sâu hơn, hãy tìm hiểu về **xử lý hậu OCR**, **sửa lỗi bằng mô hình ngôn ngữ**, hoặc **pipeline xử lý batch**.

Chúc lập trình vui vẻ, và hy vọng các biên lai của bạn luôn đọc được!  

![ví dụ chạy OCR trên hình ảnh](/images/run-ocr-on-image.png "ví dụ chạy OCR trên hình ảnh – Java")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}