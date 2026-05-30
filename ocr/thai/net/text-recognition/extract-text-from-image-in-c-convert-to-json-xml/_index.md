---
category: general
date: 2026-04-26
description: สกัดข้อความจากรูปภาพใน C# ด้วย Aspose.OCR และเรียนรู้วิธีแปลงรูปภาพเป็นรูปแบบ
  JSON และ XML ในไม่กี่นาที
draft: false
keywords:
- extract text from image
- convert image to json
- convert image to xml
- Aspose OCR C#
- image to JSON C#
- image to XML C#
language: th
og_description: ดึงข้อความจากภาพใน C# ด้วย Aspose.OCR. เรียนรู้ขั้นตอนโดยละเอียดว่าจะแปลงผลลัพธ์เป็น
  JSON และ XML ได้ทันทีอย่างไร.
og_title: ดึงข้อความจากภาพใน C# – แปลงเป็น JSON และ XML
tags:
- OCR
- C#
- Aspose
- JSON
- XML
title: ดึงข้อความจากรูปภาพใน C# – แปลงเป็น JSON และ XML
url: /th/net/text-recognition/extract-text-from-image-in-c-convert-to-json-xml/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากภาพใน C# – แปลงเป็น JSON & XML

เคยต้องการ **extract text from image** ในโปรเจกต์ .NET แต่รู้สึกติดขัดที่ “ฉันจะดึงข้อมูลออกมาได้อย่างไร?” คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันจริงหลายกรณี—เช่น การประมวลผลใบแจ้งหนี้, การสแกนใบเสร็จ, หรือการตรวจสอบบัตร—การดึงอักขระดิบจากภาพเป็นขั้นตอนแรกที่สำคัญ  

ข่าวดีคือ? ด้วย Aspose.OCR คุณสามารถทำได้ในไม่กี่บรรทัด แล้วแปลง **convert image to JSON** หรือ **convert image to XML** ให้กับระบบต่อไปได้ทันที ในคู่มือนี้เราจะพาไปดูโค้ดที่พร้อมรันเต็มรูปแบบ อธิบายว่าทำไมแต่ละส่วนถึงสำคัญ และแสดงเคล็ดลับบางอย่างเพื่อหลีกเลี่ยงข้อผิดพลาดทั่วไป

---

## สิ่งที่คุณต้องการ

- **.NET 6+** (SDK ล่าสุดใดก็ได้ทำงาน; ตัวอย่างใช้ .NET 6)
- **Aspose.OCR for .NET** NuGet package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- ไฟล์ภาพ (PNG, JPG, ฯลฯ) ที่มีข้อความที่สามารถพิมพ์ได้; เราจะใช้ `invoice.png` เป็นตัวอย่าง
- โปรแกรมแก้ไขโค้ด—Visual Studio, VS Code, หรือ Rider—ตามที่คุณชอบ

แค่นั้นเอง ไม่ต้องใช้ OCR engine เพิ่มเติม ไม่ต้องใช้บริการภายนอก เพียงแพคเกจ NuGet เดียว

## ขั้นตอนที่ 1: ตั้งค่า OCR Engine – วิธีดึงข้อความจากภาพ

ก่อนอื่นเราจะสร้างอินสแตนซ์ `OcrEngine` แล้วชี้ไปที่ไฟล์ภาพ ขั้นตอนนี้เป็นพื้นฐาน; หากไม่มีการโหลดภาพอย่างถูกต้อง engine จะไม่สามารถจดจำอะไรได้

```csharp
using Aspose.OCR;
using System.IO;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process
// Replace YOUR_DIRECTORY with the actual folder path
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/invoice.png");

// Optional: verify the image was loaded
if (ocrEngine.Image == null)
{
    throw new FileNotFoundException("Image not found. Check the path and filename.");
}
```

**ทำไมสิ่งนี้จึงสำคัญ:**
- `OcrEngine` รวมการประมวลผลภาพระดับล่างทั้งหมด (binarization, deskewing).  
- การโหลดภาพด้วย `ImageStream.FromFile` ทำให้ engine อ่านไบต์ที่ตรงกัน, รักษา DPI และความลึกสี—ซึ่งทั้งสองสามารถส่งผลต่อความแม่นยำของการจดจำ

> **เคล็ดลับ:** หากภาพต้นทางของคุณอยู่ในสตรีม (เช่น อัปโหลดผ่านเว็บ API) ให้ใช้ `ImageStream.FromStream(yourStream)` แทน `FromFile`.

## ขั้นตอนที่ 2: แจ้งให้ Engine ทราบภาษาที่คาดหวัง – ดึงข้อความจากภาพอย่างแม่นยำ

Aspose.OCR รองรับอักษรหลายชุด การระบุภาษาที่ถูกต้องจะจำกัดชุดอักขระและเพิ่มความแม่นยำ

```csharp
// Set the language; Latin covers English, French, German, etc.
ocrEngine.Language = Language.Latin;
```

**ทำไม:**
เมื่อคุณตั้งค่า `Language.Latin` OCR engine จะละเว้น glyph ของ Cyrillic หรือภาษาเอเชีย ลดการตรวจจับผิดพลาด หากคุณต้องการจัดการเอกสารหลายภาษาในภายหลัง คุณสามารถสลับเป็น `Language.Multilingual` หรือรวมหลายภาษาได้

## ขั้นตอนที่ 3: เรียกกระบวนการจดจำ – ดึงข้อความจากภาพในหนึ่งครั้ง

ตอนนี้เราจะทำการจดจำข้อความจริงๆ เมธอด `Recognize` จะคืนค่าอ็อบเจกต์ `RecognitionResult` ที่เก็บข้อความดิบ, คะแนนความมั่นใจ, และข้อมูลการจัดวาง

```csharp
// Perform OCR
RecognitionResult recognitionResult = ocrEngine.Recognize();

// Quick sanity check
if (recognitionResult == null || string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text was detected. Verify the image quality.");
    return;
}

// Print the raw extracted text to the console
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(recognitionResult.Text);
```

**ทำไม:**
การเรียก `Recognize` เพียงครั้งเดียวก็เพียงพอ เพราะ engine จะทำการ preprocessing, segmentation, และการจำแนกอักขระภายในเอง คุณสมบัติ `Text` ให้สตริงธรรมดาที่เหมาะสำหรับการบันทึกหรือการตรวจสอบอย่างรวดเร็ว

## ขั้นตอนที่ 4: แปลงผลลัพธ์เป็น JSON – แปลงภาพเป็น JSON อย่างง่าย

บริการสมัยใหม่หลายแห่งชอบใช้ payload แบบ JSON Aspose.OCR มีเมธอด `ToJson` ที่สะดวกซึ่งทำการ serialize `RecognitionResult` ทั้งหมด รวมถึงค่าความมั่นใจและ bounding box

```csharp
// Serialize the result to JSON
string jsonResult = recognitionResult.ToJson();

// Save the JSON to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonResult);

Console.WriteLine("JSON file saved at YOUR_DIRECTORY/invoice.json");
```

**ทำไมคุณอาจต้องการ JSON:**
- **Interoperability:** แอปฝั่ง Front‑end (React, Angular) สามารถใช้ JSON ได้โดยตรง.  
- **Debugging:** JSON มีความมั่นใจต่ออักขระแต่ละตัว ช่วยให้คุณทำเครื่องหมายคำที่ความมั่นใจต่ำเพื่อการตรวจสอบด้วยมือ.  

> **กรณีขอบ:** หากระบบต่อไปของคุณต้องการเพียงข้อความธรรมดา คุณสามารถดึง `recognitionResult.Text` แล้วใส่ในอ็อบเจกต์ JSON ที่กำหนดเองแทนการใช้ payload ของ Aspose ทั้งหมด

## ขั้นตอนที่ 5: แปลงผลลัพธ์เป็น XML – แปลงภาพเป็น XML สำหรับระบบเก่า

บางองค์กรยังคงพึ่งพา schema XML สำหรับการแลกเปลี่ยนข้อมูล เมธอด `ToXml` ทำงานคล้าย `ToJson` แต่ส่งออกเป็น XML

```csharp
// Serialize the result to XML
string xmlResult = recognitionResult.ToXml();

// Save the XML to a file
File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlResult);

Console.WriteLine("XML file saved at YOUR_DIRECTORY/invoice.xml");
```

**ทำไมต้อง XML:**
- **Schema validation:** คุณสามารถกำหนด XSD ที่ตรงกับโครงสร้างที่ Aspose ส่งออก เพื่อรับประกันการปฏิบัติตามสัญญา.  
- **Integration:** ระบบ ERP หรือระบบจัดการเอกสารรุ่นเก่ามักจะรองรับการแยกวิเคราะห์ XML โดยตรง

## ตัวอย่างทำงานเต็มรูปแบบ – โค้ดครบวงจร

ด้านล่างเป็นโปรแกรมเต็มที่เชื่อมทุกส่วนเข้าด้วยกัน คัดลอกและวางลงในโปรเจกต์คอนโซลใหม่ (`dotnet new console`) แล้วรัน

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Initialize OCR engine and load the image
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();
            // Adjust the path to point at your PNG/JPG file
            string imagePath = "YOUR_DIRECTORY/invoice.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image at {imagePath}");
                return;
            }

            // -------------------------------------------------
            // Step 2: Specify language (Latin for most European scripts)
            // -------------------------------------------------
            ocrEngine.Language = Language.Latin;

            // -------------------------------------------------
            // Step 3: Run OCR and get the result
            // -------------------------------------------------
            RecognitionResult result = ocrEngine.Recognize();

            if (result == null || string.IsNullOrWhiteSpace(result.Text))
            {
                Console.WriteLine("No text detected – check image quality or language setting.");
                return;
            }

            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();

            // -------------------------------------------------
            // Step 4: Convert to JSON (convert image to json)
            // -------------------------------------------------
            string json = result.ToJson();
            string jsonPath = "YOUR_DIRECTORY/invoice.json";
            File.WriteAllText(jsonPath, json);
            Console.WriteLine($"JSON output written to {jsonPath}");

            // -------------------------------------------------
            // Step 5: Convert to XML (convert image to xml)
            // -------------------------------------------------
            string xml = result.ToXml();
            string xmlPath = "YOUR_DIRECTORY/invoice.xml";
            File.WriteAllText(xmlPath, xml);
            Console.WriteLine($"XML output written to {xmlPath}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง (คอนโซล):**

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

JSON file saved at YOUR_DIRECTORY/invoice.json
XML file saved at YOUR_DIRECTORY/invoice.xml
```

ไฟล์ JSON และ XML จะมีโครงสร้างที่ละเอียดกว่า ตัวอย่างเช่น:

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
  "Confidence": 0.96,
  "Blocks": [
    { "Text": "Invoice #12345", "Confidence": 0.98, "Rectangle": { "X": 12, "Y": 30, "Width": 200, "Height": 20 } },
    ...
  ]
}
```

```xml
<RecognitionResult>
  <Text>Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00</Text>
  <Confidence>0.96</Confidence>
  <Blocks>
    <Block>
      <Text>Invoice #12345</Text>
      <Confidence>0.98</Confidence>
      <Rectangle X="12" Y="30" Width="200" Height="20"/>
    </Block>
    ...
  </Blocks>
</RecognitionResult>
```

## คำถามทั่วไป & กรณีขอบ

### ถ้าภาพเบลอหรือหมุน?

Aspose.OCR จะทำการ deskew ภาพส่วนใหญ่โดยอัตโนมัติ แต่ในกรณีสุดโต่งคุณอาจต้องทำการพรี‑โปรเซสด้วย `ocrEngine.Image = ImageProcessor.Deskew(ocrEngine.Image)` การเพิ่มคอนทราสต์เล็กน้อย (`ImageProcessor.AdjustContrast`) ก็สามารถเพิ่มคะแนนความมั่นใจได้

### ฉันสามารถดึงข้อความจาก PDF ได้ไหม?

ได้—ให้แปลงแต่ละหน้า PDF เป็นภาพก่อน (เช่น ใช้ Aspose.PDF หรือไลบรารีฟรีอย่าง PDFium) แล้วจึงส่งภาพเหล่านั้นเข้าสู่กระบวนการ OCR เดียวกัน

### ฉันจะจัดการหลายภาษาในเอกสารเดียวอย่างไร?

ตั้งค่า `ocrEngine.Language = Language.Multilingual;` หรือรวมหลายภาษาเฉพาะ:

```csharp
ocrEngine.Language = Language.English | Language.French | Language.German;
```

โปรดทราบว่าชุดภาษาที่กว้างขึ้นอาจ

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}