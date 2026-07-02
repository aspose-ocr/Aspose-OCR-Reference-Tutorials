---
category: general
date: 2026-06-28
description: เรียนรู้ตัวอย่าง Aspose OCR Java เพื่อสกัดข้อความจากภาพในโครงการ Java
  และตั้งค่าขีดจำกัดหน่วยความจำ GPU เพื่อให้ได้ผลลัพธ์ที่เร็วขึ้น.
draft: false
keywords:
- aspose ocr java example
- extract text from image java
- set gpu memory limit
- gpu accelerated OCR Java
- Aspose OCR licensing
language: th
og_description: ตัวอย่าง Aspose OCR Java ที่แสดงวิธีสกัดข้อความจากภาพด้วยโค้ด Java
  พร้อมตั้งค่าขีดจำกัดหน่วยความจำ GPU เพื่อประสิทธิภาพที่ดีที่สุด
og_title: ตัวอย่าง Aspose OCR Java – การสกัดข้อความอย่างรวดเร็วด้วย GPU
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn an Aspose OCR Java example to extract text from image Java projects
    and set GPU memory limit for faster results.
  headline: Aspose OCR Java Example – Extract Text from Image with GPU
  type: TechArticle
tags:
- Aspose OCR
- Java
- GPU
title: ตัวอย่าง Aspose OCR Java – ดึงข้อความจากภาพด้วย GPU
url: /th/java/advanced-ocr-techniques/aspose-ocr-java-example-extract-text-from-image-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตัวอย่าง Aspose OCR Java – ดึงข้อความจากภาพด้วย GPU

เคยสงสัยไหมว่า **extract text from image Java** applications อย่างไรโดยไม่ทำให้ CPU ของคุณทำงานช้าเกินไป? คุณไม่ได้เป็นคนเดียว ในหลายสถานการณ์จริง—เช่น การสแกนใบเสร็จ, การตรวจสอบบัตรประจำตัว, หรือการเก็บเอกสารจำนวนมาก—คอขวดคือเอนจิน OCR เอง  

ข่าวดี: **Aspose OCR Java example** นี้จะพาคุณผ่านโปรแกรมที่พร้อมรันเต็มรูปแบบซึ่งใช้การเร่งความเร็วด้วย GPU และยังแสดงวิธี **set GPU memory limit** เพื่อให้เซิร์ฟเวอร์ของคุณทำงานได้อย่างราบรื่น เมื่อจบคู่มือคุณจะมีคลาส Java ที่ทำงานได้ซึ่งอ่านไฟล์ภาพ, รัน OCR บน GPU, และพิมพ์ข้อความที่จดจำได้ลงคอนโซล ไม่มีการอ้างอิงที่คลุมเครือ มีเพียงโค้ดที่เป็นรูปธรรมและคำอธิบายที่ชัดเจน  

เราจะครอบคลุมทุกอย่างตั้งแต่การจัดการไลเซนส์จนถึงการปรับแต่ง GPU ดังนั้นไม่ว่าคุณจะเป็นนักพัฒนา Java ที่มีประสบการณ์หรือเพิ่งเริ่มต้นกับคอมพิวเตอร์วิทัศน์ คุณก็จะพบคุณค่าในที่นี้ เงื่อนไขเดียวที่ต้องมีคือสภาพแวดล้อมการพัฒนา Java (JDK 8 หรือใหม่กว่า) และการเข้าถึง GPU ที่รองรับ CUDA หรือ OpenCL  

---

## ข้อกำหนดเบื้องต้น

- **Java Development Kit (JDK) 8+** – คุณสามารถดาวน์โหลดได้จาก Oracle หรือ Adopt OpenJDK.  
- **Aspose.OCR for Java** library – รับไฟล์ JAR จากเว็บไซต์ Aspose หรือ Maven Central.  
- **A valid Aspose OCR license file** (`Aspose.OCR.Java.lic`). รุ่นทดลองฟรีใช้สำหรับทดสอบได้, แต่ไลเซนส์จะลบลายน้ำการประเมิน.  
- **GPU with CUDA or OpenCL support** – ตัวอย่างจะตรวจจับโหมดที่ดีที่สุดโดยอัตโนมัติ, แต่คุณต้องติดตั้งไดรเวอร์.  
- **An image to test** – PNG หรือ JPEG ที่ชัดเจนของใบเสร็จ, ป้าย, หรือข้อความพิมพ์ใด ๆ.  

หากรายการใดฟังดูแปลกใจ อย่าตื่นตระหนก ขั้นตอนต่อไปนี้จะพาคุณไปยังลิงก์ดาวน์โหลดที่แน่นอนและแสดงตำแหน่งที่ควรวางไฟล์  

## ขั้นตอนที่ 1: Aspose OCR Java Example – ตั้งค่าโปรเจกต์

แรกเริ่มให้สร้างโปรเจกต์ Maven ใหม่ (หรือโฟลเดอร์ธรรมดาหากคุณชอบใช้ `javac` ธรรมดา) เพิ่มการอ้างอิง Aspose OCR ลงในไฟล์ `pom.xml` ของคุณ:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Use the latest version -->
</dependency>
```

> **Pro tip:** Maven จะดึง dependencies ทั้งหมดที่เป็น transitive รวมถึงไลบรารีสนับสนุน GPU ด้วย, ดังนั้นคุณไม่ต้องตามหา JAR เพิ่มเติม  

วางไฟล์ `Aspose.OCR.Java.lic` ของคุณไว้ที่โฟลเดอร์รากของโปรเจกต์ (หรือโฟลเดอร์ใดก็ได้ที่คุณจะอ้างอิงต่อไป) **aspose ocr java example** ที่เรากำลังสร้างคาดหวังให้เส้นทางไลเซนส์เป็น `"Aspose.OCR.Java.lic"`  

## ขั้นตอนที่ 2: ใช้ไลเซนส์ Aspose OCR

ขั้นตอนการตั้งค่าไลเซนส์เป็นสิ่งสำคัญ—หากไม่มีไลเซนส์ เอนจิน OCR จะทำงานในโหมดประเมินผลและเพิ่มลายน้ำที่ผลลัพธ์ ด้านล่างเป็นโค้ดขั้นต่ำที่คุณต้องใช้:

```java
import com.aspose.ocr.*;

public class LicenseUtil {
    public static void applyLicense() throws Exception {
        License license = new License();
        // Adjust the path if your license file lives elsewhere
        license.setLicense("Aspose.OCR.Java.lic");
        System.out.println("Aspose OCR license applied successfully.");
    }
}
```

การเรียกใช้โค้ดนี้หนึ่งครั้งเมื่อตอนเริ่มแอปพลิเคชันของคุณจะรับประกันว่า **all subsequent OCR calls** จะได้รับการอนุญาตอย่างเต็มที่  

## ขั้นตอนที่ 3: ตั้งค่าการเร่งความเร็วด้วย GPU – กำหนดขีดจำกัดหน่วยความจำ GPU

ต่อมาคือส่วนที่สนุก: บอก Aspose ให้ใช้ GPU และโดยเลือก **set GPU memory limit** หากต้องการ ไลบรารีมาพร้อมกับ `GpuEngineOptions` ที่ให้คุณสลับโหมด GPU, เลือกอุปกรณ์, และจำกัดการใช้หน่วยความจำ การจำกัดหน่วยความจำเป็นประโยชน์บนเซิร์ฟเวอร์ที่แชร์ทรัพยากรเพื่อไม่ให้งาน OCR กิน GPU ทั้งหมด

```java
import com.aspose.ocr.gpu.*;

public class GpuConfig {
    public static GpuEngineOptions createOptions() {
        GpuEngineOptions gpuOptions = new GpuEngineOptions();
        gpuOptions.setEnableGpu(true);          // turn on GPU acceleration
        gpuOptions.setDeviceId(0);              // use the first GPU device
        gpuOptions.setMemoryLimitMb(2048);      // **set GPU memory limit** to 2 GB
        System.out.println("GPU options configured (memory limit = 2048 MB).");
        return gpuOptions;
    }
}
```

> **Why set a memory limit?** หากงาน OCR ของคุณเกี่ยวกับภาพขนาดใหญ่มากหรือรันหลายงานพร้อมกัน GPU อาจหมด VRAM อย่างรวดเร็วทำให้แอปพัง การจำกัดการจัดสรรจะทำให้กระบวนการอยู่ในขอบเขตปลอดภัยและให้โหลดงานอื่นทำงานร่วมกันได้อย่างสงบ  

## ขั้นตอนที่ 4: ดึงข้อความจาก Image Java – โหลดภาพ

เมื่อไลเซนส์และการตั้งค่า GPU พร้อมแล้ว เราจึงสามารถ **extract text from image Java** ได้ โค้ดตัวอย่างต่อไปนี้สร้าง `OcrEngine` ด้วยตัวเลือก GPU, โหลดไฟล์ภาพ, และรันการจดจำ

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply the license
        LicenseUtil.applyLicense();

        // 2️⃣ Set up GPU options (including memory limit)
        GpuEngineOptions gpuOptions = GpuConfig.createOptions();

        // 3️⃣ Create the OCR engine with GPU acceleration
        OcrEngine ocrEngine = new OcrEngine(gpuOptions);

        // 4️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        // Replace the placeholder with your actual image path
        ocrInput.add("YOUR_DIRECTORY/receipt.png");

        // 5️⃣ Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized Text (GPU):");
        System.out.println(ocrResult.getText());
    }
}
```

**Key points** ใน **aspose ocr java example** นี้:

- `OcrInput.add()` สามารถรับหลายภาพ; เอนจินจะประมวลผลตามลำดับ  
- `ocrResult.getText()` คืนค่าเป็นสตริงข้อความธรรมดา, รักษาการขึ้นบรรทัดใหม่แต่ไม่มีข้อมูลการจัดวางรูปแบบ  
- ทั้งกระบวนการทำงานบน GPU ซึ่งอาจเร็ว **5‑10×** เทียบกับการประมวลผลด้วย CPU เพียงอย่างเดียวสำหรับภาพความละเอียดสูง  

## ขั้นตอนที่ 5: รันเดโมและตรวจสอบผลลัพธ์

คอมไพล์และรันโปรแกรม:

```bash
mvn compile exec:java -Dexec.mainClass=GpuOcrDemo
```

หากทุกอย่างเชื่อมต่ออย่างถูกต้อง คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Aspose OCR license applied successfully.
GPU options configured (memory limit = 2048 MB).
Recognized Text (GPU):
Item   Qty   Price
Apple   2    $1.20
Banana  5    $0.75
Total          $5.85
```

ข้อความที่ได้จะขึ้นอยู่กับภาพของคุณ แต่สิ่งสำคัญคือคอนโซลจะแสดง **the recognized text** โดยไม่มีลายน้ำ “Evaluation version” หากคุณเจอข้อผิดพลาด `CUDA driver not found` ให้ตรวจสอบว่าไดรเวอร์ GPU ของคุณเป็นเวอร์ชันล่าสุดและ CUDA toolkit อยู่ใน PATH ของระบบ  

## ข้อผิดพลาดทั่วไปและวิธีหลีกเลี่ยง

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `OutOfMemoryError: CUDA out of memory` | GPU memory exceeded | Lower `setMemoryLimitMb` (e.g., 1024) or process smaller image chunks. |
| `LicenseException` | License file missing or path wrong | Ensure `Aspose.OCR.Java.lic` is reachable and the path matches. |
| No text returned | Image too blurry or wrong color space | Pre‑process the image (increase contrast, convert to grayscale) before feeding it to OCR. |
| GPU not used | `setEnableGpu(false)` or driver missing | Verify `gpuOptions.setEnableGpu(true)` and reinstall GPU drivers. |

## การขยายตัวอย่าง

ตอนนี้คุณมี **aspose ocr java example** ที่แข็งแรงแล้ว อาจต้องการทำต่อ:

- **Batch process a folder** – วนลูปไฟล์และบันทึกผลลงฐานข้อมูล  
- **Detect language** – ใช้ `ocrEngine.setLanguage(OcrLanguage.English)` หรือเพิ่มหลายภาษา  
- **Apply post‑processing** – ทำความสะอาดสตริงดิบด้วย regex หรือส่งไปยังตัวตรวจสอบการสะกด  

ส่วนขยายเหล่านี้ใช้โค้ดการตั้งค่าไลเซนส์และ GPU เดิม ดังนั้นคุณเพียงแค่เพิ่มตรรกะธุรกิจเท่านั้น  

## ความคิดสุดท้าย

คุณเพิ่งเห็น **aspose ocr java example** ที่ **extracts text from image Java** พร้อม **setting GPU memory limit** เพื่อประสิทธิภาพที่มั่นคง แนวคิดหลัก—ตั้งไลเซนส์ล่วงหน้า, ตั้งค่า GPU, ป้อนภาพ, อ่านข้อความ—สามารถนำไปใช้ซ้ำได้ในโครงการหลายพันโครงการ ตั้งแต่เครื่องสแกนใบเสร็จจนถึงระบบกรอกฟอร์มอัตโนมัติ  

จากนี้คุณสามารถทดลองค่าต่าง ๆ ของ `GpuEngineOptions`, ลองภาพขนาดใหญ่ขึ้น, หรือรวมขั้นตอน OCR เข้าใน microservice ของ Spring Boot ได้เลย ขอบเขตของคุณไม่มีที่สิ้นสุด และด้วยการเร่งความเร็วด้วย GPU ขีดจำกัดก็สูงกว่าที่เคย  

มีคำถามหรืออยากให้ช่วยปรับค่าหน่วยความจำให้เหมาะกับฮาร์ดแวร์ของคุณ? แสดงความคิดเห็นด้านล่าง แล้วขอให้สนุกกับการเขียนโค้ด!

![แผนภาพตัวอย่าง Aspose OCR Java แสดงกระบวนการจากการป้อนภาพ → OCR เร่งด้วย GPU → ผลลัพธ์ข้อความ](https://example.com/images/aspose-ocr-java-example-diagram.png "แผนภาพตัวอย่าง Aspose OCR Java")

## คุณควรเรียนรู้อะไรต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานแบบอื่นในโครงการของคุณ  

- [วิธีตั้งค่าไลเซนส์และตรวจสอบไลเซนส์ Aspose.OCR ใน Java](/ocr/english/java/ocr-basics/set-license/)  
- [ดึงข้อความจาก Image Java ด้วยโหมด Detect Areas ของ Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)  
- [แปลงภาพเป็นข้อความใน Java ด้วย Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}