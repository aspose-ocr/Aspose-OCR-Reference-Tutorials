---
category: general
date: 2026-03-13
description: วิธีทำ OCR ใน C# และดึงข้อความจากภาพโดยใช้ OcrEngine เรียนรู้การแปลงภาพเป็นข้อความอย่างรวดเร็วด้วยคู่มือขั้นตอนเต็มรูปแบบ
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- read text from picture
- how to extract text
language: th
og_description: วิธีทำ OCR ใน C#? คู่มือนี้จะแสดงวิธีดึงข้อความจากภาพ, แปลงภาพเป็นข้อความ,
  และอ่านข้อความจากรูปภาพโดยใช้ OcrEngine.
og_title: วิธีทำ OCR ใน C# – แยกข้อความจากรูปภาพ
tags:
- OCR
- C#
- Image Processing
title: วิธีทำ OCR ใน C# – แยกข้อความจากรูปภาพ
url: /th/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีทำ OCR ใน C# – แยกข้อความจากรูปภาพ

การทำ OCR ใน C# เป็นคำถามที่พบบ่อยสำหรับนักพัฒนาที่ต้อง **อ่านข้อความจากรูปภาพ** ไฟล์ ในคู่มือนี้เราจะพาคุณผ่านการแยกข้อความจากรูปภาพโดยใช้ไลบรารี `OcrEngine` เปลี่ยนรูปภาพให้เป็นสตริงที่สามารถค้นหาได้ด้วยเพียงไม่กี่บรรทัดของโค้ด  

หากคุณเคยมองใบแจ้งหนี้ที่สแกน, โน้ตมือเขียน, หรือภาพหน้าจอและสงสัย *“ฉันจะดึงข้อความออกมาอย่างไร?”* คุณมาถูกที่แล้ว เราจะพูดถึงการแปลงรูปภาพเป็นข้อความสำหรับการประมวลผลแบบแบตช์ เพื่อให้คุณสามารถอัตโนมัติกระบวนการทั้งหมดได้

---

## สิ่งที่คุณต้องการ

- **.NET 6.0 หรือใหม่กว่า** (API ที่เราใช้ทำงานกับ .NET Standard 2.0+)
- **แพ็คเกจ NuGet OcrEngine** (หรือไลบรารี OCR ที่เข้ากันได้ซึ่งเปิดเผยคุณสมบัติ `Language`, `Image`, `Recognize`, และ `Text`)
- ไฟล์รูปภาพตัวอย่าง เช่น `hindi_page.jpg` ที่วางไว้ในโฟลเดอร์ที่คุณสามารถอ้างอิงจากโค้ด
- ความเข้าใจพื้นฐานของไวยากรณ์ C# – ไม่ต้องการเทคนิคขั้นสูง

เท่านี้เอง ไม่ต้องใช้บริการภายนอก ไม่ต้องใช้คีย์ API เพียงไลบรารีในเครื่องที่ทำงานหนักให้คุณ

---

## การดำเนินการทีละขั้นตอน

ด้านล่างเราจะแบ่งกระบวนการออกเป็นส่วนย่อยที่มีตรรกะ แต่ละส่วนมีหัวข้อชัดเจน, โค้ดสั้น ๆ, และคำอธิบายว่า **ทำไม** ขั้นตอนนี้สำคัญ—not just **what** it does.

### วิธีทำ OCR – ขั้นตอนหลัก

กระบวนการโดยรวมสามารถสรุปได้ในห้าการกระทำ:

1. **Create** ตัวอย่างของ OCR engine
2. **Select** ภาษาที่คุณต้องการจดจำ
3. **Load** รูปภาพที่มีข้อความ
4. **Run** อัลกอริทึมการจดจำ
5. **Read** ข้อความที่แยกออกมา

นั่นคือโครงกระดูก; ส่วนต่อไปนี้จะขยายรายละเอียด

---

### แยกข้อความจากรูปภาพ – สร้าง Engine

First, we need an object that knows how to talk to the OCR engine.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

*ทำไมจึงสำคัญ:* การสร้างอินสแตนซ์ `OcrEngine` จะจัดสรรบัฟเฟอร์ภายในทั้งหมดและโหลด DLL เนทีฟที่จำเป็นสำหรับการวิเคราะห์ภาพ การข้ามขั้นตอนนี้จะทำให้คุณไม่มี recognizer ที่จะเรียกใช้ต่อไป  

> **เคล็ดลับ:** หากคุณวางแผนจะประมวลผลหลายรูปภาพต่อเนื่อง ให้คงอินสแตนซ์ `ocrEngine` เดิมไว้ มันจะใช้โมเดลภาษาเดิมซ้ำและเร่งความเร็วการเรียกครั้งต่อไป

### แปลงรูปภาพเป็นข้อความ – เลือกภาษา

OCR accuracy heavily depends on the language model you feed it. For Hindi, Tamil, or any other script, set the `Language` property accordingly.

```csharp
// Step 2: Select the language of the text to recognize (e.g., Hindi)
ocrEngine.Language = Language.Hindi;   // You can also use Language.Tamil, Language.English, etc.
```

*ทำไมจึงสำคัญ:* Engine ใช้ชุดอักขระและโมเดลสถิติที่เฉพาะเจาะจงตามภาษา การระบุภาษาที่ผิดพลาดมักทำให้ผลลัพธ์เป็นข้อความเสียหาย โดยเฉพาะสคริปต์ที่ไม่ใช่ละติน  

> **กรณีพิเศษ:** หากคุณต้องการสนับสนุนหลายภาษา บางไลบรารีให้คุณตั้งรายการ fallback เช่น `ocrEngine.Language = Language.Multilingual;`.

### อ่านข้อความจากรูปภาพ – โหลดภาพต้นฉบับ

Now we point the engine at the file that holds the visual text.

```csharp
// Step 3: Load the image that contains the text
ocrEngine.Image = ImageStream.FromFile(@"C:\OCR\Samples\hindi_page.jpg");
```

*ทำไมจึงสำคัญ:* `ImageStream.FromFile` แปลงไฟล์ดิบเป็นรูปแบบบิตแมพที่แกน OCR เข้าใจ การให้ไฟล์ที่เสียหายหรือรูปแบบที่ไม่รองรับ (เช่น SVG) จะทำให้เกิดข้อยกเว้น  

> **ระวัง:** รูปภาพขนาดใหญ่อาจใช้หน่วยความจำมาก หากคุณประมวลผลสแกนความละเอียดสูง ควรลดขนาดด้วย `Image.Resize` ก่อนส่งให้ engine

### แปลงรูปภาพเป็นข้อความ – รันการจดจำ

With the engine ready and the image loaded, we finally invoke the OCR process.

```csharp
// Step 4: Perform the OCR operation
ocrEngine.Recognize();
```

*ทำไมจึงสำคัญ:* `Recognize` เริ่มต้นขั้นตอนภายในหลายขั้นตอน—การเตรียมข้อมูล, การแบ่งส่วน, การจำแนกอักขระ, และการประมวลผลหลังขั้นตอน การเรียกนี้เป็นแบบบล็อก หมายความว่าเธรดจะรอจนกว่าข้อความจะพร้อม  

> **หมายเหตุประสิทธิภาพ:** บนเดสก์ท็อปทั่วไป การจดจำหน้าที่ 300 dpi ใช้เวลา < 1 วินาที บนเซิร์ฟเวอร์คุณอาจต้องรันในงานเบื้องหลังเพื่อหลีกเลี่ยง UI ค้าง

### วิธีดึงข้อความ – ดึงผลลัพธ์

Once recognition finishes, the engine stores the plain‑text output in the `Text` property.

```csharp
// Step 5: Output the recognized text
Console.WriteLine(ocrEngine.Text);
```

*ทำไมจึงสำคัญ:* คุณสมบัติ `Text` ให้สตริง UTF‑8 ที่สะอาดที่คุณสามารถเขียนลงไฟล์, ส่งเข้า DB, หรือส่งต่อไปยัง pipeline NLP  

> **ผลลัพธ์ที่คาดหวัง:** สำหรับหน้าภาษา Hindi ตัวอย่าง คุณอาจเห็นอย่างเช่น  
> `यह एक उदाहरण पाठ है जो OCR द्वारा पहचाना गया है।`  
> (ผลลัพธ์ที่แน่นอนขึ้นอยู่กับคุณภาพของภาพและโมเดลภาษา)

## พิจารณาเพิ่มเติมสำหรับโครงการจริง

ด้านล่างเป็นสถานการณ์ “what‑if” ที่คุณอาจเจอเมื่อพยายาม **แยกข้อความจากรูปภาพ** ในการผลิต

### การจัดการหลายรูปภาพในลูป

If you need to **convert image to text** for dozens of files, wrap the steps in a `foreach` loop and reuse the same `ocrEngine`:

```csharp
string[] files = Directory.GetFiles(@"C:\OCR\Batch\", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), ocrEngine.Text);
}
```

### การจัดการสแกนคุณภาพต่ำ

- **Pre‑process** ด้วยการไบนารี (`Image.Binarize()`), การกำจัดสัญญาณรบกวน, หรือการปรับแนวภาพ
- **Increase DPI** ขณะสแกน (300 dpi เป็นค่าพื้นฐานที่ปลอดภัย)
- **Choose a language model** ที่รองรับลิแกเชอร์ของสคริปต์ (เช่น Devanagari สำหรับ Hindi)

### อ่านข้อความจากรูปภาพบนเว็บ

When the image comes from a URL, download it into a memory stream first:

```csharp
using (HttpClient client = new())
{
    byte[] data = await client.GetByteArrayAsync(imageUrl);
    using var ms = new MemoryStream(data);
    ocrEngine.Image = ImageStream.FromStream(ms);
    ocrEngine.Recognize();
    Console.WriteLine(ocrEngine.Text);
}
```

### ความปลอดภัยของเธรดและการทำงานแบบขนาน

Most OCR libraries are **not** thread‑safe out of the box. If you plan to **read text from picture** concurrently, spin up separate `OcrEngine` instances per thread, or use a producer‑consumer queue to serialize access.

## ตัวอย่างการทำงานเต็มรูปแบบ

Putting everything together, here’s a ready‑to‑run console app that demonstrates **how to perform OCR**, **extract text from image**, and **read text from picture** in one cohesive program.

```csharp
using System;
using OcrLibrary;               // Adjust to your OCR library's namespace
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Choose the language (Hindi in this case)
        ocrEngine.Language = Language.Hindi;

        // Load the image file
        string imagePath = @"C:\OCR\Samples\hindi_page.jpg";
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found: {imagePath}");
            return;
        }

        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // Run the recognition process
        ocrEngine.Recognize();

        // Output the extracted text
        string result = ocrEngine.Text;
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(result);

        // Optional: Save to a .txt file
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, result);
        Console.WriteLine($"Text saved to {txtPath}");
    }
}
```

**สิ่งที่คุณควรเห็น:** คอนโซลจะแสดงประโยค Hindi ที่แยกจาก `hindi_page.jpg` ตามด้วยการยืนยันว่ามีการสร้างไฟล์ข้อความ หากภาพสะอาด ผลลัพธ์จะเหมือนกับข้อความพิมพ์ต้นฉบับอย่างแทบไม่มีความแตกต่าง

## สรุป

ตอนนี้คุณรู้แล้วว่า **วิธีทำ OCR** ใน C# ตั้งแต่ต้นจนจบ, วิธี **แยกข้อความจากรูปภาพ**, **แปลงรูปภาพเป็นข้อความ**, และ **อ่านข้อความจากรูปภาพ** ด้วย workflow `OcrEngine` ที่ง่าย ขั้นตอนห้าขั้นตอน—สร้าง, ตั้งค่าภาษา, โหลด, จดจำ, อ่าน—ครอบคลุมกรณีใช้งานส่วนใหญ่ และเคล็ดลับเพิ่มเติมช่วยให้คุณจัดการงานแบตช์, สแกนคุณภาพต่ำ, และแหล่งข้อมูลบนเว็บ  

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองเปลี่ยนภาษาเป็นอังกฤษ, ป้อนหน้า PDF ที่แปลงเป็นรูปภาพ, หรือเชื่อมต่อผลลัพธ์ OCR ไปยัง pipeline ดัชนีการค้นหา ไม่จำกัดอะไรเลยเมื่อคุณเชี่ยวชาญพื้นฐานของ OCR ใน C#  

มีคำถามหรือรูปภาพที่ยากต่อการประมวลผล? แสดงความคิดเห็นด้านล่าง แล้วเรามาแก้ไขปัญหาร่วมกัน ขอให้เขียนโค้ดสนุก!  

![how to perform OCR example](images/ocr-example.png "how to perform OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}