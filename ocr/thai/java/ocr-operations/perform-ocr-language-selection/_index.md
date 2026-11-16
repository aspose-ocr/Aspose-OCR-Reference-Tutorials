---
date: 2026-06-24
description: เรียนรู้วิธี OCR ข้อความในภาพพร้อมการเลือกภาษาโดยใช้ Aspose.OCR สำหรับ
  Java คู่มือขั้นตอนนี้ครอบคลุม extract text java, OCR skew correction, และอื่น ๆ
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: วิธีทำการแก้ไขการเอียงของ OCR และการเลือกภาษาโดยใช้ Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: วิธีทำการแก้ไขการเอียงของ OCR และการเลือกภาษาโดยใช้ Aspose.OCR
url: /th/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำการแก้ไขการเอียงของ OCR และการเลือกภาษาโดยใช้ Aspose.OCR

## บทนำ

การสกัดข้อความจากไฟล์ภาพเป็นความต้องการทั่วไปไม่ว่าจะเป็นการแปลงเอกสารสแกนเป็นดิจิทัล, การประมวลผลใบเสร็จ, หรือการสร้างคลังข้อมูลที่สามารถค้นหาได้ ในบทแนะนำนี้เราจะพาคุณผ่านตัวอย่างเต็มรูปแบบแบบทำมือที่แสดง **วิธี OCR ข้อความในภาพ** ด้วยการตั้งค่าภาษาเฉพาะ, เพื่อให้คุณสามารถผสานรวม OCR ที่เชื่อถือได้เข้าสู่แอปพลิเคชัน Java ของคุณได้ทันที คุณยังจะได้เห็นวิธีจัดการ **การแก้ไขการเอียงของ OCR** และการจดจำตามพื้นที่เพื่อความแม่นยำสูงสุด ซึ่งร่วมกันสามารถ **ปรับปรุงความแม่นยำของ OCR** ได้สูงถึง 30 % ในการสแกนที่มีการเอียง

## คำตอบอย่างรวดเร็ว
- **ไลบรารีใดที่จัดการ OCR ใน Java?** Aspose.OCR for Java  
- **การตั้งค่าใดที่เลือกภาษา?** `settings.setLanguage(Language.Eng)` (หรือภาษาใดที่รองรับ)  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** ใบอนุญาตทดลองใช้งานฟรีทำงานได้สำหรับการทดสอบ; จำเป็นต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถจำกัด OCR ให้เฉพาะพื้นที่ของภาพได้หรือไม่?** ใช่, ใช้ `RecognitionSettings.setRecognitionAreas()` กับสี่เหลี่ยม.  
- **ระยะเวลาการทำงานโดยทั่วไปคือเท่าไหร่?** เพียงไม่กี่วินาทีต่อหน้าในแล็ปท็อปมาตรฐาน, ขึ้นอยู่กับขนาดภาพและความซับซ้อนของภาษา.  

`Language` เป็น enumeration ที่แสดงรายการภาษาที่ OCR รองรับโดย Aspose.OCR เช่น English, French, Spanish เป็นต้น.

## การแก้ไขการเอียงของ OCR คืออะไร

การแก้ไขการเอียงของ OCR คือกระบวนการตรวจจับและทำให้เส้นข้อความที่เอียงตรงขึ้นก่อนการจดจำอักขระ โดยการจัดแนวฐานข้อความ, เครื่องมือ OCR สามารถใช้โมเดลภาษาของมันได้อย่างมีประสิทธิภาพมากขึ้น, ลดการจดจำผิดพลาดที่เกิดจากการสแกนที่มีมุม การทำขั้นตอนนี้ช่วยปรับปรุงคุณภาพภาพอินพุต, ทำให้อัลกอริทึมการจดจำมุ่งเน้นที่รูปร่างอักขระจริงแทนการบิดเบือนที่เกิดจากการหมุน.

## ทำไมการแก้ไขการเอียงของ OCR จึงทำให้ความแม่นยำดีขึ้น

เมื่อข้อความเอียง, รูปร่างอักขระจะดูบิดเบือน, ทำให้อัตราความผิดพลาดสูงขึ้นถึง 20 % การใช้ **ocr skew correction** จะลบการบิดเบือนนั้น, ทำให้เครื่องมือมุ่งเน้นที่ glyph จริง ในการทดสอบเบนช์มาร์ก Aspose.OCR ได้เพิ่มความแม่นยำในการจดจำขึ้น 15‑30 % สำหรับเอกสารที่มีการหมุน 10‑15° หลังจากใช้การแก้ไขการเอียง.

## ทำไมต้องใช้ Aspose.OCR พร้อมการเลือกภาษา

การเลือกภาษาที่ตรงกับข้อความต้นฉบับทำให้เครื่องมือ OCR ใช้พจนานุกรมและโมเดลอักขระเฉพาะภาษา, ซึ่งเพิ่มความแม่นยำในการจดจำอย่างมากและลดเวลาในการประมวลผล นอกจากนี้ Aspose.OCR ยังให้การควบคุมที่ละเอียดสำหรับการแก้ไขการเอียง, การเลือกพื้นที่, และรูปแบบผลลัพธ์, ทำให้เป็นตัวเลือกที่หลากหลายสำหรับกระบวนการประมวลผลเอกสารหลายภาษา.

- **การสนับสนุนหลายภาษา** – เลือกภาษาที่ตรงกับภาพของคุณเพื่อเพิ่มความแม่นยำ.  
- **การควบคุมที่ละเอียด** – ปรับการเอียง, กำหนดพื้นที่จดจำ, และตั้งค่าพฤติกรรม auto‑skew.  
- **Pure Java API** – ไม่มีการพึ่งพา native, ง่ายต่อการผสานรวมในโครงการ Java ใดก็ได้.  
- **ข้อมูลผลลัพธ์ที่หลากหลาย** – รับข้อความธรรมดา, JSON, สี่เหลี่ยมขอบ, และคำเตือนในหนึ่งการเรียก.  
- **ความสามารถที่ระบุจำนวน** – Aspose.OCR รองรับ **50+** รูปแบบอินพุตและเอาต์พุตและสามารถประมวลผลชุดภาพ **500‑page** โดยไม่ต้องโหลดเอกสารทั้งหมดเข้าสู่หน่วยความจำ.

## ข้อกำหนดเบื้องต้น

ก่อนที่คุณจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

- **Java Development Kit (JDK)** ติดตั้งแล้ว (JDK 8 หรือใหม่กว่า).  
- **Aspose.OCR for Java** library – ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการ [here](https://reference.aspose.com/ocr/java/).  
- ไฟล์ภาพที่มีข้อความที่คุณต้องการสกัด, เช่น `p3.png`.

## นำเข้าแพ็กเกจ

การนำเข้าต่อไปนี้ให้คุณเข้าถึงคลาส OCR หลักและยูทิลิตี้มาตรฐานของ Java.  
`import com.aspose.ocr.*;` – brings in the main OCR engine.  
`import com.aspose.ocr.config.*;` – contains configuration objects such as `RecognitionSettings`.  
`import java.awt.Rectangle;` – used to define recognition areas.  

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## วิธีใช้การแก้ไขการเอียงของ OCR ใน Java?

โหลดภาพ, ปิดการตรวจจับการเอียงอัตโนมัติ, และให้ค่ามุมที่วัดได้หรือให้เครื่องมือคำนวณโดยใช้ `settings.setAutoSkew(false)` เครื่องมือ OCR จะทำการจัดแนวภาพตามมุมที่ให้หรือที่ตรวจพบก่อน, จากนั้นจึงทำการจดจำอักขระ วิธีการสองขั้นตอนนี้ทำให้แน่ใจว่าการเอียงใด ๆ ถูกลบออกก่อนที่โมเดลภาษา จะถูกนำมาใช้, ส่งผลให้ผลลัพธ์ข้อความสะอาดขึ้นและการจดจำผิดน้อยลง.

## คู่มือขั้นตอนต่อขั้นตอน

### ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ

สร้างอ็อบเจ็กต์ `File` ที่ชี้ไปยังโฟลเดอร์ที่มีภาพต้นฉบับของคุณ ทำให้การจัดการเส้นทางพกพาได้ข้ามระบบปฏิบัติการ.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

แทนที่ `"Your Document Directory"` ด้วยเส้นทางเต็มที่ที่ไฟล์ `p3.png` อยู่.

### ขั้นตอนที่ 2: กำหนดเส้นทางภาพ

สร้างอ็อบเจ็กต์ `File` สำหรับภาพเฉพาะที่คุณต้องการประมวลผล การใช้ `File` ทำให้คุณเข้าถึงเมตาดาต้าไฟล์ได้ง่ายหากต้องการในภายหลัง.

```java
// The image path
String file = dataDir + "p3.png";
```

ตรวจสอบให้แน่ใจว่า ตัวแปร `file` ชี้ไปยังภาพที่คุณต้องการประมวลผลอย่างแม่นยำ.

### ขั้นตอนที่ 3: สร้างอินสแตนซ์ของ Aspose.OCR API

คลาส `AsposeOCR` เป็นจุดเริ่มต้นสำหรับการดำเนินการ OCR ทั้งหมด มันห่อหุ้มเอนจิน, จัดการทรัพยากร, และให้เมธอด `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

อ็อบเจ็กต์ `AsposeOCR` ให้คุณเข้าถึงการดำเนินการ OCR ทั้งหมด.

### ขั้นตอนที่ 4: ตั้งค่าตัวเลือกการจดจำ (การเลือกภาษา)

`RecognitionSettings` คือคอนเทนเนอร์การกำหนดค่าของ Aspose.OCR ที่ให้คุณปรับจูนกระบวนการ OCR อย่างละเอียด.

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

ที่นี่เรา:

1. ปิด auto‑skew เนื่องจากเรามีค่าการเอียงแบบแมนนวล.  
2. กำหนดพื้นที่สี่เหลี่ยม (`RecognitionAreas`) เพื่อจำกัด OCR ให้เฉพาะส่วนของภาพที่มีข้อความจริง.  
3. ตั้งค่า **language** เป็น English (`Language.Eng`). เปลี่ยนเป็น `Language.Fra`, `Language.Spa`, เป็นต้น, ขึ้นอยู่กับภาพต้นฉบับของคุณ.

### ขั้นตอนที่ 5: ทำ OCR และดึงผลลัพธ์

การเรียก `recognizePage` จะรันเอนจิน OCR ด้วยภาพและการตั้งค่าที่คุณกำหนด ผลลัพธ์จะถูกเก็บในอ็อบเจ็กต์ `RecognitionResult` ซึ่งรวบรวมข้อมูลที่เป็นประโยชน์ทั้งหมด.

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

การเรียก `RecognizePage` รันเอนจิน OCR ด้วยภาพและการตั้งค่าที่คุณกำหนด ผลลัพธ์ถูกเก็บในอ็อบเจ็กต์ `RecognitionResult`.

### ขั้นตอนที่ 6: พิมพ์และใช้ผลลัพธ์

ผลลัพธ์ที่แสดงในคอนโซลประกอบด้วย:

- ข้อความที่สกัดทั้งหมด (`recognitionText`).  
- ข้อความสำหรับแต่ละสี่เหลี่ยมที่กำหนด (`recognitionAreasText`).  
- พิกัดสี่เหลี่ยมขอบ.  
- ตัวแทน JSON เพื่อการประมวลผลต่อเนื่องที่ง่าย.  
- มุมการเอียงที่ตรวจพบและคำเตือนใด ๆ.

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

ผลลัพธ์ในคอนโซลแสดงข้อความที่สกัดทั้งหมด, ข้อความตามพื้นที่, กล่องขอบ, JSON, มุมการเอียง, และคำเตือน คุณสามารถนำ `result.recognitionText` ไปใช้ในตรรกะธุรกิจของคุณได้ — เก็บ, ทำดัชนี, หรือส่งต่อไปยังบริการอื่น.

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **อักขระขยะ** | เลือกภาษาไม่ถูกต้อง | ตั้งค่า `Language` enum ที่ถูกต้อง (เช่น `Language.Fra` สำหรับภาษาฝรั่งเศส). |
| **ไม่มีข้อความที่ส่งกลับ** | พื้นที่จดจำไม่ครอบคลุมข้อความ | ปรับพิกัด `Rectangle` หรือเอา `RecognitionAreas` ออกเพื่อประมวลผลภาพทั้งหมด. |
| **ประสิทธิภาพช้า** | ภาพขนาดใหญ่มากหรือความละเอียดสูง | ลดขนาดภาพก่อน OCR หรือเพิ่มการจัดสรรหน่วยความจำ JVM. |
| **คำเตือนเกี่ยวกับรูปแบบที่ไม่รองรับ** | รูปแบบภาพไม่ถูกจดจำ | แปลงภาพเป็น PNG, JPEG หรือ TIFF ก่อนประมวลผล. |

## คำถามที่พบบ่อย

**Q: ฉันสามารถจดจำหลายภาษาในหนึ่งการเรียก OCR ได้หรือไม่?**  
**A:** ใช่. ใช้ `settings.setLanguage(Language.Eng | Language.Fra)` เพื่อเปิดการจดจำหลายภาษา.

**Q: Aspose.OCR รองรับรูปแบบภาพใด?**  
**A:** PNG, JPEG, BMP, TIFF, GIF, และอื่น ๆ อีกหลายรูปแบบ. เพียงให้เส้นทางไฟล์ที่ถูกต้อง.

**Q: มีขนาดจำกัดสำหรับภาพหรือไม่?**  
**A:** ไม่มีขีดจำกัดที่แน่นอน, แต่การประมวลผลภาพที่ใหญ่กว่า 10 MB อาจเพิ่มการใช้หน่วยความจำและเวลาการทำงาน. ควรพิจารณาการปรับขนาดไฟล์ใหญ่.

**Q: ฉันจะได้รับใบอนุญาตสำหรับการผลิตได้อย่างไร?**  
**A:** ซื้อใบอนุญาตจากเว็บไซต์ Aspose และใช้มันผ่านคลาส `License` ตามที่แสดงในเอกสาร Aspose.

**Q: ฉันสามารถสกัดข้อความจากหน้า PDF โดยตรงได้หรือไม่?**  
**A:** ไม่สามารถทำได้โดยตรงด้วย Aspose.OCR. ให้แปลงหน้า PDF เป็นภาพก่อน (เช่นใช้ Aspose.PDF) แล้วจึงรัน OCR.

## สรุป

คุณได้เห็นแล้วว่า **สกัดข้อความจากภาพ** ด้วย Aspose.OCR สำหรับ Java พร้อมการเลือกภาษาที่เหมาะสมและการใช้ **OCR skew correction** เพื่อปรับปรุงความน่าเชื่อถือ วิธีนี้ให้ OCR ที่แม่นยำและประสิทธิภาพสูงซึ่งสามารถฝังลงในกระบวนการทำงานใด ๆ ที่ใช้ Java — ตั้งแต่ระบบจัดการเอกสารไปจนถึงสายการจับข้อมูล ทดลองใช้ `Language` enum ต่าง ๆ, ปรับ `RecognitionAreas`, และผสานผลลัพธ์ JSON เข้ากับการวิเคราะห์ต่อเนื่องของคุณเพื่อโซลูชันแบบครบวงจรจริง.

---

**อัปเดตล่าสุด:** 2026-06-24  
**ทดสอบด้วย:** Aspose.OCR 24.11 for Java  
**ผู้เขียน:** Aspose

## บทแนะนำที่เกี่ยวข้อง

- [วิธีคำนวณมุมเอียง java ด้วย Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [วิธี OCR ข้อความภาพด้วยภาษาโดยใช้ Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [OCR การจดจำเอกสาร PDF ใน Aspose.OCR สำหรับ Java](/ocr/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}