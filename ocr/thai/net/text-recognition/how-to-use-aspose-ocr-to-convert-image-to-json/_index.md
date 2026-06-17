---
category: general
date: 2026-03-15
description: วิธีใช้ Aspose OCR เพื่อดึงข้อความจากภาพและแปลงภาพเป็น JSON ด้วย C# เรียนรู้การจดจำข้อความจาก
  PNG และรับผลลัพธ์ที่เป็นโครงสร้างอย่างรวดเร็ว
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: th
og_description: วิธีใช้ Aspose OCR เพื่อดึงข้อความจากภาพและแปลงภาพเป็น JSON ด้วย C#
  คู่มือนี้จะพาคุณผ่านขั้นตอนการจดจำข้อความจากไฟล์ PNG และรับผลลัพธ์ที่มีโครงสร้าง
og_title: วิธีใช้ Aspose OCR เพื่อแปลงภาพเป็น JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: วิธีใช้ Aspose OCR เพื่อแปลงรูปภาพเป็น JSON
url: /th/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

/products-backtop-button >}}

We keep them.

Now ensure we didn't translate any URLs, file paths, variable names, function names. We kept code unchanged.

Check for any URLs: none.

Check for any markdown links: none.

Check for any images: we translated alt and title.

Check for any other markdown links: none.

Now produce final content with all translations.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีใช้ Aspose OCR เพื่อแปลงภาพเป็น JSON

การใช้ Aspose OCR เป็นคำถามที่พบบ่อยเมื่อผู้พัฒนาต้องการดึงข้อความจากรูปภาพ หากคุณกำลังมองหา **convert image to JSON** หรือ **recognize text from PNG** คู่มือนี้ครอบคลุมทุกอย่าง—ไม่มีสารพัดประโยชน์เกินความจำเป็น เพียงโซลูชันที่เป็นขั้นตอนครบวงจร

ในไม่กี่นาทีต่อไป เราจะพาคุณผ่านทุกขั้นตอนที่ต้องการ: การติดตั้งไลบรารี, การกำหนดค่าเอนจินสำหรับผลลัพธ์เป็น JSON, การโหลดไฟล์ PNG ของใบเสร็จ, การรัน OCR, และสุดท้ายการบันทึกผลลัพธ์ลงไฟล์ `.json` เมื่อเสร็จคุณจะสามารถ **extract text from image** ได้ด้วยการเรียกเมธอดเดียว และคุณจะเข้าใจว่าทำไมแต่ละขั้นตอนจึงสำคัญ

> **Pro tip:** Aspose OCR ทำงานกับรูปแบบภาพหลากหลาย (PNG, JPEG, BMP, TIFF) โค้ดด้านล่างนี้จะจัดการกับทั้งหมดได้ ดังนั้นคุณไม่จำเป็นต้องเขียนตรรกะเฉพาะรูปแบบ

## สิ่งที่คุณต้องการ

- .NET 6.0 หรือใหม่กว่า (โค้ดทำงานได้บน .NET Framework 4.6+ ด้วย)  
- แพคเกจ Aspose.OCR NuGet ที่ใช้งานได้ (ทดลองใช้ฟรีหรือแบบมีลิขสิทธิ์)  
- ไฟล์ภาพที่คุณต้องการประมวลผล (เช่น `receipt.png`)  
- Visual Studio, VS Code หรือเครื่องมือแก้ไข C# ที่คุณชอบ  

เท่านี้—ไม่มีการพึ่งพาเพิ่มเติม ไม่มีบริการภายนอก พร้อมหรือยัง? ไปกันเลย.

![วิธีใช้ Aspose OCR engine](image-placeholder.png "วิธีใช้ Aspose OCR engine")

## วิธีใช้ Aspose OCR – กำหนดค่าให้ส่งออกเป็น JSON

สิ่งแรกที่คุณต้องทำเมื่อ **how to use aspose** สำหรับ OCR คือสร้างอินสแตนซ์ `OcrEngine` แล้วบอกให้ส่งออกเป็น JSON การสลับค่าการกำหนดค่านี้ช่วยให้คุณไม่ต้องทำการแปลงผลลัพธ์เป็น JSON ด้วยตนเองในภายหลัง.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Why this matters:** การตั้งค่า `OutputFormat` เป็น `Json` หมายความว่า OCR engine จะจัดโครงสร้างข้อความเป็นลำดับชั้นของหน้า, บรรทัด, และคำแล้ว คุณไม่จำเป็นต้องแยกวิเคราะห์สตริงดิบในภายหลัง ซึ่งทำให้การประมวลผลต่อเนื่อง—เช่น การใส่ข้อมูลลงฐานข้อมูล—สะอาดขึ้นมาก.

## แปลงภาพเป็น JSON ด้วย Aspose OCR

เมื่อเอนจินถูกกำหนดค่าแล้ว เรามาพูดถึงส่วน **convert image to JSON** อย่างละเอียด.

1. **Load the image** – `Image.FromFile` ทำงานกับรูปแบบที่รองรับทั้งหมด หากคุณทำงานกับสตรีม (เช่นไฟล์ที่อัปโหลด) คุณสามารถใช้ `Image.FromStream` แทนได้.  
2. **Run `Recognize`** – เมธอดนี้คืนค่าอ็อบเจ็กต์ `OcrResult` เนื่องจากเราได้ตั้งค่าให้ผลลัพธ์เป็น JSON, `ocrResult.Text` จะมีสตริง JSON อยู่แล้ว.  
3. **Write the file** – `File.WriteAllText` เป็นวิธีที่ง่ายที่สุดในการบันทึก JSON หากคุณต้องการเก็บไว้ในคลาวด์บัคเก็ต เพียงเปลี่ยนบรรทัดนี้เป็นการเรียก SDK ที่เหมาะสม.

### ผลลัพธ์ JSON ที่คาดหวัง

โครงสร้าง JSON ตัวอย่างจะมีลักษณะดังนี้ (ตัดส่วนที่ไม่จำเป็นเพื่อความกระชับ):

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

คุณสามารถนำโครงสร้างนี้ไปใช้ในระบบต่อไปได้ทุกระบบ ไม่ว่าจะเป็นเครื่องมือรายงาน, โมเดล machine‑learning, หรือไฟล์บันทึกง่าย ๆ.

## ดึงข้อความจากภาพด้วย Aspose OCR

หากคุณต้องการเพียงสตริงดิบ (เช่น ไม่ต้องการ JSON) เพียงเปลี่ยนรูปแบบผลลัพธ์กลับเป็นข้อความธรรมดา:

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**When to choose plain text?**  
- การดีบักอย่างรวดเร็วหรือแสดงผลบนคอนโซล  
- สถานการณ์ที่คุณต้องการทำการประมวลผลต่อ (เช่น การสกัดด้วย regex)

แต่จำไว้ว่า, **extract text from image** ด้วย JSON จะให้ข้อมูลตำแหน่ง—มีประโยชน์สำหรับการไฮไลท์ข้อความใน UI หรือการจัดตำแหน่งกับฟิลด์ฟอร์ม.

## จดจำข้อความจากไฟล์ PNG

PNG เป็นรูปแบบที่ไม่มีการสูญเสียข้อมูล ซึ่งมักให้ความแม่นยำ OCR ดีกว่า JPEG ที่บีบอัดหนัก นี่คือเช็คลิสต์สั้น ๆ เพื่อให้คุณได้ผลลัพธ์ที่ดีที่สุดเมื่อคุณ **recognize text from PNG**:

| รายการตรวจสอบ | ทำไมจึงช่วย |
|----------------|--------------|
| ใช้ DPI 300 ขึ้นไป | ความละเอียดที่สูงขึ้นให้พิกเซลมากขึ้นสำหรับเอนจิน |
| เก็บภาพเป็นระดับสีเทา | ลดสัญญาณรบกวน; Aspose OCR จะทำการแปลงอัตโนมัติ แต่การเตรียมล่วงหน้าจะทำให้เร็วขึ้น |
| ลบสิ่งกีดขวางพื้นหลัง | พื้นหลังที่สะอาดช่วยเพิ่มคะแนนความมั่นใจ |

หากคุณพบคะแนนความมั่นใจต่ำ ลองเพิ่ม DPI หรือใช้ฟิลเตอร์ threshold อย่างง่ายก่อนส่งภาพให้ Aspose

## วิธีดึงผลลัพธ์ OCR อย่างโปรแกรมเมติก

นอกจากการบันทึก JSON แล้ว คุณอาจต้องการอ่านฟิลด์เฉพาะโดยโปรแกรมเมติก—เช่น จำนวนเงินรวมบนใบเสร็จ เนื่องจาก JSON มีโครงสร้างลำดับชั้น คุณสามารถ deserialize เป็นอ็อบเจ็กต์ C# ได้:

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

ตอนนี้คุณสามารถ query `ocrData` ด้วย LINQ:

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Why this works:** JSON บอกตำแหน่งของแต่ละคำบนหน้าแล้ว ทำให้คุณสามารถหาฟิลด์ได้อย่างแม่นยำแม้เลย์เอาต์จะเปลี่ยนแปลงเล็กน้อย

## กรณีขอบและข้อผิดพลาดทั่วไป

- **Null Result:** หาก `ocrEngine.Recognize` คืนค่า `null` ภาพอาจไม่รองรับหรือเสียหาย ควรตรวจสอบเสมอ:

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Large Files:** สำหรับภาพหลายเมกะไบต์ ควรพิจารณา stream ภาพหรือปรับขนาดก่อน OCR เพื่อหลีกเลี่ยงการใช้หน่วยความจำมากเกินไป

- **License Issues:** เวอร์ชันทดลองจะเพิ่มลายน้ำในผลลัพธ์ ตรวจสอบให้แน่ใจว่าคุณโหลดไลเซนส์ตั้งแต่ต้นโปรแกรม:

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Non‑Latin Scripts:** Aspose OCR รองรับหลายภาษา แต่คุณต้องตั้งค่า property `Language` ให้สอดคล้อง (เช่น `ocrEngine.Configuration.Language = Language.English;`)

## ตัวอย่างทำงานเต็มรูปแบบ (พร้อมคัดลอก‑วาง)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}