---
date: 2026-07-23
description: เรียนรู้วิธีสกัดข้อความจากภาพโดยใช้ Aspose.OCR for .NET, การเตรียม Rectangles
  เพื่อปรับปรุงความแม่นยำของ OCR และแปลงภาพเป็นข้อความอย่างมีประสิทธิภาพ.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: เตรียม Rectangles ในการจดจำภาพ OCR
og_description: สกัดข้อความจากภาพโดยใช้ Aspose.OCR for .NET. เรียนรู้การเตรียม Rectangles,
  เพิ่มความแม่นยำของ OCR, และแปลงภาพเป็นข้อความอย่างมีประสิทธิภาพ.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: สกัดข้อความจากภาพด้วย Rectangles – คู่มือ OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: สกัดข้อความจากภาพด้วย Rectangles – คู่มือ OCR
url: /th/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากภาพด้วยสี่เหลี่ยม – คู่มือ OCR

## บทนำ

การจดจำอักขระด้วยแสง (OCR) ทำให้คุณ **extract text from image** ไฟล์เพื่อให้สามารถค้นหาและแก้ไขได้ ในบทแนะนำนี้เราจะสาธิตวิธีเพิ่มความแม่นยำของ OCR โดยการเตรียมสี่เหลี่ยมกำหนดเองที่มุ่งเน้นเครื่องยนต์ไปยังโซนที่ต้องการอย่างแม่นยำ โดยใช้ Aspose.OCR for .NET คุณจะได้เห็นกระบวนการทำงานเต็มรูปแบบ — ตั้งแต่การตั้งค่าโครงการจนถึงการดึงสตริงที่ได้รับการรู้จำ — เพื่อให้คุณสามารถฝังการแปลงภาพเป็นข้อความที่เชื่อถือได้ในแอปพลิเคชัน .NET ใด ๆ

## คำตอบสั้น
- **What does “extract text from image” mean?** มันแปลงอักขระที่มองเห็นในภาพให้เป็นสตริงที่เครื่องคอมพิวเตอร์อ่านได้  
- **Which library handles this in .NET?** Aspose.OCR for .NET มีเครื่องมือ OCR ที่ครบถ้วน  
- **Do I need a license for production?** การทดลองใช้ฟรีใช้ได้สำหรับการพัฒนา; จำเป็นต้องมีลิขสิทธิ์เชิงพาณิชย์สำหรับการใช้งานจริง  
- **Can I limit OCR to specific zones?** ได้ — กำหนดสี่เหลี่ยมเพื่อโฟกัสเฉพาะพื้นที่ที่มีข้อความที่ต้องการ  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7  

## “extract text from image” กับสี่เหลี่ยมคืออะไร?
กระบวนการ `extract text from image` อ่านอักขระภายในโซนสี่เหลี่ยมที่กำหนดไว้และละเว้นส่วนอื่น ๆ การจำกัด OCR ให้ทำงานเฉพาะโซนเหล่านั้นทำให้ได้ความแม่นยำสูงขึ้น การประมวลผลเร็วขึ้น และลดความพยายามในการประมวลผลต่อมา วิธีนี้แยกข้อความที่คุณต้องการออกจากกราฟิกพื้นหลัง, องค์ประกอบตกแต่ง, และสัญญาณรบกวนภาพอื่น ๆ ที่อาจทำให้เครื่อง OCR สับสน  

## ทำไมต้องเตรียมสี่เหลี่ยมก่อน OCR?
การเตรียมสี่เหลี่ยมช่วยให้คุณมุ่งเน้นเครื่อง OCR ไปยังส่วนที่สำคัญที่สุดของภาพ ซึ่งทำให้ความเร็วและความแม่นยำดีขึ้น การจำกัดพื้นที่วิเคราะห์ทำให้ข้อมูลที่เครื่องต้องตรวจสอบลดลง ส่งผลให้ได้ผลลัพธ์เร็วขึ้นและลดการรับรู้ผิดพลาดที่เกิดจากสัญญาณรบกวนภาพที่ไม่จำเป็น  

- **Focus on relevant content:** ข้ามส่วนหัว, ส่วนท้าย หรือกราฟิกตกแต่งที่อาจทำให้เครื่องสับสน  
- **Boost performance:** พื้นที่เล็กลงต้องการการคำนวณน้อยลง ลดเวลาในการทำงานได้ถึง 40 % สำหรับการสแกนขนาดใหญ่  
- **Improve accuracy:** การลดสัญญาณรบกวนภาพทำให้ระดับการรับรู้ตัวอักษรเพิ่มจากประมาณ 85 % ไปเหนือ 95 % ในเอกสารที่มีเสียงรบกวน  

## ทำไมเรื่องนี้ถึงสำคัญสำหรับโครงการในโลกจริง
เอกสารธุรกิจหลายประเภท—เช่น ใบเสร็จ, ใบแจ้งหนี้, บัตรประจำตัว—มักผสมข้อความกับโลโก้หรือบาร์โค้ด โดยการวาดสี่เหลี่ยมรอบฟิลด์ที่คุณต้องการจริง ๆ คุณจะสกัดข้อมูลที่มีคุณค่าเท่านั้น ลดงานทำความสะอาดข้อมูลต่อไปและเพิ่มความน่าเชื่อถือของกระบวนการอัตโนมัติ การสกัดเป้าหมายนี้ช่วยลดความพยายามในการประมวลผลต่อมาและช่วยให้สอดคล้องกับมาตรฐานการจัดการข้อมูล  

## กรณีการใช้งานทั่วไป
- **Data entry automation:** ดึงฟิลด์เฉพาะจากแบบฟอร์มสแกนหรือใบเสร็จค่าใช้จ่าย  
- **Compliance checks:** แยกข้อกฎหมายหรือข้อความตามระเบียบเพื่อการตรวจสอบ  
- **Content indexing:** ทำดัชนีเฉพาะหัวข้อหรือคำบรรยายของภาพเพื่อให้มองเห็นได้ในเครื่องมือค้นหา  

## ข้อกำหนดเบื้องต้น
- ความรู้พื้นฐานของ C# และการพัฒนา .NET  
- ติดตั้งไลบรารี Aspose.OCR for .NET – ดาวน์โหลด **[here](https://releases.aspose.com/ocr/net/)** หรือเรียกดูเวอร์ชันทั้งหมด **[here](https://releases.aspose.com/)**  
- ตัวอย่างภาพ (เช่น `sample.png`) ที่มีข้อความที่คุณต้องการสกัด  

## นำเข้า Namespaces
คำสั่ง `using` นำเข้าคลาสของเครื่อง OCR และคลาสเรขาคณิตเข้าสู่สโคป  

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ
ระบุโฟลเดอร์ที่เก็บรูปภาพของคุณและสร้างอินสแตนซ์ของเครื่อง OCR  

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## วิธีสกัดข้อความจากภาพโดยใช้หลายสี่เหลี่ยม
โหลดภาพครั้งเดียว แล้วส่งรายการสี่เหลี่ยมให้กับเครื่อง OCR แต่ละสี่เหลี่ยมกำหนดพื้นที่ที่สนใจ และเครื่องจะคืนสตริงแยกสำหรับแต่ละพื้นที่ ทำให้คุณจัดการฟิลด์แต่ละอันได้อย่างอิสระและรวมผลลัพธ์ตามต้องการ  

### กำหนดสี่เหลี่ยม
อ็อบเจ็กต์ `Rectangle` บรรยายพิกัด X‑Y และขนาดของแต่ละโซนที่คุณต้องการสแกน  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### ทำการจดจำ OCR
เมธอด `RecognizeImage` ประมวลผลภาพโดยใช้รายการสี่เหลี่ยมที่ให้มาและคืนข้อความที่จดจำได้สำหรับแต่ละโซน  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## วิธีสกัดข้อความจากภาพโดยใช้ RecognitionSettings (วิธีทางเลือก)
หากคุณต้องการเรียกแบบตั้งค่า คุณสามารถทำผลลัพธ์เดียวกันด้วย `RecognitionSettings` วัตถุนี้ช่วยให้คุณรวมการกำหนดสี่เหลี่ยมพร้อมกับภาษา, DPI, และตัวเลือก OCR อื่น ๆ เพื่อให้ได้การเรียก API ที่สะอาดและใช้พารามิเตอร์เดียว  

### กำหนดการตั้งค่าการจดจำ
`RecognitionSettings` ให้คุณรวมรายการสี่เหลี่ยมและตัวเลือกเพิ่มเติม (เช่น ภาษา, DPI) ไว้ในอ็อบเจ็กต์เดียว  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### แสดงข้อความที่จดจำได้
วนลูปผ่านสตริงที่คืนมาและแสดงข้อความของแต่ละโซน  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## ปัญหาทั่วไป & เคล็ดลับ
- **Incorrect rectangle coordinates:** ตรวจสอบให้แน่ใจว่า `X`, `Y`, `Width`, และ `Height` ตรงกับพื้นที่ที่ต้องการ  
- **Image quality:** ภาพความละเอียดต่ำหรือบีบอัดมากทำให้ผล OCR แย่ลง; พิจารณาการประมวลผลล่วงเช่นการทำไบนารีไลเซชัน  
- **Empty results:** ตรวจสอบให้สี่เหลี่ยมมีข้อความที่อ่านได้; มิฉะนั้นเครื่องจะคืนสตริงว่าง  

## การแก้ไขปัญหาและแนวทางปฏิบัติที่ดีที่สุด
| Symptom | Likely Cause | Remedy |
|---------|--------------|--------|
| No output or empty strings | Rectangles outside image bounds | Double‑check image dimensions and rectangle coordinates |
| Garbled characters | Poor contrast or noise | Apply grayscale conversion and thresholding before OCR |
| Slow performance on large files | Too many rectangles or very large image | Split the image or reduce rectangle count where possible |

## สรุป
คุณได้เรียนรู้วิธี **extract text from image** ด้วยการเตรียมสี่เหลี่ยมกำหนดเองกับ Aspose.OCR for .NET วิธีนี้ให้การควบคุมที่แม่นยำต่อการประมวลผล OCR ส่งมอบคุณลักษณะการสกัดข้อความที่เร็วและแม่นยำยิ่งขึ้นสำหรับโซลูชัน .NET ใด ๆ  

## คำถามที่พบบ่อย
**Q:** ฉันสามารถใช้ Aspose.OCR for .NET กับเฟรมเวิร์ก .NET อื่น ๆ ได้หรือไม่?  
**A:** ใช่, Aspose.OCR for .NET ทำงานร่วมกับ .NET Framework 4.5+, .NET Core 3.1+, และ .NET 5/6/7  

**Q:** มีรุ่นทดลองฟรีหรือไม่?  
**A:** แน่นอน! ดาวน์โหลดรุ่นทดลอง **[here](https://releases.aspose.com/)**  

**Q:** จะหาการสนับสนุนสำหรับ Aspose.OCR for .NET ได้จากที่ไหน?  
**A:** เยี่ยมชม **[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16)** เพื่อรับความช่วยเหลือเฉพาะด้าน  

**Q:** สามารถขอรับลิขสิทธิ์ชั่วคราวสำหรับการทดสอบได้หรือไม่?  
**A:** ได้, ลิขสิทธิ์ชั่วคราวมีให้ **[here](https://purchase.aspose.com/temporary-license/)**  

**Q:** เอกสารอย่างเป็นทางการอยู่ที่ไหน?  
**A:** อ้างอิง API เต็มรูปแบบอยู่ **[here](https://reference.aspose.com/ocr/net/)**  

---

**อัปเดตล่าสุด:** 2026-07-23  
**ทดสอบด้วย:** Aspose.OCR 24.11 for .NET  
**ผู้เขียน:** Aspose  

{{< blocks/products/products-backtop-button >}}

## บทแนะนำที่เกี่ยวข้อง
- [วิธีสกัดสี่เหลี่ยมสำหรับย่อหน้าการจดจำภาพ OCR](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [วิธี OCR ภาพ – ทำ OCR บนภาพในการจดจำภาพ OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [วิธีสกัดข้อความจากภาพโดยใช้ Aspose.OCR for .NET](/ocr/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}