---
category: general
date: 2026-03-28
description: เรียนรู้วิธีจดจำข้อความในรูปภาพด้วย Java โดยใช้ Aspose OCR, แยกข้อความจากไฟล์
  PNG, และใช้การเร่งความเร็วด้วย GPU เพื่อทำ OCR อย่างรวดเร็วสำหรับภาพขนาดใหญ่.
draft: false
keywords:
- recognize image text
- extract text png
- use gpu acceleration
- ocr large image
- java ocr example
language: th
og_description: ค้นพบวิธีการจดจำข้อความในรูปภาพด้วย Java, แยกข้อความจากไฟล์ PNG, และใช้การเร่งความเร็วด้วย
  GPU สำหรับ OCR ของภาพขนาดใหญ่.
og_title: แยกข้อความจากภาพด้วย Java OCR – ตัวอย่างที่เร่งด้วย GPU
tags:
- OCR
- Java
- GPU
title: จดจำข้อความในภาพด้วย Java OCR – ตัวอย่างที่เร่งด้วย GPU
url: /th/java/advanced-ocr-techniques/recognize-image-text-with-java-ocr-gpu-accelerated-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความในภาพด้วย Java OCR – ตัวอย่างที่เร่งด้วย GPU

เคยต้องการ **recognize image text** จาก PNG ขนาดมหาศาลแต่พบว่าเวอร์ชัน CPU ทำงานช้าไหม? คุณไม่ได้เป็นคนเดียว ในหลาย ๆ โครงการจริง—เช่นการสแกนใบแจ้งหนี้หรือการเก็บเอกสารประวัติศาสตร์—ขนาดภาพอาจใหญ่โตและเครื่องมือ OCR เริ่มต้นไม่สามารถตามได้  

ข่าวดี: Aspose OCR for Java ให้คุณ **use GPU acceleration** เพื่อเร่งกระบวนการ และโค้ดก็สั้นและกระชับอย่างน่าประหลาดใจ ในบทแนะนำนี้คุณจะได้เห็นตัวอย่าง Java OCR ที่สมบูรณ์และสามารถรันได้ ซึ่ง **extracts text PNG** ไฟล์, ใช้ GPU ที่เปิดใช้งาน CUDA, และจัดการกับ **OCR large image** ด้วยเพียงไม่กี่บรรทัดโค้ด เมื่อจบคุณจะรู้วิธีนำไปใส่ในโปรเจค Java ของคุณและเหตุผลที่แต่ละการตั้งค่ามีความสำคัญ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR ในโปรเจค Maven หรือ Gradle.  
- กระบวนการขั้นตอน‑ต่อ‑ขั้นตอนเพื่อ **recognize image text** บน GPU.  
- เหตุผลที่การกำหนดจำนวน GPU streams สามารถเพิ่มอัตราการทำงาน.  
- วิธีตรวจสอบผลลัพธ์และแก้ไขปัญหาที่พบบ่อย.  

> **Prerequisites** – Java 17 (หรือใหม่กว่า), GPU ที่รองรับ CUDA พร้อมไดรเวอร์ล่าสุด, และใบอนุญาต Aspose OCR for Java ที่ถูกต้อง (การทดลองใช้ฟรีสำหรับการประเมิน). ไม่จำเป็นต้องใช้ไลบรารีภายนอกอื่นใด.

---

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR Dependency

ก่อนอื่น นำไลบรารี Aspose OCR เข้ามาในการสร้างของคุณ หากคุณใช้ **Maven** ให้เพิ่มโค้ดต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check Maven Central for the latest version -->
</dependency>
```

สำหรับ **Gradle** ให้วางโค้ดนี้ในไฟล์ `build.gradle` :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Pro tip:** เวอร์ชันล่าสุด (ณ มีนาคม 2026) มีการปรับปรุงประสิทธิภาพสำหรับงานที่ใช้ GPU, ดังนั้นควรดึงเวอร์ชันใหม่ที่สุดเสมอ

---

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine และเปิดใช้งาน GPU

การสร้าง OCR engine ทำได้ง่าย ส่วนสำคัญคือการเปิดใช้งานแฟล็ก GPU—หากไม่เปิด engine จะกลับไปใช้โหมด CPU

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // 3️⃣ (Optional) Set the number of GPU streams for parallel processing
        //    More streams can improve throughput on multi‑core GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);
```

### ทำไมต้องเปิด GPU?

เมื่อคุณเปิด `setUseGpu(true)` Aspose จะย้ายการคำนวณเครือข่ายประสาทเทียมที่หนักไปยังการ์ดกราฟิก ซึ่งสามารถลดเวลาในการประมวลผลของ **ocr large image** ลงเป็นวินาที โดยเฉพาะเมื่อภาพใหญ่กว่า 4000 × 4000 px หากสภาพแวดล้อมของคุณไม่มี GPU ที่รองรับ คำสั่งจะทำเป็น no‑op และ engine จะทำงานต่อบน CPU—ไม่มีการขัดข้อง เพียงแต่ช้าลง

---

## ขั้นตอนที่ 3: จดจำภาพ PNG และดึงข้อความออก

ตอนนี้ให้ชี้ engine ไปที่ไฟล์ที่ต้องการประมวลผล ตัวอย่างใช้ `sample-large.png` แต่คุณสามารถเปลี่ยนเป็น PNG หรือ JPEG ใดก็ได้

```java
        // 4️⃣ Perform OCR on the input image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // 5️⃣ Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

เมื่อคุณรันโปรแกรม คุณควรเห็นผลลัพธ์ประมาณนี้:

```
=== Recognized Text ===
Invoice #12345
Date: 2026‑03‑27
Total: $1,234.56
...
```

ผลลัพธ์นั้นยืนยันว่าการทำงาน **recognize image text** สำเร็จและคุณได้ **extract text png** เนื้อหาอย่างสำเร็จ

---

## ขั้นตอนที่ 4: ตรวจสอบการใช้ GPU (ทางเลือกแต่เป็นประโยชน์)

หากคุณอยากรู้ว่า GPU ถูกใช้จริงหรือไม่ ให้เปิดเครื่องมือมอนิเตอร์ GPU ของระบบ (เช่น `nvidia-smi` บน Linux) ขณะกระบวนการ Java ทำงาน คุณควรเห็นการเพิ่มขึ้นเล็กน้อยของการใช้หน่วยความจำและการคำนวณ

```bash
$ nvidia-smi
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   PID   Type   Process name                  GPU Memory               |
|  0    12345 C++    java                           1024MiB                  |
+-----------------------------------------------------------------------------+
```

หากคุณไม่เห็นกิจกรรมใด ๆ ตรวจสอบอีกครั้งว่า:

1. ไดรเวอร์ CUDA ตรงกับรุ่น GPU.  
2. การเรียก `setUseGpu(true)` ไม่ถูกเขียนทับในโค้ดต่อมา.  
3. ไฟล์ใบอนุญาตของคุณ (หากมี) ไม่ได้จำกัดการใช้ GPU.

---

## ขั้นตอนที่ 5: จัดการกรณีขอบที่พบบ่อย

### ภาพขนาดใหญ่เกินหน่วยความจำ GPU

เมื่อภาพมีขนาดมหาศาล (เช่น 8000 × 8000 px) GPU อาจหมดหน่วยความจำ วิธีแก้เร็วคือปรับขนาดภาพให้เล็กลงก่อนส่งให้ Aspose:

```java
import java.awt.image.BufferedImage;
import javax.imageio.ImageIO;
import java.io.File;

BufferedImage original = ImageIO.read(new File("sample-large.png"));
int maxDim = 4000; // target max dimension
int width = original.getWidth();
int height = original.getHeight();

float scale = Math.min((float)maxDim / width, (float)maxDim / height);
int newWidth = Math.round(width * scale);
int newHeight = Math.round(height * scale);

BufferedImage resized = new BufferedImage(newWidth, newHeight, original.getType());
// Simple scaling (for demo purposes)
resized.getGraphics().drawImage(original, 0, 0, newWidth, newHeight, null);
ImageIO.write(resized, "png", new File("sample-resized.png"));
```

จากนั้นส่ง `"sample-resized.png"` ไปยัง `recognizeImage` วิธีนี้ทำให้ OCR ยังคงความแม่นยำในขณะที่อยู่ในขอบเขตของ GPU

### PDF หลายหน้า

Aspose OCR ยังสามารถจัดการ PDF หน้า‑ต่อ‑หน้าได้ วนลูปแต่ละหน้า แปลงเป็นภาพ แล้วส่งให้ engine แฟล็ก **use gpu acceleration** เดียวกันทำงาน ให้คุณได้ pipeline PDF‑to‑text ที่เร็ว

---

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นคลาส Java ที่สมบูรณ์ พร้อมคอมไพล์และรัน แทนที่ `YOUR_DIRECTORY` ด้วยพาธไปยังไฟล์ PNG ของคุณ

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable GPU acceleration (requires a CUDA‑enabled GPU and driver)
        ocrEngine.getRecognitionSettings().setUseGpu(true);

        // Step 3: (Optional) Set the number of GPU streams for parallel processing
        // Using 2 streams works well on most modern GPUs.
        ocrEngine.getRecognitionSettings().setGpuStreams(2);

        // Step 4: Perform OCR on the input image
        // This will **recognize image text** from a PNG file.
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/sample-large.png");

        // Step 5: Print the recognized text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Expected output** – การแสดงผลเป็นข้อความธรรมดาที่แสดงทุกอย่างที่ engine สามารถอ่านจากภาพได้ หากภาพมีตาราง คุณจะได้เนื้อหาเซลล์ต่อเนื่องด้วยการขึ้นบรรทัด; Aspose ไม่รักษาเลย์เอาต์ แต่คุณสามารถประมวลผลต่อได้หากต้องการ

---

## คำถามที่พบบ่อย

| คำถาม | คำตอบ |
|----------|--------|
| **ต้องการใบอนุญาตแบบชำระเงินหรือไม่?** | การทดลองใช้ทำงานได้สูงสุด 200 หน้าและปิดการแสดงลายน้ำสำหรับ OCR. สำหรับการใช้งานจริง ใบอนุญาตจะลบข้อจำกัดและเปิดใช้งานสแตก GPU เต็มรูปแบบ |
| **GPU ของฉันเก่า (เช่น GTX 750) จะทำอย่างไร?** | GPU รุ่นเก่ายังอาจทำงานได้แต่ความเร็วจะลดลง; ตรวจสอบว่าคุณมี Compute Capability 3.0 อย่างน้อย |
| **ฉันสามารถประมวลผลไฟล์ JPG หรือ BMP ได้หรือไม่?** | ได้เลย—`recognizeImage` รองรับรูปแบบใดก็ได้ที่ Java ImageIO รองรับ |
| **มีวิธีประมวลผลหลายภาพพร้อมกันเป็นชุดหรือไม่?** | ใส่การเรียก OCR ในลูป และพิจารณาเพิ่มค่า `setGpuStreams` ให้ตรงกับจำนวนสตรีมพร้อมกันที่คุณต้องการ |
| **ถ้าฉันต้องการรักษาเลย์เอาต์จะทำอย่างไร?** | ใช้ `LayoutOptions` ของ Aspose OCR เพื่อรับ bounding boxes; สิ่งนี้อยู่นอกขอบเขตของคู่มือสั้นนี้แต่มีการอธิบายใน API |

---

## สรุป

ตอนนี้คุณมี **java ocr example** ที่กระชับและครบวงจร ซึ่ง **recognize image text**, **extract text png**, และ **use GPU acceleration** เพื่อเร่งการประมวลผลของ **ocr large image**. โดยการปรับจำนวน GPU stream และหากจำเป็นให้ลดขนาดภาพที่ใหญ่เกินไป คุณสามารถปรับโซลูชันให้เหมาะกับการกำหนดฮาร์ดแวร์ใด ๆ  

พร้อมสำหรับขั้นตอนต่อไปหรือยัง? ลองป้อนโฟลเดอร์ของใบเสร็จสแกนเข้าไปใน pipeline เดียวกัน หรือทดลองใช้ `TextRegion` API ของ Aspose เพื่อรักษาเลย์เอาต์เดิมไว้ หากเจอปัญหาใด ๆ ฟอรั่มของ Aspose และ Javadoc เป็นแหล่งข้อมูลที่ดี—แค่จำพื้นฐานที่เราอธิบายไว้ที่นี่  

ขอให้เขียนโค้ดอย่างสนุกสนานและ OCR ของคุณเร็วเหมือนสายฟ้า!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}