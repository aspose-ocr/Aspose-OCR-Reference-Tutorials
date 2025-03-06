---
title: รับตัวเลือกสำหรับอักขระที่จดจำในการจดจำรูปภาพ OCR
linktitle: รับตัวเลือกสำหรับอักขระที่จดจำในการจดจำรูปภาพ OCR
second_title: Aspose.OCR .NET API
description: ปรับปรุงแอปพลิเคชัน .NET ของคุณด้วย Aspose.OCR เพื่อการรู้จำอักขระที่แม่นยำ ปฏิบัติตามคำแนะนำทีละขั้นตอนของเราเพื่อดึงตัวเลือกสำหรับอักขระที่รู้จักในการจดจำรูปภาพ
weight: 10
url: /th/net/text-recognition/get-choices-for-recognized-characters/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับตัวเลือกสำหรับอักขระที่จดจำในการจดจำรูปภาพ OCR

## การแนะนำ

การปลดล็อกพลังของการรู้จำอักขระด้วยแสง (OCR) เป็นสิ่งสำคัญในยุคดิจิทัลในปัจจุบัน และ Aspose.OCR สำหรับ .NET ถือเป็นโซลูชันที่แข็งแกร่งสำหรับการรู้จำอักขระที่แม่นยำ ในบทช่วยสอนนี้ เราจะเจาะลึกคุณสมบัติเฉพาะ: การได้รับตัวเลือกสำหรับอักขระที่รู้จัก ในตอนท้ายของคู่มือนี้ คุณจะรวมฟังก์ชันการทำงานนี้เข้ากับแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- ความรู้พื้นฐานเกี่ยวกับการพัฒนา C# และ .NET
- ติดตั้ง Visual Studio บนเครื่องของคุณแล้ว
-  Aspose.OCR สำหรับไลบรารี .NET ซึ่งคุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.aspose.com/ocr/net/).

## นำเข้าเนมสเปซ

ในโปรเจ็กต์ C# ของคุณ ให้เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็น:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

เริ่มต้นด้วยการเริ่มต้นอินสแตนซ์ของ Aspose.OCR:

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";

// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 2: ระบุเส้นทางรูปภาพ

กำหนดเส้นทางสำหรับรูปภาพที่คุณต้องการวิเคราะห์:

```csharp
//เส้นทางภาพ
string fullPath = dataDir + "sample.png";
```

## ขั้นตอนที่ 3: จดจำรูปภาพ

ดำเนินการกระบวนการจดจำรูปภาพ:

```csharp
// รับรู้ถึงภาพ
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    // การตั้งค่าเริ่มต้นหรือแบบกำหนดเอง
});
```

## ขั้นตอนที่ 4: รับตัวเลือกสำหรับตัวละครที่รู้จัก

รับตัวเลือกสำหรับอักขระที่รู้จัก:

```csharp
List<char[]> resultWithChoices = result.RecognitionCharactersList;
```

## ขั้นตอนที่ 5: พิมพ์ผลลัพธ์

แสดงข้อความการจดจำและตัวเลือก:

```csharp
// พิมพ์ผล
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Choices:");
resultWithChoices.ForEach(a => Console.WriteLine($"character: {a[0]} . Choices: {a[1]} {a[2]} {a[3]} {a[4]}"));

Console.WriteLine("GetChoiceForRecognizedCharacters executed successfully");
```

ทำซ้ำขั้นตอนเหล่านี้ โดยปรับแต่งตามความต้องการของแอปพลิเคชันของคุณ

## บทสรุป

ในบทช่วยสอนนี้ เราได้สำรวจวิธีการใช้ประโยชน์จาก Aspose.OCR สำหรับ .NET เพื่อรับตัวเลือกสำหรับอักขระที่รู้จักในการจดจำรูปภาพ คุณลักษณะนี้เพิ่มมิติใหม่ให้กับความสามารถ OCR ของคุณ เพิ่มความคล่องตัวให้กับแอปพลิเคชันของคุณ

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR สำหรับ .NET เหมาะสำหรับการประมวลผลเอกสารขนาดใหญ่หรือไม่

A1: แน่นอน! Aspose.OCR สำหรับ .NET ได้รับการออกแบบมาเพื่อจัดการเอกสารจำนวนมากอย่างมีประสิทธิภาพและแม่นยำ

### คำถามที่ 2: ฉันสามารถใช้ Aspose.OCR สำหรับ .NET ในเว็บแอปพลิเคชันได้หรือไม่

ตอบ 2: ได้ คุณสามารถรวม Aspose.OCR สำหรับ .NET เข้ากับเว็บแอปพลิเคชันได้ ทำให้ใช้งานได้หลากหลายสำหรับสถานการณ์การพัฒนาที่หลากหลาย

### คำถามที่ 3: มีตัวเลือกสิทธิ์การใช้งานสำหรับ Aspose.OCR สำหรับ .NET หรือไม่

 A3: ได้ คุณสามารถสำรวจตัวเลือกใบอนุญาตและทำการซื้อได้[ที่นี่](https://purchase.aspose.com/buy).

### คำถามที่ 4: ฉันจะรับการสนับสนุนหรือถามคำถามเกี่ยวกับ Aspose.OCR สำหรับ .NET ได้อย่างไร

 A4: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุน ถามคำถาม และเชื่อมต่อกับชุมชน

### คำถามที่ 5: Aspose.OCR สำหรับ .NET มีรุ่นทดลองใช้ฟรีหรือไม่

 A5: ได้ คุณสามารถทดลองใช้ฟรีได้[ที่นี่](https://releases.aspose.com/) เพื่อสัมผัสความสามารถของ Aspose.OCR สำหรับ .NET
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
