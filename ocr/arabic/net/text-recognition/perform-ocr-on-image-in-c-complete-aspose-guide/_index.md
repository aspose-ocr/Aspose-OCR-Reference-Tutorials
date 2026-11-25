---
category: general
date: 2026-06-28
description: إجراء التعرف الضوئي على الأحرف (OCR) على صورة باستخدام Aspose.OCR في
  C#. تعلم كيفية التعرف على النص من الصورة، استخراج النص من الفاتورة، تحميل الصورة
  للتعرف الضوئي على الأحرف وكتابة JSON إلى ملف.
draft: false
keywords:
- perform OCR on image
- recognize text from image
- write JSON to file
- extract text from invoice
- load image for OCR
language: ar
og_description: قم بتنفيذ التعرف الضوئي على الحروف (OCR) على الصورة باستخدام Aspose.OCR
  في C#. يوضح هذا الدليل كيفية التعرف على النص من الصورة، استخراج النص من الفاتورة
  وكتابة JSON إلى ملف.
og_title: إجراء OCR على صورة في C# – دليل Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  headline: Perform OCR on Image in C# – Complete Aspose Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn to recognize text
    from image, extract text from invoice, load image for OCR and write JSON to file.
  name: Perform OCR on Image in C# – Complete Aspose Guide
  steps:
  - name: What if the image contains multiple languages?
    text: 'Aspose.OCR automatically detects the language based on the character set.
      If you need to force a specific language (e.g., English for most invoices),
      set the `Language` property on the engine:'
  - name: How do I handle large PDFs with many pages?
    text: Convert each page to an image first (using a PDF‑to‑image library) and then
      loop through the images, applying the same **perform OCR on image** routine.
      Aggregate the JSON results into a single array if you want a consolidated output.
  - name: Can I stream the JSON instead of writing a whole file?
    text: 'Yes. If you’re building a web API, you can return `json` directly as the
      response body:'
  - name: What about performance?
    text: The OCR engine runs synchronously in the example above. For high‑throughput
      scenarios, wrap the recognition call in `Task.Run` or use the asynchronous versions
      (if available) to keep your UI responsive or to parallelize batch processing.
  type: HowTo
tags:
- Aspose.OCR
- C#
- JSON
- ImageProcessing
title: إجراء التعرف الضوئي على الأحرف (OCR) على صورة في C# – دليل Aspose الكامل
url: /ar/net/text-recognition/perform-ocr-on-image-in-c-complete-aspose-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء OCR على الصورة في C# – دليل Aspose الكامل

هل احتجت يومًا إلى **perform OCR on image** لكن لم تكن متأكدًا أي مكتبة .NET ستمنحك نتائج نظيفة ومهيكلة؟ لست وحدك—المطورون يسألون باستمرار كيف يمكنهم **recognize text from image**، خاصةً عند التعامل مع الفواتير أو الإيصالات. في هذا الدرس سنستعرض مثالًا عمليًا لا يقتصر فقط على **loads image for OCR**، بل يشمل أيضًا **extracts text from invoice** و **writes JSON to file** لمعالجة لاحقة.

بنهاية هذا الدليل ستحصل على تطبيق console جاهز للتنفيذ يقوم بـ:

* إنشاء مثيل (instance) من محرك Aspose OCR،
* تحميل صورة PNG (أو JPG)،
* التعرف على المحتوى النصي،
* تحويل النتيجة إلى JSON منسق (pretty‑printed)،
* حفظ هذا الـ JSON على القرص.

لا خدمات خارجية، لا سحر مخفي—فقط كود C# نقي يمكنك نسخه، لصقه، وتشغيله.

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

* .NET 6 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework على حد سواء).
* رخصة صالحة لـ Aspose.OCR أو مفتاح تقييم مؤقت (الإصدار التجريبي المجاني يكفي للاختبار).
* Visual Studio 2022، VS Code، أو أي بيئة تطوير تفضّلها.
* ملف صورة—مثلاً `invoice.png`—موجود في مسار يمكنك الإشارة إليه إما بمسار كامل أو نسبي.

> **نصيحة احترافية:** إذا كنت تتعامل مع فواتير ممسوحة ضوئيًا، فكر في معالجة ما قبل الـ OCR (تصحيح الميل، تعزيز التباين) قبل تمرير الصورة إلى المحرك. Aspose.OCR يتعامل مع الكثير من هذه الخطوات تلقائيًا، لكن صورة مصدر نظيفة دائمًا ما تعطي نتائج أفضل.

---

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

أولًا، أنشئ مشروع console جديد وأضف حزمة Aspose.OCR عبر NuGet.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **لماذا هذه الخطوة مهمة:** تجميع `Aspose.OCR` يوفر الفئة `OcrEngine` التي سنستخدمها لـ **perform OCR on image**. بدون الحزمة، لن يتعرف المترجم على أي من الأنواع المتعلقة بالـ OCR.

---

## الخطوة 2: تحميل الصورة للـ OCR

الآن سنكتب الكود الذي **load image for OCR**. طريقة `OcrImage.FromFile` تقبل مسارًا مطلقًا أو نسبيًا وتغلف الـ bitmap بصيغة يفهمها المحرك.

```csharp
using Aspose.OCR;
using System.IO;

// Replace with the actual path to your invoice image
string imagePath = @"YOUR_DIRECTORY\invoice.png";

// Step 2: Load the image
OcrImage image = OcrImage.FromFile(imagePath);
```

> **شرح:** بفصل المسار في متغيّر خاص به نحافظ على نظافة الكود ونسهّل إعادة استخدام نفس مرجع الصورة لاحقًا (مثلاً عند التسجيل أو التصحيح). إذا لم يُعثر على الملف، تُطلق `FromFile` استثناء `FileNotFoundException` يمكنك التقاطه لتظهر رسالة خطأ ودية.

---

## الخطوة 3: إجراء OCR على الصورة والتعرف على النص

مع الصورة في المتناول، ننشئ مثيلًا من `OcrEngine` ونطلب منه **recognize text from image**. هذه الخطوة هي جوهر الدرس—هنا يحدث السحر الحقيقي للـ OCR.

```csharp
// Step 3: Create OCR engine and recognize text
using var ocrEngine = new OcrEngine();   // IDisposable, so we use 'using'
OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **لماذا نستخدم `using var`:** كائن `OcrEngine` يحتفظ بموارد غير مُدارة (مكتبات أصلية). وضعه داخل كتلة `using` يضمن تحريرها بشكل صحيح، مما يمنع تسرب الذاكرة—وهذا مهم خاصةً في الخدمات طويلة التشغيل.

> **ما ستحصل عليه:** المتغيّر `ocrResult` يحتوي على النص الخام، درجات الثقة، ومعلومات التخطيط (السطور، الكلمات، الصناديق المحيطة). لمعظم خطوط معالجة الفواتير، خاصية `Text` تكفي، لكن البيانات الوصفية الإضافية قد تساعد في التحقق أو التصحيح البصري.

---

## الخطوة 4: تحويل النتيجة إلى JSON منسق

تسهل Aspose.OCR عملية **write JSON to file** لأن `OcrResult` توفر طريقة `ToJson`. بتمرير `indent: true` نحصل على مخرجات قابلة للقراءة البشرية، وهو مفيد عندما تحتاج لاحقًا إلى **extract text from invoice**.

```csharp
// Step 4: Serialize OCR result to JSON
string json = ocrResult.ToJson(indent: true);
```

> **مثال مقتطف من JSON** (مقتطع للت brevity):

```json
{
  "Text": "Invoice #12345\nDate: 2026-06-01\nTotal: $1,250.00",
  "Confidence": 0.97,
  "Regions": [...]
}
```

> **ملاحظة حول الحالات الحدية:** إذا فشل محرك OCR في اكتشاف أي نص، ستكون قيمة `ocrResult.Text` سلسلة فارغة، لكن الـ JSON سيظل يحتوي على بيانات وصفية مثل أبعاد الصورة. يمكنك التحقق من النتائج الفارغة قبل كتابة الملف.

---

## الخطوة 5: كتابة JSON إلى ملف

الآن نكتب **JSON to file**. استخدام `File.WriteAllText` يضمن كتابة السلسلة بالكامل إلى القرص في عملية ذرية واحدة.

```csharp
// Step 5: Save JSON output
string jsonPath = @"YOUR_DIRECTORY\invoice.json";
File.WriteAllText(jsonPath, json);
Console.WriteLine($"JSON saved to {jsonPath}");
```

> **نصائح للإنتاج:** ضع طابع زمنية في اسم الملف (`invoice_20260628_1500.json`) لتجنب الكتابة فوق النتائج السابقة. كذلك، احيط عملية الكتابة بكتلة try/catch للتعامل مع مشاكل الأذونات بشكل سلس.

---

## الخطوة 6: مثال كامل يعمل

نجمع كل القطع معًا في البرنامج الكامل الذي يمكنك تجميعه وتشغيله فورًا. استبدل `YOUR_DIRECTORY` بالمجلد الذي يحتوي على `invoice.png`.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        string imagePath = @"YOUR_DIRECTORY\invoice.png";
        OcrImage image = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR and recognize text from image
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 4: Convert the recognition result to pretty‑printed JSON
        string json = ocrResult.ToJson(indent: true);

        // Step 5: Write JSON to file
        string jsonPath = @"YOUR_DIRECTORY\invoice.json";
        File.WriteAllText(jsonPath, json);

        // Step 6: Inform the user
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

**المخرجات المتوقعة** عند تشغيل البرنامج:

```
JSON saved to C:\Invoices\invoice.json
```

افتح `invoice.json` وسترى تمثيلًا منسقًا للبيانات المستخرجة من OCR، جاهزًا للتحليل أو التخزين اللاحق.

---

## أسئلة شائعة وحالات حدية

### ماذا لو احتوت الصورة على عدة لغات؟

Aspose.OCR يكتشف اللغة تلقائيًا بناءً على مجموعة الأحرف. إذا احتجت إلى فرض لغة معينة (مثل الإنجليزية لمعظم الفواتير)، عيّن خاصية `Language` على المحرك:

```csharp
ocrEngine.Language = OcrLanguage.English;
```

### كيف أتعامل مع ملفات PDF كبيرة تحتوي على صفحات متعددة؟

حوّل كل صفحة إلى صورة أولًا (باستخدام مكتبة تحويل PDF إلى صورة) ثم كرّر العملية على الصور، مطبقًا نفس روتين **perform OCR on image**. اجمع نتائج الـ JSON في مصفوفة واحدة إذا رغبت في مخرجات موحدة.

### هل يمكنني تدفق الـ JSON بدلاً من كتابة ملف كامل؟

نعم. إذا كنت تبني واجهة ويب API، يمكنك إرجاع `json` مباشرةً كجسم الاستجابة:

```csharp
return Results.Json(ocrResult);
```

### ماذا عن الأداء؟

محرك OCR يعمل بشكل متزامن في المثال أعلاه. للسيناريوهات ذات الإنتاجية العالية، يمكنك وضع استدعاء التعرف داخل `Task.Run` أو استخدام الإصدارات غير المتزامنة (إن وجدت) للحفاظ على استجابة الواجهة أو لتوزيع المعالجة على دفعات متوازية.

---

## الخلاصة

استعرضنا حلًا مختصرًا وشاملًا يتيح لك **perform OCR on image**، **recognize text from image**، **extract text from invoice**، وأخيرًا **write JSON to file** باستخدام Aspose.OCR في C#. الكود بسيط عمدًا لتتمكن من تعديله ليتناسب مع سير عمل أكثر تعقيدًا—سواء بإضافة معالجة مسبقة للصور، أو إدخال الـ JSON إلى قاعدة بيانات، أو إتاحة النتيجة عبر نقطة نهاية REST.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال PNG بـ JPEG، أو جرب إعدادات OCR مختلفة (مثل `ocrEngine.Dpi`)، أو أدمج خطوة تحويل PDF إلى صورة للتعامل مع حزم الفواتير الكاملة. السماء هي الحد عندما تتقن الأساسيات.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة ودقيقة!

## ما الذي ينبغي أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات المستعرضة في هذا الدليل. كل مصدر يتضمن أمثلة شاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [كيفية استخدام Aspose OCR للحصول على نتيجة JSON في التعرف على الصور](/ocr/english/net/text-recognition/get-result-as-json/)
- [استخراج نص الصورة في C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من الصورة – التعرف على السطر باستخدام Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}