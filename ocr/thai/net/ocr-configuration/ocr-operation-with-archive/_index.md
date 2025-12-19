---
date: 2025-12-19
description: เรียนรู้วิธีทำ OCR บนภาพในไฟล์เก็บข้อมูล, แปลงภาพเป็นข้อความและดึงข้อความจากไฟล์เก็บข้อมูลโดยใช้
  Aspose.OCR สำหรับ .NET.
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: วิธีทำ OCR บนภาพเก็บถาวรด้วย Aspose.OCR สำหรับ .NET
url: /th/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนรูปภาพในไฟล์เก็บข้อมูลด้วย Aspose.OCR สำหรับ .NET

## Introduction

ในบทเรียนเชิงลึกนี้คุณจะได้ค้นพบ **วิธีทำ OCR** บนไฟล์รูปภาพที่ถูกเก็บไว้ในรูปแบบ archive ด้วยไลบรารี Aspose.OCR สำหรับ .NET ไม่ว่าคุณจะต้องการ **แปลงรูปภาพเป็นข้อความ** หรือ **ดึงข้อความจากไฟล์ archive** คู่มือขั้นตอนต่อไปนี้จะพาคุณผ่านทุกขั้นตอน ตั้งแต่การตั้งค่าสภาพแวดล้อมการพัฒนา ไปจนถึงการดึงข้อความที่จดจำได้จากแต่ละรูปภาพภายในไฟล์ ZIP

## Quick Answers
- **What does the tutorial cover?** Performing OCR on archive (ZIP) images with Aspose.OCR for .NET.  
- **Which primary keyword is targeted?** *how to perform ocr*.  
- **Do I need a license?** A free trial works for evaluation; a commercial license is required for production.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Can I customize recognition settings?** Yes—use `RecognitionSettings` to tune accuracy.

## What is OCR and Why Use It on Archives?

Optical Character Recognition (OCR) แปลงภาพสแกนหรือ PDF ให้เป็นข้อความที่สามารถค้นหาและแก้ไขได้ เมื่อรูปภาพถูกบรรจุอยู่ใน archive (เช่นไฟล์ ZIP) การดึงและจดจำแต่ละรูปภาพพร้อมกันช่วยประหยัดเวลาและลดความซับซ้อนของโค้ด Aspose.OCR มีเมธอด `RecognizeMultipleImages` ที่ทำให้กระบวนการนี้เป็นเรื่องง่าย

## Prerequisites

- Visual Studio 2019 หรือใหม่กว่า (หรือ IDE ที่รองรับ .NET ใดก็ได้)  
- .NET Framework 4.5 + หรือ .NET Core 3.1 + ที่ติดตั้งแล้ว  
- เข้าถึงไลบรารี Aspose.OCR สำหรับ .NET (ลิงก์ดาวน์โหลดด้านล่าง)  
- ไลเซนส์ Aspose.OCR ที่ถูกต้องสำหรับการใช้งานในผลิตภัณฑ์ (มีเวอร์ชันทดลอง)

## Import Namespaces

ในโปรเจกต์ .NET ของคุณ ให้แน่ใจว่าได้นำเข้า namespace ที่จำเป็นเพื่อเข้าถึงฟังก์ชันของ Aspose.OCR:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Download and Install Aspose.OCR for .NET

ดาวน์โหลดแพคเกจล่าสุดจากหน้า release **[ที่นี่](https://releases.aspose.com/ocr/net/)** แล้วทำตามขั้นตอนการติดตั้งผ่าน NuGet หรือการติดตั้งแบบแมนนวลตามปกติ

## Acquire a License

รับไลเซนส์จาก **[หน้าซื้อขาย](https://purchase.aspose.com/buy)** หรือทดลองใช้ **[เวอร์ชันฟรี](https://releases.aspose.com/)** วางไฟล์ไลเซนส์ไว้ที่โฟลเดอร์รากของโปรเจกต์และโหลดมันใน runtime ตามที่เอกสารของ Aspose แนะนำ

## Step 1: Set up Your Document Directory

เริ่มต้นโดยกำหนดพาธไปยังโฟลเดอร์เอกสารของคุณ:

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **Pro tip:** ใช้ `Path.Combine` เพื่อจัดการพาธแบบข้ามแพลตฟอร์ม

## Step 2: Initialize Aspose.OCR

สร้างอินสแตนซ์ของคลาส Aspose.OCR เพื่อเริ่มต้นการทำ OCR:

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## Step 3: Specify Image Path

กำหนดพาธเต็มไปยังไฟล์ archive (ไฟล์ ZIP ที่บรรจุรูปภาพที่ต้องการอ่าน):

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## Step 4: Recognize Image

เรียกใช้การจดจำ OCR บน archive ที่ระบุโดยใช้การตั้งค่าเริ่มต้นหรือการตั้งค่าที่กำหนดเอง คำสั่งนี้จะดึงรูปภาพแต่ละไฟล์จาก ZIP และทำ OCR ให้โดยอัตโนมัติ:

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> คุณสามารถปรับ `RecognitionSettings` เพื่อเพิ่มความแม่นยำสำหรับภาษาหรือคุณภาพของภาพที่เฉพาะเจาะจงได้

## Step 5: Print Results

วนลูปผลลัพธ์และพิมพ์ข้อความที่จดจำได้สำหรับแต่ละรูปภาพภายใน archive:

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

ผลลัพธ์จะแสดงดัชนีของรูปภาพแต่ละภาพตามด้วยสตริงที่ดึงออกมา ทำให้ **แปลงรูปภาพเป็นข้อความ** และ **ดึงข้อความจากไฟล์ archive** ได้อย่างมีประสิทธิภาพ

## Common Issues & Troubleshooting

| Issue | Cause | Solution |
|-------|-------|----------|
| ไม่ได้ข้อความใดเลย | คุณภาพภาพต่ำเกินไป | ทำการประมวลผลล่วงหน้าต่อภาพ (เช่น การทำไบนารี) หรือปรับ `RecognitionSettings.Dpi` |
| เกิดข้อยกเว้นขณะอ่าน ZIP | พาธ archive ไม่ถูกต้อง | ตรวจสอบว่า `fullPath` ชี้ไปยังไฟล์ `.zip` ที่ถูกต้องและแอปมีสิทธิ์อ่าน |
| ไลเซนส์ไม่ถูกนำไปใช้ | ไฟล์ไลเซนส์หายหรือไม่ได้โหลด | เรียก `License license = new License(); license.SetLicense("Aspose.OCR.lic");` ก่อนสร้างอินสแตนซ์ `AsposeOcr` |

## Frequently Asked Questions

**Q: สามารถใช้ Aspose.OCR สำหรับ .NET ได้โดยไม่ต้องมีไลเซนส์หรือไม่?**  
A: ใช่ มีเวอร์ชันทดลองฟรีสำหรับการประเมินค่า แต่ต้องใช้ไลเซนส์ที่ได้รับอนุญาตสำหรับการใช้งานในผลิตภัณฑ์

**Q: ไลบรารีรองรับไฟล์ ZIP ที่มีการป้องกันด้วยรหัสผ่านหรือไม่?**  
A: ปัจจุบัน `RecognizeMultipleImages` ทำงานกับไฟล์ ZIP มาตรฐานเท่านั้น สำหรับ archive ที่เข้ารหัส ให้ดึงรูปภาพออกมาก่อนด้วยไลบรารีของบุคคลที่สาม แล้วจึงส่งอาร์เรย์รูปภาพให้กับเครื่องมือ OCR

**Q: จะเพิ่มความแม่นยำสำหรับข้อความลายมือได้อย่างไร?**  
A: เปิดใช้งานฟลัก `RecognitionSettings.EnableHandwritingRecognition` และตั้งค่า DPI ที่สูงขึ้น (เช่น 300)

**Q: มีวิธีรับคะแนนความเชื่อมั่นสำหรับแต่ละบรรทัดที่จดจำได้หรือไม่?**  
A: แต่ละ `RecognitionResult` มีคุณสมบัติ `Confidence` ที่คุณสามารถบันทึกหรือใช้กรองผลลัพธ์ที่ความเชื่อมั่นต่ำได้

## Conclusion

คุณมีเวิร์กโฟลว์ที่ครบถ้วนและพร้อมใช้งานในระดับผลิตภัณฑ์เพื่อ **ทำ OCR บนรูปภาพใน archive**, **แปลงรูปภาพเป็นข้อความ**, และ **ดึงข้อความจากไฟล์ archive** ด้วย Aspose.OCR สำหรับ .NET นำกระบวนการนี้ไปผสานในแอปของคุณเพื่อสร้างคลังเอกสารที่ค้นหาได้อัตโนมัติ, การป้อนข้อมูลอัตโนมัติ, หรือสถานการณ์ใด ๆ ที่ต้องการการสกัดข้อความจากรูปภาพจำนวนมาก

## Additional Resources

- **Aspose.OCR Forum:** สำหรับการสนับสนุนจากชุมชนและกรณีการใช้งานขั้นสูง ให้เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)  
- **Temporary License:** หากต้องการประเมินผลระยะสั้น สามารถขอ [temporary license](https://purchase.aspose.com/temporary-license/) ได้  
- **Official Documentation:** ติดตามการเปลี่ยนแปลง API ล่าสุดโดยตรวจสอบ [documentation](https://reference.aspose.com/ocr/net/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Last Updated:** 2025-12-19  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose