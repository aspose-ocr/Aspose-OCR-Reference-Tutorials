---
category: general
date: 2026-02-13
description: วิธีอ่านใบเสร็จอย่างรวดเร็วด้วย Aspose OCR และดึงจำนวนเงินโดยใช้ regex.
  เรียนรู้ขั้นตอนการประมวลผลใบเสร็จด้วย OCR อย่างเป็นขั้นเป็นตอน.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: th
og_description: วิธีอ่านใบเสร็จใน C# ด้วย Aspose OCR และ regex คู่มือนี้จะแสดงวิธีการประมวลผลใบเสร็จด้วย
  OCR และดึงจำนวนเงินรวมออกมา
og_title: วิธีอ่านใบเสร็จใน C# – บทเรียน OCR & Regex อย่างครบถ้วน
tags:
- OCR
- C#
- Regex
- Aspose
title: วิธีอ่านใบเสร็จใน C# – คู่มือ OCR + Regex
url: /th/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# วิธีอ่านใบเสร็จใน C# – คู่มือ OCR + Regex

เคยสงสัยไหมว่า **วิธีอ่านใบเสร็จ** โดยไม่ต้องพิมพ์ทุกบรรทัดด้วยตนเอง? ในแอปธุรกิจขนาดเล็กหลาย ๆ ตัวคุณต้องดึงยอดรวมจากรูปภาพของใบเสร็จและการทำด้วยมือทำให้การอัตโนมัติไม่มีประโยชน์ ข่าวดีคือ? ด้วย Aspose OCR คุณสามารถให้เอนจินทำงานหนักส่วนนี้ได้ แล้ว regular expression ง่าย ๆ จะช่วยหายอดรวมได้ ในบทเรียนนี้เราจะเดินผ่าน **process receipt with OCR**, ดึงจำนวนเงินด้วย regex, และได้ค่ารวมที่พร้อมใช้งาน

คุณจะได้เห็นตัวอย่างที่สมบูรณ์และสามารถรันได้, เข้าใจว่าทำไมโมเดลภาษาใบเสร็จจึงสำคัญ, และรับเคล็ดลับการจัดการกรณีขอบเช่นสัญลักษณ์สกุลเงินต่าง ๆ หรือการไม่มีป้าย “Total”. ไม่ต้องอ้างอิงเอกสารภายนอก—ทุกอย่างที่คุณต้องการอยู่ที่นี่

## สิ่งที่คุณจะได้เรียนรู้

- วิธีตั้งค่า Aspose OCR สำหรับการจดจำเฉพาะใบเสร็จ (โมเดลภาษา `Receipt` จะทำการแก้ไขการเอียงและลดสัญญาณรบกวนของภาพโดยอัตโนมัติ).  
- วิธีใช้ regular expression ที่ **extract amount using regex** ซึ่งทำงานกับใบเสร็จสไตล์ US ส่วนใหญ่.  
- วิธีจัดการกับรูปแบบที่พบบ่อยเช่น “TOTAL”, “Total:”, หรือ “Grand Total – $12.34”.  
- วิธีแสดงผลลัพธ์อย่างปลอดภัยและทำอย่างไรเมื่อไม่พบ pattern.  

**Prerequisites**: .NET 6+ (หรือ .NET Framework 4.7+), ใบอนุญาต Aspose OCR ที่ถูกต้องหรือเวอร์ชันทดลอง, และรูปภาพใบเสร็จที่บันทึกไว้ในเครื่อง. เท่านี้—ไม่มีแพ็กเกจ NuGet เพิ่มเติมนอกจาก Aspose.OCR.

---

## ขั้นตอนที่ 1 – ติดตั้ง Aspose OCR และเตรียมโปรเจกต์

### ทำไมเรื่องนี้สำคัญ

Aspose OCR ให้โมเดล **process receipt with OCR** ที่ออกแบบมาสำหรับการจัดการใบเสร็จโดยเฉพาะ ซึ่งรู้วิธีทำให้กระดาษที่ม้วนเป็นแผ่นตรงและละเลยสัญญาณรบกวนพื้นหลัง การใช้โมเดลข้อความทั่วไปจะทำให้เกิดข้อผิดพลาดมากกว่า โดยเฉพาะกับสแกนความละเอียดต่ำ

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **เคล็ดลับ:** เก็บไฟล์ใบอนุญาตให้อยู่ไกลจากโฟลเดอร์ควบคุมเวอร์ชันของคุณเพื่อหลีกเลี่ยงการคอมมิตโดยบังเอิญ.

---

## ขั้นตอนที่ 2 – ตั้งค่า OCR Engine สำหรับการจดจำใบเสร็จ

### ทำไมเรื่องนี้สำคัญ

โมเดลภาษา `Receipt` มีการแก้ไขการเอียงและลดสัญญาณรบกวนในตัว ซึ่งช่วยเพิ่มความแม่นยำอย่างมากบนใบเสร็จจริงที่มักจะพับหรือม้วน

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## ขั้นตอนที่ 3 – จดจำข้อความจากรูปภาพใบเสร็จ

### ทำไมเรื่องนี้สำคัญ

คุณต้องได้ข้อความดิบก่อนจึงจะใช้ regex ได้ วิธี `RecognizeImage` จะคืนค่า `OcrResult` ที่มีสตริงเต็ม, คะแนนความเชื่อมั่น, และข้อมูลอื่น ๆ หากต้องการใช้ต่อไป

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Expected OCR output (example)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## ขั้นตอนที่ 4 – สร้าง Regex เพื่อ **Extract Amount Using Regex**

### ทำไมเรื่องนี้สำคัญ

ใบเสร็จมีหลายรูปแบบ แต่คำว่า “Total” (หรือรูปแบบใกล้เคียง) ตามด้วยจำนวนเงินดอลลาร์เป็นจุดอ้างอิงที่เชื่อถือได้ pattern ด้านล่างรองรับช่องว่าง, เครื่องหมายโคลอน, เครื่องหมายขีด, และสัญลักษณ์ `$` ที่เป็นตัวเลือก

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Explanation of the pattern**

| ส่วน | ความหมาย |
|------|---------|
| `Total` | ค้นหาคำว่า “Total” (ไม่สนใจตัวพิมพ์ใหญ่/เล็ก). |
| `\s*[:\-]?` | อนุญาตให้มีช่องว่างใด ๆ แล้วตามด้วยเครื่องหมายโคลอนหรือ hyphen ที่เป็นตัวเลือก. |
| `\s*\$?` | ช่องว่างที่เป็นตัวเลือกและสัญลักษณ์ดอลลาร์ที่เป็นตัวเลือก. |
| `(\d+(\.\d{2})?)` | จับตัวเลขหนึ่งหรือหลายตัว, อาจตามด้วยจุดทศนิยมและสองตำแหน่งของเซนต์. |

---

## ขั้นตอนที่ 5 – แสดงผลยอดรวมที่ดึงได้หรือจัดการกับข้อมูลที่หายไป

### ทำไมเรื่องนี้สำคัญ

แม้ OCR ที่ดีที่สุดก็อาจพลาดคำบางคำ โดยเฉพาะบนใบเสร็จที่เบลอ การให้ fallback อย่างสุภาพจะป้องกันการหยุดทำงานและให้คุณมีจุดเชื่อมต่อสำหรับตรรกะกำหนดเอง (เช่น ขอให้ผู้ใช้ยืนยัน)

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Sample console output**

```
Total: $12.25
```

---

## ตัวอย่างทำงานเต็ม – ทุกขั้นตอนในไฟล์เดียว

ด้านล่างเป็นโปรแกรมแบบ self‑contained ที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์คอนโซลได้ รวมคอมเมนต์, การจัดการข้อผิดพลาด, และการโหลดใบอนุญาตแบบเลือกใช้

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Running the program**

1. สร้างโปรเจกต์คอนโซลใหม่ (`dotnet new console -n ReceiptReader`).  
2. เพิ่มแพ็กเกจ NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. แทนที่ `YOUR_DIRECTORY/receipt.jpg` ด้วยพาธจริงของรูปใบเสร็จ.  
4. สร้างและรัน (`dotnet run`).  

คุณควรเห็นผลลัพธ์ OCR ตามด้วย `Total: $xx.xx` หากทุกอย่างตรงกัน

---

## การจัดการกรณีขอบและรูปแบบทั่วไป

### 1. สัญลักษณ์สกุลเงินต่าง ๆ

หากคุณทำงานกับยูโร (€) หรือปอนด์ (£) ให้ขยาย pattern:

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. ไม่มีป้าย “Total”

บางใบเสร็จอาจแสดงเพียง “Grand Total”. เพิ่ม alternation:

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. มีหลายยอดรวม (เช่น “Subtotal” และ “Total”)

หาก regex ตรงกับการปรากฏครั้งแรก คุณอาจต้องการ **last** match:

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. รูปภาพความละเอียดต่ำ

- เพิ่ม DPI เมื่อสแกน (`300 DPI` เป็นค่าที่เหมาะสม).  
- ทำการพรี‑โปรเซสภาพด้วยฟิลเตอร์ลดเบลออย่างง่ายก่อนส่งให้ Aspose (อยู่นอกขอบเขตของคู่มือนี้ แต่คุ้มค่าที่จะสำรวจ).

---

## เคล็ดลับสำหรับโครงการจริง

- **Cache the OCR result** หากต้องดึงหลายฟิลด์ (ภาษี, รายการสินค้า ฯลฯ) – คุณจ่ายค่า OCR เพียงครั้งเดียว.  
- **Log the raw OCR text** ไปยังฐานข้อมูล; จะกลายเป็น audit trail ที่มีค่าเมื่อมีข้อโต้แย้งเรื่องค่าใช้จ่าย.  
- เมื่อสร้าง Web API, **run OCR in a background worker**; จะใช้เวลาหลายร้อยมิลลิวินาที ซึ่งเหมาะกับการทำงานแบบอะซิงโครนัสแต่ไม่เหมาะกับการร้องขอแบบซิงโครนัส.  
- **Validate the extracted amount** ตามกฎธุรกิจ (เช่น จำนวนต้อง > 0) ก่อนบันทึก.

---

## สรุป

เราได้ครอบคลุม **how to read receipt** ด้วย C# ใช้ Aspose OCR แล้ว **extract amount using regex** เพื่อค้นหาบรรทัดยอดรวมอย่างแม่นยำโดยอาศัยโมเดลภาษา `Receipt` ที่ให้ข้อความที่แก้ไขการเอียงและลดสัญญาณรบกวน, และ regular expression สั้น ๆ จัดการกับความแปรปรวนส่วนใหญ่ โค้ดเต็มที่แสดงด้านบนพร้อมใช้งานในโปรเจกต์ .NET ใดก็ได้ และคำแนะนำกรณีขอบเพิ่มเติมจะช่วยให้คุณมีพื้นฐานแข็งแรงสำหรับการใช้งานใน production

พร้อมก้าวต่อไปหรือยัง? ลองขยายโซลูชันเพื่อดึงรายการสินค้าแยกแต่ละรายการ, คำนวณภาษีอัตโนมัติ, หรือเชื่อมต่อกับ API การติดตามค่าใช้จ่าย. หากเจอใบเสร็จที่ทำให้ pattern พัง อย่าลืมว่าแนวทาง **regex find total** เป็นจุดเริ่มต้น—คุณสามารถปรับ pattern ให้ตรงกับท้องถิ่นของคุณได้เสมอ

ขอให้เขียนโค้ดสนุกและการประมวลผลใบเสร็จของคุณเร็ว, แม่นยำ, และอัตโนมัติเต็มที่!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}