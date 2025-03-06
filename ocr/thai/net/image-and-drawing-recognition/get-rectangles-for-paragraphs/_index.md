---
title: รับสี่เหลี่ยมสำหรับย่อหน้าในการจดจำรูปภาพ OCR
linktitle: รับสี่เหลี่ยมสำหรับย่อหน้าในการจดจำรูปภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดล็อกความสามารถ OCR ขั้นสูงด้วย Aspose.OCR สำหรับ .NET แยกสี่เหลี่ยมย่อหน้าได้อย่างง่ายดาย
weight: 11
url: /th/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับสี่เหลี่ยมสำหรับย่อหน้าในการจดจำรูปภาพ OCR

## การแนะนำ

ยินดีต้อนรับสู่คำแนะนำที่ครอบคลุมของเราเกี่ยวกับการใช้ประโยชน์จาก Aspose.OCR สำหรับ .NET เพื่อแยกสี่เหลี่ยมย่อหน้าในการจดจำรูปภาพ OCR หากคุณต้องการปรับปรุงความสามารถในการประมวลผลเอกสารและควบคุมประสิทธิภาพของ Optical Character Recognition (OCR) ในแอปพลิเคชัน .NET ของคุณ คุณมาถูกที่แล้ว

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกบทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- ความรู้พื้นฐานเกี่ยวกับการพัฒนา C# และ .NET
-  สภาพแวดล้อมการพัฒนาที่ตั้งค่าด้วย Aspose.OCR สำหรับ .NET หากคุณยังไม่ได้คุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.aspose.com/ocr/net/).
- ความเข้าใจแนวคิดการประมวลผลภาพและความสำคัญของ OCR ในการดึงข้อความออกจากรูปภาพ

## นำเข้าเนมสเปซ

ในโค้ด C# ของคุณ ตรวจสอบให้แน่ใจว่าคุณได้นำเข้าเนมสเปซที่จำเป็นเพื่อใช้ Aspose.OCR อย่างมีประสิทธิภาพ รวมสิ่งต่อไปนี้ไว้ที่ด้านบนของไฟล์:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

เริ่มต้นด้วยการเริ่มต้นเส้นทางไปยังไดเร็กทอรีเอกสารของคุณซึ่งจัดเก็บรูปภาพสำหรับการประมวลผล OCR:

```csharp
string dataDir = "Your Document Directory";
```

## ขั้นตอนที่ 2: เริ่มต้นอินสแตนซ์ AsposeOcr

สร้างอินสแตนซ์ของคลาส AsposeOcr เพื่อเข้าถึงฟังก์ชัน OCR:

```csharp
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 3: ระบุเส้นทางรูปภาพ

กำหนดเส้นทางแบบเต็มไปยังรูปภาพที่คุณต้องการประมวลผล:

```csharp
string fullPath = dataDir + "sample.png";
```

## ขั้นตอนที่ 4: จดจำรูปภาพและรับสี่เหลี่ยมย่อหน้า

 เรียกใช้`GetRectangles` วิธีการรับสี่เหลี่ยมสำหรับย่อหน้าในภาพ OCR ชุด`detect_areas` ถึง`true` หากคุณต้องการแยกย่อหน้า:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## ขั้นตอนที่ 5: พิมพ์ผลลัพธ์

พิมพ์พิกัดของพื้นที่ที่ระบุ:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## ขั้นตอนที่ 6: บทสรุป

ยินดีด้วย! คุณได้ดำเนินการกระบวนการจดจำรูปภาพ OCR เพื่อรับสี่เหลี่ยมสำหรับย่อหน้าโดยใช้ Aspose.OCR สำหรับ .NET สำเร็จแล้ว

## บทสรุป

ในบทช่วยสอนนี้ เราได้สำรวจขั้นตอนพื้นฐานในการรวม Aspose.OCR สำหรับ .NET เข้ากับแอปพลิเคชันของคุณ ซึ่งช่วยให้คุณสามารถแยกสี่เหลี่ยมย่อหน้าออกจากรูปภาพที่ประมวลผลด้วย OCR Aspose.OCR ทำให้การนำ OCR ไปใช้ง่ายขึ้น ทำให้เป็นเครื่องมืออันทรงคุณค่าสำหรับการประมวลผลเอกสารและการแยกข้อความ

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR เข้ากันได้กับรูปแบบรูปภาพที่แตกต่างกันหรือไม่

A1: ใช่ Aspose.OCR รองรับรูปแบบภาพที่หลากหลาย รวมถึง PNG, JPEG และ TIFF

### คำถามที่ 2: ฉันสามารถใช้ Aspose.OCR สำหรับการประมวลผลภาพหลายภาพเป็นชุดได้หรือไม่

A2: แน่นอน! Aspose.OCR อำนวยความสะดวกในการประมวลผลเป็นชุดเพื่อจัดการภาพหลายภาพได้อย่างราบรื่น

### คำถามที่ 3: Aspose.OCR สำหรับ .NET มีรุ่นทดลองใช้ฟรีหรือไม่

 A3: ได้ คุณสามารถทดลองใช้งานฟรีได้[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 4: ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.OCR ได้อย่างไร

 A4: คุณสามารถขอรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 5: ฉันจะรับการสนับสนุนและการสนทนาเพิ่มเติมที่เกี่ยวข้องกับ Aspose.OCR ได้ที่ไหน

 A5: ตรงไปที่[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) สำหรับการสนับสนุนและการอภิปรายของชุมชน
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
