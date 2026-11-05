---
category: general
date: 2026-03-18
description: วิธีเปิดใช้งาน OCR อย่างรวดเร็วด้วย Aspose OCR สำหรับ Java เรียนรู้การจดจำข้อความจากภาพ
  ตั้งค่าการทำงานขนานสูงสุด ดึงข้อความจาก PNG และโหลดภาพสำหรับ OCR.
draft: false
keywords:
- how to enable OCR
- recognize text from image
- set max parallelism
- extract text from png
- load image for OCR
language: th
og_description: วิธีเปิดใช้งาน OCR ด้วย Aspose OCR สำหรับ Java คู่มือนี้จะแสดงวิธีการจดจำข้อความจากภาพ
  ตั้งค่าการทำงานขนานสูงสุด ดึงข้อความจากไฟล์ PNG และโหลดภาพสำหรับ OCR.
og_title: วิธีเปิดใช้งาน OCR ใน Java – คู่มือเต็ม
tags:
- Aspose OCR
- Java
- Parallel Processing
title: วิธีเปิดใช้งาน OCR ใน Java ด้วย Aspose – คู่มือขั้นตอนเต็มรูปแบบ
url: /th/java/ocr-operations/how-to-enable-ocr-in-java-with-aspose-complete-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน OCR ใน Java – คู่มือขั้นตอนเต็ม

เคยสงสัยไหมว่า **วิธีเปิดใช้งาน OCR** ในแอป Java ของคุณโดยไม่ต้องใช้เวลาหลายวันค้นหาในเอกสาร API? คุณไม่ได้เป็นคนเดียวที่เจอปัญหา นักพัฒนาส่วนใหญ่มักเจออุปสรรคเมื่อจำเป็นต้อง **จดจำข้อความจากภาพ** — โดยเฉพาะไฟล์ PNG ขนาดใหญ่ — พร้อมกับต้องการรักษาประสิทธิภาพให้เหมาะสม.  

ข่าวดีคืออะไร? ด้วย Aspose OCR คุณสามารถเปิดสวิตช์ โหลดภาพเพื่อทำ OCR และแม้กระทั่งเพิ่มจำนวนคอร์ของ CPU เพื่อเร่งความเร็วได้ ในบทแนะนำนี้เราจะพาคุณผ่านทุกขั้นตอนที่ต้องการ: การติดตั้งไลบรารี การโหลด PNG การตั้งค่าระดับสูงสุดของการทำงานแบบขนาน และสุดท้ายการสกัดข้อความ เมื่อเสร็จคุณจะมีโปรแกรมที่สามารถ **สกัดข้อความจากไฟล์ PNG** ได้อย่างรวดเร็ว.

### สิ่งที่คุณต้องเตรียม

- Java 17 หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับเวอร์ชันเก่าได้ แต่ 17 เป็นจุดที่เหมาะที่สุด)
- Maven หรือ Gradle เพื่อดึง Aspose OCR JAR (เราจะแสดงตัวอย่างด้วย Maven)
- ภาพ PNG ที่มีข้อความที่สามารถค้นหาได้ (ยิ่งใหญ่ยิ่งดีสำหรับการทำงานแบบขนาน)
- ความอยากรู้อยากเห็นเล็กน้อย — ไม่จำเป็นต้องมีประสบการณ์ OCR มาก่อน

หากสิ่งใดดูแปลกใจ อย่าตื่นตระหนก เราจะอธิบายข้อกำหนดเบื้องต้นหลังจากบทนำและให้คำสั่งอย่างรวดเร็วเพื่อเริ่มต้น.

---

## ขั้นตอนที่ 1: ติดตั้ง Aspose OCR สำหรับ Java

ก่อนที่คุณจะ **เปิดใช้งาน OCR** ไลบรารีต้องอยู่ใน classpath ของคุณ วิธีที่ง่ายที่สุดคือเพิ่ม dependency ของ Maven:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **เคล็ดลับ:** หากคุณใช้ Gradle ทางเทียบเท่าคือ  
> `implementation 'com.aspose:aspose-ocr:23.12'`.  

เมื่อ dependency ถูกแก้ไข IDE ของคุณจะดาวน์โหลด JARs โดยอัตโนมัติ ไม่จำเป็นต้องจัดการ JAR ด้วยตนเอง.

## ขั้นตอนที่ 2: โหลดภาพเพื่อทำ OCR

ขั้นตอนแรกที่ใช้งานได้จริงคือ **โหลดภาพเพื่อทำ OCR** Aspose มีเมธอดสแตติก `Image.load` ที่รับพาธไฟล์หรือสตรีม เราจะทำให้เรียบง่ายโดยใช้พาธไฟล์:

```java
import com.aspose.ocr.Image;

// ...

// Replace with the absolute or relative path to your PNG
String imagePath = "src/main/resources/large-document.png";
Image image = Image.load(imagePath);
```

> **ทำไมเรื่องนี้สำคัญ:** การโหลดภาพเพียงครั้งเดียวและใช้ `Image` อินสแตนซ์เดียวกันซ้ำหลีกเลี่ยง I/O เพิ่มเติมเมื่อคุณรันการจดจำหลายครั้งบนไฟล์เดียวกัน (เช่น การตั้งค่าภาษาต่าง ๆ).

หากไม่พบไฟล์ Aspose จะโยน `IOException` ในการใช้งานจริงคุณควรห่อไว้ใน try‑catch และอาจใช้ภาพเริ่มต้นเป็นสำรอง.

## ขั้นตอนที่ 3: สร้าง OCR Engine และเปิดการประมวลผลแบบขนาน

ตอนนี้เรามาถึงหัวใจของเรื่อง — **วิธีเปิดใช้งาน OCR** ด้วยการทำงานแบบขนาน คลาส `OcrEngine` ทำงานหนักส่วนนี้ และ `ParallelSettings` ของมันให้คุณควบคุมการทำงานของเธรด.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;

// ...

OcrEngine ocrEngine = new OcrEngine();

// Turn on parallel processing
ParallelSettings parallelSettings = new ParallelSettings();
parallelSettings.setEnabled(true);

// Set the maximum number of threads to the number of available CPU cores
int cores = Runtime.getRuntime().availableProcessors();
parallelSettings.setMaxDegreeOfParallelism(cores);

// Apply the settings to the engine
ocrEngine.setParallelSettings(parallelSettings);
```

### ทำไมต้องตั้งค่า `MaxDegreeOfParallelism`?

- **ประสิทธิภาพ:** PNG ขนาดใหญ่สามารถมีส่วนข้อความหลายพันส่วน โดยค่าเริ่มต้น Aspose ประมวลผลแบบต่อเนื่อง ซึ่งอาจช้าในเครื่องหลายคอร์
- **การควบคุม:** คุณอาจต้องการจำกัดจำนวนเธรดบนเซิร์ฟเวอร์ที่แชร์เพื่อไม่ให้บริการอื่นขาดแคลน ปรับ `cores` ตามต้องการ

## ขั้นตอนที่ 4: จดจำข้อความจากภาพ

เมื่อเอนจินพร้อม การเรียก OCR จริงเป็นบรรทัดเดียว:

```java
String recognizedText = ocrEngine.recognize(image);
```

เบื้องหลัง Aspose แบ่งภาพเป็นบล็อก แล้วรันแต่ละบล็อกผ่านเครือข่ายประสาทเทียมของมัน แล้วรวมผลลัพธ์เข้าด้วยกัน เนื่องจากเราเปิดการทำงานแบบขนาน บล็อกเหล่านั้นจึงถูกประมวลผลพร้อมกัน.

## ขั้นตอนที่ 5: แสดงผลหรือบันทึกข้อความที่สกัดได้

สุดท้ายให้ตัดสินใจว่าจะทำอะไรกับผลลัพธ์ สำหรับการสาธิตอย่างรวดเร็วเราจะพิมพ์ลงคอนโซล แต่คุณก็สามารถเขียนลงไฟล์ ฐานข้อมูล หรือแม้กระทั่งส่งต่อไปยัง pipeline NLP ต่อไปได้.

```java
System.out.println("=== OCR Result ===");
System.out.println(recognizedText);
```

หากคุณต้องการ **สกัดข้อความจากไฟล์ PNG** จำนวนมาก เพียงใส่ขั้นตอนข้างต้นในลูปที่วนผ่านไดเรกทอรี จำไว้ให้ใช้ `OcrEngine` อินสแตนซ์เดียวกัน—การสร้างเอนจินใหม่สำหรับแต่ละไฟล์จะทำลายประโยชน์ของการทำงานแบบขนาน.

## ตัวอย่างการทำงานเต็มรูปแบบ

เมื่อนำทุกอย่างมารวมกัน นี่คือตัวอย่างคลาส Java ที่สมบูรณ์พร้อมรัน คัดลอกและวางลงใน `src/main/java/com/example/ParallelOcrDemo.java` แล้วรัน `mvn compile exec:java`.

```java
package com.example;

import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.ParallelSettings;
import com.aspose.ocr.Image;

/**
 * Demonstrates how to enable OCR with Aspose, set max parallelism,
 * load an image for OCR, and extract text from a PNG file.
 */
public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable parallel processing to speed up recognition
        ParallelSettings parallelSettings = new ParallelSettings();
        parallelSettings.setEnabled(true);
        // Use all available CPU cores; adjust if you need to limit resources
        parallelSettings.setMaxDegreeOfParallelism(
                Runtime.getRuntime().availableProcessors()
        );
        ocrEngine.setParallelSettings(parallelSettings);

        // Step 3: Load the image that contains the text to be recognized
        // Replace the path with your own PNG file location
        Image image = Image.load("src/main/resources/large-document.png");

        // Step 4: Perform OCR on the loaded image
        String recognizedText = ocrEngine.recognize(image);

        // Step 5: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `large-document.png` มีข้อความ “Hello World” คุณจะเห็นผลลัพธ์ประมาณ:

```
=== OCR Result ===
Hello World
```

สำหรับการสแกนหลายหน้า ผลลัพธ์จะเป็นสตริงเดียวที่มีการแบ่งบรรทัดด้วย (`\n`) เพื่อแยกแต่ละบรรทัดของข้อความ.

## คำถามทั่วไปและกรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ถ้า PNG มีขนาดใหญ่มาก (เช่น 10 000 × 10 000 พิกเซล)?** | Aspose จะทำการแบ่งภาพเป็นแผ่นโดยอัตโนมัติ คุณสามารถควบคุมขนาดแผ่นได้ผ่าน `OcrEngine.setTileSize(int width, int height)` หากต้องการการควบคุมที่ละเอียดขึ้น. |
| **ฉันสามารถจำกัดการใช้หน่วยความจำได้หรือไม่?** | ได้ — ตั้งค่า `ocrEngine.setMemoryLimit(long bytes)` เพื่อหลีกเลี่ยงข้อผิดพลาด OutOfMemory บนเครื่องที่มีสเปคต่ำ. |
| **การทำงานแบบขนานทำงานบน Windows และ Linux ได้เหมือนกันหรือไม่?** | แน่นอน. การนามธรรม `ParallelSettings` ใช้ `ForkJoinPool` ของ Java ซึ่งทำงานข้ามแพลตฟอร์ม. |
| **รองรับภาษาอะไรบ้าง?** | รองรับมากกว่า 100 ภาษาโดยตรง เรียก `ocrEngine.setLanguage("eng")` สำหรับภาษาอังกฤษ, `"spa"` สำหรับภาษาสเปน ฯลฯ. |
| **ฉันต้องการจดจำเฉพาะตัวเลขเท่านั้น** | ใช้ `ocrEngine.setCharacterWhitelist("0123456789")` เพื่อจำกัดชุดอักขระ. |

## เคล็ดลับสำหรับ OCR ที่พร้อมใช้งานใน Production

1. **แคช `OcrEngine`** – การสร้างซ้ำหลายครั้งเพิ่มภาระงาน เก็บเป็น singleton หากคุณประมวลผลภาพหลายรูป
2. **ตรวจสอบอินพุต** – ตรวจสอบขนาดไฟล์และมิติ ก่อนส่งให้เอนจิน; ไฟล์ที่ใหญ่มากอาจทำให้ JVM หยุดทำงานแม้มีการทำงานแบบขนาน
3. **การปรับแต่ง Thread Pool** – หากแอปของคุณแชร์ JVM กับบริการอื่น ให้พิจารณาตั้งค่า `parallelSettings.setMaxDegreeOfParallelism(Runtime.getRuntime().availableProcessors() / 2)` เพื่อเป็นมิตรกับระบบ
4. **การประมวลผลหลัง OCR** – OCR ไม่สมบูรณ์แบบ ใช้ตัวตรวจสอบการสะกดหรือทำความสะอาดด้วย regex เพื่อเพิ่มความแม่นยำ โดยเฉพาะตารางที่สแกน

## สรุป

เราได้อธิบาย **วิธีเปิดใช้งาน OCR** ใน Java ด้วย Aspose, แสดงวิธี **จดจำข้อความจากภาพ**, สอนวิธี **ตั้งค่าการทำงานขนานสูงสุด** เพื่อการประมวลผลที่เร็วขึ้น, อธิบายวิธี **สกัดข้อความจาก PNG**, และแสดงวิธีที่ถูกต้องในการ **โหลดภาพเพื่อทำ OCR** โค้ดตัวอย่างเต็มด้านบนพร้อมรันแล้ว และแนวคิดนี้ใช้ได้กับโปรเจกต์ Java ใด ๆ ที่ต้องการการสกัดข้อความที่เร็วและเชื่อถือได้.

พร้อมก้าวต่อหรือยัง? ลองประมวลผลโฟลเดอร์ PNG ทั้งหมด, ทดลองใช้แพ็คภาษาอื่น ๆ, หรือส่งผลลัพธ์ OCR ไปยังดัชนีการค้นหา ความเป็นไปได้ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญพื้นฐานแล้ว.

มีคำถามหรือเจอปัญหา? แสดงความคิดเห็นได้เลย แล้วเราจะช่วยแก้ไขร่วมกัน ขอให้เขียนโค้ดอย่างสนุกสนาน!

![ภาพแสดงวิธีเปิดใช้งาน OCR](https://example.com/placeholder-image.png "วิธีเปิดใช้งาน OCR ใน Java ด้วย Aspose")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}