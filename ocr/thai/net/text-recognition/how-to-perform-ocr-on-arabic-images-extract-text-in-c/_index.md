---
category: general
date: 2026-02-13
description: เรียนรู้วิธีทำ OCR บนภาพภาษาอาหรับและดึงข้อความภาษาอาหรับจากไฟล์ JPG
  คู่มือขั้นตอนต่อขั้นตอนนี้จะแสดงให้คุณเห็นวิธีอ่านข้อความจากภาพและแปลงภาพเป็นข้อความโดยใช้
  C#
draft: false
keywords:
- how to perform OCR
- extract arabic text
- read image text
- extract text jpg
- convert image to text
language: th
og_description: วิธีทำ OCR บนภาพภาษาอาหรับและดึงข้อความภาษาอาหรับออกมา ทำตามคู่มือฉบับเต็มนี้เพื่ออ่านข้อความจากไฟล์
  JPG และแปลงภาพเป็นข้อความด้วย C#
og_title: วิธีทำ OCR บนภาพอาหรับ – ดึงข้อความใน C#
tags:
- OCR
- C#
- Image Processing
title: วิธีทำ OCR บนภาพอาหรับ – ดึงข้อความใน C#
url: /th/net/text-recognition/how-to-perform-ocr-on-arabic-images-extract-text-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR บนภาพภาษาอารบิก – ดึงข้อความใน C#

เคยสงสัย **วิธีทำ OCR** บนภาพภาษาอารบิกโดยไม่ต้องบิดผมไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักเจออุปสรรคเมื่อจำเป็นต้องอ่านข้อความในภาพที่เขียนด้วยสคริปต์จากขวาไปซ้าย  

ในบทเรียนนี้คุณจะได้เห็นโซลูชันที่สมบูรณ์และสามารถรันได้ ซึ่ง **ดึงข้อความภาษาอารบิก** จากไฟล์ JPEG, แสดงวิธี **อ่านข้อความจากภาพ**, และสุดท้าย **แปลงภาพเป็นข้อความ** ที่คุณสามารถใช้ในแอปของคุณ ไม่มีการอ้างอิงที่คลุมเครือ มีเพียงโค้ดที่ชัดเจนและเหตุผลเบื้องหลังแต่ละบรรทัด  

> **Pro tip:** หากคุณทำงานกับใบเสร็จสแกน, ป้ายถนน, หรือเอกสารประวัติศาสตร์ ขั้นตอนด้านล่างจะช่วยคุณประหยัดหลายชั่วโมงจากการลองผิดลองถูก  

## สิ่งที่คุณต้องเตรียม  

- .NET 6 หรือใหม่กว่า (ตัวอย่างใช้แอปคอนโซล)  
- ไลบรารี OCR ที่รองรับภาษาอารบิก สำหรับการสาธิตเราจะใช้แพคเกจ `SimpleOcr` ที่เป็นจินตภาพ, แต่รูปแบบนี้ทำงานได้กับ Tesseract, IronOCR หรือ Microsoft Computer Vision  
- ไฟล์ภาพชื่อ `arabic_sign.jpg` ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้ (เช่น `./Images/`)  

แค่นั้นเอง ไม่ต้องใช้ SDK ขนาดใหญ่ ไม่ต้องใช้คีย์คลาวด์ เพียงไม่กี่บรรทัดของ C#  

![วิธีทำ OCR บนป้ายภาษาอารบิก](/images/arabic_sign.jpg)

*ข้อความแทนภาพ: วิธีทำ OCR บนป้ายภาษาอารบิก*

## วิธีทำ OCR บนภาพภาษาอารบิก  

ด้านล่างเราจะแบ่งกระบวนการออกเป็นสามขั้นตอนหลัก แต่ละขั้นตอนอธิบาย **ว่าอะไร** ที่เรากำลังทำ, **ทำไม** ถึงสำคัญ, และ **อย่างไร** ที่โค้ดทำงานร่วมกัน  

### ขั้นตอนที่ 1: ติดตั้งและเริ่มต้นเครื่องมือ OCR  

ขั้นแรก ให้เพิ่มแพคเกจ OCR ไปยังโปรเจกต์ของคุณ:  

```bash
dotnet add package SimpleOcr
```

จากนั้นสร้างอินสแตนซ์ของเอนจินและบอกให้ใช้โมเดลภาษาภาษาอารบิก การตั้งค่าภาษาแต่เนิ่น ๆ มีความสำคัญ; หากไม่ทำเอนจินจะถืออักขระอารบิกเป็น glyph ที่ไม่รู้จัก  

```csharp
using System;
using SimpleOcr;   // <-- fictional namespace for illustration

// Step 1: Create an OCR engine configured for Arabic
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic   // Enables right‑to‑left processing
};
```

**ทำไมถึงสำคัญ:** ภาษาอารบิกใช้ทิศทางสคริปต์ที่แตกต่างและมีรูปอักขระที่ขึ้นกับบริบท การเลือก `OcrLanguage.Arabic` อย่างชัดเจนทำให้เอนจินใช้กฎการจัดรูปที่ถูกต้องและเพิ่มความแม่นยำอย่างมาก  

### ขั้นตอนที่ 2: โหลดไฟล์ JPEG และทำการจดจำ  

ต่อไปเราจะส่งภาพให้เอนจิน วิธี `RecognizeImage` จะคืนค่าอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความดิบ, คะแนนความเชื่อมั่น, และกล่องขอบเขต (bounding boxes) ที่เป็นตัวเลือก  

```csharp
// Step 2: Recognize text from the input image
string imagePath = @"./Images/arabic_sign.jpg";

OcrResult ocrResult;
try
{
    ocrResult = ocrEngine.RecognizeImage(imagePath);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to process '{imagePath}': {ex.Message}");
    return;
}
```

**หมายเหตุกรณีขอบ:** หากไฟล์ไม่พบหรือรูปแบบไม่รองรับ, บล็อก `catch` จะให้ข้อผิดพลาดที่ชัดเจนแทนการพังแบบเงียบ ๆ สิ่งนี้เป็นประโยชน์โดยเฉพาะเมื่อ **ดึงข้อความจาก JPG** ในงานแบตช์  

### ขั้นตอนที่ 3: ดึงข้อความและใช้งาน  

สุดท้าย เราจะดึงสตริงที่จดจำได้จาก `ocrResult` แล้วแสดงผล คุณยังสามารถเขียนลงไฟล์, ส่งผ่าน API, หรือป้อนเข้าสู่สายงาน NLP ต่อไปได้  

```csharp
// Step 3: Display the extracted Arabic text
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrResult.Text);

// Optional: Save to a .txt file for later processing
System.IO.File.WriteAllText("./output/extracted_text.txt", ocrResult.Text);
```

**ผลลัพธ์ที่คาดหวัง:**  
หาก `arabic_sign.jpg` มีวลี “مكتبة المدينة” (City Library) คอนโซลจะพิมพ์ประมาณนี้:  

```
=== Extracted Arabic Text ===
مكتبة المدينة
```

ผลลัพธ์อาจมีช่องว่างเกิน; คุณสามารถทำความสะอาดด้วย `String.Trim()` หรือ regular expression หากต้องการ  

## ความแตกต่างทั่วไปและเคล็ดลับ  

### การอ่านข้อความจากภาพในรูปแบบต่าง ๆ  

โค้ดเดียวกันทำงานได้กับ PNG, BMP, หรือแม้แต่หน้า PDF (หากไลบรารีรองรับ) เพียงเปลี่ยนส่วนขยายไฟล์ใน `imagePath` จำไว้ว่าต้องคำนึงถึง **คีย์เวิร์ดหลัก** ทุกครั้งที่สลับรูปแบบคุณก็ยังทำ *วิธีทำ OCR* บนแหล่งข้อมูลใหม่อยู่  

### การปรับปรุงความแม่นยำเมื่อ **ดึงข้อความภาษาอารบิก**  

- **Pre‑process the image**: เพิ่มคอนทราสต์, แก้ไขการเอียง, หรือใช้ binary threshold  
- **Set a higher DPI**: OCR ส่วนใหญ่ต้องการอย่างน้อย 300 dpi เพื่อให้ตัวอักษรคมชัด  
- **Use language packs**: ไลบรารีบางตัวให้คุณโหลดพจนานุกรมอารบิกแบบกำหนดเองสำหรับคำเฉพาะโดเมน  

### การจัดการชุดข้อมูลขนาดใหญ่ (ดึงข้อความ JPG ในลูป)  

หากคุณมีโฟลเดอร์ที่เต็มไปด้วย JPEGs ให้ห่อขั้นตอนการจดจำไว้ในลูป `foreach`:  

```csharp
foreach (var file in Directory.GetFiles("./Images", "*.jpg"))
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text}");
}
```

รูปแบบนี้ทำให้คุณ **แปลงภาพเป็นข้อความ** ในระดับใหญ่โดยไม่ต้องเขียนโค้ดใหม่  

### เมื่อเครื่องมือให้ผลลัพธ์ว่างเปล่า  

- ตรวจสอบว่าภาพไม่มืดหรือเบลอเกินไป  
- ตรวจสอบว่าโมเดลภาษาอารบิกโหลดอย่างถูกต้อง (บางแพคเกจต้องดาวน์โหลดแยก)  
- ลองใช้ผู้ให้บริการ OCR ตัวอื่น; ตัวอย่างเช่น Tesseract มักจัดการกับภาพความละเอียดต่ำได้ดีกว่า  

## ตัวอย่างเต็มพร้อมรัน  

คัดลอกโค้ดด้านล่างไปยังโปรเจกต์คอนโซลใหม่ (`dotnet new console -n ArabicOcrDemo`) โค้ดนี้รวม `using` ที่จำเป็น, การจัดการข้อผิดพลาด, และส่วนหัวคอมเมนต์สั้น ๆ  

```csharp
// ArabicOcrDemo.csproj
// <Project Sdk="Microsoft.NET.Sdk">
//   <PropertyGroup>
//     <OutputType>Exe</OutputType>
//     <TargetFramework>net6.0</TargetFramework>
//   </PropertyGroup>
//   <ItemGroup>
//     <PackageReference Include="SimpleOcr" Version="1.2.3" />
//   </ItemGroup>
// </Project>

using System;
using SimpleOcr;   // Replace with your actual OCR library namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic
        };

        // 2️⃣ Path to the JPEG containing Arabic text
        string imagePath = @"./Images/arabic_sign.jpg";

        // 3️⃣ Run recognition with graceful error handling
        OcrResult result;
        try
        {
            result = ocrEngine.RecognizeImage(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
            return;
        }

        // 4️⃣ Output the extracted text
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(result.Text);

        // 5️⃣ Optional: persist the text for later use
        System.IO.Directory.CreateDirectory("./output");
        System.IO.File.WriteAllText("./output/extracted_text.txt", result.Text);
    }
}
```

รันด้วย:  

```bash
dotnet run --project ArabicOcrDemo.csproj
```

คุณควรเห็นวลีภาษาอารบิกแสดงบนคอนโซลและบันทึกไว้ที่ `./output/extracted_text.txt`  

## สรุป  

คุณได้เรียนรู้ **วิธีทำ OCR** บนภาพภาษาอารบิก, วิธี **ดึงข้อความภาษาอารบิก**, และวิธี **อ่านข้อความจากภาพ** จาก JPEG และ **แปลงภาพเป็นข้อความ** ในแอปคอนโซล C# ที่สะอาดและพร้อมใช้งานในผลิตภัณฑ์ กระบวนการสามขั้นตอน—ตั้งค่าเอนจิน, จดจำภาพ, และจัดการผลลัพธ์—ครอบคลุมแก่นของงาน OCR ทุกประเภท ไม่ว่าจะเป็นภาษาใดหรือไฟล์ประเภทใด  

พร้อมรับความท้าทายต่อไปหรือยัง? ลองสลับภาษาเป็นอังกฤษ, ป้อน PDF, หรือรวมผลลัพธ์กับ API แปลภาษา คุณอาจสำรวจการ **ดึงข้อความ jpg** แบบขนานโดยใช้ `Parallel.ForEach` สำหรับชุดข้อมูลขนาดมหาศาล  

มีคำถามเกี่ยวกับกรณีขอบ, การปรับประสิทธิภาพ, หรือไลบรารีทางเลือก? แสดงความคิดเห็นด้านล่าง—ขอให้เขียนโค้ดอย่างสนุก!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}