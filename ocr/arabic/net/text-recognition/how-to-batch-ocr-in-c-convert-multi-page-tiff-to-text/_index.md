---
category: general
date: 2026-03-28
description: تعلم كيفية تنفيذ OCR دفعيًا في C# وتحويل ملفات TIFF إلى نص بسهولة. يوضح
  هذا الدليل خطوة بخطوة استخراج النص من ملفات TIFF باستخدام Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: ar
og_description: كيف تقوم بعملية OCR دفعةً في C#؟ اتبع هذا الدرس الكامل لتحويل ملفات
  TIFF متعددة الصفحات إلى نص قابل للبحث باستخدام Aspose OCR.
og_title: كيفية تنفيذ التعرف الضوئي على الحروف دفعةً في C# – تحويل ملف TIFF متعدد
  الصفحات إلى نص
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR دفعيًا في C# – تحويل ملف TIFF متعدد الصفحات إلى نص
url: /ar/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعةً في C# – تحويل ملفات TIFF متعددة الصفحات إلى نص

هل تساءلت يومًا **كيف تقوم بعملية OCR دفعةً** لمجموعة من الصفحات الممسوحة ضوئيًا دون كتابة حلقة لكل صورة؟ لست الوحيد. في العديد من المشاريع—مثل معالجة الفواتير أو الرقمنة الأرشيفية—تظهر الحاجة إلى **تحويل TIFF إلى نص** يوميًا، وتصبح عملية القيام بذلك صفحةً بصفحة كابوسًا سريعًا.

الخبر السار؟ ببضع أسطر من C# وAspose OCR يمكنك تمرير ملف TIFF متعدد الصفحات بالكامل إلى المحرك والحصول على قاموس يربط أرقام الصفحات بالنص المستخرج. في هذا الدرس سنستعرض مثالًا كاملًا قابلًا للتنفيذ يوضح بالضبط **كيف تقوم بعملية OCR دفعةً**، وكيف **استخراج النص من TIFF**، ولماذا هذا النهج يتفوق على الطريقة اليدوية.

## ما ستتعلمه

- إعداد مكتبة Aspose OCR في مشروع .NET.  
- تحميل ملف TIFF متعدد الصفحات باستخدام `Image.FromMultiPageFile`.  
- تشغيل `RecognizeBatch` للحصول على `Dictionary<int,string>` للنتائج حسب الصفحات.  
- طباعة المخرجات بتنسيق نظيف وقابل للقراءة.  

بنهاية هذا الدرس ستحصل على تطبيق console جاهز للتنفيذ يحول أي ملف TIFF متعدد الصفحات إلى نص عادي—بدون الحاجة لأدوات إضافية.  

### المتطلبات المسبقة

- .NET 6.0 SDK (أو أي نسخة حديثة من .NET).  
- Visual Studio 2022 أو VS Code—أي بيئة تطوير تفضّلها.  
- رخصة Aspose OCR صالحة أو مفتاح تقييم مجاني (تعمل الواجهة البرمجية بدون رخصة لكنها تضيف علامة مائية).  
- ملف TIFF متعدد الصفحات تجريبي اسمه `multipage.tif` موجود في مجلد يمكنك الإشارة إليه.

> **نصيحة احترافية:** إذا كنت تعمل على Windows، فإن مجلد المشروع الافتراضي مكان مناسب لإسقاط ملف TIFF؛ وعلى Linux/macOS قم بتعديل المسار وفقًا لذلك.

## الخطوة 1: تثبيت حزمة NuGet الخاصة بـ Aspose OCR

قبل أن نكتب أي كود، نحتاج إلى مكتبة OCR. افتح الطرفية في مجلد مشروعك وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

هذا سيجلب أحدث نسخة مستقرة (اعتبارًا من مارس 2026 الإصدار 23.9) ويضيف ملفات DLL اللازمة إلى مشروعك. لا تحتاج إلى أي إعدادات إضافية لتطبيق console بسيط.

## الخطوة 2: إنشاء هيكل تطبيق Console

لننشئ برنامجًا بسيطًا يستدعي محرك OCR. توجيهات `using` ضرورية—بدونها سيشتكي المترجم من عدم وجود الأنواع.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **لماذا هذا مهم:** فئة `Image` موجودة في مساحة أسماء فرعية، ونسيان استيراد `ImageProcessing` سيؤدي إلى خطأ “type or namespace not found” قد يضيع عليك ساعة من التصحيح.

الآن أضف طريقة `Main` وتعليقًا مختصرًا يوضح الهدف:

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## الخطوة 3: تهيئة محرك OCR

`OcrEngine` هو العنصر الأساسي. إنشاء نسخة واحدة وإعادة استخدامها لجميع الصفحات يوفر الذاكرة ويزيد السرعة.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **ما الذي يحدث خلف الكواليس؟** المحرك يحمل نماذج اللغة ويضبط الإعدادات الافتراضية مسبقًا (مثل الإنجليزية، والتدوير التلقائي). يمكنك تعديل هذه الإعدادات لاحقًا، لكن الإعدادات الافتراضية مناسبة لمعظم المستندات.

## الخطوة 4: تحميل ملف TIFF متعدد الصفحات

تسهل Aspose عملية تحميل الصور متعددة الإطارات. قدم المسار الكامل أو مسارًا نسبيًا من دليل عمل الملف التنفيذي.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

إذا لم يُعثر على الملف، فإن `FromMultiPageFile` يرمي استثناء `FileNotFoundException`. يمكنك وضعه داخل `try/catch` إذا أردت معالجة الأخطاء برفق—وسترى مثالًا على ذلك في الخطوة التالية.

## الخطوة 5: تنفيذ OCR دفعةً

الآن يأتي نجم العرض: `RecognizeBatch`. تُعيد هذه الدالة `Dictionary<int,string>` حيث المفتاح هو فهرس الصفحة (يبدأ من 0) والقيمة هي النص المستخرج.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **حالة حافة:** بعض ملفات TIFF تحتوي على صفحات فارغة. تُعيد Aspose سلسلة فارغة لتلك الصفحات، ويمكنك تصفيتها لاحقًا إذا لا تريد الفوضى في المخرجات.

## الخطوة 6: عرض النتائج

أخيرًا، قم بالتكرار على القاموس واطبع نص كل صفحة. استخدام السلاسل المتداخلة (interpolated strings) يبقي الكود منظمًا.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

تشغيل البرنامج يجب أن ينتج شيئًا مشابهًا لـ:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

إذا ظهرت لك مخرجات مشوشة، تحقق مرة أخرى من أن ملف TIFF المصدر غير تالف وأن لغة النص تتطابق مع اللغة الافتراضية للمحرك (الإنجليزية). يمكنك أيضًا تعيين `ocrEngine.Language = OcrLanguage.Spanish;` للمستندات غير الإنجليزية.

## مثال كامل يعمل

بتجميع كل الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs` وتشغيله:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

احفظ، ثم ابنِ المشروع وشغّله:

```bash
dotnet run
```

سترى محتوى كل صفحة مستخرجًا يُطبع على وحدة التحكم. هذا هو **دليل OCR في C#** الكامل الذي طلبته.

## الأسئلة المتكررة وحالات الحافة

### ماذا لو كان ملف TIFF يحتوي على عشرات الصفحات؟

`RecognizeBatch` يعالج جميع الإطارات في استدعاء واحد، لكن استهلاك الذاكرة يزداد خطيًا مع عدد الصفحات. للمستندات الكبيرة جدًا (مئات الصفحات) فكر في المعالجة على دفعات:

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### هل يمكنني حفظ النص المستخرج إلى ملفات بدلاً من طباعته؟

بالطبع. استبدل كتلة `Console.WriteLine` بعمليات إدخال/إخراج ملفات:

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

بهذا ستحصل كل صفحة على ملف `.txt` خاص بها—مثالي للفهرسة اللاحقة.

### كيف أغيّر لغة الإخراج أو أفعّل التدوير التلقائي؟

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

يجب تطبيق هذه الإعدادات **قبل** استدعاء `RecognizeBatch`.

## الخاتمة

لقد غطينا **كيفية تنفيذ OCR دفعةً** لملف TIFF متعدد الصفحات باستخدام Aspose OCR في C#. بتحميل الصورة مرة واحدة، واستدعاء `RecognizeBatch`، والتكرار على القاموس الناتج، يمكنك **تحويل TIFF إلى نص** في ثوانٍ معدودة. يوضح المثال أيضًا **كيفية استخراج النص من TIFF**، ومعالجة الأخطاء، وإمكانية كتابة النتائج إلى ملفات—كل ذلك داخل تطبيق console نظيف ومستقل.

هل أنت مستعد للخطوة التالية؟ جرّب دمج هذا النهج مع مكتبة إنشاء PDF لإنتاج ملفات PDF قابلة للبحث، أو اربط المخرجات بقاعدة بيانات لأرشفة قابلة للبحث. يمكنك أيضًا تجربة صيغ صور أخرى (PNG، JPEG) عن طريق استبدال `Image.FromMultiPageFile` بـ `Image.FromFile`.

هل لديك أسئلة إضافية حول OCR أو الترخيص أو تحسين الأداء؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}