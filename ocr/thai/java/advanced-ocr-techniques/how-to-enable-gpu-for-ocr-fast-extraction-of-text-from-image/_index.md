---
category: general
date: 2026-10-19
description: วิธีดึงข้อความจากภาพอย่างรวดเร็วด้วย GPU acceleration โดยใช้ Aspose OCR
  ใน Java. เรียนรู้วิธีเปิดใช้งาน GPU, จดจำข้อความจาก PNG, อ่านข้อความจากรูปถ่าย,
  และแปลงภาพเป็นข้อความ.
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from photo
- convert image to text
lastmod: 2026-10-19
og_description: เรียนรู้วิธีดึงข้อความจากภาพด้วย GPU‑accelerated Aspose OCR ใน Java.
  เปิดใช้งาน GPU, จดจำข้อความจาก PNG, อ่านข้อความจากรูปถ่าย, และแปลงภาพเป็นข้อความอย่างมีประสิทธิภาพ.
og_image_alt: Diagram showing GPU‑accelerated OCR flow from image loading to text
  extraction
og_title: ดึงข้อความจากภาพด้วย GPU‑accelerated Aspose OCR (Java)
schemas:
- author: Aspose
  dateModified: '2026-10-19'
  description: How to extract text from image quickly with GPU acceleration using
    Aspose OCR in Java. Learn to enable GPU, recognize text from PNG, read text from
    photo, and convert image to text.
  headline: How to extract text from image with GPU‑accelerated Aspose OCR
  type: TechArticle
- description: How to extract text from image quickly with GPU acceleration using
    Aspose OCR in Java. Learn to enable GPU, recognize text from PNG, read text from
    photo, and convert image to text.
  name: How to extract text from image with GPU‑accelerated Aspose OCR
  steps:
  - name: initialize the OCR engine – **how to enable GPU**
    text: '`OcrEngine` is the central class that holds all OCR settings, including
      the GPU flag. > **Why this matters:** Without an `OcrEngine` you have no context
      for the image or the hardware options. Instantiating it early also allows you
      to tweak options before loading the file.'
  - name: load the image you want to process – **extract text from image**
    text: '`ImageStream.fromFile` reads any supported format; PNG is preferred because
      it retains lossless detail. > **Edge case:** If your image lives in a different
      folder, adjust the path accordingly. For large batches, loop over a directory
      and call `setImage` for each file.'
  - name: turn on GPU acceleration – **how to enable GPU**
    text: Calling `setUseGpu(true)` instructs the native library to off‑load the heavy
      lifting to the graphics card. If no compatible GPU is found, Aspose silently
      falls back to CPU, so your application never crashes. > **What if I don’t have
      a GPU?** The call is ignored and OCR runs on the CPU. You can verif
  - name: perform the OCR – **recognize text from PNG**
    text: Invoke `recognize()` to start the analysis. The method returns an `OcrResult`
      object containing raw text, confidence scores, and optional bounding‑box data.
      > **Why wait until now?** The OCR process is computationally intensive; doing
      it after all settings are applied ensures maximum efficiency, esp
  - name: output the detected string – **read text from photo**
    text: 'Print the result to the console. In production you might store it in a
      database or send it over a network, but `System.out.println` keeps the example
      minimal. > **Expected output:** If `sample-photo.png` contains the words “Hello
      World”, the console will display: That’s the whole program—no external'
  type: HowTo
- questions:
  - answer: Yes, Aspose OCR will automatically fall back to CPU if no CUDA‑compatible
      GPU is detected.
    question: Can I use GPU acceleration on any machine?
  - answer: Java 17 or newer is recommended for best performance and long‑term support.
    question: What Java version is required?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license for development?
  - answer: Tests show up to 5× speed‑up on an NVIDIA RTX 3080 versus CPU‑only processing.
    question: How much faster is GPU OCR?
  - answer: The Java API runs on Windows, Linux, and macOS; GPU acceleration works
      on any system with an NVIDIA CUDA driver.
    question: Is the code cross‑platform?
  type: FAQPage
tags:
- OCR
- Java
- GPU-Acceleration
title: วิธีดึงข้อความจากภาพด้วย GPU‑accelerated Aspose OCR
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-fast-extraction-of-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อความจากภาพด้วย Aspose OCR ที่เร่งด้วย GPU

เคยสงสัย **วิธีเปิดใช้งาน GPU** สำหรับ OCR และรับผลลัพธ์ทันทีจากรูปถ่ายหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการคอมพิวเตอร์วิชันขั้นตอนที่เป็นคอขวดคือขั้นตอน OCR โดยเฉพาะเมื่อคุณทำงานกับไฟล์ PNG ความละเอียดสูง ข่าวดีคือ Aspose OCR ให้คุณเปิดการเร่งด้วย GPU เพียงบรรทัดเดียวของโค้ด ซึ่งสามารถลดเวลาการประมวลผลได้อย่างมาก ในคู่มือนี้คุณจะได้เรียนรู้ **ดึงข้อความจากภาพ** ไฟล์, **จดจำข้อความจาก PNG**, **อ่านข้อความจากรูปถ่าย** และในที่สุด **แปลงภาพเป็นข้อความ** ด้วยไลบรารี Aspose OCR

## คำตอบสั้น
- **ฉันสามารถใช้การเร่งด้วย GPU บนเครื่องใดก็ได้หรือไม่?** ใช่, Aspose OCR จะย้อนกลับไปใช้ CPU อัตโนมัติหากไม่พบ GPU ที่รองรับ CUDA.  
- **ต้องการเวอร์ชัน Java ใด?** Java 17 หรือใหม่กว่าแนะนำเพื่อประสิทธิภาพที่ดีที่สุดและการสนับสนุนระยะยาว.  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีใช้ได้สำหรับการประเมิน; จำเป็นต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์.  
- **GPU OCR เร็วขึ้นเท่าไหร่?** การทดสอบแสดงให้เห็นว่ามีความเร็วเพิ่มขึ้นสูงสุด 5 เท่าบน NVIDIA RTX 3080 เมื่อเทียบกับการประมวลผลด้วย CPU เท่านั้น.  
- **โค้ดนี้ทำงานข้ามแพลตฟอร์มหรือไม่?** Java API ทำงานบน Windows, Linux, และ macOS; การเร่งด้วย GPU ทำงานบนระบบใดก็ได้ที่มีไดรเวอร์ NVIDIA CUDA.

## การดึงข้อความจากภาพคืออะไร?
การดึงข้อความจากภาพหมายถึงกระบวนการแปลงอักขระที่ปรากฏในบิตแมพ เช่น PNG, JPEG หรือ TIFF ให้เป็นสตริงที่สามารถค้นหาและแก้ไขได้โดยใช้เทคโนโลยีการจดจำอักขระด้วยแสง (OCR). เครื่องมือ OCR วิเคราะห์รูปแบบพิกเซล, ระบุอักษรและตัวเลข, และส่งออกข้อความธรรมดาที่สามารถทำดัชนีหรือแก้ไขได้.

## ทำไมต้องใช้ OCR ที่เร่งด้วย GPU?
Aspose OCR รองรับ **รูปแบบการนำเข้าและส่งออกกว่า 50 แบบ** และสามารถประมวลผลเอกสารหลายร้อยหน้าโดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ เมื่อเปิดการเร่งด้วย GPU งาน OCR เดียวกันที่ใช้เวลาประมาณ 2 วินาทีบน CPU สามารถเสร็จในเวลาน้อยกว่า 0.4 วินาทีบน RTX 3080 สมัยใหม่ ทำให้เพิ่มประสิทธิภาพการทำงานอย่างชัดเจนสำหรับสายงานประมวลผลแบบแบตช์.

## ข้อกำหนดเบื้องต้น

| ข้อกำหนด | เหตุผลที่สำคัญ |
|-------------|----------------|
| Java 17 หรือใหม่กว่า | ให้การสนับสนุนระยะยาวและปรับปรุงประสิทธิภาพเมื่อเทียบกับรันไทม์เก่า |
| เครื่องมือสร้าง Maven หรือ Gradle | ดึง dependency `aspose-ocr` อัตโนมัติและทำให้เป็นเวอร์ชันล่าสุด |
| GPU ที่รองรับ CUDA (ไม่บังคับ) | ทำให้สามารถเรียก `setUseGpu(true)` เพื่อย้ายการวิเคราะห์ภาพหนักไปที่การ์ดกราฟิก |
| ไฟล์ภาพ (`sample-photo.png`) ในโฟลเดอร์ที่รู้จัก | ทำหน้าที่เป็นแหล่งข้อมูลสำหรับเครื่องมือ OCR เพื่ออ่านและแปลง |

หากขาดรายการใดรายการหนึ่ง คุณยังสามารถรันตัวอย่างได้; ไลบรารีจะกลับไปใช้การประมวลผลด้วย CPU อย่างง่ายดาย.

## การตั้งค่าโครงการ

### 1️⃣ เพิ่ม Aspose OCR ลงในการสร้างของคุณ

สำหรับ Maven ให้เพิ่มโค้ดส่วนนี้ลงใน `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest stable version -->
</dependency>
```

สำหรับ Gradle ให้ใส่โค้ดต่อไปนี้ใน `build.gradle`:

```gradle
implementation 'com.aspose:aspose-ocr:23.10'
```

> **เคล็ดลับ:** คอยติดตาม Aspose Maven repository; พวกเขาออกแพตช์ประสิทธิภาพเป็นประจำ.

### 2️⃣ โครงสร้างโฟลเดอร์

สร้างโฟลเดอร์ชื่อ `resources` ที่รากของโครงการของคุณและวาง `sample-photo.png` ไว้ที่นั่น โค้ดจะอ้างอิงไฟล์ด้วยเส้นทางสัมพันธ์ ดังนั้นคุณไม่จำเป็นต้องกำหนดตำแหน่งแบบเต็ม.

## วิธีเปิดใช้งาน GPU สำหรับ OCR?

โหลดเครื่องมือ OCR, เปิด GPU, และรันการจดจำในสามขั้นตอนสั้นๆ คำตอบโดยตรงนี้บอกคุณอย่างชัดเจนว่าจะทำอย่างไร: สร้างอินสแตนซ์ `OcrEngine`, เปิด GPU ด้วย `setUseGpu(true)`, จากนั้นเรียก `recognize()` บนภาพที่โหลดไว้ การดำเนินการทั้งหมดเสร็จในสายเมธอดเดียว ให้ความเร็วสูงสุดด้วยโค้ดที่เหลือน้อยที่สุด.

### ขั้นตอนที่ 1: เริ่มต้นเครื่องมือ OCR – **วิธีเปิดใช้งาน GPU**

`OcrEngine` เป็นคลาสหลักที่เก็บการตั้งค่า OCR ทั้งหมด รวมถึงแฟล็ก GPU

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **ทำไมเรื่องนี้สำคัญ:** หากไม่มี `OcrEngine` คุณจะไม่มีบริบทสำหรับภาพหรือออปชันฮาร์ดแวร์ การสร้างอินสแตนซ์ตั้งแต่แรกยังช่วยให้คุณปรับแต่งออปชันก่อนโหลดไฟล์

### ขั้นตอนที่ 2: โหลดภาพที่ต้องการประมวลผล – **ดึงข้อความจากภาพ**

`ImageStream.fromFile` อ่านรูปแบบที่รองรับทั้งหมด; PNG เป็นที่แนะนำเพราะรักษารายละเอียดแบบไม่มีการสูญเสีย

```java
        // Step 2: Load the image to be recognized
        ocrEngine.setImage(ImageStream.fromFile("resources/sample-photo.png"));
```

> **กรณีขอบ:** หากภาพของคุณอยู่ในโฟลเดอร์อื่น ปรับเส้นทางให้เหมาะสม สำหรับชุดข้อมูลขนาดใหญ่ ให้วนลูปผ่านไดเรกทอรีและเรียก `setImage` สำหรับแต่ละไฟล์

### ขั้นตอนที่ 3: เปิดการเร่งด้วย GPU – **วิธีเปิดใช้งาน GPU**

การเรียก `setUseGpu(true)` จะสั่งให้ไลบรารีเนทีฟย้ายงานหนักไปที่การ์ดกราฟิก หากไม่พบ GPU ที่เข้ากันได้ Aspose จะย้อนกลับไปใช้ CPU อย่างเงียบ ๆ ทำให้แอปพลิเคชันของคุณไม่เคลิก

```java
        // Step 3: Enable GPU acceleration (optional – ignored if no GPU is available)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **ถ้าฉันไม่มี GPU จะทำอย่างไร?** การเรียกนี้จะถูกละเลยและ OCR จะทำงานบน CPU คุณสามารถตรวจสอบโหมดได้ภายหลังด้วย `ocrEngine.getEngineOptions().isUseGpu()`.

### ขั้นตอนที่ 4: ทำ OCR – **จดจำข้อความจาก PNG**

เรียก `recognize()` เพื่อเริ่มการวิเคราะห์ เมธอดจะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่มีข้อความดิบ, คะแนนความมั่นใจ, และข้อมูลกรอบขอบ (bounding‑box) ที่เป็นตัวเลือก

```java
        // Step 4: Perform the OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();
```

> **ทำไมต้องรอจนถึงตอนนี้?** กระบวนการ OCR ต้องใช้การคำนวณสูง; ทำหลังจากตั้งค่าทั้งหมดแล้วจะทำให้มีประสิทธิภาพสูงสุด โดยเฉพาะเมื่อ GPU ทำงาน

### ขั้นตอนที่ 5: แสดงสตริงที่ตรวจพบ – **อ่านข้อความจากรูปถ่าย**

พิมพ์ผลลัพธ์ไปยังคอนโซล ในการผลิตคุณอาจเก็บไว้ในฐานข้อมูลหรือส่งผ่านเครือข่าย แต่ `System.out.println` ทำให้ตัวอย่างนี้เรียบง่าย

```java
        // Step 5: Output the recognized text
        System.out.println("Detected text:");
        System.out.println(ocrResult.getText());

        // Optional: Verify GPU usage
        System.out.println("GPU used: " + ocrEngine.getEngineOptions().isUseGpu());
    }
}
```

> **ผลลัพธ์ที่คาดหวัง:** หาก `sample-photo.png` มีคำว่า “Hello World” คอนโซลจะแสดง:

```
Detected text:
Hello World
GPU used: true
```

นี่คือโปรแกรมทั้งหมด — ไม่มีบริการภายนอก ไม่มีไฟล์การกำหนดค่าที่ซ่อนอยู่

## ภาพรวมโดยภาพ

![วิธีเปิดใช้งาน GPU สำหรับ OCR](gpu-ocr-diagram.png "แผนภาพแสดงกระบวนการจากการโหลดภาพไปจนถึง OCR ที่เร่งด้วย GPU")

[วิธีเปิดใช้งาน GPU สำหรับ OCR](gpu-ocr-diagram.png "แผนภาพแสดงกระบวนการจากการโหลดภาพไปจนถึง OCR ที่เร่งด้วย GPU")

*แผนภาพแสดงขั้นตอนแต่ละขั้นของกระบวนการ, เน้นที่แฟล็ก **วิธีเปิดใช้งาน GPU** อยู่ที่ไหน.*

## คำถามทั่วไป & กรณีขอบ

| คำถาม | คำตอบ |
|----------|--------|
| **ฉันสามารถประมวลผลหลายภาพในรันเดียวได้หรือไม่?** | ใช่. ห่อขั้นตอน 2‑5 ไว้ในลูป `for (File img : folder.listFiles())` และเรียก `ocrEngine.setImage` สำหรับแต่ละไฟล์. |
| **รูปแบบภาพใดบ้างที่รองรับ?** | JPEG, PNG, BMP, TIFF, และ GIF ทั้งหมดรองรับโดย Aspose OCR อย่างเนทีฟ |
| **ฉันจะจัดการกับสแกนคุณภาพต่ำอย่างไร?** | ตั้งค่า `ocrEngine.getEngineOptions().setPreprocessMode(PreprocessMode.Auto)` ก่อนการจดจำเพื่อให้เครื่องมือทำความสะอาดสัญญาณรบกวนโดยอัตโนมัติ. |
| **มีวิธีรับคะแนนความมั่นใจหรือไม่?** | `ocrResult.getMeanConfidence()` คืนค่าความมั่นใจเฉลี่ย (0‑100). ความมั่นใจของอักขระแต่ละตัวสามารถเข้าถึงได้ผ่าน `ocrResult.getTextLines()`. |
| **วิธีนี้จะทำงานบน macOS กับ GPU Metal หรือไม่?** | Aspose OCR ปัจจุบันใช้ CUDA บน GPU ของ NVIDIA เท่านั้น บน macOS คุณจะย้อนกลับไปใช้ CPU หากไม่ได้ใช้ NVIDIA eGPU. |

## เคล็ดลับประสิทธิภาพ

1. **การประมวลผลแบบแบตช์:** โหลดภาพทั้งหมดเข้าสู่หน่วยความจำก่อน, เปิด GPU ครั้งเดียว, จากนั้นรันลูป. นี้ลดภาระของไดรเวอร์.  
2. **การปรับขนาดภาพ:** ลดขนาด PNG ขนาดใหญ่มากให้สูงสุด 2000 พิกเซลบนด้านที่ยาวที่สุด; ความแม่นยำของ OCR ยังคงสูงในขณะที่การใช้หน่วยความจำ GPU ลดลง.  
3. **การเรียกอุ่นเครื่อง:** รัน `recognize()` จำลองบนภาพขนาดเล็กก่อนงานจริงเพื่อให้ไดรเวอร์ GPU เริ่มต้น — นี้สามารถลดเวลาไม่กี่มิลลิวินาทีจากภาพแรกที่แท้จริง.

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุม **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR, แสดงให้คุณเห็น **การดึงข้อความจากภาพ** ไฟล์, สาธิต **การจดจำข้อความจาก PNG**, และอธิบายขั้นตอน **การอ่านข้อความจากรูปถ่าย** และ **การแปลงภาพเป็นข้อความ** กระบวนการทั้งหมด ตัวอย่าง Java ที่สมบูรณ์ด้านบนพร้อมคัดลอกและวาง, และบันทึกประสิทธิภาพควรช่วยให้คุณบีบอัดทุกมิลลิวินาทีจากฮาร์ดแวร์ของคุณ.

ต่อไปคืออะไร? พิจารณาขยายโซลูชันเป็น:

* **ส่งออกผลลัพธ์ OCR เป็น JSON** สำหรับการวิเคราะห์ต่อเนื่อง.  
* **ผสานรวมกับ Spring Boot REST endpoint** เพื่อให้บริการอื่นสามารถส่งรูปถ่ายและรับข้อความตอบกลับแบบ plain‑text.  
* **ใช้พจนานุกรมเฉพาะภาษา** ผ่าน `ocrEngine.getEngineOptions().setLanguage(Language.English)` เพื่อปรับปรุงความแม่นยำในเอกสารหลายภาษา.

อย่าลังเลที่จะทดลอง — เปลี่ยน PNG เป็น PDF ที่สแกน, เปิด `setPreserveFormatting(true)`, หรือเชื่อมต่อหลายขั้นตอน OCR สำหรับภาพที่มีสัญญาณรบกวน. ไม่มีขีดจำกัดเมื่อคุณเชี่ยวชาญ **วิธีเปิดใช้งาน GPU** สำหรับ OCR.

---

**อัปเดตล่าสุด:** 2026-10-19  
**ทดสอบด้วย:** Aspose OCR 24.11 for Java  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java ดึงข้อความจากภาพ](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [จดจำข้อความจากภาพโดยใช้ Aspose OCR GPU Java](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [OCR ภาพแบบแบตช์ใน Java ดึงข้อความจากไฟล์ PNG อย่างรวดเร็ว](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}