---
title: รับผลการรับรู้ในการจดจำรูปภาพ OCR
linktitle: รับผลการรับรู้ในการจดจำรูปภาพ OCR
second_title: Aspose.OCR .NET API
description: สำรวจ Aspose.OCR สำหรับ .NET ซึ่งเป็นโซลูชัน OCR ที่ทรงพลังสำหรับการจดจำข้อความในรูปภาพได้อย่างราบรื่น
weight: 11
url: /th/net/text-recognition/get-recognition-result/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รับผลการรับรู้ในการจดจำรูปภาพ OCR

## การแนะนำ

ในโลกของการเขียนโปรแกรมที่มีการเปลี่ยนแปลงตลอดเวลา การรู้จำข้อความที่มีประสิทธิภาพคือตัวเปลี่ยนเกม และ Aspose.OCR สำหรับ .NET ก็กลายเป็นโซลูชันที่แข็งแกร่ง บทช่วยสอนนี้จะเจาะลึกถึงความแตกต่างของการใช้ Aspose.OCR เพื่อควบคุมศักยภาพของการจดจำภาพได้อย่างราบรื่น

## ข้อกำหนดเบื้องต้น

ก่อนเริ่มต้นการเดินทางนี้ ตรวจสอบให้แน่ใจว่าคุณมีข้อกำหนดเบื้องต้นต่อไปนี้:

- .NET Framework: ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้ง .NET Framework บนเครื่องของคุณแล้ว
-  Aspose.OCR สำหรับ .NET: ดาวน์โหลดและติดตั้งไลบรารี Aspose.OCR คุณสามารถค้นหาทรัพยากรที่จำเป็นได้[ที่นี่](https://releases.aspose.com/ocr/net/).

## นำเข้าเนมสเปซ

ในแอปพลิเคชัน .NET ของคุณ ให้เริ่มด้วยการนำเข้าเนมสเปซที่จำเป็น:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเร็กทอรีเอกสารของคุณ

เริ่มต้นด้วยการระบุเส้นทางไปยังไดเร็กทอรีเอกสารของคุณ:

```csharp
string dataDir = "Your Document Directory";
```

## ขั้นตอนที่ 2: เริ่มต้น Aspose.OCR

สร้างอินสแตนซ์ของ Aspose.OCR เพื่อใช้ประโยชน์จากฟังก์ชันการทำงาน:

```csharp
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 3: ระบุเส้นทางรูปภาพ

กำหนดเส้นทางแบบเต็มของภาพที่คุณต้องการจดจำ:

```csharp
string fullPath = dataDir + "sample.png";
```

## ขั้นตอนที่ 4: การตั้งค่าการรับรู้

กำหนดการตั้งค่าการจดจำตามความต้องการของคุณ ไม่ว่าจะใช้การตั้งค่าเริ่มต้นหรือแบบกำหนดเอง:

```csharp
RecognitionSettings settings = new RecognitionSettings
{
    // ระบุการตั้งค่าการจดจำของคุณที่นี่
};
```

## ขั้นตอนที่ 5: ดำเนินการจดจำรูปภาพ

ดำเนินการกระบวนการจดจำรูปภาพโดยใช้รูปภาพและการตั้งค่าที่ระบุ:

```csharp
RecognitionResult result = api.RecognizeImage(fullPath, settings);
```

## ขั้นตอนที่ 6: ผลการจดจำการพิมพ์

แสดงผลการจดจำ รวมถึงข้อความ การเอียง ย่อหน้า พื้นที่ เส้น ตัวเลือก การแสดง JSON และคำเตือน:

```csharp
PrintRecognitionResult(result);
```

## บทสรุป

ในบทช่วยสอนนี้ เราได้สำรวจกระบวนการแยกข้อความจากรูปภาพโดยใช้ Aspose.OCR สำหรับ .NET ไลบรารีอันทรงพลังนี้ทำให้การรวม OCR ง่ายขึ้น ทำให้เป็นทรัพย์สินที่มีค่าสำหรับนักพัฒนาที่กำลังมองหาโซลูชันการรู้จำข้อความที่มีประสิทธิภาพ

## คำถามที่พบบ่อย

### คำถามที่ 1: Aspose.OCR สามารถจดจำข้อความในภาษาต่างๆ ได้หรือไม่

ตอบ 1: ใช่ Aspose.OCR รองรับการรู้จำข้อความหลายภาษา ให้ความคล่องตัวสำหรับแอปพลิเคชันที่หลากหลาย

### คำถามที่ 2: Aspose.OCR สำหรับ .NET มีรุ่นทดลองใช้ฟรีหรือไม่

 A2: แน่นอน! คุณสามารถเข้าถึงการทดลองใช้ฟรี[ที่นี่](https://releases.aspose.com/).

### คำถามที่ 3: ฉันจะหาเอกสารที่ครอบคลุมสำหรับ Aspose.OCR ได้ที่ไหน

 A3: โปรดดูเอกสารประกอบ[ที่นี่](https://reference.aspose.com/ocr/net/) เพื่อข้อมูลเชิงลึกและแนวทางการใช้งาน

### คำถามที่ 4: ฉันจะรับการสนับสนุนสำหรับ Aspose.OCR ได้อย่างไร

 A4: เยี่ยมชม[ฟอรั่ม Aspose.OCR](https://forum.aspose.com/c/ocr/16) เพื่อขอความช่วยเหลือจากชุมชนและผู้เชี่ยวชาญของ Aspose

### คำถามที่ 5: ฉันสามารถขอรับใบอนุญาตชั่วคราวสำหรับ Aspose.OCR ได้หรือไม่

 A5: ได้ คุณสามารถขอรับใบอนุญาตชั่วคราวได้[ที่นี่](https://purchase.aspose.com/temporary-license/).
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
