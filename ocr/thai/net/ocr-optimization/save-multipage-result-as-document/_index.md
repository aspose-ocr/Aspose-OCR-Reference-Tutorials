---
title: บันทึกผลลัพธ์หลายหน้าเป็นเอกสารในการจดจำรูปภาพ OCR
linktitle: บันทึกผลลัพธ์หลายหน้าเป็นเอกสารในการจดจำรูปภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดล็อกศักยภาพของ Aspose.OCR สำหรับ .NET บันทึกผลลัพธ์ OCR หลายหน้าเป็นเอกสารได้อย่างง่ายดายด้วยคำแนะนำทีละขั้นตอนที่ครอบคลุมนี้
weight: 14
url: /th/net/ocr-optimization/save-multipage-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# บันทึกผลลัพธ์หลายหน้าเป็นเอกสารในการจดจำรูปภาพ OCR

## การแนะนำ

ยินดีต้อนรับสู่โลกอันน่าทึ่งของการรู้จำอักขระด้วยแสง (OCR) โดยใช้ Aspose.OCR สำหรับ .NET! ในบทช่วยสอนนี้ เราจะสำรวจวิธีควบคุมความสามารถของ Aspose.OCR เพื่อบันทึกผลลัพธ์ OCR หลายหน้าเป็นเอกสาร ไม่ว่าคุณจะเป็นนักพัฒนาที่มีประสบการณ์หรือเพิ่งเริ่มต้นด้วย OCR คู่มือนี้จะแนะนำคุณในแต่ละขั้นตอน เพื่อให้แน่ใจว่าคุณจะได้ประโยชน์สูงสุดจากเครื่องมืออันทรงพลังนี้

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเจาะลึกบทช่วยสอน เรามาตรวจสอบให้แน่ใจว่าคุณได้ตั้งค่าทุกอย่างเรียบร้อยแล้ว:

1.  ติดตั้ง Aspose.OCR สำหรับ .NET: เริ่มต้นด้วยการดาวน์โหลดและติดตั้ง Aspose.OCR สำหรับ .NET คุณสามารถค้นหาไฟล์ที่จำเป็นได้[ที่นี่](https://releases.aspose.com/ocr/net/).

2.  รับการทดลองใช้หรือใบอนุญาตฟรี: หากคุณยังไม่ได้ดำเนินการ คุณสามารถขอรับรุ่นทดลองใช้ฟรีได้[ที่นี่](https://releases.aspose.com/) หรือซื้อใบอนุญาต[ที่นี่](https://purchase.aspose.com/buy).

3.  สำรวจเอกสารประกอบ: ทำความคุ้นเคยกับ[เอกสารประกอบ](https://reference.aspose.com/ocr/net/)สำหรับ Aspose.OCR สำหรับ .NET เป็นแหล่งข้อมูลที่เป็นประโยชน์สำหรับข้อมูลโดยละเอียด

4.  เข้าถึงฟอรัมสนับสนุน: หากคุณพบปัญหาใด ๆ หรือมีคำถาม[ฟอรัมสนับสนุน](https://forum.aspose.com/c/ocr/16) เป็นทรัพยากรชุมชนอันทรงคุณค่า

เมื่อคุณพร้อมแล้ว มาดูคำแนะนำทีละขั้นตอนกันดีกว่า

## นำเข้าเนมสเปซ

เริ่มต้นโครงการของคุณโดยการนำเข้าเนมสเปซที่จำเป็น:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

```csharp
// เส้นทางไปยังไดเร็กทอรีเอกสาร
string dataDir = "Your Document Directory";
```

 ให้แน่ใจว่าจะเปลี่ยน`"Your Document Directory"` ด้วยเส้นทางจริงไปยังไดเร็กทอรีเอกสารของคุณ

## ขั้นตอนที่ 2: เริ่มต้น Aspose.OCR

```csharp
// เริ่มต้นอินสแตนซ์ของ AsposeOcr
AsposeOcr api = new AsposeOcr();
```

 สร้างอินสแตนซ์ของ`AsposeOcr` เพื่อเข้าถึงฟังก์ชัน OCR

## ขั้นตอนที่ 3: จดจำรูปภาพ

```csharp
// รับรู้ถึงภาพ
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

ใช้ Aspose.OCR เพื่อจดจำข้อความจากหลายภาพ ปรับเส้นทางไฟล์ตามไฟล์รูปภาพของคุณ

## ขั้นตอนที่ 4: บันทึกผลลัพธ์ในรูปแบบที่ต้องการ

```csharp
// บันทึกผลลัพธ์ในรูปแบบที่คุณต้องการ
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

เลือกรูปแบบที่คุณต้องการ (Docx, Text, Pdf หรือ Xlsx) และบันทึกผลลัพธ์ OCR เป็นเอกสารหลายหน้า

## บทสรุป

ยินดีด้วย! คุณได้เรียนรู้วิธีบันทึกผลลัพธ์ OCR หลายหน้าเป็นเอกสารโดยใช้ Aspose.OCR สำหรับ .NET เรียบร้อยแล้ว เครื่องมืออเนกประสงค์นี้เปิดโลกแห่งความเป็นไปได้สำหรับการจดจำข้อความในโครงการของคุณ

## คำถามที่พบบ่อย

### คำถามที่ 1: มีใบอนุญาตชั่วคราวสำหรับการทดสอบหรือไม่

 A1: ได้ คุณสามารถขอรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/) สำหรับการทดสอบ Aspose.OCR

### คำถามที่ 2: ฉันสามารถจดจำข้อความจากรูปภาพในรูปแบบที่แตกต่างกันได้หรือไม่

A2: แน่นอน! Aspose.OCR รองรับรูปแบบภาพที่หลากหลาย ทำให้มั่นใจได้ถึงความยืดหยุ่นในงาน OCR ของคุณ

### คำถามที่ 3: มีข้อจำกัดเกี่ยวกับจำนวนรูปภาพในการจดจำหรือไม่

A3: จำนวนภาพที่คุณสามารถประมวลผลได้ขึ้นอยู่กับใบอนุญาตของคุณ ตรวจสอบเอกสารประกอบเพื่อดูรายละเอียด

### คำถามที่ 4: ฉันจะจัดการกับข้อผิดพลาดระหว่างการรับรู้ OCR ได้อย่างไร

A4: โปรดดูเอกสารประกอบสำหรับแนวทางปฏิบัติที่ดีที่สุดในการจัดการข้อผิดพลาด หรือขอความช่วยเหลือในฟอรัมการสนับสนุน

### คำถามที่ 5: Aspose.OCR รองรับภาษาอื่นที่ไม่ใช่ภาษาอังกฤษหรือไม่

A5: ใช่ Aspose.OCR รองรับหลายภาษา สำรวจเอกสารประกอบสำหรับรายละเอียดการสนับสนุนด้านภาษา
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
