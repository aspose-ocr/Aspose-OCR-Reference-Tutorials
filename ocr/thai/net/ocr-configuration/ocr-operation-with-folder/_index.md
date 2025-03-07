---
title: OCROperation กับโฟลเดอร์ในการจดจำภาพ OCR
linktitle: OCROperation กับโฟลเดอร์ในการจดจำภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดล็อกพลังของการจดจำรูปภาพ OCR ใน .NET ด้วย Aspose.OCR แยกข้อความออกจากรูปภาพได้อย่างง่ายดาย
weight: 11
url: /th/net/ocr-configuration/ocr-operation-with-folder/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCROperation กับโฟลเดอร์ในการจดจำภาพ OCR

## การแนะนำ

ยินดีต้อนรับสู่โลกแห่งการรู้จำอักขระด้วยแสง (OCR) โดยใช้ Aspose.OCR สำหรับ .NET! หากคุณต้องการแยกข้อความจากรูปภาพภายในแอปพลิเคชัน .NET ของคุณได้อย่างราบรื่น แสดงว่าคุณมาถูกที่แล้ว บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการจดจำรูปภาพ OCR ด้วยโฟลเดอร์ โดยใช้ประโยชน์จากความสามารถอันทรงพลังของ Aspose.OCR

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเข้าสู่บทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- ความรู้ด้านการทำงานของการพัฒนา C# และ .NET
- ติดตั้ง Visual Studio บนเครื่องของคุณแล้ว
-  Aspose.OCR สำหรับไลบรารี .NET ซึ่งคุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.aspose.com/ocr/net/).
- ความเข้าใจพื้นฐานเกี่ยวกับแนวคิด OCR

## นำเข้าเนมสเปซ

ในโค้ด C# ของคุณ ตรวจสอบให้แน่ใจว่าได้นำเข้าเนมสเปซที่จำเป็นสำหรับการใช้ Aspose.OCR รวมสิ่งต่อไปนี้ไว้ที่ตอนต้นของสคริปต์ของคุณ:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสาร

```csharp
// เอ็กซ์สตาร์ท:1
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
```

ตรวจสอบให้แน่ใจว่าคุณแทนที่ "Your Document Directory" ด้วยเส้นทางจริงที่ใช้จัดเก็บรูปภาพของคุณ

## ขั้นตอนที่ 2: เริ่มต้น Aspose.OCR

```csharp
// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

สร้างอินสแตนซ์ของคลาส AsposeOcr เพื่อใช้ฟังก์ชันต่างๆ

## ขั้นตอนที่ 3: ระบุเส้นทางรูปภาพ

```csharp
//เส้นทางภาพ
string fullPath = dataDir + "OCR";
```

เชื่อมต่อเส้นทางไดเร็กทอรีเอกสารกับโฟลเดอร์เฉพาะที่มีรูปภาพของคุณ

## ขั้นตอนที่ 4: จดจำรูปภาพ

```csharp
// รับรู้ถึงภาพ
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
    //ค่าเริ่มต้นหรือกำหนดเอง
});
```

ใช้วิธีการ RecognizeMultipleImages เพื่อทำ OCR กับภาพหลายภาพภายในโฟลเดอร์ที่ระบุ

## ขั้นตอนที่ 5: พิมพ์ผลลัพธ์

```csharp
// พิมพ์ผล
for (int i = 0; i < result.Length; i++)
{
    Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
```

วนซ้ำผลลัพธ์และพิมพ์ข้อความที่รู้จักสำหรับแต่ละภาพ

## ขั้นตอนที่ 6: บทสรุป

```csharp
// สิ้นสุด:1
Console.WriteLine("OCROperationWithFolder executed successfully");
```

ตรวจสอบให้แน่ใจว่าถึงบทสรุปของสคริปต์ของคุณเพื่อบ่งชี้ถึงการดำเนินการ OCR ด้วยโฟลเดอร์ที่ประสบความสำเร็จ

## บทสรุป

ยินดีด้วย! คุณได้เรียนรู้วิธีการนำการจดจำรูปภาพ OCR ไปใช้กับโฟลเดอร์ที่ใช้ Aspose.OCR สำหรับ .NET เรียบร้อยแล้ว เครื่องมืออันทรงพลังนี้เปิดความเป็นไปได้มากมายในการแยกข้อความจากรูปภาพในแอปพลิเคชัน .NET ของคุณ

## คำถามที่พบบ่อย

### คำถามที่ 1: ฉันสามารถใช้ Aspose.OCR สำหรับ .NET ในโครงการเชิงพาณิชย์ได้หรือไม่

 A1: ใช่ Aspose.OCR สำหรับ .NET เป็นผลิตภัณฑ์เชิงพาณิชย์ สำหรับข้อมูลใบอนุญาต โปรดไปที่[ที่นี่](https://purchase.aspose.com/buy).

### คำถามที่ 2:. มีการทดลองใช้ฟรีหรือไม่?

 A2: ได้ คุณสามารถทดลองใช้งานฟรีได้[ที่นี่](https://releases.aspose.com/).

### Q3: ฉันจะหาเอกสารได้จากที่ไหน?

 A3: มีเอกสารประกอบให้[ที่นี่](https://reference.aspose.com/ocr/net/).

### คำถามที่ 4: ฉันจะรับสิทธิ์ใช้งานชั่วคราวได้อย่างไร

 A4: สามารถรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### Q5: ต้องการความช่วยเหลือหรือมีคำถาม?

 A5: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) เพื่อสนับสนุนชุมชน
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
