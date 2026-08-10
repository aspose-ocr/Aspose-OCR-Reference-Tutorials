---
category: general
date: 2026-04-26
description: كيفية التعرف الضوئي على الأحرف العربية في C# – تعلم تحويل الصورة إلى
  نص، استخراج النص العربي من PNG، وتحميل الصورة للتعرف الضوئي على الأحرف باستخدام
  Aspose OCR.
draft: false
keywords:
- how to ocr arabic
- extract arabic text
- convert image to text
- extract text from png
- load image for ocr
language: ar
og_description: كيفية التعرف الضوئي على الحروف العربية في C# – دليل خطوة بخطوة يوضح
  كيفية تحويل الصورة إلى نص، استخراج النص العربي من PNG، وتحميل الصورة للتعرف الضوئي
  على الحروف.
og_title: كيفية التعرف الضوئي على الحروف العربية – دليل C# الكامل
tags:
- OCR
- C#
- Aspose
title: كيفية التعرف الضوئي على الحروف العربية – دليل C# لاستخراج النص العربي
url: /ar/net/text-recognition/how-to-ocr-arabic-c-guide-to-extract-arabic-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص العربي – دليل كامل بلغة C#

هل تساءلت يومًا **كيفية التعرف الضوئي على النص العربي** مباشرةً من عقد ممسوح ضوئيًا أو لقطة شاشة؟ لست وحدك—المطورون يسألون باستمرار، “هل يمكنني حقًا استخراج الأحرف العربية من ملف PNG دون فقدان الاتجاهية؟” الجواب المختصر هو نعم، وهذا الدليل سيقودك عبر العملية بالكامل، من تحميل الصورة إلى طباعة النتيجة.

في الدقائق القليلة القادمة ستتعلم كيف **تحول الصورة إلى نص**، وكيف **استخراج النص العربي** باستخدام Aspose OCR، ولماذا تحميل الصورة بشكل صحيح مهم. لا إطالة، مجرد مثال عملي يمكنك إدراجه في أي مشروع .NET.  

## ما ستحتاجه

* **.NET 6+** (تعمل الواجهة البرمجية بنفس الطريقة على .NET Framework، لكن أحدث بيئة تشغيل تمنحك أفضل أداء).  
* **Aspose.OCR for .NET** – يمكنك الحصول عليها من NuGet (`Install-Package Aspose.OCR`).  
* ملف صورة يحتوي على أحرف عربية، على سبيل المثال `arabic_contract.png`.  
* قدر بسيط من معرفة C#—إذا كنت تستطيع كتابة `Console.WriteLine` فأنت جاهز للانطلاق.

هذا كل شيء. لا محركات OCR إضافية، لا خدمات خارجية، مجرد مكتبة واحدة تتعامل مع النصوص من اليمين إلى اليسار مباشرةً.

## تنفيذ خطوة بخطوة

نقسم الحل إلى أجزاء صغيرة. كل قسم يحتوي على عنوان واضح، ومقتطف شفرة قصير، وتفسير **لماذا** هذه الخطوة مهمة. لا تتردد في نسخ‑لصق المقتطفات؛ الكتلة النهائية في النهاية هي برنامج جاهز للتنفيذ.

### ## كيفية التعرف الضوئي على النص العربي باستخدام Aspose OCR في C#

أول شيء تحتاج إلى فعله هو إنشاء نسخة من محرك OCR. هذا الكائن يحمل جميع خيارات التكوين—اللغة، تخطيط الصفحة، مصدر الصورة، إلخ.  

```csharp
using Aspose.OCR;

// Create the OCR engine – this is the core object that does the heavy lifting.
OcrEngine ocrEngine = new OcrEngine();
```

*لماذا هذا مهم:* `OcrEngine` يضم خوارزمية التعرف. بدون هذا لا يمكنك ضبط اللغة أو إمداد المحرك بصورة.

### ## تحويل الصورة إلى نص – تحميل PNG بشكل صحيح

الآن بعد أن المحرك موجود، وجهه إلى الصورة التي تريد معالجتها. Aspose توفر المساعد `ImageStream`، الذي يخفف من تعقيدات نظام الملفات.

```csharp
// Load the PNG that contains Arabic text.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_contract.png");
```

> **نصيحة احترافية:** إذا كانت صورتك موجودة في تدفق (مثلاً من طلب ويب)، استخدم `ImageStream.FromStream(yourStream)` بدلاً من `FromFile`. هذا يتجنب الملفات المؤقتة ويسرّع العملية.

*لماذا هذا مهم:* خطوة **تحميل الصورة للتعرف الضوئي** تضمن أن المحرك يعمل على البايتات الدقيقة التي تزودها. تنسيق بكسل غير متطابق قد يتسبب في فقدان الأحرف.

### ## ضبط اللغة – استخراج النص العربي بدقة

العربية ليست مجرد أبجدية أخرى؛ إنها نص من اليمين إلى اليسار مع تشكيل سياقي. عليك إخبار المحرك باللغة المتوقعة.

```csharp
// Tell Aspose we are dealing with Arabic.
ocrEngine.Language = Language.Arabic;
```

*لماذا هذا مهم:* إذا تركت اللغة على الإعداد الافتراضي (عادةً الإنجليزية)، سيحاول المحرك ربط رموز العربية بحروف لاتينية، ما ينتج مخرجات مشوشة. ضبط `Language.Arabic` يُفعّل مجموعة الأحرف وقواعد التشكيل الصحيحة.

### ## تمكين ترتيب من اليمين إلى اليسار (اختياري لكن صريح)

Aspose OCR يتحول تلقائيًا إلى اليمين‑إلى‑اليسار للعربية، لكن الصراحة تجعل الشيفرة ذات توثيق ذاتي.

```csharp
// Explicitly set text direction—useful when you later switch languages.
ocrEngine.Options.TextDirection = TextDirection.RightToLeft;
```

*لماذا هذا مهم:* عندما تضيف دعمًا متعدد اللغات لاحقًا (مثلاً الإنجليزية + العربية في نفس الصفحة)، العلم الصريح يمنع ترتيب غير مقصود من اليسار إلى اليمين.

### ## تنفيذ التعرف الضوئي – استخراج النص من PNG

كل التحضيرات انتهت؛ الآن نقوم فعليًا بالتعرف على الأحرف.

```csharp
// Run the recognition engine.
RecognitionResult recognitionResult = ocrEngine.Recognize();
```

*لماذا هذا مهم:* `Recognize()` تُعيد كائن `RecognitionResult` يحتوي على سلسلة Unicode الخام، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

### ## عرض النتيجة – التحقق من الاستخراج

أخيرًا، اطبع السلسلة العربية المستخرجة إلى وحدة التحكم. يمكنك أيضًا كتابتها إلى ملف أو قاعدة بيانات.

```csharp
// Output the Arabic text.
Console.WriteLine("Extracted Arabic text:");
Console.WriteLine(recognitionResult.Text);
```

**الناتج المتوقع** (بافتراض أن PNG يحتوي على العبارة “عقد إيجار”):

```
Extracted Arabic text:
عقد إيجار
```

إذا رأيت علامات استفهام أو سلاسل فارغة، تحقق مرة أخرى من وضوح الصورة وأنك ضبطت اللغة بشكل صحيح.

### ## مثال كامل يعمل

نجمع كل شيء معًا، إليك تطبيق console بسيط يمكنك تجميعه وتشغيله:

```csharp
using System;
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine.
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Set the language to Arabic – crucial for correct shaping.
            ocrEngine.Language = Language.Arabic;

            // 3️⃣ Load the image you want to process.
            // Replace the path with the actual location of your PNG.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_contract.png");

            // 4️⃣ (Optional) Explicitly enforce right‑to‑left ordering.
            ocrEngine.Options.TextDirection = TextDirection.RightToLeft;

            // 5️⃣ Run the recognition.
            RecognitionResult result = ocrEngine.Recognize();

            // 6️⃣ Output the result.
            Console.WriteLine("Extracted Arabic text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

احفظه باسم `Program.cs`، نفّذ `dotnet run`، ويجب أن ترى النص العربي يُطبع في وحدة التحكم.

## أسئلة شائعة وحالات خاصة

**ماذا لو كانت الصورة منخفضة الدقة؟**  
تنخفض دقة OCR بشكل حاد تحت 150 dpi. استخدم مكتبة تحسين الصور (مثل ImageSharp) لتكبير أو تحسين وضوح الصورة قبل تمريرها إلى Aspose.

**هل يمكنني معالجة صفحات متعددة في تشغيل واحد؟**  
نعم. كرّر عبر مجموعة من مسارات الملفات وعيّن كل مسار إلى `ocrEngine.Image` قبل استدعاء `Recognize()`. تذكّر إعادة ضبط أي خيارات خاصة بالصورة إذا اختلفت.

**هل أحتاج إلى معالجة الحركات بشكل منفصل؟**  
لا. حزمة اللغة العربية في Aspose تدعم الحركات بالكامل. الحالة الوحيدة التي قد تحتاج فيها معالجة إضافية هي عندما تريد تطبيع النص لفهرسة البحث.

**كيف أستخرج النص من JPEG بدلاً من PNG؟**  
نفس الشيفرة تمامًا—فقط غيّر امتداد الملف. Aspose OCR يعمل مع معظم صيغ الصور النقطية (`.png`, `.jpg`, `.bmp`, `.tiff`).

**هل هناك طريقة للحصول على درجات الثقة لكل كلمة؟**  
`RecognitionResult` يوفّر مجموعة `Words`، كل عنصر يحتوي على خاصية `Confidence`. يمكنك التجول فيها لتصفية النتائج ذات الثقة المنخفضة.

## نصائح لتطبيق OCR عربي جاهز للإنتاج

* **معالجة مسبقة للصورة:** ثنٍّ، تصحيح الميل، وإزالة الضوضاء الخلفية. حتى استدعاء سريع لـ `ImageProcessor` يمكن أن يزيد الدقة بنسبة 10‑15 %.  
* **تخزين المحرك في الذاكرة:** إنشاء `OcrEngine` رخيص نسبيًا، لكن إعادة استخدام نسخة واحدة عبر طلبات متعددة يقلل من استهلاك الذاكرة.  
* **التعامل مع واجهة من اليمين إلى اليسار:** عند عرض النص المستخرج في تطبيق WinForms أو ويب، اضبط خاصية `RightToLeft` للعنصر إلى `Yes` لتظهر العربية بشكل صحيح.  
* **سجّل Unicode الخام:** احفظ السلسلة الدقيقة التي تحصل عليها من `recognitionResult.Text`؛ لا تطبق أي تحويل تلقائي إلا إذا كنت بحاجة صريحة لذلك.

## الخلاصة

أنت الآن تعرف **كيفية التعرف الضوئي على النص العربي** في C# باستخدام Aspose OCR، وكيف **تحول الصورة إلى نص**، والخطوات الدقيقة **لتحميل الصورة للتعرف الضوئي** و**استخراج النص العربي** من ملف PNG. المثال الكامل أعلاه جاهز للإدراج في أي حل .NET، والنصائح الإضافية ستساعدك على الانتقال من عرض تجريبي سريع إلى خط أنابيب إنتاجي قوي.

هل أنت مستعد للتحدي التالي؟ جرّب دمج هذا مع **استخراج النص من PNG** للمستندات متعددة اللغات، أو مرّر الناتج إلى واجهة برمجة تطبيقات ترجمة للحصول على نسخ إنجليزية فورية من العقود العربية. السماء هي الحد—جرب، كرّر، ودع OCR يتولى الجزء الصعب.

إذا واجهت أي مشكلة أو لديك تحسين ذكي ترغب في مشاركته، اترك تعليقًا أدناه. برمجة سعيدة!  

![how to ocr arabic example](arabic-ocr-example.png){alt="مثال على التعرف الضوئي على النص العربي"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}