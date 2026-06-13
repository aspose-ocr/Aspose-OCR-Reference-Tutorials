---
category: general
date: 2026-03-21
description: 'บทเรียน OCR ด้วย C#: เรียนรู้วิธีดึงข้อความอูรดูจากภาพ PNG ด้วย OCR
  ใน C# โค้ดทีละขั้นตอน การตั้งค่าภาษา และเคล็ดลับปฏิบัติรวมอยู่ด้วย'
draft: false
keywords:
- c# ocr tutorial
- extract urdu text
- recognize text image
- how to extract urdu
- ocr from png file
language: th
og_description: 'คอร์สสอน OCR ด้วย C#: เรียนรู้วิธีดึงข้อความอูรดูจากภาพ PNG ด้วย
  OCR ใน C#. คู่มือเต็มพร้อมโค้ดและเคล็ดลับ'
og_title: คอร์ส OCR ด้วย C# – แยกข้อความอูรดูจากภาพ PNG
tags:
- OCR
- C#
- Urdu
- Image Processing
title: c# OCR tutorial – สกัดข้อความอูรดูจากภาพ PNG
url: /th/net/text-recognition/c-ocr-tutorial-extract-urdu-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – แยกข้อความ Urdu จากไฟล์ PNG

เคยต้องการ **c# ocr tutorial** ที่จริง ๆ แล้วดึงข้อความ Urdu ออกมาจากไฟล์ PNG หรือไม่? คุณไม่ได้อยู่คนเดียว ในหลายโครงการ—การประมวลผลใบแจ้งหนี้, การจัดเก็บเอกสาร, หรือแม้แต่เครื่องมือแปลอย่างรวดเร็ว—คุณจะเจอจุดที่ต้องรู้จำข้อมูลภาพข้อความและภาษาก็มีความสำคัญ  

ในคู่มือนี้เราจะเดินผ่านโซลูชันที่พร้อมรันครบวงจรที่ดึงข้อความ Urdu จาก PNG ด้วยเครื่องมือ OCR คุณจะเห็นว่าทำไมแต่ละบรรทัดถึงมีอยู่, วิธีจัดการกับแพ็คเกจภาษาที่หายไป, และทำอย่างไรหากภาพไม่สมบูรณ์ สุดท้ายคุณจะมั่นใจพอที่จะปรับโค้ดสำหรับภาษาอื่นหรือประเภทไฟล์อื่นได้

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่าไลบรารี OCR สำหรับ C# (ไม่มีเวทมนตร์ซ่อนเร้น)  
- ขั้นตอนที่แม่นยำเพื่อ **extract urdu text** จากไฟล์ PNG  
- ทำไมการกำหนดค่า language เป็น Urdu ถึงสำคัญและเครื่องมือจะดาวน์โหลดข้อมูลที่ขาดหายไปโดยอัตโนมัติอย่างไร  
- วิธีตรวจสอบผลลัพธ์และแก้ไขปัญหาที่พบบ่อย  

ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่

## สิ่งที่ต้องเตรียมก่อน (Prerequisites)

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6.0+ (หรือ .NET Core 3.1) | API สมัยใหม่และการสนับสนุน async |
| Visual Studio 2022 (หรือ VS Code พร้อมส่วนขยาย C#) | IDE ที่มี IntelliSense ทำให้โค้ดอ่านง่ายขึ้น |
| ไลบรารี OCR ที่เปิดเผย `OcrEngine` (เช่น **Microsoft.Windows.SDK.Contracts** หรือ NuGet ของบุคคลที่สาม) | มีเมธอด `Language.Urdu` และ `Recognize` |
| ภาพ PNG ที่มีข้อความ Urdu (เช่น `urdu_invoice.png`) | แหล่งข้อมูลสำหรับการ **recognize text image** |

หากคุณยังไม่มีแพ็คเกจ OCR ให้รันคำสั่งต่อไปนี้ใน Package Manager Console:

```powershell
Install-Package Microsoft.Windows.SDK.Contracts
```

คำสั่งนี้จะนำเข้าคลาส `OcrEngine` ที่เราจะใช้ต่อไป

> **เคล็ดลับมืออาชีพ:** SDK จะดึงข้อมูลภาษามาโดยอัตโนมัติในครั้งแรกที่ใช้ ดังนั้นคุณไม่ต้องดาวน์โหลดแพ็คเกจภาษา Urdu ด้วยตนเอง

## ขั้นตอนที่ 1: ติดตั้งและอ้างอิงไลบรารี OCR

ก่อนที่เราจะสร้าง engine โปรเจคต้องอ้างอิงแพ็คเกจ OCR เพิ่ม `using` directives ด้านบนไฟล์ของคุณ:

```csharp
using System;
using Windows.Media.Ocr;          // Core OCR classes
using Windows.Graphics.Imaging;   // For loading PNG files
using Windows.Storage;            // File handling helpers
```

เนมสเปซเหล่านี้ทำให้เราสามารถเข้าถึง `OcrEngine`, `Language` และยูทิลิตี้การโหลดภาพ หากคุณใช้ไลบรารีอื่น ให้มองหาเนมสเปซที่คล้ายกัน

## ขั้นตอนที่ 2: สร้างอินสแตนซ์ของ OCR Engine  

ตอนนี้เราจะสร้าง engine จริง ๆ คิดว่า engine คือสมองที่จะแปลรูปแบบพิกเซลเป็นอักขระ

```csharp
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));
if (ocrEngine == null)
{
    Console.WriteLine("Failed to create OCR engine for Urdu. Check your language pack.");
    return;
}
```

**ทำไมต้องทำเช่นนี้:** `TryCreateFromLanguage` จะคืนค่า `null` หากข้อมูลภาษายังไม่มีอยู่ ทำให้เราสามารถตรวจจับความล้มเหลวได้ตั้งแต่ต้น แทนที่จะให้แอปพังภายหลัง

## ขั้นตอนที่ 3: โหลดภาพ PNG  

OCR engine ทำงานกับอ็อบเจ็กต์ `SoftwareBitmap` ไม่ใช่เส้นทางไฟล์ดิบ โค้ดช่วยเหลือต่อไปนี้จะโหลด PNG จากดิสก์และแปลงเป็นรูปแบบที่ต้องการ

```csharp
// Step 3: Load the PNG image into a SoftwareBitmap
async Task<SoftwareBitmap> LoadImageAsync(string path)
{
    StorageFile file = await StorageFile.GetFileFromPathAsync(path);
    using var stream = await file.OpenReadAsync();
    var decoder = await BitmapDecoder.CreateAsync(stream);
    // Convert to Gray8 for best OCR accuracy
    return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
}
```

**กรณีขอบ:** หาก PNG มีสี การแปลงเป็นระดับสีเทา (`Gray8`) มักช่วยให้การรู้จำดีขึ้น โดยเฉพาะสคริปต์อย่าง Urdu ที่มี diacritics ละเอียด

## ขั้นตอนที่ 4: รู้จำข้อความจากภาพ  

นี่คือหัวใจของ **c# ocr tutorial**—ให้ engine อ่านภาพ

```csharp
// Step 4: Perform OCR on the loaded bitmap
async Task<string> RecognizeUrduAsync(string imagePath)
{
    SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
    OcrResult result = await ocrEngine.RecognizeAsync(bitmap);
    return result.Text;
}
```

คุณสมบัติ `OcrResult.Text` จะมีสตริง Unicode ดิบ เนื่องจากเราตั้งค่าภาษาเป็น Urdu ก่อนหน้า engine จะใช้กฎสคริปต์ที่ถูกต้อง

## ขั้นตอนที่ 5: แสดงผลและตรวจสอบข้อความที่ดึงมา  

สุดท้ายเราจะพิมพ์ผลลัพธ์ลงคอนโซล ในแอปจริงคุณอาจเก็บลงฐานข้อมูลหรือส่งต่อให้บริการแปล

```csharp
// Step 5: Run the OCR and display the result
static async Task Main(string[] args)
{
    string imageFile = @"C:\Images\urdu_invoice.png"; // adjust path as needed
    string extracted = await RecognizeUrduAsync(imageFile);
    Console.WriteLine("=== Extracted Urdu Text ===");
    Console.WriteLine(extracted);
}
```

**สิ่งที่คาดว่าจะเห็น:** หากภาพชัดเจน คุณจะเห็นข้อความประมาณนี้

```
=== Extracted Urdu Text ===
بل نمبر: 12345
تاریخ: 21/03/2026
کل رقم: 5,000 روپے
```

หากผลลัพธ์เป็นตัวอักษรแปลก ๆ ให้ตรวจสอบคุณภาพของภาพ (คอนทราสต์, สัญญาณรบกวน) และพิจารณาการทำพรี‑โปรเซสซิ่ง (เช่น การทำไบนารี)

## วิธีดึงข้อความ Urdu จากไฟล์ PNG – ปัญหาที่พบบ่อย  

1. **คอนทราสต์ต่ำ** – OCR ทำงานได้ยากเมื่อสีพื้นหน้าและพื้นหลังคล้ายกัน ใช้เครื่องมือแก้ไขภาพเพิ่มคอนทราสต์ก่อนรันโค้ด  
2. **DPI ไม่เหมาะ** – การสแกนที่ 300 dpi หรือสูงกว่าจะให้รายละเอียดมากขึ้นแก่ engine  
3. **แพ็คเกจภาษาขาด** – การเรียก `TryCreateFromLanguage` ครั้งแรกอาจทำให้ดาวน์โหลดอัตโนมัติ; ตรวจสอบว่าเครื่องของคุณมีการเชื่อมต่ออินเทอร์เน็ต  

การแก้ไขปัญหาเหล่านี้จะเพิ่มอัตราความสำเร็จของ **recognize text image** อย่างมาก

## Recognize Text Image: ขยายไปยังรูปแบบอื่น  

แม้ว่าบทเรียนนี้จะเน้น PNG แต่กระบวนการเดียวกันทำงานได้กับ JPEG, BMP หรือ TIFF—แค่เปลี่ยนนามสกุลไฟล์และตรวจสอบว่า decoder รองรับ คำสั่งสำคัญยังคงเป็น `await ocrEngine.RecognizeAsync(bitmap);`

## เคล็ดลับสำหรับ OCR จากไฟล์ PNG – ประสิทธิภาพและการขยายขนาด  

- **ประมวลผลเป็นชุด:** โหลดหลายภาพลงในลิสต์และใช้ `Task.WhenAll` เพื่อทำการรู้จำแบบขนาน  
- **แคช engine:** สร้างอินสแตนซ์ `OcrEngine` เพียงครั้งเดียวและใช้ซ้ำ; การสร้างซ้ำหลายครั้งเพิ่มภาระงาน  
- **จัดการหน่วยความจำ:** ปล่อยอ็อบเจ็กต์ `SoftwareBitmap` หลังการใช้ (`bitmap.Dispose()`) เพื่อให้โปรเซสคงที่

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

ด้านล่างเป็นโปรแกรมทั้งหมดที่คุณสามารถคอมไพล์และรันได้ รวมทุก `using` statements, การจัดการ async, และการตรวจสอบข้อผิดพลาด

```csharp
// Full C# OCR tutorial – Extract Urdu text from a PNG file
using System;
using System.Threading.Tasks;
using Windows.Media.Ocr;
using Windows.Graphics.Imaging;
using Windows.Storage;

class Program
{
    // Initialize the OCR engine for Urdu
    private static OcrEngine _ocrEngine = OcrEngine.TryCreateFromLanguage(new Language("ur"));

    static async Task Main(string[] args)
    {
        if (_ocrEngine == null)
        {
            Console.WriteLine("Urdu language pack not available. Ensure internet connectivity for automatic download.");
            return;
        }

        string imagePath = @"C:\Images\urdu_invoice.png"; // <-- change to your image location
        string text = await RecognizeUrduAsync(imagePath);
        Console.WriteLine("=== Extracted Urdu Text ===");
        Console.WriteLine(text);
    }

    // Load PNG and convert to grayscale bitmap
    private static async Task<SoftwareBitmap> LoadImageAsync(string path)
    {
        StorageFile file = await StorageFile.GetFileFromPathAsync(path);
        using var stream = await file.OpenReadAsync();
        var decoder = await BitmapDecoder.CreateAsync(stream);
        return await decoder.GetSoftwareBitmapAsync(BitmapPixelFormat.Gray8, BitmapAlphaMode.Ignore);
    }

    // Perform OCR and return the recognized text
    private static async Task<string> RecognizeUrduAsync(string imagePath)
    {
        SoftwareBitmap bitmap = await LoadImageAsync(imagePath);
        OcrResult result = await _ocrEngine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

**ผลลัพธ์ที่คาดหวัง:** คอนโซลจะแสดงอักขระ Urdu ที่พบในภาพอย่างแม่นยำตามลำดับจากขวาไปซ้าย

## สรุป  

คุณเพิ่งทำสำเร็จ **c# ocr tutorial** ที่สาธิตวิธี **extract urdu text** จาก PNG, ตั้งค่าภาษา, และจัดการผลลัพธ์อย่างปลอดภัย ขั้นตอน—การติดตั้งไลบรารี, การสร้าง engine, การโหลดภาพ, การรู้จำข้อความ, และการแสดงผล—เป็นรูปแบบที่นำกลับมาใช้ได้กับสคริปต์หรือไฟล์ประเภทใดก็ได้  

ต่อไปลองทดลอง **recognize text image** กับ PDF หลายหน้า (แปลงแต่ละหน้าเป็น PNG ก่อน) หรือเชื่อมต่อ API แปลเพื่อแปลง Urdu เป็นอังกฤษโดยอัตโนมัติ เมื่อคุณเชี่ยวชาญเวิร์กโฟลว์หลักนี้แล้ว โอกาสจะไม่มีที่สิ้นสุด

ขอให้เขียนโค้ดสนุกและผลลัพธ์ OCR ของคุณใสสะอาดเหมือนคริสตัล!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}