---
category: general
date: 2026-01-15
description: แปลงภาพเป็น JSON ด้วย Aspose OCR ใน C# เรียนรู้วิธีดึงข้อความจากภาพ,
  รับข้อมูลกรอบจำกัดในรูปแบบ JSON และจดจำภาพใบเสร็จ
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: th
og_description: แปลงภาพเป็น JSON ด้วย Aspose OCR ใน C# คู่มือแบบขั้นตอนต่อขั้นตอนเพื่อดึงข้อความจากภาพ,
  จดจำภาพใบเสร็จ, และรับกล่องขอบเขตในรูปแบบ JSON.
og_title: แปลงรูปภาพเป็น JSON ด้วยคู่มือ Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: แปลงภาพเป็น JSON ด้วย Aspose OCR C# คู่มือ
url: /th/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แปลงรูปภาพเป็น JSON ด้วย Aspose OCR C# คู่มือ

เคยต้องการ **convert image to JSON** แต่ไม่แน่ใจว่าห้องสมุดใดจะให้ทั้งข้อความดิบและพิกัดของคำที่แม่นยำหรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคนี้เมื่อพยายามดึงข้อความจากไฟล์รูปภาพ—โดยเฉพาะใบเสร็จ—พร้อมกับต้องการ payload JSON ที่เครื่องอ่านได้สำหรับการประมวลผลต่อไป

ในบทแนะนำนี้ เราจะพาคุณผ่านตัวอย่าง **Aspose OCR C# example** ที่ครบถ้วน ซึ่งจะแสดงวิธีดึงข้อความจากรูปภาพ, จดจำรูปใบเสร็จ, และส่งออก **JSON bounding boxes** สำหรับทุกคำ เมื่อเสร็จสิ้นคุณจะมีแอปคอนโซลที่พร้อมรันซึ่งพิมพ์สตริง JSON ที่จัดรูปแบบอย่างสวยงามซึ่งคุณสามารถส่งต่อไปยัง API, ฐานข้อมูล หรือ pipeline การวิเคราะห์ใด ๆ

> **สิ่งที่คุณจะได้เรียนรู้**  
> • โครงการ C# ที่ทำงานเต็มรูปแบบซึ่ง **converts image to JSON**  
> • ความเข้าใจว่าทำไมเราต้องเปิด `IncludeBoundingBoxes` (เป็นกุญแจสำคัญสำหรับ `json bounding boxes`)  
> • เคล็ดลับในการจัดการรูปแบบภาพและภาษาต่าง ๆ  

มาเริ่มกันเลย

---

## สิ่งที่คุณต้องเตรียม

ก่อนที่เราจะลงลึกไปในโค้ด ตรวจสอบให้แน่ใจว่าคุณได้ติดตั้งสิ่งต่อไปนี้แล้ว:

- **.NET 6.0 SDK** (หรือเวอร์ชันที่ใหม่กว่า) – โค้ดตั้งเป้าหมายที่ .NET 6 แต่ก็ทำงานบน .NET Framework 4.7+ ได้เช่นกัน  
- **Aspose.OCR for .NET** NuGet package – คุณสามารถติดตั้งได้ด้วยคำสั่ง `dotnet add package Aspose.OCR`.  
- ตัวอย่างรูปใบเสร็จ (`receipt.jpg`) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโปรเจกต์ของคุณ  
- Visual Studio 2022, VS Code, หรือ IDE ใด ๆ ที่คุณชอบ  

ไม่จำเป็นต้องใช้บริการภายนอกอื่น ๆ; ทุกอย่างทำงานบนเครื่องของคุณ

## แปลงรูปภาพเป็น JSON – ภาพรวม

แนวคิดหลักง่าย ๆ: โหลดรูปภาพ, บอก Aspose OCR ให้จดจำภาษาอังกฤษ (หรือภาษาที่รองรับใด ๆ), ขอให้รวม bounding boxes, และสุดท้ายขอผลลัพธ์ในรูปแบบ **JSON**. ไลบรารีทำงานหนักทั้งหมด—OCR, การวิเคราะห์เลย์เอาต์, และการแปลงเป็น JSON

นี่คือไดอะแกรมระดับสูงของกระบวนการ (ลองนึกภาพเป็นรูปเล็ก ๆ):

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

ไดอะแกรมเล็ก ๆ นั้นสรุปภาพรวมของ pipeline ทั้งหมดที่เราจะทำ

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose OCR

แรกสุด สร้างโปรเจกต์คอนโซลใหม่และดึงแพคเกจ Aspose OCR เข้ามา

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **เคล็ดลับมืออาชีพ:** หากคุณใช้ Visual Studio ให้คลิกขวาที่โปรเจกต์ → *Manage NuGet Packages* → ค้นหา **Aspose.OCR** และติดตั้งเวอร์ชันเสถียรล่าสุด (ปัจจุบัน 23.12).

## ขั้นตอนที่ 2: โหลดรูปภาพที่ต้องการจดจำ

เราจะใช้เมธอด `OcrImage.FromFile` เพื่ออ่านรูปใบเสร็จ ตรวจสอบให้แน่ใจว่าเส้นทางชี้ไปยังไฟล์ที่มีอยู่ มิฉะนั้นจะเกิด `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

หากรูปภาพของคุณอยู่ข้างไฟล์ `.csproj` คุณสามารถใช้ `"receipt.jpg"` ได้เลย.

## ขั้นตอนที่ 3: กำหนดค่า OCR Options สำหรับ JSON Bounding Boxes

ความมหัศจรรย์เกิดขึ้นเมื่อเราเปิด `OutputFormat = OutputFormat.Json` **และ** `IncludeBoundingBoxes = true`. ตัวแรกบอก Aspose ให้แปลงผลลัพธ์เป็น JSON, ส่วนตัวที่สองจะเพิ่ม `x`, `y`, `width`, และ `height` สำหรับทุกคำ—ตรงกับที่คุณต้องการสำหรับ `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

คุณยังสามารถปรับ `ocrOptions.Dpi` หรือ `ocrOptions.Language` หากต้องการความละเอียดสูงขึ้นหรือภาษาที่แตกต่าง

## ขั้นตอนที่ 4: ทำการจดจำ – ดึงข้อความจากรูปภาพ

ตอนนี้เราจะเรียก `Recognize`. เมธอดนี้คืนค่าอ็อบเจกต์ `OcrResult` ที่มีสตริง JSON, ข้อความดิบ, และอื่น ๆ

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

หากต้องการรองรับภาษาต่าง ๆ ให้เปลี่ยน `Language.English` เป็น `Language.Spanish`, `Language.French` เป็นต้น Aspose รองรับภาษากว่า 30 ภาษาโดยไม่ต้องทำอะไรเพิ่ม

## ขั้นตอนที่ 5: แสดงผลลัพธ์ – JSON Payload ของคุณ

สุดท้าย เราจะพิมพ์ JSON ไปยังคอนโซล ในแอปจริงคุณอาจเขียนลงไฟล์หรือส่งไปยังบริการ

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

การรันโปรแกรมควรสร้างเอกสาร JSON ที่คล้ายกับตัวอย่างด้านล่าง

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

สังเกตว่าแต่ละคำตอนนี้มี **JSON bounding box** ของมันเอง—เหมาะอย่างยิ่งสำหรับการส่งต่อไปยัง UI overlay หรือ parser ต่อไป

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอกและวางเต็มรูปแบบ ไม่มีส่วนที่ซ่อนอยู่ ไม่มีการเรียกภายนอก—เพียง C# ธรรมดา

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **ระวัง:**  
> • **ข้อผิดพลาดของเส้นทางไฟล์** – ตรวจสอบตำแหน่งรูปภาพสองครั้ง  
> • **ขาดแพคเกจ NuGet** – ตรวจสอบให้แน่ใจว่าอ้างอิง `Aspose.OCR` แล้ว  
> • **รูปแบบภาพที่ไม่รองรับ** – ใช้ JPEG, PNG, BMP, หรือ TIFF เพื่อผลลัพธ์ที่ดีที่สุด

## คำถามทั่วไปและกรณีขอบ

### ฉันสามารถแปลง **PDF page** เป็น JSON แทน JPEG ได้หรือไม่?

ได้. แปลงหน้า PDF เป็นรูปภาพก่อน (เช่นโดยใช้ `Aspose.PDF`), แล้วส่งรูปนั้นเข้าสู่ pipeline OCR เดียวกัน ผลลัพธ์ JSON จะเหมือนกันเพราะขั้นตอน OCR สนใจเฉพาะข้อมูลราสเตอร์

### ถ้าใบเสร็จเบลอจะทำอย่างไร?

เพิ่ม DPI ใน `ocrOptions`. ตัวอย่างเช่น:

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

DPI ที่สูงขึ้นอาจเพิ่มการใช้หน่วยความจำ ดังนั้นควรสมดุลระหว่างคุณภาพและประสิทธิภาพ

### ฉันต้องการ **หลายภาษา** บนใบเสร็จเดียวกัน (เช่น English + Spanish).

คุณสามารถส่งอาร์เรย์ของภาษาได้:

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose จะพยายามจดจำแต่ละภาษาตามลำดับที่ระบุ

### ฉันจะเขียน JSON ลงไฟล์อย่างไร?

เพียงแทนที่บรรทัด `Console.WriteLine` ด้วย:

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

ตอนนี้คุณมีไฟล์คงที่ที่สามารถส่งต่อไปยังบริการอื่นได้

## สรุปภาพรวม

![ตัวอย่างการแปลงรูปภาพเป็น json](convert-image-to-json.png "ตัวอย่างการแปลงรูปภาพเป็น json")

*ภาพหน้าจอแสดงผลลัพธ์ JSON payload ของคอนโซลหลังจากรันตัวอย่าง*

## สรุป

เราได้แสดงวิธี **convert image to JSON** ด้วย Aspose OCR ใน C# แล้ว โดยการกำหนดค่า `OutputFormat` และ `IncludeBoundingBoxes` คุณสามารถ **extract text from image**, **recognize receipt image**, และรับ **JSON bounding boxes** ที่แม่นยำสำหรับทุกคำ โค้ดที่สมบูรณ์และสามารถรันได้อยู่ในสแนปด้านบน คุณจึงสามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้ทันที

ต่อไปคุณจะทำอะไร? ลองส่ง JSON ไปยังตัวแสดงผล front‑end ที่ไฮไลท์แต่ละคำ, หรือส่งข้อมูลไปยังโมเดล machine‑learning ที่จำแนกรายการบนใบเสร็จ คุณยังสามารถทดลองใช้ภาษาต่าง ๆ, ตั้งค่า DPI สูงขึ้น, หรือประมวลผลหลายรูปภาพเป็นชุดในลูป

หากคุณเจออุปสรรคใด ๆ อย่าลืมเคล็ดลับเกี่ยวกับเส้นทางไฟล์, DPI, และอาร์เรย์ของภาษา อย่าลังเลที่จะฝากคอมเมนต์หรือเปิด issue ในรีโพ GitHub ที่คุณสร้างสำหรับเดโมนี้ ขอให้สนุกกับการเขียนโค้ดและสนุกกับการเปลี่ยนรูปภาพเป็น JSON ที่มีโครงสร้าง!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}