---
category: general
date: 2026-03-26
description: วิธีทำ OCR แบบเป็นชุดใน C# ทำให้การสกัดข้อความจากไฟล์ PNG ง่ายขึ้น ตามบทเรียน
  OCR ด้วย C# แบบขั้นตอนต่อขั้นตอนเพื่อสกัดข้อความเป็นชุดด้วย Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: th
og_description: วิธีทำ OCR แบบกลุ่มใน C# ช่วยให้คุณดึงข้อความจากไฟล์ PNG ได้อย่างรวดเร็ว
  คู่มือนี้จะพาคุณผ่านการสอน OCR ด้วย C# อย่างครบถ้วนพร้อมการดึงข้อความแบบกลุ่ม
og_title: วิธีทำ OCR แบบกลุ่มใน C# – ดึงข้อความจาก PNG
tags:
- OCR
- C#
- Aspose
title: วิธีทำ OCR แบบแบตช์ใน C# – ดึงข้อความจากไฟล์ PNG
url: /th/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR เป็นชุดใน C# – ดึงข้อความจาก PNG

เคยสงสัย **วิธีทำ OCR เป็นชุด** กับกองของภาพหน้าจอโดยไม่ต้องเขียนโปรแกรมแยกสำหรับแต่ละไฟล์หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการเรามักมี PNG หลายสิบไฟล์ที่ต้องดึงข้อความออกมา และการทำแบบทีละไฟล์นั้นน่าเบื่อ  

ข่าวดีคืออะไร? ด้วย Aspose OCR คุณสามารถสร้างแอปคอนโซล C# เล็ก ๆ ที่ประมวลผลรูปภาพทั้งหมดพร้อมกัน ทำให้คุณได้ **การดึงข้อความเป็นชุด** อย่างรวดเร็วและผลลัพธ์ที่เรียบร้อย ในคู่มือนี้เราจะพาคุณผ่าน **c# ocr tutorial** แบบเต็ม ๆ อธิบายว่าทำไมแต่ละส่วนจึงสำคัญ และแสดงให้คุณเห็นว่าผลลัพธ์ออกมาเป็นอย่างไร

เมื่ออ่านบทความนี้จนจบแล้วคุณจะสามารถ:

* โหลดรายการไฟล์ PNG (หรือภาพที่รองรับอื่น ๆ) ทั้งหมดในครั้งเดียว  
* กำหนดค่า `OcrEngine` ร่วมกันเพื่อให้การตั้งค่าเหมือนกันตลอดชุดงาน  
* รันคิวการจดจำด้วยผู้ทำงานขนานสูงสุดสี่คน  
* ดึงข้อความที่จดจำได้จากแต่ละหน้าและพิมพ์ออกที่คอนโซล  

ไม่มีเวทมนตร์ มีแค่โค้ดที่มั่นคงซึ่งคุณสามารถนำไปใส่ในโซลูชันของคุณได้ทันที

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก โปรดตรวจสอบว่าคุณมี:

* .NET 6 SDK (หรือเวอร์ชัน .NET ล่าสุด)  
* ใบอนุญาต Aspose OCR ที่ถูกต้องหรือคีย์ประเมินผลชั่วคราว  
* โฟลเดอร์ที่บรรจุไฟล์ PNG ที่ต้องการประมวลผล  
* Visual Studio 2022 หรือโปรแกรมแก้ไขที่คุณชื่นชอบ  

เท่านี้—ไม่มีแพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.OCR` และ `System.Collections.Generic` มาตรฐาน

## วิธีทำ OCR เป็นชุด – ตั้งค่าโปรเจกต์

อย่างแรกเลย ให้สร้างโปรเจกต์คอนโซลใหม่และดึงไลบรารี Aspose OCR เข้ามา

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

หลังจากการกู้คืนเสร็จสิ้น ให้เปิด **Program.cs** (หรือสร้างไฟล์ใหม่) แล้วเพิ่ม `using` directives ปกติ:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

โครงสร้างพื้นฐานง่าย ๆ นี้ทำให้เรามีการเข้าถึง `OcrEngine`, `RecognitionQueue` และคลาสช่วยเหลือต่าง ๆ ที่เราจะใช้ต่อไป

## ดึงข้อความจาก PNG – เตรียมรายการภาพ

ต่อไปเราต้องบอกโปรแกรมว่า **PNG ใด** ที่จะนำไปทำ OCR วิธีที่ตรงไปตรงมาที่สุดคือการสร้าง `List<string>` ที่เก็บพาธแบบเต็มหรือแบบสัมพันธ์

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

แทนที่ `YOUR_DIRECTORY` ด้วยพาธโฟลเดอร์จริงของคุณ หากคุณมีชุดไฟล์แบบไดนามิกก็สามารถใช้ `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` แล้วใส่ผลลัพธ์ลงในรายการได้ จุดสำคัญคือ **การดึงข้อความจาก PNG** เพียงแค่การป้อนชื่อไฟล์ที่ถูกต้องเข้าไปในคิว

![How to batch OCR workflow](https://example.com/placeholder.png "Diagram illustrating how to batch OCR a collection of PNG files")
*ข้อความภาพ: แผนผังการทำ OCR เป็นชุด*

## C# OCR tutorial – ตั้งค่าคิวการจดจำ

หัวใจของการทำงานเป็นชุดคือ `RecognitionQueue` คิดว่าเป็นสายพานที่ส่งแต่ละภาพไปยัง `OcrEngine` ร่วมกัน การแชร์เอนจินทำให้ใช้หน่วยความจำน้อยลงและรับประกันว่าการตั้งค่าเหมือนกันทุกหน้า

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

ทำไมต้องตั้งค่า `MaxDegreeOfParallelism` เป็น 4? บนแล็ปท็อปคอร์ดสี่คอร์ทั่วไป จะให้อัตราการประมวลผลที่ดีที่สุดโดยไม่ทำให้ระบบปฏิบัติการขาดแคลนทรัพยากร หากคุณรันบนเซิร์ฟเวอร์ที่มีคอร์มากกว่า สามารถเพิ่มจำนวนได้ตามต้องการ

### เคล็ดลับพิเศษ

หากต้องการแพ็คภาษาที่กำหนดเอง, การตั้งค่า DPI, หรือการครอปส่วนที่สนใจ ให้ทำ **ครั้งเดียว** บน `Engine` ร่วมก่อนที่จะใส่ภาพลงคิว ตัวอย่าง:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

การจดจำต่อ ๆ ไปจะสืบทอดตัวเลือกเหล่านี้โดยอัตโนมัติ—นี่คือแก่นของ **วิธีสร้าง OCR** pipeline ที่คงที่

## การดึงข้อความเป็นชุด – ใส่ภาพลงคิวและรันคิว

เมื่อคิวพร้อม ขั้นตอนต่อไปคือการใส่แต่ละภาพลงในคิว วิธี `Enqueue` รับออบเจกต์ `OcrImage` ซึ่งเราจะสร้างจากพาธไฟล์

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

เมื่อทุกไฟล์ถูกใส่คิวแล้ว เราก็สั่งให้เริ่มประมวลผล:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` จะบล็อกจนกว่าทุกรูปภาพจะเสร็จ แล้วคืนรายการที่แต่ละองค์ประกอบสอดคล้องกับลำดับอินพุต ซึ่งรับประกันว่าผลลัพธ์ของหน้า 1 อยู่ที่ตำแหน่ง 0, หน้า 2 ที่ตำแหน่ง 1 ฯลฯ—สะดวกเมื่อคุณต้องแมปผลลัพธ์กลับไปยังไฟล์ต้นฉบับ

## วิธีสร้าง OCR – แสดงผลลัพธ์

สุดท้าย ให้พิมพ์ข้อความที่จดจำได้ลงคอนโซล ที่นี่คุณจะเห็น **การดึงข้อความเป็นชุด** ทำงานจริง

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

เมื่อคุณรันโปรแกรม (`dotnet run`) ควรเห็นอะไรประมาณนี้:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

หากภาพใดภาพหนึ่งล้มเหลว (เช่น ไฟล์เสีย) `OcrResult` ที่สอดคล้องจะมี `Text` ว่างเปล่าและคุณสามารถตรวจสอบ `ocrResults[i].Exception` เพื่อดูสาเหตุได้

## วิธีสร้าง OCR – เคล็ดลับ, กรณีขอบ, และแนวปฏิบัติที่ดีที่สุด

### จัดการชุดงานขนาดใหญ่

การประมวลผลหลายร้อย PNG ยังอาจกินหน่วยความจำได้หากเก็บออบเจกต์ `OcrResult` ทั้งหมดไว้ในหน่วยความจำ ในกรณีเช่นนี้ ให้สตรีมผลลัพธ์ไปยังไฟล์หรือฐานข้อมูลทันทีที่แต่ละผลลัพธ์มาถึง:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### รองรับรูปแบบที่ไม่ใช่ PNG

Aspose OCR ยังรองรับ JPEG, BMP, และ TIFF โดยตรง เพียงเปลี่ยนนามสกุลไฟล์ในรายการหรือใช้การค้นหาแบบไวล์การ์ด ขั้นตอน **c# ocr tutorial** ยังคงเหมือนเดิม—ไม่ต้องแก้โค้ด

### ข้ามหน้าว่าง

หากคุณมี PDF สแกนที่บางครั้งมีหน้าว่าง คุณสามารถกรองผลลัพธ์ได้:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### พิจารณาเรื่องใบอนุญาต

เวอร์ชันประเมินผลจะใส่ลายน้ำบนแต่ละหน้า สำหรับการใช้งานจริง อย่าลืมฝังไฟล์ใบอนุญาตของคุณที่จุดเริ่มต้นของ `Main`:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### ปรับจูนระดับขนาน

ค่าเริ่มต้นของ `MaxDegreeOfParallelism` คือ `Environment.ProcessorCount` หากคุณสังเกตการใช้ CPU สูงหรือความดันหน่วยความจำ ให้ลดค่าลง ในทางกลับกัน หากรันบน VM คลาวด์ที่มีคอร์หลาย ๆ ตัว ให้เพิ่มค่าเพื่อใช้ประโยชน์จากฮาร์ดแวร์เต็มที่

## สรุป

คุณมีโซลูชัน **วิธีทำ OCR เป็นชุด** ใน C# ที่สามารถ **ดึงข้อความจาก PNG** ไฟล์ได้ ทำงานแบบขนานและให้ผลลัพธ์ที่เรียงลำดับอย่างชัดเจน ด้วยการแชร์ `OcrEngine` เพียงตัวเดียว คุณได้เรียนรู้ **วิธีสร้าง OCR** pipeline ที่ประหยัดหน่วยความจำและดูแลรักษาง่าย คู่มือ **c# ocr tutorial** นี้ยังแสดงวิธีขยายเป็น **การดึงข้อความเป็นชุด** สำหรับหลายร้อยภาพด้วยเพียงไม่กี่บรรทัดเพิ่ม

---

### ขั้นตอนต่อไปคืออะไร?

* ลองเพิ่มการตรวจจับภาษา (`Engine.Language = Language.AutoDetect`)  
* ทดลองบันทึกผลลัพธ์เป็น JSON หรือ CSV เพื่อการวิเคราะห์ต่อไป  
* ผสานการทำ OCR แบบชุดนี้กับขั้นตอนแปลง PDF‑to‑image เพื่อประมวลผลเอกสารสแกนทั้งหมด  

คุณสามารถปรับระดับขนาน, เปลี่ยนแหล่งภาพของคุณเอง, หรือเชื่อมผลลัพธ์เข้ากับดัชนีการค้นหาได้ตามต้องการ ท้องฟ้าเป็นขอบเขตเมื่อคุณเชี่ยวชาญ **วิธีทำ OCR เป็นชุด** ใน C#

ขอให้เขียนโค้ดอย่างสนุกและ OCR ของคุณทำงานเร็วและปราศจากข้อผิดพลาด!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}