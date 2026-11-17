---
category: general
date: 2026-07-05
description: บทแนะนำ OCR หลายภาษา สำหรับนักพัฒนา Java เรียนรู้วิธีดึงข้อความ OCR จากภาพไปยังโครงการ
  Java ที่เป็นข้อความด้วยตัวอย่าง OCR หลายภาษา
draft: false
keywords:
- mixed language OCR
- get OCR text
- image to text Java
- java OCR example
- multi language OCR
language: th
og_description: อธิบาย OCR หลายภาษาใน Java รับข้อความ OCR จากภาพโดยใช้ตัวอย่าง OCR
  หลายภาษาที่คุณสามารถคัดลอกและวางได้วันนี้.
og_title: OCR หลายภาษาใน Java – คู่มือการเขียนโปรแกรมเต็มรูปแบบ
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  headline: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Mixed language OCR tutorial for Java developers. Learn how to get OCR
    text from images to text Java projects with a multi language OCR example.
  name: Mixed Language OCR in Java – Complete Step‑by‑Step Guide
  steps:
  - name: 1. Create a Maven Project
    text: 'Open a terminal and run:'
  - name: 2. Add the Aspose.OCR Dependency
    text: 'Edit the generated `pom.xml` and insert the following inside the `<dependencies>`
      block:'
  - name: How It Works
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **1** | `OcrEngine` object is created. | The engine encapsulates all OCR functionality;
      without it you can’t call any methods. | | **2** | `setRecognitionLanguage`
      receives `ENGLISH` and `MALAYALAM`. | Supplying both'
  - name: Low‑Quality Images
    text: 'If the image is blurry or has poor contrast, OCR accuracy drops dramatically.
      Consider these remedies:'
  - name: Unsupported Languages
    text: Aspose currently supports over 70 scripts, but Malayalam may require a language
      pack. If `RecognitionLanguage.MALAYALAM` throws an exception, download the additional
      language data from Aspose’s portal and place it in `resources/ocr-data`.
  - name: Large PDFs
    text: When processing multi‑page PDFs, feed each page as a separate image or use
      `OcrEngine.recognizePdf`. The same `setRecognitionLanguage` call applies to
      every page, giving you a seamless **multi language OCR** experience across a
      whole document.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: OCR หลายภาษาใน Java – คู่มือแบบครบถ้วนขั้นตอนต่อขั้นตอน
url: /th/java/advanced-ocr-techniques/mixed-language-ocr-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR หลายภาษาใน Java – คู่มือขั้นตอนเต็ม

เคยต้องการ **mixed language OCR** แต่ไม่แน่ใจว่าจะทำใน Java อย่างไรไหม? คุณไม่ได้เป็นคนเดียว ไม่ว่าจะเป็นการแปลงเอกสารเก่าที่สลับระหว่าง English และ Malayalam, หรือการสร้างแอปสแกนเนอร์ที่รองรับหลายสคริปต์ ความท้าทายนี้เป็นเรื่องจริง ในบทแนะนำนี้เราจะสาธิตวิธี **get OCR text** จาก bitmap ที่มีทั้งสองภาษาโดยใช้กระบวนการ **image to text Java** ที่กระชับ

เราจะเดินผ่าน **java OCR example** ที่พร้อมรัน, อธิบายว่าทำไมแต่ละบรรทัดถึงสำคัญ, และครอบคลุมข้อแปลกของ **multi language OCR** เพื่อให้คุณหลีกเลี่ยงข้อผิดพลาดทั่วไป เมื่อเสร็จคุณจะมีโปรแกรมทำงานที่พิมพ์ข้อความที่สกัดออกมาที่คอนโซล – ไม่มีไลบรารีลึกลับที่ไม่ได้อธิบาย

## สิ่งที่คุณต้องการ

* **Java Development Kit (JDK) 17** หรือใหม่กว่า – โค้ดใช้ระบบโมดูลสมัยใหม่แต่ทำงานได้บน JDK 11+ ด้วย  
* **Maven** (หรือ Gradle) – เพื่อดึงไลบรารี OCR โดยอัตโนมัติ  
* เครื่องมือ OCR ที่รองรับหลายภาษา – สำหรับคู่มือนี้เราจะใช้ **Aspose.OCR for Java** ซึ่งให้การสนับสนุน English และ Malayalam พร้อมใช้งาน (หากคุณชอบ Tesseract ขั้นตอนก็คล้ายกัน; เพียงเปลี่ยนคำสั่ง import)  
* รูปตัวอย่างชื่อ `mixed_english_malayalam.png` ที่วางในโฟลเดอร์ชื่อ `resources` ภายในโปรเจกต์ของคุณ  
* ความอยากรู้อยากเห็นเล็กน้อย – ส่วนที่เหลือจะอธิบายต่อด้านล่าง  

> **เคล็ดลับ:** หากคุณใช้ Windows ให้รัน `mvn -v` จาก Command Prompt เพื่อตรวจสอบว่า Maven อยู่ใน PATH ของคุณ  

## การตั้งค่าโปรเจกต์

### 1. สร้าง Maven Project

Open a terminal and run:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=mixed-ocr-demo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

### 2. เพิ่ม Aspose.OCR Dependency

Edit the generated `pom.xml` and insert the following inside the `<dependencies>` block:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- latest as of July 2026 -->
</dependency>
```

รัน `mvn clean install` เพื่อดาวน์โหลด JARs. Maven จะจัดการทุกอย่าง ดังนั้นคุณไม่จำเป็นต้องค้นหา DLLs เนทีฟ  

## การเขียนโค้ด Mixed Language OCR

สร้างคลาสใหม่ `MixedLanguageOcrDemo.java` ภายใต้ `src/main/java/com/example/ocr/` แล้ววางโค้ดเต็มด้านล่าง ทุกบรรทัดมีคอมเมนต์เพื่อให้คุณเห็น **ทำไม** เราถึงทำเช่นนั้น

```java
package com.example.ocr;

import com.aspose.ocr.*;
import com.aspose.ocr.recognition.*;

public class MixedLanguageOcrDemo {

    public static void main(String[] args) {
        // Step 1: Initialise the OCR engine – this is the entry point for all operations.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Tell the engine which languages to look for.
        // We pass both English and Malayalam; the engine will automatically switch
        // between scripts as it encounters them.
        ocrEngine.setRecognitionLanguage(
                RecognitionLanguage.ENGLISH,
                RecognitionLanguage.MALAYALAM);

        // Step 3: Load the image that contains mixed text.
        // Using a relative path keeps the example portable across machines.
        String imagePath = "resources/mixed_english_malayalam.png";

        // Optional: improve accuracy on low‑resolution scans.
        // Uncomment the next line if your image is under 300 DPI.
        // ocrEngine.setResolution(300);

        // Step 4: Perform the actual OCR operation.
        RecognitionResult result = ocrEngine.recognizeImage(imagePath);

        // Step 5: Extract the plain text – this is the "get OCR text" part.
        String extractedText = result.getText();

        // Step 6: Output the result to the console.
        System.out.println("=== Extracted Text ===");
        System.out.println(extractedText);
    }
}
```

### วิธีการทำงาน

| Step | What Happens | Why It Matters |
|------|--------------|----------------|
| **1** | `OcrEngine` ถูกสร้างขึ้น | เอนจินนี้บรรจุฟังก์ชัน OCR ทั้งหมด; หากไม่มีคุณไม่สามารถเรียกเมธอดใดได้ |
| **2** | `setRecognitionLanguage` รับค่า `ENGLISH` และ `MALAYALAM` | การระบุทั้งสองภาษาช่วยให้ **multi language OCR** ทำงาน; เอนจินจะตรวจจับการเปลี่ยนสคริปต์แบบเรียลไทม์ |
| **3** | กำหนดเส้นทางของรูปภาพ | การใช้เส้นทางแบบ relative หลีกเลี่ยงการ hard‑code ที่ตั้งแบบ absolute ทำให้ **java OCR example** ใช้ซ้ำได้ |
| **4** | `recognizeImage` ประมวลผล bitmap | นี่คือจุดที่ทำงานหนัก – เอนจินวิเคราะห์พิกเซล, รัน neural nets, และคืนค่า `RecognitionResult` |
| **5** | `getText()` ดึงสตริงธรรมดา | นี่คือเมธอดที่คุณต้องการเพื่อ **get OCR text** สำหรับการประมวลผลต่อ (เช่น บันทึกลง DB) |
| **6** | `System.out.println` พิมพ์สตริงออกมา | ฟีดแบ็กแบบทันทีช่วยให้คุณตรวจสอบว่า pipeline **image to text Java** ทำงานได้ |

> **หมายเหตุ:** หากคุณพบ `java.lang.UnsatisfiedLinkError` ให้ตรวจสอบว่าโฟลเดอร์ไลบรารีเนทีฟอยู่ใน `java.library.path` ของคุณ Aspose มีไบนารีที่จำเป็นสำหรับ Windows, macOS, และ Linux  

## การรัน Demo

Compile and execute with Maven:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.MixedLanguageOcrDemo"
```

You should see output similar to:

```
=== Extracted Text ===
Welcome to the conference.
സ്വാഗതം
```

บรรทัดแรกเป็น English, บรรทัดที่สองเป็น Malayalam – เป็นหลักฐานว่า **mixed language OCR** ของเราประสบความสำเร็จ  

## การจัดการกรณีขอบที่พบบ่อย

### รูปภาพคุณภาพต่ำ

หากรูปภาพเบลอหรือคอนทราสต์ต่ำ ความแม่นยำของ OCR จะลดลงอย่างมาก พิจารณาวิธีแก้ต่อไปนี้:

* **Pre‑process** รูปภาพด้วยไลบรารีเช่น OpenCV – แปลงเป็น grayscale, ใช้ adaptive thresholding, และขยายขนาดอย่างน้อย 300 DPI.  
* เปิดใช้งาน `ocrEngine.setAutoSkewCorrection(true)` เพื่อให้เอนจินแก้ไขการเอียงของข้อความ  
* เพิ่มค่า `ocrEngine.setConfidenceThreshold(0.6f)` หากต้องการกรองด้วยความเชื่อมั่นที่เข้มงวดกว่า  

### ภาษาที่ไม่รองรับ

Aspose ปัจจุบันรองรับสคริปต์กว่า 70 ตัว, แต่ Malayalam อาจต้องการ language pack หาก `RecognitionLanguage.MALAYALAM` ทำให้เกิด exception ให้ดาวน์โหลดข้อมูลภาษาเพิ่มเติมจากพอร์ทัลของ Aspose แล้ววางไว้ใน `resources/ocr-data`  

### PDF ขนาดใหญ่

เมื่อประมวลผล PDF หลายหน้า ให้ป้อนแต่ละหน้าเป็นรูปภาพแยกหรือใช้ `OcrEngine.recognizePdf`. การเรียก `setRecognitionLanguage` เดียวกันจะใช้กับทุกหน้า ทำให้คุณได้ประสบการณ์ **multi language OCR** อย่างต่อเนื่องทั่วทั้งเอกสาร  

## การขยายตัวอย่าง: จาก Console ไปยัง Web Service

หากคุณต้องการเปิดให้ฟังก์ชันนี้ผ่าน REST endpoint ให้เพิ่ม Spring Boot:

```java
@RestController
@RequestMapping("/api/ocr")
public class OcrController {

    @PostMapping(value = "/extract", consumes = MediaType.MULTIPART_FORM_DATA_VALUE)
    public String extractText(@RequestParam("file") MultipartFile file) throws IOException {
        OcrEngine engine = new OcrEngine();
        engine.setRecognitionLanguage(RecognitionLanguage.ENGLISH, RecognitionLanguage.MALAYALM);
        // Save multipart file to a temporary location
        Path temp = Files.createTempFile("upload-", ".png");
        Files.write(temp, file.getBytes());
        RecognitionResult res = engine.recognizeImage(temp.toString());
        return res.getText();
    }
}
```

ตอนนี้ไคลเอนต์ใดก็สามารถ `POST` รูปภาพและรับผลลัพธ์ **get OCR text** เป็น JSON ธรรมดา การขยายเล็ก ๆ นี้แสดงให้เห็นว่า **java OCR example** เดียวกันสามารถขยายจากเดโมไฟล์เดียวไปเป็นบริการพร้อมใช้งานใน production  

## ภาพรวมโครงสร้างต้นไม้ของซอร์สเต็ม

```
mixed-ocr-demo/
├─ pom.xml
└─ src/
   └─ main/
      ├─ java/
      │  └─ com/example/ocr/
      │     └─ MixedLanguageOcrDemo.java
      └─ resources/
         └─ mixed_english_malayalam.png
```

การมีโครงสร้างโปรเจกต์ทั้งหมดในบทความทำให้ผู้อ่านสามารถคัดลอกโครงสร้างไปยัง IDE ของตนและรันได้ทันที  

![ผลลัพธ์ตัวอย่าง OCR หลายภาษา](https://example.com/assets/mixed-ocr-output.png "ผลลัพธ์ตัวอย่าง OCR หลายภาษา")

*ข้อความแทนภาพ:* ผลลัพธ์ตัวอย่าง OCR หลายภาษา – แสดงข้อความ English และ Malayalam ที่สกัดจากรูปเดียวกัน  

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุม pipeline **mixed language OCR** ใน Java ตั้งแต่ต้นจนจบ:

* ตั้งค่า Maven project และเพิ่ม Aspose OCR dependency.  
* ตั้งค่าเอนจินสำหรับ English + Malayalam, ทำการจดจำ, และ **got OCR text**.  
* พูดถึงคุณภาพของรูปภาพ, language packs, และวิธีเปลี่ยน console app ให้เป็น web service.  

หากคุณพร้อมที่จะก้าวต่อไป ลองไอเดียเหล่านี้:

* แทนที่ Aspose ด้วย **Tesseract** เพื่อดูว่าเอนจินโอเพนซอร์สจัดการ **multi language OCR** อย่างไร.  
* ทดลองใช้ภาษาเพิ่มเติมเช่น Hindi หรือ Tamil – เพียงเพิ่มลงใน `setRecognitionLanguage`.  
* ผสานผลลัพธ์กับดัชนีการค้นหา (เช่น Elasticsearch) เพื่อเปิดใช้งานการค้นหา **image to text Java** บนเอกสารสแกน  

อย่าลังเลที่จะคอมเมนต์หากมีสิ่งที่ไม่ทำงานตามคาด หรือแชร์การปรับแต่งของคุณเอง ขอให้เขียนโค้ดอย่างสนุกสนานและสแกนของคุณเป็นใสเหมือนคริสตัล!  

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณ  

- [สกัดข้อความจากรูปภาพ – พื้นฐาน OCR ด้วย Aspose.OCR for Java](/ocr/english/java/ocr-basics/)  
- [วิธี OCR ข้อความรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)  
- [จดจำข้อความรูปภาพด้วย Aspose OCR – คู่มือ Java OCR ฉบับเต็ม](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}