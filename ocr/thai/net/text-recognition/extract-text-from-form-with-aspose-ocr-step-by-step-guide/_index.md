---
category: general
date: 2026-03-23
description: ดึงข้อความจากแบบฟอร์มอย่างรวดเร็วด้วย Aspose OCR. เรียนรู้วิธีจดจำข้อความในพื้นที่และจัดการส่วน
  OCR ของภาพด้วยตัวอย่าง C# ที่สมบูรณ์.
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: th
og_description: ดึงข้อความจากแบบฟอร์มโดยใช้ Aspose OCR. บทเรียนนี้แสดงวิธีการจดจำข้อความในพื้นที่และประมวลผลส่วน
  OCR ของภาพด้วย C#
og_title: สกัดข้อความจากแบบฟอร์มด้วย Aspose OCR – คู่มือฉบับสมบูรณ์
tags:
- C#
- OCR
- Aspose
- Image Processing
title: สกัดข้อความจากแบบฟอร์มด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด
url: /th/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากฟอร์มด้วย Aspose OCR – คู่มือขั้นตอนโดยละเอียด

เคยต้องการ **ดึงข้อความจากฟอร์ม** แต่หน้าทั้งหมดเต็มไปด้วยเสียงรบกวนหรือไม่? คุณไม่ได้เป็นคนเดียว—นักพัฒนาต้องต่อสู้กับ PDF, ใบแจ้งหนี้ที่สแกน, หรือแบบสำรวจที่เขียนด้วยมือซึ่งมีเพียงฟิลด์เดียวที่สำคัญ ข่าวดีคือ? คุณสามารถบอก Aspose OCR ให้มองเฉพาะส่วนที่คุณสนใจโดยไม่สนใจส่วนอื่น  

ในคู่มือนี้เราจะแสดงให้คุณเห็นอย่างละเอียดว่า **การจดจำข้อความในพื้นที่** ของฟอร์มที่สแกนอย่างไร ดึงค่าที่ต้องการออกมา และทำให้ส่วนที่เหลือของภาพไม่ถูกแก้ไข เมื่อเสร็จสิ้นคุณจะมีโปรแกรม C# ที่พร้อมรันซึ่งจัดการ **ส่วนของ OCR ในภาพ** ที่คุณต้องการโดยไม่ต้องพึ่งบริการภายนอกใด ๆ

## สิ่งที่คุณจะได้รับจากบทเรียนนี้

- แอปคอนโซล C# ที่ทำงานได้เต็มรูปแบบและสามารถดึงฟิลด์จากภาพฟอร์มได้  
- คำอธิบายที่ชัดเจนว่าทำไมการกำหนดสี่เหลี่ยมเป็นวิธีที่เร็วและแม่นยำกว่า  
- เคล็ดลับการจัดการผลลัพธ์ที่ว่าง, การตั้งค่า DPI ที่ต่างกัน, และฟอร์มหลายหน้า  
- เช็คลิสต์สั้น ๆ เพื่อให้คุณปรับโค้ดให้เข้ากับโปรเจกต์ของคุณได้ในไม่กี่นาที  

**ข้อกำหนดเบื้องต้น** – คุณต้องมี .NET 6 หรือใหม่กว่า, Visual Studio 2022 (หรือ IDE ใดก็ได้ที่คุณชอบ) และการเชื่อมต่ออินเทอร์เน็ตครั้งแรกเพื่อดึงแพคเกจ Aspose.OCR จาก NuGet ไม่ต้องใช้ไลบรารีอื่นเพิ่มเติม

---

## ดึงข้อความจากฟอร์ม – การตั้งค่าโปรเจกต์

ก่อนที่เราจะลงลึกไปที่โค้ด ให้แน่ใจว่ามีสภาพแวดล้อมพร้อม ขั้นตอนถูกออกแบบให้เรียบง่าย เพราะความมหัศจรรย์จริง ๆ จะเกิดขึ้นเมื่อสร้างอินสแตนซ์ของ OCR engine

1. **สร้างโปรเจกต์คอนโซลใหม่**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **เพิ่ม Aspose.OCR ผ่าน NuGet**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **คัดลอกฟอร์มที่สแกน** ไปยังโฟลเดอร์โปรเจกต์และเปลี่ยนชื่อเป็น `form.png`  
   (หากไฟล์ของคุณเป็น PDF ให้ส่งออกหน้าที่ต้องการเป็น PNG ก่อน—Aspose OCR ทำงานได้ดีที่สุดกับภาพราสเตอร์)

เท่านี้ก็เรียบร้อยแล้ว ส่วนที่เหลือของบทเรียนถือว่าขั้นตอนทั้งสามนี้เสร็จสมบูรณ์แล้ว

![extract text from form example](form-region.png "extract text from form example")

*ข้อความอธิบายภาพ: ตัวอย่างการดึงข้อความจากฟอร์มแสดงพื้นที่ที่ไฮไลท์บนเอกสารที่สแกน*

---

## จดจำข้อความในพื้นที่ – การกำหนด Region of Interest

ทำไมต้องใช้สี่เหลี่ยม? ลองนึกว่าคุณมีสแกนขนาด 2 MB ของแบบฟอร์มภาษีทั้งหมด การรัน OCR ทั้งหมดจะเสียทรัพยากร CPU ไปโดยเปล่าประโยชน์และอาจสร้างผลบวกเท็จจากฟิลด์ที่ไม่เกี่ยวข้อง ด้วยการจำกัดขอบเขตให้ตรงกับพิกัดที่มีค่าที่ต้องการ คุณจะได้:

- **ลดเวลาในการประมวลผล** ได้ถึง 80 % สำหรับภาพขนาดใหญ่  
- **เพิ่มความแม่นยำ** เนื่องจาก engine ไม่ต้องสังเกตกราฟิกที่รบกวน  
- **ทำให้การประมวลผลต่อมาเรียบง่าย** — คุณรู้แน่นอนว่าต้องคาดหวังข้อความอะไร

สี่เหลี่ยมถูกกำหนดด้วยสี่ค่า: `x`, `y`, `width`, และ `height` ค่าต่าง ๆ นี้วัดเป็นพิกเซลจากมุมซ้ายบนของภาพ หากคุณไม่แน่ใจว่าฟิลด์อยู่ที่ไหน ให้เปิดภาพใน Paint แล้ววางเมาส์ที่มุมซ้ายบนเพื่ออ่านค่า X/Y จากนั้นลากเพื่อวัดความกว้างและความสูง

---

## ส่วนของ OCR ในภาพ – การโหลดฟอร์มและตั้งค่า Engine

เมื่อกำหนดพื้นที่แล้ว เรามาพูดถึง engine เอง `OcrEngine` คือหัวใจของ Aspose OCR มันตรวจจับภาษาอัตโนมัติ, แก้ไขการเอียง, และคืนค่าเป็นสตริงข้อความธรรมดา คุณยังสามารถปรับคุณสมบัติต่าง ๆ — เช่น `Resolution` หรือ `Language` — หากฟอร์มของคุณใช้สคริปต์ที่ไม่ใช่ละติน สำหรับฟอร์มภาษาอังกฤษส่วนใหญ่ค่าตั้งต้นทำงานได้ดี

ด้านล่างเป็น **โปรแกรมเต็มรูปแบบที่ทำงานอิสระ** ซึ่งรวมทุกอย่างไว้ด้วยกัน คุณสามารถคัดลอก‑วางลงใน `Program.cs` แล้วกด **F5** ได้เลย

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### ผลลัพธ์ที่คาดหวัง

หากสี่เหลี่ยมครอบฟิลด์ที่มีข้อความ “Invoice # 12345” อย่างถูกต้อง คอนโซลจะพิมพ์:

```
Field value: Invoice # 12345
```

หากพื้นที่ว่างหรือ OCR ล้มเหลว คุณจะเห็น:

```
Field value: [No text detected]
```

---

## การอธิบายโค้ดทีละขั้นตอน

ต่อไปเราจะแบ่งโปรแกรมเป็นส่วนย่อย ๆ อธิบาย **เหตุผล** ของแต่ละบรรทัด และชี้ให้เห็นจุดที่คุณอาจต้องปรับเปลี่ยน

### ขั้นตอนที่ 1: ติดตั้ง Aspose.OCR ผ่าน NuGet *(H3)*

```bash
dotnet add package Aspose.OCR
```

*ทำไม?* แพคเกจ NuGet นี้บรรจุ OCR engine แบบ native, ไฟล์ข้อมูลภาษาต่าง ๆ, และ wrapper .NET ที่บางเบา หากไม่มีมัน คลาส `OcrEngine` จะไม่มีอยู่จริง

### ขั้นตอนที่ 2: เริ่มต้น OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*ทำไมต้องใช้ `using`?* `OcrEngine` เก็บทรัพยากรที่ไม่จัดการโดย .NET (DLL แบบ native, บัฟเฟอร์ภาพ) คำสั่ง `using` ทำให้มั่นใจว่าทรัพยากรเหล่านั้นถูกปล่อยออกไป ป้องกันการรั่วเมมโมรีในบริการที่ทำงานต่อเนื่อง

### ขั้นตอนที่ 3: โหลดภาพฟอร์ม *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*ทำไมต้องใช้ `ImageStream`?* มันทำหน้าที่เป็นชั้นนามธรรมของการอ่านไฟล์และแปลงรูปแบบทั่วไป (PNG, JPEG, TIFF) ให้เป็น bitmap ภายในที่ Aspose OCR ต้องการโดยอัตโนมัติ

### ขั้นตอนที่ 4: ระบุพื้นที่ที่ต้องดึงข้อความ *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*ทำไมต้องใช้ `Rectangle`?* OCR engine ยอมรับ `System.Drawing.Rectangle` พารามิเตอร์สี่ตัวนี้ช่วยให้คุณระบุตำแหน่งฟิลด์ได้อย่างแม่นยำ ลดส่วนที่เหลือของหน้าออกไป

*เคล็ดลับ:* หากต้องสนับสนุนหลายฟิลด์ ให้เก็บสี่เหลี่ยมแต่ละอันใน `Dictionary<string, Rectangle>` แล้ววนลูปประมวลผล

### ขั้นตอนที่ 5: รันการจดจำและดึงผลลัพธ์ *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*ทำไมต้องตรวจสอบ `success`?* OCR อาจล้มเหลวได้หลายสาเหตุ — ภาพเบลอ, ภาษาที่ไม่รองรับ, หรือพื้นที่ว่าง การตรวจสอบบูลีนช่วยป้องกันการทำงานกับข้อมูลที่ล้าสมัย

### ขั้นตอนที่ 6: จัดการกรณีขอบและข้อผิดพลาดทั่วไป *(H3)*

- **DPI ที่ต่างกัน:** หากสแกนความละเอียดต่ำ (< 150 DPI) ให้เพิ่มค่า `ocrEngine.Image.DpiX` และ `ocrEngine.Image.DpiY` ก่อนเรียก `Recognize`  
- **หลายหน้า:** สำหรับ PDF หลายหน้า ให้แยกแต่ละหน้าเป็น PNG แยกกันและทำซ้ำขั้นตอนสี่เหลี่ยมสำหรับแต่ละหน้า  
- **ข้อความไม่ใช่ภาษาอังกฤษ:** ตั้งค่า `ocrEngine.Language = Language.Thai;` (หรือภาษาอื่นที่รองรับ) ก่อนทำการจดจำ  
- **การลดสัญญาณรบกวน:** `ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` สามารถช่วยปรับผลลัพธ์บนสแกนที่มีเม็ดสี

---

## ไปต่อ – ความแปรผันในโลกจริง

### ดึงหลายฟิลด์จากฟอร์มเดียวกัน

หากต้องการดึง “ชื่อ”, “วันที่”, และ “จำนวนเงิน” จากเอกสารเดียวกัน ให้สร้างคอลเลกชัน:

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### ผสานกับฐานข้อมูล

หลังจากดึงข้อมูลแล้ว คุณอาจต้องเก็บผลลัพธ์ลงใน SQL Server:

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### ทำงานอัตโนมัติบนเซิร์ฟเวอร์

หากต้องการให้โค้ดทำงานเป็นบริการพื้นหลัง ให้ห่อโลจิกในเมธอด `async` แล้วใช้ `Task.Run` เพื่อไม่ให้ UI ค้าง อย่าลืมตั้งค่า `ocrEngine.ParallelProcessing = true;` เพื่อใช้ประโยชน์จากหลายคอร์

---

## สรุป

คุณมีวิธีที่มั่นคงและพร้อมใช้งานในระดับ production เพื่อ **ดึงข้อความจากฟอร์ม** ด้วย Aspose OCR โดยการมุ่งเน้นที่สี่เหลี่ยมเฉพาะส่วน

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}