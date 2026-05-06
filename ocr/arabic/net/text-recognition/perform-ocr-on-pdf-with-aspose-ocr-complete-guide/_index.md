---
category: general
date: 2026-05-06
description: تعلم كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على ملفات PDF باستخدام
  Aspose OCR في C#. يوضح هذا الدرس أيضًا كيفية استخراج النص من PDF وتحميل PDF للتعرف
  الضوئي على الحروف.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF
- how to extract text from scanned PDF
- load PDF for OCR
language: ar
og_description: اكتشف كيفية تنفيذ OCR على ملفات PDF باستخدام Aspose OCR في C#. كود
  خطوة بخطوة، شروحات، ونصائح لاستخراج النص من PDF بكفاءة.
og_title: إجراء التعرف الضوئي على الأحرف (OCR) على ملفات PDF باستخدام Aspose OCR –
  دليل كامل
tags:
- Aspose OCR
- C#
- PDF processing
title: إجراء التعرف الضوئي على الأحرف في ملفات PDF باستخدام Aspose OCR – دليل شامل
url: /ar/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء التعرف الضوئي على الأحرف (OCR) على ملفات PDF باستخدام Aspose OCR – دليل شامل

هل احتجت يومًا إلى **perform OCR on PDF** لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك. في العديد من المشاريع الواقعية—مثل معالجة الفواتير تلقائيًا أو رقمنة التقارير المؤرشفة—يعد استخراج النص من ملف PDF ممسوح ضوئيًا أمرًا ضروريًا.  

في هذا الدليل سنستعرض حلًا عمليًا لا يقتصر فقط على **performs OCR on PDF** باستخدام مكتبة Aspose OCR، بل يوضح لك أيضًا كيفية **extract text from PDF**، **load PDF for OCR**، وحتى التعامل مع مستندات متعددة اللغات. في النهاية ستحصل على برنامج C# جاهز للتنفيذ يحول أي PDF ممسوح ضوئيًا إلى نص قابل للبحث والتحرير.

## ما ستتعلمه

- كيفية إعداد Aspose OCR في مشروع .NET.  
- الخطوات الدقيقة لـ **load PDF for OCR** وتغذيته إلى المحرك.  
- كيفية ربط لغات مختلفة بصفحات منفصلة—مفيد عندما يحتوي PDF على مزيج من الإنجليزية والفرنسية والألمانية.  
- طرق التحقق من النتيجة وإصلاح المشكلات الشائعة.  

> **Pro tip:** إذا كنت تتعامل مع ملفات PDF كبيرة، فكر في معالجة الصفحات بشكل متوازي لتقليل دقائق زمن التنفيذ. سنتطرق إلى ذلك لاحقًا.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).  
- ترخيص Aspose OCR صالح أو مفتاح تقييم مؤقت.  
- ملف PDF ممسوح ضوئيًا باسم `multilang.pdf` موجود في مجلد يمكنك الإشارة إليه من الكود.  

لا توجد حزم طرف ثالث أخرى مطلوبة.

---

## الخطوة 1 – تثبيت Aspose OCR وإنشاء المحرك

أولاً، أضف حزمة Aspose.OCR NuGet إلى مشروعك:

```bash
dotnet add package Aspose.OCR
```

بعد تثبيت الحزمة، يمكنك إنشاء مثيل لمحرك OCR. هذا الكائن هو قلب العملية؛ فهو يعرف كيفية قراءة الصور وملفات PDF وتحويلها إلى نص.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Create an OCR engine instance – this is where we’ll perform OCR on PDF
var ocrEngine = new OcrEngine();
```

> **Why this matters:** تهيئة المحرك مرة واحدة وإعادة استخدامه عبر الصفحات يقلل من استهلاك الذاكرة ويسرّع المعالجة.

## الخطوة 2 – تحميل مستند PDF للتعرف الضوئي على الأحرف (OCR)

يمكن للمحرك فتح ملفات PDF مباشرة، لكن عليك إخبارها بأي ملف يجب العمل عليه. هذه هي خطوة **load PDF for OCR** التي يتغافل عنها العديد من المطورين.

```csharp
// Load the multi‑language PDF document from disk
ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");
```

استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك. إذا كان الملف مدمجًا كموارد، يمكنك أيضًا تحميله من تدفق.

> **Edge case:** إذا كان PDF محميًا بكلمة مرور، استدعِ `ocrEngine.LoadPdf(path, password)` لتزويد كلمة مرور فك التشفير.

## الخطوة 3 – ربط اللغات بالصفحات (اختياري لكن قوي)

غالبًا ما يحتوي PDF الممسوح ضوئيًا على صفحات بلغات مختلفة. بشكل افتراضي، يفترض Aspose OCR اللغة الإنجليزية، مما يؤدي إلى نتائج ضعيفة على الصفحات الفرنسية أو الألمانية. سنبني قاموسًا بسيطًا يخبر المحرك أي لغة يستخدمها لكل صفحة.

```csharp
// Define a language map: page index → OcrLanguage enum
var languageMap = new Dictionary<int, OcrLanguage>
{
    { 0, OcrLanguage.English }, // Page 1
    { 1, OcrLanguage.French },  // Page 2
    { 2, OcrLanguage.German }   // Page 3
};

// Provide the mapping via a lambda expression
ocrEngine.PageLanguageProvider = pageIndex =>
    languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;
```

> **Why you’ll do this:** توفير اللغة الصحيحة يحسن الدقة بشكل كبير، خاصةً بالنسبة للأحرف ذات اللكنات وعلامات الترقيم الخاصة باللغة.

## الخطوة 4 – تشغيل OCR والتقاط النتيجة

الآن يبدأ الجزء الثقيل. استدعاء `Recognize()` يعالج *جميع* الصفحات وفقًا لخريطة اللغة التي حددناها.

```csharp
// Run OCR on every page and collect the result
var recognitionResult = ocrEngine.Recognize();
```

كائن `recognitionResult` يحتوي على خاصية `Text` التي تجمع النص المعترف به من كل صفحة.

## الخطوة 5 – إخراج النص المستخرج

أخيرًا، نكتب النص المدمج إلى وحدة التحكم—أو يمكنك كتابته إلى ملف، قاعدة بيانات، أو أي نظام لاحق.

```csharp
// Display the combined OCR output
Console.WriteLine(recognitionResult.Text);
```

إذا كنت تفضل ملفًا:

```csharp
System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
```

> **Verification tip:** افتح الملف الناتج `extracted_text.txt` وابحث عن كلمات معروفة من كل لغة. إذا ظهرت اللكنات الفرنسية مشوهة، تحقق مرة أخرى من خريطة اللغة.

## مثال كامل يعمل

بجمع جميع الأجزاء معًا، إليك برنامج كامل جاهز للتنفيذ. انسخه والصقه في مشروع وحدة تحكم جديد واضغط **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑language PDF document
        // Make sure the path points to your actual file
        ocrEngine.LoadPdf("YOUR_DIRECTORY/multilang.pdf");

        // Step 3: Define which language should be used for each page
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },
            { 1, OcrLanguage.French },
            { 2, OcrLanguage.German }
        };

        // Step 4: Provide the language mapping to the engine
        ocrEngine.PageLanguageProvider = pageIndex =>
            languageMap.TryGetValue(pageIndex, out var lang) ? lang : OcrLanguage.English;

        // Step 5: Run OCR on all pages
        var recognitionResult = ocrEngine.Recognize();

        // Step 6: Output the combined text from the document
        Console.WriteLine("=== OCR Output Start ===");
        Console.WriteLine(recognitionResult.Text);
        Console.WriteLine("=== OCR Output End ===");

        // Optional: Save to a file for later use
        System.IO.File.WriteAllText("extracted_text.txt", recognitionResult.Text);
        Console.WriteLine("Text saved to extracted_text.txt");
    }
}
```

**الناتج المتوقع** (مقتطع للاختصار):

```
=== OCR Output Start ===
Page 1 (English):
Invoice #12345
Date: 2024‑04‑30
...

Page 2 (French):
Facture #12345
Date : 30/04/2024
...

Page 3 (German):
Rechnung #12345
Datum: 30.04.2024
...
=== OCR Output End ===
Text saved to extracted_text.txt
```

---

## معالجة ملفات PDF الكبيرة وتحسين الأداء

إذا كان ملف PDF الخاص بك يحتوي على مئات الصفحات، فكر في هذه التعديلات:

1. **Chunked processing** – معالجة 50 صفحة في كل مرة، ثم كتابة النتائج الوسيطة إلى القرص.  
2. **Parallelism** – استخدام `Parallel.ForEach` مع مثيلات `OcrEngine` منفصلة (كل محرك آمن للخطوط بعد التهيئة).  
3. **Memory management** – استدعاء `ocrEngine.Dispose()` بعد كل جزء لتحرير الموارد الأصلية.

```csharp
Parallel.ForEach(pageIndices, pageIdx =>
{
    var localEngine = new OcrEngine();
    localEngine.LoadPdf("multilang.pdf", pageIdx, 1); // Load a single page
    // Apply language mapping as before …
    var result = localEngine.Recognize();
    // Append result.Text to a thread‑safe collection
    localEngine.Dispose();
});
```

---

## المشكلات الشائعة وكيفية إصلاحها

| العَرَض | السبب المحتمل | الحل |
|---------|--------------|-----|
| أحرف مشوهة في الصفحات الفرنسية | تعيين لغة خاطئة | تأكد من أن `PageLanguageProvider` يُعيد `OcrLanguage.French` لتلك الصفحات. |
| ملف إخراج فارغ | عدم تحميل PDF (مسار خاطئ) | تحقق من المسار وأن الملف غير مقفل من عملية أخرى. |
| استثناء نفاد الذاكرة في ملفات PDF الضخمة | تحميل المحرك للملف بالكامل مرة واحدة | استخدم نسخة تحميل صفحة واحدة من `LoadPdf` أو عالج الملف على أجزاء. |
| معالجة بطيئة (> 5 دقائق لـ 100 صفحة) | تنفيذ أحادي الخيط | فعّل المعالجة المتوازية كما هو موضح أعلاه. |

## الخطوات التالية – تجاوز OCR الأساسي

الآن بعد أن يمكنك **perform OCR on PDF** و **extract text from PDF**، قد ترغب في:

- **Searchable PDF creation** – استخدم Aspose.PDF لتضمين نص OCR مرة أخرى في ملف PDF الأصلي، مما يجعله قابلًا للبحث.  
- **Data extraction** – تطبيق تعبيرات نمطية لاستخراج أرقام الفواتير، التواريخ، أو الإجماليات من النص المستخرج.  
- **Integration with AI** – تمرير ناتج OCR إلى نموذج لغة (مثل Azure OpenAI) للتلخيص أو التصنيف.  

جميع هذه الإضافات لا تزال تعتمد على القدرة الأساسية على **load PDF for OCR**، لذا لديك الأساس بالفعل.

## الخلاصة

لقد غطينا كل ما تحتاجه **perform OCR on PDF** باستخدام Aspose OCR في C#. من تثبيت المكتبة، تحميل PDF، تعيين لغات لكل صفحة، تشغيل محرك التعرف، وأخيرًا **extract text from PDF** وحفظه، يقدم الدليل حلاً متكاملًا وجاهزًا للإنتاج.  

لا تتردد في تجربة المعالجة المتوازية، مجموعات لغات مختلفة، أو حتى دمج نص OCR مع مكتبات معالجة المستندات الأخرى. إذا واجهت مشكلة، راجع جدول استكشاف الأخطاء أعلاه أو اترك تعليقًا—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}