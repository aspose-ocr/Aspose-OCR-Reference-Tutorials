---
category: general
date: 2026-01-09
description: دليل C# OCR يوضح كيفية التعرف على النص من الصورة ومعالجة الصورة مسبقًا
  لـ OCR باستخدام فلاتر Aspose.OCR – دليل خطوة بخطوة.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- preprocess image for ocr
- Aspose OCR
- image preprocessing C#
language: ar
og_description: دليل C# OCR يشرح لك كيفية التعرف على النص من الصورة ومعالجة الصورة
  مسبقًا للتعرف الضوئي على الأحرف باستخدام فلاتر Aspose.OCR. يتضمن الكود الكامل.
og_title: دليل c# OCR – التعرف على النص من الصورة مع المعالجة المسبقة
tags:
- OCR
- C#
- Image Processing
title: 'دليل c# OCR: التعرف على النص من الصورة مع المعالجة المسبقة'
url: /ar/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# OCR – التعرف على النص من الصورة مع المعالجة المسبقة

هل تساءلت يومًا كيف **تتعرف على النص من الصورة** في تطبيق C# دون قضاء أسابيع في تعديل الفلاتر؟ لست وحدك. في هذا **دليل c# OCR** سنستعرض مثالًا كاملًا جاهزًا للتنفيذ لا يقرأ النص فقط بل **يعالج الصورة مسبقًا للـ OCR** لزيادة الدقة.

سنستخدم مكتبة Aspose.OCR لأنها تأتي مع خط أنابيب فلاتر مريح يتيح لك إضافة خطوات تصحيح الميل، إزالة الضوضاء، وتعزيز التباين ببضع أسطر فقط. بنهاية هذا الدليل ستحصل على تطبيق كونسول يمكنه أخذ صورة PNG مائلة ومليئة بالضوضاء، تنظيفها، وإخراج النص المستخرج—كل ذلك مع شروحات واضحة لأهمية كل خطوة.

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6 SDK (or later) | ميزات C# الحديثة وأداء أفضل |
| Visual Studio 2022 (or VS Code) | تصحيح سهل وIntelliSense مريح |
| NuGet package **Aspose.OCR** | يوفر `OcrEngine` وفئات الفلاتر |
| An input image (e.g., `skewed‑noisy.png`) | يوضح الحاجة إلى المعالجة المسبقة |

إذا كان أي من هذه مفقودًا، قم بتثبيته أولًا. خطوة NuGet مغطاة في القسم التالي.

## الخطوة 1: تثبيت Aspose.OCR عبر NuGet

افتح الطرفية (أو Package Manager Console) وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** استخدم العلامة `--version` لتثبيت إصدار محدد إذا كنت تحتاج إلى بنى قابلة لإعادة الإنتاج.

الحزمة تأتي مع جميع الفلاتر التي سنحتاجها، لذا لا توجد DLLs إضافية مطلوبة.

## الخطوة 2: تهيئة محرك OCR – قلب دليل c# OCR

إنشاء المحرك سهل، لكن من المفيد فهم ما يحدث خلف الكواليس. الـ `OcrEngine` يحتفظ بخط أنابيب من **الفلاتر** التي تعالج الـ bitmap قبل تشغيل خوارزمية التعرف.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Initialize the OCR engine – this is the core object for the entire tutorial
var ocrEngine = new OcrEngine();
```

> **لماذا التهيئة أولًا؟** المحرك يخزن موارد داخلية (مثل نماذج اللغة). إعادة استخدام نسخة واحدة عبر صور متعددة توفر الذاكرة وتسرّع عمليات التعرف اللاحقة.

## الخطوة 3: معالجة الصورة مسبقًا للـ OCR – إضافة تصحيح الميل، إزالة الضوضاء، وتعزيز التباين

معظم المسحات الواقعية ليست مثالية؛ فهي مائلة، مليئة بالبقع، أو مظلمة جدًا. لهذا السبب **معالجة الصورة للـ OCR** خطوة حاسمة. Aspose توفر ثلاثة فلاتر تعمل معًا بشكل ممتاز:

| الفلتر | ما يفعله | حالة الاستخدام النموذجية |
|--------|--------------|------------------|
| `DeskewFilter` | يدور الصورة لتصحيح الميل | مستندات ممسوحة من ماسح ضوئي |
| `DenoiseFilter` | يزيل البكسلات المعزولة (ضوضاء “ملح وفلفل”) | صور بإضاءة منخفضة |
| `ContrastBoostFilter` | يزيد التباين لتوضيح حواف النص | مطبوعات باهتة أو لقطات منخفضة الدقة |

الكود التالي يضيف كل فلتر إلى خط أنابيب المحرك:

```csharp
// 1️⃣ Deskew – automatically rotates the image to the proper orientation
ocrEngine.Filters.Add(new DeskewFilter());

// 2️⃣ Denoise – cleans up speckles that can confuse the OCR engine
ocrEngine.Filters.Add(new DenoiseFilter());

// 3️⃣ Contrast Boost – amplifies the difference between foreground text and background
ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5 });
```

> **كيف يعمل:** عندما تستدعي `RecognizeImage` لاحقًا، سيقوم المحرك بتشغيل هذه الفلاتر الثلاثة بالتسلسل قبل تمرير الـ bitmap المنظف إلى نواة التعرف.

### توضيح بصري (اختياري)

إذا أدرجت صورة، تأكد أن نص alt يحتوي على الكلمة الرئيسية:

```markdown
![c# ocr tutorial preprocessing example](/images/ocr-preprocess.png)
```

## الخطوة 4: التعرف على النص من الصورة – لحظة الحقيقة

الآن بعد أن تم معالجة الصورة، يمكننا أخيرًا استخراج الأحرف. الطريقة تُعيد سلسلة نصية عادية، يمكنك تسجيلها، تخزينها، أو تمريرها إلى نظام آخر.

```csharp
// Replace the path with the actual location of your test image
string imagePath = @"YOUR_DIRECTORY/skewed-noisy.png";

// Perform OCR – this call applies all the filters we added earlier
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

### النتيجة المتوقعة

تشغيل العينة على مسح فاتورة نموذجي ينتج شيء مثل:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

إذا كان الإخراج غير مفهوم، تحقق من جودة الصورة وفكّر في تعديل `ContrastBoostFilter.Level` (القيم > 2.0 قد تكون مفرطة).

## الخطوة 5: إخراج النتيجة والمعالجة اللاحقة الاختيارية

تطبيق كونسول يمكنه ببساطة كتابة السلسلة، لكن العديد من المشاريع تحتاج إلى معالجة إضافية—مثل حذف الفراغات، إزالة فواصل الأسطر، أو إدخال النص في قاعدة بيانات.

```csharp
// Basic console output
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);

// Example of lightweight post‑processing
string cleaned = recognizedText
    .Replace("\r", "")
    .Replace("\n", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

### لماذا المعالجة اللاحقة؟

حتى مع معالجة مسبقة جيدة، غالبًا ما يضيف OCR فواصل أسطر عشوائية أو أحرف غير مرئية. سلسلة `Replace` سريعة يمكنها جعل البيانات أكثر قابلية للاستخدام لاحقًا.

## الخطوة 6: مثال كامل جاهز للنسخ واللصق

فيما يلي البرنامج **الكامل** الذي يمكنك تجميعه وتشغيله فورًا. يتضمن جميع عبارات using، إعداد الفلاتر، استدعاء OCR، ومعالجة الإخراج.

```csharp
// ---------------------------------------------------------------
// Complete c# ocr tutorial – Recognize Text from Image
// ---------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());                     // Fix rotation
        ocrEngine.Filters.Add(new DenoiseFilter());                    // Remove speckles
        ocrEngine.Filters.Add(new ContrastBoostFilter { Level = 1.5 }); // Boost contrast

        // 3️⃣ Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed-noisy.png";

        // 4️⃣ Perform OCR – this also runs the filters we added
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // 5️⃣ Show raw OCR result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);

        // 6️⃣ Optional: simple cleanup for downstream use
        string cleaned = recognizedText
            .Replace("\r", "")
            .Replace("\n", " ")
            .Trim();

        Console.WriteLine("\n=== Cleaned Text ===");
        Console.WriteLine(cleaned);
    }
}
```

**كيفية تشغيله**

1. احفظ الملف باسم `Program.cs` داخل مشروع كونسول جديد (`dotnet new console`).
2. استبدل `YOUR_DIRECTORY/skewed-noisy.png` بالمسار الحقيقي لصورتك التجريبية.
3. نفّذ `dotnet run`. يجب أن ترى ناتج OCR مطبوعًا في الطرفية.

## المشكلات الشائعة والنصائح (التعرف على النص من الصورة بثقة)

| المشكلة | ما الذي يجب التحقق منه | الحل |
|-------|----------------|-----|
| **حروف غير مفهومة** | الصورة مظلمة جدًا أو منخفضة الدقة | زيادة `ContrastBoostFilter.Level` أو استخدام مصدر بدقة أعلى |
| **خطوط مفقودة** | لم يصحح Deskew الزاوية بالكامل | دوّر الصورة يدويًا أولاً، أو اضبط تحمل `DeskewFilter` |
| **أداء بطيء** | معالجة العديد من الصور الكبيرة في حلقة | إعادة استخدام نفس كائن `OcrEngine` واستدعاء `ocrEngine.Clear()` بعد كل تشغيل |
| **لغة غير مدعومة** | النص ليس بالإنجليزية | عيّن `ocrEngine.Language = OcrLanguage.French` (أو لغة مدعومة أخرى) قبل التعرف |

### حالة خاصة: معالجة ملفات PDF متعددة الصفحات

إذا كنت بحاجة إلى OCR لملف PDF، حوّل كل صفحة إلى صورة (مثلاً باستخدام `Aspose.PDF`) ومرّرها واحدةً تلو الأخرى إلى نفس المحرك. يبقى خط أنابيب المعالجة المسبقة كما هو، مما يضمن نتائج متسقة عبر الصفحات.

## الخلاصة

في هذا **دليل c# OCR** غطينا كل ما تحتاجه **للتعرف على النص من الصورة** و**معالجة الصورة للـ OCR** باستخدام الفلاتر المدمجة في Aspose.OCR. من خلال تهيئة المحرك، إضافة خطوات تصحيح الميل، إزالة الضوضاء، وتعزيز التباين، وأخيرًا استدعاء `RecognizeImage`، ستحصل على استخراج نص نظيف وموثوق ببضع أسطر من الشيفرة فقط.

لا تتردد في التجربة—استبدل فلترًا بآخر، اضبط مستوى التباين، أو دمج النتيجة في خط أنابيب بيانات أكبر. المفاهيم هنا تنطبق على أي مكتبة OCR: المعالجة المسبقة غالبًا ما تكون الفارق بين فاتورة نصف مقروءة ومستند مُلتقط بالكامل.

هل لديك أسئلة أخرى؟ ربما ترغب في معرفة كيفية التعامل مع النص المكتوب يدويًا أو معالجة آلاف الملفات دفعة واحدة. اترك تعليقًا، وسنستكشف تلك السيناريوهات معًا. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}