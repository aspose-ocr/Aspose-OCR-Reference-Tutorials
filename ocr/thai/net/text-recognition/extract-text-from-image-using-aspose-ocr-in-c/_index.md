---
category: general
date: 2026-08-09
description: ดึงข้อความจากภาพด้วย Aspose OCR ใน C# เรียนรู้วิธีโหลดภาพสำหรับ OCR ตั้งค่าภาษา
  OCR ประมวลผล OCR ของภาพ และแปลงภาพเป็นข้อความอย่างมีประสิทธิภาพ
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert image to text
- load image for ocr
- process image ocr
- set ocr language
language: th
lastmod: 2026-08-09
og_description: ดึงข้อความจากภาพโดยใช้ Aspose OCR ใน C# บทเรียนนี้แสดงวิธีโหลดภาพสำหรับ
  OCR ตั้งค่าภาษา OCR ประมวลผล OCR ของภาพ และแปลงภาพเป็นข้อความด้วยไม่กี่บรรทัดของโค้ด
og_image_alt: Screenshot of C# console output showing extracted text from an image
  using Aspose OCR
og_title: สกัดข้อความจากภาพด้วย Aspose OCR – คู่มือ C#
schemas:
- author: Aspose
  dateModified: '2026-08-09'
  description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  headline: Extract text from image using Aspose OCR in C#
  type: TechArticle
- description: Extract text from image with Aspose OCR in C#. Learn how to load image
    for OCR, set OCR language, process image OCR, and convert image to text efficiently.
  name: Extract text from image using Aspose OCR in C#
  steps:
  - name: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
    text: '**Create an OCR engine instance** – The `OcrEngine` encapsulates all OCR
      functionality. Disposing it promptly frees native resources, which is critical
      for long‑running services.'
  - name: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
    text: '**Set OCR language** – Selecting the correct language module dramatically
      improves accuracy. Aspose provides over 30 language packs; the default is English.
      The example uses Cyrillic to demonstrate a non‑Latin script.'
  - name: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
    text: '**Load image for OCR** – The engine works with an `ImageStream`. Supplying
      a high‑resolution image (≥300 dpi) reduces misrecognition, especially for complex
      scripts.'
  - name: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
    text: '**Process image OCR** – This is where the heavy lifting occurs. The method
      returns an `OcrResult` containing the extracted text, confidence scores, and
      optional layout data.'
  - name: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
    text: '**Convert image to text** – `result.Text` is a plain `string`. You can
      write it to a file, feed it into a search index, or pass it to downstream NLP
      pipelines.'
  - name: Instantiates `OcrEngine`.
    text: Instantiates `OcrEngine`.
  - name: '**Sets OCR language** to Cyrillic (or any language you choose).'
    text: '**Sets OCR language** to Cyrillic (or any language you choose).'
  - name: '**Loads image for OCR** from disk.'
    text: '**Loads image for OCR** from disk.'
  - name: '**Processes image OCR** to obtain the textual result.'
    text: '**Processes image OCR** to obtain the textual result.'
  - name: '**Converts image to text** and prints it.'
    text: '**Converts image to text** and prints it.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: สกัดข้อความจากภาพด้วย Aspose OCR ใน C#
url: /th/net/text-recognition/extract-text-from-image-using-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากรูปภาพด้วย Aspose OCR ใน C#

หากคุณต้องการ **extract text from image** ในแอปพลิเคชัน .NET คำแนะนำนี้จะพาคุณผ่านโซลูชันที่สมบูรณ์และพร้อมใช้งาน คุณจะได้เห็นวิธี **load image for OCR**, เลือกโมดูลภาษาที่เหมาะสม, เรียกใช้ OCR engine, และสุดท้าย **convert image to text** ด้วยเพียงไม่กี่บรรทัดของ C#.

บทแนะนำนี้ครอบคลุมทุกอย่างที่จำเป็นเพื่อให้ได้ผลลัพธ์ที่เชื่อถือได้กับ Aspose.OCR รวมถึงข้อผิดพลาดทั่วไปเช่นรูปแบบภาพที่ไม่รองรับและความแตกต่างตามภาษา เมื่อเสร็จสิ้นคุณจะมีโปรแกรมที่ทำงานอิสระซึ่งพิมพ์ข้อความที่ได้รับการจดจำออกทางคอนโซล

## สิ่งที่คุณจะได้ทำ

* โหลดไฟล์รูปภาพเข้าสู่ Aspose OCR engine.  
* **Set OCR language** (Cyrillic ในตัวอย่าง แต่ภาษาที่รองรับใดก็ได้ทำงานได้).  
* **Process image OCR** and obtain the textual representation.  
* **Convert image to text** and display it, ready for further processing or storage.  

**ข้อกำหนดเบื้องต้น**

* .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.6+ ด้วย).  
* Visual Studio 2022 (หรือ IDE ใดก็ได้ที่รองรับ C#).  
* Aspose.OCR NuGet package (`Install-Package Aspose.OCR`).  

---

## ดึงข้อความจากรูปภาพ – การเดินผ่านโค้ดเต็ม

ด้านล่างเป็นโปรแกรมที่สมบูรณ์และสามารถรันได้ คัดลอกไปยังโปรเจกต์คอนโซลใหม่และแทนที่ `YOUR_DIRECTORY/sample_cyrillic.jpg` ด้วยพาธของรูปภาพของคุณ

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 1: Create an OCR engine instance.
            // The using block ensures the engine is disposed correctly.
            using (var engine = new OcrEngine())
            {
                // Step 2: Set OCR language.
                // Change OcrLanguage.Cyrillic to any other supported language,
                // e.g., OcrLanguage.English, OcrLanguage.Chinese, OcrLanguage.Hindi.
                engine.Language = OcrLanguage.Cyrillic;

                // Step 3: Load image for OCR.
                // ImageStream.FromFile reads the image from disk.
                // Supported formats: JPEG, PNG, BMP, TIFF, GIF.
                engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/sample_cyrillic.jpg");

                // Step 4: Process image OCR.
                // The Process method runs the recognition engine and returns an OcrResult.
                var result = engine.Process();

                // Step 5: Convert image to text.
                // The recognized text is available via result.Text.
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

### ทำไมแต่ละขั้นตอนจึงสำคัญ

1. **Create an OCR engine instance** – `OcrEngine` รวมฟังก์ชัน OCR ทั้งหมด การทำลาย (Dispose) อย่างทันท่วงทีจะปล่อยทรัพยากรเนทีฟ ซึ่งสำคัญสำหรับบริการที่ทำงานเป็นเวลานาน  
2. **Set OCR language** – การเลือกโมดูลภาษาที่ถูกต้องจะเพิ่มความแม่นยำอย่างมาก Aspose มีแพ็คเกจภาษามากกว่า 30 แพ็ค; ค่าเริ่มต้นคือ English ตัวอย่างใช้ Cyrillic เพื่อสาธิตสคริปต์ที่ไม่ใช่ละติน  
3. **Load image for OCR** – Engine ทำงานกับ `ImageStream` การให้ภาพความละเอียดสูง (≥300 dpi) จะลดการจดจำผิดพลาด โดยเฉพาะสคริปต์ที่ซับซ้อน  
4. **Process image OCR** – ที่นี่เป็นขั้นตอนการประมวลผลหลัก เมธอดจะคืนค่า `OcrResult` ที่มีข้อความที่ดึงออกมา, คะแนนความเชื่อมั่น, และข้อมูลเลย์เอาต์เสริม  
5. **Convert image to text** – `result.Text` เป็น `string` ธรรมดา คุณสามารถเขียนลงไฟล์, ส่งเข้าอินเด็กซ์การค้นหา, หรือส่งต่อไปยัง pipeline NLP ต่อไป  

---

## โหลดภาพสำหรับ OCR

`ImageStream.FromFile` รองรับรูปแบบ raster ที่พบบ่อย หากคุณรับภาพเป็นอาเรย์ไบต์ (เช่นจากเว็บ API) ให้ใช้ `ImageStream.FromBytes(byte[])` แทน:

```csharp
byte[] imageBytes = File.ReadAllBytes("path/to/image.png");
engine.Image = ImageStream.FromBytes(imageBytes);
```

**Pro tip:** ตรวจสอบเสมอว่าภาพไม่เสียหายก่อนส่งให้ engine การตรวจสอบแบบ `try { Image.FromFile(...); } catch { ... }` อย่างรวดเร็วจะป้องกันข้อยกเว้นในเวลารัน

## ตั้งค่า OCR language

Aspose.OCR มาพร้อมกับแพ็คเกจภาษา ที่คุณสามารถเปิดใช้งานได้ในขณะรัน เพื่อแสดงรายการภาษาที่มีทั้งหมด:

```csharp
foreach (var lang in Enum.GetValues(typeof(OcrLanguage)))
{
    Console.WriteLine(lang);
}
```

หากต้องการจดจำหลายภาษาในเอกสารเดียว ให้รวมด้วยตัวดำเนินการ OR แบบบิต:

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Russian;
```

**Edge case:** การผสมภาษาขวาไปซ้าย (RTL) (เช่น Arabic) กับสคริปต์ซ้ายไปขวาอาจต้องการการจัดการเลย์เอาต์เพิ่มเติม Aspose ตรวจจับทิศทางอัตโนมัติ แต่คุณสามารถปรับแต่งได้ผ่าน `engine.PageSegmentationMode`.

## ประมวลผล OCR ของภาพ

การเรียก `Process` ทำงานแบบ synchronous และบล็อกจนกว่า engine จะเสร็จ สำหรับชุดข้อมูลขนาดใหญ่หรือแอป UI ให้พิจารณา overload แบบ asynchronous:

```csharp
var task = engine.ProcessAsync();
OcrResult result = await task;
```

**Common pitfall:** ลืมตั้งค่า `engine.Image` ก่อนเรียก `Process` จะทำให้เกิด `InvalidOperationException` ควรกำหนดภาพก่อนเสมอ

## แปลงภาพเป็นข้อความ

สตริงที่ดึงออกมาสามารถจัดการได้เช่น `string` ของ .NET ตัวอย่างเช่น การเขียนผลลัพธ์ลงไฟล์:

```csharp
File.WriteAllText("output.txt", result.Text);
```

หากต้องการรักษาการขึ้นบรรทัดใหม่ตามที่ปรากฏในภาพ ให้ใช้ `result.Text` โดยตรง สำหรับการประมวลผลต่อ (เช่น การลบช่องว่างเกิน) ให้ใช้เมธอดสตริงมาตรฐาน:

```csharp
string cleaned = result.Text
    .Replace("\r\n", "\n")
    .Trim();
```

## สรุปตัวอย่างเต็ม

เมื่อรวมทุกอย่างเข้าด้วยกัน โปรแกรมทำ:

1. สร้างอินสแตนซ์ `OcrEngine`.  
2. **Sets OCR language** to Cyrillic (or any language you choose).  
3. **Loads image for OCR** from disk.  
4. **Processes image OCR** to obtain the textual result.  
5. **Converts image to text** and prints it.  

การรันตัวอย่างด้วยภาพ Cyrillic ที่ชัดเจนจะให้ผลลัพธ์คล้ายกับ:

```
=== Recognized Text ===
Пример текста на кириллице
```

หากภาพมีข้อความภาษาอังกฤษ เพียงเปลี่ยน `engine.Language = OcrLanguage.English;` แล้วโค้ดเดียวกันจะ **extract text from image** อย่างถูกต้อง.

## สรุป

ตอนนี้คุณรู้วิธี **extract text from image** ด้วย Aspose OCR ใน C# แล้ว บทแนะนำครอบคลุมการโหลดภาพ, การเลือกภาษาเหมาะสม, การรันกระบวนการ OCR, และ **converting image to text** เพื่อการใช้งานต่อไป  

จากนี้คุณสามารถ:

* ทดลองกับภาษาอื่น (`load image for OCR` → `set OCR language` → `process image OCR`).  
* รวมขั้นตอน OCR เข้าไปใน pipeline ที่ใหญ่ขึ้น (เช่น การนำเข้าดocument, PDF ที่ค้นหาได้).  
* เพิ่มประสิทธิภาพโดยการจัดกลุ่มภาพหรือใช้ API แบบ asynchronous.  

อย่าลังเลที่จะสำรวจเอกสาร Aspose.OCR สำหรับคุณลักษณะขั้นสูง เช่น พจนานุกรมกำหนดเอง, โหมดการแบ่งหน้า, และการปรับความแม่นยำของ OCR. Happy coding!

## สิ่งที่คุณควรเรียนต่อไป?

บทแนะนำต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้ แต่ละแหล่งรวมตัวอย่างโค้ดทำงานเต็มรูปแบบพร้อมคำอธิบายขั้นตอนเพื่อช่วยให้คุณเชี่ยวชาญคุณลักษณะ API เพิ่มเติมและสำรวจแนวทางการทำงานอื่นในโปรเจกต์ของคุณ

- [ดึงข้อความจากรูปภาพ C# ด้วยการเลือกภาษาโดยใช้ Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [ดึงข้อความจากรูปภาพ – การปรับแต่ง OCR ด้วย Aspose.OCR สำหรับ .NET](/ocr/english/net/ocr-optimization/)
- [วิธีทำการดึงข้อความจากรูปภาพจากสตรีมโดยใช้ Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}