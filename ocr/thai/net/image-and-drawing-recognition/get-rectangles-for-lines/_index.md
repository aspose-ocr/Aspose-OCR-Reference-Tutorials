---
date: 2025-12-17
description: เรียนรู้วิธีการรับสี่เหลี่ยมของบรรทัด OCR ด้วย Aspose.OCR สำหรับ .NET
  เพื่อจดจำบรรทัดข้อความในภาพและดึงพิกัดบรรทัดได้อย่างง่ายดาย.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: รับสี่เหลี่ยมบรรทัด OCR สำหรับบรรทัดข้อความในภาพ
url: /th/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับสี่เหลี่ยมผืนผ้าบรรทัด OCR สำหรับบรรทัดข้อความในรูปภาพ

## Introduction

ในบทเรียนนี้คุณจะค้นพบ **วิธีการรับสี่เหลี่ยมผืนผ้าบรรทัด OCR** ด้วย Aspose.OCR for .NET. เมื่อจบคู่มือคุณจะสามารถ **จดจำบรรทัดข้อความในรูปภาพ** และ **ดึงพิกัดบรรทัด** สำหรับแต่ละบรรทัดที่ตรวจพบ — เหมาะสำหรับการประมวลผลต่อ เช่น การวิเคราะห์เค้าโครง การดึงข้อมูล หรือการเรนเดอร์แบบกำหนดเอง.

## Quick Answers
- **What does “get OCR line rectangles” mean?** มันคืนค่ากล่องขอบของแต่ละบรรทัดข้อความที่ตรวจพบในรูปภาพ.  
- **Which API method is used?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Do I need a license?** การทดลองใช้ฟรีทำงานสำหรับการพัฒนา; ต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **Supported image formats?** PNG, JPEG, BMP, TIFF และอื่น ๆ.  
- **Can I run this on .NET Core?** ได้, Aspose.OCR รองรับ .NET Core และ .NET 5/6 อย่างเต็มที่.

## Prerequisites

ก่อนที่จะดำดิ่งสู่บทเรียน โปรดตรวจสอบว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้พร้อมใช้งาน:

- ความรู้พื้นฐานเกี่ยวกับ C# และการพัฒนา .NET.  
- สภาพแวดล้อมการพัฒนาแบบบูรณาการ (IDE) เช่น Visual Studio.  
- ไลบรารี Aspose.OCR for .NET ติดตั้งแล้ว คุณสามารถดาวน์โหลดได้จาก [ที่นี่](https://releases.aspose.com/ocr/net/).  
- ภาพตัวอย่างที่มีข้อความสำหรับการจดจำ OCR.

## Import Namespaces

ตรวจสอบว่าคุณได้นำเข้า namespace ที่จำเป็นในโปรเจกต์ของคุณแล้ว เพิ่มบรรทัดต่อไปนี้ที่ส่วนบนของไฟล์ C# ของคุณ:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

ตอนนี้เรามาแยกกระบวนการรับสี่เหลี่ยมผืนผ้าสำหรับบรรทัดใน OCR ของรูปภาพเป็นขั้นตอนง่าย ๆ กัน.

## Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงของโฟลเดอร์ที่เก็บภาพตัวอย่างของคุณ.

## Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

สร้างอินสแตนซ์ของคลาส `AsposeOcr` เพื่อเข้าถึงฟังก์ชัน OCR.

## Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

กำหนดเส้นทางเต็มของภาพที่คุณต้องการทำ OCR.

## Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

เมธอด `GetRectangles` คืนค่ารายการของอ็อบเจ็กต์ `Rectangle` แต่ละอันแสดงพิกัดของบรรทัดข้อความที่ตรวจพบ นี่คือแกนหลักของ **การรับสี่เหลี่ยมผืนผ้าบรรทัด OCR**.

## Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

พิมพ์พิกัดของพื้นที่ที่ตรวจพบลงคอนโซล คุณจะเห็นค่าที่คุณสามารถใช้ต่อไปเพื่อ **ดึงพิกัดบรรทัด** สำหรับการประมวลผลแบบกำหนดเอง.

## Why Use Aspose.OCR for Line Rectangles?

- **ความแม่นยำสูง** – อัลกอริธึมขั้นสูงตรวจจับบรรทัดแม้ในภาพที่มีเสียงรบกวนหรือเอียง.  
- **ข้ามแพลตฟอร์ม** – ทำงานบน .NET Framework, .NET Core, และ .NET 5/6.  
- **ไม่มีการพึ่งพาภายนอก** – ไลบรารี .NET แท้ ไม่ต้องจัดส่ง DLL เนทีฟ.  
- **ผลลัพธ์ที่หลากหลาย** – นอกจากสี่เหลี่ยมผืนผ้าบรรทัดแล้ว คุณยังสามารถดึงคำ, ตัวอักษร, และคะแนนความมั่นใจได้.

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **No rectangles returned** | ตรวจสอบว่าภาพมีข้อความที่ชัดเจนและเป็นแนวนอนและได้ระบุ `AreasType.LINES` แล้ว. |
| **Incorrect coordinates** | ตรวจสอบ DPI ของภาพ; ภาพความละเอียดต่ำอาจทำให้ขอบเขตไม่แม่นยำ. |
| **Performance bottleneck on large images** | ปรับขนาดภาพให้มีความละเอียดที่เหมาะสมก่อนเรียก `GetRectangles`. |
| **License exception** | ใช้ลิขสิทธิ์ทดลองสำหรับการทดสอบ; ใช้ลิขสิทธิ์เต็มสำหรับการผลิตเพื่อหลีกเลี่ยงข้อจำกัดการประเมิน. |

## FAQ's

### Q1: ฉันสามารถใช้ Aspose.OCR for .NET กับภาพประเภทใดก็ได้หรือไม่?

A1: Aspose.OCR รองรับรูปแบบภาพที่หลากหลาย ทำให้คุณมีความยืดหยุ่นในแอปพลิเคชัน OCR ของคุณ.

### Q2: ความแม่นยำของการจดจำ OCR เป็นอย่างไร?

A2: Aspose.OCR ใช้อัลกอริธึมขั้นสูงเพื่อความแม่นยำสูง เหมาะกับสถานการณ์การจดจำข้อความต่าง ๆ.

### Q3: มีเวอร์ชันทดลองใช้งานหรือไม่?

A3: มี, คุณสามารถสำรวจความสามารถของ Aspose.OCR for .NET ด้วย [การทดลองใช้ฟรี](https://releases.aspose.com/).

### Q4: จะหาเอกสารประกอบที่ครบถ้วนได้จากที่ไหน?

A4: ดูที่ [เอกสารประกอบ](https://reference.aspose.com/ocr/net/) เพื่อข้อมูลรายละเอียดและแนวทางการใช้งาน.

### Q5: ต้องการความช่วยเหลือหรือมีคำถามเฉพาะ?

A5: เยี่ยมชม [ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุนจากชุมชนและการสนทนา.

## Frequently Asked Questions

**Q: ฉันสามารถดึงคำแต่ละคำแทนบรรทัดทั้งหมดได้หรือไม่?**  
A: ใช่, ใช้ `AreasType.WORDS` กับเมธอด `GetRectangles` เดียวกันเพื่อรับกล่องขอบระดับคำ.

**Q: API รองรับ PDF หลายหน้าได้หรือไม่?**  
A: แปลงแต่ละหน้า PDF เป็นภาพก่อน, แล้วเรียก `GetRectangles` กับแต่ละภาพ.

**Q: จะจัดการกับข้อความที่หมุนเอียงอย่างไร?**  
A: เปิดใช้งานตัวเลือก auto‑rotate ในการตั้งค่า OCR หรือหมุนภาพล่วงหน้าก่อนประมวลผล.

**Q: มีวิธีรับคะแนนความมั่นใจสำหรับแต่ละบรรทัดหรือไม่?**  
A: หลังจากได้สี่เหลี่ยมผืนผ้าแล้ว, เรียก `api.RecognizeImage(...).Lines` เพื่อเข้าถึงอ็อบเจ็กต์บรรทัดที่รวมคะแนนความมั่นใจ.

**Q: เวอร์ชัน .NET ใดบ้างที่รองรับ?**  
A: ไลบรารีทำงานกับ .NET Framework 4.5+, .NET Core 3.1+, และ .NET 5/6.

## Conclusion

Congratulations! You've successfully **got OCR line rectangles** for an image using Aspose.OCR for .NET. With the bounding boxes in hand, you can now feed line coordinates into downstream workflows such as custom rendering, data extraction, or layout analysis.

---

**Last Updated:** 2025-12-17  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}