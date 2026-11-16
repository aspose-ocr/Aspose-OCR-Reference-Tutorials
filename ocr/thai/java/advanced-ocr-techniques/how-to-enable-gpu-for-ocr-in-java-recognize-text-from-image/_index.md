---
category: general
date: 2026-08-22
description: วิธีเปิดใช้งาน GPU ใน Java OCR เพื่อแยกข้อความจากรูปภาพอย่างรวดเร็ว เรียนรู้การดึงข้อความจากไฟล์
  PNG ตั้งค่าตัวเลือกภาพ และแยกข้อความอย่างมีประสิทธิภาพด้วย Aspose OCR.
draft: false
keywords:
- how to enable gpu
- recognize text image java
- aspose ocr java tutorial
- extract text from png
- set image options
lastmod: 2026-08-22
og_description: วิธีเปิดใช้งาน GPU ใน Java OCR เพื่อแยกข้อความจากรูปภาพอย่างรวดเร็ว
  คู่มือนี้จะแสดงวิธีดึงข้อความจากไฟล์ PNG ตั้งค่าตัวเลือกภาพ และแยกข้อความอย่างมีประสิทธิภาพด้วย
  Aspose OCR.
og_image_alt: Java OCR GPU example code snippet showing Aspose OCR usage
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – การดึงข้อความอย่างรวดเร็ว
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  headline: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  type: TechArticle
- description: How to enable GPU in Java OCR to recognize text from image quickly.
    Learn to extract text from PNG, set image options, and recognize text efficiently
    using Aspose OCR.
  name: How to Enable GPU for OCR in Java – Recognize Text from Image Fast
  steps:
  - name: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
    text: '**Low‑resolution scans (< 150 dpi).** Upscale first or ask the user for
      a higher‑resolution scan.'
  - name: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
    text: '**Handwritten notes.** The default model focuses on printed text; you’d
      need a custom trained model for cursive.'
  - name: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
    text: '**Multiple languages.** Pass a comma‑separated list to `RecognitionLanguage`,
      e.g., `RecognitionLanguage.ENGLISH_FRENCH`.'
  type: HowTo
- questions:
  - answer: Yes, the Aspose OCR trial includes full GPU support; you just need to
      enable it in code.
    question: Does the free trial support GPU acceleration?
  - answer: Aspose OCR can rasterize PDF pages internally, but for best performance
      convert to high‑resolution PNG first.
    question: Can I process PDFs directly without converting to images?
  - answer: CUDA 11.2 or newer is recommended; older versions may work but are not
      officially tested.
    question: What CUDA version is required?
  - answer: Validate file size and type before processing, and run the OCR in a sandboxed
      thread to mitigate risks.
    question: Is it safe to run OCR on untrusted user uploads?
  - answer: Set `ocrEngine.setDebugMode(true)`; the console will list the selected
      GPU device and memory statistics.
    question: How do I enable logging to verify GPU usage?
  type: FAQPage
tags:
- OCR
- Java
- GPU
title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – แยกข้อความจากรูปภาพอย่างรวดเร็ว
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – แยกข้อความจากรูปภาพอย่างรวดเร็ว

การเปิดใช้งานการเร่งความเร็วด้วย GPU ในแอปพลิเคชัน OCR ของ Java สามารถลดเวลาการประมวลผลได้อย่างมาก โดยเฉพาะเมื่อคุณต้องการดึงข้อความจากภาพขนาดใหญ่หรือชุดข้อมูลจำนวนมาก ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีเปิดใช้งาน GPU**, วิธี **แยกข้อความจากไฟล์รูปภาพ**, และขั้นตอนที่แน่นอนในการ **ดึงข้อความจาก PNG** ด้วยไลบรารี Aspose OCR เราจะพาคุณผ่านตัวเลือกการเตรียมภาพที่ช่วยเพิ่มความแม่นยำและตอบคำถาม “วิธีแยกข้อความ” ที่พบบ่อยระหว่างทาง

## คำตอบสั้น
- **อะไรคือการเพิ่มความเร็วที่มากที่สุด?** สูงสุด 5× เร็วกว่าเมื่อใช้ RTX 2060 ระดับกลางเมื่อเทียบกับ OCR ที่ใช้ CPU อย่างเดียว.  
- **ฉันต้องการใบอนุญาตพิเศษหรือไม่?** ใบอนุญาต Aspose OCR มาตรฐานทำงานกับ GPU; เพียงเปิดใช้งานแฟล็ก GPU.  
- **ต้องการเวอร์ชัน Java ใด?** แนะนำให้ใช้ Java 17 หรือใหม่กว่าเพื่อประสิทธิภาพที่ดีที่สุด.  
- **ฉันสามารถรันใน Docker ได้หรือไม่?** ใช่ – เพียงเพิ่มแฟล็ก `--gpus all` และติดตั้งไดรเวอร์ NVIDIA ในคอนเทนเนอร์.  
- **โค้ดนี้เข้ากันได้กับรูปแบบภาพอื่นหรือไม่?** API เดียวกันทำงานกับ JPEG, TIFF, BMP, และ PNG โดยไม่ต้องเปลี่ยนแปลง.

## สิ่งที่คุณต้องเตรียม

คุณต้องมีเครื่องที่เปิดใช้งาน GPU, ไลบรารี Aspose OCR for Java, และสภาพแวดล้อมการพัฒนา Java 17 (หรือใหม่กว่า) การตั้งค่าทั่วไปประกอบด้วย NVIDIA RTX 3060 หรือการ์ดที่รองรับ CUDA ใด ๆ, JAR ล่าสุดของ Aspose OCR จาก Maven Central, และไฟล์ PNG ตัวอย่างสำหรับการวัดประสิทธิภาพ

**คำตอบโดยตรง (40‑70 คำ):** เพื่อเริ่มต้นคุณต้องติดตั้ง Java 17, เพิ่มการพึ่งพา Aspose OCR ลงในโปรเจกต์, ตรวจสอบว่า JVM สามารถมองเห็นอุปกรณ์ CUDA อย่างน้อยหนึ่งตัว, และมีภาพทดสอบพร้อม เมื่อทำตามเงื่อนไขเหล่านี้แล้วคุณสามารถเปิดใช้งาน GPU ในเอนจิน OCR และเริ่มประมวลผลภาพด้วยความเร็วของ GPU

- **Java 17** (หรือใหม่กว่า) – โค้ดสามารถคอมไพล์กับเวอร์ชันก่อนหน้าได้ แต่ 17 ให้การสนับสนุน API ที่ดีที่สุด.  
- **Aspose OCR for Java** – ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์ Aspose หรือ Maven Central.  
- **GPU ที่รองรับ CUDA** – เช่น NVIDIA RTX 3060, RTX 2070 หรือการ์ดสมัยใหม่ใด ๆ ที่มีไดรเวอร์ที่เหมาะสม.  
- **ภาพทดสอบ** – ใบแจ้งหนี้ PNG ขนาดใหญ่ทำงานได้ดีสำหรับการวัดประสิทธิภาพ.

> **เคล็ดลับมืออาชีพ:** บนแล็ปท็อปที่มีกราฟิกแบบรวมและแบบแยก, บังคับให้ JVM ใช้ GPU แยกผ่านแผงควบคุมไดรเวอร์; มิฉะนั้นไลบรารีจะกลับไปใช้ CPU อย่างเงียบๆ.

![ตัวอย่างการเปิดใช้งาน GPU](image.png "ตัวอย่างการเปิดใช้งาน GPU")
[ตัวอย่างการเปิดใช้งาน GPU](image.png "ตัวอย่างการเปิดใช้งาน GPU")

*Alt text: ตัวอย่างการเปิดใช้งาน GPU แสดงโค้ด Java.*

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และตรวจสอบการพร้อมใช้งานของ GPU

GpuSettings คือคลาสที่ควบคุมการใช้ GPU สำหรับเครื่องมือ Aspose OCR

เพิ่มการพึ่งพา Maven (หรือวาง JAR ลงใน `libs/`):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

รันสคริปต์ตรวจสอบเพื่อแสดงอุปกรณ์ที่พร้อมใช้งาน:

```java
import com.aspose.ocr.GpuSettings;

public class GpuCheck {
    public static void main(String[] args) {
        GpuSettings settings = new GpuSettings();
        System.out.println("GPU enabled? " + settings.getEnable());
        System.out.println("Detected GPU count: " + settings.getDeviceCount());
    }
}
```

หากผลลัพธ์แสดงจำนวนอุปกรณ์ที่ไม่เป็นศูนย์ JVM ของคุณจะเห็น GPU หากแสดงศูนย์ให้ตรวจสอบการติดตั้งไดรเวอร์และตัวแปรสภาพแวดล้อม `CUDA_PATH`.

## ขั้นตอนที่ 2 – วิธีเปิดใช้งาน GPU ใน Aspose OCR

**คำตอบโดยตรง (40‑70 คำ):** เปิดใช้งาน GPU โดยสร้างอ็อบเจ็กต์ `GpuSettings`, ตั้งค่า `setEnable(true)`, ระบุ ID ของอุปกรณ์ (ถ้าต้องการ) และส่งอ็อบเจ็กต์นี้ไปยังคอนสตรัคเตอร์ `AsposeOCR` หลังจากนั้นการเรียก OCR ทั้งหมดจะทำงานบน GPU ที่เลือก, ให้ความเร็วที่อธิบายไว้ในส่วนประสิทธิภาพ

คลาส `GpuSettings` ให้คุณสลับการใช้ GPU และเลือกอุปกรณ์เฉพาะเมื่อมีหลาย GPU

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.GpuSettings;
import com.aspose.ocr.ImageProcessingOptions;
import com.aspose.ocr.RecognitionLanguage;
import com.aspose.ocr.OcrResult;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Create the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // 2️⃣ Enable GPU processing (auto‑detects available device)
        GpuSettings gpuSettings = new GpuSettings();
        gpuSettings.setEnable(true);          // turn GPU on
        gpuSettings.setDeviceId(0);           // first GPU (change if you have multiple)
        ocrEngine.setGpuSettings(gpuSettings);

        // 3️⃣ Optimize image preprocessing for GPU performance
        ImageProcessingOptions imgOpts = new ImageProcessingOptions();
        imgOpts.setAutoDeskew(true);
        imgOpts.setBinarization(true);
        ocrEngine.setImageProcessingOptions(imgOpts);

        // 4️⃣ Recognize text from an image file (PNG in this case)
        OcrResult result = ocrEngine.recognizeImage(
                "YOUR_DIRECTORY/large_invoice.png",
                RecognitionLanguage.ENGLISH);

        // 5️⃣ Output the detected text
        System.out.println("Detected text:\n" + result.getText());
    }
}
```

### ทำไมต้องเปิดใช้งาน GPU?

การเร่งความเร็วด้วย GPU จะย้ายงานคูณเมทริกซ์หนักที่โมเดล OCR ทำไปยังคอร์ขนานหลายพันคอร์ ในการปฏิบัติคุณจะเห็น **การเร่งความเร็ว 2‑5×** บน RTX 2060 ระดับกลาง, และเร็วกว่าอีกมากบนการ์ดใหม่ ๆ การแลกเปลี่ยนคือการใช้หน่วยความจำเพิ่มขึ้นเล็กน้อย, แต่ส่วนใหญ่ไม่เป็นปัญหาสำหรับ PNG ขนาดใบแจ้งหนี้ทั่วไป

## ขั้นตอนที่ 3 – แยกข้อความจากรูปภาพใน Java – แนวทางปฏิบัติที่ดีที่สุด

เมธอด `recognizeImage` ประมวลผลไฟล์ภาพที่ระบุและคืนข้อความที่ดึงออกมา

**คำตอบโดยตรง (40‑70 คำ):** เรียก `ocrEngine.recognizeImage(filePath)` หลังจากเปิดใช้งาน GPU; เมธอดจะตรวจจับรูปแบบไฟล์โดยอัตโนมัติ, รันโมเดล OCR บน GPU, และคืนข้อความที่ดึงออกมา. เพื่อความแม่นยำสูงสุด, ควรทำให้ภาพเป็นบิทแมพและปรับแนวก่อนเรียกเมธอด

โค้ดด้านบนทำเช่นนั้นแล้ว, แต่ต่อไปนี้เป็นเวอร์ชันที่สรุปเพื่อแยกการเรียก OCR:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**สิ่งที่คุณจะสังเกต:** เมธอด `recognizeImage` ตรวจจับประเภทไฟล์โดยอัตโนมัติ, ดังนั้นคุณสามารถส่ง JPEG, TIFF หรือ PNG ได้โดยไม่ต้องตั้งค่าเพิ่มเติม. นั่นคือเหตุผลที่ **ดึงข้อความจาก PNG** ทำงานได้โดยตรง

### การจัดการไฟล์ขนาดใหญ่

หาก PNG ของคุณใหญ่กว่า 5 MB, พิจารณาลดขนาดก่อน OCR:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

การลดขนาดช่วยลดการใช้หน่วยความจำของ GPU และมักทำให้ความแม่นยำดีขึ้นเพราะโมเดลเห็นขอบที่ชัดเจนขึ้น

## ขั้นตอนที่ 4 – วิธีตั้งค่าตัวเลือกภาพเพื่อความแม่นยำที่ดียิ่งขึ้น

`ImageOptions` เป็นอ็อบเจ็กต์การกำหนดค่าที่ให้คุณปรับขั้นตอนการเตรียมภาพ เช่น การปรับแนวและการทำบิทแมพ ก่อน OCR

**คำตอบโดยตรง (40‑70 คำ):** ใช้อ็อบเจ็กต์ `ImageOptions` เพื่อเปิดใช้งาน auto‑deskew, binarization, และการปรับขนาดตามต้องการก่อนส่งภาพไปยังเอนจิน OCR. ค่าที่นิยมใช้คือ `setAutoDeskew(true)`, `setBinarization(true)`, และปัจจัยการปรับขนาดระหว่าง 0.5 และ 0.8 สำหรับสแกนขนาดใหญ่. การตั้งค่าเหล่านี้ช่วยเพิ่มคอนทราสต์และการจัดแนว, ทำให้เครือข่ายประสาทเทียมจำตัวอักษรได้แม่นยำขึ้น, โดยเฉพาะในเอกสารที่มีเสียงรบกวนหรือเอียง

วลี **วิธีตั้งค่าภาพ** ปรากฏโดยธรรมชาติเมื่อเราพูดถึงการเตรียมภาพ. Aspose OCR มีตัวเลือกหลายอย่าง:

| Option                     | What it does                               | Typical value |
|----------------------------|--------------------------------------------|---------------|
| `setAutoDeskew(true)`      | ทำให้เส้นข้อความที่เอียงตรงขึ้น          | true          |
| `setBinarization(true)`    | แปลงเป็นสีขาว‑ดำเพื่อเพิ่มคอนทราสต์      | true          |
| `setResizeFactor(x)`       | ปรับขนาดภาพ (0 < x ≤ 1)                  | 0.5‑0.8       |
| `setContrastAdjustment(y)` | เพิ่มคอนทราสต์ (0‑100)                   | 30            |

คุณสามารถรวมตัวเลือกเหล่านี้ในลำดับใดก็ได้; ไลบรารีจะประมวลผลตามลำดับก่อนส่งภาพไปยังเครือข่ายประสาทเทียม. การทดลองเป็นกุญแจ—ใบแจ้งหนี้แต่ละใบอาจต้องการค่าที่ต่างกัน

## ขั้นตอนที่ 5 – วิธีแยกข้อความในกรณีขอบ

คลาส `GpuExample` แสดงเวิร์กโฟลว์ OCR แบบครบวงจรโดยใช้ Aspose OCR พร้อมการเร่งด้วย GPU

**คำตอบโดยตรง (40‑70 คำ):** สำหรับสแกนความละเอียดต่ำ, ให้ขยายภาพก่อนหรือขอให้ผู้ใช้สแกนความละเอียดสูงกว่า; สำหรับบันทึกมือ, ต้องเปลี่ยนไปใช้โมเดลที่ฝึกฝนเอง; และสำหรับเอกสารหลายภาษา, ส่งรายการคั่นด้วยคอมม่าไปยัง `RecognitionLanguage`. การปรับเหล่านี้ทำให้เอนจินที่เร่งด้วย GPU ยังคงให้ผลลัพธ์ที่เชื่อถือได้

แม้จะมีพลังของ GPU, บางสถานการณ์ยังทำให้ OCR ผิดพลาด:

1. **สแกนความละเอียดต่ำ (< 150 dpi).** ปรับขนาดขึ้นก่อนหรือขอให้ผู้ใช้สแกนความละเอียดสูงกว่า.  
2. **บันทึกมือ.** โมเดลเริ่มต้นมุ่งเน้นที่ข้อความพิมพ์; คุณต้องใช้โมเดลที่ฝึกฝนเองสำหรับลายมือ.  
3. **หลายภาษา.** ส่งรายการคั่นด้วยคอมม่าไปยัง `RecognitionLanguage`, เช่น `RecognitionLanguage.ENGLISH_FRENCH`.

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## ผลลัพธ์ที่คาดหวัง

การรันคลาส `GpuExample` เต็มรูปแบบกับ `large_invoice.png` ควรพิมพ์ผลลัพธ์ประมาณนี้:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

หากเห็นข้อความเป็นอักขระผสม, ให้ตรวจสอบว่า `gpuSettings.setEnable(true)` ทำงานจริง (คอนโซลจะรายการอุปกรณ์ GPU หากเปิดการบันทึกดีบัก)

## ข้อผิดพลาดทั่วไป & เคล็ดลับมืออาชีพ

- **ลืมตั้งค่า GPU device ID.** ในระบบที่มีหลาย GPU, อาจต้องใช้ `setDeviceId(1)`.  
- **รันใน Docker โดยไม่มี NVIDIA runtime.** เพิ่ม `--gpus all` ไปยังคำสั่ง `docker run`.  
- **ผสมเส้นทางโค้ด CPU‑only และ GPU‑enabled.** รักษาอินสแตนซ์ `AsposeOCR` เพียงหนึ่งต่อเธรดเพื่อหลีกเลี่ยงการชนของสถานะ.  
- **การรั่วของหน่วยความจำ.** เรียก `ocrEngine.dispose()` เมื่อเสร็จสิ้น, โดยเฉพาะในบริการที่ทำงานต่อเนื่อง.

## คำถามที่พบบ่อย

**ถาม: เวอร์ชันทดลองฟรีรองรับการเร่งความเร็วด้วย GPU หรือไม่?**  
**ตอบ:** ใช่, เวอร์ชันทดลองของ Aspose OCR มีการสนับสนุน GPU เต็มรูปแบบ; เพียงเปิดใช้งานในโค้ด.

**ถาม: ฉันสามารถประมวลผล PDF โดยตรงโดยไม่ต้องแปลงเป็นภาพได้หรือไม่?**  
**ตอบ:** Aspose OCR สามารถแปลงหน้า PDF เป็นภาพภายในได้, แต่เพื่อประสิทธิภาพสูงสุดควรแปลงเป็น PNG ความละเอียดสูงก่อน.

**ถาม: ต้องการเวอร์ชัน CUDA ใด?**  
**ตอบ:** แนะนำให้ใช้ CUDA 11.2 หรือใหม่กว่า; เวอร์ชันเก่าอาจทำงานได้แต่ไม่ได้รับการทดสอบอย่างเป็นทางการ.

**ถาม: ปลอดภัยหรือไม่ที่จะรัน OCR กับไฟล์ที่ผู้ใช้อัปโหลดที่ไม่เชื่อถือ?**  
**ตอบ:** ตรวจสอบขนาดและประเภทไฟล์ก่อนประมวลผล, และรัน OCR ในเธรดที่แยก sandbox เพื่อลดความเสี่ยง.

**ถาม: ฉันจะเปิดการบันทึกเพื่อยืนยันการใช้ GPU อย่างไร?**  
**ตอบ:** ตั้งค่า `ocrEngine.setDebugMode(true)`; คอนโซลจะแสดงอุปกรณ์ GPU ที่เลือกและสถิติการใช้หน่วยความจำ.

## สรุป

เราได้อธิบาย **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR ใน Java, แสดงวิธี **แยกข้อความจากรูปภาพ**, สาธิตวิธีที่ง่ายที่สุดในการ **ดึงข้อความจาก PNG**, อธิบาย **วิธีตั้งค่าการประมวลผลภาพ**, และครอบคลุมรายละเอียดของ **วิธีแยกข้อความ** ในไฟล์จริง ๆ ด้วย GPU เปิดอยู่, กระบวนการ OCR ของคุณจะเร็วขึ้นอย่างเห็นได้ชัด, ทำให้เหมาะกับสถานการณ์ที่ต้องประมวลผลจำนวนมากเช่นการประมวลผลใบแจ้งหนี้เป็นชุดหรือการสแกนเอกสารแบบเรียลไทม์

พร้อมก้าวต่อไปหรือยัง? ลองสลับโมเดลภาษาอังกฤษเริ่มต้นเป็นโมเดลหลายภาษา, หรือทดลองสร้างสายการเตรียมภาพแบบกำหนดเองสำหรับใบเสร็จที่มีเสียงรบกวน. ท้องฟ้าเป็นขอบเขต—โดยเฉพาะเมื่อคุณมี GPU ทำงานหนักแทนคุณ

**อัปเดตล่าสุด:** 2026-08-22  
**ทดสอบด้วย:** Aspose OCR for Java 24.10  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [แยกข้อความจากภาพด้วย Aspose OCR การสอน Java OCR เต็มรูปแบบ](/ocr/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [วิธีตั้งค่าใบอนุญาต Aspose OCR และตรวจสอบใน Java](/ocr/java/ocr-basics/set-license/)
- [แยกข้อความจากภาพ Java ด้วย Aspose.OCR โหมดตรวจจับพื้นที่](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}