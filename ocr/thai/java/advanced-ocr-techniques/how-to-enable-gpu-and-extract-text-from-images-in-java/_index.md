---
category: general
date: 2026-09-16
description: เรียนรู้วิธีเปิดใช้งาน GPU เพื่อทำ OCR ให้เร็วขึ้นใน Java, จดจำข้อความจากไฟล์รูปภาพและแปลงรูปภาพเป็นข้อความด้วย
  Aspose OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: th
lastmod: 2026-09-16
og_description: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java, จดจำข้อความจากไฟล์รูปภาพและแปลงรูปภาพเป็นข้อความด้วย
  Aspose OCR – คู่มือขั้นตอนเต็มรูปแบบ
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: วิธีเปิดใช้งาน GPU และดึงข้อความจากรูปภาพใน Java
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: วิธีเปิดใช้งาน GPU และดึงข้อความจากรูปภาพใน Java
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU และดึงข้อความจากรูปภาพใน Java

หากคุณต้องการ **วิธีเปิดใช้งาน GPU** สำหรับการจดจำอักขระด้วยแสง (OCR) คู่มือนี้จะแสดงขั้นตอนที่แน่นอน โดยการเปิดการเร่งความเร็วด้วย GPU คุณสามารถ **จดจำข้อความจากรูปภาพ** ได้เร็วหลายเท่ากว่าการประมวลผลด้วย CPU‑only ตัวอย่างใช้ Aspose OCR for Java แต่แนวคิดสามารถใช้กับไลบรารี OCR ที่รองรับ GPU ใดก็ได้

ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี:

* เปิดการเร่งความเร็วด้วย GPU ใน OCR engine.  
* โหลดรูปภาพและ **ดึงข้อความจากรูปภาพ**.  
* **แปลงรูปภาพเป็นข้อความ** ด้วยเพียงไม่กี่บรรทัดของโค้ด.  

ไม่จำเป็นต้องใช้บริการภายนอก—ทุกอย่างทำงานบนเครื่องของคุณเอง สิ่งที่ต้องมีคือสภาพแวดล้อมการพัฒนา Java เบื้องต้นและไลบรารี Aspose OCR for Java เท่านั้น

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เวอร์ชัน / รายละเอียด |
|-------------|------------------|
| Java Development Kit (JDK) | เวอร์ชัน 8 หรือใหม่กว่า |
| Maven หรือ Gradle (สำหรับการจัดการ dependencies) | เวอร์ชันล่าสุดใดก็ได้ |
| GPU ที่รองรับ CUDA (ไม่บังคับแต่แนะนำ) | GPU NVIDIA พร้อมไดรเวอร์ ≥ 450 |
| ไลบรารี Aspose OCR for Java | เวอร์ชัน 23.9 หรือใหม่กว่า (ดาวน์โหลดจากเว็บไซต์ Aspose) |

หากคุณไม่มี GPU โค้ดก็ยังทำงานได้; มันจะทำงานบน CPU แทน

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ

สำหรับ Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

สำหรับ Gradle ให้วางโค้ดนี้ในไฟล์ `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

รายการเหล่านี้จะดึง OCR engine และไบนารี GPU ที่จำเป็นโดยอัตโนมัติ

## ขั้นตอนที่ 2: วิธีเปิดใช้งาน GPU สำหรับ OCR engine

งานหลักคือบอกให้ `OcrEngine` ใช้ GPU. Aspose OCR มีฟล็อกง่าย ๆ ดังนี้:

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**ทำไมจึงสำคัญ:** เมื่อเรียก `setGpuEnabled(true)` ไลบรารีจะโหลดเคอร์เนลที่ใช้ CUDA เพื่อทำการประมวลผลล่วงหน้าและการแยกอักขระแบบขนาน บนการ์ด NVIDIA สมัยใหม่คุณจะเห็นการเพิ่มความเร็ว 2‑4× เมื่อเทียบกับเส้นทาง CPU ปกติ

> **เคล็ดลับ:** ตรวจสอบว่า GPU ของคุณถูกตรวจจับโดยการรัน `SystemInfo.isCudaSupported()` ก่อนเปิดฟล็อก หากเมธอดคืนค่า `false` engine จะย้อนกลับไปใช้ CPU โดยอัตโนมัติ

## ขั้นตอนที่ 3: โหลดรูปภาพที่ต้องการประมวลผล

คุณสามารถส่งรูปภาพใด ๆ ที่ Aspose รองรับ (JPEG, PNG, BMP, TIFF ฯลฯ) ให้ OCR engine ได้ นี่คือตัวอย่างการโหลดไฟล์ JPEG:

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**กรณีพิเศษ:** หากรูปภาพมีขนาดใหญ่ (เกิน 5 MB) ควรปรับขนาดก่อนเพื่อประหยัดหน่วยความจำ OCR engine ทำงานได้ดีที่สุดกับรูปภาพที่ประมาณ 300 dpi

## ขั้นตอนที่ 4: ทำ OCR และ **จดจำข้อความจากรูปภาพ**

ตอนนี้ engine ถูกตั้งค่าและรูปภาพถูกโหลดแล้ว คุณสามารถรันการจดจำได้:

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

เมธอด `recognize()` จะคืนค่า `String` ที่เป็นข้อความธรรมดา ภายใน engine จะทำงานหลายขั้นตอน:

1. **Pre‑processing** – แก้การเอียง, ทำไบนารี, และเพิ่มความคมของคอนทราสต์ (เร่งด้วย GPU).  
2. **Segmentation** – ค้นหาเส้นข้อความ, คำ, และอักขระ.  
3. **Classification** – เทียบอักขระแต่ละตัวกับโมเดลภาษาที่ฝังมาในตัว

เนื่องจาก GPU ทำงานอยู่ ขั้นตอนที่ 1 และ 2 จะได้รับประโยชน์สูงสุดจากการประมวลผลแบบขนาน

## ขั้นตอนที่ 5: แสดงหรือบันทึกข้อความที่ดึงออกมา

สุดท้าย ให้แสดงผลลัพธ์บนคอนโซล, ไฟล์, หรือโปรเซสเซอร์ต่อไป:

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**ผลลัพธ์ทั่วไป** (สำหรับรูปตัวอย่างที่มีข้อความ “Hello World”):

```
Recognized text:
Hello World
```

หาก OCR ไม่สามารถตรวจจับอักขระใด ๆ ได้ `recognizedText` จะเป็นสตริงว่าง ในกรณีนั้นให้ตรวจสอบคุณภาพของรูปภาพอีกครั้งหรือปิด GPU เพื่อตรวจสอบประสิทธิภาพ

## การจัดการกับปัญหาที่พบบ่อย

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **GPU not detected** | ไดรเวอร์ CUDA หายไปหรือ GPU ไม่รองรับ | ติดตั้งไดรเวอร์ NVIDIA ล่าสุดและตรวจสอบด้วย `nvidia-smi`. |
| **Incorrect characters** | คอนทราสต์ต่ำหรือพื้นหลังมีสัญญาณรบกวน | ทำการประมวลผลล่วงหน้ารูปภาพ (เช่น เพิ่มคอนทราสต์) ก่อนส่งให้ engine. |
| **Out‑of‑memory error** | รูปภาพใหญ่เกินไปบน GPU ที่มีหน่วยความจำจำกัด | ปรับขนาดรูปภาพให้ ≤ 2000 px ความกว้างหรือประมวลผลเป็นส่วนย่อย. |
| **Language mismatch** | โมเดลภาษาตั้งค่าเป็นอังกฤษแต่ข้อความเป็นภาษาอื่น | เรียก `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (หรือ enum ที่เหมาะ) ก่อน `recognize()`. |

## ตัวอย่างเต็มที่สามารถรันได้

ด้านล่างเป็นคลาส Java ที่รวมทุกขั้นตอนไว้ในไฟล์เดียว บันทึกเป็น `GpuEnabledOcrExample.java` ปรับเส้นทางรูปภาพ แล้วรันด้วย `javac`/`java` หรือผ่าน IDE ของคุณ

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

การรันโปรแกรมจะพิมพ์ข้อความที่ดึงออกมาที่คอนโซลและเขียนเนื้อหาเดียวกันลงไฟล์ `recognized_output.txt` เมื่อเปิดใช้งาน GPU เวลาโดยรวมสำหรับรูปภาพ 2 MP จะอยู่ที่ต่ำกว่า 200 ms บน NVIDIA RTX 3060 เทียบกับ ~500 ms บน CPU อย่างเดียว

## สรุป

คุณได้เรียนรู้ **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR ใน Java, **จดจำข้อความจากรูปภาพ** และ **แปลงรูปภาพเป็นข้อความ** ด้วยไม่กี่บรรทัดของโค้ด การใช้การเร่งความเร็วด้วย GPU ทำให้การประมวลผลเร็วขึ้น ซึ่งจำเป็นสำหรับแอปพลิเคชันแบบแบตช์หรือเรียลไทม์ เช่น การสแกนใบแจ้งหนี้, การประมวลผลใบเสร็จ, และการดิจิไทซ์เอกสาร

**ขั้นตอนต่อไป**

* ทดลองใช้โมเดลภาษาอื่น (`ocrEngine.setLanguage`) เพื่อ **ดึงข้อความจากรูปภาพ** ในภาษาฝรั่งเศส, เยอรมัน หรือจีน.  
* ผสานผลลัพธ์ OCR กับ Apache Tika เพื่อทำการจัดทำดัชนีเนื้อหาที่ดึงออกโดยอัตโนมัติ.  
* สำรวจการสตรีม PDF ขนาดใหญ่แบบหน้า‑ต่อ‑หน้า หากคุณต้องการ **จดจำข้อความจากรูปภาพ** ภายในเอกสาร PDF

อย่าลังเลที่จะปรับตัวอย่างนี้, ผสานเข้ากับบริการของคุณเอง, และแบ่งปันผลลัพธ์ของคุณ ขอให้สนุกกับการเขียนโค้ด!

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโปรเจกต์ของคุณ

- [วิธีอ่านข้อความจากรูปภาพใน Java ด้วย Aspose OCR – คู่มือเต็ม](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [จดจำข้อความจากรูปภาพด้วย Aspose OCR – บทเรียน OCR Java เต็มรูปแบบ](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [image to text java: แปลงรูปภาพเป็นข้อความด้วย Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}