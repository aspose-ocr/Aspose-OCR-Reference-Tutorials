---
category: general
date: 2026-06-25
description: ตัวอย่าง Aspose OCR Java ที่แสดงวิธีดึงข้อความจากไฟล์ TIFF, กำหนดค่าการตั้งค่า
  OCR, และเปิดใช้งานการประมวลผล OCR แบบขนานเพื่อให้ได้ผลลัพธ์ที่เร็วขึ้น.
draft: false
keywords:
- aspose ocr java example
- how to extract text
- extract text from tiff
- how to configure ocr
- parallel ocr processing
language: th
og_description: ตัวอย่าง Aspose OCR Java ที่แสดงวิธีการดึงข้อความจากภาพ TIFF, กำหนดค่า
  OCR, และดำเนินการ OCR แบบขนานเพื่อประสิทธิภาพที่ดีที่สุด.
og_title: ตัวอย่าง Aspose OCR Java – การสกัดข้อความอย่างรวดเร็วจากไฟล์ TIFF
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  headline: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  type: TechArticle
- description: Aspose OCR Java example showing how to extract text from TIFF files,
    configure OCR settings, and enable parallel OCR processing for faster results.
  name: Aspose OCR Java Example – Extract Text from TIFF with Parallel Processing
  steps:
  - name: '**Add Aspose OCR to your project**'
    text: '**Add Aspose OCR to your project**'
  - name: '**Compile and execute**'
    text: '**Compile and execute**'
  - name: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
    text: '**Observe the console** – you should see the OCR output sandwiched between
      the `=== OCR Output Start ===` markers.'
  type: HowTo
tags:
- Aspose OCR
- Java
- Text Extraction
title: ตัวอย่าง Aspose OCR Java – ดึงข้อความจากไฟล์ TIFF ด้วยการประมวลผลแบบขนาน
url: /th/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-tiff-with-parallel/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวอย่าง Aspose OCR Java – ดึงข้อความจาก TIFF ด้วยการประมวลผลแบบขนาน

เคยสงสัย **วิธีดึงข้อความ** จากเอกสารสแกนขนาดใหญ่โดยไม่ทำให้แอปของคุณหยุดทำงานหรือไม่? คุณไม่ได้เป็นคนเดียว ใน **ตัวอย่าง Aspose OCR Java** นี้เราจะอธิบายการตั้งค่า OCR engine, เปิดใช้งานการประมวลผลแบบขนาน, และดึงข้อความ Unicode ที่สะอาดจากไฟล์ TIFF ขนาดหลายเมกะไบต์—ทั้งหมดในไม่กี่บรรทัด

คิดว่าเป็นการให้แอป Java ของคุณมีสแกนเนอร์เทอร์โบที่สามารถทำงานผ่านหลายหน้าได้ขณะคุณดื่มกาแฟ เมื่ออ่านจบคุณจะได้โปรแกรมที่รันได้, เข้าใจว่าการตั้งค่าแต่ละอย่างสำคัญอย่างไร, และรู้วิธีปรับแต่งให้เหมาะกับงานของคุณเอง

---

## สิ่งที่คุณต้องมีก่อนเริ่ม

ก่อนที่เราจะลงลึกในโค้ด, ตรวจสอบให้แน่ใจว่าคุณมี:

- **Java 17** (หรือ JDK เวอร์ชันล่าสุด) ที่ติดตั้งและเพิ่มใน `PATH`
- ใบอนุญาต **Aspose.OCR for Java** หรือคีย์ทดลองฟรี สามารถรับได้จากพอร์ทัลของ Aspose
- **ภาพ TIFF ขนาดใหญ่** (`large_scan.tif`) ที่คุณต้องการทดสอบ—ควรเป็นหลายเมกะไบต์เพื่อให้เห็นประสิทธิภาพของการประมวลผลแบบขนาน
- เครื่องมือสร้างโปรเจกต์อย่าง **Maven** หรือ **Gradle** เพื่อดึงไลบรารี Aspose OCR

เท่านี้เอง ไม่ต้องมี OCR engine ขนาดใหญ่หรือ DLL เนทีฟมาจัดการ พร้อมหรือยัง? ไปเริ่มกันเลย

---

## ตัวอย่าง Aspose OCR Java: การอธิบายโค้ดเต็มรูปแบบ

ด้านล่างเป็นโปรแกรม Java ที่สมบูรณ์และทำงานได้เอง คัดลอกวางลงในไฟล์ชื่อ `ParallelOcrDemo.java`, ปรับเส้นทางรูปภาพ, แล้วคุณก็พร้อมรัน

```java
// ParallelOcrDemo.java
// Demonstrates an Aspose OCR Java example with parallel processing.

import com.aspose.ocr.*;
import com.aspose.ocr.config.*;
import com.aspose.ocr.results.*;

public class ParallelOcrDemo {
    public static void main(String[] args) {
        // -------------------------------------------------------------
        // Step 1: Create OCR configuration and enable parallel processing
        // -------------------------------------------------------------
        OcrConfig config = new OcrConfig()
                // ParallelSettings lets us run up to 8 threads simultaneously.
                .setParallelSettings(new ParallelSettings()
                        .setMaxThreads(8)); // Adjust based on CPU cores.

        // -------------------------------------------------------------
        // Step 2: Initialise the Aspose OCR engine with the configuration
        // -------------------------------------------------------------
        AsposeOCR ocrEngine = new AsposeOCR(config);

        // -------------------------------------------------------------
        // Step 3: Recognise text from a large image (extract text from tiff)
        // -------------------------------------------------------------
        // Replace the path with your actual TIFF file location.
        ImageRecognitionResult result = ocrEngine.recognizeImage("YOUR_DIRECTORY/large_scan.tif");

        // -------------------------------------------------------------
        // Step 4: Output the recognised text (how to extract text)
        // -------------------------------------------------------------
        System.out.println("=== OCR Output Start ===");
        System.out.println(result.getText());
        System.out.println("=== OCR Output End ===");
    }
}
```

> **ผลลัพธ์ที่คาดหวัง** (ตัดบางส่วนเพื่อความกระชับ):  
> ```
> === OCR Output Start ===
> Lorem ipsum dolor sit amet, consectetur adipiscing elit...
> === OCR Output End ===
> ```

> **ภาพประกอบ**  
> ![ตัวอย่าง Aspose OCR Java ประมวลผลภาพ](https://example.com/images/aspose-ocr-java-example.png)

> *Alt text:* ตัวอย่าง Aspose OCR Java แสดงการประมวลผลแบบขนานของไฟล์ TIFF

---

## วิธีตั้งค่า OCR สำหรับการประมวลผล OCR แบบขนาน

บรรทัด `new ParallelSettings().setMaxThreads(8)` คือหัวใจของ **การประมวลผล OCR แบบขนาน** ทำไมจึงสำคัญ?

- **การใช้ CPU:** เซิร์ฟเวอร์สมัยใหม่มักมี CPU 8‑core การสร้างเธรดสูงสุดถึงแปดเธรดทำให้ engine สามารถถอดรหัสส่วนภาพหลายส่วนพร้อมกัน, ลดเวลาโดยรวมอย่างมาก
- **ข้อควรพิจารณาเรื่องหน่วยความจำ:** แต่ละเธรดจะมีบัฟเฟอร์ภายในของตนเอง หากเครื่องมี RAM จำกัด ให้ลดจำนวนเธรด (`setMaxThreads(4)`) เพื่อหลีกเลี่ยง `OutOfMemoryError`
- **ความปลอดภัยของเธรด:** Aspose OCR มีความปลอดภัยต่อเธรดโดยอัตโนมัติ, ไม่ต้องเขียนโค้ดซิงโครไนซ์เพิ่มเติม

หากต้องการประมวลผลไฟล์หลายไฟล์, เพียงห่อ `recognizeImage` ไว้ใน `ExecutorService` ของ Java และใช้ instance `AsposeOCR` เดียวกัน—ขอบคุณ thread pool ภายในที่คุณตั้งค่าไว้

---

## วิธีดึงข้อความจากไฟล์ TIFF

TIFF (Tagged Image File Format) เป็นรูปแบบที่นิยมสำหรับเอกสารสแกนเพราะสามารถเก็บหลายหน้าและข้อมูลแบบ lossless อย่างไรก็ตาม ไม่ใช่ทุก OCR library จะรองรับ TIFF หลายหน้าได้อย่างราบรื่น

Aspose OCR จะตรวจจับประเภทภาพโดยอัตโนมัติและเมื่อรับ TIFF หลายหน้า จะประมวลผลแต่ละหน้าแบบต่อเนื่อง *ภายใน* engine แบบขนาน นั่นหมายความว่าคุณจะได้ประโยชน์จาก multi‑threading โดยไม่ต้องเขียนโค้ดลูปเพิ่ม

หากต้องการเพียงหน้าแรก, ส่งอ็อบเจกต์ `PageOptions` เข้าไป:

```java
ImageRecognitionResult result = ocrEngine.recognizeImage(
        "YOUR_DIRECTORY/large_scan.tif",
        new ImageRecognitionOptions().setPageNumber(1));
```

แต่หากต้องการประสบการณ์ **ดึงข้อความจาก tiff** อย่างเต็มที่, ให้ละเว้น options ตามที่แสดงในตัวอย่าง

---

## วิธีดึงข้อความ – ตรวจสอบผลลัพธ์

เมื่อ OCR engine ทำงานเสร็จ, `result.getText()` จะคืนค่า `String` ธรรมดา คุณสามารถ:

- เขียนลงไฟล์ `.txt` ด้วย `Files.writeString(Path.of("output.txt"), result.getText());`
- ส่งต่อไปยัง pipeline NLP ต่อไป
- ค้นหาโดยใช้ Lucene เพื่อดึงเอกสารอย่างรวดเร็ว

อย่าลืมตัด whitespace หากต้องการต่อผลลัพธ์จากหลายหน้า:

```java
String cleaned = result.getText().trim();
```

---

## ข้อผิดพลาดทั่วไปและเคล็ดลับระดับมืออาชีพ

| ข้อผิดพลาด | สาเหตุ | วิธีแก้ |
|------------|--------|----------|
| **การพังจากหน่วยความจำไม่พอ** | จำนวนเธรดมากเกินไปบน VM ที่มี RAM ต่ำ | ลด `setMaxThreads` หรือเพิ่ม heap (`-Xmx2g`). |
| **ผลลัพธ์ว่างเปล่า** | เส้นทางรูปภาพผิดหรือไฟล์ไม่สามารถเข้าถึงได้ | ตรวจสอบเส้นทางแบบเต็มและสิทธิ์การเข้าถึงไฟล์. |
| **อักขระเสีย** | TIFF ต้นฉบับใช้การเข้ารหัสที่ไม่รองรับ | ทำการประมวลผลล่วงหน้าด้วย ImageMagick เพื่อให้เป็น grayscale 8‑bit. |
| **ประสิทธิภาพช้าในเครื่องที่มีคอร์เดียว** | การประมวลผลแบบขนานเพิ่มภาระ | ตั้งค่า `setMaxThreads(1)` สำหรับสภาพแวดล้อมที่มีคอร์เดียว. |

เคล็ดลับสั้น: เรียก `ocrEngine.dispose()` เสมอ (หรือใช้ try‑with‑resources หากห่อไว้) เพื่อปล่อยทรัพยากรเนทีฟเมื่อเสร็จสิ้น นี่เป็นนิสัยเล็ก ๆ ที่ช่วยป้องกัน memory leak ในบริการที่ทำงานต่อเนื่อง

---

## การรันตัวอย่าง

1. **เพิ่ม Aspose OCR ลงในโปรเจกต์**  
   Maven:  
   ```xml
   <dependency>
       <groupId>com.aspose</groupId>
       <artifactId>aspose-ocr</artifactId>
       <version>23.10</version>
   </dependency>
   ```  
   Gradle:  
   ```groovy
   implementation 'com.aspose:aspose-ocr:23.10'
   ```

2. **คอมไพล์และรัน**  
   ```bash
   javac -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo.java
   java -cp ".:path/to/aspose-ocr.jar" ParallelOcrDemo
   ```

3. **ดูผลในคอนโซล** – คุณควรเห็นผล OCR อยู่ระหว่างเครื่องหมาย `=== OCR Output Start ===`

หากผลลัพธ์ดูเป็นอักขระแปลก ๆ ให้ตรวจสอบว่า TIFF ของคุณไม่ได้เป็นรูปแบบบีบอัดที่ไลบรารีเวอร์ชันปัจจุบันไม่รองรับ การอัปเดตเป็นเวอร์ชันล่าสุดของ Aspose OCR มักจะแก้ปัญหาเหล่านี้ได้

---

## ขั้นตอนต่อไป – ขยายตัวอย่าง Aspose OCR Java

เมื่อคุณเข้าใจพื้นฐานแล้ว ลองทำการทดลองต่อไปนี้:

- **ประมวลผลเป็นชุด:** วนลูปผ่านโฟลเดอร์ของ TIFF, เก็บผลแต่ละไฟล์ลงฐานข้อมูล
- **แพ็คเกจภาษา:** โหลดโมเดลภาษาเพิ่มเติม (`ocrEngine.addLanguage(Language.Spanish);`) เพื่อเพิ่มความแม่นยำในเอกสารที่ไม่ใช่ภาษาอังกฤษ
- **การเตรียมภาพล่วงหน้า:** ใช้ `java.awt` หรือ OpenCV เพื่อแก้ไขการเอียง, กำจัดจุดรบกวน, หรือเพิ่มคอนทราสต์ก่อนส่งให้ OCR engine
- **รวมกับ Spring Boot:** เปิด REST endpoint ที่รับอัปโหลดภาพและคืนข้อความที่ดึงได้ทันที

หัวข้อเหล่านี้ล้วนเชื่อมโยงกับ **วิธีตั้งค่า OCR** และ **การประมวลผล OCR แบบขนาน** ของเรา ทำให้คุณได้ pipeline ที่แข็งแรงและพร้อมใช้งานในสภาพแวดล้อมการผลิต

---

## สรุป

ใน **ตัวอย่าง Aspose OCR Java** นี้เราได้ครอบคลุมทุกอย่างที่คุณต้องรู้เพื่อ **ดึงข้อความ** จากไฟล์ TIFF ขนาดใหญ่, ตั้งค่า OCR engine ให้ทำงานได้อย่างมีประสิทธิภาพ, และใช้ **การประมวลผล OCR แบบขนาน** เพื่อให้แอปของคุณตอบสนองได้ดี ด้วยการทำตามโค้ดขั้นตอน‑ขั้นตอน, ปรับจำนวนเธรด, และระวังข้อผิดพลาดทั่วไป คุณจะสามารถฝัง OCR ความเร็วสูงลงในบริการ Java ใด ๆ ได้ทันที

ลองรัน, ปรับตั้งค่า, แล้วให้ OCR engine ทำงานหนักส่วนที่ต้องทำขณะที่คุณมุ่งเน้นสร้างฟีเจอร์ข้อมูลเอกสารที่ยอดเยี่ยมต่อไป ขอให้สนุกกับการเขียนโค้ด!

## สิ่งที่คุณควรเรียนต่อไป

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอน‑ขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่น ๆ ในโปรเจกต์ของคุณ

- [ดึงข้อความจากรูปภาพ – พื้นฐาน OCR ด้วย Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [วิธีจดจำ TIFF ด้วย Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [วิธีใช้ OCR - เทคนิคขั้นสูงด้วย Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}