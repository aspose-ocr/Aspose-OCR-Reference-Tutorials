---
category: general
date: 2026-05-28
description: كيفية إجراء التعرف الضوئي على الأحرف (OCR) في ASP.NET Core — تعلم رفع
  الصورة، استخراج النص من الصورة، ومعالجة رفع الملفات بكفاءة.
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: ar
og_description: كيفية تنفيذ OCR في ASP.NET Core. تعلّم خطوة بخطوة كيفية تحميل صورة،
  استخراج النص من الصورة، ومعالجة رفع الملفات باستخدام Aspose OCR.
og_title: كيفية تنفيذ OCR في ASP.NET Core – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: كيفية تنفيذ OCR في ASP.NET Core – الدليل الكامل
url: /ar/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في ASP.NET Core – دليل كامل

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** داخل واجهة برمجة تطبيقات ويب حديثة دون أن تشعر بالإحباط؟ أنت لست الوحيد. يحتاج المطورون باستمرار إلى السماح للمستخدمين بتحميل صورة — ربما إيصال، أو مسح جواز سفر، أو ملاحظة مكتوبة بخط اليد — والحصول على النص الأصلي في صيغة JSON.  

في هذا الدرس سنستعرض حلًا كاملاً وجاهزًا للإنتاج يُظهر **كيفية تحميل الملف**، يتحقق من صحته، يشغّل Aspose OCR، وأخيرًا **استخراج النص من الصورة**. في النهاية ستحصل على وحدة تحكم جاهزة للنسخ يمكنك وضعها في أي مشروع ASP.NET Core.

## ما ستبنيه

- وحدة تحكم `OcrController` تقبل تحميلات multipart/form‑data
- التحقق من أن الملف موجود فعليًا وليس فارغًا
- معالجة OCR غير متزامنة باستخدام محرك Aspose OCR
- استجابة JSON نظيفة تحتوي على النص المُعترف به

## المتطلبات المسبقة (ما تحتاجه قبل البدء)

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6 SDK أو أحدث | ASP.NET Core 6+ يوفّر ميزات API الحد الأدنى ودعم async. |
| Visual Studio 2022 (أو VS Code) | بيئة التطوير تجعل تصحيح الأخطاء أسهل، لكن أي محرر يعمل. |
| حزمة Aspose.OCR NuGet (`dotnet add package Aspose.OCR`) | المحرك الذي يقوم فعليًا بعمل OCR. |
| معرفة أساسية بـ ASP.NET Core MVC | سنستخدم `ControllerBase` وسمات التوجيه. |

إذا كان لديك هذه المتطلبات، عظيم—لنبدأ.

## الخطوة 1: إعداد المشروع وتثبيت Aspose OCR

Open a terminal and create a fresh web API project:

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

هذا الأمر الواحد يجلب مكتبة OCR وجميع تبعياتها. لا شيء آخر يحتاج إلى إعداد؛ Aspose يعمل مباشرةً مع صيغ الصور الشائعة.

## الخطوة 2: إضافة وحدة تحكم OCR (نواة **كيفية تنفيذ OCR**)

أنشئ ملفًا جديدًا `Controllers/OcrController.cs` والصق الشيفرة التالية. إنها مثال كامل قابل للتنفيذ — لا توجد أجزاء مفقودة.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### لماذا يعمل هذا

- **`[FromForm] IFormFile`** يخبر ASP.NET Core بربط جزء الملف المتعدد الأجزاء إلى `uploadedFile`. هذه هي الطريقة الكلاسيكية **للتعامل مع تحميل الملف** في واجهة برمجة التطبيقات.
- شرط `if` يضمن أننا **نتعامل مع أخطاء تحميل الملف** بشكل سلس، مع إرجاع 400 Bad Request إذا نسي العميل إرسال ملف.
- `using var fileStream = uploadedFile.OpenReadStream();` يفتح تدفقًا *للقراءة فقط*، وهو ضروري للملفات الكبيرة—لا حاجة لتحميل الصورة بالكامل إلى الذاكرة مرة واحدة.
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` يمرّر التدفق مباشرةً إلى Aspose OCR، مما يحافظ على بساطة خط الأنابيب.
- `await ocrEngine.RecognizeAsync();` ينفّذ العملية الثقيلة على خيط خلفي، لذا تظل واجهتنا سريعة الاستجابة. هذا هو جوهر **كيفية تنفيذ OCR** بشكل غير متزامن.
- أخيرًا، نغلف النتيجة في كائن JSON (`{ extractedText }`)—مثالي للاستهلاك من قبل الواجهة الأمامية.

## الخطوة 3: ضبط حد حجم الطلب (اختياري لكن مفيد)

إذا كنت تتوقع مسحات عالية الدقة، قم بزيادة حجم الطلب الافتراضي. أضف هذا إلى `Program.cs`:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

الآن لن يتعطل الـ API عند صورة إيصال بحجم 10 ميغابايت. عدّل الحد وفقًا لحالتك.

## الخطوة 4: اختبار نقطة النهاية باستخدام cURL أو Postman

Here’s a quick cURL command you can run from the terminal:

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

ستظهر لك حمولة JSON مشابهة لـ:

```json
{
  "extractedText": "Sample text that was on the image."
}
```

إذا كانت الصورة لا تحتوي على أحرف يمكن التعرف عليها، ستكون السلسلة فارغة — لا يحدث عطل، فقط نتيجة فارغة. هذه حالة حافة جيدة لتذكرها.

## الخطوة 5: تأكيد بصري (صورة اختيارية)

فيما يلي لقطة شاشة توضيحية تُظهر استجابة JSON التي ستحصل عليها بعد طلب OCR ناجح.

![How to perform OCR result – screenshot of JSON response showing extracted text](/images/ocr-result.png)

*Alt text:* **لقطة شاشة لنتيجة تنفيذ OCR تُظهر النص المستخرج من الصورة**

## المشكلات الشائعة والنصائح الاحترافية

| المشكلة | الحل |
|---------|----------|
| **صيغة صورة غير مدعومة** (مثال: TIFF مع صفحات متعددة) | تحويل إلى PNG/JPEG أولاً أو استخدام `ImageConverter` الخاص بـ Aspose قبل تمريره إلى `OcrEngine`. |
| **الملفات الكبيرة تسبب ضغطًا على الذاكرة** | قم ببث الملف كما هو موضح؛ تجنّب `IFormFile.CopyToAsync` إلى `MemoryStream`. |
| **OCR يُعيد نصًا مشوشًا** | تأكد من أن الصورة ذات تباين عالي ومُوجهة بشكل صحيح. قم بالمعالجة المسبقة باستخدام `ocrEngine.Preprocess()` إذا لزم الأمر. |
| **طلبات متزامنة متعددة** | Aspose OCR آمن للثريدات، لكن قد ترغب في تحديد عدد الطلبات المتزامنة باستخدام semaphore إذا كان الخادم محدود الذاكرة. |

## توسيع المثال: تحميل جماعي ومعالجة متوازية

إذا كنت بحاجة إلى **التعامل مع تحميل الملف** لعدة صور في آن واحد، غيّر توقيع الإجراء ليقبل قائمة:

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

الآن يمكنك **تحميل OCR للصور** بشكل جماعي — مثالي لمسح مجلد من الإيصالات دفعة واحدة.

## اعتبارات الأمان

- **تحقق من امتدادات الملفات** (`.png`, `.jpg`, `.jpeg`) قبل المعالجة لتجنب التحميلات الضارة.
- **افحص للفيروسات** إذا كان الـ API متاحًا على الإنترنت؛ دمج مع خدمة مثل ClamAV.
- **حدّ من معدل الطلبات** (Rate‑limit) للنقطة لتجنب هجمات حجب الخدمة.

## المخرجات المتوقعة وكيفية التحقق

عند استدعاء نقطة النهاية `/ocr/upload` بصورة واضحة تحتوي على كلمة “Hello”، يجب أن تكون الاستجابة:

```json
{
  "extractedText": "Hello"
}
```

يمكنك التحقق بسرعة بفتح أدوات المطور في المتصفح → تبويب الشبكة، أو بفحص مخرجات cURL.

## ملخص – ما تم تغطيته

- إعداد مشروع ASP.NET Core وإضافة حزمة Aspose OCR NuGet.
- تنفيذ وحدة تحكم نظيفة تُظهر **كيفية تنفيذ OCR**، **التعامل مع تحميل الملف**، و**استخراج النص من الصورة**.
- مناقشة معالجة الأخطاء، تحسينات الأداء، وأفضل ممارسات الأمان.
- توفير عينة كود جاهزة للتنفيذ بالإضافة إلى نسخة التحميل الجماعي.

## ما التالي؟

- **إضافة دعم للغات**: يمكن تكوين Aspose OCR للغات مختلفة (`ocrEngine.Language = Language.English;`).
- **الدمج مع قاعدة بيانات**: احفظ النص المستخرج مع البيانات الوصفية للبحث لاحقًا.
- **واجهة أمامية**: بناء صفحة بسيطة بـ React أو Blazor تسمح للمستخدمين بسحب وإفلات الصور ورؤية نتيجة OCR فورًا.

لا تتردد في التجربة — استبدل محرك OCR، جرّب خطوات معالجة صورة مختلفة، أو اربط النتيجة بنموذج AI لاحق. السماء هي الحد عندما تعرف **كيفية تنفيذ OCR** في مجموعة .NET الحديثة.

برمجة سعيدة، ولتكن نصوصك دائمًا مقروءة!

## دروس ذات صلة

- [كيفية تنفيذ OCR على صورة – تنفيذ OCR على صورة في التعرف على الصور](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [كيفية استخدام Aspose للتعرف على صورة من تدفق في التعرف على الصور](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [كيفية ضبط قيمة العتبة في التعرف على الصور OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}