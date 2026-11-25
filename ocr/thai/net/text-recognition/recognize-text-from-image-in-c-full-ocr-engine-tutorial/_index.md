---
category: general
date: 2026-06-06
description: จดจำข้อความจากภาพด้วยเครื่องมือ OCR ของ C# เรียนรู้การแปลงภาพเป็น JSON,
  แปลงภาพเป็น XML, และโหลดภาพสำหรับ OCR ภายในไม่กี่นาที.
draft: false
keywords:
- recognize text from image
- convert image to json
- convert image to xml
- ocr engine c#
- load image for ocr
language: th
og_description: จดจำข้อความจากภาพด้วยเครื่องมือ OCR ของ C# ส่งออกผลลัพธ์เป็น JSON
  และ XML และจัดการการโหลดภาพสำหรับ OCR อย่างเชี่ยวชาญ.
og_title: การจดจำข้อความจากภาพใน C# – บทเรียนเต็มของเครื่อง OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Recognize text from image using C# OCR engine. Learn to convert image
    to JSON, convert image to XML, and load image for OCR in minutes.
  headline: Recognize Text from Image in C# – Full OCR Engine Tutorial
  type: TechArticle
tags:
- OCR
- C#
- Image Processing
title: แยกข้อความจากภาพด้วย C# – บทเรียนเต็มของเครื่องมือ OCR
url: /th/net/text-recognition/recognize-text-from-image-in-c-full-ocr-engine-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# จดจำข้อความจากรูปภาพใน C# – บทเรียนเต็มของ OCR Engine

เคยต้อง **จดจำข้อความจากรูปภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารี C# ตัวไหนใช่ไหม? คุณไม่ได้เป็นคนเดียว—นักพัฒนามักต้องต่อสู้กับการแปลงใบเสร็จสแกน, ภาพหน้าจอ, หรือโน้ตมือเขียนให้เป็นข้อความที่ค้นหาได้ ข่าวดีคือ? ด้วย **OCR engine C#** สมัยใหม่ คุณทำได้เพียงไม่กี่บรรทัด แล้ว **แปลงรูปภาพเป็น JSON** หรือ **แปลงรูปภาพเป็น XML** เพื่อการประมวลผลต่อไป

ในคู่มือนี้เราจะเดินผ่านทุกขั้นตอน: การติดตั้งแพคเกจ OCR, การโหลดรูปภาพสำหรับ OCR, การดึงข้อความ, และสุดท้ายการส่งออกผลลัพธ์เป็นทั้ง JSON และ XML. เมื่ออ่านจบคุณจะมีแอปคอนโซลที่ทำงานได้เองซึ่งสามารถใส่ลงในโปรเจกต์ .NET ใดก็ได้ ไม่ต้องอ้างอิงที่คลุมเครือ เพียงโซลูชันที่สมบูรณ์และรันได้

## สิ่งที่คุณจะได้เรียนรู้

- ภาพรวมชัดเจนว่าต้อง **โหลดรูปภาพสำหรับ OCR** อย่างไรด้วย OCR engine C# ที่เป็นที่นิยม  
- โค้ดทำงานที่ **จดจำข้อความจากรูปภาพ** และคืนค่าอ็อบเจ็กต์ผลลัพธ์ที่สมบูรณ์  
- ตัวอย่างสั้น ๆ ที่ **แปลงรูปภาพเป็น JSON** และ **แปลงรูปภาพเป็น XML** โดยไม่ต้องใช้ไลบรารีเพิ่มเติม  
- เคล็ดลับการจัดการ PDF หลายหน้า, รูปแบบไฟล์ต่าง ๆ, และข้อผิดพลาดทั่วไปเช่นการสแกนที่คอนทราสต์ต่ำ

### ข้อกำหนดเบื้องต้น

- .NET 6 SDK หรือใหม่กว่า (คุณสามารถเลือกเป้าหมายเป็น .NET Framework 4.8 ได้เช่นกัน)  
- ความรู้พื้นฐาน C#—ไม่ต้องซับซ้อน เพียงเข้าใจคลาสและ `async`/`await`  
- ไฟล์รูปภาพ (`structured.png` ในตัวอย่าง) ที่คุณต้องการทำ OCR  

ถ้าคุณมีสิ่งเหล่านี้แล้ว ไปต่อกันเลย

---

## จดจำข้อความจากรูปภาพ – การตั้งค่า OCR Engine

อย่างแรกเลย เราต้องมีไลบรารี OCR ที่เชื่อถือได้ สำหรับบทเรียนนี้เราจะใช้ **IronOcr** ซึ่งเป็นเอนจินระดับเชิงพาณิชย์ที่มีเวอร์ชัน community ฟรีบน NuGet. มันรองรับภาษาอังกฤษโดยอัตโนมัติและให้คลาส `OcrEngine` ตามที่แสดงในโค้ดต้นฉบับ

```bash
dotnet add package IronOcr --version 2024.3.0
```

> **เคล็ดลับ:** หากงบประมาณค่อนข้างจำกัด สามารถสลับจาก `IronOcr` ไปใช้ `Tesseract`—API จะต่างกันเล็กน้อยแต่แนวคิดยังคงเหมือนเดิม

ต่อไปสร้างโปรเจกต์คอนโซลใหม่และเพิ่ม `using` ที่จำเป็น:

```csharp
using IronOcr;
using System.IO;
```

### การกำหนดค่า Engine ทีละขั้นตอน

```csharp
// Step 1: Create and configure the OCR engine
var ocrEngine = new IronTesseract();           // IronOcr’s engine class
ocrEngine.Language = OcrLanguage.English;     // Load English language data
```

*ทำไมต้องทำเช่นนี้:* การสร้าง engine ครั้งเดียวแล้วใช้ซ้ำหลายรูปภาพช่วยลดภาระการทำงาน. การกำหนดภาษาชัดเจนยังช่วยหลีกเลี่ยงการตรวจจับอัตโนมัติของ engine ที่อาจช้าและแม่นยำน้อยลง

---

## โหลดรูปภาพสำหรับ OCR – ป้อนข้อมูลให้ Engine

Engine ต้องการอ็อบเจ็กต์ `OcrInput`. คุณสามารถชี้ไปที่พาธไฟล์, สตรีม, หรือแม้แต่ `Bitmap`. นี่คือวิธีที่ง่ายที่สุด:

```csharp
// Step 2: Load the image to be processed
var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");

// Optional: improve accuracy on low‑contrast images
input.Deskew();          // Straighten tilted pages
input.Contrast(10);      // Boost contrast by 10%
```

> **กรณีขอบ:** หากแหล่งข้อมูลของคุณเป็น PDF หลายหน้า ให้เรียก `input.AddPdf("file.pdf")` แทน PNG. OCR engine จะจัดการแต่ละหน้าเป็นภาพแยกโดยอัตโนมัติ

---

## จดจำข้อความจากรูปภาพ – รันกระบวนการ OCR

เมื่อ engine และ input พร้อม การจดจำจริงเป็นบรรทัดเดียว:

```csharp
// Step 3: Recognize text in the image
using var result = ocrEngine.Read(input);
```

`result` คืออ็อบเจ็กต์ `OcrResult` ที่ประกอบด้วย:

- `Text` – สตริงข้อความดิบที่สกัดออกมา  
- `Lines` – คอลเลกชันของอ็อบเจ็กต์ `OcrLine` พร้อมคะแนนความเชื่อมั่น  
- `Words` – คอลเลกชันของคำแต่ละคำ พร้อมคะแนนความเชื่อมั่นเช่นกัน  

คุณสามารถตรวจสอบโดยตรงใน debugger, แต่ส่วนใหญ่คุณจะต้องการทำการซีเรียลไลซ์ข้อมูล

---

## แปลงรูปภาพเป็น JSON – ส่งออกผลลัพธ์ OCR

IronOcr มีการซีเรียลไลซ์ JSON ในตัวผ่าน `System.Text.Json`. โค้ดต่อไปนี้จะเขียนไฟล์ JSON ที่จัดรูปแบบสวยงามไว้ข้างไฟล์รูปต้นฉบับของคุณ:

```csharp
// Step 4: Export the recognition result to JSON and save it
string jsonResult = System.Text.Json.JsonSerializer.Serialize(result, new System.Text.Json.JsonSerializerOptions
{
    WriteIndented = true
});
File.WriteAllText(@"YOUR_DIRECTORY\result.json", jsonResult);
```

**สิ่งที่คุณจะเห็น:** เอกสาร JSON ที่จัดรูปแบบอย่างดีซึ่งบรรจุข้อความดิบ, คะแนนความเชื่อมั่น, และกล่องขอบเขตของแต่ละบรรทัดและคำ. โครงสร้างนี้เหมาะอย่างยิ่งสำหรับส่งต่อไปยังบริการ downstream เช่น ElasticSearch หรือ Azure Cognitive Search

---

## แปลงรูปภาพเป็น XML – ส่งออกข้อมูลแบบโครงสร้าง

บางระบบ legacy ยังคงต้องการ XML. เมธอด `ToXml()` ของ IronOcr ให้การแปลงที่รวดเร็ว:

```csharp
// Step 5: Export the recognition result to XML and save it
string xmlResult = result.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY\result.xml", xmlResult);
```

XML จะสะท้อนโครงสร้างของ JSON, มีองค์ประกอบ `<Line>` และ `<Word>` ที่มีแอตทริบิวต์ `Confidence`. หากคุณต้องการสคีม่าแบบกำหนดเอง สามารถโปรเจค `result` ไปยัง `XDocument` ด้วยตนเอง—API รองรับ LINQ อย่างเต็มที่

---

## ตัวอย่างโค้ดเต็มแบบ End‑to‑End

รวมทุกอย่างเข้าด้วยกัน นี่คือ `Program.cs` ที่พร้อมรัน:

```csharp
using IronOcr;
using System;
using System.IO;
using System.Text.Json;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine
        var ocrEngine = new IronTesseract();
        ocrEngine.Language = OcrLanguage.English;

        // 2️⃣ Load the image (adjust the path to your file)
        var input = new OcrInput(@"YOUR_DIRECTORY\structured.png");
        input.Deskew();
        input.Contrast(10);

        // 3️⃣ Perform recognition
        using var result = ocrEngine.Read(input);
        Console.WriteLine("✅ OCR completed. Extracted text:");
        Console.WriteLine(result.Text);

        // 4️⃣ Convert image to JSON
        string json = JsonSerializer.Serialize(result, new JsonSerializerOptions { WriteIndented = true });
        string jsonPath = @"YOUR_DIRECTORY\result.json";
        File.WriteAllText(jsonPath, json);
        Console.WriteLine($"📄 JSON saved to {jsonPath}");

        // 5️⃣ Convert image to XML
        string xml = result.ToXml();
        string xmlPath = @"YOUR_DIRECTORY\result.xml";
        File.WriteAllText(xmlPath, xml);
        Console.WriteLine($"📄 XML saved to {xmlPath}");
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (ตัดทอนไว้เพื่อความกระชับ):

```
✅ OCR completed. Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $1,234.56
...
📄 JSON saved to YOUR_DIRECTORY\result.json
📄 XML saved to YOUR_DIRECTORY\result.xml
```

รันโปรแกรมด้วย `dotnet run`. หากทุกอย่างเชื่อมต่อถูกต้อง คุณจะเห็นการพิมพ์บนคอนโซลและไฟล์สองไฟล์ปรากฏใน `YOUR_DIRECTORY`

---

## คำถามทั่วไป & จุดที่ต้องระวัง

| Question | Answer |
|----------|--------|
| *รูปภาพเป็น JPEG ที่มีการหมุนตาม EXIF จะทำอย่างไร?* | ใช้ `input.AutoRotate()` ก่อน `Deskew()`. IronOcr จะอ่านแท็ก EXIF และแก้ไขทิศทางให้ |
| *สามารถ OCR โฟลเดอร์ของรูปภาพทั้งหมดได้ครั้งเดียวหรือไม่?* | ทำได้แน่นอน. ห่อหุ้มโลจิกข้างต้นในลูป `foreach (var file in Directory.GetFiles(folder, "*.png"))` |
| *จะเพิ่มความแม่นยำให้กับการสแกนที่มีสัญญาณรบกวนได้อย่างไร?* | เพิ่ม `input.Denoise()` และพิจารณา `input.BlackWhiteThreshold(120)`. นอกจากนี้ให้ใช้แพ็คเกจภาษาที่ตรงกับเอกสาร |
| *รูปแบบ JSON นี้เข้ากันได้กับไลบรารี OCR ตัวอื่นหรือไม่?* | สคีม่าเป็นทั่วไปพอ—มี `Text`, `Lines`, `Words`—จึงสามารถแมปไปยังผลลัพธ์ของ Tesseract ได้ด้วยการแปลงเล็กน้อย |

---

## เคล็ดลับประสิทธิภาพ (ระดับ Pro)

- **Reuse the engine**: การสร้าง `IronTesseract` ภายในลูปแคบอาจทำให้ประสิทธิภาพลดลงถึง 30 % . ควรใช้ singleton ต่อแอปพลิเคชันโดเมนหนึ่ง  
- **Parallelize I/O**: หากต้องประมวลผลหลายสิบรูปภาพ ให้อ่านเข้าเมมโมรีพร้อมกัน (`Task.WhenAll`) แล้วส่งแต่ละ `OcrInput` ไปยัง engine เดียว—IronOcr รองรับการทำงานแบบหลายเธรด  
- **Batch export**: แทนการเขียนไฟล์ JSON/XML ทีละไฟล์ ให้รวบรวมผลลัพธ์เป็นคอลเลกชันเดียวแล้วซีเรียลไลซ์ครั้งเดียว จะช่วยลดการเขียนดิสก์

---

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

ตอนนี้คุณสามารถ **จดจำข้อความจากรูปภาพ** แล้ว ลองขยาย pipeline ของคุณต่อ:

- **การรวมกับระบบค้นหา** – ส่ง JSON ไปยัง Elasticsearch เพื่อการค้นหาเต็มข้อความ  
- **การจัดประเภทเอกสาร** – ป้อนผล OCR ให้โมเดล ML ขนาดเล็กเพื่อทำการแท็กอัตโนมัติ เช่น ใบแจ้งหนี้, สัญญา, หรือใบเสร็จ  
- **ข้อความมือเขียน** – เปลี่ยนแพ็คเกจภาษาเป็น `OcrLanguage.EnglishHandwritten` (มีในระดับพรีเมี่ยมของ IronOcr)  

แต่ละหัวข้อนี้ต่อยอดจากพื้นฐานที่คุณสร้างไว้และจะทำให้คุณมีงานทำหลายสัปดาห์

---

## สรุป

เราได้อธิบายวิธี **จดจำข้อความจากรูปภาพ** ด้วย **OCR engine C#** สมัยใหม่, จากนั้น **แปลงรูปภาพเป็น JSON** และ **แปลงรูปภาพเป็น XML**, รวมถึงวิธี **โหลดรูปภาพสำหรับ OCR** อย่างมั่นคง ตัวอย่างเต็มทำงานภายในไม่กี่นาทีและไฟล์ที่ส่งออกพร้อมใช้กับระบบ downstream ใดก็ได้

ลองรันโค้ด ปรับแต่งตามต้องการ แล้วคุณจะพร้อมก้าวต่อไป

## คุณควรเรียนรู้อะไรต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดและต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายทีละขั้นตอน เพื่อช่วยให้คุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการทำงานทางเลือกในโปรเจกต์ของคุณเอง

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}