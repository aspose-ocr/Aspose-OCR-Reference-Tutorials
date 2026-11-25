---
category: general
date: 2026-05-31
description: จดจำข้อความจากภาพอย่างรวดเร็วโดยใช้ Aspose OCR Java. เรียนรู้วิธีดึงข้อความจากไฟล์
  PNG และตั้งค่าภาษา OCR เพื่อผลลัพธ์ที่ดีที่สุด.
draft: false
keywords:
- recognize text from images
- extract text from png
- set OCR language
- Aspose OCR Java
- parallel OCR processing
language: th
og_description: จดจำข้อความจากภาพอย่างมีประสิทธิภาพด้วย Aspose OCR Java. บทเรียนนี้แสดงวิธีการดึงข้อความจากไฟล์
  PNG และตั้งค่าภาษา OCR สำหรับการประมวลผลแบบกลุ่ม.
og_title: จดจำข้อความจากภาพ – Aspose OCR Java Parallel Batch
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  headline: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  type: TechArticle
- description: recognize text from images quickly using Aspose OCR Java. Learn how
    to extract text from png files and set OCR language for optimal results.
  name: recognize text from images with Aspose OCR – Java Parallel Batch Guide
  steps:
  - name: How It Works
    text: '- **Thread Count** – The processor creates a thread pool of the size you
      specify. On a quad‑core laptop, `4` is a sweet spot; increase it for servers
      with more cores. - **Language Setting** – By calling `setLanguage(OcrLanguage.FRENCH)`,
      we tell the OCR engine to bias its dictionary toward French ch'
  - name: 1️⃣ Missing or Corrupt Images
    text: If an image path is invalid, `OcrBatchProcessor` throws an `IOException`.
      Wrap the call in a try‑catch block, log the problematic file, and continue with
      the rest of the batch.
  - name: 2️⃣ Mixed Languages in One Batch
    text: 'When you have documents in multiple languages, you can either:'
  - name: 3️⃣ Memory Constraints
    text: Processing very large images (e.g., >10 MB) can inflate heap usage. Pre‑scale
      the images or increase the JVM’s `-Xmx` flag if you encounter `OutOfMemoryError`.
  - name: 4️⃣ Customizing OCR Settings
    text: 'Beyond language, you can tweak recognition speed vs. accuracy:'
  - name: LicenseUtil.java
    text: '```java import com.aspose.ocr.*;'
  - name: ImageProvider.java
    text: '```java import java.util.*;'
  - name: ParallelBatchDemo.java
    text: '```java import com.aspose.ocr.*; import java.util.*;'
  type: HowTo
tags:
- Java
- OCR
- Aspose
- Image Processing
title: แยกข้อความจากรูปภาพด้วย Aspose OCR – คู่มือการประมวลผลแบบขนานใน Java
url: /th/java/advanced-ocr-techniques/recognize-text-from-images-with-aspose-ocr-java-parallel-bat/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพ – Aspose OCR Java Parallel Batch Tutorial

เคยสงสัยไหมว่าจะ **recognize text from images** อย่างไรโดยที่ไม่ทำให้ UI ของคุณค้าง? บางทีคุณอาจมีโฟลเดอร์ที่เต็มไปด้วยสแกน, ภาพหน้าจอ, หรือแม้แต่ไฟล์ PNG และ JPEG ผสมกัน, และคุณต้องการข้อความโดยเร็วที่สุด. ข่าวดี? ด้วย Aspose OCR for Java คุณสามารถสร้างแบตช์แบบหลายเธรดที่ **extracts text from png** (และรูปแบบอื่น) ขณะคุณดื่มกาแฟ.

ในคู่มือนี้เราจะพาคุณผ่านตัวอย่างที่สมบูรณ์พร้อมรันที่แสดงวิธี **set OCR language**, เริ่มทำงานของ worker สี่ตัวแบบขนาน, และพิมพ์ผลลัพธ์. เมื่อจบคุณจะได้เทมเพลตที่มั่นคงซึ่งสามารถนำไปใช้ในโปรเจค Java ใดก็ได้—ไม่มีของเกินจำเป็น, มีแค่โค้ดที่คุณต้องการ.

## สิ่งที่คุณจะได้เรียนรู้

- วิธีการใช้ใบอนุญาต Aspose OCR เพื่อไม่ให้คุณเจอข้อจำกัดของรุ่นทดลอง.  
- ขั้นตอนที่แน่นอนเพื่อ **recognize text from images** แบบขนาน, เพิ่มประสิทธิภาพบนเครื่องหลายคอร์.  
- เหตุผลและวิธีการ **set OCR language** (ภาษาฝรั่งเศสในตัวอย่าง) เพื่อความแม่นยำที่ดียิ่งขึ้น.  
- วิธีการเชิงปฏิบัติเพื่อ **extract text from png** ไฟล์, แต่ตรรกะเดียวกันทำงานกับ JPG, TIFF, BMP, เป็นต้น.  

**Prerequisites** – คุณจะต้องมี Java 8 หรือใหม่กว่า, Maven หรือ Gradle เพื่อดึงไลบรารี Aspose OCR, และไฟล์ใบอนุญาต Aspose OCR ที่ถูกต้อง (`Aspose.OCR.Java.lic`). ไม่จำเป็นต้องใช้เทคนิคพิเศษใน IDE; แก้ไขใด ๆ ที่สามารถคอมไพล์ Java ได้ก็เพียงพอ.

---

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR Dependency

ขั้นแรก, ตรวจสอบให้แน่ใจว่าไฟล์ JAR ของ Aspose OCR อยู่ใน classpath ของคุณ. หากคุณใช้ Maven, ให้เพิ่ม:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

สำหรับ Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

> **Pro tip:** คอยติดตามบันทึกการปล่อยของ Aspose; พวกเขามักจะเพิ่มแพ็คภาษา หรือการปรับประสิทธิภาพที่สามารถลดเวลาการรันแบตช์ได้หลายวินาที.

## ขั้นตอนที่ 2: ใช้ใบอนุญาต Aspose OCR

หากไม่มีใบอนุญาต ไลบรารีจะทำงานในโหมดสาธิตและจะใส่ลายน้ำในผลลัพธ์. โหลดไฟล์ใบอนุญาตของคุณเพียงครั้งเดียว, ควรทำในขั้นตอนเริ่มต้นของแอปพลิเคชัน.

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    /** Loads the Aspose OCR license from the given path. */
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

การเรียก `LicenseUtil.applyLicense("Aspose.OCR.Java.lic")` จะทำให้การเรียก **recognize text from images** ทุกครั้งต่อมาทำงานโดยไม่มีข้อจำกัด.

## ขั้นตอนที่ 3: เตรียมรายการรูปภาพ

คุณสามารถส่งคอลเลกชันของเส้นทางไฟล์ใด ๆ ให้กับ batch processor. ด้านล่างเราจะแสดงตัวอย่างการ **extract text from png** ควบคู่กับไฟล์ JPEG และ TIFF—เพียงเปลี่ยนเส้นทางเป็นไดเรกทอรีของคุณเอง.

```java
import java.util.*;

public class ImageProvider {
    /** Returns a list of absolute image paths to be processed. */
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",   // PNG – our primary example
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

> **Why a List?** `OcrBatchProcessor` คาดหวัง `List<String>` เพื่อให้สามารถแบ่งงานไปยังเธรดได้โดยอัตโนมัติ.

## ขั้นตอนที่ 4: ตั้งค่าและรัน Parallel Batch Processor

ต่อไปเป็นหัวใจของบทแนะนำ: การสร้าง `OcrBatchProcessor`, ระบุจำนวนเธรดที่จะสร้าง, และ **set OCR language** เป็นภาษาฝรั่งเศส (เปลี่ยนเป็น `OcrLanguage.ENGLISH` หรือภาษาอื่นที่รองรับตามต้องการ).

```java
import com.aspose.ocr.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // 2️⃣ Gather image files
        List<String> imagePaths = ImageProvider.getImagePaths();

        // 3️⃣ Create and configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // 4 parallel workers
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // 4️⃣ Run OCR on the entire batch – this is where we **recognize text from images**
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // 5️⃣ Output the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### วิธีการทำงาน

- **Thread Count** – ตัวประมวลผลจะสร้าง thread pool ตามขนาดที่คุณระบุ. บนแล็ปท็อปคอร์สี่, `4` เป็นค่าที่เหมาะสม; เพิ่มจำนวนสำหรับเซิร์ฟเวอร์ที่มีคอร์มากกว่า.  
- **Language Setting** – โดยการเรียก `setLanguage(OcrLanguage.FRENCH)`, เราบอกให้เครื่อง OCR ปรับพจนานุกรมให้เหมาะกับอักขระภาษาฝรั่งเศส, ซึ่งจะเพิ่มความแม่นยำอย่างมากสำหรับเอกสารที่ไม่ใช่ภาษาอังกฤษ.  
- **Batch Recognition** – เมธอด `recognize` จะวนลูปภายในรายการที่ให้, แจกจ่ายงาน, และคืนค่า `List<OcrResult>` ที่คงลำดับเดิม. นี่เป็นวิธีที่ง่ายที่สุดในการ **recognize text from images** โดยไม่ต้องเขียนโค้ดจัดการเธรดของคุณเอง.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์

เมื่อคุณรันโปรแกรม, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
File: YOUR_DIRECTORY/doc1.png
Bonjour le monde! Ceci est un test d'OCR.
---
File: YOUR_DIRECTORY/doc2.jpg
Hello world! This is an OCR test.
---
File: YOUR_DIRECTORY/doc3.tif
¡Hola mundo! Prueba de OCR.
---
```

หากไฟล์ภาษาฝรั่งเศส (`doc1.png`) มีข้อความภาษาฝรั่งเศส, ขั้นตอน **set OCR language** จะช่วยจับอักขระที่มีสำเนียงได้อย่างถูกต้อง. สำหรับไฟล์ PNG, นี้แสดงวิธีที่ชัดเจนในการ **extract text from png** พร้อมกับจัดการรูปแบบอื่นในแบตช์เดียวกัน.

---

## การจัดการกรณีขอบเขตทั่วไป

### 1️⃣ รูปภาพหายหรือเสีย

หากเส้นทางรูปภาพไม่ถูกต้อง, `OcrBatchProcessor` จะโยน `IOException`. ห่อการเรียกในบล็อก try‑catch, บันทึกไฟล์ที่มีปัญหา, และดำเนินการต่อกับแบตช์ที่เหลือ.

```java
try {
    List<OcrResult> results = batchProcessor.recognize(imagePaths);
} catch (IOException ex) {
    System.err.println("Failed to process: " + ex.getMessage());
}
```

### 2️⃣ ภาษาผสมในแบตช์เดียว

เมื่อคุณมีเอกสารหลายภาษา, คุณสามารถทำได้สองวิธี:

- รันแบตช์แยกกัน, แต่ละแบตช์มี `setLanguage` ของตนเอง.  
- หรือไม่ตั้งค่าภาษา (`OcrLanguage.AUTO_DETECT`) ให้ Aspose คาดเดา, แม้ว่าความแม่นยำอาจลดลง.

### 3️⃣ ข้อจำกัดด้านหน่วยความจำ

การประมวลผลภาพขนาดใหญ่มาก (เช่น >10 MB) สามารถทำให้การใช้ heap เพิ่มขึ้น. ปรับขนาดภาพล่วงหน้า หรือเพิ่มค่า `-Xmx` ของ JVM หากพบ `OutOfMemoryError`.

```bash
java -Xmx2g -cp yourapp.jar ParallelBatchDemo
```

### 4️⃣ ปรับแต่งการตั้งค่า OCR

นอกเหนือจากภาษา, คุณสามารถปรับความเร็วการจดจำเทียบกับความแม่นยำ:

```java
batchProcessor.setRecognitionMode(OcrRecognitionMode.ACCURATE); // default is BALANCED
```

การเลือก `ACCURATE` จะช้ากว่าแต่ให้ผลลัพธ์ที่ดีกว่าสำหรับสแกนที่มีสัญญาณรบกวน.

## ตัวอย่างทำงานเต็ม (ทุกไฟล์)

ด้านล่างเป็นชุดไฟล์ซอร์สทั้งหมดที่คุณต้องการ. คัดลอกไปยังโปรเจค Maven, ปรับเส้นทางใบอนุญาตและไดเรกทอรีรูปภาพ, จากนั้นรัน `mvn exec:java -Dexec.mainClass=ParallelBatchDemo`.

### LicenseUtil.java
```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense(String licensePath) throws Exception {
        License license = new License();
        license.setLicense(licensePath);
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

### ImageProvider.java
```java
import java.util.*;

public class ImageProvider {
    public static List<String> getImagePaths() {
        return Arrays.asList(
            "YOUR_DIRECTORY/doc1.png",
            "YOUR_DIRECTORY/doc2.jpg",
            "YOUR_DIRECTORY/doc3.tif"
        );
    }
}
```

### ParallelBatchDemo.java
```java
import com.aspose.ocr.*;
import java.util.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // Apply license
        LicenseUtil.applyLicense("Aspose.OCR.Java.lic");

        // Gather images
        List<String> imagePaths = ImageProvider.getImagePaths();

        // Configure batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor();
        batchProcessor.setThreadCount(4);                 // Parallelism
        batchProcessor.setLanguage(OcrLanguage.FRENCH);   // set OCR language

        // Recognize text from images
        List<OcrResult> ocrResults = batchProcessor.recognize(imagePaths);

        // Output results
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imagePaths.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

รันมัน, แล้วคุณจะเห็นข้อความที่ดึงจากแต่ละไฟล์แสดงบนคอนโซล—สิ่งที่คุณต้องการเมื่อต้องสร้างคลังข้อมูลที่สามารถค้นหาได้, ระบบอัตโนมัติการป้อนข้อมูล, หรือเครื่องมือการเข้าถึง.

## สรุป

เราได้อธิบายรูปแบบที่ครบถ้วนและพร้อมใช้งานในระดับการผลิตเพื่อ **recognize text from images** ด้วย Aspose OCR for Java. ด้วยการกำหนดค่า batch processor, คุณสามารถ **extract text from png** (และรูปแบบอื่น) แบบขนาน, และความสามารถในการ **set OCR language** จะทำให้คุณได้ความแม่นยำสูงสุดสำหรับงานหลายภาษา.

ขั้นตอนต่อไป? ลองเปลี่ยนภาษาเป็น `OcrLanguage.SPANISH` หรือทดลองใช้ `OcrRecognitionMode.ACCURATE` สำหรับสแกนที่ยากขึ้น. คุณอาจรวมผลลัพธ์เข้ากับฐานข้อมูล, ส่งต่อไปยังดัชนีการค้นหา, หรือเชื่อมต่อกับ API แปลภาษา.

มีสถานการณ์ที่ท้าทาย—เช่น OCR บน PDF หรือบนรูปภาพที่เก็บในคลาวด์? สิ่งเหล่านั้นเป็นการต่อยอดที่ธรรมชาติของสิ่งที่เราสร้างวันนี้. ลองลงมือ, ปรับตั้งค่า, แล้วให้เครื่อง OCR ทำงานหนักแทนคุณ.

ขอให้เขียนโค้ดอย่างสนุกสนาน, และการดึงข้อความของคุณรวดเร็วและแม่นยำ!

## สิ่งที่คุณควรเรียนต่อไป

- [ดึงข้อความจากรูปภาพ – พื้นฐาน OCR ด้วย Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [วิธี OCR ข้อความรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [recognize text image with Aspose OCR – คู่มือ OCR Java เต็มรูปแบบ](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}