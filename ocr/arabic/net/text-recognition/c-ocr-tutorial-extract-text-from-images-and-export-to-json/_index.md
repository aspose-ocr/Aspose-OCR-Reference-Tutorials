---
category: general
date: 2026-01-01
description: دليل C# OCR يوضح كيفية استخراج النص، تحميل الصورة للتعرف الضوئي على الأحرف،
  وكتابة JSON إلى ملف باستخدام Aspose.OCR – دليل خطوة بخطوة.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: ar
og_description: دروس C# OCR التي تُرشدك إلى كيفية استخراج النص من الصور، تحميل الصورة
  للتعرف الضوئي على الأحرف، وكتابة JSON إلى ملف باستخدام Aspose.OCR.
og_title: دليل OCR بلغة C# – استخراج النص وتصديره إلى JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: دليل c# OCR – استخراج النص من الصور وتصديره إلى JSON
url: /ar/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دروس c# OCR – استخراج النص من الصور وتصديره إلى JSON

هل تساءلت يومًا كيف تستخرج النص من فاتورة ممسوحة ضوئيًا دون قضاء ساعات في كتابة محللات مخصصة؟ أنت لست وحدك. في هذا **c# OCR tutorial** سنوضح لك بالضبط كيفية تحميل صورة لـ OCR، تشغيل محرك التعرف، ثم **write JSON to file** حتى تتمكن من تغذية البيانات إلى الأنظمة اللاحقة.

تخيل أن لديك مجلدًا من الإيصالات، كل ملف اسمه `receipt1.png`، `receipt2.png`، وتحتاج إلى طريقة سريعة لتحويلها إلى سجلات JSON قابلة للبحث. هذه هي المشكلة التي سنحلها، وفي النهاية ستحصل على تطبيق console جاهز للتشغيل يقوم بذلك. لا توجد تبعيات إضافية بخلاف Aspose.OCR، ولا سحر—فقط خطوات واضحة وقابلة للتكرار.

> **ما ستتعلمه**
> - كيفية **load image for OCR** باستخدام Aspose.OCR.
> - أفضل طريقة لـ **how to extract text** والحصول على درجات الثقة.
> - تحويل نتيجة OCR إلى حمولة **OCR image to JSON** منظمة بشكل جيد.
> - بأمان **write JSON to file** والتحقق من المخرجات.

## المتطلبات المسبقة

- .NET 6 SDK أو أحدث (الكود يعمل على .NET Core أيضًا).  
- Visual Studio 2022 أو أي محرر تفضله.  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`).  
- ملف صورة (PNG, JPG, BMP) ترغب في معالجته – للعرض سنستخدم `invoice.png`.

إذا كنت تفتقد أيًا من هذه، احصل على SDK من موقع Microsoft وأضف حزمة NuGet عبر Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

الآن بعد أن تم إعداد الأساس، دعنا نغوص في التنفيذ الفعلي.

## الخطوة 1: c# OCR tutorial – تهيئة محرك OCR

قبل أن نتمكن من **load image for OCR**، نحتاج إلى نسخة من المحرك الذي سيقود عملية التعرف. فئة `OcrEngine` خفيفة الوزن، ولكن من الممارسات الجيدة تغليفها داخل كتلة `using` حتى يتم تحرير الموارد بسرعة.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*نصيحة احترافية:* إذا كنت تخطط لمعالجة العديد من الصور دفعة واحدة، أعد استخدام نفس نسخة `OcrEngine` بدلاً من إنشاء نسخة جديدة في كل مرة. هذا يقلل من استهلاك الذاكرة ويسرّع العملية.

## الخطوة 2: تحميل صورة لـ OCR

الآن نقوم فعليًا بـ **load image for OCR**. يدعم Aspose.OCR مجموعة متنوعة من الصيغ، لذا يمكنك توجيهه إلى PNG أو JPEG أو حتى TIFF متعدد الصفحات. طريقة `OcrImage.FromFile` تقرأ الملف وتجهزه للتعرف.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **لماذا هذا مهم:** تحميل الصورة بشكل منفصل يتيح لك فحص أبعادها، DPI، أو حتى معالجتها مسبقًا (مثل التحويل إلى ثنائي) قبل إرسالها إلى المحرك. إذا كانت الصورة تالفة، فإن `FromFile` سيطرح استثناء واضح يمكنك التقاطه وتسجيله.

## الخطوة 3: كيفية استخراج النص – تشغيل عملية التعرف

مع الصورة في المتناول، يمكننا أخيرًا **how to extract text** منها. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي ليس فقط على النص العادي بل أيضًا على بيانات الموقع ودرجات الثقة لكل كلمة.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*حالة حدية:* بعض ملفات PDF تحتوي على طبقات نصية غير مرئية. إذا قمت بتمرير صفحة PDF مُحولة إلى صورة، قد لا يرى المحرك شيئًا. في هذه الحالات، فكر في استخدام Aspose.PDF لاستخراج الطبقة المخفية أولاً، ثم اللجوء إلى OCR فقط عند الحاجة.

## الخطوة 4: OCR image to JSON – تحويل النتيجة

توفر فئة `OcrResult` مساعدًا مريحًا `ToJson()` الذي يُسلسل مجموعة النتائج بالكامل—بما في ذلك صندوق حدود كل كلمة ودرجة الثقة—إلى سلسلة JSON. هذه هي أنظف طريقة لتحقيق **OCR image to JSON** دون كتابة محول خاص بك.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

إذا كنت تفضل مخططًا مخصصًا، يمكنك التكرار على `ocrResult.Words` وبناء كائنك الخاص، لكن في معظم السيناريوهات يكون JSON المدمج كافيًا ومُنظمًا جيدًا بالفعل.

## الخطوة 5: كتابة JSON إلى ملف

الآن يأتي الجزء الأخير من اللغز: حفظ حمولة JSON. تضمن طريقة `File.WriteAllText` إنشاء الملف (أو استبداله) بشكل ذري. تأكد من وجود الدليل الهدف، وإلا ستواجه `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*نصيحة:* إذا كنت تحتاج إلى UTF‑8 مع BOM أو ترميز مختلف، استخدم النسخة التي تقبل معامل `Encoding`.

## الخطوة 6: التحقق من المخرجات

يعطينا `Console.WriteLine` سريعًا إشارة إلى أن العملية انتهت بنجاح. يمكنك أيضًا فتح ملف JSON في عارض لتأكيد البنية.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### مقتطف JSON المتوقع

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

يتضمن JSON موقع كل كلمة، وهو مفيد إذا رغبت لاحقًا في تمييز النص في واجهة المستخدم.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للنسخ واللصق. استبدل `YOUR_DIRECTORY` بالمسار الفعلي حيث توجد صورتك.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

شغّل البرنامج (`dotnet run` من مجلد المشروع) وستجد `invoice.json` بجانب ملف PNG الأصلي.

## المشكلات الشائعة وكيفية تجنبها

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **FileNotFoundException** عند تحميل الصورة | خطأ في مسار أو ملف مفقود | استخدم `Path.Combine` وتحقق من وجود `File.Exists` قبل استدعاء `FromFile`. |
| **درجات الثقة المنخفضة** | جودة صورة سيئة، DPI منخفض | قم بالمعالجة المسبقة باستخدام `ocrImage.AdjustContrast` أو قم بزيادة حجم الصورة إلى 300 DPI. |
| **ملف JSON فارغ** | `ocrResult` أعاد null (فشل المحرك) | تحقق من أن صيغة الصورة مدعومة وأن الترخيص (إن وجد) تم تطبيقه بشكل صحيح. |
| **عنق زجاجة الأداء في الدفعات الكبيرة** | إعادة إنشاء `OcrEngine` في كل تكرار | أعد استخدام نسخة واحدة من `OcrEngine` عبر الدفعة، وقم بتحريرها فقط في النهاية. |

## الخطوات التالية

الآن بعد أن أتقنت **c# OCR tutorial**، قد ترغب في:

- **Batch process** مجلدًا كاملاً وتجمع ملفات JSON في قاعدة بيانات واحدة.
- **Integrate** الناتج مع Azure Cognitive Search للحصول على PDFs قابلة للبحث.
- **Add language support** عن طريق ضبط `ocrEngine.Language = OcrLanguage.Spanish` (أو أي لغة مدعومة).
- **Post‑process** الـ JSON لاستخراج الجداول أو أزواج المفتاح‑القيمة باستخدام التعابير النمطية.

كل من هذه الإضافات يبني على المفاهيم الأساسية التي غطيناها: تحميل الصور لـ OCR، استخراج النص، التحويل إلى JSON، وكتابة هذا الـ JSON إلى القرص.

---

### الخلاصة

في هذا **c# OCR tutorial** استعرضنا كل خطوة مطلوبة لـ **load image for OCR**، **how to extract text**، تحويل النتيجة إلى حمولة **OCR image to JSON**، وأخيرًا **write JSON to file**. مثال الكود الكامل جاهز للإدراج في أي مشروع .NET، وتوفر الشروحات السياق الذي تحتاجه لتكييف الحل مع سيناريوهات العالم الحقيقي.

جرّبه مع مجموعة الإيصالات أو الفواتير الخاصة بك—عدل معالجة الصورة، جرب لغات مختلفة، وشاهد مخرجات JSON تتزايد. إذا واجهت أي مشاكل، راجع جدول المشكلات أو اترك تعليقًا أدناه. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}