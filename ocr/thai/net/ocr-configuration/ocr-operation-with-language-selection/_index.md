---
date: 2025-12-21
description: เรียนรู้วิธีทำ OCR และสกัดข้อความจากภาพโดยใช้ Aspose.OCR สำหรับ .NET
  คู่มือแบบขั้นตอนนี้แสดงการจดจำข้อความหลายภาษาและการเลือกภาษา.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: วิธีทำ OCR พร้อมการเลือกภาษาใน Aspose.OCR
url: /th/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR พร้อมการเลือกภาษาใน Aspose.OCR

## บทนำ

หากคุณต้องการ **how to perform OCR** บนรูปภาพและดึงข้อความจากไฟล์รูปภาพในแอปพลิเคชัน .NET, Aspose.OCR for .NET ให้โซลูชันที่เร็ว, แม่นยำ, และรับรู้ภาษา. ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างจริงที่แสดงการจดจำภาพด้วย OCR พร้อมการเลือกภาษา, เพื่อให้คุณสามารถดึงข้อความหลายภาษาออกจากรูปภาพได้ด้วยเพียงไม่กี่บรรทัดของโค้ด.

## คำตอบอย่างรวดเร็ว
- **What does Aspose.OCR do?** มันจดจำข้อความที่พิมพ์และเขียนด้วยมือในรูปภาพและคืนค่าข้อความที่ดึงออกมา.  
- **Can I choose the language?** ใช่ – คุณสามารถระบุภาษาที่รองรับใดก็ได้ เช่น English, German, Spanish, Chinese เป็นต้น.  
- **Do I need a license for development?** การทดลองใช้ฟรีทำงานสำหรับการประเมิน; จำเป็นต้องมีลิขสิทธิ์สำหรับการใช้งานจริง.  
- **Which .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **Is skew correction automatic?** คุณสามารถเปิดใช้งาน `AutoSkew` และปรับแต่งค่าการตั้งค่า `SkewAngle` ได้.

## ทำไมต้องเลือก Aspose.OCR สำหรับงาน OCR?

- **High accuracy** ครอบคลุมหลายแบบอักษรและคุณภาพของภาพ.  
- **Built‑in language selection** กำจัดความจำเป็นของแพ็คภาษาแบบภายนอก.  
- **Simple API** ที่ผสานรวมได้อย่างสะอาดกับโครงการ C# ที่มีอยู่.  
- **No external dependencies** – ทุกอย่างทำงานในเครื่อง, ทำให้ข้อมูลของคุณปลอดภัย.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงลึกไปในโค้ด, โปรดตรวจสอบว่าคุณมีข้อกำหนดต่อไปนี้พร้อมใช้งาน:

- Aspose.OCR for .NET: ตรวจสอบว่าคุณได้ติดตั้งไลบรารี Aspose.OCR แล้ว คุณสามารถดาวน์โหลดได้จาก [Aspose.OCR for .NET download page](https://releases.aspose.com/ocr/net/).

- Development Environment: ตั้งค่าสภาพแวดล้อมการทำงานด้วยแอปพลิเคชัน .NET หากคุณยังไม่ได้ทำ, โปรดดูที่ [documentation](https://reference.aspose.com/ocr/net/) สำหรับคำแนะนำโดยละเอียด.

## นำเข้า Namespaces

ในแอปพลิเคชัน .NET ของคุณ, เริ่มต้นโดยการนำเข้า namespaces ที่จำเป็น:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: เริ่มต้น Aspose.OCR

เริ่มต้นด้วยการสร้างอินสแตนซ์ของคลาส Aspose.OCR. สิ่งนี้จะเป็นการเตรียมพื้นฐานสำหรับการใช้ความสามารถ OCR ภายในแอปพลิเคชันของคุณ.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 2: ระบุเส้นทางรูปภาพ

ต่อไป, กำหนดพาธไปยังรูปภาพที่คุณต้องการทำ OCR. ตรวจสอบให้แน่ใจว่ารูปภาพเข้าถึงได้จากแอปพลิเคชันของคุณ.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## ขั้นตอนที่ 3: จดจำภาพด้วยการเลือกภาษา

ต่อไปเป็นการดำเนินการ OCR หลัก. ใช้ไลบรารี Aspose.OCR เพื่อจดจำข้อความจากรูปภาพที่ระบุ. ปรับการตั้งค่าการจดจำ, รวมถึงการเลือกภาษา.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## ขั้นตอนที่ 4: พิมพ์และแสดงผลลัพธ์

หลังจากการทำ OCR, พิมพ์และแสดงผลลัพธ์, รวมถึงข้อความที่จดจำได้, พื้นที่, คำเตือน, และการแสดงผลในรูปแบบ JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

## ปัญหาที่พบบ่อยและเคล็ดลับ

- **Incorrect language selection** – หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบให้แน่ใจว่า property `Language` ตรงกับภาษาของภาพต้นฉบับ.  
- **Skewed images** – เปิดใช้งาน `AutoSkew` หรือปรับค่า `SkewAngle` ด้วยตนเองเพื่อความแม่นยำที่ดีกว่าในสแกนที่เอียง.  
- **Large files** – ประมวลผลภาพขนาดใหญ่เป็นชิ้นส่วนหรือปรับความละเอียดลงก่อนส่งให้ `RecognizeImage` เพื่อประหยัดหน่วยความจำ.

## สรุป

ขอแสดงความยินดี! คุณได้เรียนรู้ **how to perform OCR** พร้อมการเลือกภาษาโดยใช้ Aspose.OCR for .NET. บทแนะนำนี้แสดงวิธีดึงข้อความจากไฟล์รูปภาพ, ปรับแต่งการตั้งค่าการจดจำ, และจัดการกับเนื้อหาหลายภาษาได้อย่างง่ายดาย.

## คำถามที่พบบ่อย

### Q1: Aspose.OCR เหมาะสำหรับการจดจำข้อความหลายภาษาไหม?

A1: ใช่, Aspose.OCR รองรับหลายภาษา, ให้ความยืดหยุ่นสำหรับงาน OCR หลายภาษา.

### Q2: ฉันสามารถปรับแต่งการตั้งค่า OCR สำหรับลักษณะเฉพาะของภาพได้ไหม?

A2: แน่นอน! ปรับพารามิเตอร์เช่นมุมเอียง, การจดจำบรรทัด, และการตรวจจับพื้นที่เพื่อเพิ่มประสิทธิภาพ OCR สำหรับสถานการณ์ต่าง ๆ.

### Q3: ฉันจะหาแหล่งสนับสนุนเพิ่มเติมหรือการสนทนาชุมชนได้จากที่ไหน?

A3: เยี่ยมชม [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุนและการสนทนากับชุมชน.

### Q4: มีการทดลองใช้ฟรีหรือไม่?

A4: มี, สำรวจ [free trial](https://releases.aspose.com/) เพื่อสัมผัสความสามารถของ Aspose.OCR.

### Q5: ฉันจะซื้อ Aspose.OCR สำหรับ .NET ได้อย่างไร?

A5: เพื่อซื้อ, เยี่ยมชม [purchase page](https://purchase.aspose.com/buy).

---

**อัปเดตล่าสุด:** 2025-12-21  
**ทดสอบด้วย:** Aspose.OCR 24.11 for .NET  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}