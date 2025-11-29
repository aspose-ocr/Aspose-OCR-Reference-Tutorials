---
date: 2025-11-29
description: เรียนรู้วิธีดึงข้อความจากภาพด้วยไลบรารี OCR ของ Java คู่มือนี้แสดงวิธีติดตั้ง
  Aspose OCR การจัดการหลายภาษา และการทำงานกับรูปแบบภาพ OCR ต่าง ๆ
language: th
linktitle: Performing OCR on BufferedImage in Aspose.OCR for Java
second_title: Aspose.OCR Java API
title: ทำ OCR บน BufferedImage ด้วยไลบรารี OCR ของ Java (Aspose.OCR)
url: /java/advanced-ocr-techniques/perform-ocr-buffered-image/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ทำ OCR บน BufferedImage ด้วยไลบรารี OCR ของ Java (Aspose.OCR)

## Introduction

หากคุณต้องการ **ดึงข้อความจากภาพใน Java** ไลบรารี *java ocr library* ที่เชื่อถือได้เป็นสิ่งสำคสาธิตวิธีใช้ Aspose.OCR—ไลบรารี OCR ของ Java ที่ทรงพลัง—to recognize text directly from a `BufferedImage`. คุณจะได้เห็นวิธีตั้งค่าไลบรารี, โหลดภาพ, และดึงสตริงที่ได้รับการจดจำออกมา เพียงไม่กี่บรรทัดของโค้ดเท่านั้น

## Quick Answers
- **อะไรคือไลบรารี OCR ของ Java ที่ดีที่สุด?** Aspose.OCR for Java ให้ความแม่นยำสูงและรองรับหลายภาษาอย่างครอบคลุม  
- **ฉันจะติดตั้ง Aspose OCR อย่างไร?** ดาวน์โหลดไฟล์ JAR จากเว็บไซต์ Aspose แล้วเพิ่มเข้าไปใน classpath ของโปรเจกต์  
- **ฉันสามารถจดจำหลายภาษาได้หรือไม่?** ใช่—Aspose.OCR รองรับ OCR หลายภาษาโดยอัตโนมัติ  
- **รูปแบบภาพใดบ้างที่รองรับ?** ไลบรารีทำงานกับรูปแบบภาพ OCR ที่พบบ่อย เช่น PNG, JPEG, BMP, และ TIFF  
- **โค้ดตัวอย่างทั่วไปสำหรับการดึงข้อความคืออะไร?** โหลดภาพเข้า `BufferedImage`, สร้างอินสแตนซ์ `AsposeOCR`, แล้วเรียก `RecognizePage`

## What is a Java OCR Library?

*java ocr library* คือชุดคลาส Java ที่สามารถวิเคราะห์ภาพแรสเตอร์และแปลงข้อความที่มองเห็นเป็นสตริงที่เครื่องคอมพิวเตอร์อ่านได้ Aspose.OCR for Java เป็นหนึ่งในไลบรารีเหล่านั้นที่ให้การจดจำความแม่นยำสูง, ตรวจจับภาษา, และรองรับรูปแบบภาพหลากหลาย

## Why Choose Aspose.OCR for Java?
- **High accuracy** สำหรับเอกสารที่พิมพ์และเขียนด้วยมือ  
- **OCR multiple languages** รวมถึง English, French, German, Chinese, และอื่น ๆ อีกมากมาย  
- API ที่เรียบง่ายทำงานโดยตรงกับ `BufferedImage` ไม่ต้องแปลงไฟล์กลาง  
- รองรับ **ocr image formats** อย่างเต็มรูปแบบ เช่น PNG, JPEG, BMP, TIFF, และ GIF

## Prerequisites

ก่อนเริ่มทำงาน โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้พร้อมแล้ว:

1. **Java Development Kit (JDK)** – เวอร์ชันล่าสุด (8 หรือใหม่กว่า) ดาวน์โหลดได้จาก [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html)  
2. **Aspose.OCR for Java library** – รับไฟล์ JAR ล่าสุดจากหน้าดาวน์โหลดของ Aspose ([install aspose ocr](https://releases.aspose.com/ocr/java/))  
3. **โฟลเดอร์ที่มีภาพตัวอย่าง** – ปรับค่า `dataDir` ในโค้ดให้ชี้ไปยังโฟลเดอร์นี้

## Import Packages

เพื่อเริ่มต้น ให้นำเข้าคลาสที่จำเป็น บล็อกนี้จะไม่เปลี่ยนแปลง; มันเพียงแค่ทำให้ API ของ Aspose OCR และยูทิลิตี้ I/O ของ Java พร้อมใช้งาน

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;
```

## How to Perform OCR on a BufferedImage

เราจะเดินผ่านกระบวนการทีละขั้นตอน แต่ละขั้นตอนมีคำอธิบายสั้น ๆ ตามด้วยโค้ดสแนปช็อตที่ไม่เปลี่ยนแปลงจากต้นฉบับ

### Step 1: Set Document Directory and Image Path  
กำหนดตำแหน่งที่เก็บภาพและระบุไฟล์ที่ต้องการประมวลผล

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

> **Pro tip:** ใช้เส้นทางแบบ absolute ระหว่างการพัฒนาเพื่อหลีกเลี่ยง `FileNotFoundException` แล้วเปลี่ยนเป็นเส้นทางแบบ relative สำหรับการใช้งานจริง

### Step 2: Create an AsposeOCR Instance  
สร้างอินสแตนซ์ของ OCR engine วัตถุนี้ให้คุณเข้าถึงเมธอดการจดจำทั้งหมด

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

### Step 3: Recognize Page from BufferedImage  
โหลดภาพเข้า `BufferedImage`, รัน OCR engine, และพิมพ์ผลลัพธ์ออกมา

```java
// Recognize page from BufferedImage
try {
    BufferedImage loaded = ImageIO.read(new File(imagePath));
    String result = api.RecognizePage(loaded);
    System.out.println("Result BufferedImage: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

**What’s happening?**  
1. `ImageIO.read` อ่านไฟล์เข้าสู่หน่วยความจำเป็น `BufferedImage`  
2. `api.RecognizePage` ทำการ OCR จริง  
3. ข้อความที่จดจำได้ถูกส่งกลับเป็น `String` และพิมพ์ลงคอนโซล

ทำซ้ำสามขั้นตอนนี้สำหรับแต่ละภาพที่ต้องการประมวลผล—เพียงเปลี่ยนค่า `imagePath` ตามความต้องการ

## Common Issues & Solutions

| Issue | Reason | Fix |
|-------|--------|-----|
| `NullPointerException` on `loaded` | ไม่พบไฟล์ภาพหรือรูปแบบไฟล์ไม่รองรับ | ตรวจสอบเส้นทางและยืนยันว่าไฟล์เป็น **ocr image format** ที่รองรับ (PNG, JPEG, BMP, TIFF) |
| ผลลัพธ์เป็นอักขระผิด | ไม่ได้ตั้งค่าภาษา หรืออักขระไม่รองรับ | AsposeOCR จะตรวจจับภาษาอัตโนมัติ แต่คุณสามารถกำหนดด้วย `api.setLanguage("eng")` สำหรับภาษาอังกฤษหรือรหัส ISO อื่น |
| ประมวลผลช้าเมื่อภาพขนาดใหญ่ | ความละเอียดสูงใช้หน่วยความจำมาก | ลดขนาดภาพด้วย `BufferedImage.getScaledInstance` ก่อนทำ OCR |

## Frequently Asked Questions (Original)

### Q1: Aspose.OCR รองรับหลายภาษาได้หรือไม่?

A1: ใช่, Aspose.OCR รองรับภาษาจำนวนมาก ทำให้เหมาะกับความต้องการจดจำข้อความที่หลากหลาย

### Q2: Aspose.OCR เข้ากันได้กับรูปแบบภาพต่าง ๆ หรือไม่?

A2: แน่นอน! Aspose.OCR สามารถประมวลผลภาพในหลายรูปแบบ ให้ความยืดหยุ่นในการทำ OCR ของคุณ

### Q3: Aspose.OCR มีการอัปเดตบ่อยแค่ไหน?

A3: Aspose ปล่อยอัปเดตเป็นประจำเพื่อเพิ่มฟีเจอร์และแก้ไขปัญหา ตรวจสอบ [documentation](https://reference.aspose.com/ocr/java/) สำหรับข้อมูลล่าสุด

### Q4: สามารถทดลองใช้ Aspose.OCR ก่อนซื้อได้หรือไม่?

A4: ได้, คุณสามารถดาวน์โหลดเวอร์ชันทดลองฟรีได้ [ที่นี่](https://releases.aspose.com/)

### Q5: จะหาแหล่งสนับสนุนชุมชนสำหรับ Aspose.OCR ได้จากที่ไหน?

A5: เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุนและพูดคุยกับชุมชน

## Additional FAQs (New)

**Q: จะติดตั้ง Aspose OCR ในโปรเจกต์ Maven อย่างไร?**  
A: เพิ่ม dependency ของ Aspose OCR ลงใน `pom.xml` โดยใช้พารามิเตอร์ที่ระบุบนหน้าดาวน์โหลดของ Aspose

**Q: สามารถใช้ไลบรารีนี้ดึงข้อความจาก PDF ที่สแกนได้หรือไม่?**  
A: ได้—แปลงแต่ละหน้า PDF เป็นภาพ (เช่น ใช้ Aspose.PDF) แล้วใช้กระบวนการ OCR กับ `BufferedImage` เดียวกัน

**Q: ไลบรารีรองรับ OCR บนภาพสีหรือไม่?**  
A: รองรับอย่างเต็มที่ Aspose OCR ทำงานกับภาพสี, grayscale, และ binary; อย่างไรก็ตาม ภาพที่มีคอนทราสต์สูงแบบ black‑on‑white มักให้ความแม่นยำดีที่สุด

**Q: มีขีดจำกัดจำนวนหน้าที่สามารถประมวลผลต่อครั้งหรือไม่?**  
A: ไม่มีขีดจำกัดที่แน่นอน แต่การใช้หน่วยความจำจะเพิ่มตามขนาดภาพ ควรประมวลผลเป็นชุดย่อยเพื่อหลีกเลี่ยง `OutOfMemoryError`

**Q: จะปรับปรุงความแม่นยำสำหรับข้อความเขียนมืออย่างไร?**  
A: เปิดโหมดการจดจำมือ (หากมี) หรือทำการพรี‑โปรเซสภาพเพื่อเพิ่มคอนทราสต์และลดสัญญาณรบกวน

---

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**อัปเดตล่าสุด:** 2025-11-29  
**ทดสอบด้วย:** Aspose.OCR 24.11 for Java  
**ผู้เขียน:** Aspose