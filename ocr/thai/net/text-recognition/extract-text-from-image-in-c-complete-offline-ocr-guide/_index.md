---
category: general
date: 2026-03-18
description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C#. เรียนรู้วิธีดึงข้อความ, รันการจดจำ
  OCR และจดจำข้อความ Cyrillic โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ต.
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: th
og_description: ดึงข้อความจากภาพด้วย Aspose OCR. คู่มือขั้นตอนต่อขั้นตอนในการใช้งานการจดจำ
  OCR, วิธีดึงข้อความ, และการจดจำข้อความ Cyrillic แบบออฟไลน์.
og_title: ดึงข้อความจากภาพใน C# – คู่มือ OCR แบบออฟไลน์
tags:
- C#
- OCR
- Aspose
- Image Processing
title: ดึงข้อความจากภาพใน C# – คู่มือ OCR แบบออฟไลน์ครบถ้วน
url: /th/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# สกัดข้อความจากรูปภาพ – คู่มือ OCR แบบออฟไลน์เต็มรูปแบบ

เคยต้องการ **สกัดข้อความจากรูปภาพ** แต่กังวลเรื่องความหน่วงของเครือข่ายหรือข้อจำกัดด้านลิขสิทธิ์หรือไม่? คุณไม่ได้เป็นคนเดียว นักพัฒนาหลายคนเจออุปสรรคเมื่อแอปของพวกเขาต้องทำงานในสภาพแวดล้อมแบบแซนด์บ็อกซ์ แต่ยังต้องการ OCR ที่เชื่อถือได้ ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถรันกระบวนการทั้งหมดบนเครื่องท้องถิ่น, **สกัดข้อความจากรูปภาพ** โดยไม่ต้องเชื่อมต่ออินเทอร์เน็ตเลย

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างเชิงปฏิบัติที่แสดง **วิธีสกัดข้อความ**, ตั้งค่าเครื่องมือ OCR แบบออฟไลน์, **รันการจดจำ OCR**, และแม้กระทั่ง **จดจำข้อความซีริลลิก**. เมื่อจบคุณจะมีแอปคอนโซล C# ที่พร้อมรันและพิมพ์สตริงที่ตรวจพบตรงไปที่คอนโซล

## สิ่งที่คุณต้องการ

- .NET 6.0 SDK (หรือเวอร์ชัน .NET ล่าสุดใดก็ได้)  
- Visual Studio 2022 หรือ VS Code – ตามที่คุณชอบ  
- Aspose.OCR for .NET NuGet package  
- โฟลเดอร์ที่บรรจุไฟล์โมเดล Aspose OCR (ดาวน์โหลดครั้งเดียวจากพอร์ทัลของ Aspose)  
- ไฟล์รูปภาพที่มีอักขระภาษาอังกฤษและซีริลลิก (เช่น `cyrillic_doc.jpg`)

ไม่มีบริการภายนอก, ไม่มีการดาวน์โหลดลับในขณะรัน – ทุกอย่างอยู่บนดิสก์ของคุณ

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และเตรียมทรัพยากร

ก่อนอื่นให้เพิ่มแพ็กเกจ Aspose.OCR NuGet ลงในโปรเจกต์ของคุณ:

```bash
dotnet add package Aspose.OCR
```

ต่อไปให้สร้างโฟลเดอร์ชื่อ `AsposeOCRResources` ที่ใดก็ได้บนเครื่องของคุณและคัดลอกไฟล์โมเดลที่คุณดาวน์โหลดจาก Aspose ไปใส่ในนั้น. เครื่องมือ OCR จะมองหาแพ็คภาษาในไดเรกทอรีนี้, ดังนั้นตรวจสอบให้แน่ใจว่าเส้นทางถูกต้อง

> **เคล็ดลับ:** เก็บโฟลเดอร์ทรัพยากรไว้ข้างไฟล์ `.csproj` ของคุณ; จะทำให้การจัดการเส้นทางง่ายขึ้นในระหว่างการพัฒนา

## ขั้นตอนที่ 2: สร้างเครื่องมือ OCR แบบออฟไลน์

ตอนนี้เราจะสร้างอินสแตนซ์ของเครื่องมือและชี้ไปที่โฟลเดอร์ทรัพยากร. นี่คือขั้นตอนสำคัญที่ทำให้เราสามารถ **รันการจดจำ OCR** ได้โดยเต็มรูปแบบออฟไลน์

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

ทำไมต้องโหลดภาษาตรงนี้? เพราะเราได้บอกเครื่องมือให้ทำงานออฟไลน์; มันจะไม่ติดต่อเซิร์ฟเวอร์ของ Aspose เพื่อดึงแพ็คที่หายไป. หากคุณลืมโหลดภาษาหนึ่ง, อักขระจากสคริปต์นั้นจะถูกละเว้น

## ขั้นตอนที่ 3: ส่งภาพให้กับเครื่องมือ

เมื่อเครื่องมือพร้อมแล้ว เราจะให้ภาพที่ต้องการประมวลผล. ตัวช่วย `ImageStream.FromFile` จะอ่านไฟล์และแปลงเป็นรูปแบบที่เครื่องมือ OCR เข้าใจ

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

หากภาพของคุณมีขนาดใหญ่, พิจารณาเปลี่ยนขนาดก่อนเพื่อเพิ่มความเร็วและความแม่นยำ. เครื่องมือ OCR ทำงานดีที่สุดที่ DPI ประมาณ 300

## ขั้นตอนที่ 4: ดำเนินการกระบวนการจดจำ

การเรียก `Recognize` จะทำงานหนักให้. เมธอดนี้คืนค่าอ็อบเจ็กต์ `OcrResult` ที่บรรจุสตริงที่สกัดได้, คะแนนความเชื่อมั่น, และข้อมูลอื่น ๆ

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

เบื้องหลัง, Aspose จะทำการพาร์สบิตแมพ, รันเครือข่ายประสาทเทียมตามภาษาที่กำหนด, แล้วต่ออักขระเข้าด้วยกัน. เนื่องจากเราโหลดทั้งภาษาอังกฤษและซีริลลิก, เอกสารที่มีสคริปต์ผสมจะถูกจัดการอย่างราบรื่น

## ขั้นตอนที่ 5: แสดงข้อความที่สกัดได้

สุดท้ายเราจะพิมพ์ผลลัพธ์. ในแอปจริงคุณอาจเก็บไว้ในฐานข้อมูลหรือส่งต่อให้บริการอื่น, แต่สำหรับการสาธิตนี้เราจะพิมพ์ออกเท่านั้น

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

การรันโปรแกรมควรให้ผลลัพธ์คล้ายกับ:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

หากคุณเห็นอักขระเป็นกลุ่มสับสน, ตรวจสอบอีกครั้งว่าแพ็คภาษาซีริลลิกวางอยู่ในโฟลเดอร์ทรัพยากรอย่างถูกต้องและภาพไม่เบลอเกินไป

![ตัวอย่างการสกัดข้อความจากรูปภาพ](extract_text_image.png "สกัดข้อความจากรูปภาพ")

*ข้อความแทนภาพ: สกัดข้อความจากรูปภาพ – ผลลัพธ์ OCR แสดงบรรทัดภาษาอังกฤษและซีริลลิก*

## การจัดการกับปัญหาที่พบบ่อย

### ไฟล์ภาษาไม่พบ

หากคุณได้รับข้อยกเว้นที่บอกว่า “Language data not found,” เครื่องมือไม่สามารถหาไฟล์โมเดลได้. ตรวจสอบ `ResourcesPath` และให้แน่ใจว่าโฟลเดอร์มีไฟล์ `english.dat` และ `cyrillic.dat` (หรือไฟล์ที่มีชื่อคล้ายกัน)

### คะแนนความเชื่อมั่นต่ำ

บางครั้งเครื่องมือ OCR จะให้คะแนนความเชื่อมั่นต่ำสำหรับอักขระบางตัว, โดยเฉพาะเมื่อภาพมีสัญญาณรบกวน. คุณสามารถปรับปรุงความแม่นยำได้โดย:

- แปลงภาพเป็นระดับสีเทาก่อนส่งให้เครื่องมือ  
- ใช้ฟิลเตอร์มัธยฐานเพื่อลดจุดรบกวน  
- ตรวจสอบให้ข้อความอยู่ในแนวนอน (หมุนหากจำเป็น)

### ภาพขนาดใหญ่

การประมวลผลภาพ 10 MP อาจช้า. ลดขนาดลงให้ความกว้างสูงสุดที่ 2000 px พร้อมคงอัตราส่วน; เครื่องมือยังคงจับอักขระส่วนใหญ่ได้อย่างแม่นยำ

## การขยายตัวอย่าง

- **Batch processing:** ห่อรอบตรรกะการจดจำในลูปที่วนผ่านไฟล์ทั้งหมดในไดเรกทอรี  
- **Output formats:** `OcrResult` ยังให้คอลเลกชัน `TextLines` ที่มีกรอบล้อมรอบ – มีประโยชน์สำหรับการไฮไลท์ข้อความในแอป UI  
- **Additional languages:** เพียงเรียก `LoadLanguage` พร้อมค่าที่ enum รองรับอื่น (เช่น `Language.French`)  

การขยายเหล่านี้ทั้งหมดยังคงสอดคล้องกับหลักการ **วิธีสกัดข้อความ** – เพียงโหลดแพ็คภาษาให้ตรงและให้เครื่องมือทำส่วนที่เหลือ

## สรุปโค้ดต้นฉบับทั้งหมด

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วางเต็มรูปแบบ. แทนที่ `YOUR_DIRECTORY` ด้วยเส้นทางจริงบนเครื่องของคุณ

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

บันทึกไฟล์นี้เป็น `Program.cs`, รัน `dotnet run`, แล้วดูคอนโซลพิมพ์ข้อความที่เครื่องมือดึงจากภาพของคุณ. เพียงเท่านี้ – คุณได้ **สกัดข้อความจากรูปภาพ** แบบออฟไลน์สำเร็จแล้ว

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **สกัดข้อความจากรูปภาพ** ด้วย Aspose OCR ในสถานการณ์ออฟไลน์เต็มรูปแบบ. คู่มือแสดง **วิธีสกัดข้อความ**, สาธิต **การรันการจดจำ OCR**, และพิสูจน์ว่าคุณสามารถ **จดจำข้อความซีริลลิก** ควบคู่กับภาษาอังกฤษโดยไม่ต้องเรียกใช้เครือข่ายใด ๆ  

ตั้งแต่การตั้งค่าแพ็กเกจ NuGet ไปจนถึงการจัดการกรณีขอบเช่นไฟล์ภาษาไม่พบ, ตอนนี้คุณมีพื้นฐานแข็งแรงสำหรับการสร้างฟีเจอร์ที่ใช้ OCR ในแอป .NET ใด ๆ  

ต่อไปทำอะไร? ลองป้อน PDF, สแกนหลายหน้า, หรือเชื่อมต่อผลลัพธ์กับดัชนีการค้นหา. ท้องฟ้าเป็นขีดจำกัดเมื่อคุณเชี่ยวชาญ OCR แบบออฟไลน์

ขอให้เขียนโค้ดสนุกสนาน, และขอให้ภาพของคุณใสสะอาดเสมอ!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}