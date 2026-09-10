---
category: general
date: 2026-01-10
description: อ่านทรัพยากรที่ฝังไว้และตั้งค่าไลเซนส์ Aspose ใน C# เรียนรู้วิธีใช้ GetManifestResourceStream,
  ฝังไฟล์ไลเซนส์, และดึงข้อมูล Assembly ที่กำลังทำงานของ .NET ในบทแนะนำเดียว.
draft: false
keywords:
- read embedded resource
- set aspose license
- use getmanifestresourcestream
- how to embed license
- get executing assembly .net
language: th
og_description: อ่านทรัพยากรที่ฝังไว้ใน .NET และตั้งค่าใบอนุญาต Aspose อย่างรวดเร็ว
  คู่มือขั้นตอนโดยละเอียดครอบคลุม GetManifestResourceStream การฝังใบอนุญาต และการใช้
  assembly ที่กำลังทำงานอยู่
og_title: อ่านทรัพยากรฝัง – ตั้งค่าใบอนุญาต Aspose ใน .NET
tags:
- C#
- .NET
- Aspose OCR
- Embedded Resources
title: อ่านทรัพยากรฝังใน .NET – คู่มือครบถ้วนสำหรับการตั้งค่าใบอนุญาต Aspose
url: /th/net/ocr-configuration/read-embedded-resource-in-net-complete-guide-to-set-aspose-l/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# อ่านทรัพยากรฝัง – คู่มือฉบับสมบูรณ์สำหรับตั้งค่าใบอนุญาต Aspose

เคยต้อง **อ่านทรัพยากรฝัง** ขณะทำงานและสงสัยว่าจะทำให้ไลบรารี Aspose OCR ของคุณได้รับใบอนุญาตโดยไม่ต้องกำหนดเส้นทางแบบฮาร์ด‑โค้ดหรือไม่? คุณไม่ได้เป็นคนเดียว ในหลายแอปพลิเคชันระดับองค์กร ไฟล์ใบอนุญาตจะอยู่ภายใน assembly ทำให้คุณไม่ต้องจัดส่งไฟล์เพิ่มเติมหรือกังวลเรื่องสิทธิ์ที่หายไป บทแนะนำนี้จะแสดงให้คุณเห็นวิธีอ่านทรัพยากรฝังและตั้งค่าใบอนุญาต Aspose โดยใช้เมธอด .NET `GetManifestResourceStream`

เราจะเดินผ่านทุกขั้นตอนที่คุณต้องการ: ฝังไฟล์ `.lic` เข้าไป, ดึงออกด้วย `GetExecutingAssembly`, และสุดท้ายนำไปใช้กับคลาส `License` ของ Aspose OCR เมื่อเสร็จแล้วคุณจะได้โซลูชันที่เป็นอิสระและทำงานได้บนโปรเจกต์ .NET ใด ๆ — ไม่ต้องใช้ไฟล์ภายนอก

## สิ่งที่คุณจะได้เรียนรู้

- **วิธีฝังไฟล์ใบอนุญาต** เข้าไปในโปรเจกต์ .NET เพื่อให้เป็นส่วนหนึ่งของ DLL ที่คอมไพล์
- วิธีที่ถูกต้องในการ **ใช้ GetManifestResourceStream** เพื่ออ่านทรัพยากรฝังนั้น
- **ตั้งค่าใบอนุญาต Aspose** ผ่านโค้ดโดยไม่ต้องยุ่งกับระบบไฟล์
- เคล็ดลับการจัดการกับปัญหาทั่วไป เช่น ชื่อทรัพยากรสะกดผิดหรือการตั้งค่า Build Action ที่หายไป
- ตัวอย่างโค้ดที่สมบูรณ์และรันได้ คุณสามารถนำไปวางในโซลูชันของคุณได้ทันที

### ข้อกำหนดเบื้องต้น

- .NET 6.0 หรือใหม่กว่า (โค้ดนี้ยังทำงานบน .NET Framework 4.x ได้เช่นกัน เพียงปรับไฟล์โปรเจกต์ให้เหมาะ)
- ติดตั้งแพคเกจ NuGet Aspose.OCR (`dotnet add package Aspose.OCR`)
- มีความคุ้นเคยพื้นฐานกับ C# และ Visual Studio (หรือ IDE ที่คุณชื่นชอบ)

หากคุณมีทุกอย่างพร้อมแล้ว ยอดเยี่ยม — ไปเริ่มกันเลย

## ขั้นตอนที่ 1: ฝังไฟล์ใบอนุญาต Aspose ลงใน Assembly ของคุณ

สิ่งแรกที่คุณต้องมีคือไฟล์ใบอนุญาตจริง (`Aspose.OCR.lic`) แทนที่จะคัดลอกไฟล์ไว้ข้าง ๆ executable คุณจะฝังมันเป็น **resource**  

1. เพิ่มไฟล์ `.lic` เข้าไปในโปรเจกต์ (เช่น สร้างโฟลเดอร์ `Resources` แล้ววางไฟล์ไว้ที่นั่น)  
2. ในคุณสมบัติของไฟล์ ตั้งค่า **Build Action** เป็น `Embedded Resource`  
   *เคล็ดลับ:* ให้โครงสร้างโฟลเดอร์เรียบง่าย ชื่อทรัพยากรเต็มจะเป็น `YourNamespace.Resources.Aspose.OCR.lic`

```text
MyApp/
 └─ Resources/
     └─ Aspose.OCR.lic   ← Build Action = Embedded Resource
```

ทำไมต้องฝัง? เพราะตอนนี้ Assembly จะบรรจุใบอนุญาตไว้ภายในตัวเอง ลดความเสี่ยงของไฟล์หายบนเซิร์ฟเวอร์ผลิต

## ขั้นตอนที่ 2: ดึงทรัพยากรฝังโดยใช้ GetExecutingAssembly

เมื่อใบอนุญาตอยู่ใน DLL แล้ว คุณต้องมีวิธี **อ่านทรัพยากรฝัง** ขณะทำงาน คลาส `Assembly` ของ .NET มีเมธอดที่ทำได้ตรงนี้

```csharp
using System.Reflection;

// Get the assembly that contains the embedded resource
Assembly currentAssembly = Assembly.GetExecutingAssembly();
```

เมธอด `GetExecutingAssembly` จะคืนค่า Assembly ที่กำลังรันอยู่ — เหมาะสำหรับหาทรัพยากรที่อยู่เคียงคู่กับโค้ดของคุณ

## ขั้นตอนที่ 3: เปิด Stream ของใบอนุญาตด้วย GetManifestResourceStream

เมื่อมีอ้างอิง Assembly อยู่ในมือแล้ว คุณสามารถเรียก `GetManifestResourceStream` เมธอดนี้จะคืนค่า `Stream` ที่คุณสามารถส่งต่อให้ Aspose ได้โดยตรง

```csharp
// Build the fully qualified resource name
string resourceName = "MyApp.Resources.Aspose.OCR.lic";

// Attempt to open the resource stream
using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);

if (licenseStream == null)
{
    throw new InvalidOperationException(
        $"Unable to locate embedded resource '{resourceName}'. " +
        "Check the namespace and Build Action settings.");
}
```

สังเกตว่าเราใช้ **using** แบบ null‑conditional (`using Stream?`) เพื่อให้สตรีมถูกกำจัดอัตโนมัติ หากชื่อไม่ถูกต้อง เราจะโยนข้อยกเว้นที่ชัดเจน — ช่วยหลีกเลี่ยงความล้มเหลวเงียบในภายหลัง

## ขั้นตอนที่ 4: นำใบอนุญาตไปใช้กับ Aspose OCR

คลาส `License` ของ Aspose ต้องการ `Stream` เรามีแล้ว ขั้นตอนสุดท้ายจึงง่ายมาก

```csharp
using Aspose.OCR;

// Create a License instance and set the license from the stream
License ocrLicense = new License();
ocrLicense.SetLicense(licenseStream);
```

เท่านี้! เอนจิน Aspose OCR ของคุณได้รับใบอนุญาตเต็มรูปแบบและพร้อมประมวลผลภาพโดยไม่มีลายน้ำทดลอง

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นโปรแกรมที่พร้อมคัดลอก‑วาง แสดงกระบวนการทั้งหมด รวมถึง `using` ที่จำเป็น การจัดการข้อผิดพลาด และการเรียก OCR อย่างง่ายเพื่อพิสูจน์ว่าใบอนุญาตทำงาน

```csharp
// Program.cs
using System;
using System.IO;
using System.Reflection;
using Aspose.OCR;

namespace MyApp
{
    class Program
    {
        static void Main()
        {
            try
            {
                // Step 1: Get the current executing assembly
                Assembly currentAssembly = Assembly.GetExecutingAssembly();

                // Step 2: Build the resource name (adjust namespace/folder as needed)
                const string resourceName = "MyApp.Resources.Aspose.OCR.lic";

                // Step 3: Retrieve the embedded license stream
                using Stream? licenseStream = currentAssembly.GetManifestResourceStream(resourceName);
                if (licenseStream == null)
                {
                    Console.WriteLine($"Failed to locate embedded resource: {resourceName}");
                    return;
                }

                // Step 4: Apply the license
                License ocrLicense = new License();
                ocrLicense.SetLicense(licenseStream);
                Console.WriteLine("Aspose OCR license applied successfully.");

                // Optional: Quick test – recognize text from a sample image
                var ocrEngine = new OcrEngine();
                ocrEngine.Image = ImageStream.FromFile("sample.png"); // replace with your image path
                if (ocrEngine.Process())
                {
                    Console.WriteLine("OCR Result:");
                    Console.WriteLine(ocrEngine.Text);
                }
                else
                {
                    Console.WriteLine("OCR processing failed.");
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

### ผลลัพธ์ที่คาดหวัง

เมื่อคุณรันโปรแกรมบนเครื่องที่มีใบอนุญาตฝังอย่างถูกต้อง คุณควรเห็น:

```
Aspose OCR license applied successfully.
OCR Result:
[Detected text from sample.png]
```

หากไม่พบสตรีมของใบอนุญาต คอนโซลจะรายงานชื่อทรัพยากรที่หายไป เพื่อให้คุณตรวจสอบ **Build Action** และ namespace อีกครั้ง

## ปัญหาที่พบบ่อยและวิธีหลีกเลี่ยง

| ปัญหา | สาเหตุ | วิธีแก้ |
|-------|--------|--------|
| **ชื่อทรัพยากรไม่ตรงกัน** | .NET สร้างชื่อทรัพยากรจาก default namespace + เส้นทางโฟลเดอร์ | ใช้ `Assembly.GetManifestResourceNames()` เพื่อตรวจสอบชื่อที่มีอยู่และยืนยันสตริงที่ถูกต้อง |
| **ไฟล์ใบอนุญาตไม่ได้ตั้งเป็น Embedded Resource** | ค่า Build Action เริ่มต้นเป็น `Content` | เปลี่ยนเป็น `Embedded Resource` ในคุณสมบัติของไฟล์ |
| **รันจาก Assembly ที่ต่างกัน** | หากเรียกโค้ดจากคลาสไลบรารี `GetExecutingAssembly()` อาจคืนค่าไลบรารีแทน exe หลัก | ใช้ `Assembly.GetEntryAssembly()` หรือส่ง Assembly ที่ถูกต้องโดยตรง |
| **Stream ถูกกำจัดก่อนใช้** | ใช้บล็อก `using` ที่ปิดสตรีมเร็วเกินไป | เก็บ `using` ไว้รอบการเรียก `SetLicense` ตามที่แสดงข้างต้น |
| **เวอร์ชัน Aspose.OCR ไม่ตรงกัน** | เวอร์ชันใหม่อาจต้องรูปแบบใบอนุญาตที่ต่างกัน | ดาวน์โหลดใบอนุญาตล่าสุดจากบัญชี Aspose ของคุณและฝังใหม่ |

## ใช้เทคนิคเดียวกันกับไฟล์ฝังอื่น ๆ

รูปแบบ **อ่านทรัพยากรฝัง** แล้ว **ใช้ GetManifestResourceStream** ทำงานได้กับไฟล์ทุกประเภท: คอนฟิก JSON, รูปภาพ, หรือแม้แต่ DLL เนทีฟ เพียงปรับ `resourceName` และวิธีใช้สตรีมให้เหมาะ

```csharp
// Example: Load an embedded JSON config
string jsonName = "MyApp.Resources.Config.appsettings.json";
using var jsonStream = Assembly.GetExecutingAssembly()
                               .GetManifestResourceStream(jsonName);
using var reader = new StreamReader(jsonStream);
string json = await reader.ReadToEndAsync();
```

## ภาพรวมแบบภาพ

![Diagram illustrating how to read embedded resource and set Aspose license](read-embedded-resource-diagram.png)

*ข้อความแทนภาพ:* อ่านทรัพยากรฝัง – แผนภาพแสดงการฝัง, การดึงด้วย GetManifestResourceStream, และการนำใบอนุญาต Aspose ไปใช้

## สรุป

เราได้ครอบคลุมวิธี **อ่านทรัพยากรฝัง** ใน Assembly ของ .NET ขั้นตอนที่แม่นยำในการ **ใช้ GetManifestResourceStream** และวิธีที่สะอาดในการ **ตั้งค่าใบอนุญาต Aspose** โดยไม่ต้องเปิดไฟล์บนดิสก์ การฝังใบอนุญาตช่วยลดปัญหาการจัดจำหน่ายและทำให้แอปของคุณพกพาได้ง่ายขึ้น

## ต่อไปคุณควรทำอะไร?

- **อัตโนมัติการอัปเดตใบอนุญาต:** เขียนสคริปต์ในขั้นตอนการสร้างที่แทนที่ไฟล์ `.lic` ฝังเมื่อคุณต่ออายุการสมัคร Aspose  
- **รักษาความปลอดภัยของทรัพยากร:** พิจารณาเข้ารหัสใบอนุญาตก่อนฝังและถอดรหัสที่รันไทม์เพื่อเพิ่มการปกป้อง  
- **สำรวจผลิตภัณฑ์ Aspose อื่น:** วิธีเดียวกันใช้ได้กับ Aspose.Words, Aspose.PDF ฯลฯ แต่ละตัวมีคลาส `License` ของตนเอง

ลองทดลองดู — คุณอาจฝังหลายใบอนุญาตสำหรับโมดูลต่าง ๆ หรือเปลี่ยนเป็นการกำหนดชื่อทรัพยากรจากคอนฟิก การทำได้ไม่มีขีดจำกัด

---

*Happy coding! หากเจออุปสรรคใด ๆ คอมเมนต์ด้านล่างหรือดูฟอรั่มของ Aspose เพื่อหาตัวอย่างเพิ่มเติม*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}