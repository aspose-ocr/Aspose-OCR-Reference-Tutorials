---
date: 2025-12-13
description: เรียนรู้วิธีดึงข้อความจากภาพโดยใช้ Aspose.OCR สำหรับ Java พร้อมการเลือกภาษา
  บทเรียน Aspose OCR Java แบบขั้นตอนนี้แสดงการกำหนดค่า OCR อย่างแม่นยำ.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: วิธีดึงข้อความจากภาพพร้อมการเลือกภาษาโดยใช้ Aspose.OCR
url: /th/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีดึงข้อความจากรูปภาพพร้อมการเลือกภาษาโดยใช้ Aspose.OCR

## Introduction

การดึงข้อความจากไฟล์รูปภาพเป็นความต้องการทั่วไป ไม่ว่าจะเป็นการแปลงเอกสารสแกนเป็นดิจิทัล การประมวลผลใบเสร็จ หรือการสร้างคลังข้อมูลที่สามารถค้นหาได้ Aspose.OCR for Java ทำให้ภารกิจนี้ง่ายขึ้นและให้การควบคุมระดับละเอียดเกี่ยวกับการเลือกภาษา การแก้ไขการเอียง และพื้นที่การรับรู้ ในบทเรียนนี้เราจะเดินผ่านตัวอย่างเต็มรูปแบบที่แสดง **วิธีดึงข้อความจากรูปภาพ** ด้วยการตั้งค่าภาษาเฉพาะ เพื่อให้คุณสามารถผสาน OCR ที่เชื่อถือได้เข้ากับแอปพลิเคชัน Java ของคุณได้ทันที

## Quick Answers
- **ไลบรารีใดที่จัดการ OCR ใน Java?** Aspose.OCR for Java  
- **การตั้งค่าใดที่เลือกภาษา?** `settings.setLanguage(Language.Eng)` (หรือภาษาอื่นที่รองรับ)  
- **ฉันต้องการไลเซนส์สำหรับการพัฒนาหรือไม่?** ไลเซนส์ทดลองฟรีใช้ได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **ฉันสามารถจำกัด OCR ให้ทำงานในส่วนของภาพได้หรือไม่?** ใช่, ใช้ `RecognitionSettings.setRecognitionAreas()` พร้อมสี่เหลี่ยม.  
- **ระยะเวลาการทำงานโดยทั่วไปคือเท่าไหร่?** ไม่กี่วินาทีต่อหน้าในแล็ปท็อปมาตรฐาน, ขึ้นอยู่กับขนาดภาพและความซับซ้อนของภาษา.

## What is “extract text from image”?

การดึงข้อความจากรูปภาพ (OCR) แปลงการแสดงผลของอักขระจากภาพเป็นสตริงที่เครื่องคอมพิวเตอร์อ่านได้ ซึ่งทำให้สามารถค้นหา, วิเคราะห์, และกระบวนการดึงข้อมูลที่โดยปกติจะต้องทำการถอดข้อความด้วยมือได้

## Why use Aspose.OCR with language selection?

- **การสนับสนุนหลายภาษา** – เลือกภาษาที่ปรากฏในภาพของคุณอย่างแม่นยำเพื่อเพิ่มความถูกต้อง.  
- **การควบคุมละเอียด** – ปรับการเอียง, กำหนดพื้นที่การรับรู้, และตั้งค่าพฤติกรรมการเอียงอัตโนมัติ.  
- **Pure Java API** – ไม่มีการพึ่งพา native, ง่ายต่อการผสานเข้ากับโครงการ Java ใดก็ได้.  
- **ข้อมูลผลลัพธ์ที่ครบถ้วน** – รับข้อความธรรมดา, JSON, สี่เหลี่ยมขอบ, และคำเตือนในการเรียกครั้งเดียว.

## Prerequisites

ก่อนเริ่ม, ตรวจสอบให้แน่ใจว่าคุณมี:

- **Java Development Kit (JDK)** ติดตั้ง (JDK 8 หรือใหม่กว่า).  
- **Aspose.OCR for Java** library – ดาวน์โหลดจากเว็บไซต์อย่างเป็นทางการ [ที่นี่](https://reference.aspose.com/ocr/java/).  
- ไฟล์รูปภาพที่มีข้อความที่คุณต้องการดึง, เช่น `p3.png`.

## Import Packages

In your Java source file, include the required Aspose.OCR classes and standard Java utilities:

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

## Step‑by‑Step Guide

### Step 1: Set up Your Document Directory

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Replace `"Your Document Directory"` with the absolute path where `p3.png` resides.

เปลี่ยน `"Your Document Directory"` ให้เป็นเส้นทางเต็มที่ที่มีไฟล์ `p3.png` อยู่

### Step 2: Define the Image Path

```java
// The image path
String file = dataDir + "p3.png";
```

Make sure the `file` variable points to the exact image you intend to process.

ตรวจสอบให้แน่ใจว่า ตัวแปร `file` ชี้ไปยังไฟล์รูปภาพที่ต้องการประมวลผลอย่างถูกต้อง

### Step 3: Create Aspose.OCR API Instance

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

The `AsposeOCR` object gives you access to all OCR operations.

อ็อบเจกต์ `AsposeOCR` ให้คุณเข้าถึงการทำงาน OCR ทั้งหมด

### Step 4: Set Recognition Options (Language Selection)

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

Here we:

1. Disable auto‑skew because we provide a manual skew value.  
2. Define a rectangular region (`RecognitionAreas`) to limit OCR to the part of the image that actually contains text.  
3. Set the **language** to English (`Language.Eng`). Change this to `Language.Fra`, `Language.Spa`, etc., depending on your source image.

ในที่นี้เรา:

1. ปิดการทำ auto‑skew เนื่องจากเรากำหนดค่าการเอียงด้วยตนเอง.  
2. กำหนดพื้นที่สี่เหลี่ยม (`RecognitionAreas`) เพื่อจำกัด OCR ให้ทำงานเฉพาะส่วนของภาพที่มีข้อความจริง.  
3. ตั้งค่า **ภาษา** เป็น English (`Language.Eng`). เปลี่ยนเป็น `Language.Fra`, `Language.Spa` ฯลฯ ตามภาพต้นฉบับของคุณ.

### Step 5: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

The `RecognizePage` call runs the OCR engine using the image and the settings you defined. The outcome is stored in a `RecognitionResult` object.

การเรียก `RecognizePage` จะรันเครื่องมือ OCR ด้วยภาพและการตั้งค่าที่คุณกำหนด ผลลัพธ์จะถูกเก็บไว้ในอ็อบเจกต์ `RecognitionResult`

### Step 6: Print and Utilize Results

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

The console output shows:

- The full extracted text (`recognitionText`).  
- Text for each defined rectangle (`recognitionAreasText`).  
- Bounding rectangle coordinates.  
- A JSON representation for easy downstream processing.  
- Detected skew angle and any warnings.

You can now feed `result.recognitionText` into your business logic—store it, index it, or pass it to another service.

ผลลัพธ์ที่แสดงบนคอนโซลประกอบด้วย:

- ข้อความที่ดึงทั้งหมด (`recognitionText`).  
- ข้อความสำหรับแต่ละสี่เหลี่ยมที่กำหนด (`recognitionAreasText`).  
- พิกัดของสี่เหลี่ยมขอบ.  
- ตัวแทนในรูปแบบ JSON เพื่อการประมวลผลต่อไปอย่างง่ายดาย.  
- มุมการเอียงที่ตรวจพบและคำเตือนใด ๆ

คุณสามารถนำ `result.recognitionText` ไปใช้ในตรรกะธุรกิจของคุณได้—เก็บไว้, ทำดัชนี, หรือส่งต่อให้บริการอื่น

## Common Issues and Solutions

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|-------|-----|
| **อักขระเสีย** | เลือกภาษาผิด | ตั้งค่า `Language` enum ให้ถูกต้อง (เช่น `Language.Fra` สำหรับภาษาฝรั่งเศส) |
| **ไม่มีข้อความที่ส่งกลับ** | พื้นที่การรับรู้ไม่ครอบคลุมข้อความ | ปรับพิกัดของ `Rectangle` หรือเอา `RecognitionAreas` ออกเพื่อประมวลผลภาพทั้งหมด |
| **ประสิทธิภาพช้า** | ภาพขนาดใหญ่มากหรือความละเอียดสูง | ลดขนาดภาพก่อน OCR หรือเพิ่มการจัดสรรหน่วยความจำให้กับ JVM |
| **คำเตือนเกี่ยวกับรูปแบบที่ไม่รองรับ** | รูปแบบภาพไม่ถูกต้อง | แปลงภาพเป็น PNG, JPEG หรือ TIFF ก่อนประมวลผล |

## Frequently Asked Questions

**ถาม: ฉันสามารถจดจำหลายภาษาในหนึ่งการเรียก OCR ได้หรือไม่?**  
**ตอบ:** ใช่. ใช้ `settings.setLanguage(Language.Eng | Language.Fra)` เพื่อเปิดใช้งานการจดจำหลายภาษา.

**ถาม: รูปแบบไฟล์ภาพใดบ้างที่ Aspose.OCR รองรับ?**  
**ตอบ:** PNG, JPEG, BMP, TIFF, GIF และรูปแบบอื่น ๆ เพียงระบุเส้นทางไฟล์ที่ถูกต้อง

**ถาม: มีขนาดจำกัดสำหรับภาพหรือไม่?**  
**ตอบ:** ไม่มีขีดจำกัดที่แน่นอน แต่ภาพขนาดใหญ่มากจะเพิ่มการใช้หน่วยความจำและเวลาในการประมวลผล ควรปรับขนาดไฟล์ใหญ่ให้เหมาะสม

**ถาม: ฉันจะได้ไลเซนส์สำหรับการใช้งานจริงอย่างไร?**  
**ตอบ:** ซื้อไลเซนส์จากเว็บไซต์ Aspose แล้วนำไปใช้ผ่านคลาส `License` ตามที่แสดงในเอกสาร Aspose

**ถาม: ฉันสามารถดึงข้อความจากหน้า PDF ได้โดยตรงหรือไม่?**  
**ตอบ:** ไม่ได้โดยตรงกับ Aspose.OCR. ต้องแปลงหน้า PDF เป็นภาพก่อน (เช่น ใช้ Aspose.PDF) แล้วจึงทำ OCR

## Conclusion

คุณได้เห็นวิธี **ดึงข้อความจากรูปภาพ** ด้วย Aspose.OCR for Java พร้อมการเลือกภาษาที่เหมาะสมและการจำกัดการรับรู้ให้ทำงานในพื้นที่เฉพาะ วิธีนี้ให้ผลลัพธ์ OCR ที่แม่นยำและประสิทธิภาพสูง สามารถฝังลงในกระบวนการทำงานที่ใช้ Java ใดก็ได้—from ระบบจัดการเอกสารถึงสายการจับข้อมูล

---

**อัปเดตล่าสุด:** 2025-12-13  
**ทดสอบด้วย:** Aspose.OCR 24.11 for Java  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}