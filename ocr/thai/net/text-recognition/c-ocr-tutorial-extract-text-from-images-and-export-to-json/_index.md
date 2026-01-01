---
category: general
date: 2026-01-01
description: บทเรียน OCR ด้วย C# แสดงวิธีดึงข้อความ โหลดภาพสำหรับ OCR และเขียน JSON
  ลงไฟล์โดยใช้ Aspose.OCR – คู่มือขั้นตอนโดยละเอียด
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: th
og_description: บทเรียน OCR ด้วย C# ที่อธิบายขั้นตอนการสกัดข้อความจากภาพ, โหลดภาพสำหรับ
  OCR, และเขียน JSON ไปยังไฟล์โดยใช้ Aspose.OCR.
og_title: บทเรียน OCR ด้วย C# – ดึงข้อความและส่งออกเป็น JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: บทเรียน OCR ด้วย C# – ดึงข้อความจากรูปภาพและส่งออกเป็น JSON
url: /th/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – ดึงข้อความจากรูปภาพและส่งออกเป็น JSON

เคยสงสัยไหมว่าจะแยกข้อความจากใบแจ้งหนี้ที่สแกนได้อย่างไรโดยไม่ต้องใช้เวลาหลายชั่วโมงในการเขียนตัวแยกข้อมูลแบบกำหนดเอง? คุณไม่ได้เป็นคนเดียว ใน **c# OCR tutorial** นี้เราจะสาธิตวิธีโหลดรูปภาพสำหรับ OCR, เรียกใช้เอนจินการจดจำ, และจากนั้น **write JSON to file** เพื่อให้คุณสามารถส่งข้อมูลไปยังระบบ downstream ได้

ลองนึกภาพว่าคุณมีโฟลเดอร์ของใบเสร็จรับเงิน, แต่ละไฟล์ชื่อ `receipt1.png`, `receipt2.png`, และคุณต้องการวิธีที่รวดเร็วในการแปลงเป็นบันทึก JSON ที่สามารถค้นหาได้ นั่นคือปัญหาที่เราจะแก้ไข, และเมื่อเสร็จคุณจะมีแอปคอนโซลพร้อมรันที่ทำเช่นนั้นโดยไม่มีการพึ่งพาเพิ่มเติมนอกจาก Aspose.OCR, และไม่มีเวทมนตร์—เพียงขั้นตอนที่ชัดเจนและทำซ้ำได้

> **สิ่งที่คุณจะได้เรียนรู้**
> - วิธี **load image for OCR** ด้วย Aspose.OCR.
> - วิธี **how to extract text** และรับคะแนนความมั่นใจ.
> - การแปลงผลลัพธ์ OCR ให้เป็น payload **OCR image to JSON** ที่จัดโครงสร้างอย่างดี.
> - อย่างปลอดภัย **write JSON to file** และตรวจสอบผลลัพธ์

## ข้อกำหนดเบื้องต้น

- .NET 6 SDK หรือรุ่นที่ใหม่กว่า (โค้ดทำงานบน .NET Core ด้วยเช่นกัน).  
- Visual Studio 2022 หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ.  
- Aspose.OCR NuGet package (`Install-Package Aspose.OCR`).  
- ไฟล์รูปภาพ (PNG, JPG, BMP) ที่คุณต้องการประมวลผล – สำหรับสาธิตเราจะใช้ `invoice.png`.

หากคุณขาดสิ่งใดสิ่งหนึ่ง, ให้ดาวน์โหลด SDK จากเว็บไซต์ของ Microsoft แล้วเพิ่มแพคเกจ NuGet ผ่าน Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

เมื่อพื้นฐานพร้อมแล้ว, เรามาเริ่มการทำงานจริงกัน

## Step 1: c# OCR tutorial – เริ่มต้น OCR Engine

ก่อนที่เราจะ **load image for OCR**, เราต้องมีอินสแตนซ์ของเอนจินที่ขับเคลื่อนกระบวนการจดจำ `OcrEngine` class มีน้ำหนักเบา, แต่การห่อหุ้มด้วยบล็อก `using` เป็นแนวปฏิบัติที่ดีเพื่อให้ทรัพยากรถูกปล่อยอย่างทันท่วงที

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Pro tip:* หากคุณวางแผนประมวลผลรูปภาพหลายรูปในชุด, ให้ใช้อินสแตนซ์ `OcrEngine` เดียวกันซ้ำแทนการสร้างใหม่ทุกครั้ง จะช่วยลดการใช้หน่วยความจำและเร่งความเร็ว

## Step 2: Load image for OCR

ตอนนี้เราจะ **load image for OCR** จริง ๆ Aspose.OCR รองรับหลายรูปแบบ, คุณจึงสามารถชี้ไปที่ไฟล์ PNG, JPEG, หรือแม้แต่ TIFF แบบหลายหน้าได้ เมธอด `OcrImage.FromFile` จะอ่านไฟล์และเตรียมพร้อมสำหรับการจดจำ

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **ทำไมเรื่องนี้ถึงสำคัญ:** การโหลดรูปภาพแยกออกมาช่วยให้คุณตรวจสอบขนาด, DPI, หรือแม้กระทั่งทำการประมวลผลล่วงหน้า (เช่น การทำไบนารี) ก่อนส่งไปยังเอนจิน หากรูปภาพเสียหาย, `FromFile` จะโยนข้อยกเว้นที่ชัดเจน, ซึ่งคุณสามารถจับและบันทึกได้

## Step 3: How to extract text – เรียกใช้การจดจำ

เมื่อมีรูปภาพในมือ, เราก็สามารถ **how to extract text** จากมันได้ เมธอด `Recognize` จะคืนค่าอ็อบเจกต์ `OcrResult` ที่บรรจุไม่เพียงแต่ข้อความธรรมดา แต่ยังรวมถึงข้อมูลตำแหน่งและคะแนนความมั่นใจของแต่ละคำ

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Edge case:* บางไฟล์ PDF มีเลเยอร์ข้อความที่มองไม่เห็น หากคุณป้อนหน้าของ PDF ที่แปลงเป็นรูปภาพ, เอนจินอาจไม่เห็นอะไรเลย ในกรณีนั้นให้พิจารณาใช้ Aspose.PDF เพื่อดึงเลเยอร์ที่ซ่อนอยู่ก่อน, แล้วค่อยใช้ OCR เฉพาะเมื่อจำเป็น

## Step 4: OCR image to JSON – แปลงผลลัพธ์

คลาส `OcrResult` มีเมธอดช่วย `ToJson()` ที่ทำการซีเรียลไลซ์ชุดผลลัพธ์ทั้งหมด—รวมถึงกรอบล้อมรอบของแต่ละคำและคะแนนความมั่นใจ—เป็นสตริง JSON นี่เป็นวิธีที่สะอาดที่สุดในการทำ **OCR image to JSON** โดยไม่ต้องเขียนตัวแปลงของคุณเอง

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

หากคุณต้องการสคีมาที่กำหนดเอง, สามารถวนลูป `ocrResult.Words` แล้วสร้างอ็อบเจกต์ของคุณเอง, แต่ในหลาย ๆ สถานการณ์ JSON ที่สร้างโดยในตัวนั้นเพียงพอและมีโครงสร้างที่ดีอยู่แล้ว

## Step 5: Write JSON to file

ตอนนี้มาถึงชิ้นส่วนสุดท้ายของปริศนา: การบันทึก payload JSON เมธอด `File.WriteAllText` จะรับประกันว่าไฟล์จะถูกสร้าง (หรือเขียนทับ) อย่างอะตอมิก ตรวจสอบให้แน่ใจว่าไดเรกทอรีเป้าหมายมีอยู่, ไม่เช่นนั้นคุณจะเจอ `DirectoryNotFoundException`

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Tip:* หากต้องการ UTF‑8 พร้อม BOM หรือการเข้ารหัสอื่น, ให้ใช้ overload ที่รับอาร์กิวเมนต์ `Encoding`

## Step 6: Verify the output

การใช้ `Console.WriteLine` อย่างเร็ว ๆ จะบอกให้เราทราบว่ากระบวนการสำเร็จแล้ว คุณยังสามารถเปิดไฟล์ JSON ด้วยโปรแกรมดูเพื่อยืนยันโครงสร้างได้

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### ตัวอย่าง JSON ที่คาดหวัง

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

JSON จะรวมตำแหน่งของแต่ละคำ, ซึ่งเป็นประโยชน์หากคุณต้องการไฮไลท์ข้อความใน UI ในภายหลัง

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอกและวาง ใช้ `YOUR_DIRECTORY` แทนเส้นทางจริงที่เก็บรูปภาพของคุณ

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

เรียกใช้โปรแกรม (`dotnet run` จากโฟลเดอร์โปรเจกต์) แล้วคุณจะพบ `invoice.json` อยู่ข้างไฟล์ PNG ดั้งเดิม

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **FileNotFoundException** when loading the image | พิมพ์เส้นทางผิดหรือไฟล์หาย | ใช้ `Path.Combine` และตรวจสอบ `File.Exists` ก่อนเรียก `FromFile`. |
| **Low confidence scores** | คุณภาพภาพแย่, DPI ต่ำ | ทำการประมวลผลล่วงหน้าด้วย `ocrImage.AdjustContrast` หรือเพิ่มขนาดภาพเป็น 300 DPI. |
| **JSON file empty** | `ocrResult` คืนค่า null (เอนจินล้มเหลว) | ตรวจสอบว่ารูปแบบภาพรองรับและไลเซนส์ (ถ้ามี) ถูกตั้งค่าอย่างถูกต้อง. |
| **Performance bottleneck on large batches** | สร้าง `OcrEngine` ใหม่ทุกครั้ง | ใช้ `OcrEngine` อินสแตนซ์เดียวสำหรับทั้งชุด, ปิดการใช้งานเมื่อทำเสร็จ. |

## ขั้นตอนต่อไป

ตอนนี้คุณได้เชี่ยวชาญ **c# OCR tutorial** แล้ว, คุณอาจต้องการ:

- **Batch process** โฟลเดอร์ทั้งหมดและรวมไฟล์ JSON เข้าเป็นฐานข้อมูลเดียว.
- **Integrate** ผลลัพธ์กับ Azure Cognitive Search เพื่อทำ PDF ที่ค้นหาได้.
- **Add language support** โดยตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish` (หรือภาษาอื่นที่รองรับ).
- **Post‑process** JSON เพื่อสกัดตารางหรือคู่คีย์‑ค่าโดยใช้ regular expressions.

แต่ละการขยายนี้สร้างบนแนวคิดหลักที่เราได้ครอบคลุม: การโหลดรูปภาพสำหรับ OCR, การแยกข้อความ, การแปลงเป็น JSON, และการบันทึก JSON ไปยังดิสก์

---

### สรุป

ใน **c# OCR tutorial** นี้เราได้อธิบายขั้นตอนทั้งหมดที่จำเป็นเพื่อ **load image for OCR**, **how to extract text**, แปลงผลลัพธ์เป็น payload **OCR image to JSON**, และสุดท้าย **write JSON to file** ตัวอย่างโค้ดเต็มพร้อมใช้งานสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้, และคำอธิบายให้บริบทที่คุณต้องการเพื่อปรับใช้ในสถานการณ์จริง

ลองใช้กับชุดใบเสร็จหรือใบแจ้งหนี้ของคุณเอง—ปรับการประมวลผลภาพ, ทดลองภาษาอื่น ๆ, แล้วดูผลลัพธ์ JSON เติบโต หากเจออุปสรรคใด ๆ, กลับไปดูตารางข้อผิดพลาดหรือแสดงความคิดเห็นด้านล่าง ขอให้สนุกกับการเขียนโค้ด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}