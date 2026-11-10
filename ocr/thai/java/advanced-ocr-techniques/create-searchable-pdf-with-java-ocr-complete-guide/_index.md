---
category: general
date: 2026-05-25
description: สร้าง PDF ที่ค้นหาได้ใน Java ด้วย Aspose OCR. เรียนรู้วิธีแปลง PDF เป็น
  PDF ที่ค้นหาได้, โหลด PDF เพื่อทำ OCR, และเร่งความเร็วด้วย GPU.
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: th
og_description: สร้าง PDF ที่ค้นหาได้ใน Java ด้วย Aspose OCR. บทแนะนำนี้แสดงวิธีแปลง
  PDF เป็น PDF ที่ค้นหาได้, โหลด PDF เพื่อทำ OCR, และใช้การเร่งความเร็วด้วย GPU.
og_title: สร้าง PDF ที่ค้นหาได้ด้วย Java OCR – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: สร้าง PDF ที่ค้นหาได้ด้วย Java OCR – คู่มือฉบับสมบูรณ์
url: /th/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้ด้วย Java OCR – คู่มือฉบับสมบูรณ์

เคยต้องการ **สร้าง PDF ที่สามารถค้นหาได้** จากเอกสารสแกนแต่ไม่แน่ใจว่าจะเริ่มอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว นักพัฒนาจำนวนมากเจออุปสรรคเดียวกันเมื่อต้องแปลง PDF ที่เป็นภาพอย่างเดียวให้เป็นเนื้อหาที่ค้นหาได้, โดยเฉพาะเมื่อประสิทธิภาพเป็นสิ่งสำคัญ

ในบทเรียนนี้เราจะพาคุณผ่านโซลูชันแบบทำมือที่ **สร้าง PDF ที่สามารถค้นหาได้** โดยใช้ Aspose OCR สำหรับ Java เราจะยังแสดงวิธี **แปลง PDF เป็น PDF ที่สามารถค้นหาได้**, **โหลด PDF สำหรับ OCR**, และแม้กระทั่ง **OCR PDF ด้วย GPU** เร่งความเร็ว—ทั้งหมดในสคริปต์เดียวที่อ่านง่าย เมื่อเสร็จคุณจะมีโปรแกรมที่รันได้และเข้าใจเหตุผลที่แต่ละขั้นตอนสำคัญ

> **สิ่งที่คุณจะได้เรียนรู้**  
> * โครงการ Java ครบชุดที่อ่าน PDF หลายภาษา  
> * OCR ที่เปิดใช้ GPU ช่วยเร่งการประมวลผลบนฮาร์ดแวร์สมัยใหม่  
> * ผลลัพธ์ PDF ที่สามารถค้นหาได้ซึ่งคุณสามารถใส่ลงในระบบจัดการเอกสารใดก็ได้  

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

* Java 17 (หรือใหม่กว่า) ติดตั้ง – เวอร์ชันเก่าอาจขาด API ที่จำเป็น  
* Maven หรือ Gradle สำหรับจัดการ dependencies – เราจะใช้ Maven ในตัวอย่าง  
* ใบอนุญาต Aspose OCR for Java (รุ่นทดลองฟรีใช้ทดสอบได้)  
* ไฟล์ PDF ที่มีหน้าสแกน (ตัวอย่างใช้ `mixed_lang.pdf`)  

หากมีส่วนใดที่คุณไม่คุ้นเคย, อย่ากังวล – ขั้นตอนต่อไปนี้มีคำสั่งที่ต้องใช้ทั้งหมด

![สร้าง PDF ที่สามารถค้นหาได้ด้วย Aspose OCR Java](https://example.com/images/create-searchable-pdf.png "สร้าง PDF ที่สามารถค้นหาได้ด้วย Aspose OCR Java")

## ขั้นตอนที่ 1: ตั้งค่าโครงการและ **สร้าง PDF ที่สามารถค้นหาได้** – การเริ่มต้นโครงการ

เริ่มต้นโดยสร้างโครงการ Maven เปิดเทอร์มินัลและรัน:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

เข้าสู่โฟลเดอร์:

```bash
cd SearchablePdfDemo
```

เพิ่ม dependency ของ Aspose OCR ไปยัง `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** กระบวนการ **สร้าง PDF ที่สามารถค้นหาได้** พึ่งพาคลาส `OcrEngine` ซึ่งอยู่ในไลบรารี Aspose OCR หากใช้เวอร์ชันไม่ถูกต้องจะเกิดข้อผิดพลาดในการคอมไพล์หรือฟีเจอร์หายไป

ตอนนี้สร้างคลาส Java หลัก `QuickDemo.java` ภายใต้ `src/main/java/com/example/ocr/`

## ขั้นตอนที่ 2: เปิดใช้งานการเร่งความเร็วด้วย GPU – **OCR PDF ด้วย GPU**

การเร่งด้วย GPU สามารถลดเวลาการทำ OCR หลายหน้าลงได้หลายนาที Aspose OCR ให้คุณสลับใช้งานด้วยบรรทัดเดียว:

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

หากเครื่องของคุณมี GPU NVIDIA หรือ AMD ที่รองรับและติดตั้งไดรเวอร์ที่เหมาะสม, เอนจิน OCR จะส่งงานหนักไปยังการ์ดกราฟิก มิฉะนั้นคำสั่งจะกลับไปใช้ CPU อย่างปลอดภัย – ไม่เกิดการครช, เพียงแค่ทำงานช้าลง

> **เคล็ดลับ:** บน Linux คุณอาจต้องตั้งค่า `LD_LIBRARY_PATH` ให้ชี้ไปที่ไลบรารี CUDA ก่อนเปิด JVM

## ขั้นตอนที่ 3: **โหลด PDF สำหรับ OCR** และกำหนดการสนับสนุนภาษา

ตอนนี้เราจะ **โหลด PDF สำหรับ OCR** Aspose OCR ถือหน้าของ PDF เป็นภาพภายใน, ดังนั้นคุณเพียงแค่ชี้เอนจินไปที่ไฟล์:

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

ต่อไปบอกเอนจินว่าคุณคาดหวังภาษาอะไร ในตัวอย่างของเรามุ่งเน้นที่ภาษาไทย, แต่คุณสามารถส่งอาร์เรย์ของภาษาได้หากเอกสารผสมหลายสคริปต์:

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

หากคุณมีพจนานุกรมกำหนดเอง (เช่น คำเฉพาะโดเมน), ให้เชื่อมต่อเข้าไป:

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **ทำไมต้องตั้งค่าภาษา?** ความแม่นยำของ OCR พึ่งพาโมเดลภาษา การให้ `OcrLanguage` ที่ถูกต้องช่วยลดการรับรู้ผิดพลาดอย่างมาก, โดยเฉพาะสำหรับสคริปต์ที่ไม่ใช่ละติน

## ขั้นตอนที่ 4: **แปลง PDF เป็น PDF ที่สามารถค้นหาได้** ด้วยการเรียกครั้งเดียว

Aspose OCR โดดเด่นเพราะสามารถ **แปลง PDF เป็น PDF ที่สามารถค้นหาได้** ด้วยเมธอดเดียว – ไม่ต้องต่อภาพและชั้นข้อความด้วยตนเอง

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

เบื้องหลังเอนจินทำงาน:

1. ทำ OCR บนภาพของแต่ละหน้า  
2. สร้างชั้นข้อความที่มองไม่เห็นซึ่งตรงกับเนื้อหาภาพ  
3. ฝังชั้นนั้นลงใน PDF ใหม่, คงรูปลักษณ์เดิมไว้  

ผลลัพธ์คือไฟล์ที่ดูเหมือนกับไฟล์ต้นฉบับแต่สามารถทำดัชนีโดยโปรแกรมอ่าน PDF ใดก็ได้

## ขั้นตอนที่ 5: ดึงข้อความที่รับรู้และตรวจสอบผลลัพธ์

แม้ว่าเราจะบันทึก PDF ที่สามารถค้นหาได้แล้ว, คุณอาจต้องการข้อความดิบสำหรับบันทึกหรือประมวลผลต่อ:

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

เมื่อรันโปรแกรม, คุณควรเห็นข้อความภาษาไทยที่สกัดออกมาแสดงในคอนโซล, ตามด้วยไฟล์ `mixed_lang_searchable.pdf` ที่สร้างใหม่ในไดเรกทอรีของคุณ

### ผลลัพธ์คอนโซลที่คาดหวัง (ตัดทอน)

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

เปิด PDF ที่สร้างขึ้นใน Adobe Reader หรือโปรแกรมอ่านใดก็ได้, กด **Ctrl + F**, แล้วคุณจะสามารถค้นหาคำที่เห็นในคอนโซลได้ นั่นคือหลักฐานว่าเราสามารถ **สร้าง PDF ที่สามารถค้นหาได้** อย่างสำเร็จ

## ขั้นตอนที่ 6: ปัญหาที่พบบ่อยและ **เคล็ดลับมืออาชีพ** สำหรับ OCR ประสิทธิภาพสูง

| ปัญหา | อาการ | วิธีแก้ |
|-------|----------|-----|
| **GPU ไม่ตรวจพบ** | ไม่ได้เพิ่มความเร็ว, เอนจินกลับไปใช้ CPU | ตรวจสอบว่าติดตั้งไดรเวอร์ CUDA แล้วและ `java.library.path` รวมไลบรารี GPU |
| **ฟอนต์หาย** | ชั้นข้อความแสดงอักขระผิด | ติดตั้งฟอนต์ภาษาที่เหมาะสมบน OS หรือฝังฟอนต์โดยใช้ `engine.getEngineOptions().setEmbedFonts(true)` |
| **PDF ขนาดใหญ่ (> 500 หน้า)** | เกิดข้อผิดพลาด Out‑of‑memory | เพิ่มขนาด heap ของ JVM (`-Xmx4g`) และตั้งค่า `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` เพื่อกระจายงานไปยังหลายคอร์ |
| **พจนานุกรมกำหนดเองไม่ทำงาน** | ตัวแก้ไขการสะกดดูเหมือนไม่ถูกนำไปใช้ | ตรวจสอบว่าเส้นทางเป็นแบบ absolute และไฟล์ใช้การเข้ารหัส UTF-8 |

> **จำไว้:** บรรทัด `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());` มีความสำคัญเมื่อคุณต้องการ **ocr pdf with gpu** *และ* ใช้ประโยชน์จาก CPU หลายคอร์อย่างเต็มที่ มันบอกเอนจินให้สร้าง worker ต่อคอร์, ทำให้ GPU ทำงานตลอดขณะที่ CPU ดูแลการประมวลผลก่อนและหลัง

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรม Java ที่พร้อมรันครบทุกขั้นตอนที่เราอธิบายไว้ แทนที่เส้นทางตัวอย่างด้วยเส้นทางของคุณเอง

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

คอมไพล์และรัน:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

หากทุกอย่างเชื่อมต่อถูกต้อง, คุณจะเห็นข้อความที่สกัดออกมาแสดงและ PDF ที่สามารถค้นหาได้ใหม่อยู่ข้างไฟล์ต้นฉบับ

## สรุป

เราได้สาธิตวิธี **สร้าง PDF ที่สามารถค้นหาได้** ด้วย Java และ Aspose OCR, ครอบคลุมตั้งแต่การตั้งค่าโครงการจนถึงการประมวลผลด้วย GPU โดย **โหลด PDF สำหรับ OCR**, กำหนดการสนับสนุนภาษา, และเรียกเมธอด **แปลง PDF เป็น PDF ที่สามารถค้นหาได้** เพียงบรรทัดเดียว คุณจะได้เอกสารที่ทำดัชนีได้เต็มที่พร้อมใช้ในเครื่องมือค้นหา หรือระบบจัดเก็บภายใน

ต่อไปทำอะไร? ลองเปลี่ยน `OcrLanguage.THAI` เป็น `OcrLanguage.ENGLISH` หรือรวมหลายภาษาเพื่อรองรับ PDF หลายภาษา ทดลองปรับค่า `engine.getEngineOptions().setResolution(300)` เพื่อดูว่า DPI มีผลต่อความแม่นยำอย่างไร, หรือฝังฟอนต์กำหนดเองเพื่อให้แสดงผลดีกับโปรแกรมอ่านเก่า

มีคำถามเกี่ยวกับการปรับประสิทธิภาพ, ใบอนุญาต, หรือการรวมเวิร์กโฟลว์นี้กับบริการ Spring Boot? แสดงความคิดเห็นด้านล่างหรือดูเอกสาร Aspose OCR Java เพื่อศึกษาเชิงลึกเพิ่มเติม ขอให้โค้ดสนุกและแปลงสแกนที่คงที่ให้กลายเป็นสมบัติกับการค้นหา!

## บทเรียนที่เกี่ยวข้อง

- [จดจำข้อความ PDF – การดำเนินการ OCR ด้วย Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/)
- [OCR จดจำเอกสาร PDF ใน Aspose.OCR สำหรับ Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [วิธี OCR PDF ใน .NET ด้วย Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}