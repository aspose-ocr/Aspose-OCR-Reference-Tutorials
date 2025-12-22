---
date: 2025-12-22
description: เรียนรู้วิธีดึงข้อความจากภาพโดยใช้ Aspose.OCR สำหรับ .NET คู่มือนี้จะพาคุณผ่านการเตรียมสี่เหลี่ยมสำหรับการจดจำภาพ
  OCR และเพิ่มความแม่นยำ
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: วิธีสกัดข้อความจากภาพโดยการเตรียมสี่เหลี่ยมใน OCR
url: /th/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# เตรียมสี่เหลี่ยมในระบบการรู้จำอักขระจากภาพ (OCR)

## บทนำ

Optical Character Recognition (OCR) เป็นสิ่งสำคัญสำหรับการแปลงเนื้อหาภาพให้เป็นข้อความที่สามารถค้นหาและแก้ไขได้ ในบทเรียนนี้คุณจะ **extract text from image** โดยการเตรียมสี่เหลี่ยมแบบกำหนดเองเพื่อให้เครื่อง OCR มุ่งเน้นไปที่พื้นที่เฉพาะ ใช้ Aspose.OCR for .NET เราจะอธิบายขั้นตอนทั้งหมด—ตั้งแต่การตั้งค่าโปรเจกต์ของคุณจนถึงการดึงข้อความที่ได้รับการจดจำ—เพื่อให้คุณสามารถรวมฟังก์ชันการแปลงภาพเป็นข้อความที่ทรงพลังเข้าไปในแอปพลิเคชัน .NET ของคุณ

## คำตอบสั้น
- **What does “extract text from image” mean?** หมายความว่าเป็นการแปลงอักขระที่มองเห็นในรูปภาพให้เป็นสตริงที่เครื่องคอมพิวเตอร์อ่านได้  
- **Which library helps with this in .NET?** Aspose.OCR for .NET.  
- **Do I need a license for development?** การทดลองใช้ฟรีทำงานได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์สำหรับการใช้งานจริง  
- **Can I target specific areas?** ได้โดยการกำหนดสี่เหลี่ยมที่จำกัดขอบเขตของ OCR  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7  

## “extract text from image” ด้วยสี่เหลี่ยมคืออะไร?
เมื่อคุณกำหนดโซนสี่เหลี่ยมบนภาพ เครื่อง OCR จะประมวลผลเฉพาะโซนนั้นเท่านั้น สิ่งนี้ช่วยเพิ่มความแม่นยำ ลดเวลาในการประมวลผล และทำให้คุณสามารถละเว้นพื้นหลังที่มีสัญญาณรบกวนหรือส่วนที่ไม่เกี่ยวข้องได้

## ทำไมต้องเตรียมสี่เหลี่ยมก่อนทำ OCR?
- **Focus on relevant content:** ข้ามส่วนหัว, ส่วนท้าย หรือกราฟิกตกแต่ง  
- **Boost performance:** พื้นที่ที่เล็กลงหมายถึงการจดจำที่เร็วขึ้น  
- **Improve accuracy:** สัญญาณรบกวนภาพน้อยลงทำให้ผลลัพธ์สะอาดขึ้น  

## ข้อกำหนดเบื้องต้น

- ความคุ้นเคยกับ C# และการพัฒนา .NET  
- ติดตั้งไลบรารี Aspose.OCR for .NET – คุณสามารถดาวน์โหลดได้ **[here](https://releases.aspose.com/ocr/net/)**.  
- ภาพตัวอย่าง (เช่น `sample.png`) ที่มีข้อความที่คุณต้องการ extract  

## นำเข้า Namespaces

แรกสุด นำ Namespaces ที่จำเป็นเข้าสู่สโคป:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ

ระบุที่ตั้งของไฟล์ภาพของคุณและสร้างอินสแตนซ์ของเครื่อง OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## วิธี extract text from image ด้วยหลายสี่เหลี่ยม

### ขั้นตอนที่ 2: จดจำภาพด้วยหลายสี่เหลี่ยม

#### 2.1 กำหนดสี่เหลี่ยม

สร้างรายการของอ็อบเจ็กต์ `Rectangle` ที่กำหนดขอบเขตของพื้นที่ที่คุณต้องการให้เครื่อง OCR สแกน

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 ทำการจดจำ OCR

ส่งพาธของภาพและรายการสี่เหลี่ยมไปยัง `RecognizeImage` เมธอดจะคืนค่าชุดของสตริง—แต่ละรายการสอดคล้องกับสี่เหลี่ยมหนึ่งอัน

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### ขั้นตอนที่ 3: จดจำภาพด้วย Recognition Settings (วิธีทางเลือก)

หากคุณต้องการใช้ `RecognitionSettings` คุณสามารถบรรลุผลลัพธ์เดียวกันด้วยการเรียก API ที่แตกต่างกันเล็กน้อย

#### 3.1 กำหนดการตั้งค่า recognition

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 แสดงข้อความที่จดจำได้

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## ปัญหาทั่วไปและเคล็ดลับ

- **Incorrect rectangle coordinates:** ตรวจสอบให้แน่ใจว่าค่า `X`, `Y`, `Width` และ `Height` ตรงกับพื้นที่ที่คุณต้องการ  
- **Image quality:** ภาพความละเอียดต่ำอาจให้ผลลัพธ์ OCR ที่แย่; พิจารณาการประมวลผลล่วงหน้า (เช่น การทำไบนารี)  
- **Empty results:** ตรวจสอบว่าสี่เหลี่ยมจริง ๆ มีข้อความ; มิฉะนั้นเครื่องจะคืนค่าสตริงว่าง  

## สรุป

คุณได้เรียนรู้วิธี **extract text from image** ด้วยการเตรียมสี่เหลี่ยมแบบกำหนดเองด้วย Aspose.OCR for .NET แล้ว เทคนิคนี้ให้การควบคุมระดับละเอียดต่อการประมวลผล OCR ช่วยให้คุณสร้างฟีเจอร์การดึงข้อความที่เร็วขึ้นและแม่นยำมากขึ้นในแอปพลิเคชันของคุณ

## คำถามที่พบบ่อย

**Q:** สามารถใช้ Aspose.OCR for .NET กับเฟรมเวิร์ก .NET อื่น ๆ ได้หรือไม่?  
**A:** ใช่, Aspose.OCR for .NET เข้ากันได้กับเฟรมเวิร์ก .NET ต่าง ๆ  

**Q:** มีการทดลองใช้ฟรีสำหรับ Aspose.OCR for .NET หรือไม่?  
**A:** แน่นอน! คุณสามารถเข้าถึงการทดลองใช้ฟรี **[here](https://releases.aspose.com/)**.  

**Q:** ฉันจะรับการสนับสนุนสำหรับ Aspose.OCR for .NET อย่างไร?  
**A:** ไปที่ **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** เพื่อรับการสนับสนุนโดยเฉพาะ  

**Q:** ฉันสามารถขอรับไลเซนส์ชั่วคราวเพื่อการทดสอบได้หรือไม่?  
**A:** ได้, คุณสามารถรับไลเซนส์ชั่วคราว **[here](https://purchase.aspose.com/temporary-license/)**.  

**Q:** ฉันจะหาเอกสารสำหรับ Aspose.OCR for .NET ได้จากที่ไหน?  
**A:** เอกสารพร้อมให้บริการ **[here](https://reference.aspose.com/ocr/net/)**.  

---

**อัปเดตล่าสุด:** 2025-12-22  
**ทดสอบกับ:** Aspose.OCR 24.11 for .NET  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}