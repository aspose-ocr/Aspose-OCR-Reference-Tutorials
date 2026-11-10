---
category: general
date: 2026-06-28
description: التعرف على النص من الصورة في ASP.NET Core – تعلم كيفية رفع الصورة للتعرف
  الضوئي على الأحرف ومعالجة صورة OCR من الدفق بكفاءة.
draft: false
keywords:
- recognize text from image
- upload image for ocr
- ocr image from stream
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في ASP.NET Core. تحميل
  الصورة للـ OCR، معالجة صورة الـ OCR من تدفق البيانات، وإرجاع النص النظيف.
og_title: التعرف على النص من الصورة في ASP.NET Core – دليل كامل
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  headline: recognize text from image in ASP.NET Core – upload for OCR
  type: TechArticle
- description: recognize text from image in ASP.NET Core – learn how to upload image
    for OCR and process ocr image from stream efficiently.
  name: recognize text from image in ASP.NET Core – upload for OCR
  steps:
  - name: Why This Pattern Works
    text: '- **Single `OcrEngine` instance**: Instantiating the engine once avoids
      the overhead of loading language data on every request. - **Async everything**:
      By using `await` on `FromStreamAsync` and `RecognizeAsync`, the ASP.NET Core
      thread pool stays free to serve other callers. - **`IFormFile` binding*'
  - name: Edge Cases to Watch
    text: '- **Corrupt files**: If the uploaded file isn’t a valid image, `FromStreamAsync`
      throws an exception. Wrap the call in a try/catch if you need graceful error
      messages. - **Unsupported formats**: Aspose supports PNG, JPEG, BMP, TIFF, etc.
      If you need PDF input, you’ll have to convert it to an image f'
  - name: Why Not Use `Recognize` (Sync)?
    text: The synchronous version would block the ASP.NET Core thread pool until the
      CPU‑intensive OCR finishes. On a busy server that quickly becomes a bottleneck,
      leading to 504 timeouts. The async variant keeps the API snappy.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Aspose.OCR
title: التعرف على النص من الصورة في ASP.NET Core – رفع للـ OCR
url: /ar/net/ocr-optimization/recognize-text-from-image-in-asp-net-core-upload-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة في ASP.NET Core – دليل كامل

هل احتجت يومًا إلى **التعرف على النص من الصورة** داخل واجهة برمجة تطبيقات ويب ولم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من المشاريع—مثل ماسحات الفواتير، متتبعي الإيصالات، أو حتى ميزة “اقرأ‑ني” البسيطة—الحصول على نتائج OCR موثوقة هو مهارة لا غنى عنها.

في هذا الدليل سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يوضح لك كيفية **رفع صورة للـ OCR**، تحويل ذلك الرفع إلى **ocr image from stream**، وأخيرًا إرجاع النص المستخرج كـ JSON نظيف. لا أجزاء مفقودة، لا إشارات غامضة—فقط حل مستقل يمكنك إدراجه في أي مشروع ASP.NET Core اليوم.

## ما ستحصل عليه

- تحكم `OcrController` كامل الوظائف يقبل تحميلات نموذجية multipart.  
- شرح خطوة بخطوة لكل سطر، لتفهم *لماذا* نفعل ما نقوم به.  
- نصائح للتعامل مع الملفات الكبيرة، تجنب حظر الخيوط، والحفاظ على استجابة واجهة برمجة التطبيقات.  
- نظرة على كيفية توسيع الحل (عدة لغات، معالجة مسبقة للصور، إلخ).  

**المتطلبات المسبقة**: .NET 6 أو أحدث، Visual Studio 2022 (أو VS Code)، ورخصة Aspose.OCR (الإصدار التجريبي المجاني يكفي للاختبار). إذا كان لديك كل ذلك، لنبدأ.

![مخطط سير عمل التعرف على النص من الصورة](https://example.com/ocr-workflow.png "مخطط سير عمل التعرف على النص من الصورة")

## كيفية التعرف على النص من الصورة في ASP.NET Core

قلب الحل يكمن في متحكم واحد. أدناه **الكود الكامل القابل للتنفيذ**؛ كل الاستيرادات، كل توجيه `using`، وكل استدعاء غير متزامن مدرج لتتمكن من نسخه ولصقه مباشرةً في مشروع ASP.NET Core Web API جديد.

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

[ApiController]
[Route("api/ocr")]
public class OcrController : ControllerBase
{
    // Step 1: Create a reusable OCR engine instance
    // Reusing the same OcrEngine across requests saves memory and speeds up init.
    private readonly OcrEngine _ocrEngine = new OcrEngine();

    // Step 2: Define the endpoint that accepts a file upload
    [HttpPost("recognize")]
    public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
    {
        // Guard clause – make sure we actually got a file
        if (uploadedFile == null || uploadedFile.Length == 0)
            return BadRequest(new { error = "No file uploaded." });

        // Step 3: Open the uploaded file as a read‑only stream
        // This is the **ocr image from stream** part.
        await using var imageStream = uploadedFile.OpenReadStream();

        // Step 4: Load the image asynchronously for OCR processing
        // Aspose.OCR provides FromStreamAsync which off‑loads the I/O work.
        var ocrImage = await OcrImage.FromStreamAsync(imageStream);

        // Step 5: Run OCR recognition without blocking the request thread
        // RecognizeAsync runs the heavy lifting on a background thread.
        var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);

        // Step 6: Return the extracted text as a JSON response
        return Ok(new { text = ocrResult.Text });
    }
}
```

### لماذا يعمل هذا النمط

- **مثيل `OcrEngine` واحد**: إنشاء المحرك مرة واحدة يجنب عبء تحميل بيانات اللغة في كل طلب.  
- **كل شيء غير متزامن**: باستخدام `await` على `FromStreamAsync` و `RecognizeAsync` يبقى تجمع خيوط ASP.NET Core حرًا لخدمة طلبات أخرى.  
- **ربط `IFormFile`**: سمة `[FromForm]` تسمح للعميل بإرسال طلب POST من نوع multipart/form‑data—تمامًا ما تعرفه المتصفحات والأدوات مثل Postman.  

الآن بعد أن الكود أمامك، دعنا نفصل كل جزء منطقي.

## رفع صورة للـ OCR – معالجة طلب Multipart

عندما يرسل العميل ملفًا، يقوم ASP.NET Core بربطه إلى `IFormFile`. هذا الكائن يمنحنا مقبضًا آمنًا للبايتات الخام دون تحميل الملف بالكامل إلى الذاكرة مرة واحدة.

```csharp
[HttpPost("recognize")]
public async Task<IActionResult> Recognize([FromForm] IFormFile uploadedFile)
{
    if (uploadedFile == null || uploadedFile.Length == 0)
        return BadRequest(new { error = "No file uploaded." });

    // …
}
```

**نصيحة احترافية**: إذا كنت تتوقع صورًا ضخمة (فكرًا >10 ميغابايت)، فكر في إضافة فحص حجم هنا وإرجاع 413 Payload Too Large. هذا يحمي خادمك من تعطل الذاكرة غير المقصود.

## معالجة صورة OCR من الدفق بشكل غير متزامن

السطر `await OcrImage.FromStreamAsync(imageStream)` يقوم بالعمل الشاق لتحويل بايتات الصورة إلى صيغة يمكن لـ Aspose.OCR فهمها. وبما أنه غير متزامن، فإن عمليات الإدخال/الإخراج (القرص أو الشبكة) لن تحجب خيط الطلب.

```csharp
await using var imageStream = uploadedFile.OpenReadStream();
var ocrImage = await OcrImage.FromStreamAsync(imageStream);
```

### الحالات الحدية التي يجب مراقبتها

- **ملفات تالفة**: إذا كان الملف المرفوع ليس صورة صالحة، فإن `FromStreamAsync` يرمي استثناءً. غلف الاستدعاء بـ try/catch إذا كنت بحاجة إلى رسائل خطأ لطيفة.  
- **صيغ غير مدعومة**: تدعم Aspose PNG، JPEG، BMP، TIFF، إلخ. إذا كنت تحتاج إلى إدخال PDF، سيتعين عليك تحويله إلى صورة أولًا (Aspose.PDF يمكن أن يساعد).

## تشغيل محرك OCR دون حجب

`_ocrEngine.RecognizeAsync(ocrImage)` يشغل خوارزمية OCR على خيط خلفي. هذه هي اللحظة التي يحدث فيها فعليًا عملية **التعرف على النص من الصورة**.

```csharp
var ocrResult = await _ocrEngine.RecognizeAsync(ocrImage);
```

النتيجة `ocrResult` تحتوي على خاصية `Text` التي تحمل السلسلة المستخرجة الخام. يمكنك معالجة النص لاحقًا (إزالة المسافات الزائدة، تصحيح أخطاء OCR الشائعة، إلخ) قبل إرساله مرة أخرى.

### لماذا لا نستخدم `Recognize` (متزامن)؟

الإصدار المتزامن سيحجز تجمع خيوط ASP.NET Core حتى ينتهي OCR المستهلك للمعالج. على خادم مشغول يصبح ذلك عنق زجاجة سريعًا، مما يؤدي إلى مهلات 504. النسخة غير المتزامنة تحافظ على سرعة استجابة الـ API.

## إرجاع JSON نظيف – القطعة النهائية

```csharp
return Ok(new { text = ocrResult.Text });
```

يتلقى العملاء حمولة JSON مرتبة:

```json
{
  "text": "Sample extracted text from the uploaded image."
}
```

إذا احتجت إلى بيانات وصفية إضافية—مثل درجات الثقة، اكتشاف اللغة، أو إطارات الحدود—فقط وسّع الكائن المجهول أو عرّف DTO مناسب.

## اختبار نقطة النهاية

يمكنك التحقق من أن كل شيء يعمل باستخدام **cURL**، **Postman**، أو حتى نموذج HTML بسيط.

```bash
curl -X POST https://localhost:5001/api/ocr/recognize \
     -F "uploadedFile=@/path/to/your/image.png"
```

استجابة ناجحة تبدو هكذا:

```
{"text":"Hello World"}
```

إذا نسيت إرسال ملف، ستحصل على:

```
{"error":"No file uploaded."}
```

## التقدم أكثر – تحسينات شائعة

| التحسين | لماذا يساعد | تلميح سريع للكود |
|------------|--------------|-----------------|
| **اختيار اللغة** | دقة OCR تتحسن عندما تخبر المحرك أي لغة تتوقعها. | `_ocrEngine.Language = OcrLanguage.English;` |
| **معالجة مسبقة للصور** | تعديل السطوع/التباين يمكن أن ينقذ المسحات منخفضة الجودة. | `ocrImage = OcrImage.FromBitmap(ImageProcessor` |

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك الخاصة.

- [كيفية استخراج نص الصورة من الدفق باستخدام Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}