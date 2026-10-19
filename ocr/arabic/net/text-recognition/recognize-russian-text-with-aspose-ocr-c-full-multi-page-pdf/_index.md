---
category: general
date: 2026-01-01
description: التعرف على النص الروسي فورًا باستخدام Aspose OCR C#. تعلم كيفية التعرف
  على النص الصيني، قراءة عدد صفحات PDF، وتحويل نص صفحة PDF في درس واحد.
draft: false
keywords:
- recognize russian text
- aspose ocr c#
- recognize chinese text
- read pdf page count
- convert pdf page text
language: ar
og_description: التعرف على النص الروسي بسرعة باستخدام Aspose OCR C#. يغطي هذا الدرس
  أيضًا كيفية التعرف على النص الصيني، قراءة عدد صفحات PDF، وتحويل نص صفحة PDF.
og_title: التعرف على النص الروسي باستخدام Aspose OCR C# – دليل كامل
tags:
- Aspose OCR
- C#
- PDF processing
title: التعرف على النص الروسي باستخدام Aspose OCR C# – دليل كامل لملف PDF متعدد الصفحات
url: /ar/net/text-recognition/recognize-russian-text-with-aspose-ocr-c-full-multi-page-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص الروسي باستخدام Aspose OCR C# – دليل كامل لملف PDF متعدد الصفحات

هل احتجت يومًا إلى **التعرف على النص الروسي** في ملف PDF يجمع بين لغات متعددة، وتساءلت كيف تقوم بذلك دون الحاجة إلى أداة منفصلة لكل صفحة؟ لست وحدك. في العديد من المشاريع الواقعية ستحصل على ملف PDF واحد يحتوي على الإنجليزية، الروسية، وحتى الصينية في صفحات مختلفة، وتريد الحصول على ناتج نصي موحد ونظيف.

> **ما ستحصل عليه**  
> * تطبيق Console بلغة C# يمكن تشغيله لمعالجة ملف PDF متعدد الصفحات.  
> * اختيار اللغة لكل صفحة (الروسية، الصينية، الإنجليزية).  
> * تقنيات لاستعلام عدد صفحات PDF واستخراج نص كل صفحة.  
> * نصائح، ملاحظات، وإمكانيات توسيع يمكنك تطبيقها في مشاريعك.

---

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- حزمة NuGet **Aspose.OCR for .NET** مثبتة (`dotnet add package Aspose.OCR`).  
- ملف PDF يحتوي على لغات مختلطة؛ سنستخدم في المثال `mixed_lang.pdf`.  
- معرفة أساسية بتطبيقات Console في C#.

إذا كان أي من هذه غير متوفر، احصل على أحدث نسخة من Aspose OCR عبر NuGet وضع ملف PDF في مسار يمكن الوصول إليه من مجلد المشروع.

---

## الخطوة 1 – تهيئة محرك Aspose OCR

أول شيء تحتاجه هو نسخة من `OcrEngine`. هذا الكائن يحمل جميع الإعدادات (مثل اللغة) ويقوم بالمعالجة الفعلية.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class MultiPageDemo
{
    static void Main()
    {
        // Create the OCR engine – this is where we’ll set language per page
        OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:**  
> المحرك قابل لإعادة الاستخدام، لذا لا نهدر الذاكرة بإنشاء نسخة جديدة لكل صفحة. إعادة استخدامه تسمح لنا بتغيير اللغة أثناء التشغيل، وهو أمر أساسي لـ **التعرف على النص الروسي** في صفحة واحدة و**التعرف على النص الصيني** في أخرى.

---

## الخطوة 2 – تحميل ملف PDF ومعرفة عدد صفحاته

قبل أن نبدأ بالتعرف، نحتاج إلى كائن PDF وعدد صفحاته. Aspose OCR يعامل كل صفحة كـ `OcrImage`.

```csharp
        // Load the multi‑page PDF
        OcrImage multiPageImage = OcrImage.FromFile(@"YOUR_DIRECTORY/mixed_lang.pdf");

        // Print the total number of pages – this answers the “read pdf page count” question
        Console.WriteLine($"PDF contains {multiPageImage.PageCount} pages.");
```

> **نصيحة:** إذا كان ملف PDF كبيرًا، قد ترغب أولًا في قراءة العدد ثم تقرر ما إذا كنت ستعالج جميع الصفحات أو مجموعة فرعية فقط.

---

## الخطوة 3 – ربط كل صفحة بلغتها المطلوبة

Aspose OCR يدعم العديد من اللغات، لكن عليك إخبار المحرك أي لغة يستخدمها لكل صفحة. أدناه ننشئ `Dictionary<int, OcrLanguage>` حيث المفتاح هو فهرس الصفحة (بدءًا من الصفر).

```csharp
        // Define which language each page should be read with
        var languageMap = new Dictionary<int, OcrLanguage>
        {
            { 0, OcrLanguage.English },   // Page 1 – English
            { 1, OcrLanguage.Russian },   // Page 2 – Russian (our primary focus)
            { 2, OcrLanguage.Chinese }    // Page 3 – Chinese
        };
```

> **لماذا هذا حاسم:**  
> بدون هذا الخريطة، سيحاول محرك OCR استخدام لغة افتراضية واحدة لكل الصفحات، مما يؤدي إلى ناتج غير مفهوم للنص الروسي أو الصيني. هذه الخطوة تمكّن **التعرف على النص الروسي** و**التعرف على النص الصيني** بشكل صحيح.

---

## الخطوة 4 – التكرار عبر جميع الصفحات، ضبط اللغة، والتعرف على النص

نقوم الآن بالتكرار على كل صفحة، نغيّر اللغة بناءً على الخريطة، ثم نستدعي `Recognize`. النتيجة تُخزن في `OcrResult`، ومنه نستخرج النص الصافي.

```csharp
        // Process each page one by one
        for (int pageIndex = 0; pageIndex < multiPageImage.PageCount; pageIndex++)
        {
            // Choose language – default to English if we haven’t specified one
            ocrEngine.Settings.Language = languageMap.ContainsKey(pageIndex)
                                          ? languageMap[pageIndex]
                                          : OcrLanguage.English;

            // Perform OCR on the current page
            var pageResult = ocrEngine.Recognize(multiPageImage.GetPage(pageIndex));

            // Output the recognized text – this is the “convert pdf page text” step
            Console.WriteLine($"--- Page {pageIndex + 1} ({ocrEngine.Settings.Language}) ---");
            Console.WriteLine(pageResult.Text);
            Console.WriteLine(); // Blank line for readability
        }
    }
}
```

### ناتج Console المتوقع

```
PDF contains 3 pages.
--- Page 1 (English) ---
This is an English paragraph on the first page.

--- Page 2 (Russian) ---
Это русский текст на второй странице.

--- Page 3 (Chinese) ---
这是第三页的中文文本。
```

> **شرح سير العملية:**  
> * الحلقة تحترم **قراءة عدد صفحات PDF** التي طبعناها مسبقًا.  
> * بتغيير `ocrEngine.Settings.Language` في كل دورة، نضمن **التعرف على النص الروسي** في الصفحة 2 و**التعرف على النص الصيني** في الصفحة 3.  
> * عبارات `Console.WriteLine` تحول **نص صفحة PDF** إلى سلسلة قابلة للقراءة البشرية.

---

## الخطوة 5 – تشغيل، التحقق، وتعديل

1. بناء المشروع (`dotnet build`).  
2. تشغيله (`dotnet run`).  
3. مقارنة ناتج الـ Console مع ملف PDF الأصلي.  

إذا لاحظت فقدان أحرف، فكر في:

- **زيادة دقة OCR** عبر ضبط `ocrEngine.Settings.DetectTextOrientation = true;`.  
- **توفير حزمة لغة مخصصة** إذا كانت القواميس المدمجة للروسية أو الصينية قديمة.  
- **ضبط DPI** عند تحميل PDF (`OcrImage.FromFile(path, 300)`)، ما قد يحسن التعرف على المسحات منخفضة الدقة.

---

## إضافي: معالجة الحالات الخاصة

### ماذا لو لم تكن لغة الصفحة موجودة في الخريطة؟

الكود بالفعل يرجع إلى الإنجليزية كخيار افتراضي، لكن يمكنك إضافة سجل تحذير:

```csharp
if (!languageMap.TryGetValue(pageIndex, out var lang))
{
    Console.WriteLine($"Warning: No language defined for page {pageIndex + 1}. Using English.");
    lang = OcrLanguage.English;
}
ocrEngine.Settings.Language = lang;
```

### هل يمكننا معالجة ملفات PDF بأكثر من ثلاث لغات؟

بالتأكيد. قم بتمديد `languageMap` بإضافة فهارس وقيم `OcrLanguage` إضافية (مثل `OcrLanguage.French`). الحلقة ستتعامل مع أي عدد من الصفحات.

### كيف يمكن تصدير النتائج إلى ملف بدلاً من الـ Console؟

استبدل استدعاءات `Console.WriteLine` بـ `File.AppendAllText("output.txt", …)` أو استخدم `StringBuilder` لتكتب المحتوى مرة واحدة بعد انتهاء الحلقة.

---

## توضيح صورة

![مثال على التعرف على النص الروسي](/images/recognize-russian-text.png "لقطة شاشة تُظهر ناتج OCR للنص الروسي")

*الصورة أعلاه تُظهر ناتج الـ Console عند **التعرف على النص الروسي** في ملف PDF متعدد اللغات.*

---

## الخلاصة

استعرضنا مثالًا كاملاً من البداية إلى النهاية يوضح كيفية **التعرف على النص الروسي** (وكذلك **التعرف على النص الصيني**) من ملف PDF متعدد الصفحات باستخدام **Aspose OCR C#**. من خلال قراءة عدد صفحات PDF، ربط كل صفحة بلغتها المناسبة، والتكرار عبر المستند، يمكنك **تحويل نص صفحة PDF** إلى سلاسل نصية جاهزة للتخزين أو الفهرسة أو التحليل الإضافي.

باختصار:

- **تهيئة** محرك `OcrEngine` واحد.  
- **تحميل** ملف PDF و**قراءة عدد صفحات PDF**.  
- **ربط** الصفحات باللغات (الروسية، الصينية، إلخ).  
- **التكرار**، ضبط `ocrEngine.Settings.Language`، و**التعرف** على كل صفحة.  
- **إخراج** أو حفظ النص المستخرج.

لا تتردد في تعديل هذا النمط للوثائق الأكبر، إضافة معالجة الأخطاء، أو ربط النتائج بمحرك بحث. الفكرة الأساسية—اختيار اللغة لكل صفحة—تظل هي المفتاح لجعل **التعرف على النص الروسي** موثوقًا في ملفات PDF مختلطة اللغات.

هل لديك سيناريو مختلف، مثل مسح صور بدلاً من ملفات PDF؟ نفس المحرك يعمل؛ فقط استبدل `OcrImage.FromFile` بـ `OcrImage.FromStream` أو `FromBitmap`. نتمنى لك برمجة سعيدة، ولتكن OCR دائمًا دقيقة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}