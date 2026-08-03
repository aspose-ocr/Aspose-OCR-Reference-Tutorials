---
date: 2026-02-22
description: เรียนรู้วิธีทำการวิเคราะห์เค้าโครง OCR ด้วยการจดจำบรรทัดข้อความในภาพและสกัดสี่เหลี่ยมผืนผ้าของบรรทัดโดยใช้
  Aspose.OCR สำหรับ .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: การวิเคราะห์เลย์เอาต์ OCR – ดึงสี่เหลี่ยมของบรรทัดจากภาพ
url: /th/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Layout Analysis OCR – Get Line Rectangles from Images

## Introduction

ในบทแนะนำนี้คุณจะได้เรียนรู้ **วิธีการดึงสี่เหลี่ยมของบรรทัด OCR** ด้วย Aspose.OCR สำหรับ .NET. เมื่อจบคู่มือแล้วคุณจะสามารถ **จำแนกบรรทัดข้อความในภาพ** และ **ดึงพิกัดของบรรทัด** สำหรับแต่ละบรรทัดที่ตรวจพบ—เหมาะสำหรับการประมวลผลต่อเนื่องเช่น **layout analysis OCR**, การสกัดข้อมูล, หรือการเรนเดอร์แบบกำหนดเอง

## Quick Answers
- **“get OCR line rectangles” หมายถึงอะไร?** จะคืนค่า bounding box ของแต่ละบรรทัดข้อความที่ตรวจพบในภาพ  
- **ใช้เมธอด API ใด?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`  
- **ต้องมีไลเซนส์หรือไม่?** เวอร์ชันทดลองฟรีใช้ได้สำหรับการพัฒนา; ต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **รูปแบบภาพที่รองรับ?** PNG, JPEG, BMP, TIFF และอื่น ๆ  
- **สามารถรันบน .NET Core ได้หรือไม่?** ได้, Aspose.OCR รองรับ .NET Core และ .NET 5/6 อย่างเต็มที่

## Prerequisites

ก่อนจะเริ่มทำตามบทแนะนำนี้ โปรดตรวจสอบว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้แล้ว:

- ความรู้พื้นฐานเกี่ยวกับ C# และการพัฒนา .NET  
- สภาพแวดล้อมการพัฒนา (IDE) เช่น Visual Studio  
- ไลบรารี Aspose.OCR สำหรับ .NET ที่ได้ทำการติดตั้งแล้ว คุณสามารถดาวน์โหลดได้จาก [ที่นี่](https://releases.aspose.com/ocr/net/)  
- ตัวอย่างภาพที่มีข้อความสำหรับการจดจำ OCR

## Import Namespaces

ตรวจสอบให้แน่ใจว่าคุณได้ import namespace ที่จำเป็นลงในโปรเจกต์ของคุณแล้ว เพิ่มบรรทัดต่อไปนี้ไปที่ส่วนหัวของไฟล์ C# ของคุณ:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

ตอนนี้เราจะอธิบายขั้นตอนการดึงสี่เหลี่ยมของบรรทัดในภาพ OCR อย่างเป็นระบบและง่ายต่อการทำตาม

## layout analysis ocr – Step‑by‑Step Guide

### Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

แทนที่ `"Your Document Directory"` ด้วยพาธจริงของโฟลเดอร์ที่เก็บภาพตัวอย่างของคุณ

### Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

สร้างอินสแตนซ์ของคลาส `AsposeOcr` เพื่อเข้าถึงฟังก์ชัน OCR

### Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

กำหนดพาธเต็มของภาพที่คุณต้องการทำ OCR

### Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

เมธอด `GetRectangles` จะคืนค่าเป็นรายการของอ็อบเจ็กต์ `Rectangle` ซึ่งแต่ละอ็อบเจ็กต์แสดงพิกัดของบรรทัดข้อความที่ตรวจพบ นี่คือหัวใจของ **การดึงสี่เหลี่ยมของบรรทัด OCR** และทำให้ **layout analysis OCR** ทำงานได้

### Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

พิมพ์พิกัดของพื้นที่ที่ตรวจพบลงคอนโซล คุณจะเห็นค่าต่าง ๆ ที่สามารถนำไป **สกัดพิกัดบรรทัด** สำหรับการประมวลผลต่อได้

## Why Use Aspose.OCR for Line Rectangles?

- **ความแม่นยำสูง** – อัลกอริธึมขั้นสูงตรวจจับบรรทัดแม้ในภาพที่มีเสียงรบกวนหรือเอียง  
- **ข้ามแพลตฟอร์ม** – ทำงานบน .NET Framework, .NET Core, และ .NET 5/6  
- **ไม่มีการพึ่งพาไลบรารีภายนอก** – ไลบรารี .NET แท้ ๆ ไม่ต้องมี DLL เนทีฟเพิ่มเติม  
- **ผลลัพธ์ที่หลากหลาย** – นอกจากสี่เหลี่ยมของบรรทัดแล้ว ยังสามารถดึงคำ, ตัวอักษร, และคะแนนความเชื่อมั่นได้อีกด้วย

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **No rectangles returned** | ตรวจสอบว่าภาพมีข้อความที่ชัดเจนและเป็นแนวนอน และได้ระบุ `AreasType.LINES` ไว้ |
| **Incorrect coordinates** | ตรวจสอบ DPI ของภาพ; ภาพความละเอียดต่ำอาจทำให้พิกัดไม่แม่นยำ |
| **Performance bottleneck on large images** | ปรับขนาดภาพให้มีความละเอียดที่เหมาะสมก่อนเรียก `GetRectangles` |
| **License exception** | ใช้ไลเซนส์ทดลองสำหรับการทดสอบ; ใส่ไลเซนส์เต็มสำหรับการผลิตเพื่อหลีกเลี่ยงข้อจำกัดของการประเมิน |

## Frequently Asked Questions

**Q: Can I extract individual words instead of whole lines?**  
A: Yes, use `AreasType.WORDS` with the same `GetRectangles` method to obtain word‑level bounding boxes.

**Q: Does the API support multi‑page PDFs?**  
A: Convert each PDF page to an image first, then call `GetRectangles` on each image.

**Q: How do I handle rotated text?**  
A: Enable the auto‑rotate option in the OCR settings or pre‑rotate the image before processing.

**Q: Is there a way to get confidence scores for each line?**  
A: After obtaining rectangles, call `api.RecognizeImage(...).Lines` to access line objects that include confidence values.

**Q: What .NET versions are compatible?**  
A: The library works with .NET Framework 4.5+, .NET Core 3.1+, and .NET 5/6.

## Real‑World Use Cases

- **Document layout analysis OCR** – ป้อนสี่เหลี่ยมของบรรทัดเข้าสู่เอนจิน layout เพื่อสร้างโครงสร้างคอลัมน์ใหม่  
- **Automated data extraction** – ใช้พิกัดเพื่อตัดบรรทัดแต่ละบรรทัดออกสำหรับ pipeline NLP ต่อไป  
- **Custom rendering** – วาง overlay สี่เหลี่ยมบนภาพต้นฉบับเพื่อการตรวจสอบภาพหรือแสดงผลบน UI  

## Conclusion

ขอแสดงความยินดี! คุณได้ **ดึงสี่เหลี่ยมของบรรทัด OCR** สำหรับภาพด้วย Aspose.OCR สำหรับ .NET อย่างสำเร็จ ด้วย bounding box ที่ได้ คุณสามารถนำพิกัดบรรทัดไปใช้ใน workflow ต่อไป เช่น การเรนเดอร์แบบกำหนดเอง, การสกัดข้อมูล, หรือ **layout analysis OCR** ได้แล้ว

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}