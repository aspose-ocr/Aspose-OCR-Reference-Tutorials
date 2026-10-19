---
category: general
date: 2026-09-23
description: เรียนรู้วิธีดึงข้อความจากไฟล์ TIFF อย่างรวดเร็วโดยเปิดใช้งานการเร่งความเร็วด้วย
  GPU ใน Aspose OCR for Java คู่มือแบบขั้นตอนแสดงการโหลด TIFF การตั้งค่า GPU device
  ID และการอ่านข้อความ
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: เรียนรู้วิธีดึงข้อความจากไฟล์ TIFF อย่างรวดเร็วโดยเปิดใช้งานการเร่งความเร็วด้วย
  GPU ใน Aspose OCR for Java คู่มือแสดงการโหลด TIFF การเลือกอุปกรณ์ GPU และการอ่านข้อความที่ดึงออกมา
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: ดึงข้อความจากไฟล์ TIFF ด้วยการเร่งความเร็ว GPU ใน OCR Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: วิธีดึงข้อความจากไฟล์ TIFF ด้วย GPU ใน OCR Java
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อความจากไฟล์ tiff ด้วย GPU ใน OCR Java

หากคุณต้องการ **ดึงข้อความจากไฟล์ tiff** อย่างรวดเร็ว การเปิดใช้งานการเร่งความเร็วด้วย GPU ใน Aspose OCR for Java เป็นวิธีที่เร็วที่สุด ใน 100 คำแรกเราจะอธิบายว่าทำไม GPU ถึงสำคัญ จากนั้นจะแนะนำขั้นตอนการโหลด TIFF, เปิดใช้งาน GPU, เลือกอุปกรณ์เฉพาะตามต้องการ, รัน OCR, และสุดท้ายอ่านข้อความที่ดึงออกมา เมื่อเสร็จคุณจะสามารถแปลง TIFF เป็นข้อความได้ด้วยเพียงไม่กี่บรรทัดของโค้ด

## คำตอบเร็ว
- **อะไรคือประโยชน์หลักของ GPU OCR?** เร็วขึ้นถึง 5× สำหรับการประมวลผลไฟล์ TIFF ขนาดใหญ่หลายหน้า.  
- **เวอร์ชัน Java ที่ต้องการคืออะไร?** Java 17 หรือใหม่กว่า (Java 8+ ก็ทำงานได้).  
- **ฉันต้องการไลเซนส์พิเศษหรือไม่?** จำเป็นต้องมีไลเซนส์ Aspose OCR for Java ที่ถูกต้องสำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **ฉันสามารถรันนี้บน Linux ได้หรือไม่?** ได้—Aspose OCR รองรับหลายแพลตฟอร์ม; เพียงติดตั้ง CUDA toolkit.  
- **GPU เป็นตัวเลือกหรือไม่?** คุณสามารถกลับไปใช้ CPU ได้โดยเรียก `setUseGpu(false)`.

## OcrEngine คืออะไร?
`OcrEngine` class เป็นส่วนประกอบหลักของ Aspose OCR for Java มันรวมฟังก์ชัน OCR ทั้งหมดไว้ ทำให้คุณสามารถโหลดภาพ, ตั้งค่าตัวเลือกการประมวลผลเช่นภาษาและการใช้ GPU, และดึงข้อความที่ถูกจดจำพร้อมข้อมูลความเชื่อมั่นในรูปแบบอ็อบเจกต์ที่สะดวก.  

`OcrEngine` เป็นคลาสหลักของ Aspose OCR ที่เป็นตัวแทนของเอนจินการประมวลผล OCR และให้เมธอดสำหรับโหลดภาพ, ตั้งค่าตัวเลือก, และดึงผลลัพธ์.

## วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java?
โหลดภาพของคุณ, เปิดใช้งาน GPU, และเรียก `recognize`—เท่านี้ก็พอ การเปิดใช้งาน GPU ด้วย `setUseGpu(true)` ทำให้เอนจินย้ายงานที่ใช้พิกเซลหนักไปยังการ์ดกราฟิก, ลดเวลาในการประมวลผลอย่างมาก, โดยเฉพาะสำหรับ TIFF ความละเอียดสูงหรือหลายหน้า.

## สิ่งที่คุณต้องการ
- Java 17 หรือใหม่กว่า (โค้ดยังทำงานได้บน Java 8+).  
- Aspose OCR for Java 23.10 (หรือเวอร์ชันล่าสุด).  
- GPU ที่รองรับ CUDA พร้อมติดตั้งไดรเวอร์ล่าสุด.  
- ไฟล์ TIFF หลายหน้าตัวอย่าง (เช่น `sample_large.tif`).  
- ไม่มี Maven? เพียงวางไฟล์ JAR ลงใน classpath ของคุณ.

![วิธีเปิดใช้งาน GPU tutorial](gpu-ocr.png)

[วิธีเปิดใช้งาน GPU tutorial](gpu-ocr.png)

*ข้อความแทนภาพ: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java*

## ขั้นตอนที่ 1: โหลดภาพ TIFF สำหรับ OCR

เมธอด `setImage` จะห่อไฟล์ใน `ImageStream`, ทำให้เอนจินสามารถจัดการ TIFF หลายหน้าโดยไม่ต้องแยกไฟล์ด้วยตนเอง หากไม่พบไฟล์ จะมีการโยน `FileNotFoundException` ที่ชัดเจน.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การเรียก `setImage` ทำให้การจัดการหน้าถูกแยกออก, ดังนั้นคุณสามารถประมวลผลเอกสารทั้งหมดด้วยเอนจินอินสแตนซ์เดียว.

## ขั้นตอนที่ 2: เปิดการเร่งความเร็วด้วย GPU

การเปิด GPU เป็นเพียงการตั้งค่า boolean เดียว ในระบบส่วนใหญ่ GPU เริ่มต้นคืออุปกรณ์ 0, แต่คุณสามารถให้ Aspose เลือกอุปกรณ์ที่เหมาะสมโดยอัตโนมัติ.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **เคล็ดลับ:** ในเวิร์กสเตชันที่มี GPU หลายตัว การระบุ ID ของอุปกรณ์จะช่วยหลีกเลี่ยงการย้อนกลับโดยไม่คาดคิดไปยัง GPU แบบบูรณาการที่ช้ากว่า.

## ขั้นตอนที่ 3: ตั้งค่า GPU device ID (ไม่บังคับ)

หากคุณรู้ว่า GPU ใดควรทำ OCR—เช่นการ์ด AI เฉพาะ—คุณสามารถตั้งค่าโดยตรงด้วย `setGpuDeviceId`.

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **กรณีขอบ:** การส่ง ID ที่ไม่ถูกต้องจะทำให้เกิด `IllegalArgumentException`. ใช้ `ocrEngine.getEngineOptions().getAvailableGpuDevices()` เพื่อแสดงรายการ ID ที่ถูกต้อง.

## ขั้นตอนที่ 4: ประมวลผลภาพและดึงข้อความจากภาพ

การรัน OCR จะคืนค่า `OcrResult` ที่มีสตริงข้อความธรรมดาและคะแนนความเชื่อมั่น (ถ้ามี).

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก TIFF มีข้อความ “Hello, World!” ผลลัพธ์จะเป็นดังนี้:

```
Recognized text:
Hello, World!
```

เอนจินจะจัดการการขึ้นบรรทัดใหม่, เครื่องหมายวรรคตอน, และการตรวจจับโครงสร้างพื้นฐานโดยอัตโนมัติ. สำหรับการดึงข้อความต่อหน้า, สำรวจ `ocrResult.getPages()`.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และจัดการปัญหาทั่วไป

GPU อาจถูกข้ามไปได้หลายสาเหตุ หากเวอร์ชันไดรเวอร์ที่ติดตั้งเก่ากว่าขั้นต่ำที่ต้องการ, ไลบรารีจะไม่สามารถเริ่มต้น CUDA ได้. หน่วยความจำวิดีโอไม่เพียงพออาจทำให้เอนจินย้อนกลับไปใช้ CPU และกราฟิกแบบบูรณาการบางรุ่นขาดความสามารถในการคำนวณที่จำเป็นสำหรับการเร่ง OCR.

### ทำไม GPU ถึงอาจไม่ได้ถูกใช้?
- **ไม่ตรงกันของไดรเวอร์:** ไดรเวอร์ GPU ต้องตรงกับเวอร์ชันขั้นต่ำที่ระบุในบันทึกการปล่อยของ Aspose.  
- **หน่วยความจำไม่เพียงพอ:** ภาพขนาดใหญ่มากอาจเกิน VRAM; เอนจินจะย้อนกลับไปใช้ CPU และบันทึกคำเตือน.  
- **ฮาร์ดแวร์ไม่รองรับ:** กราฟิกแบบบูรณาการมักขาดความสามารถในการคำนวณที่จำเป็น.

### วิธีย้อนกลับไปใช้ CPU อย่างโปรแกรมเมติก
หากคุณต้องการรับประกันการประมวลผลด้วย CPU, เรียกตัวตั้งค่าตัวเลือกของเอนจินด้วยค่า false. วิธีนี้จะปิดการพยายามใช้ GPU และบังคับให้กระบวนการ OCR ทำงานทั้งหมดบนโปรเซสเซอร์ของโฮสต์, ซึ่งมีประโยชน์บนเครื่องที่ไม่มีการ์ดกราฟิกที่รองรับ.

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### การอ่านข้อความจาก TIFF ในลูป
เมื่อประมวลผลไฟล์หลายไฟล์, ให้วนลูปผ่านไดเรกทอรีพร้อมเปิดใช้งานการเร่งความเร็วด้วย GPU.

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

โค้ดส่วนนั้นแสดงวิธี **อ่านข้อความจากไฟล์ TIFF** จำนวนมากโดยไม่สูญเสียการเพิ่มประสิทธิภาพ.

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานบน Linux ได้หรือไม่?**  
A: แน่นอน—Aspose OCR ทำงานบน Windows, Linux, และ macOS ตราบใดที่ติดตั้ง CUDA toolkit และไดรเวอร์แล้ว.

**Q: ถ้าฉันไม่มี GPU จะทำอย่างไร?**  
A: ไม่ต้องเรียก `setUseGpu(true)` หรือเรียก `setUseGpu(false)` อย่างชัดเจน; เอนจินจะทำงานบน CPU.

**Q: ฉันสามารถดึงข้อความจากรูปแบบอื่นได้หรือไม่?**  
A: ได้. `setImage` รองรับ JPEG, PNG, BMP, PDF, และอื่น ๆ.

**Q: ความแม่นยำของ OCR บน TIFF ความละเอียดต่ำเป็นอย่างไร?**  
A: ความแม่นยำลดลงอย่างมากเมื่อต่ำกว่า 300 dpi. ควรทำการประมวลผลล่วงหน้าภาพ (binarization, deskew) เพื่อผลลัพธ์ที่ดีกว่า.

**Q: Aspose OCR รองรับรูปแบบไฟล์กี่ประเภท?**  
A: ไลบรารีรองรับรูปแบบ raster และเอกสารกว่า 30 ประเภท, รวมถึง TIFF, JPEG, PNG, BMP, PDF, และ GIF.

## สรุป

ตอนนี้คุณรู้ **วิธีดึงข้อความจากไฟล์ tiff** ด้วยการเร่งความเร็วด้วย GPU ใน Aspose OCR for Java, วิธีตั้งค่า GPU device ID เฉพาะ, และวิธีประมวลผล TIFF เดียวหรือหลายไฟล์อย่างมีประสิทธิภาพ. ด้วยการสลับค่า flag เพียงค่าเดียว คุณจะได้เพิ่มความเร็วอย่างมหาศาลโดยไม่ต้องเปลี่ยนแปลงตรรกะ OCR ใด ๆ.

ขั้นตอนต่อไปที่คุณอาจลอง:
- ประมวลผลแบชหลายร้อยไฟล์ TIFF พร้อมกันในเธรดแบบขนาน.  
- โหลดแพ็คภาษาแบบกำหนดเองเพื่อปรับปรุงการจดจำคำศัพท์เฉพาะ.  
- ประมวลผลต่อข้อความที่ดึงออกมาด้วย regex เพื่อทำความสะอาดรูปแบบ.

หากคุณพบปัญหาใด ๆ, กรุณาแสดงความคิดเห็นด้านล่าง. โค้ดสนุก!

---

**อัปเดตล่าสุด:** 2026-09-23  
**ทดสอบด้วย:** Aspose OCR for Java 23.10  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [วิธีเปิดใช้งาน GPU สำหรับ Java OCR ขั้นตอนโดยขั้นตอน](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [จดจำข้อความจากภาพด้วย Aspose OCR คู่มือเต็ม Java](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [ประมวลผลล่วงหน้าภาพ OCR ใน Java เพื่อเพิ่มความแม่นยำการดึงข้อความ](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}