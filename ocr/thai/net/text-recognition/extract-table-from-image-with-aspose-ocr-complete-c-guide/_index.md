---
category: general
date: 2026-03-18
description: ดึงตารางจากภาพด้วย Aspose OCR ใน C# เรียนรู้วิธีแปลงตารางเป็น JSON, รับ
  JSON ของตารางและดึงข้อความจากภาพได้ในไม่กี่นาที.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: th
og_description: ดึงตารางจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้การแปลงตารางเป็น JSON
  รับ JSON ของตารางและดึงข้อความจากภาพอย่างรวดเร็ว.
og_title: สกัดตารางจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- Table Extraction
title: สกัดตารางจากภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดตารางจากรูปภาพ – คู่มือ C# ฉบับสมบูรณ์

เคยต้องการ **extract table from image** แต่ไม่แน่ใจว่ามีไลบรารีใดที่ทำได้โดยไม่ต้องทำการแยกข้อมูลด้วยมือจำนวนมากหรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการการประมวลผลใบแจ้งหนี้หรือการสแกนใบเสร็จ จุดเจ็บปวดที่แท้จริงคือการแปลงบิตแมพที่มีเสียงรบกวนให้เป็นตารางที่มีโครงสร้างซึ่งระบบต่อไปของคุณสามารถใช้งานได้.  

ข่าวดีคืออะไร? ด้วย Aspose OCR คุณสามารถ **convert table to JSON** ได้ในไม่กี่บรรทัด และคุณยังได้รับข้อความธรรมดาของภาพทั้งหมด ดังนั้น **extract text from image** จึงเป็นโบนัส ในบทแนะนำนี้เราจะเดินผ่านขั้นตอนทั้งหมด – ตั้งแต่การโหลดภาพจนถึงการได้ตัวแทน JSON ที่เรียบร้อยของตารางที่ตรวจจับได้.

> **Quick win:** เมื่อเสร็จคุณจะมีแอปคอนโซล C# ที่สามารถรันได้ซึ่งพิมพ์ทั้งข้อความ OCR ดิบและสตริง JSON ที่คุณสามารถส่งตรงไปยังฐานข้อมูลหรือ API.

## ข้อกำหนดเบื้องต้น

- .NET 6.0 SDK (หรือเวอร์ชัน .NET ล่าสุดใดก็ได้) ที่ติดตั้งแล้ว.  
- ใบอนุญาต Aspose OCR ที่ถูกต้องหรือทดลองใช้ฟรี (ไลบรารีทำงานได้โดยไม่มีใบอนุญาตแต่จะมีลายน้ำ).  
- ภาพที่จริง ๆ มีตาราง – ตัวอย่างเช่น `invoice_table.png`.  
- Visual Studio 2022, VS Code, หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ.

ไม่จำเป็นต้องใช้แพ็กเกจ NuGet เพิ่มเติมนอกจาก `Aspose.OCR`.

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และติดตั้ง Aspose  OCR

แรกเริ่ม สร้างโปรเจกต์คอนโซลใหม่และดึงไลบรารี OCR เข้ามา.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** หากคุณใช้พร็อกซีขององค์กร ให้เพิ่มแฟล็ก `--no-restore` และรัน `dotnet restore` ภายหลังพร้อมกับตัวแปรสภาพแวดล้อมที่เหมาะสม.

## ขั้นตอนที่ 2: เริ่มต้น OCR Engine และเปิดใช้งานการจดจำตาราง

หัวใจของโซลูชันคือ `OcrEngine` โดยการสลับ `EnableTableRecognition` เราบอก Aspose  OCR ให้มองหาโครงสร้างแบบกริดแทนที่จะถือทุกอย่างเป็นข้อความธรรมดา.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

ทำไมขั้นตอนนี้ถึงสำคัญ? หากไม่มีการจดจำตาราง เอนจินจะทำให้ภาพแบนเป็นสตริงเดียว ทำให้ไม่สามารถสร้างแถวและคอลัมน์ใหม่ได้ในภายหลัง การเปิดใช้งานเพิ่มขั้นตอนการวิเคราะห์เลย์เอาต์ที่มีน้ำหนักเบาซึ่งใช้ทรัพยากรเกือบไม่มีแต่ให้ประโยชน์ต่อระบบต่อไปอย่างมหาศาล.

## ขั้นตอนที่ 3: โหลดภาพของคุณและรันการจดจำ

ตอนนี้เราชี้เอนจินไปที่ไฟล์ที่มีตาราง `ImageStream.FromFile` รองรับรูปแบบที่พบบ่อยส่วนใหญ่ (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

หากภาพมีขนาดใหญ่ ควรพิจารณาปรับขนาดก่อนเพื่อเร่งการประมวลผล Aspose  OCR จะตรวจจับ DPI อัตโนมัติ แต่การสแกนที่ 300 DPI เป็นจุดที่เหมาะสมสำหรับตารางส่วนใหญ่.

## ขั้นตอนที่ 4: สกัดข้อความธรรมดา – “extract text from image”

แม้เป้าหมายหลักของเราคือตาราง แต่คุณมักยังต้องการข้อความดิบสำหรับการบันทึกหรือการประมวลผลสำรอง.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

คุณสมบัติ `Text` จะต่อข้อความทั้งหมดที่เอนจินเห็นโดยคงการขึ้นบรรทัดใหม่ไว้ นี่เป็นประโยชน์เมื่อคุณต้องการตรวจสอบว่า OCR อ่านหัวหรือท้ายตารางนอกพื้นที่ตารางได้อย่างถูกต้องหรือไม่.

## ขั้นตอนที่ 5: รับตารางที่ตรวจจับเป็น JSON – “convert table to json” & “get table json”

นี่คือจุดที่เวทมนตร์เกิดขึ้น `GetTableAsJson()` ทำการซีเรียลไลซ์แถว คอลัมน์ และเนื้อหาเซลล์ที่ตรวจจับเป็นสตริง JSON ที่สะอาด.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

JSON ที่ได้จะมีลักษณะประมาณนี้ (จัดรูปแบบเพื่อให้อ่านง่าย):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

ทำไม JSON ถึงเป็นรูปแบบที่นิยม? เพราะเป็นภาษาที่ไม่ขึ้นกับภาษา ง่ายต่อการดีซีเรียลไลซ์เป็นอ็อบเจ็กต์ และทำงานได้ดีกับ API เว็บสมัยใหม่ หากต้องการ CSV แทน เพียงวนลูปผ่านแถวและเชื่อมข้อความเซลล์ด้วยเครื่องหมายคอมม่า.

## ขั้นตอนที่ 6: (ทางเลือก) แปลง JSON เป็นอ็อบเจ็กต์ .NET – “convert image to json”

หากคุณต้องการทำงานกับประเภทที่แข็งแรง ให้ดีซีเรียลไลซ์ JSON ด้วย `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

คุณจะต้องกำหนด `TableModel`, `RowModel`, และ `CellModel` ให้ตรงกับสคีม่า JSON ขั้นตอนนี้แสดงว่าคุณสามารถเดินจาก **convert image to json** ไปจนถึงอ็อบเจ็กต์ที่มีประเภท ทำให้การตรวจสอบต่อไปเป็นเรื่องง่าย.

## ตัวอย่างทำงานเต็มรูปแบบ

เมื่อรวมทุกอย่างเข้าด้วยกัน นี่คือโปรแกรมที่สมบูรณ์พร้อมรัน ให้บันทึกเป็น `Program.cs` ภายในโฟลเดอร์โปรเจกต์ที่สร้างไว้ก่อนหน้า.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรัน `dotnet run` คุณควรเห็นผลลัพธ์ประมาณนี้:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

หากผลลัพธ์ว่างเปล่า ให้ตรวจสอบอีกครั้งว่า `EnableTableRecognition` ถูกตั้งค่าเป็น `true` และภาพมีเส้นกริดที่ชัดเจนจริงหรือไม่.

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ไม่มี JSON คืนค่า** | การตรวจจับตารางถูกปิดหรือภาพมีคอนทราสต์ต่ำเกินไป. | ตรวจสอบให้แน่ใจว่า `ocrEngine.Settings.EnableTableRecognition = true` และปรับปรุงคุณภาพของภาพ (เพิ่มคอนทราสต์, ทำให้เป็นไบนารี). |
| **แถวไม่ครบ** | OCR สับสนกับเซลล์ที่รวมกันหรือข้อความที่หมุน. | ทำการประมวลผลล่วงหน้าภาพ: ปรับแนว (`ImageProcessor.Rotate`) หรือแยกเซลล์ที่รวมกันด้วยตนเอง. |
| **Unicode ผิดพลาด** | แบบอักษรไม่ถูกจดจำ (เช่น ลายมือ). | สลับแพ็คเกจภาษาโดยใช้ `ocrEngine.Language = Language.English;` หรือใช้ OCR engine อื่นสำหรับลายมือ. |
| **ประสิทธิภาพช้า** | ภาพขนาดใหญ่มาก (>5 MP). | ลดขนาดลงประมาณ 1500 px ความกว้างโดยคง DPI. |

## ขั้นตอนต่อไป: ไปไกลกว่าพื้นฐาน

ตอนนี้คุณสามารถ **extract table from image** และ **convert table to JSON** แล้ว ให้พิจารณาการขยายต่อไปนี้:

- **Persist the JSON** ไปยังฐานข้อมูลด้วย Entity Framework.  
- **Post‑process** JSON เพื่อทำให้รูปแบบสกุลเงินเป็นมาตรฐาน (เช่น ลบ `$`).  
- **Batch process** โฟลเดอร์ของใบแจ้งหนี้โดยใช้ `Directory.GetFiles` และทำงานแบบขนานด้วย `Parallel.ForEach`.  
- **Integrate** กับ Azure Functions หรือ AWS Lambda สำหรับพายป์ไลน์ OCR แบบไม่มีเซิร์ฟเวอร์.

แต่ละหัวข้อเหล่านี้จะนำคำหลักรองอื่น ๆ เช่น **convert image to json** (เมื่อคุณส่งผลลัพธ์ OCR ทั้งหมดไปยัง endpoint ของคลาวด์) และ **get table json** สำหรับการวิเคราะห์ต่อไปโดยอัตโนมัติ.

---

### สรุป

เราเพิ่งแสดงให้คุณเห็นวิธี **extract table from image** ด้วย Aspose OCR แปลงตารางนั้นเป็น JSON ที่สะอาด และแม้กระทั่งดีซีเรียลไลซ์เป็นอ็อบเจ็กต์ C# รูปแบบเดียวกัน

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}