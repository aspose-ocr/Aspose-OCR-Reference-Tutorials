---
title: รับผลลัพธ์เป็น JSON ในการรับรู้ภาพ OCR
linktitle: รับผลลัพธ์เป็น JSON ในการรับรู้ภาพ OCR
second_title: Aspose.OCR .NET API
description: ปลดปล่อยพลังของ Aspose.OCR สำหรับ .NET เรียนรู้การรับผลลัพธ์ OCR ในรูปแบบ JSON ได้อย่างง่ายดาย ปรับปรุงการจดจำรูปภาพของคุณด้วยคำแนะนำทีละขั้นตอนนี้
weight: 12
url: /th/net/text-recognition/get-result-as-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับผลลัพธ์เป็น JSON ในการรับรู้ภาพ OCR

## การแนะนำ

ในภูมิทัศน์ของเทคโนโลยีที่เปลี่ยนแปลงตลอดเวลา Optical Character Recognition (OCR) ถือเป็นเครื่องมือสำคัญที่ช่วยให้เครื่องจักรสามารถตีความและดึงข้อมูลจากภาพได้ Aspose.OCR สำหรับ .NET ช่วยให้นักพัฒนาสามารถรวมความสามารถ OCR เข้ากับแอปพลิเคชันของตนได้อย่างราบรื่น บทช่วยสอนนี้จะแนะนำคุณตลอดกระบวนการรับผลลัพธ์ OCR ในรูปแบบ JSON โดยใช้ Aspose.OCR สำหรับ .NET

## ข้อกำหนดเบื้องต้น

ก่อนที่จะเจาะลึกบทช่วยสอน ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- Visual Studio: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง Visual Studio ในระบบของคุณ
-  Aspose.OCR สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารีจาก[Aspose.OCR สำหรับเอกสาร .NET](https://reference.aspose.com/ocr/net/).

## นำเข้าเนมสเปซ

หากต้องการเริ่มต้นการรวมระบบ ให้นำเข้าเนมสเปซที่จำเป็น:

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

เริ่มต้นด้วยการกำหนดเส้นทางไปยังไดเร็กทอรีเอกสารของคุณ:

```csharp
string dataDir = "Your Document Directory";
```

## ขั้นตอนที่ 2: เริ่มต้น Aspose.OCR

สร้างอินสแตนซ์ของ Aspose.OCR เพื่อใช้ประโยชน์จากฟังก์ชันการทำงาน:

```csharp
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 3: จดจำรูปภาพ

ใช้เครื่องมือ OCR เพื่อจดจำข้อความภายในรูปภาพ:

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

## ขั้นตอนที่ 4: แสดงผลการจดจำใน JSON

แสดงผลการจดจำในรูปแบบ JSON:

```csharp
Console.WriteLine(result.GetJson());
```

## ขั้นตอนที่ 5: เสร็จสิ้นการดำเนินการ

สรุปกระบวนการด้วยข้อความแสดงความสำเร็จ:

```csharp
Console.WriteLine("GetResultAsJson executed successfully");
```

## บทสรุป

Aspose.OCR สำหรับ .NET เพิ่มความคล่องตัวในการบูรณาการความสามารถ OCR เข้ากับแอปพลิเคชันของคุณ ด้วยการทำตามคำแนะนำทีละขั้นตอนนี้ คุณจะได้รับผลลัพธ์ OCR ในรูปแบบ JSON ได้อย่างง่ายดาย ซึ่งช่วยเพิ่มประสิทธิภาพเวิร์กโฟลว์การจดจำรูปภาพของคุณ

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR สำหรับ .NET มีให้ทดลองใช้ฟรีหรือไม่

 A1: ได้ คุณสามารถทดลองใช้งานฟรีได้[ที่นี่](https://releases.aspose.com/).

### ไตรมาสที่ 2 ฉันจะหาเอกสารสำหรับ Aspose.OCR สำหรับ .NET ได้ที่ไหน

 A2: มีเอกสารประกอบให้[ที่นี่](https://reference.aspose.com/ocr/net/).

### ไตรมาสที่ 3 ฉันจะขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.OCR สำหรับ .NET ได้อย่างไร

 A3: เยี่ยมเลย[ลิงค์นี้](https://purchase.aspose.com/temporary-license/) สำหรับตัวเลือกใบอนุญาตชั่วคราว

### ไตรมาสที่ 4 ฉันจะรับการสนับสนุนจากชุมชนสำหรับ Aspose.OCR สำหรับ .NET ได้ที่ไหน

 A4: มีส่วนร่วมกับชุมชนบน[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16).

### คำถามที่ 5: ฉันสามารถซื้อใบอนุญาตสำหรับ Aspose.OCR สำหรับ .NET ได้หรือไม่

 A5: ได้ คุณสามารถซื้อใบอนุญาตได้[ที่นี่](https://purchase.aspose.com/buy).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
