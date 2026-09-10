---
category: general
date: 2026-09-10
description: ทำ OCR บนรูปภาพโดยใช้ Aspose OCR Java เรียนรู้การจดจำข้อความจาก JPEG
  ดึงข้อความจากรูปภาพ และแปลงรูปภาพเป็นข้อความอย่างมีประสิทธิภาพ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: th
lastmod: 2026-09-10
og_description: ทำ OCR บนภาพด้วย Aspose OCR Java. บทเรียนนี้แสดงวิธีการจดจำข้อความจาก
  JPEG, ดึงข้อความจากภาพ, และแปลงภาพเป็นข้อความด้วยไม่กี่บรรทัดของโค้ด.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: ทำ OCR บนภาพด้วย Aspose OCR – คู่มือ Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: วิธีทำ OCR บนรูปภาพด้วย Aspose OCR ใน Java
url: /th/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนรูปภาพด้วย Aspose OCR ใน Java

หากคุณต้องการ **perform OCR on image** ไฟล์ในแอปพลิเคชัน Java คู่มือนี้จะให้โซลูชันที่ครบถ้วนและพร้อมใช้งาน คุณจะได้เห็นวิธี **recognize text from JPEG** ไฟล์, **extract text from image** ข้อมูล, และ **convert image to text** โดยใช้ API สมัยใหม่ของ Aspose OCR  

บทแนะนำนี้จะพาคุณผ่านทุกขั้นตอนที่จำเป็น—ตั้งแต่การโหลดรูปภาพจนถึงการพิมพ์ข้อความที่ได้รับการจดจำ—เพื่อให้คุณสามารถรวมฟังก์ชัน OCR ได้โดยไม่ต้องค้นหาแหล่งข้อมูลเพิ่มเติม ไม่จำเป็นต้องใช้เครื่องมือภายนอกใด ๆ นอกจากไลบรารี Aspose OCR สำหรับ Java  

## สิ่งที่คุณจะทำสำเร็จ

* **Load an image for OCR** โดยตรงจากระบบไฟล์  
* เปิดใช้งานการเตรียมข้อมูลของ Aspose OCR (เช่น การลดสัญญาณรบกวน) เพื่อปรับปรุงความแม่นยำ  
* **Recognize text from JPEG** และรูปแบบแรสเตอร์อื่น ๆ  
* **Extract text from image** และแสดงผลออกที่คอนโซล  
* เข้าใจวิธี **convert image to text** ในตัวอย่างโค้ดที่พร้อมใช้งานในผลิตภัณฑ์  

### ข้อกำหนดเบื้องต้น

* Java Development Kit (JDK) 8 หรือใหม่กว่า.  
* Maven หรือ Gradle เพื่อจัดการ dependencies (ตัวอย่างใช้ Maven).  
* ใบอนุญาต Aspose OCR สำหรับ Java ที่ถูกต้อง (หรือคีย์ประเมินผลชั่วคราว).  
* ไฟล์รูปภาพชื่อ `sample.jpg` ที่วางไว้ในไดเรกทอรีที่รู้จัก.  

> **เคล็ดลับ:** ใช้ JPEG ความละเอียดสูง (300 dpi หรือมากกว่า) เพื่ออัตราการจดจำที่ดีที่สุด.  

## ขั้นตอน 1: เพิ่ม Aspose OCR ไปยังโปรเจกต์ของคุณ

หากคุณจัดการ dependencies ด้วย Maven ให้แทรกโค้ดสแนปช็อตต่อไปนี้ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

สำหรับ Gradle ให้เพิ่ม:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

พิกัดเหล่านี้จะดึงไลบรารี Aspose OCR เวอร์ชันเสถียรล่าสุด ซึ่งรวมถึงคุณสมบัติการเตรียมข้อมูลที่ใช้ในภายหลัง.  

## ทำ OCR บนรูปภาพ – ทีละขั้นตอน

ส่วนต่อไปนี้จะแบ่งโปรแกรมเต็มรูปแบบออกเป็นส่วน ๆ แต่ละบล็อกเป็นส่วนที่สามารถทำงานได้เอง คุณสามารถคัดลอก วาง และรันได้.  

### โหลดรูปภาพสำหรับ OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*ทำไมเรื่องนี้สำคัญ:*  
`ImageStream.fromFile` อ่านไบต์ดิบของ JPEG และเตรียมให้กับเอนจิน OCR วิธีนี้ทำงานกับรูปแบบแรสเตอร์ใด ๆ ที่ Aspose OCR รองรับ ดังนั้นคุณสามารถเปลี่ยน JPEG เป็น PNG หรือ BMP ได้โดยไม่ต้องแก้ไขโค้ด.  

### สร้างและกำหนดค่า OCR engine

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*ทำไมเรื่องนี้สำคัญ:*  
การสร้างอินสแตนซ์ `OcrEngine` จะจัดสรรเอนจินการจดจำหลัก การเปิดใช้ฟลัก **denoise** จะลบสัญญาณรบกวนภาพที่มักขัดขวางการตรวจจับอักขระ โดยเฉพาะใน JPEG ที่สแกน.  

### จดจำข้อความจาก JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*ทำไมเรื่องนี้สำคัญ:*  
`engine.setImage` ผูกข้อมูลภาพเข้ากับ pipeline ของ OCR `engine.recognize()` ทำกระบวนการจดจำทั้งหมดและคืนค่า `OcrResult` ที่มีข้อความที่สกัดและเมตริกความมั่นใจ.  

### สกัดข้อความจากรูปภาพและแสดงผล

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*ทำไมเรื่องนี้สำคัญ:*  
`result.getText()` ให้การแสดงผลเป็นข้อความธรรมดาของเนื้อหาภาพ การพิมพ์ออกที่คอนโซลแสดงให้เห็นว่า **convert image to text** สำเร็จแล้ว และคุณสามารถส่งต่อสตริงนี้ไปยังไฟล์ ฐานข้อมูล หรือบริการต่อไปได้.  

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นคลาส Java ครบชุดที่รวมทุกขั้นตอนแล้ว แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มของไฟล์ JPEG ของคุณ.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `sample.jpg` มีข้อความ “Hello World” คอนโซลจะแสดง:

```
=== Recognized Text ===
Hello World
```

หากภาพมีหลายบรรทัด แต่ละบรรทัดจะปรากฏบนบรรทัดของตัวเองในผลลัพธ์.  

## ความแปรผันทั่วไปและกรณีขอบ

| สถานการณ์ | การปรับแต่งที่แนะนำ |
|---|---|
| **JPEG ความละเอียดต่ำ** (≤150 dpi) | เพิ่ม `engine.getPreprocessing().setUpsample(true);` เพื่อให้ Aspose ขยายขนาดก่อนการจดจำ. |
| **พื้นหลังสี** (เช่น แบบฟอร์มที่สแกน) | เปิดใช้งาน `engine.getPreprocessing().setBinarize(true);` เพื่อแปลงภาพเป็นสีขาว‑ดำ. |
| **สคริปต์ที่ไม่ใช่ละติน** (เช่น Cyrillic) | ตั้งค่าภาษา: `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **การประมวลผลเป็นชุดขนาดใหญ่** | ใช้อินสแตนซ์ `OcrEngine` เดียวกันหลายภาพเพื่อลดภาระการเริ่มต้น. |
| **ต้องการคะแนนความมั่นใจ** | เข้าถึง `result.getConfidence()` เพื่อรับค่าความมั่นใจต่ออักขระ. |

การปรับแต่งเหล่านี้แสดงให้เห็นว่าคุณสามารถ **load image for OCR** ภายใต้เงื่อนไขต่าง ๆ ในขณะที่ยังคง **perform OCR on image** อย่างเชื่อถือได้.  

## พิจารณาด้านประสิทธิภาพ

* **Memory usage:** แต่ละ `ImageStream` จะเก็บภาพทั้งหมดในหน่วยความจำ สำหรับไฟล์ขนาดใหญ่มาก (เช่น >10 MB) ควรพิจารณา stream ภาพเป็นชิ้นส่วนโดยใช้ `ImageStream.fromByteArray`.  
* **Thread safety:** `OcrEngine` *ไม่* ปลอดภัยต่อการทำงานหลายเธรด สร้างอินสแตนซ์แยกสำหรับแต่ละเธรดหากคุณวางแผนทำ OCR แบบขนาน.  
* **License mode:** โหมดประเมินผลจำกัดจำนวนหน้าที่ประมวลผลต่อเซสชัน ใช้เวอร์ชันที่มีใบอนุญาตสำหรับงานผลิตจริง.  

## สรุป

ตอนนี้คุณรู้วิธี **perform OCR on image** ไฟล์ใน Java ด้วย Aspose OCR แล้ว บทแนะนำได้ครอบคลุมการโหลดรูปภาพ การเปิดใช้การเตรียมข้อมูล การจดจำข้อความจาก JPEG การสกัดข้อความ และการแปลงรูปภาพเป็นข้อความ—ทั้งหมดในโปรแกรมสั้น ๆ ที่รวมกันเป็นหนึ่งเดียว  

จากนี้คุณสามารถสำรวจหัวข้อที่เกี่ยวข้อง เช่น **recognize text from JPEG** แบบเป็นกลุ่ม ผสานผลลัพธ์กับดัชนีการค้นหา หรือรวม OCR กับการประมวลผลภาษาธรรมชาติเพื่อสร้าง pipeline เอกสารที่ฉลาดขึ้น ทดลองใช้ตัวเลือกการเตรียมข้อมูลเพื่อให้ได้ความแม่นยำที่ดีที่สุดสำหรับแหล่งภาพของคุณ.  

--- 

*Image illustrating the code output*  
![ตัวอย่างการทำ OCR บนรูปภาพด้วย Aspose OCR Java](image-placeholder.png){alt="ทำ OCR บนรูปภาพด้วย Aspose OCR Java"}

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโครงการของคุณ.

- [จดจำข้อความจากรูปภาพด้วย Aspose OCR – บทแนะนำ OCR Java เต็มรูปแบบ](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [วิธีทำ OCR ข้อความรูปภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [เตรียมข้อมูล OCR รูปภาพใน Java ด้วย Aspose OCR – เพิ่มความแม่นยำและสกัดข้อความ](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}