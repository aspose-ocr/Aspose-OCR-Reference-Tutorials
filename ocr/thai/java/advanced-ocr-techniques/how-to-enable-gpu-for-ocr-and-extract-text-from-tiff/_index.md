---
category: general
date: 2026-02-14
description: วิธีเปิดใช้งาน GPU ใน Aspose OCR Java เพื่อดึงข้อความจากภาพอย่างรวดเร็ว
  เรียนรู้การแปลง TIFF เป็นข้อความ ตั้งค่า GPU device ID และอ่านข้อความจากไฟล์ TIFF
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert tiff to text
- set gpu device id
- read text from tiff
language: th
og_description: วิธีเปิดใช้งาน GPU ใน Aspose OCR Java เพื่อดึงข้อความจากภาพอย่างรวดเร็ว
  ทำตามคู่มือนี้เพื่อแปลง TIFF เป็นข้อความ ตั้งค่า GPU device ID และอ่านข้อความจากไฟล์
  TIFF.
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR – ดึงข้อความจากไฟล์ TIFF
tags:
- OCR
- Java
- GPU acceleration
title: วิธีเปิดใช้งาน GPU สำหรับ OCR และดึงข้อความจากไฟล์ TIFF
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

.

Translate bullet items.

Finally closing shortcodes unchanged.

Also final backtop button shortcode unchanged.

Make sure to keep markdown formatting.

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR และดึงข้อความจาก TIFF

เคยสงสัย **วิธีเปิดใช้งาน GPU** ขณะทำ OCR บนไฟล์ TIFF ขนาดใหญ่หรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต่างมองหาแรงเร่งความเร็วเพิ่มเติมอยู่เสมอ โดยเฉพาะเมื่อภาพต้นฉบับเป็น TIFF ขนาดหลายเมกะไบต์ ข่าวดีคือ? ด้วย Aspose OCR for Java คุณสามารถสลับสวิตช์ ชี้ไปที่ GPU ที่ถูกต้อง และดูเอนจินทำงานอย่างรวดเร็วผ่านภาพ

ในบทเรียนนี้เราจะเดินผ่านขั้นตอนทั้งหมด: โหลด TIFF, เปิดการเร่งความเร็วด้วย GPU, เลือกอุปกรณ์ GPU เฉพาะ (ถ้าต้องการ), รัน OCR, และสุดท้าย **ดึงข้อความจากภาพ**. เมื่อจบคุณจะสามารถ **แปลง TIFF เป็นข้อความ** ด้วยไม่กี่บรรทัดของโค้ด, และคุณยังจะเห็นวิธี **อ่านข้อความจากไฟล์ TIFF** บนแพลตฟอร์มที่รองรับใด ๆ

## สิ่งที่คุณต้องการ

- Java 17 หรือใหม่กว่า (โค้ดทำงานกับ Java 8+ ด้วยเช่นกัน)
- Aspose OCR for Java 23.10 (หรือเวอร์ชันล่าสุด ณ เวลาที่เขียน)
- GPU ที่รองรับ CUDA พร้อมติดตั้งไดรเวอร์ล่าสุด
- ไฟล์ TIFF หลายหน้าแบบตัวอย่าง (เราจะเรียกว่า `sample_large.tif`)

ไม่มี Maven wizardry? ไม่เป็นไร—แค่วาง JAR ลงใน classpath ของคุณแล้วคุณก็พร้อมใช้งาน

![วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java](gpu-ocr.png)

*ข้อความแทนภาพ: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java*

## ขั้นตอนที่ 1: โหลดภาพ TIFF สำหรับ OCR

ก่อนอื่นคุณต้องมีอินสแตนซ์ `OcrEngine` และภาพต้นฉบับ Aspose OCR สามารถอ่านรูปแบบ raster เกือบทั้งหมด, แต่ TIFF เป็นรูปแบบที่พบบ่อยสำหรับเอกสารสแกน

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การเรียก `setImage` จะห่อไฟล์ใน `ImageStream`, ซึ่งทำให้เอนจินจัดการกับ TIFF หลายหน้าได้โดยไม่ต้องแยกไฟล์ด้วยตนเอง. หากไฟล์ไม่พบ, คุณจะได้รับ `FileNotFoundException` ที่ชัดเจน—ดังนั้นตรวจสอบเส้นทางอีกครั้ง

## ขั้นตอนที่ 2: เปิดการเร่งความเร็วด้วย GPU

ตอนนี้จุดสำคัญเกิดขึ้น การเปิด GPU เพียงแค่ตั้งค่า boolean, แต่สามารถลดเวลาประมวลผลเป็นวินาที—หรือแม้กระทั่งนาที

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **เคล็ดลับ:** หากเครื่องของคุณมี GPU หลายตัว, ค่าเริ่มต้นมักจะเป็นตัวแรก (device 0). คุณสามารถให้ Aspose เลือกอุปกรณ์ที่ดีที่สุดอัตโนมัติ, แต่การระบุอุปกรณ์เองอาจหลีกเลี่ยงความประหลาดใจบนเวิร์กสเตชันที่มีหลาย GPU

## ขั้นตอนที่ 3: ตั้งค่า GPU device ID (ไม่บังคับ)

บางครั้งคุณรู้แน่ชัดว่า GPU ใดที่ต้องการใช้—เช่นการ์ดที่สองที่มุ่งเน้นงาน AI. นั่นคือจุดที่ `setGpuDeviceId` มีประโยชน์

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **กรณีขอบ:** หากคุณส่ง ID ที่ไม่ถูกต้อง, เอนจินจะโยน `IllegalArgumentException`. การพิมพ์ `System.out.println(ocrEngine.getEngineOptions().getAvailableGpuDevices())` จะช่วยแสดงรายการ ID ที่มีให้คุณ

## ขั้นตอนที่ 4: ประมวลผลภาพและ **ดึงข้อความจากภาพ**

เมื่อเอนจินตั้งค่าเรียบร้อย, ถึงเวลารัน OCR. วัตถุผลลัพธ์จะให้สตริงดิบพร้อมคะแนนความเชื่อมั่นหากคุณต้องการ

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

หาก TIFF มีข้อความ “Hello, World!” คุณควรเห็นอะไรคล้าย ๆ นี้:

```
Recognized text:
Hello, World!
```

เอนจินจัดการการขึ้นบรรทัด, เครื่องหมายวรรคตอน, และแม้กระทั่งการตรวจจับโครงสร้างพื้นฐาน. หากต้องการควบคุมระดับละเอียดมากขึ้น (เช่น ดึงข้อความต่อหน้า), สำรวจ `ocrResult.getPages()`.

## ขั้นตอนที่ 5: ตรวจสอบผลลัพธ์และจัดการปัญหาทั่วไป

### ทำไม GPU อาจไม่ได้ถูกใช้?

- **Driver mismatch:** ไดรเวอร์ GPU ต้องเป็นเวอร์ชันที่ Aspose แนะนำอย่างน้อย (ตรวจสอบใน release notes)
- **Insufficient memory:** ภาพขนาดใหญ่มากอาจเกิน VRAM ของ GPU. ในกรณีนั้นเอนจินจะสลับกลับไปใช้ CPU อย่างอ่อนโยน—มองหาคำเตือนในคอนโซล
- **Unsupported hardware:** กราฟิกแบบบูรณาการมักไม่มีความสามารถคอมพิวต์ที่จำเป็น

### วิธีกลับไปใช้ CPU อย่างโปรแกรมเมติก

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### การอ่านข้อความจาก TIFF ในลูป

หากคุณมีโฟลเดอร์ที่เต็มไปด้วย TIFF, คุณสามารถวนลูปได้:

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

โค้ดส่วนนี้แสดงวิธี **อ่านข้อความจากไฟล์ TIFF** เป็นชุด, พร้อมยังคงได้รับประโยชน์จากการเร่งความเร็วด้วย GPU

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานบน Linux ได้หรือไม่?**  
**A:** ทำได้แน่นอน—Aspose OCR รองรับหลายแพลตฟอร์ม. เพียงตรวจสอบให้แน่ใจว่าได้ติดตั้ง CUDA toolkit และไดรเวอร์แล้ว

**Q: ถ้าฉันไม่มี GPU จะทำอย่างไร?**  
**A:** ตั้งค่า `setUseGpu(false)` หรือไม่เรียกเมธอดนั้นเลย. เอนจินจะใช้ CPU เป็นค่าเริ่มต้น

**Q: สามารถดึงข้อความจากรูปแบบอื่นได้หรือไม่?**  
**A:** ได้, เมธอด `setImage` ยอมรับ JPEG, PNG, BMP, และแม้กระทั่งสตรีม PDF

**Q: ความแม่นยำของ OCR บน TIFF ความละเอียดต่ำเป็นอย่างไร?**  
**A:** ความแม่นยำจะลดลงเมื่อความละเอียดต่ำกว่า 300 dpi. ควรทำการพรี‑โปรเซสภาพ (เช่น การทำไบนารี, การแก้ไขการเอียง) ก่อนส่งให้เอนจิน

## สรุป

คุณได้เรียนรู้ **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR Java, **วิธีตั้งค่า GPU device ID**, และที่สำคัญที่สุด **วิธีดึงข้อความจากไฟล์ภาพ**, โดยเฉพาะ **แปลง TIFF เป็นข้อความ** และ **อ่านข้อความจาก TIFF** อย่างมีประสิทธิภาพ. เพียงสลับสวิตช์เดียวและอาจเลือกอุปกรณ์, คุณจะได้รับการเพิ่มประสิทธิภาพอย่างมหาศาลโดยไม่ต้องเขียนโค้ด OCR ใหม่

พร้อมก้าวต่อไปหรือยัง? ลองทดลองกับ:

- **การประมวลผลเป็นชุด** ของหลายร้อย TIFF ด้วยเธรดแบบขนาน
- **แพ็คเกจภาษาแบบกำหนดเอง** เพื่อปรับปรุงการจดจำบนเอกสารเฉพาะด้าน
- **การประมวลผลหลังจากดึงข้อความ** ด้วย regex เพื่อทำความสะอาดรูปแบบ

หากเจออุปสรรคใด ๆ อย่าลังเลที่จะแสดงความคิดเห็น, และขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}