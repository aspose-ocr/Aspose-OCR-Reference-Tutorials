---
category: general
date: 2026-02-24
description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากไฟล์รูปภาพ เรียนรู้การแปลง PNG เป็นข้อความ
  การอ่านรูปภาพแบบอะซิงโครนัส และการจัดการกับข้อผิดพลาดทั่วไป
draft: false
keywords:
- how to use OCR
- extract text from image
- convert png to text
- how to extract text
- how to read image
language: th
og_description: วิธีใช้ OCR ใน C# เพื่อดึงข้อความจากภาพ คู่มือนี้แสดงขั้นตอนการทำ
  OCR แบบอะซิงโครนัสด้วย Aspose อย่างละเอียด รวมถึงการแปลง การจัดการข้อผิดพลาด และแนวปฏิบัติที่ดีที่สุด
og_title: วิธีใช้ OCR ใน C# – คู่มือครบถ้วน
tags:
- OCR
- C#
- Aspose
title: วิธีใช้ OCR ใน C# – แยกข้อความจากภาพด้วย Aspose OCR
url: /th/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ OCR ใน C# – ดึงข้อความจากรูปภาพ

เคยสงสัย **how to use OCR** ว่าจะดึงข้อความออกจากรูปภาพโดยไม่ต้องพิมพ์ด้วยตนเองหรือไม่? คุณไม่ได้เป็นคนเดียวที่คิดเช่นนั้น นักพัฒนาหลายคนเจออุปสรรคเมื่อต้อง *extract text from image* จากไฟล์เช่น PNGs และวิธีคัดลอก‑วางแบบเดิมก็ไม่เพียงพอ  

ในบทแนะนำนี้ เราจะพาไปผ่านโซลูชันแบบอะซิงโครนัสที่สมบูรณ์ซึ่ง **converts PNG to text** ด้วยไลบรารี Aspose.OCR. เมื่อจบคุณจะรู้วิธีอ่านไฟล์รูปภาพ, จัดการข้อผิดพลาด, และรวมผลลัพธ์เข้าในแอปของคุณได้อย่างแม่นยำ.  

เราจะครอบคลุมทุกอย่างตั้งแต่การตั้งค่าแพ็กเกจ NuGet ไปจนถึงการปรับแต่ง OCR engine เพื่อความแม่นยำที่ดียิ่งขึ้น และเราจะให้เคล็ดลับเมื่อภาพไม่คมชัด ไม่ต้องตามลิงก์เอกสาร—ทุกอย่างที่คุณต้องการอยู่ที่นี่.

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานบน .NET Core และ .NET Framework ด้วย)  
- Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ)  
- **Aspose.OCR** NuGet package (`Install-Package Aspose.OCR`)  
- ไฟล์รูปภาพ (PNG, JPG, BMP) ที่คุณต้องการประมวลผล – เราจะเรียกมันว่า `input.png`

เท่านี้เอง หากคุณทำเครื่องหมายครบแล้ว คุณพร้อมที่จะเริ่มได้แล้ว.

![Diagram showing OCR workflow – how to use OCR to extract text from an image](/images/ocr-workflow.png)

## ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR และเพิ่ม Namespaces

ขั้นแรก นำไลบรารีเข้ามาในโปรเจคของคุณ เปิด Package Manager Console แล้วรัน:

```powershell
Install-Package Aspose.OCR
```

จากนั้น ที่ส่วนบนของไฟล์ C# ของคุณ ให้เพิ่ม namespaces ที่จำเป็น:

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;
```

> **Pro tip:** หากคุณใช้ .NET 6 minimal APIs คุณสามารถวาง `using` statements เหล่านี้ในไฟล์ global เพื่อไม่ต้องทำซ้ำในหลายคลาส.

### ทำไมเรื่องนี้ถึงสำคัญ

`Aspose.OCR` namespace ให้คุณเข้าถึง `OcrEngine` ซึ่งเป็นคลาสหลักที่อ่านภาพจริง ๆ หากไม่มีคุณจะต้องเขียนโค้ดวิเคราะห์พิกเซลเอง—เป็นหลุมดำที่ใหญ่โต การเพิ่ม namespaces ทำให้โค้ดเป็นระเบียบและบอกคอมไพเลอร์ว่าควรหา type ที่คุณใช้จากที่ไหน.

## ขั้นตอนที่ 2: สร้าง Asynchronous OCR Engine

เราจะห่อการเรียก OCR ไว้ในเมธอด `async` เพื่อให้ UI ของคุณตอบสนองได้และโค้ดฝั่งเซิร์ฟเวอร์สามารถสเกลได้ นี่คือโครงสร้างของแอปคอนโซล:

```csharp
class AsyncExample
{
    static async Task Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Recognize text from the image asynchronously
        OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");

        // Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

### คำอธิบาย

- **`OcrEngine ocrEngine = new OcrEngine();`** – สร้างอินสแตนซ์ของ engine ด้วยการตั้งค่าเริ่มต้น คุณสามารถปรับเปลี่ยนภาษา, โหมดการตรวจจับ, หรือฟิลเตอร์การเตรียมภาพได้ในภายหลัง.  
- **`await ocrEngine.RecognizeImageAsync(...)`** – เมธอด async นี้คืนค่า `Task<OcrResult>` การ `await` จะปล่อยเธรดขณะ OCR ทำงานในพื้นหลัง.  
- **`ocrResult.Text`** – การแสดงผลเป็น plain‑text ของทุกอย่างที่ engine สามารถอ่านได้ นี่คือหัวใจของ *how to extract text* จากรูปภาพ.

## ขั้นตอนที่ 3: ปรับแต่ง Engine เพื่อความแม่นยำที่ดียิ่งขึ้น

OCR ที่ใช้ได้ทันทีทำงานดีบนภาพที่สะอาดและคอนทราสต์สูง แต่ภาพในโลกจริงมักต้องการการช่วยเหลือเล็กน้อย คุณสามารถปรับคุณสมบัติบางอย่างก่อนเรียก `RecognizeImageAsync`:

```csharp
// Set language (English is default, but you can add more)
ocrEngine.Language = OcrLanguage.English;

// Enable automatic image preprocessing (deskew, despeckle)
ocrEngine.ImagePreprocessingOptions = ImagePreprocessingOptions.Auto;

// If you only need numbers, restrict the character set
ocrEngine.Characters = "0123456789";
```

### เมื่อใดควรใช้การตั้งค่าเหล่านี้

- **Low‑quality scans** – เปิด `ImagePreprocessingOptions.Auto` เพื่อให้ Aspose ทำความสะอาดสัญญาณรบกวน.  
- **Multilingual PDFs** – เปลี่ยน `Language` เป็น `OcrLanguage.French` หรือรวมหลายภาษาโดยใช้ bitmask.  
- **Form fields** – จำกัด `Characters` ให้เป็นตัวเลขหรืออักษรพิมพ์ใหญ่เพื่อ ลด false positives.

## ขั้นตอนที่ 4: จัดการข้อผิดพลาดอย่างราบรื่น

OCR ไม่ใช่เวทมนตร์; มันอาจล้มเหลวหากไฟล์หาย, เสียหาย, หรืออยู่ในรูปแบบที่ไม่รองรับ ให้ห่อการเรียก async ด้วยบล็อก try/catch:

```csharp
try
{
    OcrResult ocrResult = await ocrEngine.RecognizeImageAsync("YOUR_DIRECTORY/input.png");
    Console.WriteLine("Extracted Text:");
    Console.WriteLine(ocrResult.Text);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"File not found: {ex.Message}");
}
catch (OcrException ex)
{
    Console.Error.WriteLine($"OCR failed: {ex.Message}");
}
```

### ทำไมสิ่งนี้ถึงช่วยได้

การให้ข้อความข้อผิดพลาดที่ชัดเจนช่วยเร่งการดีบักและปรับปรุงประสบการณ์ผู้ใช้ แทนการพังโดยทั่วไป คุณจะได้รับพรอมต์ที่บอกให้ตรวจสอบเส้นทาง, รูปแบบไฟล์, หรือการตั้งค่า OCR engine.

## ขั้นตอนที่ 5: รวมทุกอย่างเข้าด้วยกัน – ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมคอนโซลที่สมบูรณ์พร้อมรันที่แสดง **how to use OCR**, ใช้การเตรียมภาพ, และจัดการข้อผิดพลาด คัดลอกและวางลงใน `.csproj` ใหม่แล้วกด F5.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Threading.Tasks;

class AsyncOcrDemo
{
    static async Task Main()
    {
        // 1️⃣  Initialize the OCR engine with optional tweaks
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImagePreprocessingOptions = ImagePreprocessingOptions.Auto
        };

        // 2️⃣  Define the path to the image you want to read
        string imagePath = Path.Combine(Environment.CurrentDirectory, "input.png");

        // 3️⃣  Perform the async recognition inside a safe try/catch
        try
        {
            OcrResult result = await ocrEngine.RecognizeImageAsync(imagePath);
            Console.WriteLine("\n--- Extracted Text ---\n");
            Console.WriteLine(result.Text);
            Console.WriteLine("\n--- End of Output ---\n");
        }
        catch (FileNotFoundException fnf)
        {
            Console.Error.WriteLine($"❌ Image not found: {fnf.Message}");
        }
        catch (OcrException ocrEx)
        {
            Console.Error.WriteLine($"❌ OCR processing error: {ocrEx.Message}");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Unexpected error: {ex.Message}");
        }
    }
}
```

**ผลลัพธ์ที่คาดหวัง** (สมมติว่า `input.png` มีข้อความ “Hello World”):

```
--- Extracted Text ---

Hello World

--- End of Output ---
```

หากภาพเบลอ คุณอาจเห็นอักขระเพิ่มหรือคำหาย—นี่คือจุดที่ตัวเลือกการเตรียมภาพจากขั้นตอนที่ 3 มีความสำคัญ.

## ขั้นตอนที่ 6: ขยายโซลูชัน – จาก PNG ไปยัง PDF หรือไฟล์ข้อความ

บางครั้งคุณต้อง **convert PNG to text** แล้วเก็บผลลัพธ์ในไฟล์ `.txt` หรือฝังลงในรายงาน PDF นี่คือตัวอย่างสั้นที่เขียนผล OCR ลงไฟล์:

```csharp
string outputPath = Path.Combine(Environment.CurrentDirectory, "output.txt");
await File.WriteAllTextAsync(outputPath, result.Text);
Console.WriteLine($"✅ Text saved to {outputPath}");
```

หรือ หากคุณกำลังสร้าง PDF ด้วย Aspose.PDF:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// ... after OCR result is obtained
Document pdfDoc = new Document();
Page page = pdfDoc.Pages.Add();
TextFragment fragment = new TextFragment(result.Text);
page.Paragraphs.Add(fragment);
pdfDoc.Save("Result.pdf");
Console.WriteLine("✅ PDF created with extracted text.");
```

ส่วนขยายเหล่านี้แสดงให้เห็นว่า **how to read image** data สามารถส่งต่อไปยังกระบวนการต่อเนื่อง—การสร้างรายงาน, การทำดัชนีการค้นหา, หรือแม้กระทั่งป้อนให้กับโมเดลภาษา.

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| *รูปแบบภาพที่รองรับคืออะไร?* | Aspose.OCR รองรับ PNG, JPEG, BMP, TIFF, และ GIF. หากคุณมี PDF ให้แยกหน้าของมันเป็นภาพก่อน. |
| *ฉันสามารถประมวลผลหลายภาพพร้อมกันได้หรือไม่?* | ได้—ห่อการเรียก `RecognizeImageAsync` แต่ละอันใน task ของมันเองและใช้ `Task.WhenAll`. เพียงแค่ระวังการใช้หน่วยความจำ. |
| *ถ้า OCR คืนข้อความว่างจะทำอย่างไร?* | ตรวจสอบคุณภาพของภาพ: คอนทราสต์ต่ำหรือข้อความที่หมุนมักล้มเหลว. เปิด `ImagePreprocessingOptions.Deskew` หรือหมุนภาพด้วยตนเองก่อน OCR. |
| *มีขนาดจำกัดของภาพหรือไม่?* | ภาพขนาดใหญ่ (>10 MP) อาจทำให้เกิด `OutOfMemoryException`. ลดขนาดลงเป็นความละเอียดที่เหมาะสม (เช่น 300 DPI) ก่อนทำการจดจำ. |
| *ฉันต้องการไลเซนส์สำหรับ Aspose.OCR หรือไม่?* | โหมดพัฒนาทำงานได้ด้วยไลเซนส์ชั่วคราว, แต่สำหรับการใช้งานจริงคุณจะต้องมีไลเซนส์ที่ซื้อเพื่อเอาน้ำลายน้ำการประเมินออก. |

## เคล็ดลับด้านประสิทธิภาพ

- **Reuse the `OcrEngine` instance** สำหรับการประมวลผลเป็นชุด; การสร้าง engine ใหม่ต่อภาพเพิ่มภาระ.  
- **Turn off unused languages** เพื่อเร่งการตรวจจับ—แต่ละภาษาที่เพิ่มเข้ามาจะเพิ่มค่าใช้จ่ายการประมวลผลเล็กน้อย.  
- **Run OCR on a background thread** (ตามที่แสดง) เพื่อให้เธรด UI ทำงานได้อย่างรวดเร็วในแอปเดสก์ท็อปหรือเว็บ.

## สรุป

เราได้ครอบคลุม **how to use OCR** ใน C# ตั้งแต่ต้นจนจบ: การติดตั้ง Aspose.OCR, การเขียนเมธอด async, การปรับตั้งค่าสำหรับภาพที่มีเสียงรบกวน, การจัดการข้อผิดพลาด, และการบันทึกผลลัพธ์ ตอนนี้คุณมีวิธีที่เชื่อถือได้ในการ *extract text from image* ไฟล์, *convert PNG to text*, และแม้กระทั่งป้อนข้อความนั้นเข้าสู่กระบวนการอื่น ๆ เช่นการสร้าง PDF.  

พร้อมสำหรับความท้าทายต่อไปหรือยัง? ลองนำผล OCR ไปใส่ในดัชนี Azure Cognitive Search ที่ค้นหาได้, หรือทดลอง OCR หลายภาษาโดยเพิ่ม `OcrLanguage.Spanish | OcrLanguage.French` ไปยัง engine. ไม่มีขีดจำกัดเมื่อคุณรู้ **how to read image** data ด้วยโปรแกรม.  

---  

*หากคุณพบว่าคู่มือนี้เป็นประโยชน์, ให้ดาวบน GitHub, แบ่งปันกับทีม, หรือแสดงความคิดเห็นด้านล่างพร้อมเทคนิค OCR ของคุณเอง. Happy coding!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}