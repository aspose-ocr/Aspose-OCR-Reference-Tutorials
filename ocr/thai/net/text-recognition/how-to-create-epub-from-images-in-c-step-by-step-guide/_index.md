---
category: general
date: 2026-03-07
description: วิธีสร้าง ePub จากภาพสแกนโดยใช้ Aspose OCR – เรียนรู้การแปลงภาพเป็น ePub,
  การดึงข้อความจากภาพ, การเพิ่มผู้เขียนลงใน ePub, และการโหลดภาพสำหรับ OCR.
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: th
og_description: วิธีสร้าง ePub จากภาพสแกนใน C# บทเรียนนี้จะแสดงวิธีแปลงภาพเป็น ePub,
  ดึงข้อความจากภาพ, เพิ่มผู้เขียนลงใน ePub, และโหลดภาพเพื่อทำ OCR.
og_title: วิธีสร้าง ePub จากรูปภาพด้วย C# – คู่มือฉบับสมบูรณ์
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: วิธีสร้าง ePub จากรูปภาพใน C# – คู่มือขั้นตอนต่อขั้นตอน
url: /th/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีสร้าง ePub จากรูปภาพใน C# – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **how to create ePub** จากชุดของหน้าที่สแกน?  บางทีคุณอาจมี PNG จำนวนไม่กี่ไฟล์ของนวนิยายคลาสสิกและต้องการแปลงให้เป็น ePub ที่เรียบร้อยซึ่งสามารถอ่านได้บนอุปกรณ์ใดก็ได้ ข่าวดีคือด้วย Aspose OCR คุณสามารถ **load image for OCR**, ดึงข้อความออกมา, แล้ว **convert image to ePub** เพียงไม่กี่บรรทัดของ C#.

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: โหลดรูปภาพ, ดึงข้อความ, เติม metadata บางส่วน (ใช่, เราจะ **add author to epub**), และสุดท้ายเขียนไฟล์ ePub ที่เป็นไปตามมาตรฐาน. เมื่อเสร็จคุณจะมี ePub พร้อมเผยแพร่และเข้าใจแต่ละขั้นตอนอย่างชัดเจน, เพื่อให้คุณสามารถปรับโค้ดสำหรับหนังสือหลายหน้า, ฟอนต์กำหนดเอง, หรือแม้กระทั่งการแจกจ่ายแบบไม่มี DRM.

## สิ่งที่คุณต้องเตรียม

- **.NET 6** หรือใหม่กว่า (API ทำงานกับ .NET Standard 2.0+ ด้วย)  
- **Aspose.OCR for .NET** – คุณสามารถดาวน์โหลดเวอร์ชันทดลองฟรีจากเว็บไซต์ของ Aspose.  
- ภาพสแกนเช่น `book_page.png` ที่จัดเก็บไว้ที่ใดที่หนึ่งบนดิสก์.  
- IDE ที่คุณชื่นชอบ (Visual Studio, Rider, หรือ VS Code – ฉันจะใช้ Visual Studio ในภาพหน้าจอ).

ไม่จำเป็นต้องติดตั้งแพ็คเกจ NuGet เพิ่มเติม; Aspose.OCR มีทุกอย่างที่คุณต้องการสำหรับการส่งออก ePub อยู่ในตัว.

---

![วิธีสร้าง ePub จากภาพสแกน](/images/how-to-create-epub.png "วิธีสร้าง ePub จากภาพสแกนโดยใช้ Aspose OCR")

## ขั้นตอนที่ 1 – ตั้งค่าโปรเจกต์และติดตั้ง Aspose.OCR

เริ่มต้นกันก่อน. สร้างแอปคอนโซลใหม่:

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

เพิ่มแพคเกจ Aspose.OCR:

```bash
dotnet add package Aspose.OCR
```

เท่านี้ – ไลบรารีมาพร้อมกับความสามารถ OCR และการส่งออก ePub, ดังนั้นคุณจะไม่ต้องการ dependencies เพิ่มเติม.

## ขั้นตอนที่ 2 – Load Image for OCR

ก่อนที่เราจะ **extract text from image**, เราต้องให้เครื่อง OCR มีสิ่งที่อ่าน. ตัวช่วย `ImageStream.FromFile` ทำให้เรื่องนี้ง่ายมาก:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **Pro tip:** หากภาพของคุณอยู่ใน resource ที่ฝังไว้, ให้ใช้ `ImageStream.FromResource` แทน `FromFile`.

## ขั้นตอนที่ 3 – Extract Text from Image

ตอนนี้เครื่องจะอ่านพิกเซลและแปลงเป็นสตริง Unicode. เมธอด `Recognize` ทำงานหนักส่วนนี้.

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

ทำไมต้องเรียก `Recognize` แยกออก? มันทำให้คุณตรวจสอบผลลัพธ์ OCR ดิบ, ปรับตั้งค่าภาษา, หรือแม้กระทั่งทำการตรวจสอบการสะกดก่อนที่จะไปสู่การสร้าง ePub.

## ขั้นตอนที่ 4 – Prepare ePub Export Options (Add Author to ePub)

การสร้าง ePub ที่เรียบร้อยไม่ใช่แค่การใส่ข้อความ; คุณยังต้องการ metadata ที่เหมาะสม. คลาส `EpubExportOptions` ให้วิธีที่สะอาดในการ **add author to epub**, ตั้งชื่อเรื่อง, และกำหนดว่าจะฝังภาพต้นฉบับหรือไม่.

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

หากคุณมีหลายหน้า, คุณสามารถเรียก `ocrEngine.Image = …` และ `ocrEngine.Recognize()` ภายในลูปต่อเนื่อง; ทุกการเรียกจะเพิ่มเนื้อหาของหน้าที่ใหม่ลงในเอกสาร ePub เดียวกัน.

## ขั้นตอนที่ 5 – Convert Image to ePub and Export

เมื่อดึงข้อความและตั้งค่า metadata แล้ว, ขั้นตอนสุดท้ายคือบรรทัดเดียวที่เขียนไฟล์ ePub ลงดิสก์:

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

ไฟล์ `book.epub` ที่ได้สามารถเปิดใน Calibre, Apple Books, หรือโปรแกรมอ่าน EPUB ใดก็ได้. เนื่องจากเราตั้งค่า `IncludeImages = true`, PNG ต้นฉบับจะปรากฏเป็นหน้าภาพ, รักษาลักษณะของแหล่งสแกน.

## ตัวอย่างการทำงานเต็มรูปแบบ

เมื่อนำทั้งหมดมารวมกัน, นี่คือโปรแกรมที่สมบูรณ์พร้อมรัน:

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

เปิด `book.epub` ในโปรแกรมอ่านที่คุณชื่นชอบและคุณจะเห็นหน้าปก, บรรทัดผู้เขียน (แม้จะเป็น “Unknown”), และภาพสแกนที่แสดงพร้อมกับข้อความที่สามารถเลือกได้.

## คำถามทั่วไปและกรณีขอบ

### ถ้าภาษา OCR ไม่ใช่ภาษาอังกฤษ?

Aspose.OCR รองรับมากกว่า 70 ภาษา. เพียงตั้งค่า property `Language` ก่อนเรียก `Recognize`:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### จะจัดการหนังสือหลายหน้าอย่างไร?

ห่อหุ้มตรรกะการโหลด/การจดจำในลูป `foreach`:

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

แต่ละรอบจะเพิ่มข้อความที่จดจำใหม่ลงใน ePub เดียวกัน, รักษาลำดับหน้า.

### ฉันสามารถยกเว้นภาพต้นฉบับได้หรือไม่?

ได้ – ตั้งค่า `IncludeImages = false` ใน `EpubExportOptions`. ePub ที่ได้จะเป็นข้อความที่ไหลได้อย่างเดียว, ซึ่งทำให้ขนาดไฟล์ลดลงอย่างมาก.

### แล้วฟอนต์หรือสไตล์ที่กำหนดเองล่ะ?

ตัวส่งออก ePub ของ Aspose.OCR ให้คุณระบุไฟล์สไตล์ CSS ผ่าน property `Css` ของ `EpubExportOptions`. วิธีนี้คุณสามารถบังคับใช้ฟอนต์ที่กำหนด, ความสูงบรรทัด, หรือระยะขอบ.

## สรุป

ตอนนี้คุณรู้ **how to create ePub** จากภาพสแกนโดยใช้ Aspose OCR ใน C# แล้ว. บทแนะนำครอบคลุมทุกอย่างตั้งแต่ **load image for OCR**, ผ่าน **extract text from image**, ไปจนถึง **add author to epub**, และสุดท้าย **convert image to epub** ด้วยการเรียกส่งออกครั้งเดียว. ด้วยตัวอย่างโค้ดเต็มคุณสามารถขยายโซลูชันเพื่อประมวลผลหลายไฟล์ในชุด, ใส่ภาพปกที่กำหนดเอง, หรือแม้กระทั่งรวม workflow นี้เข้าใน Web API.

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองแปลง PDF เป็น ePub, หรือทดลองปรับค่าเกณฑ์ความเชื่อมั่นของ OCR เพื่อเพิ่มความแม่นยำบนสแกนที่มีเสียงรบกวน. ไม่มีขีดจำกัดเมื่อคุณผสาน OCR ที่ทรงพลังกับการสร้าง ePub ที่ยืดหยุ่น.

ขอให้เขียนโค้ดอย่างสนุกสนาน, และเพลิดเพลินกับการอ่าน ePub ที่คุณสร้างใหม่!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}