---
category: general
date: 2026-01-07
description: ทำการประมวลผลล่วงหน้าภาพ OCR เพื่อปรับปรุงความแม่นยำของ OCR และสกัดข้อความจากภาพด้วย
  Aspose OCR – คู่มือแบบขั้นตอนต่อขั้นตอนสำหรับนักพัฒนา
draft: false
keywords:
- preprocess image OCR
- extract text image
- improve OCR accuracy
- how to preprocess OCR
language: th
og_description: ประมวลผลล่วงหน้า OCR ของรูปภาพเพื่อปรับปรุงความแม่นยำของ OCR และดึงข้อความจากรูปภาพโดยใช้
  Aspose OCR. บทเรียน Java ฉบับสมบูรณ์พร้อมโค้ด.
og_title: การเตรียมภาพ OCR ใน Java – เพิ่มความแม่นยำ
tags:
- OCR
- Java
- Image Processing
title: การเตรียมภาพ OCR ใน Java – เพิ่มความแม่นยำและดึงข้อความ
url: /th/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมภาพ OCR ใน Java – คู่มือเต็ม

เคยเจอปัญหา **preprocess image OCR** เพราะสแกนของคุณดูเป็นจุดรบกวนและข้อความเอียงไหม? คุณไม่ได้อยู่คนเดียว นักพัฒนาส่วนใหญ่มักเจออุปสรรคเมื่อภาพดิบมีเสียงรบกวน, เอียง, หรือคอนทราสต์ต่ำ ทำให้เครื่องมือ OCR แสดงผลเป็นอักขระไร้ความหมายแทนประโยคที่คาดหวัง  

ข่าวดีคือขั้นตอนการเตรียมภาพเพียงไม่กี่ขั้นตอนสามารถ **improve OCR accuracy** ได้อย่างมหาศาล เปลี่ยนภาพถ่ายที่สั่นไหวให้กลายเป็นข้อความที่เครื่องอ่านได้อย่างชัดเจน ในบทแนะนำนี้เราจะอธิบาย **how to preprocess OCR** ด้วย Aspose OCR for Java อย่างละเอียด และคุณจะได้เห็นวิธี **extract text image** อย่างเชื่อถือได้

เราจะครอบคลุมทุกอย่างที่คุณต้องการ: ไลบรารีที่จำเป็น, โค้ดทีละขั้นตอน, เหตุผลที่แต่ละตัวเลือกสำคัญ, และเคล็ดลับสำหรับกรณีขอบที่อาจเจอ สุดท้ายคุณจะได้โปรแกรมพร้อมรันที่รับไฟล์ JPEG ที่มีเสียงรบกวน, ทำความสะอาด, และพิมพ์ข้อความที่สกัดออกมาที่คอนโซล

---

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- Java Development Kit (JDK) 8 หรือใหม่กว่า
- Maven หรือ Gradle เพื่อจัดการ dependencies (เราจะให้ตัวอย่าง Maven)
- ใบอนุญาต Aspose OCR for Java (รุ่นทดลองฟรีใช้ทดสอบได้)
- ตัวอย่างภาพ, เช่น `skewed-noisy.jpg`, วางไว้ในโฟลเดอร์ที่รู้จัก

เท่านี้—ไม่ต้องใช้ไลบรารีประมวลผลภาพเพิ่มเติม เพราะ Aspose OCR มาพร้อมความสามารถ **preprocess image OCR** ในตัว

---

## ขั้นตอนที่ 1: ตั้งค่า Aspose OCR ในโปรเจคของคุณ

แรกเริ่มให้เพิ่ม dependency ของ Aspose OCR ลงในไฟล์ `pom.xml` ของคุณ ซึ่งจะดึงเอาเอนจินหลักและตัวช่วยประมวลผลภาพที่เราจะใช้ต่อไป

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- use the latest version available -->
</dependency>
```

หากคุณใช้ Gradle, ตัวเทียบเท่าคือ:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** คอยอัปเดต dependencies อยู่เสมอ; เวอร์ชันใหม่มักมีอัลกอริทึม deskew ที่ฉลาดกว่า ซึ่งช่วย **improve OCR accuracy** เพิ่มเติม

---

## Preprocess Image OCR – ขั้นตอนที่ 2: โหลดภาพ

เมื่อไลบรารีพร้อมแล้ว เราสามารถสร้างอินสแตนซ์ `OcrEngine` และชี้ไปที่ภาพที่ต้องการทำความสะอาดได้

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to preprocess
        // Replace "YOUR_DIRECTORY" with the actual folder path
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));
```

ทำไมต้องสร้าง engine ก่อน? Aspose OCR ผูก pipeline การเตรียมภาพไว้กับ engine โดยตรง ดังนั้นตัวเลือกใด ๆ ที่ตั้งค่าต่อมาจะส่งผลต่อสตรีมภาพเดียวกัน นี้ทำให้การทำงาน **extract text image** เกิดบนเวอร์ชันที่ทำความสะอาดแล้ว ไม่ใช่ไฟล์ดิบ

---

## Improve OCR Accuracy – ขั้นตอนที่ 3: ตั้งค่าตัวเลือกการเตรียมภาพ

ความมหัศจรรย์อยู่ใน `ImageProcessingOptions` แต่ละแฟล็กมุ่งเป้าไปที่ข้อบกพร่องทั่วไปที่ทำให้ OCR ทำงานได้แย่

```java
        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();

        // Straighten rotated text – essential for skewed scans
        processingOptions.setDeskew(true);

        // Remove isolated pixels that look like speckles
        processingOptions.setDespeckle(true);

        // Boost contrast by 30% – helps low‑contrast prints
        processingOptions.setContrastBoost(1.3f);
```

- **Deskew**: ตรวจจับมุมการหมุนและหมุนภาพกลับเป็นแนวนอน หากไม่ทำ OCR อาจอ่านอักขระผิดพลาด
- **Despeckle**: กำจัดสัญญาณรบกวนแบบสุ่มที่อาจถูกตีความเป็นเครื่องหมายวรรคตอนหรืออักษรแปลก
- **Contrast Boost**: เพิ่มความแตกต่างระหว่างพื้นหน้า (ข้อความ) กับพื้นหลัง ซึ่งเป็นปัจจัยสำคัญในการ **how to preprocess OCR** สำหรับการพิมพ์ที่จาง

คุณสามารถเปิด/ปิดแฟล็กเหล่านี้ตามลักษณะของแหล่งข้อมูล ตัวอย่างเช่น เอกสารที่สแกนอย่างสมบูรณ์อาจไม่ต้องการ `setDespeckle(true)` ซึ่งจะประหยัดเวลาเพียงไม่กี่มิลลิวินาที

---

## Extract Text Image – ขั้นตอนที่ 4: รัน OCR บนภาพที่เตรียมแล้ว

เมื่อภาพสะอาดแล้ว เราก็เรียก Aspose OCR ให้ทำการจดจำข้อความ

```java
        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

เมธอด `recognize()` จะใช้ pipeline การเตรียมภาพที่ตั้งค่าไว้ภายใน แล้วทำการแยกส่วนอักขระและจดจำผลลัพธ์เป็นสตริงข้อความธรรมดาที่คุณสามารถส่งต่อไปยังกระบวนการต่อไปได้—เช่น การทำดัชนีค้นหา, ระบบอัตโนมัติการกรอกข้อมูล, หรืออะไรก็ตามที่คุณต้องการ

---

## How to Preprocess OCR – ข้อผิดพลาดทั่วไป & กรณีขอบ

### 1. ขนาดภาพมีผล
ภาพขนาดใหญ่มาก (เช่น > 5 MP) อาจทำให้หน่วยความจำเต็ม หากเจอ `OutOfMemoryError` ให้ปรับขนาดภาพก่อนด้วย `processingOptions.setResizeFactor(0.5f)`

### 2. สี vs. Grayscale
Aspose OCR ทำงานดีที่สุดกับภาพระดับสีเทา หากแหล่งของคุณเป็นสี ให้เปิด `processingOptions.setConvertToGrayscale(true)` ก่อนทำ deskew

### 3. PDF หลายหน้า
เมื่อต้องจัดการกับ PDF ให้แยกแต่ละหน้าเป็นภาพแล้วรัน pipeline เดียวกันในลูป API มี `PdfImageExtractor` ให้ใช้

### 4. การสนับสนุนภาษา
หากข้อความของคุณไม่ใช่ภาษาอังกฤษ ให้ตั้งค่าภาษาอย่างชัดเจน:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

การข้ามขั้นตอนนี้อาจทำให้ **improve OCR accuracy** ลดลง เพราะ engine จะพยายามเดาชุดอักขระเอง

---

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste Ready)

ด้านล่างเป็นโปรแกรมครบชุดพร้อมคอมไพล์และรัน เพียงเปลี่ยนพาธ placeholder ให้เป็นตำแหน่งภาพของคุณ

```java
import com.aspose.ocr.*;

public class PreprocessExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/skewed-noisy.jpg"));

        // Step 3: Configure image preprocessing options
        ImageProcessingOptions processingOptions = ocrEngine.getImageProcessingOptions();
        processingOptions.setDeskew(true);          // straighten rotated text
        processingOptions.setDespeckle(true);      // remove isolated pixels
        processingOptions.setContrastBoost(1.3f);   // boost contrast by 30%
        // Optional: processingOptions.setConvertToGrayscale(true);

        // Step 4: Run OCR on the preprocessed image
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดบางส่วนเพื่อความกระชับ):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
```

หากคุณเห็นอักขระแปลก ๆ ตรวจสอบให้แน่ใจว่าพาธภาพถูกต้องและแฟล็กการเตรียมภาพสอดคล้องกับสภาพของภาพ

---

## สรุปภาพรวม

<img src="preprocess-ocr.png" alt="preprocess image OCR demonstration" style="max-width:100%;">

แผนภาพแสดงกระบวนการ: **Load → Deskew → Despeckle → Contrast Boost → Recognize → Extract Text** ทุกบล็อกสอดคล้องกับโค้ดสแนปด้านบน

---

## สรุป

เราได้พาคุณผ่านวิธีการ **preprocess image OCR** ใน Java ด้วย Aspose OCR ตั้งแต่การตั้งค่าโปรเจคจนถึงการปรับแต่งตัวเลือกที่ **improve OCR accuracy** ด้วยการใช้ deskew, despeckle, และ contrast‑boost ทำให้ JPEG ที่มีเสียงรบกวนและเอียงกลายเป็นข้อความที่สะอาดและค้นหาได้—สิ่งที่คุณต้องการเมื่ออยาก **extract text image** ไปใช้ในแอปพลิเคชันต่อไป

ต่อไปคุณอาจลองใช้ฟีเจอร์การเตรียมภาพอื่น ๆ เช่น `setBinarizationThreshold` สำหรับภาพไบนารี, หรือทำ batch job กับหลายภาพพร้อมกัน คุณอาจผสานผลลัพธ์กับ Apache Tika เพื่อทำดัชนี, หรือป้อนให้โมเดลภาษาวิเคราะห์อารมณ์ ความเป็นไปได้ไม่มีที่สิ้นสุดเมื่อคุณเชี่ยวชาญพื้นฐานของ **how to preprocess OCR**

มีคำถามเกี่ยวกับประเภทไฟล์หรือภาษาที่เฉพาะเจาะจงไหม? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}