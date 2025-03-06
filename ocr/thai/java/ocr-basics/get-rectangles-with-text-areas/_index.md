---
title: รับสี่เหลี่ยมพร้อมพื้นที่ข้อความใน Aspose.OCR
linktitle: รับสี่เหลี่ยมพร้อมพื้นที่ข้อความใน Aspose.OCR
second_title: Aspose.OCR Java API
description: ปลดล็อกพลังของ Aspose.OCR สำหรับ Java เรียนรู้วิธีแยกข้อความจากรูปภาพได้อย่างราบรื่นในคำแนะนำทีละขั้นตอนนี้ ดาวน์โหลดเดี๋ยวนี้เพื่อการรู้จำข้อความที่มีประสิทธิภาพ
weight: 12
url: /th/java/ocr-basics/get-rectangles-with-text-areas/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับสี่เหลี่ยมพร้อมพื้นที่ข้อความใน Aspose.OCR

## การแนะนำ

คุณกำลังมองหาที่จะรวมความสามารถในการรู้จำอักขระด้วยแสง (OCR) อันทรงพลังเข้ากับแอปพลิเคชัน Java ของคุณหรือไม่? Aspose.OCR สำหรับ Java เป็นโซลูชันที่เหมาะกับคุณสำหรับการแยกข้อความจากรูปภาพที่แม่นยำและมีประสิทธิภาพ บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการรับสี่เหลี่ยมพร้อมพื้นที่ข้อความโดยใช้ Aspose.OCR ซึ่งช่วยให้คุณใช้ประโยชน์จากไลบรารี Java OCR นี้ได้อย่างเต็มประสิทธิภาพ

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- สภาพแวดล้อมการพัฒนา Java: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Java บนระบบของคุณแล้ว
-  Aspose.OCR สำหรับไลบรารี Java: ดาวน์โหลดและตั้งค่าไลบรารี Aspose.OCR คุณสามารถค้นหาลิงค์ดาวน์โหลด[ที่นี่](https://releases.aspose.com/ocr/java/).

## แพ็คเกจนำเข้า

ในโปรเจ็กต์ Java ของคุณ ให้นำเข้าแพ็คเกจที่จำเป็นเพื่อใช้ประโยชน์จากฟังก์ชันการทำงานของ Aspose.OCR:

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

## ขั้นตอนที่ 1: ตั้งค่าโครงการของคุณ

ตรวจสอบให้แน่ใจว่าคุณมีโปรเจ็กต์ Java พร้อมแล้ว และไลบรารี Aspose.OCR ได้รับการรวมเข้าด้วยกัน

## ขั้นตอนที่ 2: กำหนดไดเรกทอรีเอกสารและเส้นทางรูปภาพ

```java
// เส้นทางไปยังไดเร็กทอรีเอกสาร
String dataDir = "Your Document Directory";

// เส้นทางภาพ
String imagePath = dataDir + "p3.png";
```

## ขั้นตอนที่ 3: สร้างอินสแตนซ์ Aspose.OCR

```java
// สร้างอินสแตนซ์ Aspose.OCR
AsposeOCR api = new AsposeOCR();
```

## ขั้นตอนที่ 4: จดจำข้อความในรูปภาพ

```java
try {
    // จดจำหน้าตามเส้นทางแบบเต็มไปยังไฟล์
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

## ขั้นตอนที่ 5: รับสี่เหลี่ยมพร้อมพื้นที่ข้อความ

```java
// รับสี่เหลี่ยมพร้อมพื้นที่ข้อความในภาพ
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// พิมพ์สี่เหลี่ยมพื้นที่ข้อความแต่ละอัน
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## บทสรุป

ในบทช่วยสอนนี้ คุณได้เรียนรู้วิธีผสานรวม Aspose.OCR สำหรับ Java เข้ากับโปรเจ็กต์ของคุณเพื่อแยกข้อความจากรูปภาพอย่างมีประสิทธิภาพ Aspose.OCR ทำให้งาน OCR ง่ายขึ้น โดยให้ผลลัพธ์ที่แม่นยำเพื่อประสบการณ์ผู้ใช้ที่ราบรื่น

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR เข้ากันได้กับ Java 11 หรือไม่

A1: ใช่ Aspose.OCR เข้ากันได้กับ Java 11 และเวอร์ชันที่ใหม่กว่า

### คำถามที่ 2: ฉันสามารถใช้ Aspose.OCR สำหรับทั้งโครงการส่วนตัวและเชิงพาณิชย์ได้หรือไม่

 ตอบ 2: ได้ Aspose.OCR สามารถใช้กับทั้งโครงการส่วนตัวและเชิงพาณิชย์ สำหรับรายละเอียดใบอนุญาต โปรดไปที่[ที่นี่](https://purchase.aspose.com/buy).

### คำถามที่ 3: ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.OCR ได้อย่างไร

 A3: คุณสามารถขอรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 4: ฉันจะรับการสนับสนุนสำหรับ Aspose.OCR ได้ที่ไหน

 A4: สำหรับการสนับสนุนและการสนทนา โปรดไปที่[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16).

### คำถามที่ 5: Aspose.OCR รองรับการทำงานแบบมัลติเธรดหรือไม่

A5: ใช่ Aspose.OCR รองรับมัลติเธรดเพื่อประสิทธิภาพที่ดีขึ้นในสภาพแวดล้อมที่เกิดขึ้นพร้อมกัน

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
