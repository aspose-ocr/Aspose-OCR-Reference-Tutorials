---
category: general
date: 2026-01-09
description: استخراج النص من ملفات TIFF باستخدام Aspose OCR في C#. تعلم كيفية الحصول
  على أول 50 حرفًا من كل نتيجة في هذا الدليل خطوة بخطوة.
draft: false
keywords:
- extract text from tiff
- get first 50 characters
- aspose ocr c# tutorial
language: ar
og_description: استخراج النص من ملف TIFF باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية الحصول على أول 50 حرفًا من كل نتيجة OCR، خطوة بخطوة.
og_title: استخراج النص من ملف TIFF باستخدام Aspose OCR – دليل C# الكامل
tags:
- Aspose OCR
- C#
- TIFF processing
title: استخراج النص من ملف TIFF باستخدام Aspose OCR C# – دليل كامل
url: /ar/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-c-full-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من TIFF – دليل Aspose OCR الكامل بلغة C#

هل احتجت يومًا إلى **استخراج النص من TIFF** من الصور لكن لم تكن متأكدًا من أي مكتبة تثق بها؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحاولون استخراج نص قابل للبحث من ملفات TIFF متعددة الصفحات، خاصةً عندما تكون الأداء مهمة.

في هذا **aspose ocr c# tutorial** سنستعرض مثالًا جاهزًا للتنفيذ لا يقتصر فقط على استخراج النص الكامل بل يوضح لك أيضًا كيفية **الحصول على أول 50 حرفًا** من كل صفحة للحصول على معاينات سريعة. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- .NET 6 (أو أي نسخة حديثة من .NET) – الكود يُترجم مع .NET Core و .NET Framework على حد سواء.  
- رخصة Aspose.OCR for .NET سارية (يمكنك البدء بتجربة مجانية).  
- مجلد يحتوي على ملف أو أكثر بامتداد `.tif` تريد معالجته.  
- Visual Studio أو VS Code أو أي بيئة تطوير تفضلها – المثال مكتوب بلغة C# بسيطة لذا اختيار المحرر غير مهم.

> **نصيحة احترافية:** إذا كنت تعمل على خادم CI، أضف حزمة Aspose.OCR NuGet (`Aspose.OCR`) إلى ملف المشروع؛ المكتبة مُدارة بالكامل ولا تعتمد على مكونات أصلية.

## الخطوة 1: تثبيت حزمة Aspose OCR NuGet

أولًا، لنُدخل محرك OCR إلى المشروع. افتح الطرفية في مجلد الحل الخاص بك وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

## الخطوة 2: تهيئة محرك OCR

الآن نقوم بإنشاء نسخة من `OcrEngine`. فكر فيها كـ “العقل” الذي سيقرأ كل صفحة من TIFF.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: tweak recognition settings if you know the language
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300; // higher DPI can improve accuracy
```

لماذا ننشئ المحرك مرة واحدة فقط؟ لأن `RecognizeImages` يمكنه قبول مجموعة من مسارات الملفات، مما يسمح للمحرك بإعادة استخدام الذاكرة الداخلية وتسريع معالجة الدفعات بشكل كبير.

## الخطوة 3: جمع جميع ملفات TIFF في استدعاء واحد

بدلاً من التجول في الدليل بنفسك، نترك .NET يتولى العملية الثقيلة. تُعيد طريقة `Directory.GetFiles` كائنًا من نوع `IEnumerable<string>` يمكننا تمريره مباشرةً إلى استدعاء OCR.

```csharp
            // Step 3: Collect all TIFF images from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }
```

> **ماذا لو كانت صوري JPEG أو PNG؟** فقط غيّر نمط البحث (`"*.jpg"` أو `"*.*"`). Aspose OCR يعمل مع جميع صيغ الرسوم النقطية الشائعة.

## الخطوة 4: تشغيل OCR على المجموعة الكاملة

هذه هي السطر السحري الذي يعالج كل ملف في طلب واحد. تُعيد الطريقة قاموسًا حيث المفتاح هو مسار الملف والقيمة هي كائن `OcrResult` يحتوي على النص المُعترف به.

```csharp
            // Step 4: Perform OCR on the entire collection in one call
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);
```

لماذا المعالجة على دفعات؟ لأنها تقلل من الحمل الناتج عن تحميل محرك OCR مرارًا، وعلى الأجهزة متعددة النوى يقوم Aspose بتوازي العمل داخليًا، مما يمنحك زيادة ملحوظة في السرعة.

## الخطوة 5: عرض معاينة – الحصول على أول 50 حرفًا

معظم سيناريوهات واجهة المستخدم تحتاج فقط إلى مقتطف، وليس المستند بالكامل. سنستخرج أول 50 حرفًا (أو أقل إذا كانت الصفحة قصيرة) ونطبعها بجانب اسم الملف.

```csharp
            // Step 5: Display each file name with a preview of the recognized text
            foreach (var entry in ocrResults) // entry.Key = file path, entry.Value = OcrResult
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;
                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));

                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

السطر `Math.Min(50, fullText.Length)` يضمن أننا لا نتجاوز حدود السلسلة – وهو تدبير صغير يمنع حدوث `ArgumentOutOfRangeException` عندما يكون نتيجة OCR أقصر من 50 حرفًا.

### النتيجة المتوقعة في وحدة التحكم

بافتراض أن لديك ملفي TIFF (`invoice1.tif` و `receipt2.tif`) قد تُظهر وحدة التحكم التالي:

```
invoice1.tif → Invoice Number: 2025-07-14 Date: 07/14/...
receipt2.tif → Store: QuickMart Total: $23.45 Date: ...
```

كل سطر ينتهي بثلاث نقاط (`...`) للدلالة على أن المعاينة هي مجرد بداية كتلة نصية أطول.

## الخطوة 6: التعامل مع الحالات الحدية والمشكلات الشائعة

### ملفات فارغة أو تالفة

إذا تعذر قراءة ملف، لا يزال `RecognizeImages` يُعيد إدخالًا مع خاصية `Text` فارغة. يمكنك تصفية هذه الإدخالات:

```csharp
if (string.IsNullOrWhiteSpace(fullText))
{
    Console.WriteLine($"{fileName} → (No recognizable text)");
    continue;
}
```

### دفعات كبيرة

معالجة آلاف ملفات TIFF قد تستهلك الكثير من الذاكرة. في هذه الحالات، استخدم النسخة التي تقبل `Stream` لكل صورة، أو عالج القائمة على دفعات أصغر:

```csharp
var batches = imageFiles.Chunk(100); // .NET 6+ extension
foreach (var batch in batches)
{
    var batchResults = ocrEngine.RecognizeImages(batch);
    // handle batchResults...
}
```

### دعم اللغة والخطوط

إذا كانت مستنداتك تحتوي على أحرف غير لاتينية، اضبط اللغة قبل استدعاء `RecognizeImages`:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.MultiLanguage
```

هذا التعديل الصغير يمكنه تحسين الدقة بشكل كبير.

## الخطوة 7: مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع وحدة تحكم جديد (`dotnet new console`) وتشغيله كما هو (فقط استبدل `YOUR_DIRECTORY/Batch` بالمسار الفعلي).

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: set language or DPI for better accuracy
            // ocrEngine.Language = Language.English;
            // ocrEngine.Dpi = 300;

            // Collect all TIFF files from the batch folder
            IEnumerable<string> imageFiles = Directory.GetFiles(@"YOUR_DIRECTORY/Batch", "*.tif");

            if (!imageFiles.Any())
            {
                Console.WriteLine("No TIFF files found in the specified folder.");
                return;
            }

            // Perform OCR on the entire collection
            var ocrResults = ocrEngine.RecognizeImages(imageFiles);

            // Show a preview – get first 50 characters of each result
            foreach (var entry in ocrResults)
            {
                string fileName = Path.GetFileName(entry.Key);
                string fullText = entry.Value.Text ?? string.Empty;

                if (string.IsNullOrWhiteSpace(fullText))
                {
                    Console.WriteLine($"{fileName} → (No recognizable text)");
                    continue;
                }

                string preview = fullText.Substring(0, Math.Min(50, fullText.Length));
                Console.WriteLine($"{fileName} → {preview}...");
            }
        }
    }
}
```

شغّل البرنامج باستخدام `dotnet run`. يجب أن ترى معاينة مختصرة لكل ملف TIFF، مما يؤكد أنك نجحت في **استخراج النص من TIFF** باستخدام Aspose OCR.

## الأسئلة المتكررة (FAQ)

**س: هل يعمل هذا مع ملفات TIFF متعددة الصفحات؟**  
ج: نعم. Aspose OCR يعامل كل صفحة كصورة منفصلة داخليًا، لذا فإن ملف TIFF متعدد الصفحات ينتج سلسلة موحدة واحدة لكل ملف. يمكنك تقسيمها لاحقًا إذا لزم الأمر.

**س: ما مدى دقة OCR مباشرةً بعد التثبيت؟**  
ج: بالنسبة للماسحات النظيفة وعالية الدقة (300 DPI أو أعلى) يمكنك توقع دقة >95 % للنص الإنجليزي. المعالجة المسبقة (إزالة الميل، التحويل إلى ثنائي) يمكن أن تزيد الدقة أكثر.

**س: هل يمكنني تصدير النتائج إلى ملف CSV؟**  
ج: بالتأكيد. استبدل `Console.WriteLine` بـ `StreamWriter` واكتب صفوفًا بصيغة `fileName,preview`. تذكر أن تهرب الفواصل في نص المعاينة.

## الخطوات التالية والمواضيع ذات الصلة

- **Persist OCR results** – خزن النص الكامل في قاعدة بيانات لأرشفة قابلة للبحث.  
- **Combine with PDF conversion** – استخدم Aspose.PDF لإدراج النص المستخرج مرة أخرى في ملفات PDF قابلة للبحث.  
- **Batch processing on Azure Functions** – قم بتوسيع معالجة OCR باستخدام Azure Functions دون الحاجة لإدارة الخوادم.  

جميع هذه الإضافات ترتبط بالفكرة الأساسية لـ **استخراج النص من TIFF** بكفاءة، مع الاستمرار في تمكينك من **الحصول على أول 50 حرفًا** للحصول على معاينات سريعة في واجهة المستخدم.

---

*برمجة سعيدة! إذا واجهت أي مشاكل، اترك تعليقًا أدناه – سأبذل قصارى جهدي لمساعدتك في تحسين خط أنابيب OCR.*

![Extract text from TIFF using Aspose OCR](https://example.com/images/extract-text-from-tiff.png "Extract text from TIFF using Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}