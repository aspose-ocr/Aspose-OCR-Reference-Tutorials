---
date: 2026-06-19
description: เรียนรู้วิธีแปลงภาพเป็นข้อความใน Java, ดึงย่อหน้าจากภาพ, และดึงสี่เหลี่ยมพื้นที่ข้อความโดยใช้
  Aspose OCR Java library.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – จดจำข้อความจากภาพและดึงสี่เหลี่ยมพื้นที่ข้อความ
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – แปลงภาพเป็นข้อความและดึงสี่เหลี่ยมพื้นที่ข้อความ
url: /th/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ภาพเป็นข้อความใน Java – แปลงภาพเป็นข้อความและดึงสี่เหลี่ยมพื้นที่ข้อความ

## บทนำ

หากคุณต้องการ **convert image to text** ในแอปพลิเคชัน Java, Aspose.OCR for Java ให้โซลูชันที่เร็วและแม่นยำ ในบทแนะนำนี้เราจะอธิบายขั้นตอนที่จำเป็นเพื่อดึงย่อหน้าจากภาพ, รับสี่เหลี่ยมขอบเขตของแต่ละพื้นที่ข้อความ, และพิมพ์พิกัดเหล่านั้นลงคอนโซล เมื่อเสร็จคุณจะเข้าใจว่าทำไมวิธีนี้ถึงได้ผล, วิธีรวมไลบรารี, และจุดที่คุณสามารถขยายต่อสำหรับกรณีการใช้งานของคุณเอง

## คำตอบสั้น ๆ
`AreasType` เป็น enumeration ที่ระบุระดับการแบ่งส่วนข้อความ (คำ, บรรทัด, ย่อหน้า).

- **What does “recognize text from image” mean?** หมายถึงการแปลงอักขระภาพเป็นข้อมูลสตริงที่แก้ไขได้.  
- **Which library handles this in Java?** Aspose.OCR for Java.  
- **Do I need a license for development?** มีใบอนุญาตชั่วคราวสำหรับการทดสอบ; จำเป็นต้องมีใบอนุญาตเต็มสำหรับการผลิต.  
- **Can I extract paragraphs instead of single words?** ใช่ – ใช้ `AreasType.PARAGRAPHS` เพื่อรับสี่เหลี่ยมระดับย่อหน้า.  
- **Is the code compatible with Java 11+?** แน่นอน, API ทำงานกับ Java 11 และรุ่นต่อ ๆ ไป.

## “convert image to text” ใน Aspose.OCR คืออะไร?

`convert image to text` หมายถึงกระบวนการวิเคราะห์บิตแมพ, ใช้อัลกอริทึม OCR, และส่งคืนอักขระที่ได้รับการจดจำเป็นสตริง Aspose.OCR’s `RecognizePage` ทำการแปลงนี้พร้อมกับให้พิกัด `Rectangle` ที่แม่นยำสำหรับแต่ละบล็อกข้อความที่ตรวจพบ (ถ้าต้องการ)

## ทำไมต้องใช้ **java ocr library** นี้?

Aspose.OCR รองรับ **30+ languages** และสามารถประมวลผลภาพขนาดสูงสุด **50 MB** โดยไม่ต้องโหลดไฟล์ทั้งหมดเข้าสู่หน่วยความจำ, ให้เวลาตอบสนองระดับวินาทีบนเซิร์ฟเวอร์ทั่วไป ไลบรารีนี้ปลอดภัยต่อเธรด, ต้องการเพียง JAR ไฟล์เดียว, และให้รูปแบบผลลัพธ์ที่ยืดหยุ่น—รวมถึงข้อความดิบ, HTML, และสี่เหลี่ยมพื้นที่ข้อความที่แม่นยำ—ทำให้เหมาะสำหรับสถานการณ์องค์กรที่ต้องการประมวลผลจำนวนมาก

## ข้อกำหนดเบื้องต้น

- **Java Development Kit** (JDK 11 หรือใหม่กว่า) ติดตั้งบนเครื่องของคุณ.  
- **Aspose.OCR for Java** library – ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการ [here](https://releases.aspose.com/ocr/java/).  
- IDE หรือเครื่องมือสร้าง (Maven/Gradle) เพื่อจัดการการพึ่งพา JAR.

## นำเข้าแพ็กเกจ

ในโปรเจกต์ Java ของคุณ, นำเข้าคลาสที่จำเป็น:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## คู่มือขั้นตอนโดยละเอียด

### ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ของคุณ
สร้างโปรเจกต์ Java ใหม่ (หรือเพิ่มในโปรเจกต์ที่มีอยู่) และวางไฟล์ Aspose.OCR JAR บน classpath หากคุณใช้ Maven, เพิ่ม dependency ตามที่อธิบายในแพ็กเกจดาวน์โหลด

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### ขั้นตอนที่ 2: กำหนดไดเรกทอรีเอกสารและเส้นทางภาพ
ระบุที่ตั้งของภาพตัวอย่างของคุณ:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### ขั้นตอนที่ 3: สร้างอินสแตนซ์ AsposeOCR
`AsposeOCR` คือคลาสหลักที่ให้ฟังก์ชัน OCR

สร้างอินสแตนซ์ของเครื่อง OCR:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### ขั้นตอนที่ 4: จดจำข้อความในภาพ
โหลดภาพของคุณและเรียก `RecognizePage` เพื่อแปลงรูปภาพเป็นข้อความธรรมดา วิธีเรียกเดียวนี้ทำการเตรียมภาพ, แบ่งส่วนอักขระ, และการจดจำตามภาษาที่กำหนดในขั้นตอนเดียว

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### ขั้นตอนที่ 5: รับสี่เหลี่ยมที่มีพื้นที่ข้อความ
ดึงสี่เหลี่ยมขอบเขตสำหรับแต่ละย่อหน้า (หรือประเภทพื้นที่อื่น) ขั้นตอนนี้จะคืนคอลเลกชันของอ็อบเจกต์ `Rectangle` ที่ล้อมรอบบล็อกข้อความที่ตรวจพบอย่างแม่นยำ, ช่วยให้คุณไฮไลท์หรือประมวลผลส่วนย่อยต่อไปได้

CODE_BLOCK_PLACEHOLDER_5_END

## ปัญหาที่พบบ่อย & การแก้ไข

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | เส้นทางไฟล์ไม่ถูกต้องหรือไม่มีสิทธิ์อ่าน | ตรวจสอบว่า `imagePath` ชี้ไปยังไฟล์ PNG/JPG ที่มีอยู่และแอปมีสิทธิ์เข้าถึงระบบไฟล์ |
| Empty result string | ภาพคุณภาพต่ำหรือภาษาที่ไม่รองรับ | ทำการพรี‑โปรเซสภาพ (เพิ่มคอนทราสต์, ทำไบนารี) หรือระบุภาษาที่ถูกต้องด้วย `api.setLanguage("eng")` |
| No rectangles returned | ใช้ `AreasType` ผิด (เช่น `WORDS` แทนที่จะเป็นย่อหน้า) | เปลี่ยนเป็น `AreasType.PARAGRAPHS` หรือ `AreasType.LINES` ตามต้องการ |

## คำถามที่พบบ่อย

**Q: Aspose.OCR รองรับ Java 11 หรือไม่?**  
A: รองรับ, Aspose.OCR ทำงานกับ Java 11 และรุ่นต่อ ๆ ไป

**Q: สามารถใช้ Aspose.OCR ในโครงการส่วนบุคคลและเชิงพาณิชย์ได้หรือไม่?**  
A: ใช่, คุณสามารถใช้ในโครงการทุกประเภท สำหรับรายละเอียดใบอนุญาต, เยี่ยมชม [here](https://purchase.aspose.com/buy)

**Q: จะขอรับใบอนุญาตชั่วคราวสำหรับการประเมินผลได้อย่างไร?**  
A: คุณสามารถรับใบอนุญาตชั่วคราวได้จาก [here](https://purchase.aspose.com/temporary-license/)

**Q: จะหาชุมชนสนับสนุนหรือความช่วยเหลืออย่างเป็นทางการได้จากที่ไหน?**  
A: สำหรับการสนับสนุนและการสนทนา, เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)

**Q: Aspose.OCR รองรับการทำงานหลายเธรดหรือไม่?**  
A: รองรับ, ไลบรารีนี้ปลอดภัยต่อเธรดและสามารถใช้ในสภาพแวดล้อมพร้อมกันเพื่อประสิทธิภาพที่ดีกว่า

## สรุป

ใน **aspose ocr java tutorial** นี้คุณได้เรียนรู้วิธี **convert image to text** ด้วย Aspose.OCR for Java, ดึงย่อหน้า, และรับสี่เหลี่ยมที่แม่นยำที่ล้อมรอบแต่ละบล็อกข้อความ ความสามารถเหล่านี้ช่วยให้คุณสร้าง PDF ที่ค้นหาได้, ไฮไลท์ข้อความใน UI overlay, หรือส่งข้อมูลโครงสร้างไปยังกระบวนการต่อไป สำรวจ API เพิ่มเติมเพื่อปรับตั้งค่าภาษา, จัดการรูปแบบภาพต่าง ๆ, หรือรวมกับคลาวด์สตอเรจ

---

**Last Updated:** 2026-06-19  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## บทแนะนำที่เกี่ยวข้อง

- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}