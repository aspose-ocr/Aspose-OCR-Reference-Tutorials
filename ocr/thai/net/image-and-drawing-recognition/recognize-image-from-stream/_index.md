---
date: 2026-04-12
description: เรียนรู้วิธีการดึงข้อความจากภาพจากสตรีมด้วย Aspose OCR สำหรับ .NET ตัวอย่างขั้นตอนต่อขั้นตอนนี้แสดงการดึงข้อความ
  OCR อย่างง่าย
keywords:
- image text extraction
- image to memorystream
- ocr png file
- image stream ocr
- read image stream c#
linktitle: รู้จำภาพจากสตรีมในการจดจำภาพ OCR
second_title: Aspose.OCR .NET API
title: วิธีทำการสกัดข้อความจากภาพจากสตรีมโดยใช้ Aspose OCR
url: /th/net/image-and-drawing-recognition/recognize-image-from-stream/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการสกัดข้อความจากภาพจากสตรีมโดยใช้ Aspose OCR

ยินดีต้อนรับสู่โลกของ **image text extraction** กับ **Aspose.OCR for .NET**. ในบทแนะนำนี้คุณจะได้เห็นวิธีการอ่านสตรีมภาพ, รัน OCR บนไฟล์ PNG, และดึงข้อความที่ได้รับการจดจำเข้าสู่แอปพลิเคชัน C# ของคุณ. ไม่ว่าคุณจะกำลังสร้าง pipeline การประมวลผลเอกสาร, เครื่องมืออัตโนมัติการป้อนข้อมูล, หรือเพียงแค่ทดลองใช้ OCR, ขั้นตอนต่อไปนี้จะช่วยให้คุณเปลี่ยนภาพดิบเป็นข้อความที่ค้นหาได้ในไม่กี่นาที.

## คำตอบอย่างรวดเร็ว
- **บทแนะนำนี้สาธิตอะไร?** การสกัดข้อความจากภาพที่ให้เป็นสตรีมโดยใช้ Aspose OCR.  
- **คีย์เวิร์ดหลักที่มุ่งหมายคืออะไร?** *image text extraction* (used throughout the guide).  
- **ฉันต้องการใบอนุญาตสำหรับการพัฒนาหรือไม่?** การทดลองใช้ฟรีสามารถทำงานสำหรับการทดสอบได้; จำเป็นต้องมีใบอนุญาตเชิงพาณิชย์สำหรับการใช้งานในสภาพแวดล้อมการผลิต.  
- **ฉันสามารถประมวลผลไฟล์ PNG ได้โดยตรงหรือไม่?** ได้ – Aspose OCR รองรับรูปแบบ **ocr png file** โดยไม่ต้องแปลงเพิ่มเติม.  
- **เวอร์ชัน .NET ที่รองรับคืออะไร?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## การสกัดข้อความจากภาพคืออะไร?
Image text extraction (หรือที่เรียกว่า OCR) แปลงอักขระภาพที่มองเห็นในรูปภาพให้เป็นข้อความที่แก้ไขได้และค้นหาได้. ด้วย Aspose OCR คุณสามารถส่ง `MemoryStream` ที่บรรจุภาพที่รองรับใดก็ได้ (PNG, JPEG, BMP, ฯลฯ) และรับสตริงที่จดจำได้ในการเรียกครั้งเดียว.

## ทำไมต้องเลือก Aspose OCR สำหรับการสกัดข้อความจากภาพ?
- **การสนับสนุนหลายภาษาอย่างกว้างขวาง** – ทำงานกับหลายสิบภาษาโดยไม่ต้องตั้งค่าเพิ่มเติม.  
- **API ที่เรียบง่าย** – เพียงไม่กี่บรรทัดของ C# จะเปลี่ยน **image to memorystream** ให้เป็นข้อความที่อ่านได้.  
- **ความแม่นยำสูง** – อัลกอริทึมขั้นสูงจัดการกับการสแกนที่มีสัญญาณรบกวนและ PNG ความละเอียดต่ำ.  
- **ข้ามแพลตฟอร์ม** – ทำงานบน Windows, Linux, และ macOS ด้วย .NET Core.

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะเริ่ม, โปรดตรวจสอบว่าคุณมี:

- Aspose.OCR for .NET ที่ติดตั้งแล้ว (ดาวน์โหลดจาก [Aspose.OCR for .NET Documentation](https://reference.aspose.com/ocr/net/)).  
- ไฟล์ภาพตัวอย่าง (เช่น **sample.png**) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ดได้.

## นำเข้า Namespaces

เพิ่ม Namespaces ที่จำเป็นลงในไฟล์ C# ของคุณ:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## คู่มือขั้นตอนต่อขั้นตอน

### ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสาร
```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```
แทนที่ **"Your Document Directory"** ด้วยโฟลเดอร์จริงที่มี *sample.png*.

### ขั้นตอนที่ 2: เริ่มต้น Aspose OCR Engine
```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```
การสร้างอ็อบเจ็กต์ `AsposeOcr` จะทำให้คุณเข้าถึงเมธอด OCR ทั้งหมด.

### ขั้นตอนที่ 3: อ่านสตรีมภาพและจดจำข้อความ
```csharp
// Recognize image
using (MemoryStream ms = new MemoryStream())
using (FileStream file = new FileStream(dataDir + "sample.png", FileMode.Open, FileAccess.Read))
{
    file.CopyTo(ms);
    result = api.RecognizeImage(ms);
}
```
ที่นี่เราจะเปิด **sample.png**, คัดลอกไบต์ของมันลงใน `MemoryStream`, และส่งสตรีมนั้นไปยัง `RecognizeImage`. นี้แสดงตัวอย่าง **image stream ocr** และรูปแบบ **read image stream c#** ในกระบวนการเดียว.

### ขั้นตอนที่ 4: แสดงข้อความที่จดจำได้
```csharp
// Display the recognized text
Console.WriteLine(result);
```
ผลลัพธ์ OCR จะพิมพ์ออกที่คอนโซล; คุณยังสามารถบันทึกลงฐานข้อมูลหรือไฟล์ได้.

### ขั้นตอนที่ 5: ยืนยันการทำงานสำเร็จ
```csharp
Console.WriteLine("RecognizeImageFromStream executed successfully");
```
การยืนยันอย่างง่ายจะบอกคุณว่ากระบวนการเสร็จสมบูรณ์โดยไม่มีข้อยกเว้น.

## ปัญหาที่พบบ่อยและวิธีแก้

| ปัญหา | วิธีแก้ |
|-------|----------|
| *ผลลัพธ์ว่างเปล่า* | ตรวจสอบเส้นทางของภาพ, ให้แน่ใจว่าไฟล์สามารถอ่านได้, และยืนยันว่าภาพมีข้อความที่ชัดเจนและคอนทราสต์สูง. |
| *รูปแบบภาพที่ไม่รองรับ* | แปลงแหล่งภาพเป็น PNG หรือ JPEG ก่อนเรียก `RecognizeImage`. |
| *ข้อยกเว้นใบอนุญาต* | ใช้ใบอนุญาตชั่วคราวในระหว่างการพัฒนา หรือซื้อใบอนุญาตเต็มรูปแบบสำหรับการผลิต (ดูด้านล่าง). |

## คำถามที่พบบ่อย

**ถาม: Aspose.OCR สามารถจัดการหลายภาษาได้หรือไม่?**  
A: ใช่, Aspose.OCR รองรับภาษาหลากหลาย ทำให้เหมาะสำหรับโครงการ OCR ระดับโลก.

**ถาม: มีเวอร์ชันทดลองที่ฉันสามารถใช้ได้หรือไม่?**  
A: แน่นอน! คุณสามารถสำรวจ Aspose.OCR for .NET ด้วยการทดลองใช้ฟรี [ที่นี่](https://releases.aspose.com/).

**ถาม: ฉันจะหาความช่วยเหลือได้จากที่ไหนหากเจอปัญหา?**  
A: เยี่ยมชม [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุนจากชุมชนและผู้เชี่ยวชาญ.

**ถาม: ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับการทดสอบได้อย่างไร?**  
A: ใบอนุญาตชั่วคราวพร้อมให้บริการ [ที่นี่](https://purchase.aspose.com/temporary-license/) สำหรับการประเมิน.

**ถาม: ฉันสามารถซื้อใบอนุญาตถาวรได้จากที่ไหน?**  
A: เพื่อเพิ่ม Aspose.OCR ลงในชุดเครื่องมือการผลิตของคุณ, ไปที่ [หน้า purchase](https://purchase.aspose.com/buy).

## สรุป

คุณได้เชี่ยวชาญการ **image text extraction** จากสตรีมโดยใช้ Aspose OCR for .NET แล้ว. API ที่กระชับทำให้คุณสามารถแปลงภาพที่รองรับใดก็ได้—เช่น **ocr png file**—เป็นข้อความที่ค้นหาได้ด้วยเพียงไม่กี่บรรทัดของโค้ด. ลองทดลองกับแหล่งภาพต่าง ๆ, แพ็คภาษาต่าง ๆ, และการตั้งค่าขั้นสูงเพื่อปรับแต่งผลลัพธ์ OCR ให้เหมาะกับสถานการณ์ของคุณ.

---

**อัปเดตล่าสุด:** 2026-04-12  
**ทดสอบด้วย:** Aspose.OCR 24.12 for .NET  
**ผู้เขียน:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}