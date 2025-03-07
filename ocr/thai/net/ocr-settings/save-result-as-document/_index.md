---
title: บันทึกผลลัพธ์เป็นเอกสารในการจดจำรูปภาพ OCR
linktitle: บันทึกผลลัพธ์เป็นเอกสารในการจดจำรูปภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดล็อกศักยภาพของ Aspose.OCR สำหรับ .NET จดจำข้อความในรูปภาพได้อย่างง่ายดายและบันทึกผลลัพธ์ในรูปแบบเอกสารต่างๆ
weight: 10
url: /th/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บันทึกผลลัพธ์เป็นเอกสารในการจดจำรูปภาพ OCR

## การแนะนำ

ยินดีต้อนรับสู่โลกที่น่าตื่นเต้นของการรู้จำอักขระด้วยแสง (OCR) ด้วย Aspose.OCR สำหรับ .NET! ในบทช่วยสอนที่ครอบคลุมนี้ เราจะเจาะลึกความซับซ้อนของการใช้ Aspose.OCR เพื่อจดจำข้อความในรูปภาพ และสาธิตวิธีบันทึกผลลัพธ์เป็นรูปแบบเอกสารต่างๆ

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่มต้นการเดินทาง OCR นี้ ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

-  Aspose.OCR สำหรับ .NET ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.OCR แล้ว คุณสามารถดาวน์โหลดได้[ที่นี่](https://releases.aspose.com/ocr/net/).

-  Document Directory: มีไดเร็กทอรีที่กำหนดสำหรับเอกสารของคุณและอัปเดต`dataDir` ตัวแปรในโค้ดที่ให้มาตามลำดับ

## นำเข้าเนมสเปซ

เริ่มต้นด้วยการนำเข้าเนมสเปซที่จำเป็น สิ่งเหล่านี้คือองค์ประกอบหลักที่จะเสริมศักยภาพโค้ดของคุณด้วยความสามารถ OCR

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

ตอนนี้ เรามาแบ่งตัวอย่างออกเป็นหลายขั้นตอน:

## ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";

// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

ขั้นตอนนี้กำหนดขั้นตอนโดยการเริ่มต้น Aspose.OCR API

## ขั้นตอนที่ 2: จดจำรูปภาพ

```csharp
// รับรู้ถึงภาพ
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

ที่นี่ เราใช้ Aspose.OCR เพื่อจดจำข้อความภายในรูปภาพที่ระบุ (แทนที่ "sample.png" ด้วยไฟล์รูปภาพของคุณ)

## ขั้นตอนที่ 3: บันทึกผลลัพธ์ในรูปแบบที่แตกต่างกัน

```csharp
// บันทึกผลลัพธ์ในรูปแบบที่คุณต้องการ
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

ปรับแต่งขั้นตอนนี้ตามความต้องการของคุณ Aspose.OCR ช่วยให้คุณสามารถบันทึกข้อความที่รู้จักในรูปแบบเอกสารต่างๆ เช่น DOCX, TXT, PDF และ XLSX

## ขั้นตอนที่ 4: แสดงข้อความแสดงความสำเร็จ

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

ข้อความยืนยันง่ายๆ เพื่อแจ้งให้คุณทราบว่ากระบวนการนี้เสร็จสมบูรณ์โดยไม่มีปัญหาใดๆ

ด้วยการทำตามขั้นตอนเหล่านี้ คุณได้ประสบความสำเร็จในการควบคุมพลังของ Aspose.OCR สำหรับ .NET ในการจดจำข้อความภายในรูปภาพและบันทึกผลลัพธ์ในรูปแบบเอกสารที่แตกต่างกัน

## บทสรุป

โดยสรุป Aspose.OCR สำหรับ .NET เปิดโลกแห่งความเป็นไปได้สำหรับการจดจำข้อความในรูปภาพ ไม่ว่าคุณจะดึงข้อมูลหรือสร้างเอกสารที่ค้นหาได้ Aspose.OCR จะทำให้กระบวนการง่ายขึ้นด้วย API ที่ใช้งานง่าย

## คำถามที่พบบ่อย

### ไตรมาสที่ 1 Aspose.OCR เข้ากันได้กับรูปแบบภาพที่แตกต่างกันหรือไม่

ตอบ 1: ใช่ Aspose.OCR รองรับรูปแบบภาพที่หลากหลาย ทำให้มั่นใจได้ถึงความยืดหยุ่นในงาน OCR ของคุณ

### คำถามที่ 2: ฉันสามารถปรับแต่งการตั้งค่าการจดจำให้แม่นยำยิ่งขึ้นได้หรือไม่

A2: แน่นอน! Aspose.OCR ให้การตั้งค่าการจดจำเพื่อปรับแต่งกระบวนการ OCR ตามความต้องการเฉพาะของคุณ

### คำถามที่ 3: มีการทดลองใช้ฟรีหรือไม่?

 A3: ได้ คุณสามารถเริ่มต้นด้วยการทดลองใช้ฟรีได้[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 4: ฉันจะรับใบอนุญาตชั่วคราวสำหรับ Aspose.OCR ได้อย่างไร

 A4: สามารถรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).

### คำถามที่ 5: ฉันจะขอความช่วยเหลือหรือติดต่อกับชุมชนได้ที่ไหน?

 A5: เข้าร่วมชุมชน Aspose.OCR ได้ที่[ตั้งฟอรั่ม](https://forum.aspose.com/c/ocr/16) สำหรับการสนับสนุนและการอภิปราย
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
