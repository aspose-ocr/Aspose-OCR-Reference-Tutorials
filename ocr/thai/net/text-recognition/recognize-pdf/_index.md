---
title: รับรู้ PDF ในการรับรู้ภาพ OCR
linktitle: รับรู้ PDF ในการรับรู้ภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดล็อกศักยภาพของ OCR ใน .NET ด้วย Aspose.OCR แยกข้อความจาก PDF ได้อย่างง่ายดาย ดาวน์โหลดทันทีเพื่อประสบการณ์การบูรณาการที่ราบรื่น
weight: 14
url: /th/net/text-recognition/recognize-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับรู้ PDF ในการรับรู้ภาพ OCR

## การแนะนำ

ยินดีต้อนรับสู่โลกแห่งการรู้จำอักขระด้วยแสง (OCR) ด้วย Aspose.OCR สำหรับ .NET! หากคุณกระตือรือร้นที่จะควบคุมความสามารถของ OCR ในแอปพลิเคชัน .NET ของคุณ แสดงว่าคุณมาถูกที่แล้ว ในคำแนะนำทีละขั้นตอนนี้ เราจะสำรวจวิธีจดจำข้อความใน PDF โดยใช้ไลบรารี Aspose.OCR ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้น บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการ เพื่อให้มั่นใจว่าคุณสามารถรวมฟังก์ชัน OCR เข้ากับโปรเจ็กต์ของคุณได้อย่างง่ายดาย

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกบทช่วยสอน เรามาตรวจสอบให้แน่ใจว่าคุณมีทุกสิ่งที่คุณต้องการ:

-  Aspose.OCR สำหรับ .NET: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งไลบรารี Aspose.OCR แล้ว ถ้าไม่เช่นนั้นคุณสามารถดาวน์โหลดได้จาก[Aspose.OCR สำหรับเอกสาร .NET](https://reference.aspose.com/ocr/net/).

- เอกสาร: เตรียมเอกสาร PDF ที่คุณต้องการดำเนินการ OCR ตรวจสอบให้แน่ใจว่าคุณมีเส้นทางไฟล์ที่ถูกต้อง

เมื่อคุณมีเครื่องมือที่จำเป็นครบแล้ว มาดูบทช่วยสอนกันดีกว่า

## นำเข้าเนมสเปซ

ในแอปพลิเคชัน .NET ของคุณ ให้นำเข้าเนมสเปซ Aspose.OCR เพื่อเข้าถึงฟังก์ชัน OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";

// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

ที่นี่ เรากำหนดเส้นทางไปยังไดเร็กทอรีเอกสารและสร้างอินสแตนซ์ของคลาส AsposeOcr

## ขั้นตอนที่ 2: ระบุเส้นทางรูปภาพ

```csharp
//เส้นทางภาพ
string fullPath = dataDir + "multi_page_1.pdf";
```

ระบุเส้นทางไปยังเอกสาร PDF ที่คุณต้องการดำเนินการ

## ขั้นตอนที่ 3: จดจำ PDF

```csharp
// รับรู้ถึงภาพ
List<RecognitionResult> results = api.RecognizePdf(fullPath, new DocumentRecognitionSettings { StartPage = 2, PagesNumber = 2 });
```

ใช้ไลบรารี Aspose.OCR เพื่อจดจำข้อความในเอกสาร PDF คุณสามารถกำหนดการตั้งค่าการจดจำได้เอง เช่น หน้าเริ่มต้นและจำนวนหน้าที่ต้องดำเนินการ

## ขั้นตอนที่ 4: พิมพ์ผลลัพธ์

```csharp
// พิมพ์ผล
int pageCounter = 0;
foreach (var result in results)
{
    PrintRecognitionResult(result, pageCounter++);
}
```

วนซ้ำผลการจดจำและพิมพ์ข้อความที่แยกออกมาสำหรับแต่ละหน้า

## บทสรุป

ยินดีด้วย! คุณได้รวม Aspose.OCR สำหรับ .NET เพื่อจดจำข้อความในเอกสาร PDF สำเร็จแล้ว ไลบรารีอันทรงพลังนี้เปิดโลกแห่งความเป็นไปได้ในการแยกข้อความอัตโนมัติในแอปพลิเคชันของคุณ

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR สำหรับ .NET เหมาะสำหรับการประมวลผลรูปแบบภาพต่างๆ หรือไม่

ตอบ 1: ใช่ Aspose.OCR รองรับรูปแบบรูปภาพที่หลากหลาย รวมถึง PDF, PNG, JPEG และอื่นๆ

### คำถามที่ 2: ฉันสามารถใช้ Aspose.OCR สำหรับ .NET ทั้งในแอปพลิเคชันบนเว็บและเดสก์ท็อปได้หรือไม่

A2: แน่นอน! Aspose.OCR ผสานรวมเข้ากับแอปพลิเคชันบนเว็บและเดสก์ท็อปที่พัฒนาโดยใช้ .NET ได้อย่างราบรื่น

### คำถามที่ 3: มี Aspose.OCR สำหรับ .NET รุ่นทดลองใช้งานหรือไม่

 A3: ใช่ คุณสามารถสำรวจคุณสมบัติต่างๆ ได้ด้วย[ทดลองฟรี](https://releases.aspose.com/).

### คำถามที่ 4: ฉันจะได้รับการสนับสนุนสำหรับ Aspose.OCR สำหรับ .NET ได้อย่างไร

 A4: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) เพื่อรับความช่วยเหลือและเชื่อมต่อกับชุมชน

### คำถามที่ 5: ฉันจะซื้อ Aspose.OCR สำหรับ .NET ได้ที่ไหน

 A5: คุณสามารถซื้อผลิตภัณฑ์ได้จาก[หน้าซื้อ](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
