---
title: ดำเนินการ OCR กับรูปภาพจาก URL ใน OCR Image Recognition
linktitle: ดำเนินการ OCR กับรูปภาพจาก URL ใน OCR Image Recognition
second_title: Aspose.OCR .NET API
description: สำรวจการบูรณาการ OCR อย่างราบรื่นกับ Aspose.OCR สำหรับ .NET จดจำข้อความจากรูปภาพได้อย่างแม่นยำ
weight: 10
url: /th/net/ocr-optimization/perform-ocr-on-image-from-url/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดำเนินการ OCR กับรูปภาพจาก URL ใน OCR Image Recognition

## การแนะนำ

ในขอบเขตของการรู้จำอักขระด้วยแสง (OCR) Aspose.OCR สำหรับ .NET มีความโดดเด่นในฐานะเครื่องมืออันทรงพลังที่ช่วยให้นักพัฒนาสามารถแยกเนื้อหาข้อความจากรูปภาพได้อย่างแม่นยำ หากคุณต้องการรวมความสามารถ OCR เข้ากับแอปพลิเคชัน .NET ของคุณและดำเนินการจดจำข้อความได้อย่างง่ายดาย คำแนะนำทีละขั้นตอนนี้จะแนะนำคุณตลอดกระบวนการดำเนินการ OCR บนรูปภาพจาก URL

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกบทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

-  Aspose.OCR สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณมีไลบรารี Aspose.OCR ที่รวมอยู่ในโปรเจ็กต์ .NET ของคุณ คุณสามารถดาวน์โหลดได้จาก[หน้าปล่อย](https://releases.aspose.com/ocr/net/).

- สภาพแวดล้อมการพัฒนา: ตั้งค่าสภาพแวดล้อมการพัฒนา .NET ที่ใช้งานได้บนเครื่องของคุณ

## นำเข้าเนมสเปซ

ในโปรเจ็กต์ .NET ของคุณ ให้รวมเนมสเปซที่จำเป็นเพื่อเข้าถึงฟังก์ชัน Aspose.OCR เพิ่มข้อมูลโค้ดต่อไปนี้ในโครงการของคุณ:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

 เริ่มต้นด้วยการระบุไดเร็กทอรีที่เก็บเอกสารของคุณ แทนที่`"Your Document Directory"` พร้อมเส้นทางสู่เอกสารของคุณจริง

```csharp
string dataDir = "Your Document Directory";
```

## ขั้นตอนที่ 2: รับภาพเพื่อการจดจำ

ระบุ URL ของภาพที่คุณต้องการใช้ OCR ตรวจสอบให้แน่ใจว่ารูปภาพสามารถเข้าถึงได้แบบสาธารณะ

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

## ขั้นตอนที่ 3: เริ่มต้น AsposeOcr

สร้างอินสแตนซ์ของคลาส AsposeOcr เพื่อเข้าถึงฟังก์ชัน OCR

```csharp
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 4: จดจำรูปภาพ

ใช้ไลบรารี Aspose.OCR เพื่อจดจำข้อความจาก URL รูปภาพที่ระบุ ปรับการตั้งค่าการจดจำตามความต้องการของคุณ

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## ขั้นตอนที่ 5: พิมพ์ผลลัพธ์

แสดงผลการจดจำ รวมถึงข้อความที่รู้จัก พื้นที่ และคำเตือนใดๆ

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## ขั้นตอนที่ 6: ดำเนินการและตรวจสอบ

เรียกใช้แอปพลิเคชันของคุณ และหากทุกอย่างได้รับการตั้งค่าอย่างถูกต้อง คุณจะเห็นกระบวนการ OCR ที่ดำเนินการได้สำเร็จ

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## บทสรุป

ด้วย Aspose.OCR สำหรับ .NET การรวมความสามารถ OCR เข้ากับแอปพลิเคชัน .NET ของคุณจะกลายเป็นประสบการณ์ที่ราบรื่น บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการดำเนินการ OCR บนรูปภาพจาก URL เพื่อเป็นพื้นฐานในการใช้ประโยชน์จากพลังของการรู้จำข้อความในโปรเจ็กต์ของคุณ

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR เหมาะสำหรับการจัดการหลายภาษาหรือไม่

ตอบ 1: ใช่ Aspose.OCR รองรับการจดจำข้อความในภาษาต่างๆ ทำให้มีความหลากหลายสำหรับการใช้งานในระดับสากล

### คำถามที่ 2: ฉันสามารถใช้ Aspose.OCR สำหรับการจดจำข้อความทั้งบรรทัดเดียวและหลายบรรทัดได้หรือไม่

A2: แน่นอน! Aspose.OCR ให้ความยืดหยุ่นในการจดจำทั้งข้อความบรรทัดเดียวและหลายบรรทัด โดยปรับให้เข้ากับกรณีการใช้งานเฉพาะของคุณ

### คำถามที่ 3: มีตัวเลือกสิทธิ์การใช้งานสำหรับ Aspose.OCR หรือไม่

 A3: ได้ คุณสามารถสำรวจตัวเลือกใบอนุญาตและทำการซื้อได้ที่[แอสโพสสโตร์](https://purchase.aspose.com/buy).

### คำถามที่ 4: Aspose.OCR มีรุ่นทดลองใช้ฟรีหรือไม่

 A4: ได้ คุณสามารถทดลองใช้ Aspose.OCR ได้ฟรีโดยไปที่[หน้าเผยแพร่](https://releases.aspose.com/).

### คำถามที่ 5: ฉันจะรับการสนับสนุนหรือการสนทนาในชุมชนที่เกี่ยวข้องกับ Aspose.OCR ได้ที่ไหน

 A5: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) เพื่อการสนับสนุนและการมีส่วนร่วมกับชุมชน
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
