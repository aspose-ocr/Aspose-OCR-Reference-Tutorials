---
category: general
date: 2026-01-02
description: วิธีเปิดใช้งาน GPU ใน Java OCR เพื่อจดจำข้อความจากภาพอย่างรวดเร็ว เรียนรู้การดึงข้อความจาก
  PNG ตั้งค่าตัวเลือกภาพ และจดจำข้อความอย่างมีประสิทธิภาพ
draft: false
keywords:
- how to enable gpu
- recognize text from image
- extract text from png
- how to set image
- how to recognize text
language: th
og_description: วิธีเปิดใช้งาน GPU ใน Java OCR เพื่อจดจำข้อความจากภาพอย่างรวดเร็ว
  คู่มือนี้จะแสดงวิธีดึงข้อความจากไฟล์ PNG ตั้งค่าตัวเลือกภาพ และจดจำข้อความอย่างมีประสิทธิภาพ
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – แยกข้อความจากภาพอย่างรวดเร็ว
tags:
- OCR
- Java
- GPU
title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – แยกข้อความจากภาพอย่างรวดเร็ว
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – จดจำข้อความจากภาพอย่างรวดเร็ว

การเปิดใช้งาน GPU ในแอปพลิเคชัน OCR ด้วย Java เป็นอุปสรรคที่หลายคนต้องเผชิญเมื่อต้องการสกัดข้อความอย่างเร็ว ในบทเรียนนี้เราจะแสดง **วิธีเปิดใช้งาน GPU** , จดจำข้อความจากภาพ, และสกัดข้อความจาก PNG ด้วยไลบรารี Aspose OCR  

หากคุณเคยเจอกระบวนการ OCR ที่ช้าและสงสัยว่าการ์ดจอจะช่วยเร่งได้หรือไม่ คุณมาถูกที่แล้ว เราจะอธิบายวิธีตั้งค่าตัวเลือกการประมวลผลภาพเพื่อให้เครื่อง OCR อ่านไฟล์ของคุณได้อย่างแม่นยำ และตอบคำถาม “วิธีจดจำข้อความ” ที่ตามมาอย่างแน่นอน

## สิ่งที่คุณต้องเตรียม

- **Java 17** หรือใหม่กว่า (โค้ดสามารถคอมไพล์กับเวอร์ชันก่อนหน้าได้ แต่ 17 เป็นจุดที่เหมาะที่สุด)  
- **Aspose OCR for Java** – ดาวน์โหลด JAR ล่าสุดจากเว็บไซต์ Aspose หรือ Maven Central  
- เครื่องที่ **รองรับ GPU** (NVIDIA RTX 3060 หรือการ์ดที่เข้ากันได้กับ CUDA ใดก็ได้)  
- ไฟล์ภาพสำหรับทดสอบ – PNG ใบแจ้งหนี้ขนาดใหญ่เป็นตัวเลือกที่ดีสำหรับการวัดประสิทธิภาพ  

> **เคล็ดลับ:** หากคุณใช้แล็ปท็อปที่มีกราฟิกแบบรวมไว้, ตรวจสอบให้แน่ใจว่าได้เลือก GPU แยกต่างหากในการตั้งค่าไดรเวอร์; มิฉะนั้นไลบรารีจะกลับไปใช้ CPU โดยอัตโนมัติ

![ตัวอย่างการเปิดใช้งาน GPU](image.png "ตัวอย่างการเปิดใช้งาน GPU")

*ข้อความแทนภาพ: ตัวอย่างการเปิดใช้งาน GPU แสดงโค้ด Java*

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และตรวจสอบความพร้อมของ GPU

ก่อนที่คุณจะ *เปิดใช้งาน GPU* ได้, คุณต้องมีไลบรารีอยู่ใน classpath เพิ่ม dependency ของ Maven (หรือวาง JAR ลงใน `libs/`):

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Check for the latest version -->
</dependency>
```

เมื่อเพิ่ม dependency แล้ว, รันการตรวจสอบอย่างเร็ว:

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

หากผลลัพธ์แสดงจำนวนอุปกรณ์ที่ไม่เป็นศูนย์, JVM ของคุณเห็น GPU แล้ว หากแสดงศูนย์, ตรวจสอบการติดตั้งไดรเวอร์และตัวแปรสภาพแวดล้อม `CUDA_PATH` อีกครั้ง

## ขั้นตอนที่ 2 – วิธีเปิดใช้งาน GPU ใน Aspose OCR

ตอนนี้ระบบรับรู้การ์ดกราฟิกแล้ว, มาลองเปิดใช้งานจริง คำสำคัญหลักปรากฏในส่วนหัวตามกฎ SEO

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

การเร่งความเร็วด้วย GPU จะย้ายงานคูณเมทริกซ์ที่หนักของโมเดล OCR ไปยังคอร์ขนานหลายพันคอร์ ในการใช้งานจริงคุณจะเห็น **การเร่ง 2‑5×** บน RTX 2060 ปานกลาง, และเร็วกว่าอีกบนการ์ดรุ่นใหม่ ข้อเสียคือใช้หน่วยความจำเพิ่มขึ้นเล็กน้อย, แต่ส่วนใหญ่ไม่เป็นปัญหาสำหรับ PNG ขนาดใบแจ้งหนี้ทั่วไป

## ขั้นตอนที่ 3 – จดจำข้อความจากภาพ (และสกัดข้อความจาก PNG)

เมื่อ GPU ทำงานแล้ว, เรามาโฟกัสที่ขั้นตอน *จดจำข้อความจากภาพ* โค้ดข้างบนทำแล้ว, แต่นี่คือเวอร์ชันที่สรุปให้เห็นการเรียก OCR อย่างชัดเจน:

```java
// Assuming ocrEngine is already configured with GPU
String imagePath = "sample.png";
OcrResult ocrResult = ocrEngine.recognizeImage(imagePath, RecognitionLanguage.ENGLISH);
String extractedText = ocrResult.getText();

System.out.println("Extracted text from PNG:");
System.out.println(extractedText);
```

**สิ่งที่คุณจะสังเกต:** เมธอด `recognizeImage` ตรวจจับประเภทไฟล์โดยอัตโนมัติ, ดังนั้นคุณสามารถใส่ JPEG, TIFF หรือ PNG ได้โดยไม่ต้องตั้งค่าเพิ่มเติม นั่นคือเหตุผลที่ *สกัดข้อความจาก png* ทำงานได้โดยตรง

### การจัดการไฟล์ขนาดใหญ่

หาก PNG ของคุณใหญ่กว่า 5 MB, พิจารณาลดขนาดก่อนทำ OCR:

```java
imgOpts.setResizeFactor(0.5); // shrink to 50 % of original dimensions
ocrEngine.setImageProcessingOptions(imgOpts);
```

การลดความละเอียดช่วยลดการใช้หน่วยความจำของ GPU และมักทำให้ความแม่นยำดีขึ้น เพราะโมเดลเห็นขอบที่ชัดเจนขึ้น

## ขั้นตอนที่ 4 – วิธีตั้งค่าตัวเลือกภาพเพื่อความแม่นยำที่ดียิ่งขึ้น

วลี *วิธีตั้งค่าภาพ* ปรากฏตามธรรมชาติเมื่อพูดถึงการเตรียมข้อมูลล่วงหน้า Aspose OCR มีตัวเลือกหลายอย่าง:

| Option                | คำอธิบาย                                   | Typical value |
|-----------------------|--------------------------------------------|---------------|
| `setAutoDeskew(true)`| ทำให้ข้อความที่เอียงตรงขึ้น                | true          |
| `setBinarization(true)`| แปลงเป็นสีขาว‑ดำเพื่อเพิ่มคอนทราสต์   | true          |
| `setResizeFactor(x)` | ปรับขนาดภาพ (0 < x ≤ 1)                  | 0.5‑0.8       |
| `setContrastAdjustment(y)`| เพิ่มคอนทราสต์ (0‑100)               | 30            |

คุณสามารถรวมตัวเลือกเหล่านี้ได้ตามต้องการ; ไลบรารีจะประมวลผลตามลำดับก่อนส่งภาพให้กับเครือข่ายประสาททดลอง การทดลองเป็นกุญแจ—ใบแจ้งหนี้แต่ละใบอาจต้องค่าที่ต่างกัน

## ขั้นตอนที่ 5 – วิธีจดจำข้อความในกรณีเฉพาะ

แม้จะมีพลังจาก GPU, ยังมีสถานการณ์ที่ OCR ทำงานไม่ถูกต้อง:

1. **สแกนความละเอียดต่ำ (< 150 dpi).** ขยายก่อนหรือขอให้ผู้ใช้สแกนความละเอียดสูงขึ้น  
2. **โน้ตมือเขียน.** โมเดลเริ่มต้นออกแบบมาสำหรับข้อความพิมพ์; ต้องใช้โมเดลฝึกพิเศษสำหรับลายมือ  
3.หลายภาษา.** ส่งรายการคั่นด้วยคอมม่าให้ `RecognitionLanguage`, เช่น `RecognitionLanguage.ENGLISH_FRENCH`

```java
ocrEngine.recognizeImage("multilang.png",
        RecognitionLanguage.ENGLISH_FRENCH);
```

## ผลลัพธ์ที่คาดหวัง

รันคลาส `GpuExample` เต็มรูปแบบกับ `large_invoice.png` ควรพิมพ์ผลลัพธ์ประมาณนี้:

```
Detected text:
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
...
```

หากเห็นข้อความเป็นอักขระแปลก, ตรวจสอบว่า `gpuSettings.setEnable(true)` ทำงานจริงหรือไม่ (คอนโซลจะรายชื่ออุปกรณ์ GPU หากเปิดการบันทึกดีบัก)

## ข้อผิดพลาดทั่วไป & เคล็ดลับระดับมืออาชีพ

- **ลืมตั้งค่า GPU device ID.** บนเครื่องที่มีหลาย GPU, อาจต้องใช้ `setDeviceId(1)`  
- **รันใน Docker โดยไม่มี NVIDIA runtime.** เพิ่ม `--gpus all` ในคำสั่ง `docker run`  
- **ผสมโค้ด CPU‑ กับ GPU‑enabled.** ใช้ instance ของ `AsposeOCR` เพียงหนึ่งต่อแต่ละเธรดเพื่อหลีกเลี่ยงการชนของสถานะ  
- **หน่วยความจำรั่ว.** เรียก `ocrEngine.dispose()` เมื่อเสร็จ, โดยเฉพาะในบริการที่ทำงานต่อเนื่องเป็นเวลานาน  

## สรุป

เราได้อธิบาย **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR ใน Java, แสดง **วิธีจดจำข้อความจากภาพ**, สาธิตวิธี **สกัดข้อความจาก PNG** อย่างง่าย, อธิบาย **วิธีตั้งค่าภาพ** เพื่อประสิทธิภาพที่ดียิ่งขึ้น, และครอบคลุมความละเอียดของ **วิธีจดจำข้อความ** ในไฟล์จริง ๆ ด้วย GPU เปิดอยู่, pipeline OCR ของคุณจะเร็วขึ้นอย่างเห็นได้ชัด, เหมาะกับสถานการณ์ที่ต้องประมวลผลจำนวนมาก เช่น การประมวลผลใบแจ้งหนี้เป็นชุดหรือการสแกนเอกสารเรียทม์  

พร้อมก้าวต่อไปหรือยัง? ลองสลับโมเดลภาษาอังกฤษเริ่มต้นเป็นโมเดลหลายภาษา, หรือทดลอง pipeline การเตรียมข้อมูลแบบกำหนดเองสำหรับใบเสร็จที่มีเสียงรบกวน ความเป็นไปได้ไม่มีที่สิ้นสุด—โดยเฉพาะเมื่อคุณมี GPU ทำงานหนักแทนคุณ

---

*ขอให้เขียนโค้ดสนุกและ OCR ของคุณเร็วไว!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}