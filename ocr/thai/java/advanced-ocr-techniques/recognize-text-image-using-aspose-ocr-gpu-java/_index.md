---
category: general
date: 2026-02-17
description: จดจำข้อความจากภาพอย่างรวดเร็วด้วย Aspose OCR ที่รองรับ GPU ใน Java. เรียนรู้การดึงข้อความจากภาพและตั้งค่า
  ID ของอุปกรณ์ GPU เพื่อประสิทธิภาพที่ดีที่สุด.
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: th
og_description: จดจำข้อความในภาพอย่างรวดเร็วด้วย Aspose OCR ที่รองรับ GPU ใน Java
  คู่มือนี้แสดงวิธีดึงข้อความจากภาพและตั้งค่า ID ของอุปกรณ์ GPU.
og_title: จดจำข้อความในภาพโดยใช้ Aspose OCR GPU – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: จดจำข้อความจากภาพโดยใช้ Aspose OCR GPU – Java
url: /th/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพด้วย Aspose OCR GPU – Java

เคยต้อง **จดจำข้อความจากภาพ** ในแอปพลิเคชัน Java แต่ CPU ทำงานช้าเมื่อต้องจัดการไฟล์ขนาดใหญ่หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอปัญหาเดียวกันเมื่อต้องประมวลผลสแกนความละเอียดสูง ข่าวดีคือ Aspose OCR ให้คุณ **ดึงข้อความจากภาพ** บน GPU ทำให้เวลาในการประมวลผลลดลงอย่างมาก  

ในบทเรียนนี้เราจะเดินผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบ ซึ่งจะแสดงวิธีตั้งค่าไลเซนส์, เปิดใช้งานการเร่งความเร็วด้วย GPU, และ **ตั้งค่า gpu device id** เมื่อคุณมีการ์ดกราฟิกหลายตัว สุดท้ายคุณจะได้โปรแกรมที่พิมพ์ข้อความที่จดจำได้ลงคอนโซล—ไม่มีขั้นตอนเพิ่มเติมใด ๆ

## สิ่งที่คุณต้องเตรียม

- **Java 17** หรือใหม่กว่า (API รองรับ Java 8+ แต่ LTS ล่าสุดให้ประสิทธิภาพดีกว่า)  
- ไลบรารี **Aspose OCR for Java** (ดาวน์โหลดไฟล์ JAR จากเว็บไซต์ Aspose)  
- ไฟล์ไลเซนส์ **Aspose OCR** ที่ถูกต้อง (`Aspose.OCR.lic`) เวอร์ชันทดลองใช้ได้ แต่ฟีเจอร์ GPU จะต้องมีไลเซนส์เต็ม  
- ไฟล์ภาพ (`sample-image.png`) ที่มีข้อความอ่านได้ชัดเจน  
- สภาพแวดล้อมที่รองรับ GPU (การ์ด NVIDIA ที่เข้ากันได้กับ CUDA จะดีที่สุด)  

หากคุณไม่คุ้นเคยกับข้อใดข้อหนึ่ง ไม่ต้องกังวล—แต่ละหัวข้อจะอธิบายต่อไป

## ขั้นตอนที่ 1: เพิ่ม Aspose OCR ลงในโปรเจกต์ของคุณ

แรกสุดให้ใส่ไฟล์ JAR ของ Aspose OCR ลงใน classpath หากใช้ Maven ให้เพิ่ม dependency ต่อไปนี้ใน `pom.xml`:

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

หากคุณชอบวิธีแมนนวล ให้วาง JAR ลงในโฟลเดอร์ `libs/` แล้วเพิ่มเข้าไปใน module path ของ IDE

> **เคล็ดลับ:** ควรทำให้หมายเลขเวอร์ชันตรงกับบันทึกการปล่อยของไลบรารี; เวอร์ชันใหม่มักมีการปรับปรุงประสิทธิภาพสำหรับการประมวลผลด้วย GPU

## ขั้นตอนที่ 2: โหลดไลเซนส์ Aspose OCR (จำเป็นสำหรับการใช้ GPU)

หากไม่มีไลเซนส์ การเรียก `setEnableGpu(true)` จะกลับไปใช้โหมด CPU อย่างเงียบ ๆ โหลดไลเซนส์ตั้งแต่เริ่มต้นเมธอด `main`:

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธเต็มหรือพาธสัมพันธ์ที่คุณเก็บไฟล์ `.lic` หากพาธผิด Aspose จะโยน `FileNotFoundException` ตรวจสอบการสะกดให้ถูกต้อง

## ขั้นตอนที่ 3: สร้าง OCR engine และเปิดการเร่งความเร็วด้วย GPU

ตอนนี้เราจะสร้างอ็อบเจ็กต์ `OcrEngine` และบอกให้ใช้ GPU เมธอด `setGpuDeviceId` ช่วยให้คุณเลือกการ์ดเฉพาะเมื่อมีมากกว่าหนึ่งตัว

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

ทำไมต้องระบุ device ID? ในเซิร์ฟเวอร์ที่มีหลาย GPU คุณอาจจองการ์ดหนึ่งสำหรับการเตรียมภาพและอีกการ์ดหนึ่งสำหรับ OCR การตั้งค่า ID จะทำให้ฮาร์ดแวร์ที่ถูกต้องทำงานหนักแทน

## ขั้นตอนที่ 4: เตรียมภาพอินพุต

Aspose OCR รองรับหลายรูปแบบ (PNG, JPG, BMP, TIFF) ให้ห่อไฟล์ของคุณในอ็อบเจ็กต์ `OcrInput`:

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

หากต้องการประมวลผลจากสตรีม (เช่นไฟล์ที่อัปโหลด) ให้ใช้ `ocrInput.add(InputStream)` แทน

## ขั้นตอนที่ 5: รันกระบวนการจดจำและดึงผลลัพธ์

เมธอด `recognize` จะคืนค่า `OcrResult` ซึ่งบรรจุข้อความธรรมดา, คะแนนความมั่นใจ, และข้อมูลเลย์เอาต์หากต้องการ

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

หากภาพเบลอหรือภาษาที่ใช้ไม่รองรับ ผลลัพธ์อาจเป็นค่าว่าง ในกรณีนั้นตรวจสอบค่า `ocrResult.getConfidence()` (0‑100) เพื่อพิจารณาว่าจะทำการประมวลผลใหม่ด้วยการเตรียมภาพหรือไม่

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

> **ผลลัพธ์ที่คาดหวัง:** คอนโซลพิมพ์ข้อความที่ปรากฏใน `sample-image.png` อย่างตรงไปตรงมา หาก GPU ทำงานอยู่ คุณจะสังเกตเห็นเวลาในการประมวลผลลดจากหลายวินาที (CPU) เหลือน้อยกว่า 1 วินาทีสำหรับสแกน 300 dpi ปกติ

## คำถามที่พบบ่อยและกรณีขอบ

### ทำงานได้บนเซิร์ฟเวอร์แบบ headless หรือไม่?

ได้ครับ ต้องติดตั้งไดรเวอร์ GPU แต่ไม่จำเป็นต้องมีจอแสดงผล เพียงตรวจสอบให้ `CUDA` toolkit (หรือเทียบเท่าสำหรับ GPU ของคุณ) อยู่ใน `PATH` ของระบบ

### ถ้ามี GPU มากกว่าหนึ่งตัวและต้องการใช้ GPU 1 จะทำอย่างไร?

เปลี่ยนค่า device ID:

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### จะดึงข้อความจากภาพในภาษาต่าง ๆ อย่างไร?

ตั้งค่าภาษาให้กับ engine ก่อนเรียก `recognize`:

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose รองรับมากกว่า 30 ภาษา; ดูเอกสาร API เพื่อดูรายการเต็ม

### หากภาพมีหลายหน้า (เช่น PDF ที่แปลงเป็นภาพ) จะทำอย่างไร?

สร้างรายการ `OcrInput` แยกแต่ละหน้า หรือวนลูปไฟล์:

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

Engine จะต่อผลลัพธ์ตามลำดับหน้า

### จะจัดการกับผลลัพธ์ที่ความมั่นใจต่ำอย่างไร?

ตรวจสอบคะแนนความมั่นใจ:

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

ขั้นตอนเตรียมภาพทั่วไป ได้แก่ การทำไบนารีเซชัน, ลดสัญญาณรบกวน, หรือปรับขนาดเป็น 300 dpi

## เคล็ดลับเพื่อประสิทธิภาพ

- **ประมวลผลเป็นชุด:** เพิ่มหลายภาพลงใน `OcrInput` เดียวจะลดค่าโอเวอร์เฮดจากการเริ่มต้นบริบท GPU ซ้ำหลายครั้ง  
- **อุ่นเครื่อง:** รันการจดจำเทียมหนึ่งครั้งหลังจากเปิด JVM; การเรียกครั้งแรกจะใช้เวลาตั้งค่าไดรเวอร์  
- **การจัดการหน่วยความจำ:** ทำลายอ็อบเจ็กต์ `OcrInput` ขนาดใหญ่ (`ocrInput.clear()`) หลังใช้งานเพื่อคืนหน่วยความจำ GPU  

## สรุป

ตอนนี้คุณรู้วิธี **จดจำข้อความจากภาพ** อย่างมีประสิทธิภาพด้วยเอ็นจิ้น GPU ของ Aspose OCR ใน Java, วิธี **ดึงข้อความจากภาพ** ในภาษาที่รองรับ, และวิธี **ตั้งค่า gpu device id** เมื่อทำงานกับการ์ดกราฟิกหลายตัว โค้ดที่สามารถรันได้เต็มรูปแบบข้างต้นควรทำงานได้ทันที—เพียงเปลี่ยนไลเซนส์และพาธภาพของคุณ

พร้อมก้าวต่อไปหรือยัง? ลองประมวลผลโฟลเดอร์ของ PDF ที่สแกน, ทดลองตัวเลือก `setLanguage` ต่าง ๆ, หรือผสาน OCR กับโมเดลแมชชีนเลิร์นนิงเพื่อทำ post‑processing ความเป็นไปได้ไม่มีที่สิ้นสุดและการเร่งความเร็วด้วย GPU ทำให้โครงการขนาดใหญ่เป็นเรื่องทำได้

ขอให้เขียนโค้ดสนุกนะครับ และอย่าลังเลที่จะคอมเมนต์หากเจออุปสรรคใด ๆ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}