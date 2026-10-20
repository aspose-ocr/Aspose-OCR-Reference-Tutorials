---
category: general
date: 2026-05-25
description: تعلم كيفية استخراج النص من الصورة باستخدام واجهة برمجة تطبيقات ASP.NET Core
  بسيطة. حمّل الصورة عبر طلب POST، واقرأ بيانات النموذج المتعدد الأجزاء، ثم نفّذ تقنية
  OCR على الصورة.
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: ar
og_description: استخراج النص من الصورة باستخدام واجهة برمجة تطبيقات ASP.NET Core Minimal.
  يوضح هذا الدليل كيفية تحميل الصورة عبر POST، وقراءة بيانات النموذج المتعدد الأجزاء،
  وإجراء OCR على الصورة.
og_title: استخراج النص من الصورة في ASP.NET Core – خطوة بخطوة
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
title: استخراج النص من الصورة في ASP.NET Core Minimal API – دليل كامل
url: /ar/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في ASP.NET Core Minimal API – دليل كامل

هل تساءلت يومًا كيف **استخراج النص من الصورة** دون التعامل مع أطر عمل ضخمة؟ أنت لست وحدك. يحتاج العديد من المطورين إلى طريقة سريعة لتمكين المستخدمين من إلقاء صورة والحصول على الأحرف الخام، سواء كان ذلك لمسح الفواتير، أو تحويل الملاحظات المكتوبة يدويًا إلى نص، أو تعزيز فهرس بحث.

في هذا الدرس سننشئ API Minimal صغير باستخدام ASP.NET Core يقوم **برفع الصورة عبر POST**، ويحلل حمولة *multipart/form‑data*، ثم **يُجري OCR على الصورة** باستخدام كائن `OcrEngine` أحادي. في النهاية ستحصل على تطبيق جاهز للتشغيل يمكنك إدراجه في أي مشروع .NET 8 والبدء في استخراج النص من الصورة فورًا.

## ما ستبنيه

- تطبيق ويب بسيط يستمع على `/ocr`.
- نقطة نهاية تقبل ملف صورة يُرسل عبر طلب POST من نوع `multipart/form-data`.
- منطق يقرأ الملف المرفوع، يمرره إلى محرك OCR، ويعيد النتائج كنص عادي.
- مقتطف تسريع GPU اختياري (مُعَلَّق) لأولئك الذين لديهم بطاقة متوافقة.

**المتطلبات المسبقة**  
- .NET 8 SDK (أو أحدث).  
- إلمام أساسي بـ C# وسطر الأوامر.  
- مكتبة OCR تُوفر فئة `OcrEngine` (العينة تفترض حزمة NuGet افتراضية).

إذا كان لديك ذلك، لنبدأ.

## الخطوة 1: إعداد المشروع وإضافة حزمة OCR

First, create a new web project and pull in the OCR library.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **نصيحة احترافية:** حافظ على تحديث تبعياتك. غالبًا ما تجلب الإصدارات الأحدث تحسينات في الأداء، خاصةً في الاستدلال المدعوم بـ GPU.

## الخطوة 2: تسجيل محرك OCR أحادي (الخدمة الأساسية)

We want a single `OcrEngine` instance for the whole app—no need to spin up a new engine per request. Register it in the builder’s service container.

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

**لماذا أحادي؟**  
إنشاء محرك OCR قد يكون مكلفًا—فكر في تحميل أوزان الشبكة العصبية إلى الذاكرة. بإعادة استخدام نفس المثيل نوفر دورات CPU والذاكرة، مما يترجم إلى أوقات استجابة أسرع لكل طلب `/ocr`.

## الخطوة 3: بناء التطبيق

Now we materialize the `WebApplication` object.

```csharp
var app = builder.Build();
```

That line looks almost magical, but under the hood it wires up routing, middleware, and the DI container we just configured.

## الخطوة 4: تعريف نقطة النهاية POST – “رفع صورة عبر POST”

Here’s the heart of the tutorial: an endpoint that **upload image via POST**, reads the multipart payload, and hands the data to the OCR engine.

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

### تفصيل المنطق

| الخطوة | ما يحدث | لماذا يهم |
|------|--------------|----------------|
| **ReadFormAsync** | يقوم بتحليل طلب *multipart/form-data* الوارد. | بدون ذلك، لا يمكنك الوصول إلى الملفات المرفوعة. |
| **form.Files["image"]** | يسترجع الملف الذي اسم حقل النموذج الخاص به هو `image`. | يضمن عقدًا متوقعًا للمتصلين. |
| **Content‑type check** | يتحقق من أن الملف صورة (مثال: `image/png`). | يمنع محرك OCR من الفشل عند بيانات غير صورة. |
| **Image.FromStream** | يحول الدفق الخام إلى كائن `System.Drawing.Image`. | مكتبة OCR تتوقع كائن `Image`، وليس مصفوفة بايتات خام. |
| **ocr.Recognize(img)** | يستدعي محرك OCR **لتعرف النص من الصورة**. | هذه هي خطوة **إجراء OCR على الصورة** الأساسية. |
| **Results.Text** | يرسل استجابة النص العادي. | تنسيق بسيط وقابل للاستهلاك للخدمات اللاحقة. |

## الخطوة 5: تشغيل الـ API

Finally, start the web server.

```csharp
app.Run();
```

When you execute `dotnet run`, the API will listen on `http://localhost:5000` (or a port of your choosing). You can test it with `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**الناتج المتوقع:** سيطبع الكونسول الأحرف التي تم التعرف عليها، مثال:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

If the image is blurry or the language isn’t supported, the OCR engine will return an empty string or an error message—handle those cases in production code.

## الحالات الحدية وأفضل الممارسات

### 1. ملفات كبيرة

The default request body limit is 30 MB. For larger scans you might need to adjust:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. OCR غير متزامن

Some OCR libraries expose async methods (`RecognizeAsync`). If yours does, replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the lambda as `async`.

### 3. اعتبارات الأمان

- **تحقق من حجم الملف** قبل تحميله إلى الذاكرة.
- **نقّح اسم الملف** إذا قررت حفظه على القرص.
- **حدّ من معدل الطلبات** لتجنب هجمات حجب الخدمة.

### 4. تسريع GPU

If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially on high‑resolution images.

## مثال كامل يعمل

Below is the complete `Program.cs` you can copy‑paste into a fresh Minimal API project.

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

Save, run `dotnet run`, and you’re ready to **extract text from image** on demand.

## الخلاصة

We’ve walked through a **complete, end‑to‑end solution** for extracting text from image using ASP.NET Core Minimal API. Starting from project scaffolding, we **registered a singleton OCR engine**, built an endpoint that **uploads image via POST**, **read multipart form data**, and finally **perform OCR on image** to return clean plain‑text. 

From here you can:

- إضافة أغلفة JSON لاستجابات أغنى.  
- ربط قاعدة بيانات لتخزين النص المستخرج.  
- توسيع الدعم لعدة لغات (`OcrLanguage.Spanish`, إلخ).

النمط يتوسع بسهولة—فقط أضف نفس نقطة النهاية إلى خدمة مصغرة أكبر أو عرّضها عبر بوابة API.

هل لديك أسئلة حول معالجة ملفات PDF، أو المعالجة الدفعية، أو ضبط GPU؟ اترك تعليقًا، وبرمجة سعيدة!

## دروس ذات صلة

- [استخراج النص من الصورة باستخدام Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}