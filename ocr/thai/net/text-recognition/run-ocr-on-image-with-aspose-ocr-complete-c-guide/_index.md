---
category: general
date: 2026-02-17
description: เรียกใช้ OCR บนภาพด้วย Aspose OCR ใน C# เรียนรู้วิธีดึงข้อความจากไฟล์
  JPG, เตรียมภาพสำหรับ OCR, และโหลดภาพสำหรับ OCR ด้วยโค้ดทีละขั้นตอน.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: th
og_description: ทำ OCR บนรูปภาพโดยใช้ Aspose OCR ใน C# คู่มือนี้จะแสดงวิธีดึงข้อความจากไฟล์
  JPG, เตรียมภาพล่วงหน้า, และโหลดรูปภาพสำหรับ OCR.
og_title: เรียกใช้ OCR บนภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
tags:
- Aspose OCR
- C#
- Image Processing
title: เรียกใช้ OCR บนภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์
url: /th/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# รัน OCR บนรูปภาพด้วย Aspose OCR – คู่มือ C# ฉบับสมบูรณ์

เคยต้อง **รัน OCR บนไฟล์รูปภาพ** แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรหรือไม่? ในหลายแอปพลิเคชันจริง – เช่น เครื่องสแกนใบแจ้งหนี้หรือแอปติดตามใบเสร็จ – อุปสรรคแรกคือการดึงข้อความที่เชื่อถือได้ออกจาก JPEG ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถ **รัน OCR บนไฟล์รูปภาพ** ได้ด้วยเพียงไม่กี่บรรทัดของโค้ด C# และคุณยังจะได้เรียนรู้วิธี **extract text from jpg**, **preprocess image for OCR**, และ **load image for OCR** โดยไม่ต้องค้นหาเอกสารกระ散

ในบทแนะนำนี้เราจะเดินผ่านตัวอย่างเต็มรูปแบบที่พร้อมคัดลอก‑วาง ที่แสดงอย่างชัดเจนว่าตั้งค่าเอนจินอย่างไร, เพิ่มฟิลเตอร์การเตรียมข้อมูลที่เป็นประโยชน์, ป้อนรูปภาพเข้าสู่ recognizer, และพิมพ์ผลลัพธ์ไปยังคอนโซล. เมื่อเสร็จแล้วคุณจะมีโปรแกรมที่สามารถนำไปใส่ในโปรเจกต์ .NET ใดก็ได้และเริ่มดึงข้อความจากรูปภาพได้ทันที

## สิ่งที่คุณต้องเตรียม

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานบน .NET Core ด้วย)  
- แพคเกจ NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- ตัวอย่าง JPEG (`input.jpg`) ที่วางไว้ในโฟลเดอร์ที่คุณอ้างอิงได้  
- ความเข้าใจพื้นฐานเกี่ยวกับไวยากรณ์ C# (ไม่มีอะไรซับซ้อน)

หากคุณมีสิ่งเหล่านี้แล้ว เยี่ยม – มาเริ่มกันเลย. หากยังไม่มี ให้ดาวน์โหลดแพคเกจ NuGet และรูปภาพทดสอบ; ส่วนที่เหลือของคู่มือสมมติว่าคุณทำแล้ว

## ขั้นตอนที่ 1: สร้าง OCR Engine – แกนหลักของการรัน OCR บนรูปภาพ

สิ่งแรกที่คุณต้องทำเพื่อ **รัน OCR บนข้อมูลรูปภาพ** คือสร้างอินสแตนซ์ของ `OcrEngine`. อ็อบเจกต์นี้เก็บการตั้งค่าและสถานะทั้งหมดที่จำเป็นสำหรับการจดจำ

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **ทำไมจึงสำคัญ:** `OcrEngine` คือประตูสู่ pipeline การจดจำของ Aspose. หากไม่มีคุณจะไม่สามารถเข้าถึงฟิลเตอร์, language pack, หรือเมธอด `Recognize` ได้

## ขั้นตอนที่ 2: เพิ่มฟิลเตอร์การเตรียมข้อมูล – เพิ่มความแม่นยำเมื่อคุณ **extract text from jpg**

รูปภาพที่ได้ตรงจากกล้องมักไม่สมบูรณ์. มุมเอียงหรือเม็ดสีสุ่มอาจทำให้แม้แต่ OCR ที่ดีที่สุดก็สับสน. การเพิ่มฟิลเตอร์สองสามตัวก่อนที่คุณจะ **extract text from jpg** สามารถปรับปรุงผลลัพธ์ได้อย่างมาก

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **เคล็ดลับ:** หากรูปภาพต้นทางของคุณสะอาดแล้ว คุณสามารถข้าม `DenoiseGaussianFilter` ได้. การทำ smoothing มากเกินไปอาจลบอักขระที่จางหายไป

## ขั้นตอนที่ 3: โหลดรูปภาพสำหรับ OCR – ป้อน JPEG ให้กับเอนจิน

ต่อมาคือขั้นตอนที่คุณ **load image for OCR**. Aspose มีตัวช่วย `ImageStream.FromFile` ที่ห่อเส้นทางไฟล์เป็นสตรีมที่เอนจินเข้าใจ

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **กรณีขอบ:** หากไฟล์ไม่พบ, `FromFile` จะโยน `FileNotFoundException`. ควรห่อการเรียกใน try/catch หากคาดว่าจะมีไฟล์หายระหว่างรัน

## ขั้นตอนที่ 4: ดึงและแสดงข้อความที่จดจำได้

สุดท้าย, เมื่อเอนจินทำงานเสร็จ, คุณสามารถเข้าถึงผลลัพธ์เป็นข้อความธรรมดาผ่านคุณสมบัติ `Text`. การพิมพ์ลงคอนโซลเพียงพอสำหรับการสาธิตอย่างรวดเร็ว, แต่คุณก็สามารถบันทึกลงฐานข้อมูลหรือไฟล์ข้อความได้เช่นกัน

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ผลลัพธ์ที่คาดหวัง**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

เนื้อหาโดยละเอียดจะขึ้นอยู่กับรูปภาพที่คุณป้อน, แต่คุณควรเห็นบล็อกข้อความที่จัดรูปแบบอย่างดีแทนที่จะเป็นอักขระไร้ความหมาย

![Diagram showing the OCR pipeline – run OCR on image, preprocess, load, recognize](/images/ocr-pipeline.png "run OCR on image pipeline diagram")

### ทำไมแต่ละขั้นตอนจึงสำคัญ

| ขั้นตอน | วัตถุประสงค์ | จะเกิดอะไรหากข้ามขั้นตอนนี้ |
|------|---------|--------------------------|
| **สร้างเอนจิน** | เริ่มต้นโครงสร้างภายใน | ไม่มี recognizer – จะเกิด `NullReferenceException`. |
| **เพิ่มฟิลเตอร์** | ปรับปรุงความแม่นยำโดยแก้ไขการหมุนและสัญญาณรบกวน | รูปภาพเอียงหรือมีสัญญาณรบกวนจะให้ผลลัพธ์เป็นข้อความยุ่งยาก |
| **โหลดรูปภาพ** | ส่งบิตแมพดิบให้เอนจิน | เอนจินไม่มีข้อมูลจะทำให้ฟิลด์ `Text` ว่างเปล่า |
| **อ่านผลลัพธ์** | ดึงสตริงข้อความธรรมดาเพื่อใช้งานต่อ | คุณรัน OCR แต่ไม่เห็นผลลัพธ์ – ไม่ค่อยมีประโยชน์! |

## ความแปรผันทั่วไป & วิธีปรับกระบวนการ

### เปลี่ยน Language Pack

Aspose OCR รองรับหลายภาษาโดยตรง. หากคุณต้องการ **รัน OCR บนไฟล์รูปภาพ** ที่มีข้อความเป็นภาษาฝรั่งเศสหรือเยอรมัน, ตั้งค่า `Language` ก่อนเรียก `Recognize`

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### จัดการกับ PDF หลายหน้า

หากแหล่งข้อมูลของคุณเป็น PDF หลายหน้าแทน JPEG เดียว, คุณสามารถแปลงแต่ละหน้าเป็นรูปภาพก่อน (ใช้ Aspose.PDF) แล้วป้อนแต่ละรูปภาพเข้าสู่ pipeline เดียวกัน. การวนลูปผ่านหน้าเป็นเรื่องง่าย:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### จัดการไฟล์ขนาดใหญ่

เมื่อประมวลผลรูปภาพความละเอียดสูง, การใช้หน่วยความจำอาจพุ่งสูง. พิจารณาลดขนาดภาพก่อนที่คุณจะ **load image for OCR**:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## ตัวอย่างเต็มพร้อมรัน

ด้านล่างเป็นโปรแกรมครบชุดที่รวมทุกอย่างที่เราได้พูดถึง. คัดลอก‑วางลงในโปรเจกต์คอนโซลใหม่, แทนที่ `YOUR_DIRECTORY` ด้วยโฟลเดอร์ที่เก็บ `input.jpg`, แล้วกด **F5**

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### ตรวจสอบผลลัพธ์

1. รันโปรแกรม.  
2. ตรวจสอบคอนโซล – คุณควรเห็นข้อความที่อยู่บน `input.jpg`.  
3. หากผลลัพธ์ดูเป็นอักขระสับสน, ลองปรับค่า `Sigma` ของ `DenoiseGaussianFilter` หรือเพิ่มฟิลเตอร์อื่น ๆ เช่น `ContrastEnhancementFilter`.

## สรุป & ขั้นตอนต่อไป

เราได้อธิบายวิธี **รัน OCR บนไฟล์รูปภาพ** ด้วย Aspose OCR ตั้งแต่การตั้งค่าเอนจินจนถึงการได้ข้อความที่สะอาดและอ่านง่าย. จุดสำคัญที่ควรจำ:

- สร้างอินสแตนซ์ `OcrEngine`.  
- **Preprocess image for OCR** ด้วยฟิลเตอร์เช่น `DeskewFilter` และ `DenoiseGaussianFilter`.  
- **Load image for OCR** ด้วย `ImageStream.FromFile`.  
- เรียก `Recognize` และอ่าน `ocrResult.Text` เพื่อ **extract text from jpg**.

ต้องการก้าวต่อ? ลองไอเดียต่อไปนี้:

- **ประมวลผลเป็นชุด** – อ่านโฟลเดอร์ของ JPEG ทั้งหมดและบันทึกผลลัพธ์แต่ละไฟล์เป็น `.txt` แยกกัน.  
- **รวมกับ Azure Blob Storage** – ดึงรูปภาพจากคลาวด์, รัน OCR, แล้วเก็บข้อความกลับไป.  
- **ผสานกับ NLP** – ส่งข้อความที่ดึงมาให้โมเดลความเข้าใจภาษาวิเคราะห์เพื่อจัดหมวดหมู่อัตโนมัติ เช่น ใบแจ้งหนี้.  

อย่ากลัวทดลองผสมฟิลเตอร์ต่าง ๆ, language pack, หรือแม้กระทั่งเปลี่ยนเป็น PNG และ TIFF – pipeline เดียวกันทำงานได้ตราบใดที่คุณ **load image for OCR** อย่างถูกต้อง

---

หากคุณเจอปัญหาใด ๆ, แสดงความคิดเห็นด้านล่างหรือดูเอกสาร Aspose OCR สำหรับการตั้งค่าขั้นสูง. Happy coding, และสนุกกับการแปลงรูปภาพให้เป็นข้อความที่ค้นหาได้!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}