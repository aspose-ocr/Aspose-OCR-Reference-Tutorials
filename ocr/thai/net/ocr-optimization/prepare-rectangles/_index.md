---
title: เตรียมสี่เหลี่ยมในการจดจำภาพ OCR
linktitle: เตรียมสี่เหลี่ยมในการจดจำภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดล็อกศักยภาพของ Aspose.OCR สำหรับ .NET ด้วยคำแนะนำที่ครอบคลุมของเรา เรียนรู้วิธีการเตรียมสี่เหลี่ยมสำหรับการจดจำรูปภาพทีละขั้นตอน ยกระดับแอปพลิเคชัน .NET ของคุณด้วยการผสานรวม OCR ที่ราบรื่น
weight: 11
url: /th/net/ocr-optimization/prepare-rectangles/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เตรียมสี่เหลี่ยมในการจดจำภาพ OCR

## การแนะนำ

ในภูมิทัศน์ของเทคโนโลยีที่เปลี่ยนแปลงตลอดเวลา Optical Character Recognition (OCR) มีบทบาทสำคัญในการแปลงรูปภาพให้เป็นข้อความที่เครื่องอ่านได้ Aspose.OCR สำหรับ .NET โดดเด่นในฐานะโซลูชันที่แข็งแกร่งสำหรับนักพัฒนาที่ต้องการบูรณาการความสามารถ OCR เข้ากับแอปพลิเคชัน .NET ของตนได้อย่างราบรื่น ในคู่มือที่ครอบคลุมนี้ เราจะสำรวจกระบวนการเตรียมสี่เหลี่ยมในการจดจำรูปภาพ OCR โดยใช้ Aspose.OCR สำหรับ .NET

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- ความรู้ด้านการทำงานของการพัฒนา .NET
-  ติดตั้ง Aspose.OCR สำหรับไลบรารี .NET แล้ว คุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.aspose.com/ocr/net/).
- ความเข้าใจพื้นฐานเกี่ยวกับแนวคิดการรู้จำภาพ

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็นเพื่อเริ่มต้นการเดินทาง OCR ของเรา:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

 เริ่มต้นด้วยการระบุไดเร็กทอรีที่เก็บเอกสารของคุณ แทนที่`"Your Document Directory"` พร้อมเส้นทางสู่เอกสารของคุณจริง

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";

// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 2: จดจำภาพที่มีหลายสี่เหลี่ยมผืนผ้า

ในขั้นตอนนี้ เราจะสาธิตวิธีการจดจำข้อความจากรูปภาพโดยใช้สี่เหลี่ยมหลายอัน ทำตามขั้นตอนย่อยเหล่านี้:

### 2.1 กำหนดสี่เหลี่ยม

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 ดำเนินการรับรู้ OCR

```csharp
// กรณีแรก
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// แสดงข้อความที่รู้จัก
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## ขั้นตอนที่ 3: จดจำรูปภาพด้วยการตั้งค่าการจดจำ

ในขั้นตอนนี้ เราจะแสดงวิธีการอื่นโดยใช้ RecognitionSettings สำหรับการจดจำรูปภาพ:

### 3.1 กำหนดการตั้งค่าการรับรู้

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 แสดงข้อความที่รู้จัก

```csharp
// แสดงข้อความที่รู้จัก
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## บทสรุป

ยินดีด้วย! คุณได้สำรวจกระบวนการเตรียมสี่เหลี่ยมในการจดจำรูปภาพ OCR โดยใช้ Aspose.OCR สำหรับ .NET สำเร็จแล้ว คู่มือนี้ช่วยให้คุณสามารถรวม OCR เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น ช่วยเพิ่มความสามารถในการจดจำข้อความ

### คำถามที่พบบ่อย

### คำถามที่ 1: ฉันสามารถใช้ Aspose.OCR สำหรับ .NET กับเฟรมเวิร์ก .NET อื่นๆ ได้หรือไม่

ตอบ 1: ใช่ Aspose.OCR สำหรับ .NET เข้ากันได้กับกรอบงาน .NET ต่างๆ

### คำถามที่ 2: Aspose.OCR สำหรับ .NET มีรุ่นทดลองใช้ฟรีหรือไม่

 A2: แน่นอน! คุณสามารถเข้าถึงการทดลองใช้ฟรี[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 3: ฉันจะได้รับการสนับสนุนสำหรับ Aspose.OCR สำหรับ .NET ได้อย่างไร

 A3: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) สำหรับการสนับสนุนโดยเฉพาะ

### คำถามที่ 4: ฉันสามารถขอรับใบอนุญาตชั่วคราวเพื่อการทดสอบได้หรือไม่

 A4: ได้ คุณสามารถขอรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 5: ฉันจะหาเอกสารสำหรับ Aspose.OCR สำหรับ .NET ได้ที่ไหน

 A5: มีเอกสารประกอบให้[ที่นี่](https://reference.aspose.com/ocr/net/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
