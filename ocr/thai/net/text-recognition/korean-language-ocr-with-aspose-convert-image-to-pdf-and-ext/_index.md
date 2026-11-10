---
category: general
date: 2026-05-28
description: บทเรียน OCR ภาษาเกาหลีโดยใช้ Aspose ใน C#. เรียนรู้วิธีโหลดภาพจากสตรีม,
  ดึงข้อความธรรมดา, แปลงภาพเป็น PDF และส่งออก PDF ที่ค้นหาได้.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: th
og_description: การทำ OCR ภาษาเกาหลีใน C# ด้วย Aspose. คู่มือขั้นตอนต่อขั้นตอนในการโหลดภาพจากสตรีม,
  แยกข้อความธรรมดา, แปลงภาพเป็น PDF และส่งออก PDF ที่ค้นหาได้.
og_title: OCR ภาษาเกาหลี – แปลงรูปภาพเป็น PDF และดึงข้อความ (คู่มือ C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR ภาษาเกาหลีด้วย Aspose: แปลงภาพเป็น PDF และสกัดข้อความใน C#'
url: /th/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR ภาษาเกาหลีด้วย Aspose: แปลงภาพเป็น PDF และดึงข้อความใน C#

เคยสงสัยไหมว่าจะทำ **OCR ภาษาเกาหลี** บนรูปภาพโดยไม่ต้องส่งข้อมูลไปยังคลาวด์? คุณไม่ได้เป็นคนเดียว ไม่ว่าจะเป็นการดิจิไทซ์ป้ายถนน, ประมวลผลใบเสร็จ, หรือสร้างดัชนีการค้นหาหลายภาษา การรู้จำอักขระเกาหลีแบบออฟไลน์สามารถช่วยประหยัดเวลา, เงิน, และปัญหาความเป็นส่วนตัวได้

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างที่ทำงานได้เต็มรูปแบบ ซึ่งจะแสดงวิธี **โหลดภาพจากสตรีม**, **ดึงข้อความธรรมดา**, **แปลงภาพเป็น PDF**, และสุดท้าย **ส่งออก PDF ที่สามารถค้นหาได้**—ทั้งหมดด้วย Aspose.OCR และเพียงไม่กี่บรรทัดของ C# ไม่มีบริการภายนอก, ไม่มีเวทมนตร์ที่ซ่อนอยู่—เพียงโค้ด .NET ที่คุณสามารถใส่ลงในแอปคอนโซลใดก็ได้

## สิ่งที่คุณจะได้เรียนรู้

- โปรแกรมคอนโซลที่ทำงานได้ซึ่งอ่านไฟล์ JPEG ผ่านสตรีมไฟล์  
- ข้อความเกาหลีที่ดึงออกมาเป็นสตริง Unicode ธรรมดา  
- รายงาน JSON รายละเอียดของการทำ OCR สำหรับการดีบักหรือวิเคราะห์  
- PDF ที่สามารถค้นหาได้ซึ่งคุณสามารถเปิดในโปรแกรมอ่าน PDF ใดก็ได้และเลือกคำเกาหลีได้จริง  

**ข้อกำหนดเบื้องต้น**  
- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.7+)  
- Aspose.OCR for .NET NuGet package ที่ติดตั้งแล้ว (`Install-Package Aspose.OCR`)  
- โฟลเดอร์ที่มีไฟล์ `korean_sign.jpg` และตำแหน่งที่สามารถเขียนไฟล์ผลลัพธ์ได้  

หากคุณมีทุกอย่างพร้อมแล้ว, ไปกันเลย

## ขั้นตอนที่ 1: เริ่มต้น OCR Engine สำหรับ OCR ภาษาเกาหลี

สิ่งแรกที่ต้องมีคืออินสแตนซ์ของ `OcrEngine` การเปิดใช้งาน GPU (หากมี) จะทำให้การรู้จำเร็วขึ้นอย่างมาก, และการปิดการดาวน์โหลดทรัพยากรอัตโนมัติจะบังคับให้ไลบรารีใช้แพ็คภาษาออฟไลน์ที่คุณเตรียมไว้

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **ทำไมเรื่องนี้ถึงสำคัญ:**  
> *GPU acceleration* สามารถลดเวลาประมวลผลจากวินาทีเป็นมิลลิวินาทีสำหรับชุดข้อมูลขนาดใหญ่ การตั้งค่า `AutomaticResourceDownload` เป็น `false` ทำให้ตัวอย่างทำงานแบบออฟไลน์—เป็นข้อกำหนดสำคัญสำหรับหลายองค์กร

## ขั้นตอนที่ 2: โหลดภาพจากสตรีม

การอ่านภาพผ่านสตรีมให้ความยืดหยุ่น: คุณสามารถดึงไฟล์จากดิสก์, แชร์เครือข่าย, หรือแม้แต่บล็อบที่แคชในหน่วยความจำ ที่นี่เราเปิดไฟล์ JPEG ในเครื่อง, แต่รูปแบบเดียวกันใช้ได้กับ `Stream` ใดก็ได้

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **เคล็ดลับ:** หากต้องประมวลผลภาพที่อัปโหลดผ่านเว็บ API เพียงเปลี่ยน `File.OpenRead` เป็น `IFormFile.OpenReadStream()`—ส่วนที่เหลือคงเดิม

## ขั้นตอนที่ 3: เลือกภาษาเกาหลีและใช้ฟิลเตอร์การเตรียมภาพล่วงหน้า

Aspose.OCR รองรับขั้นตอนการเตรียมภาพหลายขั้นตอนที่ทำความสะอาดภาพก่อนการรู้จำ สำหรับป้ายเกาหลี การจัดแนวและการลดสัญญาณรบกวนมักเพียงพอ

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **เกิดอะไรขึ้นเบื้องหลัง?**  
> ฟิลเตอร์ `Deskew` ทำให้ข้อความที่หมุนเอียงตรงขึ้น, ส่วน `Denoise` ลบเม็ดสีที่อาจทำให้ตัวจำแนกอักขระสับสน การข้ามขั้นตอนเหล่านี้มักทำให้ผลลัพธ์เป็นข้อความที่อ่านไม่ออก, โดยเฉพาะภาพความละเอียดต่ำ

## ขั้นตอนที่ 4: ดึงข้อความธรรมดาแบบอะซิงโครนัส

นี่คือช่วงเวลาที่ต้องการให้เอนจินรู้จำอักขระและคืนสตริงที่สะอาด การใช้ `RecognizeAsync` ทำให้ UI ตอบสนองได้ดีหากคุณนำไปฝังในแอปเดสก์ท็อปหรือเว็บ

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

เมื่อคุณรันโปรแกรม, คุณควรเห็นผลลัพธ์ประมาณนี้:

```
OCR complete. Extracted text:
서울시청
```

> **ทำไมต้องใช้ async?**  
> OCR ใช้ CPU อย่างหนัก การทำงานแบบอะซิงโครนัสช่วยป้องกันไม่ให้เธรดของคุณบล็อก, ซึ่งเป็นประโยชน์มากใน ASP.NET Core ที่ปัญหา thread starvation เป็นเรื่องจริง

## ขั้นตอนที่ 5: รับผลลัพธ์การรู้จำอย่างละเอียดและบันทึกเป็น JSON

บางครั้งคุณต้องการข้อมูลมากกว่าข้อความดิบ—เช่นคะแนนความมั่นใจ, กล่องขอบเขต, หรือข้อมูลภาพต้นฉบับ เมธอด `RecognizeDetailed` จะคืนอ็อบเจ็กต์ `RecognitionResult` ที่สามารถแปลงเป็น JSON เพื่อวิเคราะห์ต่อไป

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

การเปิดไฟล์ `korean_ocr.json` จะเผยโครงสร้างคล้ายกับ:

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **เมื่อใดควรใช้?**  
> หากคุณกำลังสร้างดัชนีการค้นหา, ค่า confidence ช่วยกรองผลลัพธ์คุณภาพต่ำ. หากต้องการไฮไลท์ข้อความใน UI, กล่องขอบเขตคือแผนที่ของคุณ

## ขั้นตอนที่ 6: แปลงภาพเป็น PDF และส่งออก PDF ที่สามารถค้นหาได้

Aspose ทำให้การเปลี่ยนจาก raster ไปเป็น vector ง่ายดาย เพียงตั้งค่า `OutputFormat` เป็น `SearchablePdf`, ไลบรารีจะฝังภาพต้นฉบับและวางเลเยอร์ข้อความที่มองไม่เห็นซึ่งมีผลลัพธ์ OCR อยู่ PDF ที่ได้สามารถค้นหา, คัดลอก, และทำดัชนีได้เหมือน PDF ปกติ

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

เปิดไฟล์ `korean_searchable.pdf` ใน Adobe Reader หรือโปรแกรมดู PDF ใดก็ได้, กด **Ctrl+F**, พิมพ์คำภาษาเกาหลี, แล้วดูว่ามันพาคุณไปยังตำแหน่งที่ตรงบนหน้า นั่นคือพลังของ PDF ที่สามารถค้นหาได้

> **เคล็ดลับเพิ่มเติม:** หากคุณต้องการ PDF ที่เป็นภาพเท่านั้นโดยไม่มีเลเยอร์ข้อความ, ให้เปลี่ยน `OutputFormat` เป็น `Pdf` แทน

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมทั้งหมด—คัดลอก, วาง, แทนที่ `YOUR_DIRECTORY` ด้วยพาธจริง, แล้วกด **F5**

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### ผลลัพธ์ที่คาดว่าจะเห็นในคอนโซล

```
OCR complete. Extracted text:
서울시청
```

และคุณจะพบไฟล์ใหม่สามไฟล์อยู่ข้างๆ ภาพต้นฉบับของคุณ:

- `korean_ocr.json` – ข้อมูลการรู้จำเต็มรูปแบบ  
- `korean_searchable.pdf` – PDF ที่สามารถค้นหาได้  
- (ทางเลือก) บันทึกใดๆ ที่คุณเพิ่มเข้ามาเป็นกลาง

## คำถามที่พบบ่อย & กรณีขอบ

**ถ้าไม่มี GPU จะทำอย่างไร?**  
ตั้งค่า `EnableGpu = false`; การทำงานบน CPU เพียงพอสำหรับชุดข้อมูลขนาดเล็ก

**สามารถประมวลผลหลายภาพในรอบเดียวได้หรือไม่?**  
ทำได้แน่นอน. ใส่ตรรกะหลักไว้ในลูป `foreach (var file in Directory.GetFiles(...))` แล้วกำหนด `ocrEngine.Image` ใหม่ในแต่ละรอบ

**จะจัดการหลายภาษาพร้อมกับเกาหลีอย่างไร?**  
Aspose.OCR ให้คุณตั้งค่า `Language = Language.AutoDetect` หรือรวมหลายภาษาโดยใช้ตัวดำเนินการ OR แบบบิต (เช่น `Language.Korean | Language.English`)

**ถ้าความมั่นใจของ OCR ต่ำควรทำอย่างไร?**  
ตรวจสอบ `detailedResult.Pages[0].Words` และกรองรายการที่มี `Confidence < 0.7`. คุณยังสามารถปรับฟิลเตอร์การเตรียมภาพ—ลองเพิ่ม `PreprocessFilter.ContrastEnhancement`

## สรุป

คุณเพิ่งเห็นวิธีทำ **OCR ภาษาเกาหลี** ตั้งแต่ **โหลดภาพจากสตรีม** ไปจนถึง **ดึงข้อความธรรมดา**, จากนั้น **แปลงภาพเป็น PDF** และสุดท้าย **ส่งออก PDF ที่สามารถค้นหาได้** วิธีการนี้เป็นโมดูลาร์, คุณจึงสามารถสลับแหล่งภาพ, เปลี่ยนรูปแบบผลลัพธ์, หรือเชื่อมต่อ JSON ไปยัง pipeline ใดก็ได้

What’s next


## Related Tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}