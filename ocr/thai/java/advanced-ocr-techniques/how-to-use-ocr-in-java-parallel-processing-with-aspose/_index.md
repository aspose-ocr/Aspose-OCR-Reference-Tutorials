---
category: general
date: 2026-10-24
description: เรียนรู้วิธีทำ OCR บนไฟล์ PDF และรูปภาพ TIFF ด้วย Java โดยใช้การประมวลผลแบบขนานของ
  Aspose OCR คู่มือที่เร็วและเชื่อถือได้สำหรับนักพัฒนา
draft: false
keywords:
- perform ocr pdf
- extract image text
- java ocr library
- process scanned pdf
- aspose ocr maven
lastmod: 2026-10-24
og_description: ทำ OCR บนไฟล์ PDF ด้วย Java อย่างรวดเร็วด้วยการประมวลผลแบบขนานของ
  Aspose OCR คู่มือนี้จะแสดงวิธีเปิดใช้งานการทำ OCR แบบหลายเธรด, กำหนดขีดจำกัดของเธรด,
  และสกัดข้อความจากไฟล์ PDF และภาพ TIFF อย่างมีประสิทธิภาพ
og_image_alt: Diagram of Java OCR pipeline with parallel processing using Aspose OCR
og_title: ทำ OCR บน PDF ด้วย Java – การประมวลผลแบบขนานกับ Aspose
schemas:
- author: Aspose
  dateModified: '2026-10-24'
  description: Learn how to perform OCR on PDF and TIFF images in Java using Aspose
    OCR's parallel processing. Fast, reliable guide for developers.
  headline: How to perform OCR on PDF in Java with parallel processing
  type: TechArticle
- questions:
  - answer: Yes, Aspose OCR’s parallel engine runs on Windows, Linux, and macOS as
      long as the JVM can create native threads.
    question: Does the parallel mode work on any operating system?
  - answer: Absolutely—pass the password to `processImage` via the overload that accepts
      a `PdfLoadOptions` object.
    question: Can I process password‑protected PDFs?
  - answer: Aspose OCR supports Java 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  - answer: For images under 300 dpi, accuracy drops to around 80 %; increasing the
      resolution to 400 dpi typically pushes it above 95 %.
    question: How accurate is the OCR for low‑resolution scans?
  - answer: Yes, a valid Aspose license removes evaluation limits and enables full‑performance
      features like parallel processing.
    question: Is a commercial license required for production use?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- parallel processing
- PDF
title: วิธีทำ OCR บน PDF ด้วย Java พร้อมการประมวลผลแบบขนาน
url: /th/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บน PDF ด้วย Java พร้อมการประมวลผลแบบขนาน

เคยสงสัย **วิธีใช้ OCR** เพื่อดึงข้อความจากเอกสารสแกนโดยไม่ต้องเหนื่อยไหม? ในบทแนะนำนี้คุณจะได้เรียนรู้วิธี **ทำ OCR PDF** ด้วย Java โดยใช้การประมวลผลแบบขนานในตัวของ Aspose OCR วิธีนี้ทำงานได้ทั้งแหล่ง PDF และ TIFF ลดเวลาในการประมวลผลอย่างมาก และให้คุณควบคุมการใช้เธรดได้อย่างละเอียด เมื่อเสร็จคุณจะมีคลาส Java ที่พร้อมรันซึ่งสามารถดึงข้อความจากรูปภาพของ PDF ที่สแกนหรือ TIFF หลายหน้าได้ในส่วนหนึ่งของเวลาที่โซลูชันแบบใช้เธรดเดียวต้องใช้

## คำตอบอย่างรวดเร็ว
- **Parallel OCR ทำอะไร?** มันจะแบ่งหน้าออกไปยังหลายคอร์ของ CPU ทำให้หลายหน้าถูกประมวลผลพร้อมกัน.  
- **ใช้ไลบรารีอะไร?** Aspose.OCR สำหรับ Java ที่สามารถดาวน์โหลดได้จาก Maven Central.  
- **ต้องการไลเซนส์หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการพัฒนา; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์.  
- **สามารถจำกัดจำนวนเธรดได้หรือไม่?** ได้ — ใช้ `setMaxThreads(int)` เพื่อจำกัดจำนวนเธรดในพูล.  
- **โซลูชันนี้เข้ากันได้กับ Java 8 และรุ่นใหม่หรือไม่?** แน่นอน มันทำงานบน Java 8, 11, 17 และรุ่นต่อๆ ไป.

## perform OCR PDF คืออะไร?
`perform OCR PDF` หมายถึงการดึงข้อความที่ค้นหาได้และแก้ไขได้จากเอกสาร PDF ที่สแกนโดยใช้การจดจำอักขระด้วยแสง (OCR) Aspose OCR จะอ่านภาพเรสเตอร์ของแต่ละหน้า รันเอนจินการจดจำ และคืนข้อความ Unicode ธรรมดาที่คุณสามารถจัดเก็บ ดัชนี หรือประมวลผลต่อได้.

## ทำไมต้องใช้การประมวลผลแบบขนานของ Aspose OCR?
Aspose OCR รองรับ **รูปแบบอินพุตกว่า 50** (รวมถึง PDF, TIFF, JPEG, PNG, BMP) และสามารถจัดการ **เอกสารหลายร้อยหน้า** ได้โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ การประมวลผลแบบขนานโดยทั่วไปจะลดเวลาในการทำงานลง **30‑70 % บนแล็ปท็อป 4‑คอร์** และสูงสุด **80 % บนเซิร์ฟเวอร์ 32‑คอร์** ตามชุดมาตรฐานการทดสอบของ Aspose.

## ข้อกำหนดเบื้องต้น
- Java 8 หรือใหม่กว่า (โค้ดนี้ยังคอมไพล์ได้กับ JDK 11 ด้วย).  
- ไลบรารี Aspose.OCR สำหรับ Java – คุณสามารถดาวน์โหลด JAR ล่าสุดจาก Maven Central (`com.aspose:aspose-ocr`).  
- ไฟล์รูปภาพ (`.tif`, `.tiff`) หรือ PDF ที่คุณต้องการประมวลผล.  
- RAM ปริมาณพอสมควร — การประมวลผลแบบขนานจะเปิดหลายเธรด แต่ Aspose มีประสิทธิภาพการใช้หน่วยความจำ.

หากคุณมีทั้งหมดนี้แล้ว ไปเริ่มกันเลย.

![แผนภาพแสดงกระบวนการ OCR – วิธีใช้ OCR ใน Java ด้วยการประมวลผลแบบขนาน](how-to-use-ocr-pipeline.png)

*ข้อความแทนภาพ: ตัวอย่างแผนภาพการใช้ OCR*

---

## การประมวลผลแบบขนานช่วยเพิ่มความเร็วของ OCR อย่างไร?
การประมวลผลแบบขนานจะกระจายงาน OCR ไปยังคอร์ CPU ทั้งหมดที่มีอยู่ ทำให้หลายหน้าถูกจดจำพร้อมกัน บนแล็ปท็อป 4‑คอร์ทั่วไป การเปิดใช้งานโหมดขนานจะลดเวลาการประมวลผลของ PDF 100‑หน้าจากประมาณ 45 วินาทีเหลือประมาณ 18 วินาที ในขณะที่เวิร์กสเตชัน 16‑คอร์สามารถทำงานเดียวกันให้เสร็จภายในน้อยกว่า 7 วินาที การเพิ่มความเร็วนี้มาพร้อมกับค่าใช้จ่ายหน่วยความจำที่ต่ำ เนื่องจากแต่ละเธรดทำงานกับบัฟเฟอร์ของหน้าเดียวเท่านั้น.

## วิธีตั้งค่าโปรเจกต์ของคุณและเพิ่ม Aspose OCR
การตั้งค่าโปรเจกต์อย่างถูกต้องทำให้แน่ใจว่า OCR engine สามารถโหลดได้ในขณะรัน โดยการเพิ่ม Aspose OCR dependency ลงในไฟล์ build ของคุณ จะทำให้คลาสต่าง ๆ อยู่ใน classpath ซึ่งจำเป็นสำหรับการทำ OCR ใด ๆ ต่อไป.

### ทำไมเรื่องนี้ถึงสำคัญ
ก่อนที่คุณจะ **ทำ OCR บน PDF** ไฟล์ได้ ไลบรารีต้องอยู่ใน classpath ของคุณ หากไม่มีคอมไพเลอร์จะโยน `ClassNotFoundException` และคุณจะติดขัดที่ขั้นตอนต่อไป.

### วิธีทำ
หากคุณใช้ Maven ให้เพิ่ม dependency:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

สำหรับ Gradle ให้เพิ่ม:

```gradle
implementation 'com.aspose:aspose-ocr:24.10'
```

> **เคล็ดลับ:** รักษาเลขเวอร์ชันให้ตรงกับบันทึกการปล่อยของ Aspose; เวอร์ชันใหม่มักมีการปรับปรุงประสิทธิภาพสำหรับการประมวลผลแบบขนาน.

## OcrEngine class คืออะไร?
`OcrEngine` เป็นคลาสหลักใน Aspose OCR ที่ขับเคลื่อนกระบวนการจดจำสำหรับรูปภาพและเอกสาร PDF.  
`OcrEngine` เป็นคลาสแกนกลางของ Aspose OCR ที่ทำการดึงข้อความจากรูปภาพและไฟล์ PDF มันให้เมธอดสำหรับเปิดใช้งานการประมวลผลแบบขนาน, ตั้งค่าภาษา, และดึงข้อความที่จดจำได้เป็นสตริง นอกจากนี้ยังมีตัวเลือกการกำหนดค่าเพื่อเพิ่มประสิทธิภาพหน่วยความจำและการเลือกภาษา ทำให้ยืดหยุ่นสำหรับสถานการณ์ OCR หลากหลาย.

## วิธีสร้าง OCR engine และเปิดใช้งานการประมวลผลแบบขนาน
การสร้างอินสแตนซ์ของ `OcrEngine` และเปิดโหมดขนานจะเตรียมไลบรารีให้กระจายงานไปยังคอร์ CPU คุณยังสามารถกำหนดภาษและการตั้งค่าอื่น ๆ ก่อนประมวลผลไฟล์ใด ๆ และอาจจำกัดจำนวนเธรดเพื่อให้สอดคล้องกับสภาพแวดล้อมการใช้งานของคุณได้.

โหลด engine, เปิดโหมดขนาน, และอาจจำกัดพูลเธรด:

```java
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getConfig().setUseParallelProcessing(true);
ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors() - 1);
```

- `setUseParallelProcessing(true)`: บอกให้ Aspose แบ่งงานไปยังคอร์ CPU ที่มีอยู่.  
- `setMaxThreads(...)`: คุณสามารถจำกัดพูลเธรดได้หากอยู่บนเซิร์ฟเวอร์ที่แชร์หรืออยากเหลือพื้นที่ให้บริการอื่น.  
- `processImage(inputPath)`: ทำงานได้ทั้งไฟล์รูปภาพและเอกสาร PDF, ดังนั้นการเรียกเดียวกันนี้ **ทำ OCR บน PDF** และบน TIFF ได้เช่นกัน.

## วิธีจัดการกับประเภทอินพุตที่แตกต่าง – PDF vs. TIFF
แม้ว่า `processImage` จะรับสตริงพาธ, การจัดการภายในจะแตกต่างกัน PDF มักมีหลายหน้า, แต่ละหน้าจะกลายเป็นงาน OCR แยกกัน TIFF สามารถเป็นหน้าเดียวหรือหลายหน้า; Aspose จะถือแต่ละเฟรมเป็นหน้า.

### สิ่งที่ควรระวัง
| อินพุต | ปัญหาที่พบบ่อย | วิธีแก้แนะนำ |
|------|----------------|-----------------|
| PDF | PDF ขนาดใหญ่อาจทำให้หน่วยความจำหมดหากโหลดทุกหน้าพร้อมกัน. | ใช้ `ocrEngine.getConfig().setMemoryOptimization(true);` (มีในรุ่นใหม่). |
| Multi‑page TIFF | TIFF รุ่นเก่าบางไฟล์ใช้การบีบอัดที่ไม่รองรับ. | แปลงเป็นรูปแบบที่รองรับก่อน หรือใช้ตัวช่วย `TiffImage` ของ Aspose. |

ด้านล่างเป็นโค้ดสั้น ๆ ที่แสดงวิธีตรวจจับประเภทไฟล์และบันทึกข้อความที่เป็นมิตร:

```java
String ext = Files.getFileExtension(inputPath).toLowerCase();
if (ext.equals("pdf")) {
    System.out.println("Processing PDF document...");
} else if (ext.equals("tif") || ext.equals("tiff")) {
    System.out.println("Processing TIFF image...");
} else {
    System.out.println("Unsupported file type: " + ext);
}
```

## วิธีตรวจสอบผลลัพธ์ – ควรเห็นอะไรบ้าง?
หลังจากรันโปรแกรมจะพิมพ์ข้อความที่ดึงออกมาที่คอนโซล พร้อมรักษาการขึ้นบรรทัดและตัวคั่นหน้า ตรวจสอบผลลัพธ์เพื่อให้แน่ใจว่าข้อมูลที่คาดหวังทั้งหมดปรากฏและส่วนที่อ่านไม่ออกถูกทำเครื่องหมายด้วย placeholder เพื่อบ่งบอกว่า OCR ไม่สามารถจดจำอักขระได้.

เมื่อโปรแกรมเสร็จสิ้น คุณจะเห็นข้อความดิบที่ดึงออกมาพิมพ์ที่คอนโซล ตัวอย่างผลลัพธ์สำหรับใบแจ้งหนี้สแกนง่าย ๆ อาจเป็นดังนี้:

```
Invoice #12345
Date: 2023‑07‑15
Total Amount: $1,250.00
...
```

หาก OCR มีปัญหากับหน้าหนึ่ง Aspose จะใส่บรรทัด placeholder เช่น `[Unrecognizable]` คุณสามารถกรองออกในภายหลังหากต้องการข้อมูลที่สะอาด.

**ตรวจสอบอย่างเร็ว**

รันโปรแกรมด้วยไฟล์ทดสอบที่รู้จักและเปรียบเทียบผลลัพธ์ที่คอนโซลกับเอกสารต้นฉบับ หากข้อความตรงกันภายในเกณฑ์ความแม่นยำ 95 % การตั้งค่าของคุณทำงานถูกต้อง.

## วิธีปรับแต่งประสิทธิภาพ – เมื่อใดควรปรับจำนวนเธรด
การปรับจำนวนเธรดช่วยให้คุณสมดุลการใช้ CPU กับค่าโอเวอร์เฮด บนเครื่องที่คอร์น้อย จำนวนเธรดต่ำจะลดการสลับคอนเท็กซ์, ในขณะที่บนเซิร์ฟเวอร์คอร์สูงคุณสามารถเพิ่มเพื่อใช้ประโยชน์จากการขนานอย่างเต็มที่, ควรทดสอบเพื่อหาการตั้งค่าที่เหมาะที่สุดเสมอ.

### วิธีหาจุดที่เหมาะสม
รันชุดการทดสอบ benchmark ด้วยค่า `setMaxThreads` ต่าง ๆ, วัดเวลาการทำงานรวมของเอกสารตัวอย่าง สร้างกราฟผลลัพธ์เพื่อระบุจุดที่การเพิ่มเธรดไม่ให้ความเร็วเพิ่มขึ้นอีก.

```java
long start = System.nanoTime();
ocrEngine.processImage("large-document.pdf");
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed ms: " + elapsed / 1_000_000);
```

รันโปรแกรมด้วยค่า `setMaxThreads` ต่าง ๆ และบันทึกเวลา เลือกการกำหนดค่าที่ให้ผ่านอัตราการทำงานดีที่สุดและนำไปใช้ในผลิตภัณฑ์.

## วิธีขยายตัวอย่าง – การประมวลผลหลายไฟล์เป็นชุด
เพื่อประมวลผลหลายไฟล์อัตโนมัติ ให้วนลูปผ่านไดเรกทอรีและเรียก OCR routine สำหรับแต่ละเอกสาร ลูปภายนอกนี้สามารถทำขนานได้ด้วย `ExecutorService` หากต้องการจัดการไฟล์จำนวนมากพร้อมกัน.

```java
Files.list(Paths.get("input-folder"))
     .filter(Files::isRegularFile)
     .forEach(path -> ocrEngine.processImage(path.toString()));
```

รูปแบบนี้สเกลได้ดีเพราะ engine จะประมวลผลหน้าของแต่ละไฟล์แบบขนานอยู่แล้ว ลูปภายนอกทำงานตามลำดับ, แต่คุณก็สามารถส่งแต่ละไฟล์ไปยัง `ExecutorService` หากต้องการใช้ CPU ฟาร์มขนาดใหญ่เต็มที่.

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง
| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|-------------------|--------|
| `OutOfMemoryError` | โหลดหน้ามากเกินไปพร้อมกัน (โดยเฉพาะกับ PDF ขนาดใหญ่). | เปิดใช้งานการเพิ่มประสิทธิภาพหน่วยความจำ (`setMemoryOptimization(true)`) หรือประมวลผล PDF ทีละหน้าโดยใช้ `processPage`. |
| Garbled characters | การตั้งค่าภาษา/ชุดอักขระไม่ถูกต้อง. | เรียก `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` หรือ enum ภาษาที่เหมาะสม. |
| Slow performance despite parallel flag | ระบบปฏิบัติการจำกัดการสร้างเธรดหรือ JVM รันด้วย heap ขนาดเล็ก. | เพิ่ม flag `-Xmx` ของ heap, และตรวจสอบขีดจำกัดเธรดของ OS (`ulimit -u`). |
| Blank output | ความละเอียดของภาพอินพุต < 300 dpi. | ขยายภาพก่อน OCR หรือใช้สแกนเนอร์ที่ให้ความละเอียดสูงกว่า. |

## สรุป – สิ่งที่เราได้ครอบคลุม
- **วิธีทำ OCR บน PDF** และไฟล์ TIFF ด้วย Java โดยใช้ `OcrEngine` ของ Aspose.  
- เปิดใช้งาน **การประมวลผลแบบขนาน** เพื่อเร่งความเร็วการจดจำ.  
- ปรับจำนวนเธรดเพื่อประสิทธิภาพที่ดีที่สุด.  
- จัดการกรณีขอบเช่น PDF ขนาดใหญ่, TIFF หลายหน้า, และการตั้งค่าภาษา.  
- ขยายตัวอย่างไฟล์เดียวให้เป็นตัวประมวลผลแบบชุดสำหรับงานจริง.

## ขั้นตอนต่อไป
ตอนนี้คุณเชี่ยวชาญพื้นฐานแล้ว ลองสำรวจหัวข้อที่เกี่ยวข้องต่อไปนี้:

- **Extract image text java** จากบันทึกมือ (เปิด `setHandwritingRecognition(true)`).  
- ผสานผลลัพธ์ OCR กับ Apache Tika เพื่อดึงข้อมูลเมตาดาต้า.  
- เก็บผลลัพธ์ใน Elasticsearch เพื่อสร้างคลังเอกสารที่ค้นหาได้.  
- ใช้ OCR ของ Aspose กับภาษาต่าง ๆ เช่น Python หรือ .NET — หลักการยังคงเหมือนเดิม.

อย่ากลัวที่จะทดลองกับขีดจำกัดเธรดต่าง ๆ, รูปแบบไฟล์, และแพ็คเกจภาษา ยิ่งคุณเล่นมากเท่าไหร่ คุณก็จะเข้าใจการแลกเปลี่ยนระหว่างความเร็วและความแม่นยำได้ดียิ่งขึ้น.

## คำถามที่พบบ่อย
**Q: โหมดขนานทำงานบนระบบปฏิบัติการใดก็ได้หรือไม่?**  
A: ใช่, เอนจินขนานของ Aspose OCR ทำงานบน Windows, Linux, และ macOS ตราบใดที่ JVM สามารถสร้างเธรดเนทีฟได้.

**Q: สามารถประมวลผล PDF ที่มีรหัสผ่านได้หรือไม่?**  
A: แน่นอน — ส่งรหัสผ่านไปยัง `processImage` ผ่าน overload ที่รับอ็อบเจ็กต์ `PdfLoadOptions`.

**Q: เวอร์ชัน Java ที่รองรับอย่างเป็นทางการคืออะไร?**  
A: Aspose OCR รองรับ Java 8, 11, 17, และรุ่น LTS ต่อ ๆ ไป.

**Q: ความแม่นยำของ OCR สำหรับสแกนความละเอียดต่ำเป็นอย่างไร?**  
A: สำหรับภาพที่ความละเอียดต่ำกว่า 300 dpi ความแม่นยำจะลดลงเหลือประมาณ 80 %; การเพิ่มความละเอียดเป็น 400 dpi มักทำให้เกิน 95 %.

**Q: จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานในผลิตภัณฑ์หรือไม่?**  
A: ใช่, ไลเซนส์ Aspose ที่ถูกต้องจะลบข้อจำกัดการประเมินและเปิดใช้งานคุณสมบัติเต็มประสิทธิภาพเช่นการประมวลผลแบบขนาน.

**อัปเดตล่าสุด:** 2026-10-24  
**ทดสอบด้วย:** Aspose.OCR 24.10 for Java  
**ผู้เขียน:** Aspose  






```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

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

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

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

## บทแนะนำที่เกี่ยวข้อง

- [วิธีใช้ OCR ใน Java ดึงข้อความจาก PDF ด้วย Aspose OCR](/ocr/java/advanced-ocr-techniques/how-to-use-ocr-in-java-extract-text-from-pdf-aspose-ocr/)
- [จดจำข้อความ PDF ด้วย Aspose OCR ใน Java คู่มือเต็ม](/ocr/java/ocr-operations/recognize-pdf-text-with-aspose-ocr-in-java-complete-guide/)
- [วิธีเปิดใช้งาน GPU สำหรับ OCR ใน Java ดึงข้อความจากรูปภาพ](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}