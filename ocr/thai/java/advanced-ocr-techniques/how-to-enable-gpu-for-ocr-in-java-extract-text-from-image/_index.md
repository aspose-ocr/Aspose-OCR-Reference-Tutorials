---
category: general
date: 2026-02-27
description: เรียนรู้วิธีเปิดใช้งาน GPU ในโค้ด Aspose OCR Java เพื่อดึงข้อความจากภาพ
  แปลงรูปถ่ายเป็นข้อความและจดจำข้อความจากรูปถ่ายอย่างมีประสิทธิภาพ
draft: false
keywords:
- how to enable gpu
- extract text from image
- convert photo to text
- how to extract text
- recognize text from photo
language: th
og_description: วิธีเปิดใช้งาน GPU ใน Aspose OCR Java และดึงข้อความจากภาพอย่างรวดเร็ว
  แปลงรูปภาพเป็นข้อความและจดจำข้อความจากรูปภาพได้อย่างง่ายดาย.
og_title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – การสกัดข้อความอย่างรวดเร็ว
tags:
- OCR
- Java
- GPU
- Aspose
title: วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – แยกข้อความจากภาพ
url: /th/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java – ดึงข้อความจากภาพ

เคยสงสัย **วิธีเปิดใช้งาน GPU** เมื่อทำ OCR บนภาพความละเอียดสูงหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนา Java หลายคนเจออุปสรรคเมื่อ pipeline OCR ของพวกเขาช้าในสภาพแวดล้อมที่ใช้ CPU เท่านั้น โดยเฉพาะเมื่อขนาดภาพพุ่งเกินหลายเมกะพิกเซล ข่าวดีคือ การเปิดใช้งานการเร่งความเร็วด้วย GPU ผ่าน Aspose OCR ทำได้ง่ายดาย และช่วยให้คุณ **ดึงข้อความจากภาพ** ได้ในเวลาที่สั้นกว่ามาก

ในบทเรียนนี้เราจะเดินผ่านกระบวนการทั้งหมด: ตั้งค่าไลบรารี Aspose OCR, เปิดสวิตช์ GPU, ป้อนภาพขนาดใหญ่, และสุดท้าย **แปลงรูปภาพเป็นข้อความ**. เมื่อเสร็จคุณจะรู้ **วิธีดึงข้อความ** อย่างเชื่อถือได้ และคุณจะได้เห็นวิธี **จดจำข้อความจากรูปภาพ** บนเครื่องที่มีหลาย GPU. ไม่ต้องอ้างอิงภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่แล้ว

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะดำเนินการต่อ โปรดตรวจสอบว่าคุณมี:

* Java 17 หรือใหม่กว่า (เวอร์ชัน LTS ล่าสุดทำงานได้ดีที่สุด)
* GPU จาก NVIDIA หรือ AMD ที่รองรับพร้อมไดรเวอร์อัปเดต (CUDA 12.x สำหรับ NVIDIA, ROCm สำหรับ AMD)
* Aspose OCR for Java JARs—ดาวน์โหลดเวอร์ชัน 23.x ล่าสุดจากเว็บไซต์ Aspose
* Maven หรือ Gradle เพื่อจัดการ dependencies (เราจะแสดงตัวอย่าง Maven)
* ภาพความละเอียดสูง (เช่น `high-res-photo.jpg`) ที่คุณต้องการประมวลผล

หากขาดอย่างใดอย่างหนึ่ง โค้ดยังคอมไพล์ได้ แต่สวิตช์ GPU จะถูกละเว้นและคุณจะกลับไปใช้การประมวลผลด้วย CPU

## ขั้นตอนที่ 1 – เพิ่ม Aspose OCR ลงใน Build ของคุณ (วิธีเปิดใช้งาน GPU)

ก่อนอื่นบอกโครงการของคุณว่าต้องหาไลบรารี OCR ที่ไหน ใน Maven ให้เพิ่ม dependency ต่อไปนี้ในไฟล์ `pom.xml` ของคุณ:

```xml
<!-- Step 1: Include Aspose OCR for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **เคล็ดลับ:** หากคุณใช้ Gradle ให้ใช้ `implementation 'com.aspose:aspose-ocr:23.10'`. การอัปเดตไลบรารีให้เป็นเวอร์ชันล่าสุดจะทำให้คุณได้รับ kernel GPU ใหม่และการแก้บั๊กล่าสุด

เมื่อไลบรารีอยู่ใน classpath แล้ว เราจึงสามารถ **เปิดใช้งาน GPU** ใน OCR engine ได้จริง

## ขั้นตอนที่ 2 – สร้าง OCR Engine และเปิดใช้งาน GPU (วิธีเปิดใช้งาน GPU)

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Instantiate the OCR engine – this is the core object.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration.
        // This is the line that answers the question "how to enable gpu".
        ocrEngine.getConfig().setUseGpu(true);

        // Optional: If your system has more than one GPU, pick the one you want.
        // The device ID is zero‑based, so 0 refers to the first GPU.
        // ocrEngine.getConfig().setGpuDeviceId(0);

        // Step 2.3: Process the image and get the result.
        OcrResult ocrResult = ocrEngine.processImage("YOUR_DIRECTORY/high-res-photo.jpg");

        // Step 2.4: Print the recognized text – now you have converted photo to text.
        System.out.println(ocrResult.getText());
    }
}
```

> **ทำไมจึงสำคัญ:** การตั้งค่า `setUseGpu(true)` บอกไลบรารีเนทีฟพื้นฐานให้ย้ายงานเครือข่ายประสาทเทียมคอนโวลูชันหนักไปยัง GPU. บน RTX 3080 สมัยใหม่ ภาพเดียวที่ใช้เวลา 8 วินาทีบน CPU สามารถประมวลผลได้ภายในน้อยกว่า 1 วินาที. หากข้ามขั้นตอนนี้ คุณยังคง **จดจำข้อความจากรูปภาพ** ได้ แต่จะไม่ได้รับประโยชน์จากความเร็วที่เพิ่มขึ้น

## ขั้นตอนที่ 3 – ตรวจสอบว่า GPU ถูกใช้งานจริงหรือไม่

คุณอาจสงสัยว่า “GPU ทำงานจริงหรือเปล่า?” วิธีที่ง่ายที่สุดคือดูข้อความที่แสดงในคอนโซลของไลบรารี Aspose OCR เมื่อเปิดการบันทึก debug:

```java
// Enable verbose logging – helpful for confirming GPU usage.
ocrEngine.getConfig().setLogLevel(com.aspose.ocr.Config.LogLevel.DEBUG);
```

เมื่อรันโปรแกรม คุณจะเห็นบรรทัดเช่น:

```
[DEBUG] Using GPU device 0 (NVIDIA GeForce RTX 3080) for OCR processing.
```

หากไม่เห็นข้อความนั้น ให้ตรวจสอบการติดตั้งไดรเวอร์อีกครั้งและตรวจสอบว่า GPU มี compute capability ขั้นต่ำ (3.5 สำหรับ NVIDIA, 6.0 สำหรับ AMD)

## ขั้นตอนที่ 4 – การจัดการหลาย GPU และกรณีขอบ

### การเลือก GPU อื่น

หากเวิร์กสเตชันของคุณมี GPU มากกว่าหนึ่งตัว (เช่น GPU Intel แบบบูรณาการและการ์ด NVIDIA แยก) คุณสามารถกำหนดให้ใช้ GPU ที่เร็วกว่าได้:

```java
ocrEngine.getConfig().setGpuDeviceId(1); // 1 = second GPU in the system
```

### หากไม่พบ GPU?

Aspose OCR จะถอยกลับไปใช้ CPU อย่างอ่อนโยนเมื่อไม่พบ GPU ที่เหมาะสม. เพื่อหลีกเลี่ยงการถอยกลับโดยไม่มีการแจ้งเตือน คุณสามารถเพิ่มการตรวจสอบได้:

```java
if (!ocrEngine.getConfig().isGpuAvailable()) {
    throw new IllegalStateException("No compatible GPU found – cannot enable GPU acceleration.");
}
```

### ภาพขนาดใหญ่และขีดจำกัดหน่วยความจำ

การประมวลผลภาพ 100 MP ยังอาจทำให้หน่วยความจำของ GPU หมด. เทคนิคที่ใช้ได้คือการลดขนาดภาพ **ให้พอเหมาะ** เพื่อให้อยู่ในขีดจำกัดหน่วยความจำขณะยังคงความคมชัดของข้อความ:

```java
ocrEngine.getConfig().setMaxImageDimension(4096); // caps width/height to 4096px
```

### รูปแบบภาพที่รองรับ

Aspose OCR รองรับ JPEG, PNG, BMP, TIFF, และแม้กระทั่ง PDF. หากคุณต้องการ **ดึงข้อความจากภาพ** ที่เก็บในรูปแบบอื่น ให้แปลงเป็นหนึ่งในรูปแบบที่รองรับก่อนโดยใช้ไลบรารีอย่าง ImageIO

## ขั้นตอนที่ 5 – ผลลัพธ์ที่คาดหวังและการตรวจสอบ

เมื่อโปรแกรมทำงานเสร็จ คอนโซลจะพิมพ์ข้อความ OCR ดิบออกมา. สำหรับรูปถ่ายใบเสร็จทั่วไป คุณอาจเห็นข้อความเช่น:

```
Store: Coffee Corner
Date: 2026-02-25
Items:
  - Latte $4.50
  - Croissant $2.75
Total: $7.25
```

หากผลลัพธ์ดูเป็นอักษรผิดพลาด ให้พิจารณา:

* ตรวจสอบให้แน่ใจว่าภาพมีแสงสว่างเพียงพอและไม่ได้บีบอัดมากเกินไป
* ปรับค่า `setLanguage` หากข้อความไม่ใช่ภาษาอังกฤษ
* ยืนยันว่าเวอร์ชัน kernel GPU ตรงกับไดรเวอร์ของคุณ (เวอร์ชันไม่ตรงกันอาจทำให้เกิดข้อบกพร่องเล็กน้อย)

## ขั้นตอนที่ 6 – ไปไกลกว่านั้น: การประมวลผลเป็นชุดและการเรียกแบบอะซิงโครนัส

โครงการจริงมักต้อง **ดึงข้อความจากภาพ** จำนวนมาก. คุณสามารถใส่ตรรกะข้างต้นในลูปหรือใช้ `CompletableFuture` ของ Java เพื่อรันงาน OCR หลายงานพร้อมกัน, แต่ละงานใช้ stream ของ GPU แยก (หากฮาร์ดแวร์รองรับ). ตัวอย่างสั้น ๆ:

```java
import java.util.concurrent.*;
import java.nio.file.*;

public class BatchGpuOcr {
    public static void main(String[] args) throws Exception {
        ExecutorService pool = Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors());

        Files.list(Paths.get("photos/"))
             .filter(p -> p.toString().endsWith(".jpg"))
             .forEach(path -> pool.submit(() -> {
                 OcrEngine engine = new OcrEngine();
                 engine.getConfig().setUseGpu(true);
                 OcrResult result = engine.processImage(path.toString());
                 System.out.println("Result for " + path.getFileName() + ":\n" + result.getText());
             }));

        pool.shutdown();
        pool.awaitTermination(1, TimeUnit.HOURS);
    }
}
```

วิธีนี้ทำให้คุณ **แปลงรูปภาพเป็นข้อความ** ในระดับใหญ่ได้พร้อมยังคงใช้ประโยชน์จากการเร่งความเร็วด้วย GPU

## คำถามที่พบบ่อย (FAQ)

**Q: ทำงานบน macOS ได้หรือไม่?**  
A: ได้, ตราบใดที่คุณมี GPU ที่รองรับ Metal และไบนารี Aspose OCR สำหรับ macOS ที่เหมาะสม. การเรียก `setUseGpu(true)` ยังคงใช้ได้เช่นกัน

**Q: สามารถใช้ Community Edition ฟรีได้หรือไม่?**  
A: Community Edition มีเฉพาะการสรุปผลด้วย CPU. หากต้องการเปิดใช้งาน GPU คุณต้องใช้เวอร์ชันที่มีลิขสิทธิ์ (หรือทดลองเวอร์ชันที่รองรับ GPU)

**Q: หากต้อง **จดจำข้อความจากรูปภาพ** ในภาษาที่ไม่ใช่ภาษาอังกฤษต้องทำอย่างไร?**  
A: เรียก `ocrEngine.getConfig().setLanguage("spa")` สำหรับสเปน, `"fra"` สำหรับฝรั่งเศส ฯลฯ. แพ็คภาษาเหล่านี้มาพร้อมกับไลบรารี

**Q: มีวิธีรับคะแนนความเชื่อมั่นสำหรับแต่ละคำหรือไม่?**  
A: มี — `ocrResult.getWords()` คืนคอลเลกชันที่แต่ละอ็อบเจ็กต์ `Word` มีเมธอด `getConfidence()`

## สรุป

เราได้อธิบาย **วิธีเปิดใช้งาน GPU** สำหรับ Aspose OCR ใน Java, แสดงตัวอย่างที่สมบูรณ์และพร้อมรัน, และสำรวจปัญหาที่พบบ่อยเมื่อคุณต้อง **ดึงข้อความจากภาพ**, **แปลงรูปภาพเป็นข้อความ**, หรือ **จดจำข้อความจากรูปภาพ**. เพียงเปิดสวิตช์เดียวและอัปเดตไดรเวอร์ของคุณ คุณสามารถลดเวลาการเรียก OCR ได้หลายวินาทีและขยายการประมวลผลภาพจำนวนมากโดยไม่ต้องกังวล

พร้อมก้าวต่อไปหรือยัง? ลองส่งผลลัพธ์ OCR เข้าไปยัง pipeline การประมวลผลภาษาธรรมชาติ, หรือทดลองใช้ฟิลเตอร์การเตรียมภาพต่าง ๆ เพื่อเพิ่มความแม่นยำ. ท้องฟ้าเป็นขอบเขตเมื่อคุณผสาน OCR ที่ใช้ GPU กับเครื่องมือ Java สมัยใหม่

---

![Diagram illustrating how to enable GPU in Aspose OCR Java code – how to enable gpu](gpu-ocr-diagram.png)

*ข้อความแทนรูป:* "แผนภาพแสดงวิธีเปิดใช้งาน GPU ในโค้ด Aspose OCR Java – วิธีเปิดใช้งาน GPU"

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}