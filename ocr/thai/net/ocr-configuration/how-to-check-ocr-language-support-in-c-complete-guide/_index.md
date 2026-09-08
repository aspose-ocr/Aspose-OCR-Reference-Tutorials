---
category: general
date: 2026-09-08
description: เรียนรู้วิธีตรวจสอบการสนับสนุนภาษา OCR ใน C# ด้วย Aspose.OCR. ตรวจสอบโมดูลภาษา,
  จัดการกับแพ็คที่หายไป, และทำให้ฟีเจอร์ OCR ของคุณเชื่อถือได้.
draft: false
keywords:
- check OCR language
- OCR language support
- Aspose OCR C#
- verify OCR language modules
- OCR language availability
lastmod: 2026-09-08
og_description: เรียนรู้วิธีตรวจสอบการสนับสนุนภาษา OCR ใน C# ด้วย Aspose.OCR. ตรวจสอบโมดูลภาษา,
  จัดการกับแพ็คที่หายไป, และทำให้ฟีเจอร์ OCR ของคุณเชื่อถือได้.
og_image_alt: Diagram of checking OCR language support in a C# console app
og_title: ตรวจสอบการสนับสนุนภาษา OCR ใน C# – คู่มือแบบขั้นตอนต่อขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to check OCR language support in C# using Aspose.OCR. Verify
    language modules, handle missing packs, and keep your OCR feature reliable.
  headline: Check OCR language support in C# – Step‑by‑step guide
  type: TechArticle
- description: Learn how to check OCR language support in C# using Aspose.OCR. Verify
    language modules, handle missing packs, and keep your OCR feature reliable.
  name: Check OCR language support in C# – Step‑by‑step guide
  steps:
  - name: create a minimal console project
    text: A console app lets you see output instantly without UI boilerplate. Create
      a new project with `dotnet new console -n OcrLanguageCheck` and add the Aspose.OCR
      package via `dotnet add package Aspose.OCR`. This environment mirrors any other
      .NET host (ASP.NET, WinForms, Azure Functions) once you copy t
  - name: implement the language‑check helper
    text: The core of **how to check OCR language** lives in the `CheckLanguageSupport`
      method. It receives a `Language` enum and returns a boolean. The method also
      logs the result, which is useful for diagnostics.
  - name: call the helper for a specific language
    text: In `Main`, invoke `CheckLanguageSupport(Language.Japanese)`. The method
      will print “Japanese language pack is available.” or a warning if it isn’t.
      You can replace `Language.Japanese` with any enum value such as `Language.French`,
      `Language.Spanish`, or `Language.English`.
  - name: handling missing DLLs at runtime
    text: If the language pack DLL isn’t in the same folder as the executable, `IsLanguageAvailable`
      returns `false`. Ensure the DLLs are copied to the output directory. For self‑contained
      single‑file deployments, list the language DLLs as **additional files** in the
      publish profile. **Pro tip:** Add a post‑b
  - name: avoid version mismatches
    text: Aspose.OCR releases language packs in lockstep with the core library. If
      you upgrade the core NuGet package but keep an older language DLL, the version
      check will fail and the method will return `false`. Always keep the language
      DLL version identical to the core package version.
  - name: cache the result for high‑throughput services
    text: '`IsLanguageAvailable` is thread‑safe, but repeatedly creating `OcrEngine`
      instances in a high‑traffic API can add overhead. Perform the language check
      once during application startup, store the result in a static dictionary, and
      reuse it for each OCR request.'
  type: HowTo
- questions:
  - answer: No single method returns all available languages, but you can iterate
      over `Enum.GetValues(typeof(Language))` and call `IsLanguageAvailable` for each
      entry.
    question: Can I check multiple languages in one call?
  - answer: Yes. Aspose.OCR is cross‑platform; just ensure the native language DLLs
      are present for the target OS.
    question: Does the check work on Linux/macOS?
  - answer: Most language DLLs are under 10 MB. The largest, Chinese‑Traditional,
      is approximately 12 MB, which is still trivial for modern deployment pipelines.
    question: How large can a language pack be?
  - answer: The `IsLanguageAvailable` method works in evaluation mode, but a full
      license is needed for production deployments to avoid evaluation watermarks.
    question: Is a license required for the language check?
  - answer: Aspose provides a REST endpoint for language pack downloads; you can call
      it from your app, store the DLL locally, and reload the engine without restarting
      the process.
    question: Can I download missing language packs programmatically?
  type: FAQPage
tags:
- OCR
- Aspose.OCR
- C#
- .NET
title: ตรวจสอบการสนับสนุนภาษา OCR ใน C# – คู่มือแบบขั้นตอนต่อขั้นตอน
url: /th/net/ocr-configuration/how-to-check-ocr-language-support-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ตรวจสอบการสนับสนุนภาษา OCR ใน C# – คู่มือฉบับสมบูรณ์

ในหลายโครงการจริง ๆ เครื่องมือ OCR ทำงานเบื้องหลังโดยแปลงภาพสแกนเป็นข้อความที่สามารถค้นหาได้ ก่อนที่คุณจะส่งมอบโซลูชัน คุณต้องมีวิธีที่เชื่อถือได้ในการ **ตรวจสอบโมดูลภาษา OCR** เพื่อให้ฟีเจอร์ไม่ล้มเหลวในขณะรันไทม์ คู่มือนี้จะแสดงให้คุณเห็นขั้นตอนต่อขั้นตอนว่าอย่างไรตรวจสอบการสนับสนุนภาษา OCR ใน C# ด้วย Aspose.OCR ทำไมการตรวจสอบนี้สำคัญ และวิธีตอบสนองเมื่อแพ็คเกจภาษาที่ต้องการหายไป

คุณจะได้เรียนรู้ว่า:

* ตรวจสอบว่าภาษาเฉพาะ (เช่นญี่ปุ่นในตัวอย่างของเรา) ถูกติดตั้งหรือไม่
* ตอบสนองอย่างสุภาพเมื่อโมดูลภาษาไม่มีอยู่
* ขยายการตรวจสอบไปยังภาษาใดก็ได้ที่คุณต้องการ เพื่อ **กำหนดความสามารถของ OCR ภาษา** ได้ในขณะรันไทม์

ไม่ต้องอ้างอิงเอกสารภายนอก—เพียงคัดลอก‑วางโค้ดและทำตามเคล็ดลับการปฏิบัติที่ดีที่สุดไม่กี่ข้อ

![แผนภาพการตรวจสอบการสนับสนุนภาษา OCR](image.png "แผนภาพแสดงวิธีตรวจสอบการสนับสนุนภาษา OCR ในแอปคอนโซล C#")
[แผนภาพการตรวจสอบการสนับสนุนภาษา OCR](image.png "แผนภาพแสดงวิธีตรวจสอบการสนับสนุนภาษา OCR ในแอปคอนโซล C#")

## คำตอบด่วน
คลาส `OcrEngine` ให้ฟังก์ชัน OCR และ enum `Language` แสดงรายการแพ็คเกจภาษาที่รองรับ

- **ฉันสามารถตรวจสอบการสนับสนุนภาษาในขณะรันไทม์ได้หรือไม่?** ได้, เรียก `OcrEngine.IsLanguageAvailable` พร้อมค่าของ enum `Language` ที่ต้องการ  
- **ต้องใช้ DLL แยกสำหรับแต่ละภาษาไหม?** Aspose.OCR จัดแพ็คเกจภาษาเป็น DLL แยก; ให้รวม DLL ที่คุณตั้งใจจะใช้  
- **จะเกิดอะไรขึ้นถ้า DLL ของภาษาหายไป?** การตรวจสอบจะคืนค่า `false`; คุณสามารถแสดงข้อความแจ้งผู้ใช้หรือดาวน์โหลดแพ็คเกจได้  
- **การตรวจสอบนี้ปลอดภัยต่อเธรดหรือไม่?** แน่นอน—`IsLanguageAvailable` สามารถเรียกจากหลายเธรดพร้อมกันได้โดยไม่ต้องล็อก  
- **เวอร์ชัน .NET ใดบ้างที่รองรับ?** .NET 6.0 หรือใหม่กว่า, และไลบรารียังทำงานกับ .NET Core 3.1 และ .NET Framework 4.7.2

## การตรวจสอบการสนับสนุนภาษา OCR คืออะไร?
**การตรวจสอบการสนับสนุนภาษา OCR หมายถึงการยืนยันว่า DLL ของแพ็คเกจภาษาที่ต้องการมีอยู่และเข้ากันได้กับไลบรารีหลักของ Aspose.OCR** เมื่อคุณเรียก `OcrEngine.IsLanguageAvailable` เอนจินจะค้นหาแอสเซมบลีภาษาที่สอดคล้องกันในโฟลเดอร์แอปพลิเคชันและตรวจสอบเวอร์ชัน หาก DLL ไม่พบหรือเวอร์ชันไม่ตรง วิธีจะคืนค่า `false` ทำให้คุณหลีกเลี่ยงข้อยกเว้นในขณะรันไทม์

## ทำไมต้องตรวจสอบโมดูลภาษา OCR ก่อนประมวลผลภาพ?
การตรวจสอบโมดูลภาษา OCR ป้องกันการพังของแอปโดยไม่คาดคิดและปรับปรุงประสบการณ์ผู้ใช้ Aspose.OCR รองรับ **กว่า 30 แพ็คเกจภาษา** — รวมถึงญี่ปุ่น, อาหรับ, และฮินดี — ดังนั้นการขาดแพ็คเกจอาจทำให้การประมวลผลหยุดชะงักสำหรับผู้ใช้ในหลายภูมิภาค การตรวจสอบล่วงหน้าช่วยให้คุณสามารถ:

* แสดงข้อความข้อผิดพลาดที่ชัดเจนแทนข้อยกเว้นที่ไม่ได้จัดการ  
* เสนอลิงก์ดาวน์โหลดอัตโนมัติสำหรับแพ็คเกจภาษาที่หายไป  
* ถอยกลับไปใช้ภาษาตั้งต้น (มักเป็นอังกฤษ) เพื่อให้เวิร์กโฟลว์ดำเนินต่อได้  

ข้อเท็จจริงเชิงปริมาณ: Aspose.OCR สามารถประมวลผล **เอกสารขนาดสูงสุด 200 หน้า** ในคำขอเดียวโดยคงการใช้หน่วยความจำต่ำกว่า 150 MB หากโหลด DLL ภาษาที่เหมาะสมแล้ว

## ข้อกำหนดเบื้องต้น
- .NET 6.0 หรือใหม่กว่า (โค้ดยังทำงานบน .NET Core 3.1 และ .NET Framework 4.7.2)  
- ติดตั้งแพคเกจ NuGet `Aspose.OCR` (`Aspose.OCR`)  
- มีโมดูลภาษาที่คุณต้องการใช้ (เช่น `Aspose.OCR.Japanese.dll`)  

หากมีสิ่งใดขาดหาย โค้ดที่เราจะเขียนต่อไปจะแจ้งให้คุณทราบว่าปัญหาอยู่ที่ไหน

## วิธีตรวจสอบการสนับสนุนภาษา OCR ใน C# ทีละขั้นตอน

โหลดเอนจิน OCR ครั้งเดียว แล้วสอบถามว่าภาษาใดพร้อมใช้งาน วิธีต่อไปนี้สรุปตรรกะไว้ในเมธอดเดียว:

```csharp
// Program.cs – entry point for the demo
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // We'll call a helper method that checks the language support.
        CheckLanguageSupport(Language.Japanese);
    }

    // Helper that encapsulates the check logic.
    static void CheckLanguageSupport(Language language)
    {
        // Step 2 lives here – see the next section.
    }
}
```

**คำตอบโดยตรง:** เรียกเมธอดสแตติก `OcrEngine.IsLanguageAvailable` พร้อมค่า enum `Language` ที่ต้องการ; จะคืนค่า `true` หาก DLL ที่ตรงกันมีอยู่และเข้ากันได้กับเวอร์ชัน, มิฉะนั้น `false` บรรทัดเดียวนี้ให้ข้อมูลว่าภาษาใช้งานได้หรือไม่โดยไม่มีข้อยกเว้น

### ขั้นตอนที่ 1: สร้างโปรเจกต์คอนโซลขนาดเล็กที่สุด

แอปคอนโซลช่วยให้คุณเห็นผลลัพธ์ทันทีโดยไม่ต้องเขียน UI สร้างโปรเจกต์ใหม่ด้วย `dotnet new console -n OcrLanguageCheck` แล้วเพิ่มแพคเกจ Aspose.OCR ผ่าน `dotnet add package Aspose.OCR` สภาพแวดล้อมนี้สะท้อนการโฮสต์ .NET ใด ๆ (ASP.NET, WinForms, Azure Functions) หลังจากคัดลอกเมธอดช่วยเหลือ

### ขั้นตอนที่ 2: Implement ตัวช่วยตรวจสอบภาษา

แกนของ **วิธีตรวจสอบ OCR ภาษา** อยู่ในเมธอด `CheckLanguageSupport` ซึ่งรับค่า enum `Language` และคืนค่า boolean เมธอดยังบันทึกผลลัพธ์เพื่อการวินิจฉัย

```csharp
static void CheckLanguageSupport(Language language)
{
    // Ask Aspose.OCR whether the requested language is installed.
    bool isSupported = OcrEngine.IsLanguageAvailable(language);

    // Provide clear feedback to the developer or end‑user.
    Console.WriteLine($"{language} language module installed: {isSupported}");

    // Optional: react if the module is missing.
    if (!isSupported)
    {
        Console.WriteLine("⚠️  Language pack not found. You can download it from Aspose's website:");
        Console.WriteLine("https://downloads.aspose.com/ocr/net");
        // In a real app you might throw an exception or fall back to a default language.
    }
}
```

### ขั้นตอนที่ 3: เรียกตัวช่วยสำหรับภาษาที่กำหนด

ใน `Main` ให้เรียก `CheckLanguageSupport(Language.Japanese)` เมธอดจะพิมพ์ “Japanese language pack is available.” หรือคำเตือนหากไม่มี คุณสามารถเปลี่ยน `Language.Japanese` เป็นค่า enum ใดก็ได้ เช่น `Language.French`, `Language.Spanish`, หรือ `Language.English`

```csharp
// Example: user selects language via a UI dropdown.
Language userChoice = GetUserSelectedLanguage(); // pseudo‑method
CheckLanguageSupport(userChoice);
```

### ขั้นตอนที่ 4: จัดการ DLL ที่หายไปในขณะรันไทม์

ถ้าแพ็คเกจ DLL ของภาษาไม่ได้อยู่ในโฟลเดอร์เดียวกับไฟล์ exe, `IsLanguageAvailable` จะคืนค่า `false` ตรวจสอบให้แน่ใจว่า DLL ถูกคัดลอกไปยังไดเรกทอรีเอาต์พุต สำหรับการปรับใช้แบบไฟล์เดียวแบบ self‑contained ให้ระบุ DLL ภาษานั้นเป็น **additional files** ในโปรไฟล์การเผยแพร่

**เคล็ดลับ:** เพิ่มสคริปต์ PowerShell หลังการสร้างที่ตรวจสอบการมีอยู่ของ DLL ที่ต้องการ:

```powershell
$required = @("Aspose.OCR.Japanese.dll", "Aspose.OCR.English.dll")
foreach ($dll in $required) {
    if (-Not (Test-Path "$PSScriptRoot\bin\Release\net6.0\$dll")) {
        Write-Host "Missing $dll – please add it to your project."
    }
}
```

### ขั้นตอนที่ 5: ป้องกันการไม่ตรงกันของเวอร์ชัน

Aspose.OCR ปล่อยแพ็คเกจภาษาให้สอดคล้องกับไลบรารีหลัก หากคุณอัปเกรดแพคเกจ NuGet หลักแต่ยังคงใช้ DLL ภาษาเก่า การตรวจสอบเวอร์ชันจะล้มและเมธอดจะคืนค่า `false` ควรทำให้เวอร์ชัน DLL ภาษาเท่ากับเวอร์ชันของแพคเกจหลักเสมอ

### ขั้นตอนที่ 6: แคชผลลัพธ์สำหรับบริการที่รับคำขอสูง

`IsLanguageAvailable` ปลอดภัยต่อเธรด แต่การสร้างอินสแตนซ์ `OcrEngine` ซ้ำ ๆ ใน API ที่รับคำขอจำนวนมากอาจเพิ่มภาระงาน ทำการตรวจสอบภาษาเพียงครั้งเดียวระหว่างการเริ่มแอป, เก็บผลลัพธ์ในพจนานุกรมสแตติก, แล้วใช้ซ้ำสำหรับแต่ละคำขอ OCR

## ปัญหาที่พบบ่อยและวิธีแก้

### DLL ที่หายไป
*อาการ*: `IsLanguageAvailable` คืนค่า `false` เสมอ  
*วิธีแก้*: ยืนยันว่า DLL ภาษา (เช่น `Aspose.OCR.Japanese.dll`) อยู่ในโฟลเดอร์เดียวกับไฟล์ exe หรือระบุเป็น additional file ในการเผยแพร่แบบไฟล์เดียว ใช้สคริปต์ PowerShell ด้านบนเพื่ออัตโนมัติการตรวจสอบ

### ไม่ตรงกันของเวอร์ชัน
*อาการ*: หลังอัปเดต `Aspose.OCR` ผ่าน NuGet การตรวจสอบภาษาไม่ทำงาน  
*วิธีแก้*: ติดตั้งแพ็คเกจภาษาใหม่จาก NuGet หรือดาวน์โหลดเวอร์ชันที่ตรงกันจากพอร์ทัล Aspose เวอร์ชันของแพคเกจหลักและ DLL ภาษาต้องตรงกันอย่างแม่นยำ

### การทำงานใน Docker
*อาการ*: การสร้างคอนเทนเนอร์สำเร็จ แต่การตรวจสอบภาษาไม่ทำงานในขณะรันไทม์  
*วิธีแก้*: คัดลอก DLL ภาษาลงในไดเรกทอรี `/app` ของ Docker image และตั้งค่า `LD_LIBRARY_PATH` (Linux) หรือให้แน่ใจว่า DLL อยู่ใน `PATH` (Windows) การสร้างแบบ multi‑stage ที่เผยแพร่ไบนารี self‑contained พร้อมแพ็คเกจภาษาจะช่วยแก้ปัญหาได้

### สภาพแวดล้อมหลายเธรด
*อาการ*: เกิดข้อผิดพลาด `LicenseException` อย่างสุ่มเมื่อมีการร้องขอ OCR จำนวนมากพร้อมกัน  
*วิธีแก้*: เริ่มต้นไลเซนส์ครั้งเดียวที่การเริ่มแอป, แล้วใช้อินสแตนซ์ `OcrEngine` เดียวกันหรือสร้างพูลของเอนจินที่กำหนดค่าไว้ล่วงหน้า แคชผลลัพธ์การตรวจสอบภาษาเพื่อหลีกเลี่ยงการตรวจสอบซ้ำหลายครั้ง

## คำถามที่พบบ่อย

**ถาม: ฉันสามารถตรวจสอบหลายภาษาในคำสั่งเดียวได้หรือไม่?**  
ตอบ: ไม่มีเมธอดเดียวที่คืนค่าภาษาทั้งหมด, แต่คุณสามารถวนลูป `Enum.GetValues(typeof(Language))` แล้วเรียก `IsLanguageAvailable` สำหรับแต่ละค่าได้

**ถาม: การตรวจสอบทำงานบน Linux/macOS หรือไม่?**  
ตอบ: ทำงานได้. Aspose.OCR รองรับหลายแพลตฟอร์ม; เพียงให้แน่ใจว่า DLL ภาษาเนทีฟอยู่ในตำแหน่งที่เหมาะสมสำหรับ OS นั้น

**ถาม: แพ็คเกจภาษามีขนาดใหญ่แค่ไหน?**  
ตอบ: ส่วนใหญ่ต่ำกว่า 10 MB. แพ็คเกจที่ใหญ่ที่สุดคือ Chinese‑Traditional ประมาณ 12 MB ซึ่งยังถือว่าเล็กสำหรับ pipeline การปรับใช้สมัยใหม่

**ถาม: จำเป็นต้องมีไลเซนส์เพื่อทำการตรวจสอบหรือไม่?**  
ตอบ: เมธอด `IsLanguageAvailable` ทำงานในโหมดประเมินผล, แต่ต้องมีไลเซนส์เต็มรูปแบบสำหรับการใช้งานในโปรดักชันเพื่อหลีกเลี่ยงลายน้ำประเมินผล

**ถาม: ฉันสามารถดาวน์โหลดแพ็คเกจภาษาที่หายไปโดยอัตโนมัติได้หรือไม่?**  
ตอบ: Aspose มี REST endpoint สำหรับดาวน์โหลดแพ็คเกจภาษา; คุณสามารถเรียกจากแอปของคุณ, เก็บ DLL ไว้ในเครื่อง, แล้วรีโหลดเอนจินโดยไม่ต้องรีสตาร์ทกระบวนการ

## สรุป

เราได้ครอบคลุมทุกอย่างที่คุณต้องการเพื่อ **ตรวจสอบการสนับสนุนภาษา OCR** ในสภาพแวดล้อม C# ด้วย Aspose.OCR:

* การเรียกสแตติกเดียว (`OcrEngine.IsLanguageAvailable`) บอกได้ว่ามีแพ็คเกจภาษาติดตั้งหรือไม่  
* ห่อเมธอดนั้นในฟังก์ชันช่วยเหลือเพื่อให้โค้ดของคุณสะอาดและอ่านง่าย  
* เตรียมพร้อมรับสถานการณ์ DLL หาย, เวอร์ชันไม่ตรง, และการทำงานหลายเธรด  
* ขยายรูปแบบนี้เพื่อ **กำหนด OCR ภาษา** แบบไดนามิกตามการป้อนของผู้ใช้หรือการตั้งค่า

โดยการบูรณาการการตรวจสอบเหล่านี้ตั้งแต่ต้น คุณสามารถส่งมอบแอปที่เปิดใช้ OCR ด้วยความมั่นใจ, ให้ข้อมูลชัดเจนเมื่อโมดูลภาษาไม่มีอยู่, และหลีกเลี่ยงการพังของแอป ขั้นต่อไป? ลองโหลดภาพจริง, ทำ OCR ด้วยภาษาที่ตรวจสอบแล้ว, หรือสร้าง UI ให้ผู้ใช้เลือกภาษาที่ต้องการและแสดงคำเตือนเมื่อแพ็คเกจยังไม่ได้ติดตั้ง

ขอให้เขียนโค้ดสนุกนะครับ, และขอให้ OCR ของคุณอ่านอักขระที่ถูกต้องเสมอ!

---

**อัปเดตล่าสุด:** 2026-09-08  
**ทดสอบกับ:** Aspose.OCR 24.10 for .NET  
**ผู้เขียน:** Aspose  






```csharp
// FullDemo.cs – complete, runnable example
using System;
using Aspose.OCR;

class FullDemo
{
    static void Main()
    {
        // List of languages we care about.
        Language[] languagesToCheck = { Language.Japanese, Language.English, Language.French };

        foreach (var lang in languagesToCheck)
        {
            VerifyLanguage(lang);
        }

        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }

    static void VerifyLanguage(Language lang)
    {
        bool available = OcrEngine.IsLanguageAvailable(lang);
        Console.WriteLine($"{lang} language module installed: {available}");

        if (!available)
        {
            Console.WriteLine($"⚠️  {lang} pack missing. Download from:");
            Console.WriteLine("https://downloads.aspose.com/ocr/net");
        }
        else
        {
            // Optional: demonstrate a quick OCR run with the verified language.
            // (We skip actual image processing to keep the demo lightweight.)
            Console.WriteLine($"✅  Ready to run OCR with {lang}.");
        }

        Console.WriteLine(new string('-', 40));
    }
}
```

```
Japanese language module installed: True
✅  Ready to run OCR with Japanese.
----------------------------------------
English language module installed: True
✅  Ready to run OCR with English.
----------------------------------------
French language module installed: False
⚠️  French pack missing. Download from:
https://downloads.aspose.com/ocr/net
----------------------------------------

Press any key to exit...
```

## บทแนะนำที่เกี่ยวข้อง

- [Extract image text C# with language selection using Aspose.OCR](/ocr/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How To Apply License In Aspose Ocr Step By Step C Guide](/ocr/net/ocr-configuration/how-to-apply-license-in-aspose-ocr-step-by-step-c-guide/)
- [How To Enable Gpu For Aspose Ocr Step By Step Guide](/ocr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}