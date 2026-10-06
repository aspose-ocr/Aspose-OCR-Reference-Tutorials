---
category: general
date: 2026-02-22
description: สร้าง PDF ที่ค้นหาได้และดึงข้อความจากภาพด้วย Aspose OCR. เรียนรู้วิธีแปลงภาพเป็น
  PDF และแสดงข้อความธรรมดาในบทเรียนเดียว.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: th
og_description: สร้าง PDF ที่ค้นหาได้จากภาพสแกนด้วย Aspose OCR คู่มือนี้แสดงวิธีการดึงข้อความจากภาพ,
  ส่งออกเป็นข้อความธรรมดา, และแปลงภาพเป็น PDF.
og_title: สร้าง PDF ที่ค้นหาได้จากรูปภาพ – บทเรียน C# อย่างครบถ้วน
tags:
- C#
- OCR
- PDF generation
- Aspose
title: สร้าง PDF ที่ค้นหาได้จากรูปภาพใน C# – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สร้าง PDF ที่ค้นหาได้จากรูปภาพใน C# – บทเรียนเต็ม

เคยต้องการ **generate searchable PDF** จากรูปสแกนแต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้อยู่คนเดียว—นักพัฒนาส่วนใหญ่เจออุปสรรคนี้เมื่อต้องทำงานกับ OCR ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถ **extract text from image**, **output plain text**, และ **convert image to PDF** เพียงไม่กี่บรรทัดของ C#.

ในคู่มือนี้ เราจะพาคุณผ่านกระบวนการทั้งหมด ตั้งแต่การโหลดไฟล์ PNG ไปจนถึงการบันทึก PDF ที่ค้นหาได้และไฟล์ข้อความธรรมดา เมื่อเสร็จคุณจะมีโค้ดสั้นที่สามารถนำไปใช้ในโครงการ .NET ใดก็ได้ ไม่มีเนื้อหาเกินความจำเป็น เพียงสิ่งที่ทำให้สำเร็จ

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า **Aspose.OCR** ในแอปคอนโซล .NET.  
- ความแตกต่างระหว่างโหมด **output plain text** และ **searchable PDF**.  
- วิธี **extract text from image** และเขียนลงไฟล์ `.txt`.  
- วิธี **convert image to PDF** ที่รักษาบิตแมปต้นฉบับไว้พร้อมเลเยอร์ข้อความที่ซ่อนอยู่.  
- เคล็ดลับการจัดการแบตช์ขนาดใหญ่, ปัญหาที่พบบ่อย, และจุดที่ควรปรับตั้งค่าเพื่อความแม่นยำที่ดียิ่งขึ้น

> **Prerequisites** – คุณต้องมี .NET 6+ (หรือ .NET Framework 4.7+), Visual Studio 2022 (หรือโปรแกรมแก้ไขใดก็ได้) และใบอนุญาต Aspose OCR (หรือทดลองใช้ฟรี) ไม่จำเป็นต้องใช้ไลบรารีของบุคคลที่สามอื่นใด

![generate searchable pdf example](image-placeholder.png "Example of a generated searchable PDF")

## ขั้นตอนที่ 1: ติดตั้ง Aspose OCR และสร้าง Engine

สิ่งแรกที่ต้องทำ—เพิ่มแพ็กเกจ NuGet ไปยังโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

ตอนนี้เราสามารถสร้าง OCR engine ขึ้นมาและบอกว่าภาษาใดที่ต้องการใช้ ภาษาอังกฤษเป็นค่าเริ่มต้น แต่คุณสามารถเปลี่ยนเป็นภาษาฝรั่งเศส, สเปน ฯลฯ โดยการเปลี่ยนค่า enum `Language`

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Why this matters:** Engine จะเก็บการกำหนดค่าทั้งหมด—ภาษา, รูปแบบผลลัพธ์, และแฟล็กการเตรียมข้อมูลล่วงหน้า (optional preprocessing) การตั้งค่าเพียงครั้งเดียวและนำกลับมาใช้ซ้ำจะช่วยลดภาระการสร้างอินสแตนซ์ใหม่สำหรับแต่ละไฟล์

## ขั้นตอนที่ 2: ดึงข้อความและบันทึกเป็น Plain Text

หากคุณต้องการเพียงอักขระดิบ ให้สลับ engine ไปที่ `OutputFormat.Text` ซึ่งบอก Aspose OCR ให้ข้ามการสร้าง PDF ทั้งหมดและคืนค่าเป็นสตริง

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Pro tip:** `plainTextResult.Text` จะลบการขึ้นบรรทัดใหม่ที่เป็นส่วนของการจัดหน้า OCR ไปแล้ว หากคุณต้องการรักษาการเว้นวรรคเดิม ให้ตรวจสอบ `plainTextResult.TextBlocks` แทน

### ผลลัพธ์ที่คาดหวัง

เปิดไฟล์ `output.txt` คุณควรเห็นข้อความประมาณนี้:

```
Hello, world!
This is a sample scanned document.
```

นี่คือส่วน **output plain text** ของบทเรียน—รวดเร็ว, มีน้ำหนักเบา, และเหมาะสำหรับการประมวลผลต่อ (เช่น การทำดัชนี)

## ขั้นตอนที่ 3: สลับเป็นโหมด Searchable PDF

ตอนนี้เรามาสร้าง **searchable PDF** กัน Engine จะฝังบิตแมปต้นฉบับและวางข้อความที่สร้างโดย OCR ไว้ด้านล่าง ทำให้เอกสารสามารถค้นหาได้ในโปรแกรมอ่าน PDF ใดก็ได้

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Why we re‑recognize:** OCR engine จะเก็บภาพล่าสุดในแคช แต่รูปแบบผลลัพธ์กำหนดว่าข้อมูลใดจะถูกส่งคืน การสลับรูปแบบจะบังคับให้ทำการจดจำใหม่เพื่อรวมเลเยอร์ข้อความที่ซ่อนอยู่

### PDF จะเป็นอย่างไร

เปิดไฟล์ `output.pdf` ด้วย Adobe Reader หรือโปรแกรมอ่านใดก็ได้และลองเลือกข้อความ คุณจะเห็นว่าคุณสามารถคัดลอก, ค้นหา, และไฮไลท์เนื้อหาได้—แม้ว่ารูปแบบภาพจะยังคงเป็นบิตแมปต้นฉบับ นั่นคือลักษณะสำคัญของ **convert scanned image pdf**

## ขั้นตอนที่ 4: จัดการหลายไฟล์ (ทางเลือก)

ในโครงการจริงมักไม่ใช่แค่ภาพเดียว ด้านล่างเป็นลูปสั้นที่ประมวลผลไฟล์ PNG ทุกไฟล์ในโฟลเดอร์และสร้างไฟล์ `.txt` และ `.pdf` ที่ตรงกัน

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Edge case note:** ภาพขนาดใหญ่อาจทำให้หน่วยความจำหมด หากเกิด `OutOfMemoryException` ให้พิจารณาลดขนาดด้วย `Image.Resize` ก่อนทำการจดจำ หรือประมวลผลไฟล์เป็นชุดเล็ก ๆ

## ขั้นตอนที่ 5: ปรับแต่งความแม่นยำของ OCR

Aspose OCR มีตัวเลือกบางอย่างที่คุณสามารถปรับได้:

| Setting | What it does | When to use |
|---------|--------------|-------------|
| `ocrEngine.PageSegmentationMode` | ควบคุมวิธีที่ engine แบ่งภาพเป็นบล็อกข้อความ | มีประโยชน์สำหรับเลย์เอาต์หลายคอลัมน์ |
| `ocrEngine.Deskew` | หมุนอัตโนมัติสำหรับหน้าที่เอียงเล็กน้อย | เอกสารสแกนที่ไม่ได้จัดแนวอย่างสมบูรณ์ |
| `ocrEngine.RemoveNoise` | พยายามทำความสะอาดจุดรบกวนและศิลปะพื้นหลัง | สแกนคุณภาพต่ำหรือหน้าที่ส่งแฟกซ์ |

Example:

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

การเปิดใช้งานตัวเลือกเหล่านี้อาจทำให้เวลาในการประมวลผลเพิ่มขึ้น แต่การปรับปรุงคุณภาพของ **extract text from image** มักคุ้มค่า

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์โดยโปรแกรม

บางครั้งคุณต้องการยืนยันว่า PDF มีข้อความที่ค้นหาได้จริง (เช่น ในการทดสอบอัตโนมัติ) วิธีตรวจสอบง่ายที่สุดคือยืนยันว่าอาเรย์ไบต์ของ PDF ไม่ว่างเปล่าและความยาวของ `RawData` มากกว่าขนาดของภาพ

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

สำหรับการตรวจสอบที่ลึกกว่านี้ คุณอาจใช้ไลบรารี PDF (เช่น iTextSharp) เพื่อดึงสตรีมข้อความและเปรียบเทียบกับ `plainTextResult.Text`

## ข้อผิดพลาดทั่วไป & วิธีหลีกเลี่ยง

- **Missing License** – หากไม่มีใบอนุญาต Aspose ที่ถูกต้อง ไลบรารีจะทำงานในโหมดประเมินผลและใส่ลายน้ำบน PDF ลงทะเบียนใบอนุญาตตั้งแต่ต้น (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Incorrect Path** – การกำหนดเส้นทางแบบ absolute อย่างตายตัวอาจทำงานบนเครื่องของคุณแต่ล้มเหลวที่อื่น ใช้ `Path.Combine` กับ `AppDomain.CurrentDomain.BaseDirectory` เพื่อความพกพา.  
- **Unsupported Image Formats** – GIF และ TIFF ที่มีหลายเฟรมต้องการการจัดการพิเศษ (`Image.LoadMultiPage`). แปลงเป็น PNG/JPEG ก่อนหากคุณต้องการเฉพาะหน้าแรก.  
- **Performance Bottlenecks** – การสร้าง `OcrEngine` ซ้ำภายในลูปทำให้เสียเวลา เก็บอินสแตนซ์เดียวและเปลี่ยน `OutputFormat` ตามที่แสดง.

## สรุป

เราได้อธิบายขั้นตอนทั้งหมดเพื่อ **generate searchable PDF** จากภาพสแกนโดยใช้ Aspose OCR:

1. ติดตั้งแพ็กเกจ NuGet และสร้าง `OcrEngine`.  
2. ตั้งค่า `OutputFormat.Text` เพื่อ **output plain text** และเขียนลงไฟล์ `.txt`.  
3. สลับเป็น `OutputFormat.SearchablePdf` เพื่อ **convert image to PDF** พร้อมเลเยอร์ข้อความที่มองไม่เห็น.  
4. บันทึกไบต์ของ PDF และหากต้องการสามารถวนลูปผ่านไดเรกทอรีเพื่อประมวลผลแบตช์.  
5. ปรับแต่งความแม่นยำด้วยการตั้งค่า deskew, การลบสัญญาณรบกวน, และตัวเลือกการแบ่งหน้า.

ทั้งหมดนี้สามารถใส่ในโปรแกรมที่กะทัดรัดและอิสระที่คุณสามารถคัดลอกและวางลงใน Visual Studio ได้

## สิ่งที่ควรลองต่อไป?

- **Batch processing** ด้วย UI front‑end (WinForms หรือ WPF) เพื่อให้ผู้ใช้สามารถลากและวางไฟล์ได้.  
- **Language detection** – Aspose OCR สามารถตรวจจับภาษาตามอัตโนมัติ; ลอง `ocrEngine.Language = Language.AutoDetect`.  
- **Post‑processing** – ส่งข้อความที่ดึงมาใส่ในดัชนีการค้นหา (ElasticSearch, Azure Cognitive Search) เพื่อการดึงเอกสารแบบทันที.  
- **Alternative outputs** – ใช้ `OutputFormat.Hocr` สำหรับผลลัพธ์ OCR แบบ HTML ที่เหมาะกับการแสดงตัวอย่างบนเว็บ.

คุณสามารถทดลองกับความละเอียดของภาพ, โหมดสี, และการตั้งค่า OCR ต่าง ๆ ได้ตามต้องการ ยิ่งคุณลองมากเท่าไหร่ คุณจะเข้าใจการแลกเปลี่ยนระหว่างความเร็วและความแม่นยำได้ดียิ่งขึ้น

---

**Happy coding!** หากคุณพบปัญหาใด ๆ โปรดแสดงความคิดเห็นด้านล่างหรือดูเอกสาร Aspose OCR เพื่อศึกษาเพิ่มเติม โครงการต่อไปของคุณ—ไม่ว่าจะเป็นการออกใบแจ้งหนี้, การเก็บถาวร, หรือการสร้างฐานความรู้ที่ค้นหาได้—จะง่ายขึ้นมาก

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}