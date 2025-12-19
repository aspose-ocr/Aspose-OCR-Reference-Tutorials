---
date: 2025-12-06
description: เรียนรู้วิธีใช้ Aspose.OCR สำหรับ Java เพื่อทำการจดจำข้อความด้วย OCR,
  ดึงข้อความจากภาพ, และเตรียมสี่เหลี่ยมสำหรับการจดจำแบบเจาะจง.
linktitle: Preparing Rectangles for OCR Text Recognition in Aspose.OCR
second_title: Aspose.OCR Java API
title: การเตรียมสี่เหลี่ยมสำหรับการจดจำข้อความ OCR ใน Aspose.OCR
url: /th/java/advanced-ocr-techniques/prepare-rectangles-for-ocr/
weight: 13
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การเตรียมสี่เหลี่ยมสำหรับการจดจำข้อความ OCR ใน Aspose.OCR

## Introduction

ในโลกที่ขับเคลื่อนด้วยข้อมูลในปัจจุบัน, **ocr text recognition** เป็นหัวใจสำคัญในการแปลงเอกสารสแกน, ภาพหน้าจอ, และรูปถ่ายให้เป็นเนื้อหาที่สามารถค้นหาและแก้ไขได้ Aspose.OCR for Java ทำให้กระบวนการนี้เร็วและเชื่อถือได้, โดยเฉพาะเมื่อคุณต้องการโฟกัสไปยังพื้นที่เฉพาะของภาพ ในบทเรียนนี้เราจะอธิบายขั้นตอนทั้งหมดที่จำเป็นในการเตรียมสี่เหลี่ยมเพื่อจำกัด OCR ให้ทำงานในพื้นที่ที่คุณต้องการ, ให้คุณควบคุมได้อย่างแม่นยำและประสิทธิภาพที่ดียิ่งขึ้น.

## Quick Answers
- **ไลบรารีใดที่จัดการ OCR text recognition ใน Java?** Aspose.OCR for Java.  
- **ฉันต้องการใบอนุญาตสำหรับการใช้งานในผลิตภัณฑ์หรือไม่?** ใช่ – ใบอนุญาต Aspose.OCR ที่ถูกต้องจะเปิดใช้งานฟังก์ชันทั้งหมด.  
- **ฉันสามารถจำกัด OCR ให้ทำงานในส่วนบางของภาพได้หรือไม่?** ได้แน่นอน; คุณกำหนดสี่เหลี่ยมที่ล้อมรอบโซนเป้าหมาย.  
- **ข้อกำหนดเบื้องต้นหลักคืออะไร?** JDK 17+, Aspose.OCR for Java, และ IDE สำหรับ Java.  
- **วิธีนี้เหมาะสำหรับการสกัดข้อความจากภาพหรือไม่?** ใช่, เป็นวิธีที่มีประสิทธิภาพในการ **extract text image java** projects.

## OCR Text Recognition คืออะไร?

OCR (Optical Character Recognition) text recognition แปลงภาพที่เป็นพิกเซลให้เป็นอักขระที่เครื่องคอมพิวเตอร์อ่านได้ ช่วยให้คุณสามารถค้นหา, แก้ไข, และวิเคราะห์เนื้อหาที่เดิมเป็นเพียงรูปภาพเท่านั้น.

## ทำไมต้องเตรียมสี่เหลี่ยมสำหรับ OCR Text Recognition?

การกำหนดสี่เหลี่ยมทำให้เครื่องยนต์มุ่งเน้นไปที่บริเวณที่มีข้อความจริง ๆ ซึ่ง:
* ลดเวลาการประมวลผล
* เพิ่มความแม่นยำโดยละเลยพื้นหลังที่มีสัญญาณรบกวน
* ทำให้คุณสกัดข้อมูลที่ต้องการเท่านั้น—เหมาะสำหรับแบบฟอร์ม, ใบแจ้งหนี้, และใบเสร็จ

## ข้อกำหนดเบื้องต้น

ก่อนเริ่ม, ตรวจสอบว่าคุณมี:

- **Java Development Kit (JDK)** – Aspose.OCR for Java ทำงานกับ JDK 17 หรือใหม่กว่า ดาวน์โหลดได้จากเว็บไซต์ Oracle.
- **Aspose.OCR for Java library** – รับไฟล์ JAR ล่าสุดจากหน้าดาวน์โหลดอย่างเป็นทางการ [here](https://releases.aspose.com/ocr/java/). ทำตามคู่มือการติดตั้ง [here](https://reference.aspose.com/ocr/java/).
- **Development Environment** – IDE สำหรับ Java ใดก็ได้ (IntelliJ IDEA, Eclipse, VS Code, ฯลฯ) ก็ใช้ได้.

## นำเข้าแพ็กเกจ

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

> *เรานำเข้า `java.awt.Rectangle` เนื่องจาก OCR API ต้องการสี่เหลี่ยมที่กำหนดบริเวณที่จะสแกน.*

## ขั้นตอนที่ 1: ตั้งค่าใบอนุญาต

```java
SetLicense.main(null);
```

การเรียก `SetLicense` จะเปิดใช้งานใบอนุญาต Aspose.OCR ของคุณ, ยกเลิกข้อจำกัดการประเมินผลและเปิดใช้งาน OCR text recognition เต็มรูปแบบ.

## ขั้นตอนที่ 2: กำหนดไดเรกทอรีเอกสารและเส้นทางรูปภาพ

```java
String dataDir = "Your Document Directory";
String imagePath = dataDir + "p.png";
```

แทนที่ `"Your Document Directory"` ด้วยเส้นทางเต็มที่เก็บรูปภาพของคุณ (`p.png`). นี่คือรูปภาพที่จะถูกประมวลผล.

## ขั้นตอนที่ 3: สร้างอินสแตนซ์ AsposeOCR

```java
AsposeOCR api = new AsposeOCR();
```

การสร้างอินสแตนซ์ `AsposeOCR` จะทำให้คุณเข้าถึงเมธอด `RecognizePage` ซึ่งทำการ OCR จริง.

## ขั้นตอนที่ 4: เตรียมสี่เหลี่ยมพร้อมข้อความ

```java
ArrayList<Rectangle> rectArray = new ArrayList<Rectangle>();
rectArray.add(new Rectangle(138, 352, 2033, 537));
rectArray.add(new Rectangle(147, 890, 2033, 1157));
rectArray.add(new Rectangle(923, 2045, 465, 102));
rectArray.add(new Rectangle(104, 2147, 2076, 819));
```

แต่ละ `Rectangle(x, y, width, height)` บอก AsposeOCR ว่าจะมองหาข้อความที่ตำแหน่งใด ปรับค่าพิกัดให้ตรงกับการจัดวางของภาพต้นฉบับของคุณ.

## ขั้นตอนที่ 5: ทำการ OCR Recognition

```java
try {
    String result = api.RecognizePage(imagePath, rectArray);
    System.out.println("Result with rect: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

การเรียก `RecognizePage` จะประมวลผลเฉพาะสี่เหลี่ยมที่กำหนดและคืนสตริงที่สกัดออกมา ผลลัพธ์ที่แสดงในคอนโซลช่วยให้คุณตรวจสอบผลลัพธ์ของ **ocr text recognition** ได้ทันที.

## ปัญหาทั่วไปและเคล็ดลับ

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|----------|
| **ไม่มีผลลัพธ์** | พิกัดสี่เหลี่ยมหรือเส้นทางรูปภาพไม่ถูกต้อง | ตรวจสอบค่าของ `dataDir` อีกครั้งและให้แน่ใจว่าสี่เหลี่ยมครอบคลุมบริเวณข้อความจริง. |
| **อักขระแปลก** | ภาพความละเอียดต่ำหรือฟอนต์ที่ไม่รองรับ | ใช้แหล่งที่มาที่มีความละเอียดสูงขึ้นหรือทำการประมวลผลภาพล่วงหน้า (เช่น การทำเป็นสีขาวดำ). |
| **ไม่ได้ใช้ใบอนุญาต** | `SetLicense` ไม่ได้ถูกเรียกก่อน OCR | ตรวจสอบให้แน่ใจว่า `SetLicense.main(null);` ทำงานก่อนการเรียก API ใด ๆ. |
| **ความล่าช้าของประสิทธิภาพ** | สี่เหลี่ยมขนาดใหญ่จำนวนมาก | จำกัดจำนวนสี่เหลี่ยมและทำให้พวกมันกระชับที่สุดเท่าที่จะเป็นไปได้รอบข้อความ. |

## สรุป

คุณได้เรียนรู้วิธีรวม Aspose.OCR สำหรับ Java, ตั้งค่าใบอนุญาต, กำหนดเส้นทางรูปภาพ, และที่สำคัญที่สุดคือการเตรียมสี่เหลี่ยมเพื่อให้ **ocr text recognition** มุ่งเน้นไปที่ส่วนเฉพาะของภาพ เทคนิคนี้เหมาะสำหรับ **java ocr tutorial** ใด ๆ ที่ต้องการการสกัดข้อความที่แม่นยำและมีประสิทธิภาพสูง.

## คำถามที่พบบ่อย

**Q: Aspose.OCR รองรับภาษาโปรแกรมอื่นหรือไม่?**  
A: ใช่, Aspose.OCR ยังรองรับ .NET, C++, และ Python. ตรวจสอบเอกสารอย่างเป็นทางการสำหรับตัวอย่างตามภาษา.

**Q: ฉันสามารถใช้ Aspose.OCR ในโครงการเชิงพาณิชย์ได้หรือไม่?**  
A: ได้แน่นอน. ซื้อใบอนุญาตเชิงพาณิชย์ผ่าน [Aspose store](https://purchase.aspose.com/buy).

**Q: มีรุ่นทดลองฟรีหรือไม่?**  
A: มี, คุณสามารถดาวน์โหลดรุ่นทดลองได้ [here](https://releases.aspose.com/).

**Q: ฉันจะขอใบอนุญาตชั่วคราวสำหรับการประเมินได้อย่างไร?**  
A: ใบอนุญาตชั่วคราวจะให้ผ่าน [Aspose temporary‑license portal](https://purchase.aspose.com/temporary-license/).

**Q: ฉันสามารถรับการสนับสนุนจากชุมชนได้จากที่ไหน?**  
A: เยี่ยมชม Aspose.OCR [forum](https://forum.aspose.com/c/ocr/16) สำหรับคำถาม, เคล็ดลับ, และตัวอย่างโค้ด.

---

**Last Updated:** 2025-12-06  
**Tested With:** Aspose.OCR for Java 24.12  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
