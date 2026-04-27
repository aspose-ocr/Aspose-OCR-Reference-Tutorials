---
category: general
date: 2026-04-26
description: เรียนรู้วิธีจดจำข้อความจากภาพโดยใช้ Aspose OCR พร้อมการเร่งความเร็วด้วย
  GPU ใน Java รวมถึงการตั้งค่าขีดจำกัดหน่วยความจำ GPU และขั้นตอนการโหลดภาพสำหรับ OCR.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: th
og_description: ค้นพบวิธีการจดจำข้อความจากภาพอย่างรวดเร็วด้วย Aspose OCR ที่เร่งด้วย
  GPU ใน Java คู่มือแบบขั้นตอนพร้อมการตั้งค่าขีดจำกัดหน่วยความจำ GPU และการโหลดภาพสำหรับ
  OCR.
og_title: แยกข้อความจากภาพด้วย GPU Aspose OCR (Java)
tags:
- OCR
- Java
- GPU
- Aspose
title: แยกข้อความจากภาพด้วย GPU Aspose OCR (Java)
url: /th/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพด้วย GPU Aspose OCR (Java)

เคยต้อง **จดจำข้อความจากภาพ** อย่างรวดเร็วบนแบ็กเอนด์ Java หรือไม่? ด้วยการเร่งความเร็วด้วย GPU ของ Aspose OCR คุณจะลดเวลาในการสแกนลงเป็นวินาที—ไม่ต้องรอให้ CPU ทำงานกับเมกะไบต์ของพิกเซลอีกต่อไป ในบทแนะนำนี้เราจะสาธิตการเปิดใช้งาน GPU, ตั้งค่าขีดจำกัดหน่วยความจำ GPU (ถ้าต้องการ) และสุดท้าย **โหลดภาพสำหรับ OCR** เพื่อให้คุณได้สตริงข้อความที่สะอาดในไม่กี่บรรทัดของโค้ด

เราจะครอบคลุมทุกอย่างที่คุณต้องการเพื่อรันเดโมบนการ์ดที่รองรับ CUDA, อธิบายว่าการตั้งค่าแต่ละอย่างสำคัญอย่างไร, และแสดงตัวอย่างที่พร้อมรันครบถ้วน เมื่อจบคุณจะสามารถนำ OCR ที่เร่งด้วย GPU ไปใส่ในบริการ Java ใดก็ได้ ไม่ว่าจะเป็น pipeline การนำเข้าหนังสือเอกสารหรือแบ็กเอนด์โมบายแบบเรียลไทม์

## สิ่งที่คุณต้องมี

- **Java 17** หรือใหม่กว่า (Aspose OCR JAR รองรับ JVM สมัยใหม่)  
- **GPU ที่รองรับ CUDA** ที่มี VRAM อย่างน้อย 2 GB (เดโมจำกัดการใช้ที่ 1024 MB)  
- ไลบรารี **Aspose.OCR for Java** (ดาวน์โหลดจากเว็บไซต์ Aspose หรือดึงจาก Maven)  
- ไฟล์ภาพที่คุณต้องการประมวลผล – แนะนำให้เป็นสแกนหรือรูปถ่ายความละเอียดสูง  

ไม่มีบริการภายนอก, ไม่มีคีย์คลาวด์, เพียงการติดตั้งแบบโลคัล หากคุณยังไม่มี GPU, คุณยังสามารถรันโค้ดได้; คำสั่ง `setUseGpu(true)` จะถอยกลับไปใช้ CPU โดยอัตโนมัติ

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ไปยังโปรเจกต์และจดจำข้อความจากภาพ

แรกสุด, ตรวจสอบให้แน่ใจว่า Aspose OCR JAR อยู่ใน classpath ของคุณ หากใช้ Maven ให้เพิ่ม:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

เมื่อไลบรารีพร้อมใช้งาน, สร้างอินสแตนซ์ `OcrEngine` ซึ่งเป็นจุดเริ่มต้นสำหรับการ **จดจำข้อความจากภาพ**  

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

ทำไมต้องสร้าง `OcrEngine` ก่อน? เพราะอ็อบเจ็กต์นี้เก็บการตั้งค่าการจดจำทั้งหมด (แฟล็ก GPU, แพ็คภาษาต่าง ๆ ฯลฯ) และแยกแต่ละการสแกนออกจากกัน ทำให้คุณสามารถใช้เอนจินเดียวกันหลายภาพโดยไม่เกิดการรั่วของหน่วยความจำ

## ขั้นตอนที่ 2: เปิดใช้งานการเร่งความเร็วด้วย GPU และ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** (ถ้าต้องการ)

การเร่งความเร็วด้วย GPU คือส่วนสำคัญที่ทำให้ OCR ขนาดใหญ่เป็นไปได้ Aspose ให้คุณสลับการใช้งานด้วยคำสั่งเดียว:

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

หาก GPU ของคุณแชร์กับงานอื่น ๆ คุณอาจต้องจำกัดจำนวน VRAM ที่เอนจินสามารถใช้ได้ นั่นคือจุดที่ **ตั้งค่าขีดจำกัดหน่วยความจำ GPU** เข้ามาช่วย:

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

การกำหนดขีดจำกัดหน่วยความจำช่วยป้องกันการพังจาก out‑of‑memory เมื่อประมวลผลภาพความละเอียดสูงหลายภาพพร้อมกัน ค่าเป็นเมกะไบต์, ดังนั้น `1024` หมายถึง “ใช้ VRAM ไม่เกิน 1 GB”

> **เคล็ดลับ:** บนการ์ด 4 GB, ขีดจำกัด 2 GB มักเป็นจุดที่ปลอดภัย; คุณสามารถทดลองเพิ่มค่าได้หากพบว่า GPU ยังไม่ได้ทำงานเต็มที่

## ขั้นตอนที่ 3: **โหลดภาพสำหรับ OCR** – ชี้เอนจินไปที่ไฟล์ของคุณ

ตอนนี้เอนจินพร้อมแล้ว, เราต้องบอกว่าต้องสแกนภาพใด Aspose รองรับเส้นทางไฟล์, `java.io.File`, หรือแม้แต่ `java.awt.image.BufferedImage` สำหรับความง่าย เราจะใช้เส้นทางไฟล์:

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

แทนที่ `YOUR_DIRECTORY/high_res_photo.jpg` ด้วยตำแหน่งจริงของภาพทดสอบของคุณ หากภาพอยู่ในโฟลเดอร์ resources คุณสามารถใช้ `getClass().getResource("/images/sample.png").getPath()` แทนได้

ทำไมการโหลดจึงสำคัญ? เอนจินทำขั้นตอนการเตรียมล่วงหน้า (deskew, binarization) ที่พึ่งพา GPU อย่างมาก การให้ไฟล์ที่สะอาดและความละเอียดสูงทำให้ GPU ทำงานได้อย่างมีประสิทธิภาพและเพิ่มความแม่นยำของการ **จดจำข้อความจากภาพ**

## ขั้นตอนที่ 4: รันการจดจำและดึงสตริงที่สกัดออกมา

เมื่อเปิด GPU แล้วและโหลดภาพแล้ว, คำสั่งสุดท้ายเป็นเรื่องง่าย:

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

เมธอด `recognize()` จะบล็อกจนกว่า GPU จะทำงานเสร็จ, จากนั้น `getText()` จะคืนค่า `String` ธรรมดา ภายใต้การทำงาน Aspose ใช้โมเดล deep‑learning ที่รันบนคอร์ CUDA, ดังนั้นความหน่วงจึงเป็นส่วนเล็กของที่ OCR บน CPU เพียงอย่างเดียวต้องใช้

## ขั้นตอนที่ 5: แสดงผลลัพธ์

พิมพ์ผลลัพธ์ OCR ไปที่คอนโซลเพื่อให้คุณตรวจสอบได้:

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

หากทุกอย่างเชื่อมต่ออย่างถูกต้อง คุณจะเห็นข้อความที่ถอดออกมาปรากฏทันที บน RTX 2060 ระดับกลาง, ภาพ 3000 × 2000 px จะประมวลผลภายในไม่ถึงหนึ่งวินาที

![จดจำข้อความจากภาพด้วย GPU Aspose OCR](/images/gpu-ocr-demo.png "เดโม OCR ที่เร่งด้วย GPU")

*ข้อความอธิบายภาพ:* **จดจำข้อความจากภาพ** – ภาพหน้าจอของผลลัพธ์คอนโซลหลังจากทำ OCR ด้วย GPU

## ผลลัพธ์ที่คาดหวัง

รันโปรแกรมเต็มรูปแบบกับใบเสร็จตัวอย่างจะได้ผลลัพธ์ประมาณนี้:

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

ข้อความจริงของคุณอาจแตกต่างกันตามภาพต้นฉบับ, แต่รูปแบบข้างต้นแสดงให้เห็นว่าเอนจินสามารถสกัดบรรทัดและตัวเลขได้อย่างถูกต้อง

## ปัญหาที่พบบ่อย & เคล็ดลับปฏิบัติ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **GPU ไม่ถูกตรวจจับ** | ไดรเวอร์ CUDA หายไปหรือเวอร์ชัน JAR ไม่เข้ากัน | ติดตั้งไดรเวอร์ NVIDIA ล่าสุด, ตรวจสอบว่า `nvidia-smi` ทำงาน, และใช้ Aspose OCR 23.12 หรือใหม่กว่า |
| **ข้อผิดพลาด out‑of‑memory** | ภาพใหญ่เกินขีดจำกัด VRAM ที่ตั้งไว้ | เพิ่มค่า `setGpuMemoryLimit` หรือย่อขนาดภาพก่อนโหลด |
| **อักขระแปลก** | ภาพเบลอหรือคอนทราสต์ต่ำ | ทำการพรี‑โปรเซสด้วย `ocrEngine.getPreprocessingSettings().setBinarization(true)` |
| **ประสิทธิภาพช้าในรอบแรก** | ค่าเริ่มต้นของคอนเท็กซ์ GPU ใช้เวลา | ทำการวอร์ม‑อัพเอนจินโดยประมวลผลภาพ dummy ขนาดเล็กก่อนงานจริง |

จำไว้ว่า **set gpu memory limit** เป็นตัวเลือกเสริมแต่

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}