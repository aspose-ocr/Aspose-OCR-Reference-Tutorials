---
date: 2025-12-17
description: เรียนรู้วิธีการดึงสี่เหลี่ยมสำหรับย่อหน้าในภาพ OCR ด้วย Aspose.OCR สำหรับ
  .NET – คู่มือที่ต้องใช้สำหรับการดึงสี่เหลี่ยมและดึงพิกัดย่อหน้า
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: วิธีสกัดสี่เหลี่ยมสำหรับย่อหน้าในระบบจดจำภาพ OCR
url: /th/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีการสกัดสี่เหลี่ยมสำหรับย่อหน้าในการจดจำภาพ OCR

## บทนำ

ยินดีต้อนรับสู่คู่มือเชิงลึกของเราเกี่ยวกับ **how to extract rectangles** สำหรับย่อหน้าในการจดจำภาพ OCR ด้วย Aspose.OCR สำหรับ .NET หากคุณกำลังมองหาเพื่อปรับปรุง pipeline การประมวลผลเอกสารของคุณ ดึงขอบเขตย่อหน้า และทำให้การสกัดข้อมูลเป็นอัตโนมัติ คุณมาถูกที่แล้ว เราจะพาคุณผ่านทุกขั้นตอน — ตั้งแต่การตั้งค่าสภาพแวดล้อมจนถึงการพิมพ์พิกัดสี่เหลี่ยม — เพื่อให้คุณเริ่มใช้ผลลัพธ์ OCR ได้ทันที

## คำตอบสั้น
- **What does “extract rectangles” mean?** มันคืนค่า bounding boxes (x, y, width, height) ของพื้นที่ข้อความที่ตรวจพบ.  
- **Which API method provides the rectangles?** เมธอด API ที่ให้สี่เหลี่ยมคือ `AsposeOcr.GetRectangles` กับ `AreasType.PARAGRAPHS`.  
- **Do I need a license for development?** ต้องการไลเซนส์สำหรับการพัฒนาหรือไม่? การทดลองใช้ฟรีทำงานได้สำหรับการทดสอบ; จำเป็นต้องมีไลเซนส์เชิงพาณิชย์สำหรับการใช้งานจริง.  
- **Can I process multiple images at once?** ฉันสามารถประมวลผลหลายภาพพร้อมกันได้หรือไม่? ใช่ — ทำลูปผ่านรายการภาพของคุณและเรียก `GetRectangles` สำหรับแต่ละไฟล์.  
- **What formats are supported?** รูปแบบที่รองรับคืออะไร? PNG, JPEG, TIFF, BMP และอื่น ๆ อีกมาก.

## “how to extract rectangles” คืออะไรใน OCR?

ในศัพท์ของ OCR การสกัดสี่เหลี่ยมหมายถึงการระบุขอบเขตเชิงเรขาคณิตที่ล้อมรอบแต่ละย่อหน้าหรือบรรทัดของข้อความภายในภาพ พิกัดเหล่านี้ทำให้คุณสามารถไฮไลท์, ครอบ, หรือวิเคราะห์ต่อส่วนเฉพาะของเอกสารที่สแกนได้

## ทำไมต้องสกัดพิกัดย่อหน้า?

- **Precise post‑processing** – คุณสามารถส่งสี่เหลี่ยมแต่ละอันเข้าสู่กระบวนการต่อเนื่อง (เช่น การแปล, การลบข้อมูล).  
- **Improved UI/UX** – แสดง bounding boxes บนภาพต้นฉบับเพื่อให้ผู้ใช้เห็นตำแหน่งที่พบข้อความ.  
- **Batch automation** – ค้นหาและแยกย่อหน้าอย่างรวดเร็วในชุดเอกสารขนาดใหญ่.

## ข้อกำหนดเบื้องต้น

- ความรู้พื้นฐานเกี่ยวกับ C# และการพัฒนา .NET.  
- สภาพแวดล้อมการพัฒนาที่ติดตั้ง Aspose.OCR สำหรับ .NET – คุณสามารถดาวน์โหลดได้จาก [here](https://releases.aspose.com/ocr/net/).  
- ความคุ้นเคยกับแนวคิดการประมวลผลภาพและเหตุผลที่ OCR มีความสำคัญสำหรับการสกัดข้อความจากไฟล์ที่สแกน.

## นำเข้า Namespaces

ในไฟล์ C# ของคุณ ให้นำเข้า namespaces ที่จำเป็นเพื่อให้คลาส OCR พร้อมใช้งาน:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## ขั้นตอนที่ 1: ตั้งค่าไดเรกทอรีเอกสารของคุณ

กำหนดโฟลเดอร์ที่บรรจุภาพที่คุณต้องการวิเคราะห์:

```csharp
string dataDir = "Your Document Directory";
```

## ขั้นตอนที่ 2: เริ่มต้นอินสแตนซ์ AsposeOcr

สร้างอ็อบเจ็กต์ `AsposeOcr` – ซึ่งให้คุณเข้าถึงฟังก์ชัน OCR ทั้งหมด:

```csharp
AsposeOcr api = new AsposeOcr();
```

## ขั้นตอนที่ 3: ระบุเส้นทางภาพ

ชี้ไปที่ไฟล์ภาพที่ต้องการประมวลผลอย่างแม่นยำ:

```csharp
string fullPath = dataDir + "sample.png";
```

## ขั้นตอนที่ 4: จดจำภาพและรับสี่เหลี่ยมย่อหน้า

เรียกเมธอด `GetRectangles` การตั้งค่า `detect_areas` เป็น `true` จะบอกเอนจินให้คืนค่า **paragraph** rectangles:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## ขั้นตอนที่ 5: พิมพ์ผลลัพธ์

แสดงพิกัดออกเพื่อให้คุณเห็น **extract paragraph coordinates** ที่ถูกตรวจจับ:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## ปัญหาทั่วไปและวิธีแก้

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|-----|
| ไม่มีสี่เหลี่ยมที่คืนค่า | คุณภาพภาพต่ำเกินไปหรือ `AreasType` ไม่ถูกต้อง | ตรวจสอบให้แน่ใจว่าภาพชัดเจนและใช้ `AreasType.PARAGRAPHS`. |
| พิกัดผิดหนึ่งตำแหน่ง | การไม่ตรงกันของการสเกล DPI | ตั้งค่า DPI ที่ถูกต้องเมื่อโหลดภาพหรือใช้ `api.Config.Dpi`. |
| ข้อยกเว้นไลเซนส์ | ทำงานโดยไม่มีไลเซนส์ที่ถูกต้องในสภาพการผลิต | ใช้ไลเซนส์ชั่วคราวหรือถาวรผ่าน `api.SetLicense`. |

## คำถามที่พบบ่อย

**Q: Is Aspose.OCR compatible with different image formats?**  
A: ใช่, Aspose.OCR รองรับ PNG, JPEG, TIFF, BMP และรูปแบบทั่วไปอื่น ๆ อีกหลายรูปแบบ.

**Q: Can I use Aspose.OCR for batch processing of multiple images?**  
A: แน่นอน! ทำลูปผ่านคอลเลกชันของเส้นทางไฟล์และเรียก `GetRectangles` สำหรับแต่ละภาพ.

**Q: Is there a free trial available for Aspose.OCR for .NET?**  
A: ใช่, คุณสามารถสำรวจการทดลองใช้ฟรีได้ที่ [here](https://releases.aspose.com/).

**Q: How can I obtain a temporary license for Aspose.OCR?**  
A: คุณสามารถรับไลเซนส์ชั่วคราวได้ที่ [here](https://purchase.aspose.com/temporary-license/).

**Q: Where can I find additional support and discussions related to Aspose.OCR?**  
A: ไปที่ [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) เพื่อรับการสนับสนุนจากชุมชนและการสนทนา.

## สรุป

ในบทแนะนำนี้เราได้แสดง **how to extract rectangles** สำหรับย่อหน้าโดยใช้ Aspose.OCR สำหรับ .NET พาเดินผ่านแต่ละโค้ดสแนปและอธิบายวิธีการตีความพิกัดที่คืนค่า โดยการนำขั้นตอนเหล่านี้เข้าไปในแอปพลิเคชันของคุณ คุณจะสามารถดึงขอบเขตย่อหน้าได้อย่างเชื่อถือได้ ปรับปรุง workflow ของเอกสาร และสร้างโซลูชัน OCR ที่ชาญฉลาดยิ่งขึ้น

---

**Last Updated:** 2025-12-17  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}