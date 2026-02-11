---
category: general
date: 2026-02-11
description: สร้าง PDF ที่ค้นหาได้จากภาพภาษาอาหรับใน C# เรียนรู้วิธีแปลงภาพเป็น PDF,
  ดึงข้อความภาษาอาหรับ, และเพิ่มข้อความที่ซ่อนอยู่โดยใช้ Aspose OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract arabic text
- pdf with hidden text
- ocr arabic image
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพภาษาอาหรับโดยใช้ Aspose OCR ใน C# ทำตามคำแนะนำนี้เพื่อแปลงภาพเป็น
  PDF, ดึงข้อความภาษาอาหรับ, และฝังข้อความที่ซ่อนอยู่.
og_title: สร้าง PDF ที่ค้นหาได้จากภาพอารบิก – ขั้นตอนโดยละเอียด
tags:
- Aspose
- OCR
- PDF
- C#
- Arabic
title: สร้าง PDF ที่ค้นหาได้จากภาพอาหรับ – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/create-searchable-pdf-from-arabic-image-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่สามารถค้นหาได้จากภาพภาษาอาหรับ – คู่มือฉบับสมบูรณ์

เคยต้องการ **สร้าง PDF ที่สามารถค้นหาได้** จากใบแจ้งหนี้ภาษาอาหรับที่สแกนแล้วแต่ไม่แน่ใจว่าจะรักษารูปแบบเดิมไว้ได้อย่างไรในขณะที่ทำให้ข้อความสามารถเลือกได้หรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายโครงการอัตโนมัติเอกสาร ความท้าทายไม่ได้อยู่แค่การแปลงภาพเป็น PDF เท่านั้น แต่ยังต้องคงรูปแบบการแสดงผลและเพิ่มชั้นข้อความที่ซ่อนอยู่ซึ่งเครื่องมือค้นหาสามารถทำดัชนีได้

ในบทแนะนำนี้เราจะเดินผ่านกระบวนการทั้งหมด: **แปลงภาพเป็น PDF**, **สกัดข้อความภาษาอาหรับ** ด้วย Aspose OCR, และสุดท้ายฝังข้อความนั้นเป็น **PDF ที่มีข้อความซ่อน** เพื่อให้ไฟล์ที่ได้สามารถค้นหาได้อย่างเต็มที่ เมื่อเสร็จคุณจะมีโค้ดสแนปช็อต C# ที่พร้อมใช้งานซึ่งสามารถใส่ลงในโซลูชัน .NET ใดก็ได้ ไม่ต้องใช้บริการภายนอก เพียงแค่ไลบรารี Aspose ที่คุณมีอยู่แล้ว

## สิ่งที่คุณต้องการ

- .NET 6 หรือใหม่กว่า (โค้ดนี้ทำงานกับ .NET Core ด้วย)  
- **Aspose.OCR** และ **Aspose.Pdf** NuGet packages (เวอร์ชันล่าสุด ณ กุมภาพันธ์ 2026)  
- ไฟล์ภาพภาษาอาหรับ (เช่น `arabic_invoice.jpg`) ที่คุณต้องการแปลงเป็น PDF ที่สามารถค้นหาได้  
- ความรู้พื้นฐานของ C# – แนวคิดง่ายต่อการเข้าใจ แต่เราจะอธิบาย “ทำไม” ของแต่ละบรรทัด

> **เคล็ดลับ:** หากคุณยังไม่ได้เพิ่ม NuGet packages ให้รัน  
> `dotnet add package Aspose.OCR` และ  
> `dotnet add package Aspose.Pdf` จากโฟลเดอร์โปรเจกต์ของคุณ

ตอนนี้เมื่อเงื่อนไขเบื้องต้นเรียบร้อยแล้ว เรามาเริ่มต้นการทำงานแบบขั้นตอนต่อขั้นตอนกันเลย

## Step 1 – Set Up the OCR Engine for Arabic Text

สิ่งแรกที่เราต้องทำคือกำหนดค่า Aspose OCR ให้รับรู้ตัวอักษรภาษาอาหรับ ภาษาอาหรับเป็นสคริปต์จากขวาไปซ้าย ดังนั้นเราต้องบอกเครื่องมือว่าต้องโหลดภาษาใดและเปิดการดาวน์โหลดทรัพยากรอัตโนมัติในกรณีที่ข้อมูลภาษายังไม่มีบนเครื่อง

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Configure OCR for Arabic and let Aspose fetch the language pack if needed
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Arabic,
    AutomaticResourceDownload = true
};
```

**ทำไมจึงสำคัญ:**  
หากคุณละเว้นการตั้งค่า `Language = OcrLanguage.Arabic` เครื่องมือจะใช้ค่าเริ่มต้นเป็นภาษาอังกฤษและคุณจะได้อักขระที่อ่านไม่ออก การเปิด `AutomaticResourceDownload` จะช่วยคุณไม่ต้องวางไฟล์ภาษาเองบนเซิร์ฟเวอร์

## Step 2 – Load the Source Image

ต่อไปเราจะโหลดภาพที่มีข้อความภาษาอาหรับ การใช้ `Image.FromFile` ทำให้ภาพถูกอ่านเข้าสู่วัตถุ GDI+ `Image` ซึ่ง Aspose OCR คาดหวัง

```csharp
using System.Drawing;          // For Image
using System.IO;                // For MemoryStream

// Replace with the actual path to your Arabic invoice
string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";

using (var inputImage = Image.FromFile(imagePath))
{
    // The rest of the workflow lives inside this using block
```

**กรณีขอบ:** หากภาพมีขนาดใหญ่มาก (เช่น หน้า A3 ที่สแกน) ควรลดขนาดลงก่อนเพื่อปรับปรุงประสิทธิภาพ เครื่องมือ OCR สามารถจัดการไฟล์ขนาดใหญ่ได้ แต่การใช้หน่วยความจำจะพุ่งสูงอย่างรวดเร็ว

## Step 3 – Recognize Arabic Text and Capture the Result

ตอนนี้เราจะเรียกใช้ OCR จริง ๆ เมธอด `Recognize` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่บรรจุข้อความที่ตรวจพบ, คะแนนความเชื่อมั่น, และกล่องขอบเขต (หากคุณต้องการใช้สำหรับการวิเคราะห์เลย์เอาต์ขั้นสูง)

```csharp
    // Perform OCR on the loaded image
    OcrResult ocrResult = ocrEngine.Recognize(inputImage);
    string extractedText = ocrResult.Text;

    // Quick sanity check: print the first 200 characters to the console
    Console.WriteLine("Extracted Arabic text (preview):");
    Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**ทำไมต้องดูตัวอย่าง:**  
การเห็นส่วนหนึ่งของข้อความที่สกัดออกมาช่วยให้คุณตรวจสอบว่าชุดภาษาถูกโหลดอย่างถูกต้องก่อนที่คุณจะเสียเวลาในการสร้าง PDF

## Step 4 – Create a New PDF Document and Add a Blank Page

เมื่อมีข้อความในมือแล้ว เราก็สามารถเริ่มสร้าง PDF ได้ Aspose PDF ให้วัตถุ `Document` ที่เป็นตัวแทนของไฟล์ทั้งหมด การเพิ่มหน้าใหม่ทำให้เรามีพื้นที่วางทั้งภาพต้นฉบับและชั้นข้อความซ่อน

```csharp
    // Initialize a new PDF document
    var pdfDocument = new Aspose.Pdf.Document();

    // Add a blank page – this will become the background for our image
    var pdfPage = pdfDocument.Pages.Add();
```

**หมายเหตุ:** คุณสามารถเพิ่มหลายหน้าได้หากกำลังประมวลผล TIFF หรือ PDF แบบหลายหน้า แต่สำหรับกรณีภาพเดี่ยวหนึ่งหน้าก็เพียงพอ

## Step 5 – Insert the Original Image as a Background Element

เราต้องการให้ PDF สุดท้ายดูเหมือนใบแจ้งหนี้ที่สแกนไว้อย่างแม่นยำ ดังนั้นจึงฝังภาพเป็นพื้นหลังที่มองเห็นได้ คลาส `Image` ของ Aspose PDF ต้องการสตรีม ดังนั้นเราจะอ่านไฟล์เข้าสู่ `MemoryStream`

```csharp
    // Load the same image bytes for the PDF background
    var backgroundImage = new Aspose.Pdf.Image
    {
        ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
    };

    // Add the image to the page's paragraph collection
    pdfPage.Paragraphs.Add(backgroundImage);
```

**ทำไมต้องใช้ภาพพื้นหลัง?**  
การวางภาพโดยตรงบนหน้าช่วยคงเลย์เอาต์เดิม, สี, และตราประทับหรือโลโก้ใด ๆ ที่เครื่องมือ OCR อาจมองข้าม

## Step 6 – Add the OCR Text as a Hidden Layer

สูตรลับสำหรับ **PDF ที่สามารถค้นหาได้** คือชั้นข้อความซ่อนที่วางอยู่บนภาพ โดยตั้งค่าขนาดฟอนต์เป็น `0` เราจะทำให้ข้อความมองไม่เห็นต่อสายตามนุษย์ แต่ยังคงเลือกและค้นหาได้

```csharp
    // Create a TextFragment with the extracted Arabic text
    var searchableText = new Aspose.Pdf.Text.TextFragment(extractedText)
    {
        // Hide the visible text; only the text layer remains searchable
        TextState = { FontSize = 0 }
    };

    // Add the hidden text fragment to the same page
    pdfPage.Paragraphs.Add(searchableText);
```

**รายละเอียดสำคัญ:**  
หากคุณต้องการให้ข้อความซ่อนจัดตำแหน่งตรงกับภาพอย่างสมบูรณ์ (เช่น OCR คืนค่าพิกัด) คุณสามารถใช้ `TextFragmentAbsorber` แล้วกำหนดตำแหน่งของแต่ละ fragment ด้วยตนเอง สำหรับใบแจ้งหนี้ส่วนใหญ่การวางทับเต็มหน้าแบบง่ายก็เพียงพอ

## Step 7 – Save the Searchable PDF

สุดท้ายเราจะบันทึก PDF ลงดิสก์ ไฟล์ผลลัพธ์จะบรรจุทั้งภาพที่มองเห็นและข้อความอาหรับที่ซ่อนอยู่ ทำให้สามารถค้นหาได้เต็มที่ใน Adobe Reader, Google Drive หรือโปรแกรมดู PDF ที่รองรับ OCR

```csharp
    // Define the output path
    string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";

    // Save the document
    pdfDocument.Save(outputPath);

    Console.WriteLine($"Searchable PDF created at: {outputPath}");
}
```

### Full Working Example

รวมส่วนต่าง ๆ เข้าด้วยกัน นี่คือโปรแกรมที่พร้อมรันเต็มรูปแบบ:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR for Arabic
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Arabic,
            AutomaticResourceDownload = true
        };

        // 2️⃣ Load the source image
        string imagePath = @"YOUR_DIRECTORY/arabic_invoice.jpg";
        using (var inputImage = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR and get the text
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);
            string extractedText = ocrResult.Text;

            // Optional preview
            Console.WriteLine("Extracted Arabic text (preview):");
            Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));

            // 4️⃣ Create PDF document
            var pdfDocument = new Document();
            var pdfPage = pdfDocument.Pages.Add();

            // 5️⃣ Add original image as background
            var backgroundImage = new Aspose.Pdf.Image
            {
                ImageStream = new MemoryStream(File.ReadAllBytes(imagePath))
            };
            pdfPage.Paragraphs.Add(backgroundImage);

            // 6️⃣ Add hidden searchable text
            var searchableText = new TextFragment(extractedText)
            {
                TextState = { FontSize = 0 }
            };
            pdfPage.Paragraphs.Add(searchableText);

            // 7️⃣ Save the searchable PDF
            string outputPath = @"YOUR_DIRECTORY/arabic_invoice_searchable.pdf";
            pdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** เปิดไฟล์ `arabic_invoice_searchable.pdf` ที่สร้างขึ้นในโปรแกรมดู PDF ใดก็ได้ กด **Ctrl + F** แล้วพิมพ์คำภาษาอาหรับที่ปรากฏบนใบแจ้งหนี้ต้นฉบับ โปรแกรมดูควรเจอคำนั้นแม้ว่าคุณจะไม่เห็นชั้นข้อความใด ๆ

## Common Questions & Gotchas

- **ทำงานกับภาษาอื่นได้หรือไม่?**  
  แน่นอน เพียงเปลี่ยน `Language = OcrLanguage.YourLanguage` และตรวจสอบให้แน่ใจว่าชุดภาษานั้นพร้อมใช้งาน ส่วนที่เหลือของกระบวนการยังคงเหมือนเดิม

- **ถ้าความเชื่อมั่นของ OCR ต่ำล่ะ?**  
  คุณสามารถตรวจสอบ `ocrResult.Confidence` (ค่าระหว่าง 0 ถึง 1) หากค่าต่ำกว่าขีดจำกัด (เช่น 0.75) ให้พิจารณาเตรียมภาพล่วงหน้า – แก้ไขการเอียง, เพิ่มคอนทราสต์, หรือแปลงเป็นระดับสีเทา – ก่อนส่งให้เครื่องมือ

- **สามารถใส่หลายภาพใน PDF หนึ่งไฟล์ได้หรือไม่?**  
  ได้ คุณเพียงวนลูปผ่านคอลเลกชันของเส้นทางภาพ, เพิ่มหน้าใหม่สำหรับแต่ละภาพ, แล้วทำซ้ำขั้นตอน 5‑6 อย่าลืมรักษา `using` block สำหรับแต่ละภาพเพื่อปล่อยทรัพยากร GDI

- **ข้อความซ่อนจริง ๆ แล้วมองไม่เห็นหรือ?**  
  การตั้งค่า `FontSize = 0` ทำให้ข้อความมองไม่เห็นในโปรแกรมส่วนใหญ่ หากโปรแกรมยังแสดง glyph ที่บอบบาง คุณสามารถตั้งค่าสีข้อความให้โปร่งใสเต็ม (`TextState.FillColor = Color.Transparent`) ได้เช่นกัน

## Next Steps

ตอนนี้คุณรู้วิธี **สร้าง PDF ที่สามารถค้นหาได้** จากภาพภาษาอาหรับแล้ว อาจอยากสำรวจต่อไป:

- **การประมวลผลเป็นชุด** – อ่านภาพทั้งหมดในโฟลเดอร์และสร้าง PDF ที่สามารถค้นหาได้หนึ่งไฟล์ต่อภาพ  
- **การเพิ่มพิกัด OCR** – ใช้ `OcrResult.Regions` เพื่อวางแต่ละ fragment ของข้อความตรงตำแหน่งที่ปรากฏจริง ๆ เพิ่มความแม่นยำในการค้นหาสำหรับเลย์เอาต์ที่ซับซ้อน  
- **การเข้ารหัส PDF** – Aspose PDF ให้คุณเพิ่มรหัสผ่านหรือลายเซ็นดิจิทัลหากต้องการความปลอดภัยเพิ่มขึ้น  
- **การเชื่อมต่อกับ Azure Blob Storage** – เก็บ PDF ที่สร้างขึ้นโดยตรงในคลาวด์เพื่อใช้ในกระบวนการต่อไป

แต่ละหัวข้อเหล่านี้โดยธรรมชาติจะเกี่ยวข้องกับคีย์เวิร์ดรอง **convert image to pdf**, **extract

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}