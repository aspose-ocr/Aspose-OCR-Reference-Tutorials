---
category: general
date: 2026-06-06
description: วิธีทำ OCR ใน Java – ดึงข้อความจากภาพอย่างรวดเร็ว, แปลงภาพเป็นข้อความ,
  และอ่านข้อความจากไฟล์ jpg ด้วยตัวอย่างโค้ดง่าย ๆ
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: th
og_description: วิธีทำ OCR ใน Java – เรียนรู้วิธีดึงข้อความจากภาพ, แปลงภาพเป็นข้อความ,
  และอ่านข้อความจากไฟล์ JPG พร้อมตัวอย่างที่พร้อมใช้งาน
og_title: วิธีทำ OCR ใน Java – คู่มือขั้นตอนโดยละเอียด
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: วิธีทำ OCR ใน Java – คู่มือครบวงจรสำหรับการดึงข้อความจากภาพ
url: /th/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน Java – คู่มือเต็มสำหรับการดึงข้อความจากรูปภาพ

เคยสงสัย **how to perform OCR** บนรูปภาพที่คุณถ่ายด้วยโทรศัพท์ของคุณหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างแอปสแกนใบเสร็จหรือแค่ต้องการดึงข้อความจาก PDF ที่สแกน, **how to perform OCR** ใน Java เป็นทักษะที่ให้ผลตอบแทนอย่างรวดเร็ว ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างเชิงปฏิบัติที่ **extracts text from image** ไฟล์, **converts image to text**, และแม้แต่แสดงวิธี **read text from jpg** ด้วยเพียงไม่กี่บรรทัดของโค้ด.

> *Pro tip:* วิธีเดียวกันทำงานได้กับ PNG, BMP หรือรูปแบบใดก็ได้ที่ OCR engine รองรับ—แค่เปลี่ยนชื่อไฟล์.

## วิธีทำ OCR ใน Java – ภาพรวม

Optical Character Recognition (OCR) คือเทคโนโลยีที่เปลี่ยนรูปภาพของตัวอักษรให้เป็นข้อความที่สามารถค้นหาได้จริง ในระบบนิเวศของ Java มีไลบรารีหลายตัว—Tesseract, Asprise, และ SDK เชิงพาณิชย์—ทั้งหมดให้ workflow คล้ายกัน: โหลดรูปภาพ, บอก engine ว่าคาดหวังภาษาอะไร, รันการจดจำ, แล้วดึงผลลัพธ์ออกมา ด้านล่างเราจะใช้คลาส `OcrEngine` แบบทั่วไปเพื่อให้ตัวอย่างชัดเจน, แต่คุณสามารถเปลี่ยนเป็นการทำงานของไลบรารีใดก็ได้ที่ทำตามรูปแบบเดียวกัน.

### สิ่งที่คุณจะได้เรียนรู้

- ติดตั้งไลบรารี OCR (ใช่, **ocr in java** ง่ายกว่าที่คุณคิด).
- สร้างและกำหนดค่าอินสแตนซ์ของ OCR engine.
- โหลดไฟล์ JPG (หรือรูปภาพใดก็ได้) และตั้งค่าภาษา.
- ประมวลผลรูปภาพและ **extract text from image** ไฟล์.
- พิมพ์สตริงที่ได้รับการจดจำออกทางคอนโซล.

เมื่อเสร็จสิ้นคุณจะมีโปรแกรม Java ที่ทำงานอิสระซึ่งสามารถนำไปใส่ในโปรเจกต์ใดก็ได้และรันได้ทันที.

![how to perform OCR example](ocr-example.png "how to perform OCR in Java illustration")

## ขั้นตอนที่ 1 – ติดตั้งและนำเข้าไลบรารี OCR (ocr in java)

ก่อนที่คุณจะเขียนบรรทัด Java ใด ๆ คุณต้องมีไลบรารีที่ทำงานหนักจริง ๆ หากคุณใช้ Maven ให้เพิ่ม dependency ดังนี้ (แทนที่ `com.example.ocr` ด้วย group ID ที่แท้จริงของ SDK ที่คุณเลือก):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

หากคุณชอบ Gradle:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

เมื่อ JAR อยู่ใน classpath แล้ว ให้นำเข้าคลาสที่คุณต้องการใช้:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Why this matters:** การนำเข้าคลาสที่ถูกต้องช่วยป้องกันข้อผิดพลาด “cannot find symbol” และทำให้ IDE ของคุณมีความสุข—ไม่มีอะไรน่าหงุดหงิดกว่าการขาด import เมื่อคุณกำลังพยายาม **convert image to text**.

## ขั้นตอนที่ 2 – สร้างอินสแตนซ์ของ OCR Engine (how to perform OCR)

ตอนนี้ไลบรารีพร้อมแล้ว ให้สตาร์ท engine คิดว่า engine คือสมองที่จะมองพิกเซลและคาดเดาตัวอักษร

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

การสร้าง engine มักจะมีค่าใช้จ่ายต่ำ; SDK ส่วนใหญ่จะจัดสรรบัฟเฟอร์ภายในแบบ lazy, ดังนั้นคุณสามารถใช้อินสแตนซ์เดียวกันซ้ำได้หลายรูปภาพหากต้องประมวลผลเป็นชุด.

## ขั้นตอนที่ 3 – โหลดรูปภาพและตั้งค่าภาษา (extract text from image)

ขั้นตอนต่อไปคือให้ engine มีอะไรให้อ่าน ที่นี่เราจะโหลด JPEG จากดิสก์และบอก OCR engine ว่าข้อความอยู่ในภาษามองโกเลีย (ISO 639‑2 code “mon”). คุณสามารถเปลี่ยนเส้นทางหรือรหัสภาษาให้ตรงกับกรณีการใช้งานของคุณได้

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Side note:** หากคุณไม่ได้ตั้งค่าภาษา, engine จะใช้ค่าเริ่มต้นเป็นภาษาอังกฤษ, ซึ่งอาจทำให้ความแม่นยำลดลงอย่างมากเมื่อข้อความจริงเป็น Cyrillic หรือสคริปต์อื่น ๆ ควรระบุภาษาที่ถูกต้องเสมอเมื่อทำได้.

## ขั้นตอนที่ 4 – ประมวลผลรูปภาพและรับผลลัพธ์ (convert image to text)

เมื่อรูปภาพและภาษาเตรียมพร้อมแล้ว ให้สั่ง engine ทำเวทมนตร์ของมัน การเรียก `process()` จะรันอัลกอริทึม OCR และคืนค่าอ็อบเจ็กต์ `OcrResult` ที่มีสตริงที่จดจำได้และคะแนนความเชื่อมั่น

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

เบื้องหลัง engine อาจทำการพรีโพรเซสซิ่ง—deskewing, binarization, noise reduction—เพื่อให้คุณไม่ต้องเขียนขั้นตอนเหล่านั้นเอง นั่นคือเหตุผลที่ไลบรารี OCR สมัยใหม่ส่วนใหญ่เป็นมิตรต่อการใช้งานสำหรับงาน **convert image to text**.

## ขั้นตอนที่ 5 – แสดงข้อความที่ดึงออกมา (read text from jpg)

สุดท้ายให้ดึง plain‑text จากผลลัพธ์และทำสิ่งที่เป็นประโยชน์กับมัน สำหรับการสาธิตนี้เราจะพิมพ์ลงคอนโซลเท่านั้น, แต่คุณก็สามารถเขียนลงไฟล์, ส่งเข้า index การค้นหา, หรือส่งต่อให้บริการอื่นได้

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

บรรทัดนั้นพิสูจน์ว่าคุณได้ **read text from jpg** (หรือรูปแบบที่สนับสนุนใด ๆ) สำเร็จแล้ว หากผลลัพธ์ดูเป็นอักขระผิดพลาด ให้ตรวจสอบรหัสภาษาและคุณภาพของรูปภาพอีกครั้ง

## ตัวอย่างทำงานเต็ม (รวมทุกขั้นตอน)

ด้านล่างเป็นคลาส Java ที่พร้อมรันครบถ้วนซึ่งเชื่อมทุกส่วนเข้าด้วยกัน คัดลอกไปไฟล์ชื่อ `OcrDemo.java`, ปรับเส้นทางรูปภาพและภาษา, แล้วรัน `javac OcrDemo.java && java OcrDemo`

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `input.jpg` มีประโยคมองโกเลีย “Сайн байна уу?” คอนโซลจะแสดง:

```
=== Recognized Text ===
Сайн байна уу?
```

หากรูปภาพเบลอหรือรหัสภาษาไม่ถูกต้อง คุณจะเห็นอักขระผิดพลาดหรือสตริงว่าง—เป็นข้อผิดพลาดทั่วไปที่เราจะพูดถึงต่อไป

## ปัญหาที่พบบ่อยและวิธีแก้ไข

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| อักขระ Cyrillic ผิดพลาด | รหัสภาษาไม่ถูกต้อง (ค่าเริ่มต้นเป็นภาษาอังกฤษ) | ตั้งค่า `ocrEngine.getSettings().setLanguage("mon")` หรือรหัสที่เหมาะสม |
| ไม่มีผลลัพธ์เลย | เส้นทางไฟล์ไม่ถูกต้องหรือไฟล์ไม่สามารถอ่านได้ | ตรวจสอบเส้นทาง, ยืนยันว่าไฟล์มีอยู่, และให้สิทธิ์การอ่านกับโปรเซส |
| ความแม่นยำต่ำ (<70 %) | รูปภาพมีคอนทราสต์ต่ำหรือหมุน | พรีโพรเซสรูปภาพ: เพิ่มคอนทราสต์, deskew, หรือแปลงเป็น grayscale ก่อนส่งให้ engine |
| `OutOfMemoryError` บน PDF ขนาดใหญ่ | โหลดหลายหน้าความละเอียดสูงพร้อมกัน | ประมวลผลหน้าแต่ละหน้าแยกกัน, หรือย่อขนาดภาพก่อนทำ OCR |

### เคล็ดลับพิเศษ: การประมวลผลเป็นชุด

หากคุณต้องการ **extract text from image** ไฟล์เป็นจำนวนมาก, ให้ห่อโค้ดหลักในลูป:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

สแนปช็อตนี้แสดงให้เห็นว่าการขยายจาก JPG เดียวไปจนถึงโฟลเดอร์สแกนทั้งหมดทำได้ง่ายแค่ไหน

## ไปต่อ – สิ่งที่ควรสำรวจต่อ

- **Language Packs:** SDK OCR ส่วนใหญ่ให้คุณดาวน์โหลดไฟล์ข้อมูลภาษาที่เพิ่มขึ้น การเพิ่มแพ็คใหม่ทำให้คุณ **convert image to text** สำหรับภาษานอกเหนือจากอังกฤษและมองโกเลียได้
- **PDF OCR:** Combine this code with Apache PDFBox to

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑โดย‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [ดึงข้อความจากรูปภาพ – พื้นฐาน OCR ด้วย Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-basics/)
- [แปลงรูปภาพเป็นข้อความใน Java ด้วย Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [วิธี OCR ข้อความรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}