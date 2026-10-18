---
category: general
date: 2026-02-27
description: เรียนรู้วิธีใช้ OCR ใน Java เพื่อดึงข้อความจากภาพในไฟล์ TIFF และ PDF
  ด้วยการประมวลผลแบบขนานของ Aspose OCR คู่มือที่เร็วและง่าย.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: th
og_description: เรียนรู้วิธีใช้ OCR ใน Java เพื่อดึงข้อความจากภาพในไฟล์ TIFF และ PDF
  ด้วยการประมวลผลแบบขนานของ Aspose OCR.
og_title: วิธีใช้ OCR ใน Java – การประมวลผลแบบขนานกับ Aspose
tags:
- OCR
- Java
- Aspose
title: วิธีใช้ OCR ใน Java – การประมวลผลแบบขนานกับ Aspose
url: /th/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน Java – การประมวลผลแบบขนานกับ Aspose

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อความจากเอกสารสแกนโดยไม่ต้องเสียแรงไหม? คุณไม่ได้เป็นคนเดียว นักพัฒนามักเจออุปสรรคเมื่อต้องอ่านข้อความจากภาพ—โดยเฉพาะ TIFF และ PDF—พร้อมกับต้องคำนึงถึงประสิทธิภาพ  

ในบทเรียนนี้เราจะสาธิตโซลูชันที่พร้อมรันเต็มรูปแบบที่ **ดึงข้อความจากภาพใน Java** ด้วย Aspose OCR, เปิดการประมวลผลแบบขนาน, และแม้กระทั่งจำกัดจำนวนเธรดให้คุณได้ ด้วยโค้ดเดียวคุณจะสามารถ **ทำ OCR บน PDF** และ **ดึงข้อความจาก TIFF** ได้เร็วกว่าแบบใช้เธรดเดียวหลายเท่า

> **สิ่งที่คุณจะได้เรียนรู้**  
> * คำอธิบายชัดเจนว่าทำไมการทำ OCR แบบขนานจึงสำคัญ  
> * โปรแกรม Java ฉบับเต็ม (ไม่มีการขาด import)  
> * เคล็ดลับการปรับการใช้เธรดและการจัดการกับปัญหาที่พบบ่อย  

## ความต้องการเบื้องต้น

- Java 8 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ JDK 11 ด้วย)  
- ไลบรารี Aspose.OCR for Java – สามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central (`com.aspose:aspose-ocr`)  
- ไฟล์ภาพ (`.tif`, `.tiff`) หรือ PDF ที่ต้องการประมวลผล  
- RAM ปริมาณพอสมควร—การประมวลผลแบบขนานจะสร้างเธรดหลายตัว แต่ Aspose ใช้หน่วยความจำอย่างมีประสิทธิภาพ  

ถ้าคุณมีทั้งหมดนี้แล้ว ไปต่อกันเลย

![แผนภาพแสดงกระบวนการ OCR – วิธีใช้ OCR ใน Java ด้วยการประมวลผลแบบขนาน](how-to-use-ocr-pipeline.png)

*ข้อความแทนภาพ: แผนภาพตัวอย่างการใช้ OCR*

---

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่ม Aspose OCR

### ทำไมขั้นตอนนี้สำคัญ

ก่อนที่คุณจะ **ทำ OCR บน PDF** หรือภาพใด ๆ ไลบรารีต้องอยู่ใน classpath ของคุณ หากไม่มีจะทำให้คอมไพเลอร์โยน `ClassNotFoundException` และคุณจะติดอยู่ที่ขั้นตอนที่สอง

### วิธีทำ

หากคุณใช้ Maven ให้เพิ่ม dependency:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

สำหรับ Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **เคล็ดลับ:** ให้เวอร์ชันของไลบรารีสอดคล้องกับบันทึกการปล่อยของ Aspose; เวอร์ชันใหม่มักมีการปรับปรุงประสิทธิภาพสำหรับการประมวลผลแบบขนาน

---

## ขั้นตอนที่ 2: สร้าง OCR Engine และเปิดการประมวลผลแบบขนาน

### ทำไมขั้นตอนนี้สำคัญ

โดยค่าเริ่มต้น Aspose OCR ทำงานบนเธรดเดียว เมื่อคุณป้อน PDF หลายหน้า หรือชุด TIFF จำนวนมาก เครื่องจะประมวลผลแต่ละหน้าเรียงต่อกัน—ช้าและไม่มีประสิทธิภาพ การเปิดการประมวลผลแบบขนานทำให้ CPU สามารถประมวลผลหลายหน้าได้พร้อมกัน ลดเวลาได้อย่างมหาศาล

### โค้ด

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**คำอธิบายบรรทัดสำคัญ**

- `setUseParallelProcessing(true)`: บอก Aspose ให้แบ่งงานไปยังคอร์ CPU ที่มีอยู่  
- `setMaxThreads(...)`: คุณสามารถจำกัดจำนวนเธรดในพูลได้ หากทำงานบนเซิร์ฟเวอร์ที่แชร์หรืออยากเหลือทรัพยากรให้บริการอื่น  
- `processImage(inputPath)`: ทำงานได้ทั้งไฟล์ภาพและ PDF ดังนั้นการเรียกเดียวกันนี้ **ทำ OCR บน PDF** และบน TIFF ได้เช่นกัน  

---

## ขั้นตอนที่ 3: จัดการกับประเภทอินพุตที่แตกต่าง – PDF vs. TIFF

### ทำไมขั้นตอนนี้สำคัญ

แม้ `processImage` จะรับพาธเป็นสตริง แต่การจัดการภายในแตกต่างกัน PDF มักมีหลายหน้า ซึ่งแต่ละหน้าจะกลายเป็นงาน OCR แยกกัน ส่วน TIFF อาจเป็นหน้าเดียวหรือหลายหน้า; Aspose จะถือแต่ละเฟรมเป็นหน้า

### สิ่งที่ควรระวัง

| อินพุต | ปัญหาที่พบบ่อย | วิธีแก้แนะนำ |
|------|----------------|-----------------|
| PDF | PDF ขนาดใหญ่อาจทำให้หน่วยความจำหมดหากโหลดทุกหน้าในครั้งเดียว | ใช้ `ocrEngine.getConfig().setMemoryOptimization(true);` (มีในเวอร์ชันใหม่) |
| TIFF หลายหน้า | TIFF รุ่นเก่าบางไฟล์ใช้การบีบอัดที่ไม่รองรับ | แปลงเป็นฟอร์แมตที่รองรับก่อน หรือใช้ตัวช่วย `TiffImage` ของ Aspose |

ต่อไปเป็นโค้ดสั้น ๆ ที่แสดงวิธีตรวจจับประเภทไฟล์และบันทึกข้อความแจ้งผู้ใช้:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## ขั้นตอนที่ 4: ตรวจสอบผลลัพธ์ – ควรเห็นอะไรบ้าง?

เมื่อโปรแกรมทำงานเสร็จ คุณจะเห็นข้อความที่ดึงออกมาจากภาพแสดงบนคอนโซล สำหรับใบแจ้งหนี้สแกนง่าย ๆ ผลลัพธ์อาจมีลักษณะดังนี้:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

หาก OCR มีปัญหากับหน้าหนึ่ง Aspose จะใส่บรรทัด placeholder เช่น `[Unrecognizable]` คุณสามารถกรองบรรทัดเหล่านี้ออกในภายหลังหากต้องการข้อมูลที่สะอาด

**การตรวจสอบอย่างรวดเร็ว**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## ขั้นตอนที่ 5: ปรับประสิทธิภาพ – เมื่อไหร่ควรปรับจำนวนเธรด

### ทำไมขั้นตอนนี้สำคัญ

การเพิ่มเธรดไม่ได้หมายความว่าจะเร็วขึ้นเสมอไป บนแล็ปท็อป 4‑คอร์ การเปิด 8 เธรดอาจทำให้เกิด overhead จากการสลับคอนเท็กซ์ ในทางกลับกันบนเซิร์ฟเวอร์ 32‑คอร์ คุณอาจต้องการใช้พลังเต็มที่

### วิธีหาจุดที่เหมาะสม

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

รันโปรแกรมด้วยการตั้งค่าต่าง ๆ แล้ววัดเวลา:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

บันทึกเวลา, เลือกการตั้งค่าที่ให้ throughput ที่ดีที่สุด, แล้วนำไปใช้ในสภาพแวดล้อมการผลิต

---

## ขั้นตอนที่ 6: ขยายตัวอย่าง – การประมวลผลเป็นชุดหลายไฟล์

หากคุณต้องการ **ดึงข้อความจากภาพใน Java** จากโฟลเดอร์ทั้งหมด ให้ห่อรอบตรรกะหลักด้วยลูป:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

รูปแบบนี้สเกลได้ดีเพราะ engine จะประมวลผลหน้าของแต่ละไฟล์แบบขนานอยู่แล้ว ลูปภายนอกทำงานแบบต่อเนื่อง แต่คุณก็สามารถส่งแต่ละไฟล์ไปยัง `ExecutorService` หากต้องการใช้ CPU จำนวนมากเต็มที่

---

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| `OutOfMemoryError` | โหลดหน้ามากเกินไปพร้อมกัน (โดยเฉพาะกับ PDF ขนาดใหญ่) | เปิดการปรับแต่งหน่วยความจำ (`setMemoryOptimization(true)`) หรือประมวลผล PDF ทีละหน้าโดยใช้ `processPage` |
| ตัวอักษรบิดเบี้ยว | การตั้งค่าภาษา/charset ไม่ถูกต้อง | เรียก `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` หรือ enum ภาษาที่เหมาะสม |
| ประสิทธิภาพช้าแม้เปิด parallel flag | ระบบปฏิบัติการจำกัดการสร้างเธรดหรือ JVM มี heap ขนาดเล็ก | เพิ่มพารามิเตอร์ `-Xmx` ของ heap, ตรวจสอบข้อจำกัดของ OS (`ulimit -u`) |
| ผลลัพธ์เป็นค่าว่าง | ความละเอียดของภาพอินพุต < 300 dpi | ขยายภาพก่อน OCR หรือใช้สแกนเนอร์ที่ส่งออกความละเอียดสูงกว่า |

---

## สรุป – สิ่งที่เราได้ครอบคลุม

- **วิธีใช้ OCR** ใน Java ด้วย `OcrEngine` ของ Aspose  
- การเปิด **การประมวลผลแบบขนาน** เพื่อเร่ง **ทำ OCR บน PDF** และ **ดึงข้อความจาก TIFF**  
- การปรับจำนวนเธรดเพื่อประสิทธิภาพสูงสุด  
- การจัดการกรณีขอบเช่น PDF ขนาดใหญ่, TIFF หลายหน้า, และการตั้งค่าภาษา  
- การขยายตัวอย่างไฟล์เดียวเป็นตัวประมวลผลแบบชุดสำหรับงานจริง

---

## ขั้นตอนต่อไป

ตอนนี้คุณได้เชี่ยวชาญพื้นฐานแล้ว ลองสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

- **ดึงข้อความจากภาพใน Java** จากบันทึกมือ (เปิด `setHandwritingRecognition(true)`)  
- ผสานผลลัพธ์ OCR กับ Apache Tika เพื่อดึงเมตาดาต้า  
- เก็บผลลัพธ์ใน Elasticsearch เพื่อทำเอกสาร searchable  
- ใช้ OCR ของ Aspose กับภาษาอื่น ๆ เช่น Python หรือ .NET—หลักการยังคงเหมือนเดิม  

ลองปรับเปลี่ยนขีดจำกัดเธรด, ฟอร์แมตภาพ, และแพ็คเกจภาษาให้หลากหลาย ยิ่งคุณทดลองมากเท่าไหร่ คุณก็จะเข้าใจการแลกเปลี่ยนระหว่างความเร็วและความแม่นยำได้ดียิ่งขึ้น

---

### Happy coding!

หากคุณเจออุปสรรคหรือมีไอเดียสำหรับการปรับแต่งเพิ่มเติม แสดงความคิดเห็นด้านล่างได้เลย ฉันพร้อมพูดคุยเรื่องเทคนิค OCR เสมอ—ไม่มีความเครียด แค่โค้ดเท่านั้น

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}