---
category: general
date: 2026-05-31
description: ดึงตารางจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีแปลงภาพเป็นตาราง เปิดใช้งานการตรวจจับตาราง
  และแสดงผลลัพธ์อย่างมีประสิทธิภาพ
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: th
og_description: ดึงตารางจากภาพด้วย Aspose OCR. คู่มือนี้แสดงวิธีแปลงภาพเป็นตาราง,
  เปิดใช้งานการตรวจจับตาราง และจัดการผลลัพธ์ใน C#.
og_title: สกัดตารางจากภาพ – คำแนะนำ C# ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: ดึงตารางจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# แยกตารางจากรูปภาพ – คู่มือ C# ฉบับสมบูรณ์

เคยต้อง **แยกตารางจากรูปภาพ** แต่ไม่รู้จะเริ่มต้นอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว; นักพัฒนาจำนวนมากเจออุปสรรคนี้เมื่อต้องแปลงใบแจ้งหนี้หรือใบเสร็จสแกนเป็นข้อมูลที่ใช้ได้ ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถ **แปลงรูปภาพเป็นตาราง** ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C#.

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างจริง: โหลดไฟล์ PNG ที่มีตาราง, แปลงเลย์เอาต์ภาพให้เป็นกริดที่เป็นโครงสร้าง, และพิมพ์เนื้อหาของแต่ละเซลล์พร้อมคะแนนความเชื่อมั่น. เมื่อเสร็จคุณจะได้สแนปช็อตที่ทำงานได้เต็มที่ซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้, พร้อมเคล็ดลับการจัดการกรณีขอบและการขยายขนาดโซลูชัน.

## สิ่งที่คุณต้องมี

ก่อนที่เราจะลงลึก, ตรวจสอบให้แน่ใจว่าคุณมี:

- **.NET 6.0** หรือใหม่กว่า (โค้ดนี้ยังทำงานกับ .NET Framework 4.6+ ด้วย)
- แพคเกจ NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- ไฟล์รูปภาพที่มีตารางจริง ๆ (เช่น `invoice_with_table.png`)
- IDE C# เบื้องต้น (Visual Studio, Rider, หรือ VS Code พร้อมส่วนขยาย C#)

เท่านี้—ไม่มีเครื่องมือ OCR เพิ่มเติม, ไม่มีการพึ่งพาไลบรารีหนัก. พร้อมหรือยัง? ไปเริ่มกันเลย.

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine เพื่อ **แยกตารางจากรูปภาพ**

แรกสุด เราจะสร้างอินสแตนซ์ `OcrEngine` และชี้ไปที่ไฟล์รูปภาพต้นฉบับของเรา. คิดว่า engine นี้เป็นสมองที่จะอ่านทุกพิกเซลและพยายามทำความเข้าใจเลย์เอาต์.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **ทำไมจึงสำคัญ:** หากไม่ได้เริ่มต้น engine อย่างถูกต้อง, OCR engine จะไม่มีอะไรให้วิเคราะห์และคุณจะไม่สามารถดึงตารางออกจากภาพได้. คำสั่ง `ImageStream.FromFile` ยังจัดการกับปัญหารูปแบบทั่วไป (PNG, JPEG, BMP) ทำให้คุณไม่ต้องทำขั้นตอนแปลงเพิ่มเติม.

## ขั้นตอนที่ 2: เปิดใช้งานการตรวจจับตาราง – กุญแจสู่ **แปลงรูปภาพเป็นตาราง**

Aspose OCR สามารถอ่านข้อความธรรมดาจากภาพได้, แต่จะไม่เข้าใจแถวและคอลัมน์โดยอัตโนมัติหากไม่ได้บอกให้มองหาตาราง. ที่นี่ `DetectTables` จะเข้ามามีบทบาท.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **เคล็ดลับ:** หากคุณต้องการเพียงข้อความดิบ, ให้ตั้งค่า `DetectTables` เป็น `false`. การเปิดใช้งานจะเพิ่มภาระงานเล็กน้อย, แต่ผลลัพธ์ที่ได้จะเป็นโครงสร้างที่สะอาดและพร้อมนำเข้า spreadsheet หรือฐานข้อมูลโดยตรง.

## ขั้นตอนที่ 3: ทำการรับรู้ OCR – ช่วงเวลาที่สำคัญ

ต่อไปเราจะสั่งให้ engine อ่านภาพจริง. เมธอด `Recognize` จะคืนค่าอ็อบเจกต์ `OcrResult` ที่บรรจุทั้งข้อความธรรมดาและตารางที่ตรวจพบ.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **เกิดอะไรขึ้นเบื้องหลัง?** Aspose จะดำเนินการขั้นตอนการเตรียมภาพหลายขั้นตอน (deskewing, binarization) ก่อนนำไปใช้กับตัวรับรู้ข้อความแบบ neural‑network. เมื่อ `DetectTables` เป็น true, ระบบจะทำการวิเคราะห์เลย์เอาต์เพื่อจัดกลุ่มอักขระเป็นแถวและคอลัมน์.

## ขั้นตอนที่ 4: วนลูปผ่านตารางที่ตรวจพบ – **แยกตารางจากรูปภาพ** ในการทำงานจริง

หาก engine พบตารางใด ๆ, ตารางเหล่านั้นจะอยู่ใน `result.Tables`. เราจะวนลูปผ่านแต่ละตาราง, จากนั้นแต่ละแถวและคอลัมน์, พิมพ์ข้อความเซลล์และเปอร์เซ็นต์ความเชื่อมั่น.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **ทำไมต้องตรวจสอบความเชื่อมั่น?** OCR ไม่สมบูรณ์โดยเฉพาะกับสแกนที่ความละเอียดต่ำ. ค่า `Confidence` (0‑100) ช่วยให้คุณตัดสินใจว่าจะรับเซลล์นั้นตามที่เป็นหรือจะทำการตรวจสอบด้วยมือ. ค่าเกณฑ์ทั่วไปคือ 80 % สำหรับข้อมูลสำคัญ.

### ผลลัพธ์ที่คาดหวัง

สมมติว่าภาพต้นทางมีตาราง 3 × 4 ของรายการบิล, คุณอาจเห็นผลลัพธ์ประมาณนี้:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

หากไม่พบตารางใดเลย, `result.Tables` จะว่างเปล่า—ไม่มีอะไรพิมพ์, แต่โปรแกรมจะออกอย่างราบรื่น.

## ขั้นตอนที่ 5: การจัดการกรณีขอบและข้อผิดพลาดทั่วไป

### รูปภาพความละเอียดต่ำ

เมื่อรูปภาพต้นทางมีความละเอียดต่ำกว่า 150 dpi, อัลกอริทึมตรวจจับตารางอาจพลาดเส้นขอบเซลล์. วิธีแก้อย่างรวดเร็วคือขยายภาพด้วย `System.Drawing` ก่อนส่งให้ Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### ตารางเอียง

หากตารางหมุนเล็กน้อยหลายองศา, ให้เปิดใช้งาน auto‑deskew:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### หลายตารางในหน้าเดียว

Aspose OCR จะคืนแต่ละตารางเป็นอ็อบเจกต์แยกใน `result.Tables`. คุณสามารถจัดการแยกกัน, หรือรวมเป็น `DataTable` เดียวหากต้องการมุมมองรวม.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### ส่งออกเป็น Excel

เมื่อคุณมี `DataTable`, การส่งออกเป็นไฟล์ `.xlsx` ทำได้ง่ายดายด้วย `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

ตอนนี้คุณได้ **แปลงรูปภาพเป็นตาราง** อย่างแท้จริงและสามารถส่งต่อไฟล์สเปรดชีตให้กระบวนการต่อไปได้.

## ตัวอย่างทำงานเต็มรูปแบบ – ตั้งแต่เริ่มต้นจนจบ

ด้านล่างเป็นโปรแกรมที่พร้อมรันครบชุด. คัดลอกไปวางในโปรเจกต์คอนโซลใหม่, แก้ไขเส้นทางไฟล์, แล้วกด **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**คำอธิบายการทำงาน**

1. **ตั้งค่า Engine** – โหลดภาพและบอก Aspose ให้มองหาตาราง.
2. **ปรับตัวเลือก** – `DetectTables` ทำงานหนัก; `Deskew` ช่วยเพิ่มความแม่นยำบนสแกนที่เอียง.
3. **การรับรู้** – คืนค่าข้อความธรรมดาและคอลเลกชันของอ็อบเจกต์ `Table`.
4. **การวนลูป** – พิมพ์แต่ละเซลล์พร้อมความเชื่อมั่น, พร้อมสร้าง `DataTable` สำหรับการส่งออกต่อไป.
5. **การส่งออก** – ใช้ `ClosedXML` (ไลบรารีเบาไม่มี interop) เขียนไฟล์ `.xlsx`—เหมาะสำหรับการวิเคราะห์หรือรายงานต่อไป.

## คำถามที่พบบ่อย

- **ทำงานกับ PDF ได้หรือไม่?**  
  ใช่. ให้แปลงแต่ละหน้า PDF เป็นภาพก่อน (`PdfRenderer` หรือ `Ghostscript`), แล้วส่งบิตแมปให้ Aspose OCR.

- **สามารถแยกตารางจาก JPG ได้หรือไม่?**  
  แน่นอน. เมธอด `ImageStream.FromFile` รองรับ JPEG, PNG, BMP, และ TIFF ตั้งแต่แรก.

- **ถ้าตารางของฉันมีเซลล์ที่รวมกันล่ะ?**  
  Aspose OCR จะถือเซลล์ที่รวมกันเป็นเซลล์เชิงตรรกะแยกกัน; คุณอาจต้องทำการประมวลผลต่อเพื่อรวมตามความเชื่อมั่นหรือรูปแบบเนื้อหา.

- **มีขีดจำกัดขนาดตารางหรือไม่?**  
  โดยปฏิบัติ, engine รองรับตารางหลายร้อยแถว. ประสิทธิภาพจะลดลงตามจำนวนแถว, ดังนั้นควรแบ่งสแกนขนาดใหญ่ออกเป็นส่วนย่อย.

## สรุป

เราเพิ่งแสดงให้คุณเห็นวิธีการ


## คุณควรเรียนรู้อะไรต่อไป?

- [วิธีแยกตารางจากรูปภาพด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/text-recognition/recognize-table/)
- [แยกข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)
- [วิธีแยกข้อความจากรูปภาพโดยการเตรียมสี่เหลี่ยมใน OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}