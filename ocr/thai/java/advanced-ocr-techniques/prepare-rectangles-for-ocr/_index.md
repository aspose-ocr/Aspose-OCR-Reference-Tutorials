---
date: 2026-02-20
description: เรียนรู้วิธีการจดจำสี่เหลี่ยมหน้าโดยใช้ Aspose.OCR สำหรับ Java, ดึงข้อความจากภาพในโครงการ
  Java, และทำตามบทแนะนำ Aspose OCR Java นี้เพื่อการ OCR ที่แม่นยำ
linktitle: How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: วิธีระบุสี่เหลี่ยมหน้ากระดาษสำหรับการจดจำข้อความ OCR ด้วย Aspose.OCR
url: /th/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการระบุสี่เหลี่ยมหน้ากระดาษสำหรับการจดจำข้อความ OCR ใน Aspose.OCR

ในสายงานอัตโนมัติเอกสารสมัยใหม่, **recognize page rectangles** เป็นเทคนิคสำคัญที่ทำให้คุณบอกเครื่องมือ OCR ว่าต้องมองหาในตำแหน่งใดโดยเฉพาะ การจำกัด Aspose.OCR ให้ทำงานเฉพาะพื้นที่ที่มีข้อความจริงจะช่วยเพิ่มความเร็ว ลดสัญญาณรบกวน และได้ผลลัพธ์ที่สะอาดยิ่งขึ้น ในบทแนะนำนี้เราจะเดินผ่านทุกขั้นตอน—ตั้งค่าห้องสมุด, ใบอนุญาต, การกำหนดสี่เหลี่ยม, และสุดท้ายการเรียก API OCR—เพื่อให้คุณสามารถสกัดข้อความจากภาพใดก็ได้อย่างมั่นใจ

## คำตอบอย่างรวดเร็ว
- **What library handles OCR text recognition in Java?** Aspose.OCR for Java.  
- **Do I need a license for production use?** Yes – a valid Aspose.OCR license unlocks full functionality.  
- **Can I limit OCR to certain parts of an image?** Absolutely; you define rectangles that bound the target zones.  
- **What are the main prerequisites?** JDK 17+, Aspose.OCR for Java, and a Java IDE.  
- **Is this approach suitable for extracting text from images?** Yes, it’s an efficient way to **extract text image java** projects.

## “recognize page rectangles” คืออะไร?
วลีนี้หมายถึงการส่งรายการของอ็อบเจ็กต์ `java.awt.Rectangle` ไปยังเครื่องมือ OCR เพื่อให้มันประมวลผลเฉพาะพื้นที่ที่กำหนดบนหน้า วิธีการที่มุ่งเน้นนี้ช่วยลดเวลาในการประมวลผลและเพิ่มความแม่นยำ โดยเฉพาะกับเอกสารที่ซับซ้อนเช่น ใบแจ้งหนี้หรือแบบฟอร์ม

## ทำไมต้องเตรียมสี่เหลี่ยมสำหรับการจดจำข้อความ OCR?
การกำหนดสี่เหลี่ยมทำให้เครื่องมือมุ่งเน้นไปที่บริเวณที่มีข้อความจริง ซึ่ง:
* ลดเวลาในการประมวลผล  
* เพิ่มความแม่นยำโดยไม่สนใจพื้นหลังที่มีสัญญาณรบกวน  
* ให้คุณสกัดข้อมูลที่ต้องการเท่านั้น—เหมาะสำหรับแบบฟอร์ม, ใบแจ้งหนี้, และใบเสร็จ

## ข้อกำหนดเบื้องต้น

ก่อนเริ่ม, ตรวจสอบว่าคุณมี:

- **Java Development Kit (JDK)** – Aspose.OCR for Java ทำงานกับ JDK 17 หรือใหม่กว่า ดาวน์โหลดได้จากเว็บไซต์ของ Oracle  
- **Aspose.OCR for Java library** – รับ JAR ล่าสุดจากหน้าดาวน์โหลดอย่างเป็นทางการ [ที่นี่](https://releases.aspose.com/ocr/java/). ดูคำแนะนำการติดตั้ง [ที่นี่](https://reference.aspose.com/ocr/java/).  
- **Development Environment** – IDE ใดก็ได้สำหรับ Java (IntelliJ IDEA, Eclipse, VS Code ฯลฯ) ก็ใช้ได้

## Import Packages

ในไฟล์ซอร์ส Java ของคุณ, นำเข้าคลาส Aspose.OCR ที่จำเป็นและยูทิลิตี้มาตรฐานของ Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

> *We import `java.awt.Rectangle` because the OCR API expects rectangles that define the regions to scan.*

## Step 1: Set Up License

```java
SetLicense.main(null);
```

การเรียก `SetLicense` จะเปิดใช้งานใบอนุญาต Aspose.OCR ของคุณ, ยกเลิกข้อจำกัดการประเมินผลและเปิดฟีเจอร์ OCR เต็มรูปแบบ

## Step 2: Define Document Directory and Image Path

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

แทนที่ `"Your Document Directory"` ด้วยพาธเต็มที่เก็บภาพของคุณ (`p.png`). นี่คือภาพที่จะถูกประมวลผล

## Step 3: Create Aspose.OCR Instance

```java
AsposeOCR api = new AsposeOCR();
```

การสร้างอินสแตนซ์ `AsposeOCR` ให้คุณเข้าถึงเมธอด `RecognizePage` ที่ทำการ OCR จริง

## Step 4: Prepare Rectangles with Texts

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

แต่ละ `Rectangle(x, y, width, height)` บอก Aspose.OCR ว่าต้องมองหาข้อความที่ตำแหน่งใด ปรับค่าพิกัดให้ตรงกับเลย์เอาต์ของภาพต้นฉบับของคุณ

## Step 5: Perform OCR Recognition

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

การเรียก `RecognizePage` จะประมวลผลเฉพาะสี่เหลี่ยมที่กำหนดและคืนสตริงที่สกัดออกมา ผลลัพธ์บนคอนโซลช่วยให้คุณตรวจสอบ **ocr text recognition** ได้ทันที

## Common Issues and Tips

| ปัญหา | สาเหตุ | วิธีแก้ไข |
|-------|-------|----------|
| **ไม่มีผลลัพธ์** | พิกัดสี่เหลี่ยมหรือพาธภาพไม่ถูกต้อง | ตรวจสอบค่าของ `dataDir` อีกครั้งและให้แน่ใจว่าสี่เหลี่ยมครอบคลุมพื้นที่ข้อความจริง |
| **อักขระแปลก** | ภาพความละเอียดต่ำหรือฟอนต์ที่ไม่รองรับ | ใช้แหล่งภาพความละเอียดสูงขึ้นหรือทำการประมวลผลภาพล่วงหน้า (เช่น การไบนารี) |
| **ใบอนุญาตไม่ถูกนำไปใช้** | `SetLicense` ไม่ได้ถูกเรียกก่อน OCR | ตรวจสอบให้ `SetLicense.main(null);` ทำงานก่อนการเรียก API ใด ๆ |
| **การทำงานช้า** | มีสี่เหลี่ยมขนาดใหญ่จำนวนมาก | จำกัดจำนวนสี่เหลี่ยมและทำให้พวกมันแคบที่สุดเท่าที่เป็นไปได้รอบข้อความ |

## Frequently Asked Questions

**Q:** *Aspose.OCR รองรับภาษาโปรแกรมอื่น ๆ หรือไม่?*  
**A:** ใช่, Aspose.OCR ยังสนับสนุน .NET, C++, และ Python. ตรวจสอบเอกสารอย่างเป็นทางการสำหรับตัวอย่างตามภาษา

**Q:** *ฉันสามารถใช้ Aspose.OCR ในโครงการเชิงพาณิชย์ได้หรือไม่?*  
**A:** แน่นอน. ซื้อใบอนุญาตเชิงพาณิชย์ผ่าน [ร้านค้า Aspose](https://purchase.aspose.com/buy)

**Q:** *มีรุ่นทดลองฟรีหรือไม่?*  
**A:** มี, คุณสามารถดาวน์โหลดรุ่นทดลองได้ [ที่นี่](https://releases.aspose.com/)

**Q:** *ฉันจะขอใบอนุญาตชั่วคราวสำหรับการประเมินได้อย่างไร?*  
**A:** ใบอนุญาตชั่วคราวให้บริการผ่าน [พอร์ทัลใบอนุญาตชั่วคราวของ Aspose](https://purchase.aspose.com/temporary-license/)

**Q:** *จะหาแหล่งสนับสนุนจากชุมชนได้จากที่ไหน?*  
**A:** เยี่ยมชม [ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) สำหรับคำถาม, เคล็ดลับ, และตัวอย่างโค้ด

## Conclusion

คุณได้เรียนรู้วิธี **recognize page rectangles** ด้วย Aspose.OCR สำหรับ Java, ตั้งค่าใบอนุญาต, กำหนดพาธภาพ, และที่สำคัญที่สุดคือการเตรียมสี่เหลี่ยมที่แคบเพื่อให้ OCR มุ่งเน้นที่ส่วนที่ต้องการของภาพ เทคนิคนี้เหมาะสำหรับ **aspose ocr java tutorial** ใด ๆ ที่ต้องการการสกัดข้อความที่แม่นยำและประสิทธิภาพสูง

---

**อัปเดตล่าสุด:** 2026-02-20  
**ทดสอบกับ:** Aspose.OCR for Java 24.12  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}