---
category: general
date: 2026-04-11
description: استخراج النص من ملفات TIFF باستخدام معالجة دفعات OCR من Aspose في C#.
  تعلّم كيفية معالجة دفعات OCR بفعالية والحصول على تغذية راجعة فورية حول التقدّم.
draft: false
keywords:
- extract text from tiff
- process batch ocr
- OCR batch processing
- Aspose OCR C#
- TIFF image OCR
language: ar
og_description: استخراج النص من ملفات TIFF باستخدام معالجة الدُفعات OCR من Aspose
  في C#. يوضح هذا الدرس خطوة بخطوة كيفية معالجة OCR على دفعات وقراءة التقدم.
og_title: استخراج النص من ملفات TIFF باستخدام OCR دفعي في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
- Image Processing
title: استخراج النص من ملفات TIFF باستخدام OCR دفعي في C# – دليل كامل
url: /ar/net/text-recognition/extract-text-from-tiff-with-batch-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من ملفات TIFF – دليل كامل لمعالجة OCR دفعة

هل احتجت يوماً إلى **استخراج النص من ملفات TIFF** لكن شعرت بأن مرحلة المعالجة الدفعة عائق؟ لست وحدك. في العديد من مشاريع أتمتة المستندات، يمكن أن يصبح التعامل مع عشرات الصور عالية الدقة بصيغة TIF عبئاً كبيراً—خاصةً عندما تريد الحصول على تغذية راجعة مباشرة حول التقدم.

الخبر السار؟ باستخدام Aspose OCR يمكنك **معالجة OCR دفعة** ببضع أسطر فقط، والحصول على أحداث تقدم في الوقت الحقيقي، وإخراج النص المعترف به لكل صورة. في هذا الدرس سنستعرض تطبيقًا جاهزًا بلغة C# يعمل على وحدة التحكم يقوم بذلك تمامًا.

سنغطي كل ما تحتاج معرفته: الحزم المطلوبة، لماذا كل سطر مهم، الحالات الخاصة مثل الملفات المفقودة، وكيفية التحقق من النتائج. في النهاية ستتمكن من إضافة العينة إلى مشروعك والبدء في استخراج النص من صور TIFF فورًا.

## ما ستحتاجه

- **.NET 6 أو أحدث** (الكود يُجمّع أيضًا مع .NET Core)  
- حزمة NuGet **Aspose.OCR for .NET** – `Install-Package Aspose.OCR`  
- مجلد يحتوي على بعض صور **TIFF** التي تريد قراءتها (العينة تستخدم `img1.tif`, `img2.tif`, `img3.tif`)  
- أي بيئة تطوير تفضلها – Visual Studio، Rider، أو VS Code تكفي  

لا تحتاج إلى أي إعدادات إضافية؛ المكتبة تأتي مع محرك OCR الخاص بها، لذا لن تحتاج إلى تثبيت ملفات تنفيذية أصلية خارجية.

---

## الخطوة 1 – إنشاء كائن محرك OCR  

أول ما تقوم به هو إنشاء `OcrEngine`. فكر فيه كالعقل الذي سيحلل كل بكسل ويحوّله إلى أحرف.

```csharp
using Aspose.OCR;

// Step 1: Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:**  
> يحتفظ المحرك بنماذج اللغة الداخلية والإعدادات (مثل DPI، اللغة). إن إنشاؤه مرة واحدة وإعادة استخدامه لمعالجة دفعة هو أكثر كفاءة من إنشاء محرك جديد لكل صورة.

---

## الخطوة 2 – ربط أحداث التقدم في الوقت الحقيقي  

إذا كنت تعالج عشرات ملفات TIFF، فإن مؤشر التقدم يمكن أن ينقذك من التساؤل عما إذا كان التطبيق عالقًا.

```csharp
using Aspose.OCR.Events;

// Step 2: Subscribe to progress updates
ocrEngine.ProgressChanged += Ocr_ProgressChanged;

// Event handler definition (placed later in the file)
```

حدث `ProgressChanged` يُطلق بعد انتهاء كل صورة، موفرًا لك القيم `Current`, `Total`, و `Percentage`. هذه هي حلقة التغذية الراجعة **process batch OCR** التي ينسى معظم المطورين تنفيذها.

---

## الخطوة 3 – بناء قائمة من تدفقات الصور  

Aspose.OCR يعمل مع كائنات `ImageStream`. أسهل طريقة هي تحميل كل TIFF من القرص.

```csharp
using Aspose.OCR;
using System.Collections.Generic;

// Step 3: Prepare the batch of TIFF images
List<ImageStream> imageFiles = new List<ImageStream>
{
    ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
    ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
};
```

> **نصيحة:**  
> إذا كان لديك مجلد ديناميكي، استبدل القائمة الثابتة بـ `Directory.GetFiles(path, "*.tif")` ثم `Select(ImageStream.FromFile)` – بهذه الطريقة ستتمكن من **process batch OCR** دون تحديث يدوي.

---

## الخطوة 4 – تشغيل عملية OCR الدفعة  

الآن يحدث العمل الشاق. `ProcessBatch` تُعيد قائمة قراءة‑فقط من كائنات `OcrResult`، كل منها يحتوي على النص المستخرج وتقييمات الثقة.

```csharp
// Step 4: Execute batch OCR and collect results
IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);
```

> **لماذا هذا فعال:**  
> يعيد المحرك استخدام نفس نموذج اللغة عبر جميع الصور، مما يقلل بشكل كبير استهلاك الذاكرة مقارنةً بالاتصالات الفردية لكل صورة.

---

## الخطوة 5 – عرض أو تخزين النص المعترف به  

أخيرًا، قم بالتكرار على النتائج. في مشروع حقيقي قد تكتبها إلى قاعدة بيانات أو ملف JSON، لكن في هذه العينة سنطبعها فقط على وحدة التحكم.

```csharp
// Step 5: Output the recognised text for each TIFF
foreach (var result in ocrResults)
{
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();
}
```

**الناتج المتوقع على وحدة التحكم** (مقتطع للوضوح):

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,250.00

=== OCR Result ===
Meeting Minutes
1. Project kickoff...
```

إذا فشلت أي صورة، سيكون `result.Text` سلسلة فارغة، وستظل حدث `ProgressChanged` يُبلغ عن العنصر كمعالج—وبالتالي يمكنك تسجيل الأخطاء بشكل منفصل.

---

## معالج حدث التقدم (الكود الكامل)

ضع هذه الطريقة في أي مكان داخل فئة `BatchDemo`—يفضل بعد `Main`.

```csharp
private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
{
    // Gives you a live view of how many files have been processed
    Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
}
```

> **نصيحة احترافية:**  
> قم بإعادة توجيه هذا الإخراج إلى شريط تقدم في واجهة المستخدم إذا كنت تبني تطبيق سطح مكتب؛ الحدث نفسه يعمل مع WinForms، WPF، أو حتى إشعارات ASP.NET Core SignalR.

---

## عينة كاملة جاهزة للتنفيذ  

بجمع كل ما سبق، إليك البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Events;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Subscribe to progress events
        ocrEngine.ProgressChanged += Ocr_ProgressChanged;

        // 3️⃣ Load TIFF images into a list
        List<ImageStream> imageFiles = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/img1.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img2.tif"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/img3.tif")
        };

        // 4️⃣ Run batch OCR
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imageFiles);

        // 5️⃣ Print results
        foreach (var result in ocrResults)
        {
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);
            Console.WriteLine();
        }
    }

    // Progress event handler
    private static void Ocr_ProgressChanged(object sender, ProgressChangedEventArgs e)
    {
        Console.WriteLine($"Processed {e.Current}/{e.Total} – {e.Percentage}%");
    }
}
```

احفظ الملف باسم `Program.cs`، نفّذ `dotnet add package Aspose.OCR`، استبدل `YOUR_DIRECTORY` بالمسار الفعلي، واضغط **Ctrl+F5**. يجب أن ترى أرقام التقدم متبوعة بالنص المستخرج لكل ملف TIFF.

---

## معالجة الحالات الشائعة

| الحالة | ما يجب مراقبته | الحل السريع |
|-----------|-------------------|-----------|
| **TIFF مفقود أو تالف** | `ImageStream.FromFile` يرمي `FileNotFoundException` أو `ArgumentException`. | غلف إنشاء القائمة بـ `try/catch` وتجاوز الملفات غير الصالحة مع تسجيل المشكلة. |
| **صور كبيرة جدًا ( >10 MP )** | قد يستهلك OCR الكثير من الذاكرة ويبطئ العملية. | قلل DPI قبل المعالجة: `ocrEngine.ImagePreprocessing.Dpi = 300;` |
| **نص غير إنجليزي** | نموذج اللغة الافتراضي هو الإنجليزية. | عيّن `ocrEngine.Language = Language.Spanish;` (أو أي لغة مدعومة). |
| **الحاجة لحفظ النتائج** | إخراج وحدة التحكم غير دائم. | اكتب `result.Text` إلى ملف `.txt` باستخدام `File.WriteAllText`. |

معالجة هذه السيناريوهات تجعل حلك قويًا وتظهر للذكاء الاصطناعي أنك فكرت بما يتجاوز المسار السعيد.

---

## الخطوات التالية والمواضيع ذات الصلة  

- **استخراج النص من PDF** – API مشابه، فقط استبدل `ImageStream` بـ `PdfDocument`.  
- **OCR دفعة متوازية** – لأحمال عمل ضخمة، شغّل عدة مثيلات من `OcrEngine` على خيوط منفصلة؛ تذكّر احترام حدود الترخيص.  
- **ما بعد المعالجة** – مرّر ناتج OCR عبر مدقق إملائي أو تعبيرات regex لتنظيف الأخطاء الشائعة.  

جميع هذه الإضافات لا تزال تعتمد على الفكرة الأساسية لـ **process batch OCR** ويمكن إضافتها تدريجيًا.

---

## الخلاصة  

لقد عرضنا للتو كيفية **استخراج النص من ملفات TIFF** بفعالية عبر **process batch OCR** باستخدام Aspose OCR بلغة C#. العينة تنشئ محركًا واحدًا، تشترك في أحداث التقدم، تُحمّل قائمة من تدفقات الصور، تُنفّذ الدفعة، وتطبع كل نتيجة.

من هنا يمكنك دمج المخرجات في قواعد بيانات، إنشاء ملفات PDF قابلة للبحث، أو تمرير النص إلى خطوط أنابيب NLP لاحقة. السماء هي الحد—جرّب إعدادات اللغة، تعديل DPI، والتنفيذ المتوازي لتناسب عبء عملك الخاص.

هل لديك أسئلة أو تريد مشاركة تعديلك للدفعة؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}