---
category: general
date: 2026-04-04
description: เรียนรู้วิธีใช้ Aspose เพื่อดึงข้อมูลใบเสร็จ โหลดภาพใบเสร็จ และทำ OCR
  ภาพใบเสร็จด้วยตัวอย่าง C# ฉบับสมบูรณ์ คู่มือขั้นตอนต่อขั้นตอนสำหรับนักพัฒนา
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: th
og_description: วิธีใช้ Aspose เพื่อดึงข้อมูลใบเสร็จจากภาพใบเสร็จที่สแกน โค้ด C# เต็มรูปแบบ
  คำอธิบาย และเคล็ดลับสำหรับการประมวลผล OCR ของภาพใบเสร็จ
og_title: วิธีใช้ Aspose – ดึงข้อมูลใบเสร็จจากภาพ
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: วิธีใช้ Aspose – ดึงข้อมูลใบเสร็จจากภาพใน C#
url: /th/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose – ดึงข้อมูลใบเสร็จจากรูปภาพใน C#

เคยสงสัย **how to use Aspose** ว่าจะดึงข้อมูลที่มีโครงสร้างออกจากภาพถ่ายของใบเสร็จอย่างไรหรือไม่? คุณไม่ได้เป็นคนเดียว ไม่ว่าคุณจะกำลังสร้างแอปติดตามค่าใช้จ่ายหรือทำระบบอัตโนมัติสำหรับการบันทึกใบแจ้งหนี้ ปัญหาก็เหมือนกัน: คุณมีไฟล์ PNG หรือ JPEG และต้องการชื่อผู้ขาย, วันที่, และยอดรวมโดยไม่ต้องพิมพ์ด้วยมือ.

เรื่องคือ—Aspose.OCR ทำให้กระบวนการทั้งหมดเป็นเรื่องง่าย ในบทแนะนำนี้เราจะอธิบายขั้นตอนการโหลดภาพใบเสร็จ, รัน OCR, และสุดท้ายดึงข้อมูลใบเสร็จด้วยไม่กี่บรรทัดของ C# เมื่อเสร็จคุณจะได้โปรแกรมคอนโซลที่สามารถรันได้ซึ่งจะแสดงชื่อผู้ขาย, วันที่, และยอดรวมโดยตรงบนคอนโซล.

> **Quick win:** หากคุณต้องการโค้ดเท่านั้น ให้ข้ามไปที่ส่วน “Complete Working Example” ด้านล่างและคัดลอก‑วาง.

## สิ่งที่คุณต้องการ

- **.NET 6.0 หรือใหม่กว่า** (API ทำงานกับ .NET Core และ .NET Framework)
- **Aspose.OCR for .NET** NuGet package (`Install-Package Aspose.OCR`)
- ภาพใบเสร็จตัวอย่าง (PNG, JPG, หรือ BMP) ที่บันทึกไว้ในเครื่อง
- Visual Studio 2022 หรือโปรแกรมแก้ไขใด ๆ ที่รองรับโครงการ C#

ไม่จำเป็นต้องใช้ไลบรารีของบุคคลที่สามอื่น ๆ สิ่งที่ต้องมีเพียงความเข้าใจพื้นฐานเกี่ยวกับแอปพลิเคชันคอนโซล C#—ถ้าคุณเคยเขียน “Hello World” ก็พร้อมแล้ว.

## ขั้นตอนที่ 1 – ติดตั้งและอ้างอิง Aspose.OCR

เพื่อ **how to use Aspose**, คุณต้องมีไลบรารีในโครงการของคุณก่อน เปิด Package Manager Console แล้วรัน:

```powershell
Install-Package Aspose.OCR
```

หรือใช้ UI ของ NuGet แล้วค้นหา “Aspose.OCR”. เมื่อติดตั้งแล้ว ให้เพิ่ม namespace ที่จำเป็นที่ส่วนหัวของไฟล์ของคุณ:

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip:** ควรอัปเดตแพ็กเกจ NuGet ของคุณให้เป็นเวอร์ชันล่าสุด ปัจจุบัน (เมษายน 2026) เวอร์ชันเสถียรล่าสุดคือ 23.11.0 ซึ่งรวมการปรับปรุงประสิทธิภาพสำหรับ OCR บนใบเสร็จความละเอียดสูง.

## ขั้นตอนที่ 2 – โหลดภาพใบเสร็จ

เมื่อคุณ **load receipt image** ไฟล์, มีแหล่งที่มาสองแบบทั่วไป: เส้นทางในเครื่องหรือสตรีมจากคำขอเว็บ สำหรับบทแนะนำนี้เราจะทำให้เรียบง่ายและอ่านจากดิสก์:

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

แทนที่ `YOUR_DIRECTORY/receipt.png` ด้วยเส้นทางจริงของไฟล์ใบเสร็จของคุณ หากคุณจัดการกับการอัปโหลดของผู้ใช้ คุณสามารถส่ง `MemoryStream` ไปยัง `ImageStream.FromStream`.

> **Why this matters:** การระบุภาษา (English) จะบอกเครื่องมือ OCR ว่าควรคาดหวังชุดอักขระใด เพื่อลดการรับรู้ผิดพลาด—โดยเฉพาะอย่างยิ่งเมื่อคุณ **ocr receipt image** ที่มีตัวเลขและสัญลักษณ์.

## ขั้นตอนที่ 3 – รัน OCR และจับข้อมูลการจัดวาง

ขั้นตอน OCR ทำมากกว่าการแสดงข้อความดิบ; มันยังจับข้อมูลการจัดวางซึ่งสำคัญสำหรับการสกัดข้อมูลเชิงโครงสร้างในภายหลัง.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

หลังจาก `Recognize()` เสร็จสิ้น, `ocrEngine` จะเก็บทั้งข้อความธรรมดาและข้อมูลตำแหน่งของแต่ละคำ นี่เป็นพื้นฐานสำหรับขั้นตอนต่อไปที่เราจะให้ Aspose ทำการ “**how to extract receipt**” ฟิลด์โดยอัตโนมัติ.

## ขั้นตอนที่ 4 – เริ่มต้น Layout Recognizer

Aspose มีคลาส `LayoutRecognizer` ที่รู้ว่าการจัดเรียงใบเสร็จโดยทั่วไปเป็นอย่างไร (ผู้ขายที่ด้านบน, บรรทัดวันที่, ยอดรวมใกล้ด้านล่าง) คุณเพียงแค่ส่ง OCR engine ที่กำหนดค่าแล้วเข้าไป:

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

ภายใน, recognizer จะใช้ชุดของ heuristic—เช่นการมองหาสัญลักษณ์สกุลเงินหรือรูปแบบวันที่—to map raw text to semantic fields.

## ขั้นตอนที่ 5 – สกัดข้อมูลใบเสร็จเชิงโครงสร้าง

ตอนนี้เป็นส่วนที่สนุก: **extract receipt data**. การเรียกเมธอดเดียวทำงานหนัก:

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` เป็นอ็อบเจกต์ประเภท `ReceiptData` (กำหนดใน `Aspose.OCR.Structured`). มันมีคุณสมบัติหลักสามอย่าง:

- `Merchant` – ชื่อของร้าน
- `Date` – วันที่ซื้อเป็น `DateTime` (ถ้าพบ)
- `TotalAmount` – ยอดรวมเป็น `decimal`

หาก engine ไม่พบฟิลด์ใด ฟิลด์นั้นจะเป็น `null` หรือ `0`. คุณสามารถเพิ่มตรรกะสำรองได้หากต้องการ (เช่น ให้ผู้ใช้ยืนยัน).

## ขั้นตอนที่ 6 – แสดงข้อมูลที่สกัดออกมา

สุดท้าย, แสดงผลลัพธ์บนคอนโซล นี่คือจุดที่คุณเห็นผลลัพธ์จากความพยายามของคุณ:

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

สตริงฟอร์แมต (`:d` และ `:C`) จะสร้างวันที่สั้นและสตริงสกุลเงินตามลำดับ ทำให้ผลลัพธ์อ่านง่ายสำหรับมนุษย์.

### ผลลัพธ์ที่คาดหวัง

สมมติว่าใบเสร็จเป็นของ “Coffee Corner”, วันที่ 2025‑12‑01, และยอดรวม $4.75, คอนโซลจะแสดง:

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

หากฟิลด์ใดหายไป คุณจะเห็นบรรทัดว่างหรือค่าดีฟอลต์—เหมาะสำหรับการดีบัก.

## กรณีขอบและข้อผิดพลาดทั่วไป

### 1. ภาพความละเอียดต่ำ

หากภาพใบเสร็จเบลอหรือความละเอียดต่ำกว่า 150 dpi, ความแม่นยำของ OCR จะลดลงอย่างมาก การขยายภาพด้วยฟิลเตอร์ bilinear อย่างง่ายก่อนส่งให้ Aspose สามารถปรับปรุงผลลัพธ์ได้.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. ใบเสร็จที่ไม่ใช่ภาษาอังกฤษ

ตัวอย่างหลักใช้ `Language.English`. สำหรับใบเสร็จหลายภาษา ให้ตั้งค่า `Language` เป็น enum ที่เหมาะสม (เช่น `Language.French`) หรือใช้ `Language.AutoDetect` หากไม่แน่ใจ.

### 3. หลายใบเสร็จในภาพเดียว

Layout recognizer ของ Aspose คาดว่าจะมีใบเสร็จเดียวต่อภาพ หากคุณมีภาพของหลายใบเสร็จวางเคียงกัน คุณต้องทำการประมวลผลล่วงหน้า—ครอบตัดแต่ละใบเสร็จเป็นไฟล์ของมันเองก่อนรัน OCR.

### 4. ขาดสัญลักษณ์สกุลเงิน

บางครั้งยอดรวมปรากฏโดยไม่มีสัญลักษณ์ `$`. recognizer ยังคงจับตัวเลขได้ แต่คุณอาจต้องทำ post‑process สตริงเพื่อให้ตำแหน่งทศนิยมถูกต้อง.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## เคล็ดลับสำหรับการผลิต

- **Cache the OCR engine** หากคุณประมวลผลใบเสร็จหลายใบในชุด; การใช้ instance เดียวซ้ำจะลดภาระการจัดสรรหน่วยความจำ.
- **Log the raw OCR text** (`ocrEngine.Text`) เพื่อเป็นบันทึกตรวจสอบ. มีประโยชน์เมื่อฟิลด์ใดฟิลด์หนึ่งไม่สามารถสกัดได้.
- **Wrap the entire flow in a try/catch** และแสดงข้อความข้อผิดพลาดที่เป็นมิตร (เช่น “Unable to read receipt, please upload a clearer image”).

## ตัวอย่างทำงานสมบูรณ์

ด้านล่างเป็นแอปพลิเคชันคอนโซลที่สมบูรณ์แบบซึ่งคุณสามารถคอมไพล์และรันได้ทันที เพียงแทนที่เส้นทางภาพและคุณก็พร้อมใช้งาน.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Running the code**

1. สร้างโปรเจกต์คอนโซล .NET ใหม่ (`dotnet new console -n ReceiptExtractor`).
2. เพิ่มแพ็กเกจ Aspose.OCR (`dotnet add package Aspose.OCR`).
3. แทนที่ `Program.cs` ที่สร้างขึ้นด้วยสแนปชอตด้านบน.
4. วางภาพใบเสร็จที่เส้นทางที่คุณระบุ.
5. คอมไพล์และรัน (`dotnet run`).

คุณควรเห็นชื่อผู้ขาย, วันที่, และยอดรวมที่พิมพ์ออกมาตรงตามที่แสดงก่อนหน้านี้.

## สรุป

ในคู่มือนี้เราได้อธิบาย **how to use Aspose** เพื่อ **load receipt image**, รัน **ocr receipt image**, และสุดท้าย **extract receipt data** ด้วยเพียงไม่กี่บรรทัด สิ่งสำคัญคือ Aspose.OCR ทำงานหนักให้—เมื่อคุณตั้งค่า OCR engine แล้ว `LayoutRecognizer` จะเปลี่ยนข้อความดิบเป็นอ็อบเจกต์เชิงโครงสร้างที่คุณเชื่อถือได้.

ขั้นตอนต่อไป? ลองนำค่าที่สกัดไปบันทึกในฐานข้อมูล, สร้างสรุปใบเสร็จ PDF, หรือแม้กระทั่งป้อนเข้าสู่โมเดล machine‑learning เพื่อการจัดประเภทค่าใช้จ่าย คุณยังสามารถทดลองกับประเภทเอกสารเชิงโครงสร้างอื่น ๆ เช่น ใบแจ้งหนี้หรือป้ายจัดส่ง—`ExtractInvoiceData` ของ Aspose ทำงานในลักษณะคล้ายกัน.

มีคำถามเกี่ยวกับกรณีขอบหรืออยากดูวิธีจัดการกับ PDF หลายหน้า? แสดงความคิดเห็นหรือดูเอกสารอย่างเป็นทางการของ Aspose.OCR สำหรับสถานการณ์ขั้นสูง ขอให้สนุกกับการเขียนโค้ดและเพลิดเพลินกับความง่ายของ **how to use Aspose** สำหรับการอัตโนมัติใบเสร็จ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}