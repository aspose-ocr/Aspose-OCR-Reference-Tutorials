---
category: general
date: 2026-03-18
description: วิธีแก้ไขการเอียงของภาพอย่างรวดเร็วด้วย Aspose OCR Java. เรียนรู้การเตรียมภาพล่วงหน้าสำหรับ
  OCR ทำความสะอาดภาพสแกนและปรับปรุงความแม่นยำของ OCR เพียงไม่กี่ขั้นตอน.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: th
og_description: วิธีแก้ไขการเอียงของภาพด้วย Aspose OCR Java, เตรียมภาพล่วงหน้าสำหรับ
  OCR, ทำความสะอาดภาพสแกนและปรับปรุงความแม่นยำของ OCR.
og_title: วิธีแก้เอียงภาพสำหรับ OCR – คู่มือ Java
tags:
- OCR
- Java
- Image Processing
title: วิธีปรับแนวภาพสำหรับ OCR – คู่มือการเตรียมภาพด้วย Java
url: /th/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีแก้ไขการเอียงของภาพสำหรับ OCR – คู่มือการเตรียมภาพด้วย Java

เคยสงสัยไหมว่า **how to deskew image** ไฟล์ที่สแกนออกมามีมุมแปลก ๆ? คุณไม่ได้เป็นคนเดียว—นักพัฒนาหลายคนเจอปัญหานี้เมื่อต้องดึงข้อความจากเอกสารที่มีภาพเป็นส่วนใหญ่ ข่าวดีคือ ด้วยเพียงไม่กี่บรรทัดของ Java และ Aspose OCR คุณก็สามารถทำให้ภาพตรง, ลดสัญญาณรบกวน, และดึงข้อความที่สะอาดได้โดยไม่ต้องเสียแรงมาก

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนทั้งหมด: โหลดสแกนที่มีสัญญาณรบกวนและหมุน, ใช้ฟิลเตอร์ deskew, ลบความยุ่งเหยิงทางภาพ, และสุดท้าย **extract text from image**. เมื่อจบคุณจะรู้วิธี **preprocess image for OCR**, **clean scanned image** files, และ **improve OCR accuracy** สำหรับโครงการใด ๆ ที่ต้องการการสกัดข้อความที่เชื่อถือได้

## สิ่งที่คุณต้องเตรียม

- Java 17 (หรือ JDK เวอร์ชันใหม่) – โค้ดใช้คุณสมบัติมาตรฐานของภาษา
- Aspose OCR for Java library (เวอร์ชันทดลองฟรีใช้งานได้สำหรับการทดลอง)
- ตัวอย่างภาพที่มีสัญญาณรบกวนและหมุน (เช่น `noisy-rotated.png`)
- IDE ที่คุณชอบ (IntelliJ IDEA, Eclipse, VS Code…) – สิ่งใดก็ได้ที่สามารถคอมไพล์ Java

ไม่ต้องใช้เฟรมเวิร์กเพิ่มเติม, ไม่ต้องใช้ Maven/Gradle พิเศษ; เพียงแค่ import ตามที่แสดงด้านล่าง

---

## วิธี Deskew Image ด้วย Aspose OCR

สิ่งแรกที่ต้องจัดการคือการเอียงของภาพ หากบรรทัดข้อความไม่เป็นแนวนอน OCR จะอ่านตัวอักษรผิด `DeskewFilter` จะทำหน้าที่หลักนี้ให้

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **ทำไมเรื่องนี้สำคัญ:** `DeskewFilter` วิเคราะห์รูปทรงของภาพ, ประเมินมุมการหมุน, และหมุนบิตแมพกลับสู่แนวระดับ. หากข้ามขั้นตอนนี้ OCR ส่วนใหญ่จะมองอักษรที่เอียงเป็น glyph ที่แตกต่างกัน ทำให้ความพยายาม **improve OCR accuracy** ตกลงไปในหลุมดำ

> **เคล็ดลับ:** หากต้องจัดการกับเอกสารที่อาจกลับหัว, เปิดฟลัก `setAutoRotate` บน `DeskewFilter` (พร้อมใช้งานในเวอร์ชันใหม่ของ Aspose). มันจะพลิก 180° อัตโนมัติเมื่อจำเป็น

![Diagram showing before and after rotation – how to deskew image](https://example.com/deskew-diagram.png "how to deskew image example")

*Image alt text: how to deskew image example*

---

## Preprocess Image for OCR – การลดสัญญาณรบกวนและทำความสะอาด

เมื่อภาพตรงแล้วอุปสรรคต่อไปคือสัญญาณรบกวน—จุด speckles, artifacts จากการบีบอัด, หรือแพทเทิร์นพื้นหลังที่ทำให้ OCR สับสน `DenoiseFilter` ใช้อัลกอริทึมการลบรอยเบา ๆ ที่รักษาขอบ (ตัวอักษร) ไว้ขณะลบเม็ดฝุ่น

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### เมื่อใดควรปรับค่าการลดสัญญาณรบกวน

- **Very dark scans:** เพิ่มความแรงของฟิลเตอร์ (`denoiseFilter.setStrength(2)`) เพื่อขจัดเงาพื้นหลัง
- **Fine‑print fonts:** ลดความแรงเพื่อหลีกเลี่ยงการเบลอ serif เล็ก ๆ
- **Colored documents:** แปลงเป็น grayscale ก่อน (`scannedImage = scannedImage.toGrayscale();`)—OCR ทำงานดีที่สุดกับภาพช่องเดียว

การปรับเหล่านี้เป็นส่วนหนึ่งของแนวทาง **clean scanned image**; bitmap ที่สะอาดยิ่งทำให้คะแนนความเชื่อมั่นจาก OCR สูงขึ้น

---

## Extract Text from Image – การรัน OCR Engine

ตอนนี้ภาพตรงและเงียบแล้ว, ถึงเวลาที่จะ **extract text from image**. คลาส `OcrEngine` ดูแลทุกอย่างเบื้องหลัง: segmentation, การจำแนกตัวอักษร, และการสร้างโมเดลภาษา

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### ผลลัพธ์ที่คาดหวัง

หากไฟล์ต้นฉบับของคุณมีบรรทัด “**Invoice # 12345**”, คอนโซลควรพิมพ์ประมาณนี้:

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

หากผลลัพธ์ดูเป็นอักษรผสม, ตรวจสอบขั้นตอนก่อนหน้า—โดยเฉพาะการ deskew. แม้การเอียงเพียง 1° ก็อาจทำให้ตัวเลขและสัญลักษณ์ผิดพลาดได้

---

## ปัญหาที่พบบ่อย & เคล็ดลับเพื่อ **Improve OCR Accuracy**

| Issue | Why it hurts accuracy | Quick fix |
|-------|----------------------|-----------|
| **Residual rotation** | OCR คาดหวังบรรทัดฐานแนวนอน | ตรวจสอบด้วย `deskewFilter.getAngle()` และบันทึกค่าที่ได้ |
| **Over‑denoising** | ทำให้เส้นบาง ๆ เบลอ, ทำให้ “i” กลายเป็น “l” | ใช้ `setStrength(0.5)` สำหรับฟอนต์ที่ละเอียด |
| **Wrong image format** | การบีบอัด JPEG เพิ่ม artifacts | แนะนำให้ใช้ PNG หรือ TIFF เพื่อเก็บแบบ lossless |
| **Incorrect language** | Engine ตั้งค่าเป็น English เริ่มต้น; อักษรอื่นต้องกำหนด | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **Low DPI (≤150)** | พิกเซลไม่พอสำหรับ segmentation ที่เชื่อถือได้ | รีแซมพล์เป็น 300 DPI ก่อนประมวลผล (`scannedImage = scannedImage.resample(300);`) |

### โบนัส: การประมวลผลแบบกลุ่ม

หากคุณมีโฟลเดอร์ของสแกน, ห่อโค้ดตัวอย่างในลูป:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

รูปแบบนี้ทำให้คุณ **preprocess image for OCR** ได้ในระดับใหญ่, รักษาโค้ดให้เป็นระเบียบและประสิทธิภาพคาดเดาได้

---

## สรุป & ขั้นตอนต่อไป

เราได้ครอบคลุม **how to deskew image**, **preprocess image for OCR**, และสุดท้าย **extract text from image** ด้วย Aspose OCR Java. ด้วยการทำให้สแกนตรง, ทำความสะอาดสัญญาณรบกวน, และส่งบิตแมพที่บริสุทธิ์ให้กับ engine, คุณจะเห็นการ **improve OCR accuracy** อย่างชัดเจนในทุกโครงการ

ต่อไปคุณอาจพิจารณา:

- **Language detection** – สลับ `ocrEngine.setLanguage` ตามสคริปต์ที่ตรวจพบ
- **PDF output** – ส่งข้อความที่รู้จำเข้าไปในตัวสร้าง PDF เพื่อสร้างเอกสารที่ค้นหาได้
- **Machine‑learning post‑processing** – รัน spell‑check หรือพจนานุกรมกำหนดเองบนผลลัพธ์ OCR

ลองไอเดียเหล่านี้, ทดลองปรับความแรงของฟิลเตอร์ต่าง ๆ, แล้วคุณจะมี pipeline ที่แข็งแกร่งสำหรับโครงการดิจิไทเซชันเอกสารใดก็ได้

---

*Happy coding! If you hit a snag, drop a comment below—I'll help you fine‑tune the deskew and denoise parameters.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}