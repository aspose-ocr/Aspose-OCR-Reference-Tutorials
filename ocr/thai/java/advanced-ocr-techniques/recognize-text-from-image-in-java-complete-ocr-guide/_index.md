---
category: general
date: 2026-08-12
description: จดจำข้อความจากภาพโดยใช้เครื่องมือ OCR ของ Java เรียนรู้วิธีดึงข้อความจากภาพ
  ปรับปรุงความแม่นยำของ OCR และเตรียมภาพล่วงหน้าสำหรับ OCR บนไฟล์ PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: th
lastmod: 2026-08-12
og_description: รู้จำข้อความจากภาพด้วย Java. บทแนะนำนี้แสดงวิธีการดึงข้อความจากภาพ,
  เพิ่มความแม่นยำของ OCR, และทำ OCR บนไฟล์ PNG โดยใช้การทำงานหลายเธรดและ GPU.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: รู้จำข้อความจากภาพใน Java – คู่มือ OCR ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: แยกข้อความจากภาพใน Java – คู่มือ OCR ฉบับเต็ม
url: /th/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การจดจำข้อความจากรูปภาพใน Java – คู่มือ OCR ฉบับสมบูรณ์

หากคุณต้องการ **จดจำข้อความจากรูปภาพ** ในแอปพลิเคชัน Java คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนอย่างละเอียด เมื่อเสร็จสิ้นคุณจะสามารถดึงข้อความจากไฟล์รูปภาพ, ปรับปรุงความแม่นยำของ OCR, และทำ OCR บนไฟล์ PNG ด้วยการสนับสนุนหลายคอร์และ GPU

นักพัฒนาหลายคนสงสัย **วิธีดึงข้อความจากรูปภาพ** โดยไม่ต้องเขียนเครือข่ายประสาทเทียมของตนเอง วิธีแก้คือการใช้ OCR engine ที่ได้รับการพิสูจน์แล้ว, ตั้งค่าเพื่อความเร็วและความแม่นยำ, และใช้ขั้นตอนการเตรียมข้อมูลล่วงหน้าที่เหมาะสม ส่วนต่อไปนี้จะอธิบายแต่ละข้อกำหนดเพื่อให้คุณคัดลอกโค้ดไปใส่ในโปรเจกต์ได้โดยตรง

## สิ่งที่คุณจะได้เรียนรู้

* ตั้งค่า OCR engine ใน Java
* เปิดใช้งานการทำงานหลายเธรดและการเร่งความเร็วด้วย GPU (ถ้าต้องการ)
* เพิ่มแพ็คภาษาอังกฤษและสเปน
* ใช้ฟิลเตอร์การเตรียมภาพล่วงหน้าเพื่อเพิ่มคุณภาพการจดจำ
* เปิดใช้งานตัวแก้ไขการสะกดในตัวสำหรับผลลัพธ์ที่สะอาดขึ้น
* ทำ OCR บนไฟล์ PNG และพิมพ์ข้อความที่จดจำได้

ไม่ต้องพึ่งบริการภายนอก—ทุกอย่างทำงานบนเครื่องท้องถิ่น ทำให้เหมาะสำหรับแอปพลิเคชันที่ทำงานออฟไลน์หรือมีความต้องการความเป็นส่วนตัวสูง

## ข้อกำหนดเบื้องต้น

* Java 17 หรือใหม่กว่า (โค้ดใช้ไวยากรณ์ `var` สมัยใหม่แต่สามารถย้อนกลับได้)
* ไลบรารี OCR ที่มีคลาส `OcrEngine`, `Language`, และ `EngineOptions` (เช่น **GroupDocs.Parser**, **Aspose.OCR** หรือ SDK ที่เข้ากันได้อื่นใด)
* Maven หรือ Gradle สำหรับการจัดการ dependencies
* ตัวอย่างไฟล์ PNG (`sample-image.png`) ที่วางไว้ใน `YOUR_DIRECTORY`

> **เคล็ดลับมืออาชีพ:** หากคุณวางแผนจะประมวลผลภาพหลายพันรูป ควรจัดสรร RAM เพียงพอสำหรับบัฟเฟอร์ GPU และปิดตัวแก้ไขการสะกดเฉพาะเมื่อคุณต้องการผลลัพธ์ OCR ดิบ

## จดจำข้อความจากรูปภาพด้วย Java OCR engine

ด้านล่างเป็นโปรแกรม Java ที่สมบูรณ์และสามารถรันได้ ซึ่งทำตามแปดขั้นตอนที่แสดงในโค้ดต้นฉบับ รวมถึงการ import, เมธอด `main`, และคอมเมนต์ในบรรทัดที่อธิบายวัตถุประสงค์ของแต่ละบรรทัด

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### คำอธิบายของแต่ละขั้นตอน

| ขั้นตอน | ทำไมถึงสำคัญ | วิธีที่ช่วยคุณ **จดจำข้อความจากรูปภาพ** |
|------|----------------|-----------------------------------------------|
| 1️⃣ สร้าง OCR engine | สร้างอินสแตนซ์ของคอมโพเนนต์หลักที่ขับเคลื่อนการทำงานทั้งหมดต่อมา | เป็นจุดเริ่มต้นสำหรับการทำ OCR ทั้งหมด |
| 2️⃣ เปิดการประมวลผลหลายคอร์ | CPU สมัยใหม่มีหลายคอร์; การใช้ประโยชน์จากคอร์เหล่านี้ช่วยลดเวลาการประมวลผลโดยรวม | เร่งการทำงานแบบแบตช์เมื่อคุณ **ทำ OCR บนไฟล์ PNG** แบบขนาน |
| 3️⃣ เปิดการเร่งความเร็วด้วย GPU (ถ้าต้องการ) | GPU มีความเชี่ยวชาญในการประมวลผลพิกเซลแบบขนาน โดยเฉพาะภาพขนาดใหญ่ | สามารถลดเวลาการจดจำได้ถึง 70 % บนฮาร์ดแวร์ที่รองรับ |
| 4️⃣ เพิ่มแพ็คภาษา | ความแม่นยำของ OCR ขึ้นอยู่กับโมเดลภาษา; การระบุเฉพาะภาษาที่ต้องการช่วยลดผลบวกเท็จ | เพิ่มโอกาสในการระบุอักขระอย่างถูกต้องเมื่อคุณ **วิธีดึงข้อความจากรูปภาพ** ในสถานการณ์หลายภาษา |
| 5️⃣ การเตรียมภาพล่วงหน้า | การหมุน, แก้การเอียง, และลดสัญญาณรบกวนช่วยแก้ปัญหาการสแกนทั่วไป | โดยตรง **วิธีปรับปรุงความแม่นยำของ OCR** ด้วยการให้บิตแมพที่สะอาดยิ่งขึ้นต่อ engine |
| 6️⃣ ตัวแก้ไขการสะกด | ขั้นตอนหลังการประมวลผลที่แก้ไขการสะกดผิดทั่วไปของ OCR | ให้ผลลัพธ์ที่อ่านง่ายขึ้นโดยไม่ต้องทำความสะอาดด้วยมือ |
| 7️⃣ ทำ OCR บน PNG | เมธอด `recognizeImage` อ่านไฟล์, ใช้การเตรียมภาพล่วงหน้า, และรัน pipeline การจดจำ | สาธิต **ทำ OCR บน PNG** พร้อมจัดการลักษณะเฉพาะของฟอร์แมต (เช่น การบีบอัดแบบไม่มีการสูญเสีย) |
| 8️⃣ พิมพ์ผลลัพธ์ | ให้ฟีดแบ็กทันทีเพื่อยืนยันความสำเร็จ | ทำให้คุณยืนยันว่าข้อความถูก **จดจำจากรูปภาพ** อย่างถูกต้อง |

### ผลลัพธ์ที่คาดหวัง

หาก `sample-image.png` มีประโยค “Hello, world! 123” คอนโซลจะแสดงผลคล้ายกับ:

```
=== OCR Result ===
Hello, world! 123
```

ผลลัพธ์ที่ได้อาจแตกต่างกันเล็กน้อยขึ้นอยู่กับคุณภาพของภาพและการตั้งค่าภาษา แต่ตัวแก้ไขการสะกดมักจะแก้ไขการจดจำผิดเล็กน้อยเช่น “Helli” → “Hello”

## วิธีการเตรียมภาพสำหรับ OCR – การเจาะลึก

แม้โค้ดข้างต้นจะใช้การเตรียมภาพล่วงหน้าในตัวของ engine, คุณก็สามารถใช้ฟิลเตอร์กำหนดเองก่อนส่งภาพให้ OCR engine ได้ ด้านล่างเป็นเทคนิคสองวิธีที่พบบ่อย:

### 1. การทำ Binarization ด้วยวิธี Otsu

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

Binarization แปลงภาพเป็นสีขาว‑ดำ ซึ่งมักจะ **วิธีปรับปรุงความแม่นยำของ OCR** สำหรับการสแกนที่คอนทราสต์ต่ำ

### 2. การปรับขนาดเป็น 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

ส่วนใหญ่ OCR engine ต้องการความละเอียดอย่างน้อย 300 dpi เพื่อการจดจำอักขระที่ดีที่สุด การปรับขนาดช่วยป้องกัน engine จากการอ่าน glyph ขนาดเล็กผิดพลาด

> **หมายเหตุ:** หากคุณเปิดใช้งานการเตรียมภาพล่วงหน้ากำหนดเองและตัวเลือกในตัวของ engine พร้อมกัน, engine จะใช้ฟิลเตอร์ของมัน *หลังจาก* ของคุณ เลือกลำดับที่เหมาะสมกับลักษณะของภาพของคุณที่สุด

## วิธีดึงข้อความจากรูปภาพ – การจัดการกรณีขอบ

| สถานการณ์ | การปรับแต่งที่แนะนำ |
|-----------|-------------------|
| **พื้นหลังที่มีสัญญาณรบกวนมาก** | เพิ่มความเข้มของ `setDenoise(true)` หรือใช้ฟิลเตอร์มัธยฐานก่อน OCR. |
| **เอียง > 15°** | ใช้ `setDeskew(true)` *และ* ระบุมุมการหมุนด้วยตนเองผ่าน `imgOpts.setRotateAngle(θ)`. |
| **หลายภาษา (เช่น อังกฤษ + สเปน)** | เพิ่มแพ็คภาษาทั้งสองตามที่แสดงในขั้นตอน 4; engine จะสลับบริบทโดยอัตโนมัติ. |
| **PDF ขนาดใหญ่ที่แปลงเป็น PNG** | ประมวลผลแต่ละหน้าเป็น PNG แยกกันและรวมผลลัพธ์; การทำหลายเธรด (ขั้นตอน 2) จะทำให้เวลารวมต่ำลง. |
| **GPU ไม่พร้อมใช้งาน** | คง `setUseGpu(true)` แต่ห่อไว้ใน try‑catch; engine จะย้อนกลับไปใช้ CPU โดยไม่ทำให้แอปพัง. |

## ทำ OCR บน PNG – ตัวอย่างการประมวลผลแบบแบตช์

เมื่อคุณต้องการ **ทำ OCR บนไฟล์ PNG** ทั่วทั้งไดเรกทอรี, ลูปง่าย ๆ ที่ใช้ engine อินสแตนซ์เดียวกันทำงานได้ดี:

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

เนื่องจาก engine ได้รับการตั้งค่าสำหรับหลายคอร์และ GPU แล้ว, ลูปนี้สามารถประมวลผลหลายสิบภาพพร้อมกันโดยไม่ต้องเขียนโค้ดเพิ่มเติม

## ตัวอย่างการทำงานเต็มรูปแบบ

รวมทุกอย่างเข้าด้วยกัน นี่คือคลาสที่เป็นอิสระที่คุณสามารถคัดลอก‑วางลงใน IDE, เพิ่ม dependency ของ Maven ที่เหมาะสม, แล้วรันได้ทันที:



## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการนำไปใช้แบบต่าง ๆ ในโปรเจกต์ของคุณเอง

- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}