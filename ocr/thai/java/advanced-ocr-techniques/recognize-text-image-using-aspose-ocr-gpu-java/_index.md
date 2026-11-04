---
category: general
date: 2026-10-30
description: เรียนรู้วิธีดึงข้อความจากรูปภาพอย่างรวดเร็วด้วยการสนับสนุน Aspose OCR
  GPU ใน Java คู่มือนี้แสดงวิธีตั้งค่า GPU device ID เพื่อให้ได้ OCR ประสิทธิภาพสูง
draft: false
keywords:
- extract text from image
- how to extract text
- aspose ocr gpu
- recognize text image java
- gpu acceleration OCR
lastmod: 2026-10-30
og_description: เรียนรู้วิธีดึงข้อความจากรูปภาพอย่างรวดเร็วด้วยการสนับสนุน Aspose
  OCR GPU ใน Java คู่มือนี้แสดงวิธีตั้งค่า GPU device ID เพื่อประสิทธิภาพที่ดีที่สุด
og_image_alt: 'Developer guide: extract text from image using Aspose OCR GPU in Java'
og_title: วิธีดึงข้อความจากรูปภาพด้วย Aspose OCR GPU ใน Java
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to extract text from image quickly with Aspose OCR GPU support
    in Java. This guide shows how to set GPU device ID and achieve high‑performance
    OCR.
  headline: How to extract text from image with Aspose OCR GPU in Java
  type: TechArticle
- questions:
  - answer: Yes—just install a valid Aspose OCR license. The free trial is for evaluation
      only.
    question: Can I use this in a commercial application?
  - answer: Absolutely; as long as the NVIDIA driver and CUDA toolkit are installed,
      the library runs on headless Linux environments.
    question: Does the GPU version work on Linux servers?
  - answer: Aspose OCR can process images up to **5000 × 5000 px** without loading
      the whole file into memory.
    question: What is the maximum image size supported?
  - answer: Replace the old JAR with the new one and update your Maven/Gradle dependency
      version number.
    question: How do I upgrade to the latest Aspose OCR version?
  - answer: Yes—`OcrResult` provides layout information, including word‑level bounding
      boxes, when you enable the `setIncludeLayout(true)` option.
    question: Is there a way to get bounding‑box coordinates for each word?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: วิธีดึงข้อความจากรูปภาพด้วย Aspose OCR GPU ใน Java
url: /th/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการดึงข้อความจากภาพด้วย Aspose OCR GPU ใน Java

หากคุณเคยพยายาม **ดึงข้อความจากภาพ** ในแอปพลิเคชัน Java แล้วพบว่า CPU ทำงานหนักกับสแกนความละเอียดสูง คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนเจออุปสรรคด้านประสิทธิภาพเมื่อประมวลผลเอกสารขนาดใหญ่ Aspose OCR for Java จะแก้ปัญหานี้โดยให้คุณรัน OCR บน GPU ซึ่งช่วยลดเวลาการประมวลผลอย่างมาก ในบทแนะนำนี้คุณจะได้เห็นตัวอย่างที่พร้อมรันเต็มรูปแบบ ซึ่งจะแสดงวิธีตั้งค่าไลเซนส์, เปิดใช้งานการเร่งความเร็วด้วย GPU, และ **ตั้งค่า gpu device id** เมื่อมีการ์ดกราฟิกหลายตัว

## คำตอบอย่างรวดเร็ว
- **วิธีที่เร็วที่สุดในการดึงข้อความจากภาพใน Java คืออะไร?** ใช้ Aspose OCR พร้อมการเร่งความเร็วด้วย GPU และตั้งค่า GPU device ID ที่เหมาะสม  
- **ต้องใช้ Java เวอร์ชันใด?** แนะนำให้ใช้ Java 17 หรือใหม่กว่าเพื่อประสิทธิภาพที่ดีที่สุด  
- **ต้องมีไลเซนส์สำหรับการสนับสนุน GPU หรือไม่?** ใช่—ฟีเจอร์ GPU จะเปิดใช้งานได้เฉพาะเมื่อมีไลเซนส์ Aspose OCR ที่ถูกต้อง  
- **สามารถรันบนเซิร์ฟเวอร์แบบ headless ได้หรือไม่?** แน่นอน; เพียงต้องมีไดรเวอร์ GPU และชุดเครื่องมือ CUDA  
- **รองรับกี่ภาษาบ้าง?** มากกว่า 30 ภาษา รวมถึง English, Chinese, Arabic, และ Hindi

## การดึงข้อความจากภาพคืออะไร?
การดึงข้อความจากภาพหมายถึงการแปลงการแสดงผลของอักขระที่เก็บอยู่ในรูปแบบบิตแมป เช่น PNG, JPG หรือ TIFF ให้เป็นข้อความ Unicode ที่แก้ไขได้และค้นหาได้ กระบวนการนี้เรียกว่า Optical Character Recognition (OCR) ซึ่งช่วยให้ทำงานต่อได้ เช่น การทำดัชนี, การแปล, และการสกัดข้อมูล

## ทำไมต้องใช้ Aspose OCR GPU?
Aspose OCR ใช้การเร่งความเร็วด้วย GPU เพื่อจัดการกับภาพความละเอียดสูงได้อย่างมีประสิทธิภาพกว่าการประมวลผลด้วย CPU เพียงอย่างเดียว รองรับรูปแบบอินพุตกว่า 30 แบบและสามารถประมวลผลภาพขนาดสูงสุด 5000 × 5000 px ในขณะที่ใช้หน่วยความจำน้อย ให้ความเร็วการจดจำสูงสุดถึงห้าเท่าบน GPU NVIDIA รุ่นใหม่

## สิ่งที่คุณต้องเตรียม
- **Java 17** หรือใหม่กว่า (เข้ากันได้กับ Java 8+ แต่รุ่น LTS ให้ประสิทธิภาพ JIT ดีกว่า)  
- **Aspose OCR for Java** library (ดาวน์โหลดไฟล์ JAR จากเว็บไซต์ Aspose)  
- ไฟล์ไลเซนส์ **Aspose OCR** ที่ถูกต้อง (`Aspose.OCR.lic`) รุ่นทดลองฟรีใช้งานได้ แต่ฟีเจอร์ GPU ต้องมีไลเซนส์  
- ไฟล์ภาพ (`sample-image.png`) ที่มีข้อความที่อ่านได้ชัดเจน  
- GPU NVIDIA ที่รองรับ CUDA (หรืออุปกรณ์เทียบเท่า) พร้อมไดรเวอร์ที่ติดตั้งแล้ว  

หากคุณไม่คุ้นเคยกับข้อใดข้อหนึ่ง ไม่ต้องกังวล—เราจะอธิบายแต่ละหัวข้อขณะดำเนินการ

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ
แรกเริ่มให้ใส่ไฟล์ JAR ของ Aspose OCR ลงใน classpath หากใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ใน `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

สำหรับ Gradle ให้ใช้:

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

หากคุณชอบวิธีแบบแมนนวล ให้วาง JAR ไว้ในโฟลเดอร์ `libs/` แล้วเพิ่มเข้าไปใน module path ของ IDE

> **เคล็ดลับ:** ควรให้หมายเลขเวอร์ชันตรงกับบันทึกการปล่อยเวอร์ชันใหม่ ๆ เพราะเวอร์ชันล่าสุดมักมีการปรับปรุงประสิทธิภาพสำหรับการประมวลผลด้วย GPU

## ขั้นตอนที่ 2: โหลดไลเซนส์ Aspose OCR (จำเป็นสำหรับการใช้ GPU)
หากไม่มีไลเซนส์ การเรียก `setEnableGpu(true)` จะกลับไปใช้โหมด CPU อย่างเงียบ ๆ โหลดไลเซนส์ตั้งแต่ต้นของเมธอด `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มหรือพาธสัมพันธ์ที่เก็บไฟล์ `.lic` ไว้ พาธที่ไม่ถูกต้องจะทำให้เกิด `FileNotFoundException` ดังนั้นตรวจสอบการสะกดให้แน่นอน

## ขั้นตอนที่ 3: สร้าง OCR engine และเปิดใช้งานการเร่งความเร็วด้วย GPU
คลาส `OcrEngine` เป็นคอมโพเนนต์หลักที่ทำการ OCR บนภาพ

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

ทำไมต้องตั้งค่า device ID? ในสภาพแวดล้อมที่มีหลาย GPU คุณสามารถกำหนดให้การประมวลผลบางส่วนทำบนการ์ดหนึ่งและ OCR บนการ์ดอีกการ์ดหนึ่ง การตั้งค่า ID จะทำให้แน่ใจว่าการทำงานหนักใช้ฮาร์ดแวร์ที่ต้องการ

## ขั้นตอนที่ 4: เตรียมภาพอินพุต
คลาส `OcrInput` แสดงชุดของภาพที่คุณต้องการประมวลผล

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

หากต้องการประมวลผลจากสตรีม (เช่นไฟล์ที่อัปโหลด) ให้ใช้ `ocrInput.add(InputStream)` แทน

## ขั้นตอนที่ 5: รันกระบวนการจดจำและดึงผลลัพธ์
คลาส `OcrResult` เก็บข้อความที่ได้, คะแนนความมั่นใจ, และข้อมูล layout (ถ้ามี) ที่ส่งกลับจาก engine

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

คอนโซลจะแสดงผลประมาณนี้:

```
Recognized text:
Hello, world!
This is a sample image.
```

หากภาพเบลอหรือภาษาที่เลือกไม่รองรับ ผลลัพธ์อาจเป็นค่าว่าง ในกรณีนั้นให้ตรวจสอบค่า `ocrResult.getConfidence()` (0‑100) เพื่อพิจารณาว่าต้องทำการ preprocessing ใหม่หรือไม่

## ตัวอย่างเต็มที่สามารถรันได้
รวมทุกส่วนเข้าด้วยกันจะได้คลาส Java เดียวที่คุณสามารถคัดลอก‑วางลงใน IDE ได้:

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **ผลลัพธ์ที่คาดหวัง:** คอนโซลจะแสดงข้อความที่ตรงกับที่อยู่ใน `sample-image.png` เมื่อ GPU ทำงานอยู่ เวลาในการประมวลผลจะลดจากหลายวินาที (CPU) เหลือภายใต้หนึ่งวินาทีสำหรับสแกน 300 dpi ปกติ

## คำถามทั่วไป & กรณีขอบ

### ทำงานบนเซิร์ฟเวอร์แบบ headless ได้หรือไม่?
ได้. เพียงต้องติดตั้งไดรเวอร์ GPU แต่ไม่จำเป็นต้องมีหน้าจอ ตรวจสอบให้แน่ใจว่า toolkit `CUDA` (หรือเทียบเท่าสำหรับ GPU ของคุณ) อยู่ใน `PATH` ของระบบ การตั้งค่านี้ทำให้ OCR รันบนคลาวด์หรือคอนเทนเนอร์ที่ไม่มี GUI ได้

### ถ้ามี GPU มากกว่าหนึ่งตัวและต้องการใช้ GPU 1 จะทำอย่างไร?
เปลี่ยน device ID ตามตัวอย่าง:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

การตั้งค่าเป็น `1` จะสั่งให้ OCR engine ใช้ GPU ตัวที่สองในระบบ ซึ่งมีประโยชน์เมื่อ GPU ตัวแรกถูกสงวนไว้ให้กับงานอื่น

### วิธีดึงข้อความจากภาพในภาษาต่าง ๆ?
ตั้งค่าภาษา ก่อนเรียก `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose OCR รองรับ **มากกว่า 30 ภาษา** รวมถึงสคริปต์จากขวาไปซ้ายเช่น Arabic และ Hebrew การเลือกภาษาที่ถูกต้องจะเพิ่มความแม่นยำอย่างมาก

### ถ้าภาพมีหลายหน้า (เช่น PDF ที่แปลงเป็นภาพ) จะทำอย่างไร?
สร้างรายการ `OcrInput` แยกสำหรับแต่ละหน้า หรือวนลูปไฟล์:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Engine จะต่อผลลัพธ์ตามลำดับหน้าเพื่อให้ได้ลำดับที่ถูกต้องในเอาต์พุตสุดท้าย

### จะจัดการกับผลลัพธ์ที่ความมั่นใจต่ำอย่างไร?
ตรวจสอบคะแนนความมั่นใจ:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

ขั้นตอน preprocessing ที่มักใช้ได้แก่ การทำ binarization, ลดสัญญาณรบกวน, หรือปรับขนาดเป็น 300 dpi การรัน OCR ใหม่หลังจาก preprocessing มักทำให้คะแนนความมั่นใจสูงขึ้น

## เคล็ดลับการเพิ่มประสิทธิภาพ
- **การประมวลผลเป็นชุด:** เพิ่มหลายภาพลงใน `OcrInput` เดียวจะลดค่าโอเวอร์เฮดจากการเริ่มต้น context ของ GPU ซ้ำหลายครั้ง  
- **Warm‑up:** รันการจดจำจำลองหนึ่งครั้งหลังจากเริ่ม JVM; คำเรียกแรกจะใช้เวลาโหลดไดรเวอร์  
- **การจัดการหน่วยความจำ:** ทำลายอ็อบเจ็กต์ `OcrInput` ขนาดใหญ่ (`ocrInput.clear()`) หลังใช้งานเพื่อคืนหน่วยความจำ GPU  

## สรุป
คุณได้เรียนรู้วิธี **ดึงข้อความจากภาพ** อย่างมีประสิทธิภาพด้วย Aspose OCR GPU engine ใน Java, วิธี **ตั้งค่า gpu device id** เมื่อทำงานกับการ์ดกราฟิกหลายตัว, และวิธีจัดการกับสถานการณ์หลายภาษา โค้ดเต็มที่พร้อมรันด้านบนควรทำงานได้ทันที—เพียงเปลี่ยนไลเซนส์และพาธของภาพของคุณ

พร้อมก้าวต่อไปหรือยัง? ลองประมวลผลโฟลเดอร์เต็มของ PDF ที่สแกน, ทดลองตัวเลือก `setLanguage` ต่าง ๆ, หรือผสานผลลัพธ์ OCR กับโมเดลแมชชีนเลิร์นนิงเพื่อทำ post‑processing การเร่งความเร็วด้วย GPU ทำให้โครงการขนาดใหญ่เป็นไปได้จริง

ขอให้เขียนโค้ดสนุกนะครับ และหากเจอปัญหาใด ๆ อย่าลังเลที่จะคอมเมนต์!

## คำถามที่พบบ่อย

**ถาม: สามารถใช้ในแอปพลิเคชันเชิงพาณิชย์ได้หรือไม่?**  
ตอบ: ใช่—เพียงติดตั้งไลเซนส์ Aspose OCR ที่ถูกต้อง รุ่นทดลองฟรีใช้เพื่อการประเมินเท่านั้น

**ถาม: เวอร์ชัน GPU ทำงานบนเซิร์ฟเวอร์ Linux ได้หรือไม่?**  
ตอบ: แน่นอน; ตราบใดที่ติดตั้งไดรเวอร์ NVIDIA และ toolkit CUDA แล้ว ไลบรารีจะทำงานบนสภาพแวดล้อม Linux แบบ headless

**ถาม: ขนาดภาพสูงสุดที่รองรับคือเท่าไหร่?**  
ตอบ: Aspose OCR สามารถประมวลผลภาพได้สูงสุด **5000 × 5000 px** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ

**ถาม: จะอัปเกรดเป็นเวอร์ชัน Aspose OCR ล่าสุดอย่างไร?**  
ตอบ: แทนที่ JAR เก่าด้วยไฟล์ใหม่และอัปเดตหมายเลขเวอร์ชันใน dependency ของ Maven/Gradle

**ถาม: มีวิธีรับพิกัด bounding‑box ของแต่ละคำหรือไม่?**  
ตอบ: มี—`OcrResult` ให้ข้อมูล layout รวมถึง bounding box ระดับคำเมื่อเปิดใช้งาน `setIncludeLayout(true)`

---

**อัปเดตล่าสุด:** 2026-10-30  
**ทดสอบด้วย:** Aspose OCR for Java 24.11  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [Recognize Text From Image Java Ocr With Gpu Acceleration](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/)
- [How To Enable Gpu For Ocr In Java Extract Text From Image](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)
- [Extract Text From Image With Aspose Ocr Java Quick Guide](/ocr/java/ocr-basics/extract-text-from-image-with-aspose-ocr-java-quick-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}