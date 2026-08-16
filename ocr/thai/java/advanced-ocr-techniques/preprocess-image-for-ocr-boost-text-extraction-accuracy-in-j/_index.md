---
category: general
date: 2026-03-28
description: เตรียมภาพสำหรับ OCR และจดจำข้อความจากภาพด้วย Aspose OCR. เรียนรู้วิธีดึงข้อความจากรูปถ่ายและปรับปรุงความแม่นยำของ
  OCR ด้วยขั้นตอนการเตรียมภาพทีละขั้นตอน.
draft: false
keywords:
- preprocess image for OCR
- recognize text from image
- extract text from photo
- improve OCR accuracy preprocessing
- Aspose OCR Java
- image preprocessing pipeline
language: th
og_description: เตรียมภาพล่วงหน้าสำหรับ OCR และดึงข้อความจากรูปภาพด้วย Aspose OCR
  Java ปฏิบัติตามบทแนะนำนี้เพื่อปรับปรุงความแม่นยำของ OCR ด้วยการเตรียมภาพเพียงไม่กี่ขั้นตอน.
og_title: การเตรียมภาพสำหรับ OCR – คู่มือ Java ฉบับสมบูรณ์
tags:
- OCR
- Java
- Image Processing
title: เตรียมภาพสำหรับ OCR – เพิ่มความแม่นยำในการสกัดข้อความด้วย Java
url: /th/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-text-extraction-accuracy-in-j/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพสำหรับ OCR – คู่มือ Java ฉบับสมบูรณ์

เคยลอง **preprocess image for OCR** แล้วผลลัพธ์ออกมาดูเหมือนอักขระผสมกันหรือไม่? คุณไม่ได้เป็นคนเดียวที่เจอปัญหานี้ ในหลายโครงการจริง ๆ การสแกนดิบหรือภาพถ่ายจากสมาร์ทโฟนมักมีการเอียง, สัญญาณรบกวน, หรือคอนทราสต์ต่ำ ซึ่งทำให้แม้แต่เครื่องมือจดจำที่ฉลาดที่สุดก็สับสน ข่าวดีคือ การใช้ pipeline การเตรียมภาพสั้น ๆ — de‑skew, denoise, binarize — สามารถ **improve OCR accuracy preprocessing** ได้อย่างมหาศาล

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่แสดงให้เห็นอย่างชัดเจนว่า จะ **recognize text from image** อย่างไรโดยใช้ Aspose OCR for Java เมื่อจบคุณจะสามารถ **extract text from photo** ได้ด้วยข้อผิดพลาดที่น้อยลงมาก และคุณจะเข้าใจเหตุผลที่แต่ละขั้นตอนการเตรียมภาพมีความสำคัญ

> **สิ่งที่คุณจะได้เรียนรู้**  
> * โปรแกรม Java ที่สามารถรันได้เต็มรูปแบบ ซึ่งโหลดภาพที่เอียง, ใช้ฟิลเตอร์คลาสสิกสามตัว, และพิมพ์ข้อความที่สะอาดออกมา  
> * ความเข้าใจใน “ทำไม” ของการทำ de‑skew, denoise, และ binarize  
> * เคล็ดลับการจัดการกับกรณีขอบ—ไฟล์ขนาดใหญ่, ฟอร์แมตภาพต่าง ๆ, และการจัดลำดับฟิลเตอร์แบบกำหนดเอง

## Prerequisites

- ติดตั้ง Java 8 หรือใหม่กว่า (โค้ดยังคอมไพล์ได้กับ JDK 11 ด้วย)  
- มี Maven หรือ Gradle เพื่อดึงไลบรารี Aspose OCR  
- มีภาพตัวอย่าง (เช่น `angled-photo.jpg`) ที่มีการเอียงเล็กน้อยและมีสัญญาณรบกวนบางส่วน  
- คุ้นเคยกับเมธอด `main` ของ Java พื้นฐาน — ไม่จำเป็นต้องเป็นผู้เชี่ยวชาญ OCR

หากคุณขาดส่วนใดส่วนหนึ่ง เพียงดาวน์โหลด JDK ล่าสุดจาก Oracle หรือ OpenJDK แล้วเพิ่ม dependency ของ Maven ต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the newest version -->
</dependency>
```

ตอนนี้มาดูโค้ดกันเลย

## Step 1 – Create the OCR Engine Instance

สิ่งแรกที่คุณต้องมีคืออ็อบเจ็กต์ `OcrEngine` คิดว่าเป็นสมองที่จะอ่านภาพที่ผ่านการประมวลผลต่อไป

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **ทำไมสิ่งนี้ถึงสำคัญ:** Engine จะบรรจุการตั้งค่าการจดจำ, แพ็คภาษา, และ—ที่สำคัญที่สุดสำหรับเรา—ตัวเลือกการเตรียมภาพ หากไม่มี Engine คุณจะต้องเชื่อมต่อไลบรารีการประมวลผลภาพด้วยตนเอง ซึ่งทำให้เสียเป้าหมายของ pipeline ที่สะอาด

## Step 2 – Build a Preprocessing Pipeline (de‑skew → denoise → binarize)

Aspose OCR มาพร้อมกับคลาส `PreprocessingOptions` ที่สร้างขึ้นมาให้คุณสามารถเรียงฟิลเตอร์ตามลำดับที่ต้องการ ที่นี่เราจะเพิ่มฟิลเตอร์สามตัว:

1. **DE_SKEW** – ทำให้ข้อความที่เอียงกลับเป็นแนวตรง  
2. **DENOISE** – กำจัดพิกเซลเม็ดฝุ่นที่อาจถูกมองว่าเป็นอักขระ  
3. **BINARIZE** – แปลงภาพเป็นสีขาว‑ดำบริสุทธิ์ ทำให้งานของ OCR ง่ายขึ้น

```java
        // Step 2: Assemble the preprocessing pipeline
        PreprocessingOptions preprocessingOptions = new PreprocessingOptions();
        preprocessingOptions.addFilter(PreprocessFilter.DE_SKEW);   // correct rotation
        preprocessingOptions.addFilter(PreprocessFilter.DENOISE);  // remove grain
        preprocessingOptions.addFilter(PreprocessFilter.BINARIZE); // high‑contrast B&W

        // Attach the pipeline to the OCR engine
        ocrEngine.getRecognitionSettings().setPreprocessingOptions(preprocessingOptions);
```

> **Pro tip:** ลำดับของฟิลเตอร์เป็นสิ่งสำคัญ หากคุณทำ binarize *ก่อน* denoise สัญญาณรบกวนอาจกลายเป็นจุดสีดำขอบแข็งที่ทำให้ recognizer สับสน การทำ de‑skew ก่อนจะทำให้เส้นฐานของข้อความเป็นแนวนอน ซึ่งช่วยให้ผลลัพธ์ของ denoise และ binarize ดียิ่งขึ้น

## Step 3 – Feed the Image to the Engine

ต่อไปเราจะชี้ engine ไปยังไฟล์ที่ต้องการอ่าน เส้นทางไฟล์สามารถเป็นแบบ absolute หรือ relative จากโฟลเดอร์รากของโปรเจกต์ได้

```java
        // Step 3: Run OCR on the target image
        String imagePath = "YOUR_DIRECTORY/angled-photo.jpg";
        OcrResult ocrResult = ocrEngine.recognizeImage(imagePath);
```

> **ถ้าภาพมีขนาดใหญ่กว่าปกติจะทำอย่างไร?** Aspose OCR จะปรับขนาดภาพอัตโนมัติให้ภาพที่ด้านยาวเกิน 2000 px ลดลง แต่คุณสามารถเขียนทับได้ด้วย `ocrEngine.getRecognitionSettings().setMaxImageDimension(1500)` หากเป็นกังวลเรื่องหน่วยความจำ

## Step 4 – Output the Recognized Text

สุดท้ายเราจะพิมพ์สตริงที่สกัดออกมาที่คอนโซล ในแอปพลิเคชันจริงคุณอาจบันทึกลงฐานข้อมูล, ไฟล์, หรือส่งต่อไปยัง pipeline NLP ต่อไป

```java
        // Step 4: Print the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

### Expected Output

หาก `angled-photo.jpg` มีประโยค *“The quick brown fox jumps over the lazy dog.”* คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

สังเกตว่าผลลัพธ์ออกมาสะอาด—ไม่มีสัญลักษณ์แปลกปลอม, ไม่มีบรรทัดขาด นี่คือพลังของ **preprocess image for OCR**

## Step 5 – Verify and Tweak (Optional)

แม้จะมี pipeline ที่แข็งแรงแล้ว คุณอาจเจอกับกรณีขอบต่าง ๆ:

| Situation | Suggested tweak |
|-----------|-----------------|
| **Very low contrast** (เช่น เอกสารสแกนที่ซีด) | ใส่ฟิลเตอร์ `ContrastAdjustment` เพิ่มก่อน binarization |
| **Colorful background** (เช่น ใบเสร็จที่มีตราสี) | เพิ่มฟิลเตอร์ `BackgroundRemoval` หรือแปลงเป็น grayscale ก่อน |
| **Multi‑page PDFs** | วนลูปผ่านแต่ละหน้าภาพและใช้ `preprocessingOptions` เดียวกัน |

คุณสามารถทดลองโดยเรียก `preprocessingOptions.addFilter(PreprocessFilter.CONTRAST)` หรือฟิลเตอร์อื่นใดที่ระบุในเอกสาร Aspose OCR API

## Full, Runnable Example

ด้านล่างเป็นโปรแกรมเต็มรูปแบบ พร้อมคัดลอก‑วางลงในไฟล์ชื่อ `PreprocessExample.java` ตรวจสอบให้แน่ใจว่า dependency ของ Maven ถูกดึงมาเรียบร้อยก่อนคอมไพล์

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

คอมไพล์และรัน:

```bash
mvn compile exec:java -Dexec.mainClass=PreprocessExample
```

คุณควรเห็นข้อความที่สะอาดพิมพ์ออกมาที่คอนโซล ยืนยันว่าคุณได้ทำ **preprocess image for OCR** และ **recognize text from image** สำเร็จแล้ว

## Common Questions & Answers

**Q1: Does this work with PNG or TIFF files?**  
ใช่ — Aspose OCR รองรับ JPEG, PNG, BMP, TIFF และฟอร์แมตอื่น ๆ อีกหลายประเภท Pipeline การเตรียมภาพเดียวกันจะทำงาน; ไลบรารีจะตรวจจับฟอร์แมตโดยอัตโนมัติ

**Q2: What if I need to extract text from a photo taken on a phone?**  
ภาพจากโทรศัพท์มักมีแสงไม่สม่ำเสมอ การเพิ่มฟิลเตอร์ `LIGHTING_CORRECTION` ก่อน binarization จะช่วยได้ การเปลี่ยนแปลงโค้ดเป็นเพียงบรรทัดเดียว:

```java
preprocessingOptions.addFilter(PreprocessFilter.LIGHTING_CORRECTION);
```

**Q3: Can I change the language of the OCR?**  
แน่นอน หลังจากสร้าง engine แล้วให้ตั้งค่าภาษา:

```java
ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.SPANISH);
```

**Q4: How does this improve OCR accuracy preprocessing?**  
แต่ละฟิลเตอร์ลดประเภทของสัญญาณรบกวนที่แตกต่างกัน De‑skew ทำให้บรรทัดข้อความตรง, denoise กำจัดจุดสีรบกวน, และ binarize สร้างภาพคอนทราสต์สูง ทั้งหมดนี้ทำให้อัลกอริธึมจดจำได้รับสัญญาณที่สะอาดขึ้น ส่งผลให้ความแม่นยำระดับอักขระสูงขึ้น — มักเพิ่ม 15‑30 % ในอินพุตที่มีสัญญาณรบกวน

## Next Steps & Related Topics

- **Batch processing:** ห่อหุ้มตรรกะหลักในลูปเพื่อจัดการโฟลเดอร์ภาพทั้งหมด  
- **Custom filter order:** ทดลองใช้ `BINARIZE` ก่อน `DENOISE` สำหรับเอกสารที่คอนทราสต์สูงอยู่แล้ว  
- **Performance tuning:** ใช้ `ocrEngine.getRecognitionSettings().setThreadCount(4)` เพื่อทำงานแบบขนานบนเครื่องหลายคอร์  
- **Alternative libraries:** เปรียบเทียบ Aspose OCR กับ Tesseract‑Java สำหรับกรณีโอเพ่นซอร์ส  
- **Post‑processing:** ใช้การตรวจสอบการสะกดหรือทำความสะอาดด้วย regex กับผลลัพธ์ดิบเพื่อให้ได้ผลลัพธ์ที่ยิ่งสะอาดขึ้น

เมื่อคุณเชี่ยวชาญ workflow **preprocess image for OCR** คุณจะพบว่าการสกัดข้อความจากแหล่งภาพถ่ายกลายเป็นงานที่ทำได้อย่างคาดการณ์ได้และทำซ้ำได้ ไม่ใช่การทดลองแบบสุ่ม

---

*พร้อมเพิ่มประสิทธิภาพให้ pipeline OCR ของคุณหรือยัง? ดึงโค้ด, ปรับฟิลเตอร์, แล้วดูความแม่นยำพุ่งสูงขึ้น หากเจออุปสรรคใด ๆ คอมเมนต์ไว้ด้านล่าง — Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}