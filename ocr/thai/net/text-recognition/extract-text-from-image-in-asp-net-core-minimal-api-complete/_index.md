---
category: general
date: 2026-05-25
description: เรียนรู้วิธีดึงข้อความจากรูปภาพด้วย API ASP.NET Core ขั้นต่ำ อัปโหลดรูปภาพผ่าน
  POST อ่านข้อมูลแบบ multipart form และทำ OCR บนรูปภาพ.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: th
og_description: ดึงข้อความจากภาพโดยใช้ ASP.NET Core API แบบ Minimal คู่มือนี้แสดงวิธีอัปโหลดภาพผ่าน
  POST, อ่านข้อมูลแบบ multipart form, และทำ OCR บนภาพ
og_title: สกัดข้อความจากภาพใน ASP.NET Core – ทีละขั้นตอน
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: สกัดข้อความจากรูปภาพใน ASP.NET Core Minimal API – คู่มือฉบับสมบูรณ์
url: /th/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ดึงข้อความจากภาพใน ASP.NET Core Minimal API – คู่มือฉบับสมบูรณ์

เคยสงสัยไหมว่า **ดึงข้อความจากภาพ** อย่างไรโดยไม่ต้องพึ่งพาเฟรมเวิร์กขนาดใหญ่? คุณไม่ได้อยู่คนเดียว นักพัฒนาหลายคนต้องการวิธีที่รวดเร็วให้ผู้ใช้ลากรูปภาพแล้วได้ข้อความดิบกลับมา ไม่ว่าจะเป็นการสแกนใบเสร็จ, แปลงโน้ตมือเขียนเป็นดิจิทัล, หรือเสริมดัชนีการค้นหา

ในบทเรียนนี้เราจะสร้าง ASP.NET Core Minimal API ขนาดเล็กที่ **อัปโหลดภาพผ่าน POST**, แยก payload แบบ *multipart/form‑data*, แล้ว **perform OCR on image** ด้วย singleton `OcrEngine` เมื่อเสร็จคุณจะได้แอปที่พร้อมรันที่สามารถใส่ลงในโปรเจกต์ .NET 8 ใดก็ได้และเริ่มดึงข้อความจากภาพได้ทันที

## สิ่งที่คุณจะสร้าง

- แอปเว็บขนาดเล็กที่รับฟังที่ `/ocr`
- Endpoint ที่รับไฟล์ภาพผ่านคำขอ `multipart/form-data` แบบ POST
- โลจิกที่อ่านไฟล์ที่อัปโหลด, ส่งให้ OCR engine, แล้วคืนผลเป็นข้อความธรรมดา
- ตัวอย่างการเร่งความเร็วด้วย GPU (คอมเมนต์ไว้) สำหรับผู้ที่มีการ์ดที่รองรับ

**ข้อกำหนดเบื้องต้น**  
- .NET 8 SDK (หรือใหม่กว่า)  
- ความคุ้นเคยพื้นฐานกับ C# และ command line  
- ไลบรารี OCR ที่มีคลาส `OcrEngine` (ตัวอย่างสมมติว่ามี NuGet package)

ถ้าคุณมีทั้งหมดนี้แล้ว ไปต่อกันเลย

## ขั้นตอนที่ 1: ตั้งค่าโปรเจกต์และเพิ่มแพคเกจ OCR

แรกเริ่มสร้างโปรเจกต์เว็บใหม่และดึงไลบรารี OCR เข้ามา

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **เคล็ดลับ:** คอยอัปเดต dependencies ของคุณ เวอร์ชันใหม่มักมาพร้อมกับประสิทธิภาพที่ดีขึ้น โดยเฉพาะการ inference ที่เร่งด้วย GPU

## ขั้นตอนที่ 2: ลงทะเบียน Singleton OCR Engine (บริการหลัก)

เราต้องการอินสแตนซ์ `OcrEngine` เพียงหนึ่งตัวสำหรับทั้งแอป – ไม่ต้องสร้าง engine ใหม่ทุกคำขอ ลงทะเบียนใน service container ของ builder

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**ทำไมต้องเป็น singleton?**  
การสร้าง OCR engine มีค่าใช้จ่ายสูง – คิดถึงการโหลดน้ำหนักของ neural‑network เข้า memory การใช้อินสแตนซ์เดียวช่วยประหยัด CPU และ RAM ทำให้เวลาตอบสนองของทุกคำขอ `/ocr` เร็วขึ้น

## ขั้นตอนที่ 3: สร้างแอปพลิเคชัน

ตอนนี้เราจะ materialize วัตถุ `WebApplication`

```csharp
var app = builder.Build();
```

บรรทัดนั้นดูเหมือนเวทมนตร์ แต่เบื้องหลังมันได้เชื่อม routing, middleware, และ DI container ที่เราตั้งค่าไว้แล้ว

## ขั้นตอนที่ 4: กำหนด POST Endpoint – “Upload Image via POST”

นี่คือหัวใจของบทเรียน: endpoint ที่ **upload image via POST**, อ่าน payload แบบ multipart, แล้วส่งข้อมูลให้ OCR engine

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### วิเคราะห์โลจิก

| ขั้นตอน | สิ่งที่เกิดขึ้น | ทำไมถึงสำคัญ |
|------|--------------|----------------|
| **ReadFormAsync** | แยกคำขอ *multipart/form-data* ที่เข้ามา | หากไม่มีคุณจะไม่สามารถเข้าถึงไฟล์ที่อัปโหลดได้ |
| **form.Files["image"]** | ดึงไฟล์ที่มีชื่อฟิลด์ `image` | ทำให้สัญญา (contract) กับผู้เรียกคาดเดาได้ |
| **Content‑type check** | ตรวจสอบว่าไฟล์เป็นภาพ (เช่น `image/png`) | ป้องกัน OCR engine จากการทำงานกับข้อมูลที่ไม่ใช่ภาพ |
| **Image.FromStream** | แปลงสตรีมดิบเป็น `System.Drawing.Image` | ไลบรารี OCR ต้องการอ็อบเจ็กต์ `Image` ไม่ใช่ byte array |
| **ocr.Recognize(img)** | เรียก OCR engine เพื่อ **how to recognize text from image** | นี่คือขั้นตอนหลักของ **perform OCR on image** |
| **Results.Text** | ส่งกลับผลลัพธ์เป็นข้อความธรรมดา | รูปแบบง่ายต่อการใช้งานต่อในบริการอื่น |

## ขั้นตอนที่ 5: รัน API

สุดท้าย เริ่มเว็บเซิร์ฟเวอร์

```csharp
app.Run();
```

เมื่อคุณรัน `dotnet run` API จะฟังที่ `http://localhost:5000` (หรือพอร์ตที่คุณกำหนด) คุณสามารถทดสอบด้วย `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**ผลลัพธ์ที่คาดหวัง:** คอนโซลจะแสดงอักขระที่จำได้ เช่น:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

หากภาพเบลอหรือภาษาที่ใช้ไม่รองรับ OCR engine จะคืนสตริงว่างหรือข้อความข้อผิดพลาด – ควรจัดการกรณีเหล่านี้ในโค้ด production

## กรณีขอบและแนวปฏิบัติที่ดีที่สุด

### 1. ไฟล์ขนาดใหญ่

ขีดจำกัด body ของคำขอเริ่มต้นที่ 30 MB หากต้องจัดการสแกนที่ใหญ่กว่านี้อาจต้องปรับ:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR แบบอะซิงโครนัส

บางไลบรารี OCR มีเมธอด async (`RecognizeAsync`) หากมีให้แทนที่ `ocr.Recognize(img)` ด้วย `await ocr.RecognizeAsync(img)` และทำให้ lambda เป็น `async`

### 3. พิจารณาด้านความปลอดภัย

- **ตรวจสอบขนาดไฟล์** ก่อนโหลดเข้าสู่ memory  
- **ทำความสะอาดชื่อไฟล์** หากต้องบันทึกลงดิสก์  
- **จำกัดอัตราการเรียก** endpoint เพื่อป้องกันการโจมตีแบบ denial‑of‑service

### 4. การเร่งความเร็วด้วย GPU

หากคุณยกคอมเมนต์บรรทัด `engine.GpuDevice = new GpuDevice(0);` และฮาร์ดแวร์รองรับ CUDA หรือ DirectML คุณจะเห็นความเร็วเพิ่มขึ้นอย่างชัดเจน โดยเฉพาะกับภาพความละเอียดสูง

## ตัวอย่างทำงานเต็มรูปแบบ

ด้านล่างเป็นไฟล์ `Program.cs` เต็มรูปแบบที่คุณสามารถคัดลอก‑วางลงในโปรเจกต์ Minimal API ใหม่

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

บันทึก, รัน `dotnet run`, แล้วคุณพร้อม **extract text from image** ตามต้องการ

## สรุป

เราได้เดินผ่าน **โซลูชันครบวงจร** สำหรับการดึงข้อความจากภาพด้วย ASP.NET Core Minimal API ตั้งแต่การสร้างโครงงาน, **ลงทะเบียน singleton OCR engine**, สร้าง endpoint ที่ **uploads image via POST**, **read multipart form data**, และสุดท้าย **perform OCR on image** เพื่อคืนผลเป็น plain‑text

ต่อจากนี้คุณสามารถ:

- เพิ่ม wrapper แบบ JSON เพื่อให้ผลลัพธ์มีรายละเอียดมากขึ้น  
- เชื่อมต่อฐานข้อมูลเพื่อเก็บข้อความที่ดึงได้  
- รองรับหลายภาษา (`OcrLanguage.Spanish` เป็นต้น)  

แพทเทิร์นนี้ขยายได้ง่าย – เพียงแค่ใส่ endpoint เดียวกันลงในไมโครเซอร์วิสที่ใหญ่ขึ้นหรือเปิดให้ผ่าน API gateway

มีคำถามเกี่ยวกับการจัดการ PDF, การประมวลผลเป็นชุด, หรือการปรับ GPU? แสดงความคิดเห็นได้เลย, Happy coding!

## บทเรียนที่เกี่ยวข้อง

- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}