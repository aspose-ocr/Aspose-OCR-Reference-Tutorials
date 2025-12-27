---
date: 2025-12-27
description: สำรวจการสนับสนุนภาษา OCR ขั้นสูงและความสามารถกับ Aspose.OCR สำหรับ .NET
  อย่างมีประสิทธิภาพ แม่นยำ และเป็นมิตรต่อผู้พัฒนา
linktitle: OCR Language Support – Ignored Characters in Image Recognition
second_title: Aspose.OCR .NET API
title: การสนับสนุนภาษา OCR – ตัวอักษรที่ละเว้นในการจดจำภาพ
url: /th/net/ocr-settings/specify-ignored-characters/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# การสนับสนุนภาษา OCR: ระบุอักขระที่ละเว้นในการจดจำภาพ

## Introduction

การสนับสนุนภาษา OCR เป็นหัวใจสำคัญของการทำงานอัตโนมัติของเอกสารสมัยใหม่ ทำให้แอปพลิเคชันสามารถอ่านข้อความจากภาพได้หลายอักษรและสัญลักษณ์ ในบทเรียนนี้คุณจะได้เรียนรู้วิธีบอก **Aspose.OCR for .NET** ให้ละเว้นอักขระเฉพาะระหว่างการจดจำ — เทคนิคสำคัญเมื่อคุณต้องการผลลัพธ์ที่สะอาดขึ้นหรือกรองสัญญาณรบกวน เช่น หมายเลขหน้า หรือสัญลักษณ์ตกแต่ง เมื่อจบคู่มือคุณจะมีโค้ดสั้นที่พร้อมรันซึ่งแสดงคุณลักษณะนี้ตั้งแต่ต้นจนจบ

## Quick Answers
- **อะไรคือ “อักขระที่ละเว้น”?** อักขระที่เครื่อง OCR ข้ามขณะสร้างสตริงผลลัพธ์  
- **ทำไมต้องใช้?** ช่วยเพิ่มความแม่นยำเมื่อสัญลักษณ์บางอย่างไม่มีความเกี่ยวข้องกับตรรกะธุรกิจของคุณ  
- **เมธอด API ใดจัดการเรื่องนี้?** `RecognitionSettings.IgnoredCharacters`  
- **สามารถใช้ร่วมกับแพ็คเกจภาษาได้หรือไม่?** ใช่ — อักขระที่ละเว้นทำงานร่วมกับภาษาที่คุณโหลดใด ๆ  
- **ต้องการใบอนุญาตหรือไม่?** จำเป็นต้องมีใบอนุญาตชั่วคราวหรือเต็มสำหรับการใช้งานในสภาพแวดล้อมการผลิต  

## Prerequisites

ก่อนจะลงลึกในฟังก์ชันการทำงานที่ครอบคลุมของ Aspose.OCR for .NET โปรดตรวจสอบว่าคุณมีเงื่อนไขต่อไปนี้พร้อมใช้งาน:

1. Aspose.OCR Installation  

   ตรวจสอบว่าคุณได้ติดตั้ง Aspose.OCR for .NET อย่างสำเร็จแล้ว คุณสามารถค้นหาไฟล์ที่จำเป็นได้จาก [download page](https://releases.aspose.com/ocr/net/).

2. Document Directory Setup  

   ตั้งค่าไดเรกทอรีเฉพาะสำหรับเอกสารของคุณ ซึ่งจะเป็นสิ่งสำคัญสำหรับการรันตัวอย่างอย่างราบรื่น ปรับค่า `dataDir` ในตัวอย่างให้เป็นเส้นทางไปยังไดเรกทอรีเอกสารของคุณ

3. Temporary License (Optional)  

   หากคุณกำลังสำรวจ Aspose.OCR for .NET ด้วยใบอนุญาตชั่วคราว ให้รับได้จาก [here](https://purchase.aspose.com/temporary-license/).

## Import Namespaces

เพื่อเริ่มต้นการทำงานกับ Aspose.OCR for .NET คุณต้องนำเข้า Namespaces ที่จำเป็น เพิ่มบรรทัดต่อไปนี้ลงในโค้ดของคุณ:

```csharp
using System.IO;

using Aspose.OCR;
using System;
```

## Why Specify Ignored Characters?

ในหลายสถานการณ์จริง — เช่น การประมวลผลใบแจ้งหนี้ ใบเสร็จ หรือแบบฟอร์มหลายภาษา — คุณอาจเจออักขระที่ซ้ำซ้อนซึ่งไม่ได้เป็นส่วนของข้อมูลที่มีความหมาย (เช่น เครื่องหมายขีดที่ใช้เป็นตัวคั่น หมายเลขหน้า หรือสัญลักษณ์ตกแต่ง) การบอกให้เครื่อง OCR ข้ามอักขระเหล่านี้จะช่วยลดความพยายามในการประมวลผลต่อมาและเพิ่มความเชื่อถือได้ของการวิเคราะห์ต่อเนื่อง

## Step‑by‑Step Guide

### Step 1: Set Up Your Document Directory

เริ่มต้นโดยระบุไดเรกทอรีที่เก็บเอกสารของคุณ แทนที่ `"Your Document Directory"` ด้วยเส้นทางจริงของเอกสารของคุณ

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

### Step 2: Initialize Aspose.OCR

สร้างอินสแตนซ์ของเครื่อง OCR วัตถุนี้จะจัดการการเรียกจดจำทั้งหมดต่อไป

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Step 3: Recognize Image with Ignored Characters

ส่งไฟล์ภาพพร้อมกับอ็อบเจกต์ `RecognitionSettings` ที่ระบุอักขระที่คุณต้องการละเว้น ในตัวอย่างนี้เราจะละเว้นอักขระ `a`, `b` และ `1`

```csharp
// Recognize image with specified ignored characters
RecognitionResult result = api.RecognizeImage(dataDir + "SpanishOCR.bmp", new RecognitionSettings
{
    IgnoredCharacters = "ab1"
});
```

### Step 4: Display Recognized Text

สุดท้ายให้แสดงข้อความที่ทำความสะอาดแล้วออกทางคอนโซลหรือที่อื่นที่คุณต้องการ

```csharp
// Display the recognized text
Console.WriteLine(result.RecognitionText);
```

## Common Issues & Tips

- **เส้นทางไม่ถูกต้อง:** ตรวจสอบให้ `dataDir` ลงท้ายด้วยตัวคั่นเส้นทาง (`\` หรือ `/`) ที่เหมาะสมกับ OS ของคุณ  
- **ภาษาที่ไม่รองรับ:** เครื่อง OCR ต้องมีแพ็คเกจภาษาสำหรับภาพต้นฉบับ; หากไม่มี อักขระที่ละเว้นจะไม่ถูกนำไปใช้อย่างถูกต้อง  
- **ข้อผิดพลาดใบอนุญาต:** หากคุณเห็นข้อยกเว้นเกี่ยวกับใบอนุญาต ตรวจสอบว่าไฟล์ใบอนุญาตชั่วคราวถูกอ้างอิงอย่างถูกต้องในโปรเจกต์ของคุณ  

## Conclusion

Aspose.OCR for .NET มอบความสามารถ OCR ขั้นสูงให้กับนักพัฒนา ช่วยทำให้กระบวนการแปลงภาพเป็นข้อความที่แก้ไขและค้นหาได้ง่ายขึ้น โดยการทำตามคู่มือขั้นตอนนี้ คุณได้เรียนรู้วิธีการตัดอักขระที่ไม่ต้องการออก ทำให้สายงาน OCR ของคุณสะอาดและเชื่อถือได้มากขึ้น สำรวจ [documentation](https://reference.aspose.com/ocr/net/) เพื่อรับข้อมูลเชิงลึกเพิ่มเติมและค้นพบว่า Aspose.OCR สามารถยกระดับโครงการ OCR ของคุณได้อย่างไร

## Frequently Asked Questions

### Q1: Can I use Aspose.OCR for .NET in non‑commercial projects?

A1: ใช่, Aspose.OCR for .NET สามารถใช้ได้ทั้งในโครงการเชิงพาณิชย์และไม่เชิงพาณิชย์ ดูรายละเอียดเพิ่มเติมได้ที่ [licensing details](https://purchase.aspose.com/buy)

### Q2: Is there a free trial available?

A2: แน่นอน! คุณสามารถเข้าถึงการทดลองใช้ฟรี [here](https://releases.aspose.com/) เพื่อสำรวจคุณสมบัติและประโยชน์ของ Aspose.OCR for .NET ก่อนตัดสินใจซื้อ

### Q3: How can I get support for Aspose.OCR?

A3: สำหรับคำถามหรือขอความช่วยเหลือใด ๆ ให้เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) เพื่อเชื่อมต่อกับชุมชนและขอคำแนะนำจากผู้เชี่ยวชาญ

### Q4: What languages does Aspose.OCR support?

A4: Aspose.OCR รองรับภาษาหลากหลาย ทำให้เป็นตัวเลือกที่หลากหลายสำหรับงาน OCR ดูเอกสารสำหรับรายการเต็มได้

### Q5: Can I purchase a temporary license for Aspose.OCR?

A5: ใช่, หากคุณต้องการใบอนุญาตชั่วคราว คุณสามารถรับได้ [here](https://purchase.aspose.com/temporary-license/) สำหรับการใช้งานระยะสั้น

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 23.12 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}