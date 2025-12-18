---
date: 2025-12-10
description: เรียนรู้วิธีการจดจำข้อความจากภาพและดึงย่อหน้าจากภาพโดยใช้ Aspose.OCR
  สำหรับ Java คู่มือแบบขั้นตอนพร้อมตัวอย่างโค้ด
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: จดจำข้อความจากภาพและดึงสี่เหลี่ยมของพื้นที่ข้อความ
url: /th/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากภาพและดึงสี่เหลี่ยมพื้นที่ข้อความ

## Introduction

หากคุณต้องการ **recognize text from image** ไฟล์ในแอปพลิเคชัน Java, Aspose.OCR for Java ให้วิธีที่รวดเร็วและแม่นยำในการทำเช่นนั้น ในบทแนะนำนี้เราจะอธิบายขั้นตอนที่จำเป็นเพื่อสกัดย่อหน้าจากภาพ, รับสี่เหลี่ยมขอบเขตสำหรับแต่ละพื้นที่ข้อความ, และพิมพ์พิกัดเหล่านั้นไปยังคอนโซล เมื่อเสร็จคุณจะเข้าใจว่าทำไมวิธีนี้ถึงได้ผล, วิธีการรวมไลบรารี, และจุดที่คุณสามารถขยายเพื่อใช้ในกรณีของคุณเอง

## Quick Answers
- **“recognize text from image” หมายถึงอะไร?** หมายถึงการแปลงอักขระที่มองเห็นในภาพให้เป็นข้อมูลสตริงที่สามารถแก้ไขได้.  
- **ไลบรารีใดที่จัดการเรื่องนี้ใน Java?** Aspose.OCR for Java.  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** มีใบอนุญาตชั่วคราวสำหรับการทดสอบ; จำเป็นต้องมีใบอนุญาตเต็มสำหรับการใช้งานจริง.  
- **ฉันสามารถสกัดย่อหน้าต่างจากคำเดี่ยวได้หรือไม่?** ได้ – ใช้ `AreasType.PARAGRAPHS` เพื่อรับสี่เหลี่ยมระดับย่อหน้า.  
- **โค้ดนี้เข้ากันได้กับ Java 11+ หรือไม่?** แน่นอน, API ทำงานกับ Java 11 และรุ่นต่อ ๆ ไป.

## What is “recognize text from image” in Aspose.OCR?
`RecognizePage` ของ Aspose.OCR วิเคราะห์บิตแมพ, ใช้อัลกอริทึม OCR, และคืนสตริงที่จดจำได้ เมื่อคุณร้องขอพื้นที่ข้อความ, ไลบรารีจะคำนวณพิกัด `Rectangle` ที่แม่นยำสำหรับแต่ละบล็อกของข้อความ, ทำให้การไฮไลท์หรือประมวลผลส่วนเฉพาะในภายหลังเป็นเรื่องง่าย

## Why use Aspose.OCR for Java?
- **High accuracy** – รองรับหลายภาษาและฟอนต์ที่ซับซ้อน.  
- **Easy integration** – JAR เพียงไฟล์เดียวเพิ่มความสามารถ OCR ครบวงจร.  
- **Flexible output** – คุณสามารถดึงข้อความดิบ, HTML ที่จัดรูปแบบ, หรือสี่เหลี่ยมพื้นที่ข้อความที่แม่นยำ.  
- **Thread‑safe** – เหมาะสำหรับสภาพแวดล้อมเซิร์ฟเวอร์ที่มีการประมวลผลสูง.

## Prerequisites

- **Java Development Kit** (JDK 11 หรือใหม่กว่า) ติดตั้งบนเครื่องของคุณ.  
- **Aspose.OCR for Java** library – ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการ [here](https://releases.aspose.com/ocr/java/).  
- IDE หรือเครื่องมือสร้าง (Maven/Gradle) เพื่อจัดการการพึ่งพา JAR.

## Import Packages

ในโปรเจค Java ของคุณ, ให้ import คลาสที่จำเป็น:

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

## Step‑by‑Step Guide

### Step 1: Set Up Your Project
สร้างโปรเจค Java ใหม่ (หรือเพิ่มในโปรเจคที่มีอยู่) และวางไฟล์ JAR ของ Aspose.OCR ลงใน classpath หากคุณใช้ Maven ให้เพิ่ม dependency ตามที่อธิบายในแพคเกจดาวน์โหลด

### Step 2: Define Document Directory and Image Path
ระบุที่ตั้งของภาพตัวอย่างของคุณ:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Step 3: Create Aspose.OCR Instance
สร้างอินสแตนซ์ของ Aspose.OCR:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Step 4: Recognize Text in the Image
เรียก `RecognizePage` เพื่อแปลงรูปภาพเป็นข้อความธรรมดา ขั้นตอนนี้แสดงความสามารถหลักของ **recognize text from image**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Step 5: Get Rectangles with Text Areas
ตอนนี้ดึงสี่เหลี่ยมขอบเขตสำหรับแต่ละย่อหน้า (หรือประเภทพื้นที่อื่น) นี่คือจุดที่คุณ **extract paragraphs from image** และรับพิกัดของพวกมัน:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Common Issues & Troubleshooting

| อาการ | สาเหตุที่เป็นไปได้ | วิธีแก้ |
|---------|--------------|-----|
| `IOException` on `RecognizePage` | เส้นทางไฟล์ไม่ถูกต้องหรือไม่มีสิทธิ์อ่าน | ตรวจสอบว่า `imagePath` ชี้ไปยังไฟล์ PNG/JPG ที่มีอยู่และแอปมีสิทธิ์เข้าถึงระบบไฟล์. |
| Empty result string | ภาพคุณภาพต่ำหรือภาษาที่ไม่รองรับ | ทำการประมวลผลล่วงหน้าภาพ (เพิ่มคอนทราสต์, ทำไบนารี) หรือระบุภาษาที่ถูกต้องโดยใช้ `api.setLanguage("eng")`. |
| No rectangles returned | ใช้ `AreasType` ผิด (เช่น `WORDS` เมื่อคาดหวังย่อหน้า) | เปลี่ยนเป็น `AreasType.PARAGRAPHS` หรือ `AreasType.LINES` ตามต้องการ. |

## Frequently Asked Questions

**Q: Aspose.OCR รองรับ Java 11 หรือไม่?**  
A: ใช่, Aspose.OCR ทำงานกับ Java 11 และรุ่นต่อ ๆ ไป.

**Q: ฉันสามารถใช้ Aspose.OCR สำหรับโครงการส่วนบุคคลและเชิงพาณิชย์ได้หรือไม่?**  
A: ใช่, คุณสามารถใช้ในโครงการทุกประเภท สำหรับรายละเอียดใบอนุญาต, เยี่ยมชม [here](https://purchase.aspose.com/buy).

**Q: ฉันจะขอใบอนุญาตชั่วคราวสำหรับการประเมินได้อย่างไร?**  
A: คุณสามารถรับใบอนุญาตชั่วคราวได้ที่ [here](https://purchase.aspose.com/temporary-license/).

**Q: ฉันจะหาแหล่งสนับสนุนจากชุมชนหรือความช่วยเหลืออย่างเป็นทางการได้จากที่ไหน?**  
A: สำหรับการสนับสนุนและการสนทนา, เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

**Q: Aspose.OCR รองรับการทำงานหลายเธรดหรือไม่?**  
A: ใช่, ไลบรารีเป็น thread‑safe และสามารถใช้ในสภาพแวดล้อมพร้อมกันเพื่อประสิทธิภาพที่ดีกว่า.

## Conclusion

ในบทแนะนำนี้คุณได้เรียนรู้วิธี **recognize text from image** ไฟล์โดยใช้ Aspose.OCR for Java, สกัดย่อหน้า, และดึงสี่เหลี่ยมที่แม่นยำซึ่งล้อมรอบแต่ละบล็อกของข้อความ ความสามารถเหล่านี้ทำให้คุณสามารถสร้าง PDF ที่ค้นหาได้, ไฮไลท์ข้อความใน UI overlay, หรือส่งข้อมูลโครงสร้างไปยังกระบวนการต่อไป สำรวจ API เพิ่มเติมเพื่อปรับแต่งการตั้งค่าภาษา, จัดการรูปแบบภาพต่าง ๆ, หรือรวมกับคลาวด์สตอเรจ.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}