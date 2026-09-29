---
category: general
date: 2026-02-13
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# เรียนรู้วิธีอ่านข้อความจากไฟล์
  JPG และรัน OCR บนภาพด้วยตัวอย่างที่สมบูรณ์และสามารถทำงานได้.
draft: false
keywords:
- extract text from image
- read text from jpg
- run OCR on image
- Aspose OCR C#
- OCR language packs
language: th
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# คู่มือนี้แสดงวิธีอ่านข้อความจากไฟล์
  JPG และทำ OCR บนภาพพร้อมตัวอย่างโค้ดเต็ม
og_title: สกัดข้อความจากภาพด้วย Aspose OCR – เริ่มต้นเร็ว C#
tags:
- C#
- OCR
- Aspose
title: ดึงข้อความจากภาพด้วย Aspose OCR – เริ่มต้นอย่างรวดเร็วด้วย C#
url: /th/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-quickstart/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากภาพด้วย Aspose OCR – คำแนะนำเร็ว C#

เคยต้องการ **สกัดข้อความจากภาพ** แต่ไม่แน่ใจว่าจะเลือกไลบรารีไหนใช่ไหม? คุณไม่ได้อยู่คนเดียว—นักพัฒนามักต้องต่อสู้กับการอ่านข้อความจากไฟล์ jpg อยู่เสมอ, โดยเฉพาะเมื่อเนื้อหาอยู่ในสคริปต์ที่ไม่ใช่ละติน. ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถรัน OCR บนไฟล์ภาพได้เพียงไม่กี่บรรทัดของโค้ด C#, และไลบรารีจะจัดการดาวน์โหลดแพคภาษาเมื่อจำเป็น.

ในบทเรียนนี้เราจะพาคุณผ่านตัวอย่างครบวงจรที่แสดงวิธี **สกัดข้อความจากภาพ** ด้วย Aspose OCR, จำกัดการจดจำเป็นภาษารัสเซีย, และพิมพ์ผลลัพธ์ไปที่คอนโซล. เมื่อจบคุณจะสามารถอ่านข้อความจากไฟล์ jpg, รัน OCR บนทรัพยากรภาพขนาดใดก็ได้, และปรับโค้ดให้รองรับภาษาอื่นด้วยการเปลี่ยนแปลงเพียงเล็กน้อย.

> **สิ่งที่คุณจะได้เรียนรู้**
> * วิธีติดตั้งและอ้างอิง Aspose OCR ในโครงการ .NET.  
> * ขั้นตอนที่แม่นยำเพื่อ **สกัดข้อความจากภาพ**—การเริ่มต้น engine, การเลือกภาษา, และการเรียก `RecognizeImage`.  
> * ทำไมคุณอาจต้องล็อก engine ให้ใช้แพคภาษาเดียว (ความเร็ว, ความแม่นยำ).  
> * ข้อผิดพลาดทั่วไปเช่นไฟล์หายหรือรูปแบบที่ไม่รองรับ, และวิธีจัดการอย่างราบรื่น.  

## ความต้องการเบื้องต้น

ก่อนที่เราจะลงลึก, โปรดตรวจสอบว่าคุณมีสิ่งต่อไปนี้บนเครื่องของคุณ:

| ความต้องการ | เหตุผล |
|-------------|--------|
| .NET 6.0 SDK หรือใหม่กว่า | Aspose OCR รองรับ .NET Standard 2.0+, ดังนั้น .NET 6 จะให้คุณใช้คุณสมบัติ runtime ล่าสุด. |
| Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ) | มีประโยชน์สำหรับการดีบัก, แต่ไม่จำเป็นต้องมี. |
| ไฟล์ภาพ (`cyrillic_sample.jpg`) ที่มีข้อความเป็นอักษรซีริลลิก | เราจะใช้ไฟล์นี้เพื่อสาธิต **อ่านข้อความจาก jpg**. |
| การเชื่อมต่ออินเทอร์เน็ต (ครั้งแรกเท่านั้น) | Aspose OCR จะดาวน์โหลดแพคภาษาเมื่อจำเป็น. |

หากคุณขาดสิ่งใดสิ่งหนึ่ง, ให้ดาวน์โหลดและติดตั้งทันที—ไม่ต้องรีสตาร์ทหลังจากติดตั้ง SDK.

## ขั้นตอนที่ 1: ติดตั้งแพคเกจ NuGet ของ Aspose OCR

สิ่งแรกที่คุณต้องการคือไลบรารี Aspose OCR. เปิดเทอร์มินัลในโฟลเดอร์โครงการของคุณและรัน:

```bash
dotnet add package Aspose.OCR
```

คำสั่งนี้จะดึงเวอร์ชันเสถียรล่าสุด (ณ กุมภาพันธ์ 2026 คือ 23.12) และเพิ่มลงในไฟล์ `.csproj` ของคุณ. แพคเกจนี้รวมเอา core OCR engine และตัวดาวน์โหลดขนาดเล็กสำหรับแพคภาษา, ดังนั้นคุณไม่ต้องบรรจุไฟล์ขนาดใหญ่กับแอปของคุณ.

> **เคล็ดลับ:** หากคุณทำงานอยู่หลังพร็อกซี่ขององค์กร, ตั้งค่าตัวแปรสภาพแวดล้อม `http_proxy` ก่อนรันคำสั่งเพื่อหลีกเลี่ยงข้อผิดพลาดการดาวน์โหลด.

## ขั้นตอนที่ 2: สร้างโครงสร้างแอปคอนโซลพื้นฐาน

มาสร้างแอปคอนโซลขนาดเล็กที่ใช้โค้ด OCR ของเรา. เปิด `Program.cs` (หรือสร้างไฟล์ใหม่) แล้ววางโครงร่างด้านล่าง. สังเกต `using` directives ที่ด้านบน—มันทำให้เนมสเปซของ Aspose OCR สามารถเข้าถึงได้.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in in the next steps.
        }
    }
}
```

ในตอนนี้โครงการจะคอมไพล์ได้, แต่ยังไม่มีการทำงานใด ๆ. ส่วนต่อไปจะเติมเต็ม workflow **run OCR on image**.

## ขั้นตอนที่ 3: เริ่มต้น OCR Engine (สกัดข้อความจากภาพ)

เพื่อ **สกัดข้อความจากภาพ**, คุณต้องสร้างอินสแตนซ์ของ `OcrEngine` ก่อน. Aspose OCR จะดาวน์โหลดทรัพยากรภาษาแบบ lazy ครั้งแรกที่ต้องการ, ทำให้ไบนารีเริ่มต้นมีขนาดเล็ก.

```csharp
// Step 3: Initialize the OCR engine (resources are downloaded on demand)
var ocrEngine = new OcrEngine();
```

ทำไมต้องเริ่มต้นที่นี่แทนการใช้ฟิลด์ static? การทำใน `Main` ทำให้ข้อยกเว้นใด ๆ (เช่นการพึ่งพาเนทีฟที่หายไป) ปรากฏตั้งแต่ต้น, ทำให้การดีบักง่ายขึ้น.

## ขั้นตอนที่ 4: จำกัดการจดจำให้เป็นภาษาที่ต้องการ (อ่านข้อความจาก JPG)

หากคุณรู้ภาษาของข้อความที่สแกน—เช่นรัสเซีย—คุณสามารถเพิ่มความเร็วและความแม่นยำได้โดยตั้งค่า `Language` property. สิ่งนี้มีประโยชน์อย่างยิ่งเมื่อคุณ **อ่านข้อความจาก jpg** ที่มีอักษรซีริลลิก.

```csharp
// Step 4: Limit recognition to the Russian language pack (ISO code "ru")
ocrEngine.Language = OcrLanguage.Russian;
```

เบื้องหลัง Aspose OCR จะดาวน์โหลดแพคภาษารัสเซียครั้งแรกที่รันบรรทัดนี้. ครั้งต่อ ๆ ไปจะใช้แพคที่แคชไว้, ดังนั้นไม่มีค่าใช้จ่ายเครือข่ายหลังจากดาวน์โหลดครั้งแรก.

> **ทำไมต้องล็อกภาษา?**  
> * **Performance:** Engine จะข้ามการสแกนอักขระที่อยู่นอกอักษรที่เลือก.  
> * **Accuracy:** ใช้ heuristic เฉพาะภาษา (เช่นความถี่ของคำทั่วไป) เพื่อลดการจดจำผิดพลาด.  

หากต้องการรองรับหลายภาษา, คุณสามารถส่งรายการคั่นด้วยเครื่องหมายคอมม่า, เช่น `OcrLanguage.English | OcrLanguage.Russian`.

## ขั้นตอนที่ 5: รัน OCR บนไฟล์ JPG เป้าหมาย (Run OCR on Image)

ตอนนี้เราจะ **run OCR on image** จริง ๆ. ระบุพาธเต็มของไฟล์ JPG ของคุณ—Aspose OCR รองรับหลายรูปแบบ (`.png`, `.bmp`, `.tif`, ฯลฯ), แต่ในตัวอย่างนี้เราจะใช้ `.jpg`.

```csharp
// Step 5: Perform OCR on the image containing Cyrillic text
string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";
var recognizedResult = ocrEngine.RecognizeImage(imagePath);
```

หากไฟล์ไม่พบ, `RecognizeImage` จะโยน `FileNotFoundException`. เพื่อทำให้บทเรียนนี้ทนทาน, ให้ห่อการเรียกในบล็อก try‑catch:

```csharp
try
{
    var recognizedResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("✅ OCR succeeded!");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(recognizedResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ Error during OCR: {ex.Message}");
}
```

เมธอด `RecognizeImage` จะคืนค่าเป็นอ็อบเจ็กต์ `OcrResult` ที่มี property `Text` เก็บข้อความที่สกัดออกมา. คุณยังสามารถเข้าถึง `Boxes` เพื่อรับข้อมูล bounding‑box หากต้องการข้อมูลการจัดวางในภายหลัง.

## ขั้นตอนที่ 6: ตรวจสอบผลลัพธ์

เมื่อคุณรันโปรแกรม (`dotnet run`), คุณควรเห็นผลลัพธ์ประมาณนี้:

```
✅ OCR succeeded!
Extracted text:
Пример текста на кириллице
```

หากผลลัพธ์ดูเป็นอักขระผสม, ตรวจสอบให้แน่ใจว่าภาพชัดเจนและคุณเลือกภาษาที่ถูกต้อง. ภาพเบลอหรือคอนทราสต์ต่ำเป็นสาเหตุหลักของผล OCR ที่แย่.

### กรณีขอบและคำถามทั่วไป

| สถานการณ์ | วิธีทำ |
|-----------|------------|
| **ภาพมีหลายภาษา** | ตั้งค่า `ocrEngine.Language` เป็นการผสม, เช่น `OcrLanguage.English | OcrLanguage.Russian`. |
| **ประมวลผลชุดภาพขนาดใหญ่** | ใช้ `OcrEngine` ตัวเดียวกันซ้ำสำหรับหลายไฟล์; มันจะเก็บข้อมูลภาษาไว้ในแคช. |
| **รันบนเซิร์ฟเวอร์แบบไม่มี UI** | ไม่ต้องการ UI—Aspose OCR ทำงานได้ดีใน Docker หรือ Azure Functions. |
| **ต้องการความแม่นยำสูงขึ้น** | ปรับ `ocrEngine.Options` (เช่น `ocrEngine.Options.Denoise = true`). |
| **รูปแบบไฟล์ไม่รองรับ** | แปลงภาพเป็นรูปแบบที่รองรับ (PNG หรือ JPG) ก่อนเรียก `RecognizeImage`. |

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางทั้งหมดซึ่งรวมทุกขั้นตอนที่กล่าวมา. บันทึกเป็น `Program.cs` แล้วรันจากคอมมานด์ไลน์.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (downloads language packs on first use)
            var ocrEngine = new OcrEngine();

            // 2️⃣ Restrict recognition to Russian – speeds up processing and boosts accuracy
            ocrEngine.Language = OcrLanguage.Russian;

            // 3️⃣ Path to the JPG you want to read text from
            string imagePath = @"YOUR_DIRECTORY/cyrillic_sample.jpg";

            // 4️⃣ Perform OCR and handle possible errors
            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("✅ OCR completed successfully.");
                Console.WriteLine("🖼️ Extracted text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ Failed to extract text from image: {ex.Message}");
            }
        }
    }
}
```

**ผลลัพธ์คอนโซลที่คาดหวัง** (สมมติว่าภาพตัวอย่างมีข้อความ “Пример текста на кириллице”):

```
✅ OCR completed successfully.
🖼️ Extracted text:
Пример текста на кириллице
```

หากคุณเปลี่ยนภาพเป็นรูปภาษาอังกฤษและแก้ `ocrEngine.Language = OcrLanguage.English;`, โค้ดเดียวกันจะ **อ่านข้อความจาก jpg** เป็นภาษาอังกฤษโดยไม่ต้องแก้ไขเพิ่มเติม.

## โบนัส: รัน OCR บนหลายไฟล์

บ่อยครั้งคุณอาจต้อง **run OCR on image** จำนวนหลายไฟล์. นี่คือตัวอย่างสั้น ๆ ที่วนลูปผ่านโฟลเดอร์:

```csharp
string folder = @"YOUR_DIRECTORY";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    try
    {
        var result = ocrEngine.RecognizeImage(file);
        Console.WriteLine($"[{System.IO.Path.GetFileName(file)}] => {result.Text}");
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Error processing {file}: {ex.Message}");
    }
}
```

Engine จะใช้แพคภาษาที่ดาวน์โหลดไว้แล้ว, ทำให้การประมวลผลเป็นชุดทำได้อย่างมีประสิทธิภาพ.

## สรุป

คุณมีแพทเทิร์นที่มั่นคงและพร้อมใช้งานในระดับ production สำหรับ **สกัดข้อความจากภาพ** ด้วย Aspose OCR ใน C# แล้ว. บทเรียนนี้ครอบคลุมตั้งแต่การติดตั้งแพคเกจ NuGet ไปจนถึงการจัดการข้อผิดพลาดและการขยายเป็นหลายไฟล์. ไม่ว่าคุณจะ **อ่านข้อความจาก jpg** assets, สแกน PDF, หรือสร้าง pipeline การทำงานอัตโนมัติของเอกสาร, วิธีเดียวกันนี้ก็ใช้ได้—เพียงสลับแพคภาษา หรือปรับตัวเลือก OCR ตามต้องการ.

พร้อมก้าวต่อไปหรือยัง? ลอง:

* ทดลองกับภาษาอื่น (เช่น `OcrLanguage.ChineseSimplified`).  
* สกัดข้อมูลการจัดวางผ่าน `recognizedResult.Boxes`.  
* ผสานกระบวนการ OCR เข้าไปใน ASP.NET Core API เพื่อให้บริการอื่น ๆ สามารถขอสกัดข้อความได้ตามต้องการ.

ขอให้เขียนโค้ดสนุกและภาพของคุณมีความคมชัดพอสำหรับ OCR ที่สมบูรณ์แบบเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}