---
category: general
date: 2026-06-16
description: معالجة OCR الدفعية في C# تتيح لك تحويل الصور إلى نص بسرعة. تعلم كيفية
  استخراج النص من الصور باستخدام Aspose.OCR مع كود خطوة بخطوة.
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: ar
og_description: معالجة OCR دفعة في C# تحول الصور إلى نص. اتبع هذا الدليل لاستخراج
  النص من الصور باستخدام Aspose.OCR.
og_title: معالجة OCR دفعية في C# – استخراج النص من الصور
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: معالجة OCR دفعيًا في C# – دليل كامل لاستخراج النص من الصور
url: /ar/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة OCR دفعيًا في C# – دليل كامل لاستخراج النص من الصور

هل تساءلت يومًا كيف تقوم **بمعالجة OCR دفعيًا** في C# دون كتابة حلقة منفصلة لكل صورة؟ لست وحدك. عندما يكون لديك العشرات — أو حتى المئات — من الإيصالات الممسوحة ضوئيًا، الفواتير، أو الملاحظات المكتوبة يدويًا، يصبح إدخال كل ملف يدويًا إلى محرك OCR كابوسًا سريعًا.  

الأخبار السارة؟ مع Aspose.OCR يمكنك *تحويل الصور إلى نص* في عملية واحدة منظمة. في هذا الدرس سنستعرض سير العمل بالكامل، من تثبيت المكتبة إلى تشغيل مهمة دفعية جاهزة للإنتاج **تستخرج النص من الصور** وتحفظ النتائج بالتنسيق الذي تحتاجه.

> **ما ستحصل عليه:** تطبيق كونسول جاهز للتنفيذ يعالج مجلدًا كاملًا، يكتب ملفات نصية عادية (أو JSON، XML، HTML، PDF) جنبًا إلى جنب مع الأصليات، ويظهر لك كيفية تعديل التوازي لتحقيق أقصى معدل نقل.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework على حد سواء)
- Visual Studio 2022، VS Code، أو أي محرر C# تفضله
- رخصة Aspose.OCR عبر NuGet (الإصدار التجريبي المجاني يكفي للتقييم)
- مجلد يحتوي على ملفات صور (`.png`، `.jpg`، `.tif`، إلخ) تريد **تحويل الصور إلى نص**

إذا كانت كل هذه المتطلبات متوفرة، لنبدأ.

![مخطط يوضح تدفق معالجة OCR دفعيًا](batch-ocr-workflow.png "تدفق معالجة OCR دفعيًا")

## الخطوة 1: تثبيت Aspose.OCR عبر NuGet

أولاً، أضف حزمة Aspose.OCR إلى مشروعك. افتح طرفية في دليل المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت داخل Visual Studio، انقر بزر الماوس الأيمن على *Dependencies → Manage NuGet Packages*، ابحث عن **Aspose.OCR**، وانقر *Install*. هذه السطر الواحد يجلب لك كل ما تحتاجه لـ **معالجة OCR دفعيًا**.

> **نصيحة احترافية:** حافظ على تحديث نسخة الحزمة؛ الإصدار الأخير (حتى يونيو 2026) يضيف دعمًا لتنسيقات صور جديدة ويحسن الدقة متعددة اللغات.

## الخطوة 2: إنشاء هيكلية تطبيق الكونسول

أنشئ تطبيق كونسول C# جديد (إذا لم تقم بذلك بعد) واستبدل ملف `Program.cs` المُولد بالهيكلية التالية. لاحظ توجيه `using Aspose.OCR;` في الأعلى – هذا هو النطاق الذي يوفر لنا فئة `OcrBatchProcessor`.

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

في هذه المرحلة الملف مجرد عنصر نائب، لكنه نقطة انطلاق نظيفة لمنطق **معالجة OCR دفعيًا**.

## الخطوة 3: تهيئة OcrBatchProcessor

`OcrBatchProcessor` هو العنصر الأساسي الذي يفحص مجلدًا، ينفذ OCR على كل صورة مدعومة، ويكتب الناتج. إنشاء كائن منه بسيط كالتالي:

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

لماذا نستخدم معالج دفعي بدلاً من واجهة برمجة تطبيقات صورة واحدة؟ الفئة الدفعية تتعامل تلقائيًا مع تعداد الملفات، وتسجيل الأخطاء، وحتى التنفيذ المتوازي، مما يعني أنك تقضي وقتًا أقل في كتابة الحلقات ووقتًا أكثر في تحسين الدقة.

## الخطوة 4: تحديد مجلدات الإدخال والإخراج

أخبر المعالج من أين يقرأ الصور وإلى أين يضع النتائج. استبدل مسارات العنصر النائب بأدلة حقيقية على جهازك.

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

يجب أن يكون كلا المجلدين موجودين قبل تشغيل التطبيق؛ وإلا ستحصل على استثناء `DirectoryNotFoundException`. إنشاءهما برمجيًا سهل، لكن من أجل الوضوح نحتفظ بالمثال بسيطًا.

## الخطوة 5: اختيار تنسيق الإخراج

يمكن لـ Aspose.OCR إنتاج نص عادي، JSON، XML، HTML، أو حتى PDF. في معظم سيناريوهات **استخراج النص من الصور**، النص العادي يكفي، لكن لا تتردد في تغييره.

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

إذا كنت تحتاج إلى بيانات منظمة للمعالجة اللاحقة، فإن `ResultFormat.Json` خيار قوي. المكتبة ستغلف نص كل صفحة تلقائيًا في كائن JSON، مع الحفاظ على معلومات التخطيط.

## الخطوة 6: ضبط اللغة والتوازي

دقة OCR تعتمد على نموذج اللغة الصحيح. الإنجليزية تعمل لمعظم المستندات الغربية، لكن يمكنك اختيار أي لغة مدعومة (العربية، الصينية، إلخ). بالإضافة إلى ذلك، يمكنك إخبار المعالج بعدد الخيوط التي يجب تشغيلها — حتى أربعة بشكل افتراضي.

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**لماذا التوازي مهم:** إذا كان لديك معالج رباعي النواة، ضبط `MaxDegreeOfParallelism` إلى `4` يمكن أن يقلل وقت المعالجة بنحو 75 ٪. على لابتوب ثنائي النواة، `2` هو خيار أكثر أمانًا. جرب لتجد الإعداد المثالي لجهازك.

## الخطوة 7: تشغيل المهمة الدفعية

الآن يحدث العمل الشاق. سطر واحد يطلق كامل خط الأنابيب، يعالج كل صورة في مجلد الإدخال ويكتب النتائج إلى مجلد الإخراج.

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

عندما يطبع الكونسول *Batch OCR completed.*، ستجد ملف `.txt` (أو أي تنسيق اخترته) بجانب كل صورة أصلية. أسماء الملفات تتطابق مع المصدر، مما يجعل ربط ناتج OCR بالصورة الأصلية أمرًا بسيطًا.

## مثال كامل يعمل

بجمع كل ذلك معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs` وتشغيله فورًا:

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### النتيجة المتوقعة

بافتراض أن لديك ثلاث صور (`invoice1.png`، `receipt2.jpg`، `form3.tif`) في مجلد الإدخال، سيحتوي مجلد الإخراج على:

```
invoice1.txt
receipt2.txt
form3.txt
```

كل ملف `.txt` يحتوي على الأحرف الخام المستخرجة من الصورة المقابلة. افتح أي ملف باستخدام Notepad، وسترى تمثيل النص العادي للمسح الأصلي.

## أسئلة شائعة وحالات حافة

### ماذا لو فشلت معالجة بعض الصور؟

`OcrBatchProcessor` يسجل الأخطاء إلى الكونسول بشكل افتراضي ويستمر في الملف التالي. للاستخدام في الإنتاج، يمكنك الاشتراك في حدث `OnError` لجمع أسماء الملفات الفاشلة وإعادة المحاولة لاحقًا.

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### هل يمكنني معالجة ملفات PDF مباشرةً؟

نعم. Aspose.OCR يتعامل مع كل صفحة من PDF كصورة داخليًا. فقط ضع `InputFolder` إلى دليل يحتوي على ملفات PDF، وسيستخرج المعالج النص من كل صفحة — بفعالية **تحويل الصور إلى نص** حتى عندما يكون المصدر PDF.

### كيف أتعامل مع مستندات متعددة اللغات؟

اضبط `Language` إلى `OcrLanguage.Multilingual` أو حدد قائمة باللغات إذا كانت نسخة المكتبة تدعم ذلك. سيحاول المحرك التعرف على الأحرف من جميع اللغات المحددة، وهو مفيد للفواتير الدولية.

### ماذا عن استهلاك الذاكرة؟

معالج الدفعات يبث كل صورة، لذا يبقى استهلاك الذاكرة منخفضًا حتى مع آلاف الملفات. ومع ذلك، تمكين `MaxDegreeOfParallelism` عالي على جهاز ذاكرة محدودة قد يسبب ارتفاعًا مفاجئًا. راقب الذاكرة RAM واضبط عدد الخيوط وفقًا لذلك.

## نصائح لتحسين الدقة

- **معالجة مسبقة للصور**: إزالة الضوضاء، تصحيح الميل، وتحويل إلى تدرج الرمادي قبل OCR. Aspose.OCR يقدم `ImagePreprocessOptions` يمكنك إرفاقه بـ `ocrBatchProcessor`.
- **اختر التنسيق المناسب**: إذا كنت تحتاج إلى الحفاظ على التخطيط، فإن `ResultFormat.Html` أو `Pdf` يحافظان على فواصل الأسطر والتنسيق الأساسي.
- **تحقق من النتائج**: نفّذ خطوة ما بعد المعالجة البسيطة التي تتحقق من وجود ملفات إخراج فارغة — غالبًا ما تشير إلى فشل التعرف.

## الخطوات التالية

الآن بعد أن أتقنت **معالجة OCR دفعيًا** لـ **استخراج النص من الصور**، قد ترغب في:

- **الدمج مع قاعدة بيانات** – احفظ كل نتيجة OCR مع البيانات الوصفية للبحث.
- **إضافة واجهة مستخدم** – أنشئ واجهة WPF أو WinForms صغيرة تسمح للمستخدمين بسحب وإفلات المجلدات.
- **التوسع** – شغّل المهمة الدفعية على Azure Functions أو AWS Lambda للمعالجة السحابية.

كل من هذه المواضيع يبني على نفس المفاهيم الأساسية التي غطيناها، لذا أنت في موقع جيد لتوسيع حلك.

**برمجة سعيدة!** إذا واجهت أي مشكلة أو لديك أفكار للتحسين، اترك تعليقًا أدناه. دعونا نستمر في النقاش لجعل أتمتة OCR أكثر سلاسة.

## ماذا يجب أن تتعلم بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة تعمل مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [كيفية معالجة صور OCR دفعيًا باستخدام قائمة في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [كيفية استخراج النص من أرشيفات ZIP باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}