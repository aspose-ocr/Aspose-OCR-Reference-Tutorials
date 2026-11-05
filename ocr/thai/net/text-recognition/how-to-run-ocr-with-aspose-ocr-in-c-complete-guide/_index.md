---
category: general
date: 2026-02-28
description: วิธีใช้งาน OCR ใน C# ด้วย Aspose OCR – เรียนรู้วิธีดึงข้อความจากรูปภาพ,
  แปลงรูปภาพเป็น JSON หรือ XML เพียงไม่กี่ขั้นตอน.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: th
og_description: วิธีรัน OCR ใน C# ด้วย Aspose OCR – ค้นพบวิธีดึงข้อความจากภาพและแปลงภาพเป็น
  JSON หรือ XML พร้อมตัวอย่างที่พร้อมใช้งาน
og_title: วิธีใช้งาน OCR ด้วย Aspose OCR ใน C# – คู่มือฉบับสมบูรณ์
tags:
- OCR
- C#
- Aspose
- Image Processing
title: วิธีใช้งาน OCR ด้วย Aspose OCR ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีรัน OCR ด้วย Aspose OCR ใน C# – คู่มือฉบับสมบูรณ์

หากคุณกำลังสงสัย **วิธีรัน OCR** บนรูปใบเสร็จโดยใช้ C# คุณมาถูกที่แล้ว ในบทแนะนำนี้เราจะเดินผ่าน **การดึงข้อความจากรูปภาพ** แล้วต่อด้วย **การแปลงรูปภาพเป็น JSON** หรือ **การแปลงรูปภาพเป็น XML** ด้วย Aspose OCR—all in a single, self‑contained program.

ลองนึกภาพว่าคุณกำลังสร้างแอปติดตามค่าใช้จ่ายและต้องการดึงรายการจากใบเสร็จที่ถ่ายรูป การพิมพ์ข้อมูลด้วยมือทุกรายการเป็นเรื่องน่าเบื่อใช่ไหม? เมื่อจบคู่มือนี้คุณจะมีโค้ดสั้น ๆ ที่สามารถอ่านรูปใดก็ได้ ส่งคืนข้อความที่จัดโครงสร้าง และให้ผลลัพธ์ทั้งในรูปแบบ JSON และ XML พร้อมใช้ในขั้นตอนต่อไป

## ข้อกำหนดเบื้องต้น

ก่อนที่เราจะลงมือทำ โปรดตรวจสอบว่าคุณมี:

- .NET 6.0 SDK หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.8 ด้วย)
- Visual Studio 2022 (หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ)
- แพคเกจ **Aspose.OCR** จาก NuGet (`Install-Package Aspose.OCR`)
- รูปตัวอย่าง (เช่น `receipt.png`) ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงได้

ไม่ต้องตั้งค่าพิเศษเพิ่มเติม; ไลบรารีมาพร้อมโมเดล OCR ที่จำเป็นทั้งหมดแล้ว

![รูปใบเสร็จสำหรับการประมวลผล OCR – วิธีรัน OCR](receipt.png)

> *ข้อความแทนรูป: รูปใบเสร็จสำหรับการประมวลผล OCR – วิธีรัน OCR*

## การดำเนินการแบบขั้นตอนต่อขั้นตอน

ด้านล่างเราจะแบ่งโซลูชันออกเป็นส่วน ๆ แต่ละขั้นอธิบาย **ทำไม** เราต้องทำเช่นนั้น ไม่ใช่แค่ **อะไร** ที่โค้ดทำ

### 1️⃣ เริ่มต้น OCR Engine – พื้นฐานของ **วิธีรัน OCR**

คลาส `OcrEngine` คือจุดเริ่มต้น การสร้างอินสแตนซ์จะโหลดโมเดลภาษาภายในและเตรียมเครื่องมือสำหรับการจดจำ

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **เคล็ดลับ:** การใช้ `OcrEngine` ตัวเดียวกันสำหรับหลายรูปภาพจะลดการใช้หน่วยความจำและเร่งการประมวลผลแบบชุด

### 2️⃣ โหลดรูปภาพ – แกนหลักของ **การดึงข้อความจากรูปภาพ**

Aspose OCR ทำงานกับตัวห่อ `Image` ของมันเอง การใช้คำสั่ง `using` จะรับประกันว่าการเชื่อมต่อไฟล์จะถูกปล่อยออกอย่างรวดเร็ว

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

หากรูปอยู่ในรูปแบบอื่น (BMP, TIFF, PDF) วิธี `Load` เดียวกันก็รองรับ—ไม่ต้องแปลงเพิ่มเติม

### 3️⃣ รันการจดจำ OCR – ใจกลางของ **วิธีรัน OCR**

การเรียก `Recognize` จะทำงานหนัก: วิเคราะห์เลย์เอาต์, แบ่งอักขระ, และจำแนกตามภาษาที่กำหนด

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

ผลลัพธ์ `OcrResult` จะมีข้อความดิบ, คะแนนความมั่นใจ, และโครงสร้างเลย์เอาต์ที่สามารถทำซีเรียลไลซ์ได้

### 4️⃣ แปลงรูปภาพเป็น JSON – วิธีตรงไปตรงมาสำหรับ **การแปลงรูปภาพเป็น json**

JSON เหมาะกับ API เว็บหรือฐานข้อมูล NoSQL เมธอด `ToJson` จะให้สตริงที่จัดรูปแบบอย่างสวยงาม ทำให้ดีบักง่าย

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

ตัวอย่างผลลัพธ์ JSON (ตัดบางส่วนเพื่อความกระชับ):

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

คุณสามารถส่ง JSON นี้ตรงไปยัง endpoint REST หรือเก็บไว้ใน Azure Cosmos DB ได้เลย

### 5️⃣ แปลงรูปภาพเป็น XML – เมื่อ **การแปลงรูปภาพเป็น xml** จำเป็น

ระบบเก่าบางระบบยังคงใช้ XML Aspose มีเมธอด `ToXml` สำหรับสร้างตัวแทนที่สะอาดและสอดคล้องกับสคีม่า

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

ตัวอย่างส่วนของ XML:

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

ทั้งสองรูปแบบเก็บข้อมูลเชิงลำดับเดียวกัน คุณจึงเลือกใช้ตามที่เหมาะกับ pipeline ของคุณ

## ปัญหาที่พบบ่อย & วิธีดึงข้อความอย่างมั่นคง

แม้จะใช้ไลบรารีที่แข็งแรงแล้ว ภาพในโลกจริงก็ยังอาจทำให้เกิดปัญหาได้ ต่อไปนี้คือสามปัญหาที่อาจเจอและวิธีแก้

### 📏 รูปความละเอียดต่ำ

**ทำไมสำคัญ:** ตัวอักษรขนาดเล็กอาจรวมกัน ทำให้คะแนนความมั่นใจลดลง  
**วิธีแก้:** ทำการพรี‑โปรเซสภาพ—ขยายขนาดด้วย `Image.Resize` หรือใช้ฟิลเตอร์เพิ่มความคมชัดก่อนส่งให้ `Recognize`

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 คอนทราสต์แย่

**ทำไมสำคัญ:** ข้อความสีอ่อนบนพื้นหลังสีเข้มทำให้ขั้นตอนการแบ่งส่วนสับสน  
**วิธีแก้:** กลับสีหรือปรับความสว่าง/คอนทราสต์ด้วย `Image.AdjustBrightnessContrast`

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 เอกสารหลายภาษา

**ทำไมสำคัญ:** โมเดลภาษาตั้งต้นคืออังกฤษ; หากมีหลายภาษาอาจทำให้ผลลัพธ์เป็นอักขระผสมกัน  
**วิธีแก้:** ตั้งค่า `ocrEngine.Language = OcrLanguage.Multilingual;` ก่อนทำการจดจำ

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

การจัดการกับกรณีข้างต้นจะทำให้ **การดึงข้อความ** จากภาพใด ๆ กลายเป็นกระบวนการที่เชื่อถือได้ ไม่ใช่เรื่องเสี่ยงโชค

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมเต็มรูปแบบ พร้อมคอมไพล์และรัน เพียงเปลี่ยน `YOUR_DIRECTORY` ให้เป็นพาธที่เก็บรูปภาพของคุณแล้วกด F5

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล** (จัดรูปแบบเพื่ออ่านง่าย) จะมีโครงสร้าง JSON และ XML ที่บรรจุข้อความและกรอบตำแหน่งที่ดึงมาได้

## สรุป – สิ่งที่เราได้เรียนรู้

- **วิธีรัน OCR** ด้วย Aspose OCR ใน C#
- กระบวนการขั้นตอน‑ต่อ‑ขั้นตอนเพื่อ **การดึงข้อความจากรูปภาพ**
- ตัวเลือกการซีเรียลไลซ์สองแบบ: **การแปลงรูปภาพเป็น json** และ **การแปลงรูปภาพเป็น xml**
- เคล็ดลับการจัดการกับภาพความละเอียดต่ำ, คอนทราสต์แย่, และเอกสารหลายภาษา
- ตัวอย่างโค้ดครบชุดที่คัดลอก‑วางได้และสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้

## ขั้นตอนต่อไปคืออะไร?

เมื่อคุณสามารถ **ดึงข้อความ** และได้ข้อมูลที่จัดโครงสร้างแล้ว ลองพิจารณาไอเดียต่อไปนี้:

- ส่ง JSON ไปยัง Azure Function ที่เก็บใบเสร็จใน Cosmos DB
- ใช้ผลลัพธ์ XML เพื่อเติมข้อมูลในระบบบัญชีแบบ SOAP ที่มีอยู่
- ผสาน Aspose OCR กับโมเดล Machine Learning เพื่อจำแนกประเภทค่าใช้จ่ายโดยอัตโนมัติ

อย่ากลัวทดลอง—เปลี่ยน `receipt.png` เป็นใบแจ้งหนี้, นามบัตรธุรกิจ, หรือโน้ตมือเขียนก็ได้ รูปแบบเดียวกันทำงานได้กับทุกกรณี

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}