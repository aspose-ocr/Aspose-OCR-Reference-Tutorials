---
category: general
date: 2026-05-31
description: เรียนรู้วิธีรับคะแนนความเชื่อมั่นของ OCR ใน C# ขณะสกัดข้อความจากภาพและอ่านภาพใบเสร็จด้วย
  Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: th
og_description: คะแนนความเชื่อมั่นของ OCR ช่วยให้คุณประเมินความแม่นยำ; คู่มือนี้แสดงวิธีดึงข้อความจากภาพ,
  รับกล่องขอบเขต, และอ่านภาพใบเสร็จโดยใช้ Aspose OCR.
og_title: คะแนนความเชื่อมั่นของ OCR ใน C# – คู่มือฉบับสมบูรณ์
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: คะแนนความเชื่อมั่น OCR ใน C# – คู่มือฉบับสมบูรณ์
url: /th/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คะแนนความเชื่อมั่นของ OCR ใน C# – คู่มือเต็ม

เคยสงสัยไหมว่าจะแสดง **OCR confidence scores** อย่างไรเมื่อคุณต้องการ *extract text from image*? บางทีคุณอาจกำลังพยายาม **read receipt image** เพื่อการติดตามค่าใช้จ่ายและต้องการรู้ว่าตัวอักษรใดที่เครื่องไม่แน่ใจ ข่าวดีคือ? ด้วย Aspose.OCR คุณสามารถดึงเปอร์เซ็นต์ความเชื่อมั่น, bounding boxes, และ plain text จากไฟล์ JPG ได้ในไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้เราจะพาคุณผ่านทุกอย่างที่ต้องรู้: การติดตั้งไลบรารี, การกำหนดค่า engine เพื่อ **perform OCR on JPG**, การดึงคะแนนความเชื่อมั่น, และการตีความ **OCR bounding boxes** ที่บอกตำแหน่งของแต่ละอักษรบนหน้า. เมื่อจบคุณจะมีแอปคอนโซลพร้อมรันที่พิมพ์อักขระทุกตัว, ความเชื่อมั่นของมัน, และตำแหน่ง—เหมาะสำหรับการตรวจสอบใบเสร็จหรือเอกสารสแกนใด ๆ.

## What You’ll Learn

- ติดตั้ง Aspose.OCR ผ่าน NuGet และตั้งค่า OCR engine เบื้องต้น  
- กำหนดค่า `OcrOptions` เพื่อขอผลลัพธ์ plain‑text **with confidence scores** และ **bounding boxes**  
- วนลูป `OcrResult` เพื่อ **extract text from image** ทีละบรรทัดและสัญลักษณ์  
- จัดการกับปัญหาทั่วไปเช่นไฟล์หาย, ตัวอักษรที่ความเชื่อมั่นต่ำ, และรูปแบบที่ไม่ใช่ JPG  
- ขยายตัวอย่างเพื่อประมวลผลหลายไฟล์ receipt image ในโฟลเดอร์  

ไม่จำเป็นต้องมีประสบการณ์กับ Aspose มาก่อน; เพียงแค่สภาพแวดล้อม .NET ที่ทำงานได้และ receipt image (JPG) ที่คุณต้องการทดสอบ.

---

## ขั้นตอนที่ 1 – Install Aspose.OCR และเตรียมโปรเจคของคุณ

อย่างแรกสุดคุณต้องการแพคเกจ Aspose.OCR จาก NuGet. เปิดเทอร์มินัลในโฟลเดอร์โปรเจคของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** การทดลองใช้ฟรีทำงานได้ถึง 200 หน้า, ซึ่งเพียงพอสำหรับการทดสอบการสแกนใบเสร็จ.

หลังจากติดตั้งแพคเกจแล้ว, สร้างโปรเจคคอนโซลใหม่ (หากคุณยังไม่มี):

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

ตอนนี้คุณสามารถเปิดไฟล์ `Program.cs` ที่สร้างขึ้นและเริ่มเพิ่ม using directives:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

เนมสเปซเหล่านี้ให้คุณเข้าถึง `OcrEngine`, `OcrOptions`, และประเภทผลลัพธ์ที่เราจะต้องใช้ต่อไป.

## ขั้นตอนที่ 2 – Get OCR confidence scores and OCR bounding boxes

นี่คือหัวใจของบทแนะนำ. เราจะกำหนดค่า engine เพื่อให้แต่ละอักขระที่รู้จำมาพร้อมกับ **confidence score** และ **bounding box** (สี่เหลี่ยมที่ล้อมรอบ glyph). ส่วนหัว H2 เองก็มีคีย์เวิร์ดหลักตามกฎ SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**ทำไมต้องรวม confidence scores?**  
คะแนนความเชื่อมั่น (0‑100%) บอกคุณว่า engine แน่ใจแค่ไหนกับแต่ละอักขระ. หากคุณนำผลลัพธ์ไปใช้ในตรรกะต่อเนื่อง—เช่น workflow การอนุมัติค่าใช้จ่าย—คุณสามารถปฏิเสธหรือทำเครื่องหมายสัญลักษณ์ที่ความเชื่อมั่นต่ำโดยอัตโนมัติ.

**ทำไมต้องขอ bounding boxes?**  
Bounding boxes มีความสำคัญเมื่อคุณต้องการไฮไลท์ข้อความบนภาพต้นฉบับ, ดึงส่วนย่อย, หรือจัดตำแหน่งผลลัพธ์ OCR กับ UI overlay. แต่ละ `character.Bounds` ให้ค่า X, Y, ความกว้าง, และความสูงในพิกเซล.

## ขั้นตอนที่ 3 – Perform OCR on JPG and extract text from image

ตอนนี้เราจะรัน engine จริง ๆ. การเรียก `Recognize()` ทำงานหนักทั้งหมดและคืนค่าอ็อบเจ็กต์ `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

หากเส้นทางภาพผิดหรือไฟล์ไม่ใช่รูปแบบที่รองรับ, Aspose จะโยน `FileNotFoundException` หรือ `UnsupportedImageFormatException`. ควรห่อการเรียกในบล็อก try/catch ในโค้ด production เพื่อจัดการกรณีขอบอย่างราบรื่น.

### ดึง plain text

หากคุณต้องการเพียงข้อความที่ต่อเนื่อง, คุณสามารถอ่าน `ocrResult.Text` ได้:

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

แต่เนื่องจากเรายังขอ confidence scores และ bounding boxes, เราจะวนลูปผ่านโครงสร้างเพื่อดูรายละเอียดของแต่ละอักขระ.

## ขั้นตอนที่ 4 – Iterate through lines, symbols, and display OCR confidence scores

นี่คือลูปที่พิมพ์อักขระทุกตัว, ความเชื่อมั่นของมัน, และกล่องของมัน. นี่คือจุดที่ตัวอย่าง **read receipt image** ส่องแสงจริง ๆ.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

ผลลัพธ์ตัวอย่างอาจมีลักษณะดังนี้:

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**การตีความตัวเลข:**  
- **Confidence ≥ 90%** – ปกติปลอดภัยต่อการยอมรับ.  
- **Confidence 70‑89%** – คุณอาจต้องตรวจสอบสองครั้ง, โดยเฉพาะตัวเลขในจำนวนเงิน.  
- **Confidence < 70%** – ควรทำเครื่องหมายเพื่อการตรวจสอบด้วยมือ.

## ขั้นตอนที่ 5 – Full runnable example (including error handling)

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมเต็มที่คุณสามารถ copy‑paste ไปยัง `Program.cs`. มันรวมการตรวจสอบไฟล์หายอย่างง่ายและพิมพ์ข้อความเป็นมิตรหาก OCR ล้มเหลว.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรัน `dotnet run` คอนโซลจะแสดงข้อความใบเสร็จที่ต่อเนื่องก่อน, จากนั้นรายการของแต่ละอักขระพร้อมคะแนนความเชื่อมั่นและ bounding box. หากความเชื่อมั่นของอักขระต่ำ, คุณจะเห็นเปอร์เซ็นต์ต่ำกว่า 80, ซึ่งเป็นสัญญาณให้ตรวจสอบส่วนนั้นของใบเสร็จด้วยมือ.

## โบนัส: Processing Multiple Receipts in a Folder

หากคุณมีชุดของ receipt JPGs, ให้ใส่ตรรกะข้างต้นในลูป `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. จำไว้ว่าให้รีเซ็ต `OcrEngine` สำหรับแต่ละไฟล์, หรือสร้างอ็อบเจ็กต์ใหม่ภายในลูปเพื่อหลีกเลี่ยงการรั่วของสถานะ.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

การประมวลผลเป็นกลุ่มเป็นประโยชน์สำหรับการนำเข้าค่าใช้จ่ายรายคืน.

## สรุป

ตอนนี้คุณมีโซลูชันครบวงจรสำหรับการรับ **OCR confidence scores** ใน C#, **extracting text from image**, และการดึง **OCR bounding boxes** ขณะ **perform OCR on JPG** เช่น **read receipt image**. โค้ดเป็นอิสระเต็มรูปแบบ, ทำงานกับเวอร์ชันล่าสุดของ Aspose.OCR (ตั้งแต่ 2026‑05‑31), และให้ข้อมูลละเอียดที่คุณต้องการเพื่อสร้าง pipeline การประมวลผลเอกสารที่เชื่อถือได้.

ต่อไปทำอะไร? ลองแสดง bounding boxes บนใบเสร็จต้นฉบับด้วย `System.Drawing` หรือไลบรารี UI, หรือส่งอักขระที่ความเชื่อมั่นต่ำไปยังบริการตรวจสอบระดับสอง. คุณยังสามารถทดลองกับภาษาต่าง ๆ โดยตั้งค่า `ocrEngine.Options.Language = OcrLanguage.French;` – API รองรับหลาย locale.

ขอให้สนุกกับการเขียนโค้ด, และขอให้คะแนนความเชื่อมั่นของคุณสูงเสมอ! 

![Console output showing OCR confidence scores and bounding boxes for a receipt


## สิ่งที่คุณควรเรียนต่อไป?

- [ดึงข้อความจากภาพ C# ด้วยการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [วิธีรับตัวเลือกอักขระ OCR สำหรับอักขระที่รู้จำในการจดจำภาพ](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [วิธีใช้ Aspose OCR เพื่อผลลัพธ์ JSON ในการจดจำภาพ](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}