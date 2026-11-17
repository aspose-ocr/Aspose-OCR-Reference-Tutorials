---
category: general
date: 2026-03-17
description: บทเรียน OCR ด้วย C# – ค้นพบวิธีดึงข้อความจากไฟล์รูปภาพ, อ่านข้อความจากภาพ
  WebP, และแปลงรูปภาพเป็นข้อความโดยใช้ OcrEngine อย่างง่าย.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: th
og_description: บทเรียน OCR ด้วย C# แสดงวิธีดึงข้อความจากไฟล์รูปภาพ อ่านข้อความจากภาพ
  WebP และแปลงรูปเป็นข้อความด้วยไม่กี่บรรทัดของโค้ด
og_title: บทเรียน OCR ด้วย C# – ดึงข้อความจากภาพในไม่กี่นาที
tags:
- C#
- OCR
- Image Processing
title: 'บทเรียน OCR ด้วย C#: วิธีดึงข้อความจากภาพ (WebP, Photo) – คู่มือสั้น'
url: /th/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – ดึงข้อความจากรูปภาพ (WebP, Photo)

เคยต้องการ **extract text from image** ไฟล์แต่ไม่แน่ใจว่าจะเริ่มต้นอย่างไรใน C#? บางทีคุณอาจมีภาพหน้าจอ WebP, JPEG ของใบเสร็จ, หรือหน้า PDF ที่สแกนและคุณแค่ต้องการคำภายใน. ใน **c# OCR tutorial** นี้ เราจะพาไปผ่านตัวอย่างที่สมบูรณ์พร้อมรันที่อ่านข้อความจากรูปถ่าย, รองรับ WebP และฟอร์แมตสมัยใหม่อื่น ๆ, และแปลงภาพเป็นข้อความธรรมดา—ทั้งหมดในไม่กี่บรรทัด.

**ผลลัพธ์คืออะไร?** คุณจะสามารถแปลงรูปภาพใด ๆ ที่มีข้อความให้เป็นสตริงที่ค้นหาได้, ใส่ลงในฐานข้อมูล, หรือส่งต่อไปยัง pipeline AI ต่อไป. ไม่มีเวทมนตร์, เพียง OCR engine ที่แข็งแรง, API ของ .NET ไม่กี่ตัว, และคำอธิบายที่ชัดเจนของ “ทำไม” ในแต่ละขั้นตอน.

## สิ่งที่คุณต้องการ

- **.NET 6 SDK** (หรือเวอร์ชันใหม่กว่า). โค้ดด้านล่างจะคอมไพล์ด้วย .NET 6+ และทำงานบน Windows, Linux, หรือ macOS.
- **Visual Studio 2022** หรือโปรแกรมแก้ไขใด ๆ ที่คุณชอบ (VS Code ใช้งานได้ดี).
- แพคเกจ NuGet **`Microsoft.Windows.SDK.Contracts`** (ให้ `Windows.Media.Ocr`). ติดตั้งด้วย:

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- ไฟล์รูปภาพที่คุณต้องการประมวลผล – สำหรับบทเรียนนี้เราจะใช้รูป **WebP** ชื่อ `photo.webp` ที่อยู่ในโฟลเดอร์ชื่อ `YOUR_DIRECTORY`.

> เคล็ดลับ: หากคุณอยู่บนแพลตฟอร์มที่ไม่ใช่ Windows, คุณสามารถเปลี่ยน `OcrEngine` เป็นไลบรารีข้ามแพลตฟอร์มอย่าง **Tesseract**. โค้ดส่วนที่เหลือจะเหมือนเดิมเกือบทั้งหมด.

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์ C# OCR Tutorial

แรก, สร้างแอปคอนโซลใหม่. เปิดเทอร์มินัลและรัน:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

เพิ่มแพคเกจที่จำเป็น (ตามที่แสดงข้างบน) และเปิดโปรเจกต์ใน IDE ของคุณ. โครงสร้างนี้ให้เราเริ่มต้นสะอาดสำหรับ **c# OCR tutorial**.

## ขั้นตอนที่ 2: นำเข้า Namespaces และเตรียมภาพ

เราต้องการ `using` directives บางอย่างเพื่อให้คอมไพเลอร์รู้ว่าจะหา `OcrEngine`, `SoftwareBitmap`, และตัวช่วยโหลดภาพได้จากที่ไหน.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **ทำไมต้องใช้ namespaces เหล่านี้?**  
> `Windows.Media.Ocr` มีคลาส `OcrEngine` ที่ทำการจดจำจริง ๆ. `Windows.Graphics.Imaging` ช่วยให้เราถอดรหัสภาพ (รวมถึง WebP) เป็น `SoftwareBitmap` ที่ engine เข้าใจได้. ตัวช่วย `System.IO` และ `Windows.Storage.Streams` ทำให้การโหลดไฟล์เป็นเรื่องง่าย.

ต่อไป, โหลดภาพ. ตัวถอดรหัสในตัวสามารถจัดการ WebP, HEIF, PNG, JPEG, และอื่น ๆ, ดังนั้นคุณสามารถ **read text from WebP** ได้โดยไม่ต้องใช้ปลั๊กอินเพิ่มเติม.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **กรณีขอบ:** หากภาพของคุณเป็นขาว‑ดำอยู่แล้ว, คุณสามารถข้ามขั้นตอนการแปลงได้. การแปลงเป็นระดับสีเทาเป็นการเพิ่มประสิทธิภาพเล็กน้อยและมักช่วยให้การจดจำดีขึ้นในภาพที่มีสัญญาณรบกวน.

## ขั้นตอนที่ 3: รัน OCR Engine – จดจำข้อความจากรูปถ่าย

นี่คือหัวใจของ **c# OCR tutorial**. เราจะสร้างอินสแตนซ์ของ `OcrEngine`, ป้อน bitmap ให้มัน, แล้วดึงข้อความที่จดจำได้ออกมา.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**เกิดอะไรขึ้น?**  
- `TryCreateFromUserProfileLanguages()` เลือกภาษา(ภาษาที่) โปรไฟล์ผู้ใช้ Windows ของคุณตั้งค่าไว้, ซึ่งโดยทั่วไปครอบคลุมอังกฤษ, สเปน, ฯลฯ. หากต้องการภาษาที่เฉพาะเจาะจง, ใช้ `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.  
- `RecognizeAsync` ทำงานหนักบนเธรดพื้นหลัง, คืนค่า `OcrResult` ที่มีสตริงดิบ, กล่องขอบคำ, และคะแนนความมั่นใจ.  
- สุดท้าย, เราแสดง `ocrResult.Text`, ให้คุณผลลัพธ์ **convert image to text** ที่สามารถส่งต่อไปยังที่อื่นได้.

## ขั้นตอนที่ 4: ตัวอย่างเต็มที่สามารถรันได้

รวมทุกอย่างเข้าด้วยกัน, นี่คือโปรแกรมที่ทำงานได้เองที่คุณสามารถคัดลอก‑วางลงใน `Program.cs`. มันคอมไพล์, รัน, และพิมพ์ข้อความที่ดึงจาก `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หาก `photo.webp` มีประโยค “Hello, world! This is a test.” คุณจะเห็นบางอย่างเช่น:

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

การแบ่งบรรทัดที่แน่นอนขึ้นอยู่กับการจัดวางของภาพต้นฉบับ, แต่ผลลัพธ์ **extract text from image** จะเป็นสตริงธรรมดาที่คุณสามารถจัดการต่อได้.

## คำถามทั่วไป & กรณีขอบ

### ใช้งานได้กับฟอร์แมตภาพอื่นหรือไม่?

แน่นอน. ตัวถอดรหัสที่ใช้ (`BitmapDecoder`) ตรวจจับ JPEG, PNG, BMP, GIF, **WebP**, HEIF, และอื่น ๆ อัตโนมัติ. ดังนั้นคุณสามารถ **read text from WebP**, JPEG, หรือแม้แต่ TIFF ได้โดยไม่ต้องเปลี่ยนโค้ด.

### ถ้า OCR engine คืนค่าความมั่นใจต่ำจะทำอย่างไร?

คุณสามารถตรวจสอบ `ocrResult.Lines` และแต่ละ `OcrWord` สำหรับ `ConfidenceScore`. หากคะแนนต่ำกว่าขีดจำกัด (เช่น 0.6), พิจารณา:

- ทำการประมวลผลล่วงหน้าภาพ (เพิ่มคอนทราสต์, คมชัด, แก้ไขการเอียง).  
- ใช้ภาพต้นฉบับที่ความละเอียดสูงกว่า.  
- เปลี่ยนไปใช้ไลบรารีเฉพาะเช่น **Tesseract** เพื่อสนับสนุนหลายภาษา.

### จัดการหลายภาษาในภาพเดียวอย่างไร?

สร้างอินสแตนซ์ `OcrEngine` แยกต่างหากสำหรับแต่ละภาษาและรันต่อเนื่อง, หรือใช้ไลบรารีที่สนับสนุนการตรวจจับหลายภาษา. สำหรับ engine ในตัว, คุณสามารถส่งออบเจกต์ `Language` ได้:

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### สามารถรันบน Linux/macOS ได้หรือไม่?

`Windows.Media.Ocr` API ใช้ได้เฉพาะ Windows. บนแพลตฟอร์มที่ไม่ใช่ Windows, ให้แทนที่ส่วน OCR ด้วย **Tesseract** (ผ่าน `Tesseract.Net.SDK`). โค้ดการโหลดและการประมวลผลล่วงหน้ายังคงเหมือนเดิม, ดังนั้นส่วนที่เหลือของ **c# OCR tutorial** ยังใช้ได้.

## เคล็ดลับสำหรับความแม่นยำที่ดียิ่งขึ้น

- **Resize** ปรับขนาดภาพขนาดใหญ่ให้สูงสุด 2000 px ที่ด้านยาวที่สุด – OCR engine ทำงานเร็วขึ้นกับขนาดปานกลาง.  
- **Denoise** ลดสัญญาณรบกวนด้วย Gaussian blur อย่างง่ายหากภาพมีเม็ด.  
- **Deskew** แก้ไขการเอียงของ bitmap หากข้อความไม่เป็นแนวนอนสมบูรณ์; `SoftwareBitmap` สามารถหมุนก่อนส่งให้ `OcrEngine`.  
- **Cache** เก็บอินสแตนซ์ `OcrEngine` หากคุณประมวลผลหลายภาพในชุด; การสร้างซ้ำเพิ่มภาระ.

## หัวข้อที่เกี่ยวข้องเพื่อสำรวจ

- **Convert image to text** ด้วย **Tesseract** สำหรับโครงการข้ามแพลตฟอร์ม.  
- **Extract text from PDF** โดยเรนเดอร์แต่ละหน้าเป็นภาพก่อน.  
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}