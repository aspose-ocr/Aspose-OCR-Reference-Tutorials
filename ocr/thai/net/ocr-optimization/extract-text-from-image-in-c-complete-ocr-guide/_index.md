---
category: general
date: 2026-02-11
description: ดึงข้อความจากภาพใน C# ด้วย Aspose OCR. เรียนรู้วิธีโหลดภาพสำหรับ OCR,
  ปรับปรุงความแม่นยำของ OCR, และแก้ไขข้อผิดพลาดของ OCR ด้วยการตรวจสอบการสะกด.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: th
og_description: ดึงข้อความจากภาพใน C# ด้วย Aspose OCR คู่มือนี้แสดงวิธีโหลดภาพสำหรับ
  OCR, ปรับปรุงความแม่นยำของ OCR, และแก้ไขข้อผิดพลาดของ OCR.
og_title: ดึงข้อความจากภาพใน C# – คู่มือ OCR ครบวงจร
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: ดึงข้อความจากภาพใน C# – คู่มือ OCR ฉบับสมบูรณ์
url: /th/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากภาพใน C# – คู่มือ OCR ฉบับสมบูรณ์

เคยต้องการ **extract text from image** แต่ผลลัพธ์ออกมาดูเหมือนอักขระไร้ความหมายหรือไม่? คุณไม่ได้เป็นคนเดียว ในแอปพลิเคชันจริงหลายกรณี—เช่น การสแกนใบเสร็จ, การแปลงโน้ตเป็นดิจิทัล, หรือการย้ายเอกสารเก่า—การได้ข้อความที่สะอาดจากภาพเป็นอุปสรรคแรกและมักเป็นอุปสรรคที่ยากที่สุด

โชคดีที่ด้วย Aspose OCR คุณสามารถ **load image for OCR**, ทำการตรวจสอบการสะกด, และได้ข้อความที่เรียบร้อยและสามารถค้นหาได้ ในบทแนะนำนี้เราจะเดินผ่านขั้นตอนทั้งหมด ตั้งแต่การอ่านไฟล์ JPEG ไปจนถึงการปรับผลลัพธ์ และคุณจะได้เห็นวิธี **improve OCR accuracy** อย่างชัดเจน

> **What you’ll walk away with:** โปรแกรมคอนโซล C# ที่พร้อมรันซึ่ง **extracts text from image**, แก้ไขข้อผิดพลาด OCR ที่พบบ่อย, และพิมพ์ผลลัพธ์ทั้งแบบดิบและแบบทำความสะอาด

---

## สิ่งที่คุณต้องการ

- .NET 6 หรือใหม่กว่า (โค้ดยังทำงานบน .NET Framework 4.7+ ด้วย)
- Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ)
- คีย์ทดลอง Aspose OCR ฟรีหรือเวอร์ชันที่มีลิขสิทธิ์
- ไฟล์ภาพที่มีข้อความพิมพ์หรือพิมพ์ออกมา (เช่น `typed_note.jpg`)

ไม่จำเป็นต้องใช้ไลบรารีของบุคคลที่สามอื่นใด—Aspose จัดการโมเดลภาษาและการตรวจสอบการสะกดโดยอัตโนมัติ

---

## ขั้นตอนที่ 1 – ติดตั้งแพคเกจ NuGet ของ Aspose  OCR

ก่อนที่เราจะสามารถ **extract text from image** ได้, เครื่องมือ OCR ต้องพร้อมใช้งานบนเครื่อง

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

หรือ, หากคุณชอบใช้ CLI:

```bash
dotnet add package Aspose.OCR
```

แพคเกจรวมข้อมูลภาษาไว้ด้วย, แต่การตั้งค่า `AutomaticResourceDownload = true` (ตามที่เราจะทำในภายหลัง) จะรับประกันว่าพจนานุกรมที่ขาดหายจะถูกดาวน์โหลดในขณะรัน

---

## ขั้นตอนที่ 2 – โหลดภาพสำหรับ OCR

สิ่งแรกที่เครื่องมือจำเป็นต้องมีคือบิตแมพ คุณสามารถส่งภาพในรูปแบบใดก็ได้ที่ `System.Drawing.Image` รองรับ เช่น PNG, JPEG, BMP หรือ TIFF

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Why the `using` block?** มันทำการปล่อยอ็อบเจ็กต์ `Image` โดยอัตโนมัติ, ป้องกันปัญหาไฟล์ล็อกที่มักทำให้ผู้พัฒนาลืมปล่อยทรัพยากร

---

## ขั้นตอนที่ 3 – ทำ OCR – “Image to Text C#” ในการทำงาน

ตอนนี้เราจริง ๆ แล้ว **extract text from image**. คลาส `OcrEngine` ทำหน้าที่หลัก

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

ในขั้นตอนนี้คุณจะได้สตริงที่สะท้อนสิ่งที่เครื่องมองเห็นในภาพ ในการใช้งานจริงผลลัพธ์อาจมีอักขระแปลกปลอม, คำที่อ่านผิด, หรือการแบ่งบรรทัดที่แปลกประหลาด—จึงต้องทำขั้นตอนต่อไป

---

## ขั้นตอนที่ 4 – ปรับปรุงความแม่นยำของ OCR ด้วยการตรวจสอบการสะกด

Aspose มี `SpellChecker` เฉพาะที่รู้จักภาษาที่คุณกำลังประมวลผล การรันมันบนสตริงดิบมักจะแก้ข้อผิดพลาดที่เด่นชัดที่สุด

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **Pro tip:** หากคุณทำงานกับคำศัพท์เฉพาะโดเมน (เช่น คำทางการแพทย์) คุณสามารถส่งพจนานุกรมกำหนดเองให้กับ `SpellChecker` ผ่าน overloads ของมัน

---

## ขั้นตอนที่ 5 – แก้ไขข้อผิดพลาด OCR ด้วยตนเอง (ทางเลือก)

แม้ว่า spell‑checker ที่ดีที่สุดก็อาจพลาดข้อผิดพลาดที่ต้องพิจารณาบริบท การประมวลผลหลังอย่างรวดเร็วสามารถจับกรณีเช่น “l” กับ “1” หรือ “O” กับ “0”

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

คุณสามารถขยายส่วนนี้ด้วย heuristic ของคุณเอง—เช่น ตารางค้นหาสำหรับรหัสสินค้า หรือรายการของอักษรย่อที่รู้จัก

---

## ตัวอย่างการทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมเต็มที่คุณสามารถคัดลอกและวางลงในโปรเจกต์ Console App ใหม่ มันรวมทุกขั้นตอนที่อธิบายไว้ พร้อมคอมเมนต์ที่เป็นประโยชน์

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

สมมติว่า `typed_note.jpg` มีประโยค “Hello world, this is a test 123”, คอนโซลจะแสดงประมาณนี้:

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

สังเกตว่า spell‑checker แปลง “H3llo” เป็น “Hello”, และ regex ทำความสะอาด “1” ที่แปลกปลอมที่ปรากฏใน “th1s”

---

## คำถามทั่วไป & กรณีขอบ

| Question | Answer |
|----------|--------|
| **ฉันสามารถใช้ภาษาที่แตกต่างได้หรือไม่?** | ได้. ตั้งค่า `ocrEngine.Language = OcrLanguage.Spanish` (หรือ enum ที่รองรับอื่น) และส่งภาษานั้นไปยัง `SpellChecker` ด้วย |
| **ถ้าภาพของฉันมีขนาดใหญ่มากล่ะ?** | ลดขนาดลงก่อนส่งให้ OCR; `Image` มีเมธอด `GetThumbnailImage` สำหรับการปรับขนาดอย่างรวดเร็ว |
| **ต้องการการเชื่อมต่ออินเทอร์เน็ตหรือไม่?** | จำเป็นเฉพาะครั้งแรกที่ไม่มีแพ็คภาษาที่ต้องการ; หลังจากนั้นทรัพยากรจะถูกแคชไว้ในเครื่อง |
| **ฉันจะจัดการกับ PDF หลายหน้าอย่างไร?** | แปลงแต่ละหน้ามาเป็นภาพ (เช่น ใช้ `PdfRenderer`) แล้วรันพายไลน์เดียวกันต่อแต่ละหน้า |
| **Spell‑checker มีความเข้าใจภาษาไหม?** | แน่นอน. มันใช้โมเดลภาษาที่คุณกำหนดให้กับ OCR engine ทำให้สอดคล้องกัน |

---

## ขั้นตอนต่อไป & หัวข้อที่เกี่ยวข้อง

- **Batch processing:** ห่อโค้ดด้วยลูป `foreach` เพื่อจัดการโฟลเดอร์ของภาพหลายไฟล์
- **Hand‑written text:** เปลี่ยนเป็น `OcrLanguage.EnglishHandwritten` เพื่อผลลัพธ์ที่ดีกว่าในโน้ตลายมือ
- **Parallelism:** ใช้ `Parallel.ForEach` เพื่อเร่งความเร็วงานขนาดใหญ่บนเครื่องหลายคอร์
- **Export to JSON/CSV:** Serialize `finalText` พร้อมเมตาดาต้า (ชื่อไฟล์, คะแนนความมั่นใจ) เพื่อการวิเคราะห์ต่อไป

หากคุณสนใจที่จะเปลี่ยนสตริงที่ดึงออกมาให้เป็น PDF ที่สามารถค้นหาได้, ดูคู่มือของเราที่ **“Create searchable PDF from image in C#”**. มันสร้างบนพายไลน์ OCR เดียวกันที่เราอธิบาย

---

## สรุป

เราได้สาธิตวิธีเชิงปฏิบัติในการ **extract text from image** ใน C# ด้วย Aspose OCR พร้อมแสดงวิธี **load image for OCR**, **improve OCR accuracy**, และ **fix OCR errors** ด้วย spell‑checker ในตัวและการทำความสะอาดด้วย regex เล็ก ๆ ตัวอย่างเต็มทำงานได้ทันที, ต้องการเพียงแพคเกจ NuGet เดียว, และสามารถขยายให้เข้ากับสถานการณ์การแปลงเอกสารใด ๆ ได้อย่างอเนกประสงค์

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}