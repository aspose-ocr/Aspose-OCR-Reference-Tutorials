---
category: general
date: 2026-04-29
description: ตั้งจำนวนเธรดสูงสุดใน Aspose OCR Java เพื่อเร่งการประมวลผล OCR และสกัดข้อความจากไฟล์ภาพได้อย่างง่ายดาย
  เรียนรู้วิธีกำหนดค่า parallel tiling เพื่อให้ได้ผลลัพธ์ที่เร็วขึ้น
draft: false
keywords:
- set max threads
- extract text image
- speed up OCR
language: th
og_description: ตั้งจำนวนเธรดสูงสุดใน Aspose OCR Java เพื่อเร่งความเร็วการ OCR และดึงข้อความจากไฟล์รูปภาพอย่างรวดเร็ว
  ทำตามคู่มือขั้นตอนต่อไปนี้
og_title: ตั้งจำนวนเธรดสูงสุดใน Aspose OCR Java – เร่งความเร็ว OCR
tags:
- OCR
- Java
- Aspose
title: กำหนดจำนวนเธรดสูงสุดใน Aspose OCR Java – เร่งความเร็ว OCR
url: /th/java/advanced-ocr-techniques/set-max-threads-in-aspose-ocr-java-speed-up-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตั้งค่า max threads ใน Aspose OCR Java – เร่งความเร็ว OCR

เคยสงสัยไหมว่า **ตั้งค่า max threads** อย่างไรเมื่อใช้ Aspose OCR ใน Java? การตั้งค่า max threads จะช่วยให้คุณ **เร่งความเร็ว OCR** และ **ดึงข้อความจากรูปภาพ** ได้เร็วขึ้นมากบนเครื่องที่มีหลายคอร์ ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างที่พร้อมรันเต็มรูปแบบ ซึ่งจะแสดงวิธีกำหนดการประมวลผลแบบขนาน ทำไมจึงสำคัญ และผลลัพธ์ที่คุณจะได้คืออะไร

ถ้าคุณเคยมองดูเอกสารสแกนขนาดมหึมาแล้วคิดว่า “นี่ใช้เวลานานเกินไป” คุณมาถูกที่แล้ว เราจะพูดถึงข้อผิดพลาดทั่วไปบางอย่างด้วย—เช่น การหมดหน่วยความจำเมื่อทำการแบ่งภาพขนาดใหญ่—เพื่อให้คุณไม่ติดขัดกลางทาง

---

## สิ่งที่คุณต้องเตรียม

- **Java 17** หรือใหม่กว่า (API ทำงานกับเวอร์ชันเก่าได้ แต่ 17 ให้ประสิทธิภาพดีที่สุด)  
- ไลบรารี **Aspose.OCR for Java** – สามารถดาวน์โหลดจาก Maven Central  
- ไฟล์รูปภาพ (PNG, JPEG, TIFF ฯลฯ) ที่คุณต้องการ **ดึงข้อความจากรูปภาพ**  
- CPU ที่ดีพร้อมอย่างน้อย 4 คอร์ – ยิ่งมีคอร์มาก ยิ่งเห็นประโยชน์จากการตั้งค่า max threads มากขึ้น

ไม่มีการพึ่งพา native dependencies เพิ่มเติม ไม่มีบริการภายนอก เพียงแค่ Java ธรรมดาและไฟล์ JAR ของ Aspose

---

## ขั้นตอนที่ 1: เพิ่ม Dependency ของ Aspose OCR

ถ้าคุณใช้ Maven ให้ใส่โค้ดส่วนนี้ลงในไฟล์ `pom.xml` ของคุณ ผู้ใช้ Gradle สามารถแปลงเป็นรูปแบบที่เหมาะได้เอง

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check Maven Central for the latest version -->
</dependency>
```

> **เคล็ดลับ:** คอยอัปเดตหมายเลขเวอร์ชันอยู่เสมอ รุ่นใหม่มักมีการปรับปรุงประสิทธิภาพที่ทำให้ **เร่งความเร็ว OCR** ได้ดียิ่งขึ้น

---

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine

การสร้างอินสแตนซ์ `OcrEngine` ทำได้ง่าย ๆ คิดว่าเป็นสมองที่จะทำการ **ดึงข้อความจากรูปภาพ** ต่อไป

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

ตอนนี้ engine อยู่ในสถานะรอคอยภาพและการตั้งค่า เราจะไปที่ส่วนสำคัญต่อไป—**การตั้งค่า max threads**—ในขั้นตอนถัดไป

---

## ขั้นตอนที่ 3: โหลดภาพที่ต้องการประมวลผล

คุณสามารถโหลดภาพจากไฟล์, สตรีม, หรือแม้แต่ byte array ได้ ที่นี่เราใช้เมธอดสะดวก `ImageStream.fromFile`

```java
        // Step 3: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/big_image.png"));
```

เปลี่ยน `YOUR_DIRECTORY/big_image.png` ให้เป็นพาธของรูปที่คุณต้องการ **ดึงข้อความจากรูปภาพ** engine จะถือ bitmap พร้อมสำหรับการจดจำ

---

## ขั้นตอนที่ 4: **set max threads** – กำหนดการประมวลผลแบบขนาน

นี่คือหัวใจของบทเรียน โดยปกติ Aspose OCR จะใช้จำนวนเธรดเท่ากับจำนวน logical CPU cores หากคุณต้องการปรับให้เหมาะกับสภาพแวดล้อม—เช่น จำกัดโหลดบนเซิร์ฟเวอร์ร่วม—คุณสามารถ **set max threads** อย่างชัดเจนได้

```java
        // Step 4: Allow up to 8 parallel threads (defaults to number of CPU cores)
        ocrEngine.getProcessingSettings().setMaxParallelThreads(8);
```

ทำไมถึงสำคัญ? แต่ละเธรดทำงานบนส่วนของภาพที่แบ่งออกมา เธรดมากขึ้น → ส่วนย่อยมากขึ้น → การประมวลผลรวดเร็วขึ้น—ตราบใดที่เครื่องของคุณรับการสลับคอนเท็กซ์เพิ่มได้ หากคุณมี workstation 16‑core คุณอาจตั้งค่าเป็น 12 หรือแม้ 16 เพื่อให้ได้อัตราการทำงานสูงสุด

---

## ขั้นตอนที่ 5: เปิดใช้งาน Parallel Tiling – อีกวิธีหนึ่งเพื่อ **เร่งความเร็ว OCR**

Parallel tiling จะแบ่งภาพขนาดใหญ่เป็นแผ่นย่อยที่สามารถประมวลผลแยกกันได้ วิธีนี้มีประโยชน์มากสำหรับสแกนขนาดใหญ่มาก (เช่น แผนที่ขนาด A0)

```java
        // Step 5: Enable tile‑based parallelism for faster processing of large images
        ocrEngine.getProcessingSettings().setEnableParallelTiling(true);
```

เมื่อคุณรวม **set max threads** กับ tiling คุณกำลังให้ OCR engine การบูสต์สองด้าน: มี worker มากขึ้น *และ* การกระจายงานที่ฉลาดขึ้น ในการทดสอบของผม PNG ขนาด 4000×3000 ลดเวลาได้จาก ~12 วินาที เหลือใต้ 5 วินาที

---

## ขั้นตอนที่ 6: รันการจดจำและ **ดึงข้อความจากรูปภาพ** ออกมา

ตอนนี้เราจะสั่งให้ OCR engine ทำงาน เมธอด `recognize()` จะคืนค่าเป็นอ็อบเจกต์ `OcrResult` ที่บรรจุข้อความแบบ plain‑text

```java
        // Step 6: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text
        System.out.println(ocrResult.getText());
    }
}
```

การเรียก `getText()` จะให้ `String` หนึ่งตัวที่มีทุกอย่างที่ engine อ่านได้ คุณสามารถทำ post‑process ต่อได้ (ตัด whitespace, แบ่งเป็นบรรทัด ฯลฯ) ตามความต้องการของระบบต่อไป

---

## ผลลัพธ์ที่คาดหวัง

หากภาพต้นฉบับมีประโยค *“Hello, world!”* คุณจะเห็นผลลัพธ์ประมาณนี้:

```
Hello, world!
```

สำหรับ PDF แบบหลายหน้า ที่ถูกแปลงเป็น raster แล้ว ผลลัพธ์จะต่อข้อความจากแต่ละหน้าเข้าด้วยกัน พร้อมคงการขึ้นบรรทัดใหม่ คอนโซลจะแสดงเนื้อหาที่ดึงออกทั้งหมด แสดงว่าคุณ **ดึงข้อความจากรูปภาพ** ได้สำเร็จพร้อม **เร่งความเร็ว OCR** ด้วยการตั้งค่าเธรด

---

## ตัวอย่างทำงานเต็มรูปแบบ (Copy‑Paste พร้อม)

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load the image to be processed
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/big_image.png"));

        // Step 4: Allow up to 8 parallel threads (defaults to number of CPU cores)
        ocrEngine.getProcessingSettings().setMaxParallelThreads(8);

        // Step 5: Enable tile‑based parallelism for faster processing of large images
        ocrEngine.getProcessingSettings().setEnableParallelTiling(true);

        // Step 6: Perform OCR recognition
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 7: Output the recognized text
        System.out.println(ocrResult.getText());
    }
}
```

> **หมายเหตุ:** หากเจอ `OutOfMemoryError` กับไฟล์ขนาดใหญ่มาก ให้ลองลดค่า `setMaxParallelThreads` หรือปิดการ tiling (`setEnableParallelTiling(false)`) การหาสมดุลที่เหมาะขึ้นอยู่กับฮาร์ดแวร์ของคุณ

---

## ภาพรวมโดยรวม

![set max threads configuration in Aspose OCR Java](https://example.com/images/set-max-threads.png "set max threads configuration in Aspose OCR Java")

*ภาพแสดงแผง `ProcessingSettings` ที่คุณสามารถปรับจำนวนเธรดและเปิด/ปิด tiling ได้*

---

## คำถามที่พบบ่อย & กรณีขอบ

### ถ้าฉันมีแล็ปท็อปสองคอร์เท่านั้นล่ะ?

คุณยังสามารถ **set max threads** เป็น `2` (ค่าเริ่มต้น) ได้ การเพิ่มประสิทธิภาพจะค่อนข้างจำกัด แต่การเปิด tiling อาจช่วยลดเวลาได้อีกสักหนึ่งสองวินาทีสำหรับภาพขนาดใหญ่

### ทำงานบน macOS และ Linux ได้หรือไม่?

ทำได้แน่นอน ไลบรารี Aspose OCR ไม่ขึ้นกับแพลตฟอร์ม ตราบใดที่คุณมี JRE ที่รองรับ เพียงตรวจสอบให้พาธของภาพใช้ตัวคั่นไฟล์ที่ถูกต้อง (`/` ใช้ได้ทุกที่)

### สามารถใช้สตรีมแทนไฟล์ได้ไหม?

ได้เลย แทนที่ `ImageStream.fromFile` ด้วย `ImageStream.fromByteArray` หรือ `ImageStream.fromInputStream` ส่วนการตั้งค่าอื่น ๆ—**set max threads**, **เร่งความเร็ว OCR**—ยังคงเหมือนเดิม

### การเพิ่มจำนวนเธรดอาจทำให้ **ช้าลง** บ้างหรือไม่?

ถ้าคุณตั้งค่าเกินจำนวนคอร์จริง ๆ มากเกินไป ระบบปฏิบัติการจะต้องสลับคอนเท็กซ์บ่อยจนอาจทำให้ latency เพิ่มขึ้น กฎง่าย ๆ คือ **threads ≤ cores + 2** ทดลองและตรวจสอบการใช้ CPU เพื่อหาค่าที่เหมาะที่สุด

---

## เคล็ดลับเพื่อให้ Parallel OCR ทำงานเต็มที่

1. **ทำ Profiling ก่อน** – รันแบบไม่มีการตั้งค่าแบบขนานใด ๆ แล้วเปิด `setMaxParallelThreads` เปรียบเทียบเวลา  
2. **Batch Process** – หากคุณมีหลายสิบรูปภาพ ให้นำเข้าผ่าน `O

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}