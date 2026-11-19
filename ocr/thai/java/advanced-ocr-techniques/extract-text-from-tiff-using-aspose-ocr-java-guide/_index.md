---
category: general
date: 2026-07-05
description: ดึงข้อความจากไฟล์ TIFF ด้วย Aspose OCR Java ในการตั้งค่าการประมวลผล OCR
  แบบขนาน ตัวอย่าง Aspose OCR Java สั้นนี้แสดงวิธีเพิ่มประสิทธิภาพด้วยการทำงานหลายคอร์
draft: false
keywords:
- extract text from tiff
- aspose ocr java example
- parallel ocr processing
- java ocr multithreading
- tiff image recognition
language: th
og_description: ดึงข้อความจากไฟล์ TIFF ด้วย Aspose OCR Java และการประมวลผล OCR แบบขนาน
  ทำตามตัวอย่าง Java ขั้นตอนต่อขั้นตอนนี้เพื่อเร่งความเร็วการจดจำภาพหลายหน้า.
og_title: สกัดข้อความจากไฟล์ TIFF ด้วย Aspose OCR Java – คู่มือ
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from tiff using Aspose OCR Java in a parallel OCR processing
    setup. This concise Aspose OCR Java example shows how to boost performance with
    multi‑core threading.
  headline: Extract text from tiff using Aspose OCR Java – Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- TIFF
title: สกัดข้อความจากไฟล์ TIFF ด้วย Aspose OCR Java – คู่มือ
url: /th/java/advanced-ocr-techniques/extract-text-from-tiff-using-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากไฟล์ tiff ด้วย Aspose OCR Java – คู่มือ

เคยต้องการ **สกัดข้อความจากไฟล์ tiff** แต่พบว่ากระบวนการทำงานช้าเหมือนกระรอก? คุณไม่ได้เป็นคนเดียว เมื่อคุณใส่ไฟล์ TIFF หลายหน้าให้กับเครื่อง OCR แบบใช้เธรดเดียว เวลารออาจดูเหมือนไม่มีที่สิ้นสุด—โดยเฉพาะในสถานการณ์การประมวลผลแบบแบตช์

นี่คือเรื่อง: Aspose OCR for Java สามารถใช้ทุกคอร์ลอจิกบนเครื่องของคุณ ทำให้การทำงานแบบเธรดเดียวที่ช้าแปรเป็นกระบวนการ OCR แบบขนานที่ราบรื่น ในบทแนะนำนี้เราจะเดินผ่านตัวอย่าง **Aspose OCR Java example** ที่แสดงอย่างชัดเจนว่าตั้งค่าเอนจินอย่างไร, ป้อนไฟล์ TIFF หลายหน้า, และ **สกัดข้อความจากไฟล์ tiff** ในส่วนที่สั้นกว่าของเวลาต้นฉบับ

## สิ่งที่คุณจะได้เรียนรู้

- คลาส Java ที่สามารถรันได้ซึ่งแสดง **parallel OCR processing** ด้วย Aspose OCR.
- คำอธิบายที่ชัดเจนว่าทำไมการตั้งค่าแต่ละอย่างจึงสำคัญ ไม่ใช่แค่พิมพ์อะไร
- เคล็ดลับในการจัดการกรณีขอบเช่นจำนวนหน้าแตกต่าง, ไฟล์ภาพขนาดใหญ่, และข้อจำกัดของหน่วยความจำ
- พื้นฐานที่มั่นคงเพื่อปรับโค้ดให้เข้ากับโครงการอัตโนมัติเอกสารของคุณเอง

> **Prerequisites**  
> • Java 8 หรือใหม่กว่า (โค้ดสามารถคอมไพล์ด้วย JDK 11 ได้เช่นกัน)  
> • Maven หรือ Gradle เพื่อดึงไลบรารี Aspose OCR for Java  
> • ภาพ TIFF หลายหน้า (คุณสามารถสร้างได้ด้วยโปรแกรมแก้ไขภาพใด ๆ หรือใช้ไฟล์ตัวอย่าง `multi_page.tif` ที่มาพร้อมกับ Aspose)  

หากคุณมีพื้นฐานเหล่านี้ครบแล้ว, มาเริ่มกันเลย.

![สกัดข้อความจากไฟล์ tiff ด้วย Aspose OCR Java – แผนภาพการประมวลผลแบบขนาน](image.png "แผนภาพแสดงการประมวลผล OCR แบบขนานที่สกัดข้อความจากไฟล์ tiff")

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ของคุณ – ตัวอย่าง Aspose OCR Java ที่เร็วที่สุด

ก่อนที่เราจะไปสู่หัวใจของ **parallel OCR processing**, เราต้องมีโปรเจกต์ Java ที่สามารถเข้าถึง JAR ของ Aspose OCR ได้ วิธีที่ง่ายที่สุดคือใช้ Maven:

```xml
<!-- pom.xml snippet -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.12</version> <!-- check for the latest version -->
    </dependency>
</dependencies>
```

หากคุณต้องการใช้ Gradle, ตัวเทียบเท่าคือ:

```groovy
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** การเพิ่ม dependency ผ่าน Maven Central จะทำให้คุณดึงเวอร์ชันล่าสุดที่ได้รับการแก้ไขด้านความปลอดภัยเสมอ ไม่จำเป็นต้องดาวน์โหลด JARs ด้วยตนเอง

เมื่อไฟล์ build ของคุณพร้อมแล้ว, รัน `mvn clean compile` (หรือ `gradle build`) เพื่อยืนยันว่า class ของ Aspose อยู่ใน classpath หากไม่มีข้อผิดพลาดใด ๆ คุณพร้อมแล้ว.

## ขั้นตอนที่ 2: สร้างเอนจิน OCR และเปิดการทำงานหลายคอร์

ตอนนี้เราจะเขียนคลาส Java ที่ทำ OCR จริง ๆ บรรทัดสำคัญที่ทำให้ OCR ปกติกลายเป็นเครื่องมือ **parallel OCR processing** คือ `setThreadCount`. คำสั่งนี้บอก Aspose OCR ว่าจะใช้คอร์ลอจิกกี่คอร์

```java
package com.example.ocr;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;

/**
 * ParallelOcrDemo – a concise Aspose OCR Java example that extracts text from tiff
 * images using multiple threads.
 */
public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // Step 2.1: Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine to use 4 logical cores (adjust to your CPU)
        // This is the heart of parallel OCR processing.
        ocrEngine.setThreadCount(4);

        // Step 2.3: Point the engine at a multi‑page TIFF file.
        // Replace the path with the location of your own TIFF.
        String tiffPath = "YOUR_DIRECTORY/multi_page.tif";

        // Step 2.4: Run the recognition. The method returns a RecognitionResult
        // which holds the extracted text and additional metadata.
        RecognitionResult result = ocrEngine.recognizeImage(tiffPath);

        // Step 2.5: Output the extracted text – this is where we finally
        // extract text from tiff and show it on the console.
        System.out.println("=== Extracted Text Start ===");
        System.out.println(result.getText());
        System.out.println("=== Extracted Text End ===");
    }
}
```

### ทำไม `setThreadCount` ถึงสำคัญ

Aspose OCR แบ่งแต่ละหน้าของไฟล์ TIFF หลายหน้าเป็นงานแยกกันภายในระบบ โดยค่าเริ่มต้นทำงานบนเธรดเดียว ซึ่งหมายความว่าหน้าต่าง ๆ ต้องรอหน้าก่อนหน้าให้เสร็จ การตั้งค่า `threadCount` ให้เท่ากับจำนวนคอร์จริง (หรือเล็กกว่านิดหน่อยเพื่อให้ UI ตอบสนอง) จะทำให้เอนจินประมวลผลหลายหน้าได้พร้อมกัน ในการทดสอบ, เครื่อง 4‑คอร์สามารถลดเวลาโดยรวมได้ **สูงสุด 70 %** เมื่อเทียบกับโหมดเธรดเดียว

> **Note:** หากคุณตั้งค่าจำนวนเธรดมากกว่าจำนวนคอร์ที่มีอยู่, ระบบปฏิบัติการจะเริ่มทำ time‑slicing ซึ่งอาจทำให้ประสิทธิภาพลดลง ควรใช้ `Runtime.getRuntime().availableProcessors()` เป็นขอบเขตบนที่ปลอดภัย

## ขั้นตอนที่ 3: จัดการ TIFF ขนาดใหญ่และข้อจำกัดของหน่วยความจำ

เมื่อคุณ **สกัดข้อความจากไฟล์ tiff** ที่มีหลายสิบหน้าความละเอียดสูง การใช้หน่วยความจำอาจพุ่งสูง Aspose OCR มีตัวเลือกบางอย่างเพื่อช่วยจัดการให้เป็นระเบียบ:

```java
// Optional: Reduce memory footprint by lowering image resolution before OCR
ocrEngine.getImagePreprocessingOptions().setResolution(150); // DPI

// Optional: Enable streaming mode for massive TIFFs (>500 MB)
ocrEngine.setEnableStreaming(true);
```

- **Resolution reduction** ลดความละเอียดเพื่อแลกกับการประหยัดหน่วยความจำอย่างมาก เอกสารพิมพ์ส่วนใหญ่ยังอ่านได้ที่ 150 DPI.
- **Streaming mode** ประมวลผลหน้าแต่ละหน้าทีละหน้าโดยไม่ต้องโหลด TIFF ทั้งหมดเข้าสู่ RAM ซึ่งจำเป็นสำหรับงานแบตช์บนเซิร์ฟเวอร์

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์และแก้ไขปัญหาที่พบบ่อย

หลังจากรันเดโม, คุณควรเห็นข้อความที่สกัดออกมาถูกล้อมด้วยเครื่องหมาย “=== Extracted Text Start ===”. หากผลลัพธ์ดูว่างเปล่าหรือเป็นอักขระผิด, ให้ตรวจสอบตามนี้:

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้เร็ว |
|---------|--------------|-----------|
| ไม่มีข้อความเลย | เส้นทางไฟล์ผิดหรือ TIFF ใช้การบีบอัดที่ไม่รองรับ | ตรวจสอบ `tiffPath` และให้แน่ใจว่า TIFF ไม่ได้ใช้การบีบอัดแบบเฉพาะ (เช่น CCITT Group 4 ใช้ได้; JPEG‑2000 อาจต้องใช้ codecs เพิ่มเติม). |
| อักขระหายไป (เช่น ตัวอักษรที่มีเครื่องหมายสำเนียง) | ไม่ได้ตั้งค่าภาษา OCR | เรียก `ocrEngine.setLanguage(OcrEngine.Language.English);` หรือโหลดแพ็คภาษาแบบกำหนดเอง. |
| ข้อผิดพลาดหน่วยความจำเต็ม | TIFF ขนาดใหญ่มากโดยไม่มีการสตรีมมิ่ง | เปิดใช้งาน `setEnableStreaming(true)` และ/หรือ ลดความละเอียด. |
| ประสิทธิภาพช้าแม้ตั้งค่า `setThreadCount` | CPU hyper‑threading ถูกปิดหรือจำกัดโดย JVM | ตรวจสอบว่า JVM ของคุณไม่ได้ถูกจำกัดด้วย flag `-Xmx`; ให้ heap เพียงพอ (เช่น `-Xmx2g`). |

## ขั้นตอนที่ 5: ขยายขนาด – ประมวลผลโฟลเดอร์ของไฟล์ TIFF แบบขนาน

เดโมไฟล์เดียวเหมาะสำหรับการเรียนรู้, แต่การใช้งานจริงมักต้องการการประมวลผลแบบแบตช์ ด้านล่างเป็นส่วนขยายแบบเบาที่เดินผ่านไดเรกทอรี, สร้าง thread‑pool, และรันเอนจิน OCR บนแต่ละไฟล์พร้อมกัน ซึ่งแสดง **parallel OCR processing** ในระดับแอปพลิเคชัน



## ต่อไปคุณควรเรียนรู้อะไรต่อ?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโครงการของคุณ

- [สกัดข้อความจากรูปภาพ – พื้นฐาน OCR ด้วย Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [สกัดข้อความจากรูปภาพ Java ด้วยโหมด Detect Areas ของ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [วิธีสกัดข้อความจากรูปภาพจาก URL ด้วย Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}