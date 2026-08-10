---
category: general
date: 2026-06-25
description: يظهر دليل معالجة OCR الدفعي كيفية تحويل الصور إلى نص واستخراج النص من
  الصور باستخدام Aspose.OCR في C#. تعلم التنفيذ خطوة بخطوة.
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: ar
og_description: تتيح لك معالجة OCR الدفعية في C# تحويل الصور إلى نص بسرعة. اتبع هذا
  الدليل لتتعلم كيفية استخراج النص من الصور باستخدام Aspose.OCR.
og_title: معالجة OCR دفعة في C# – تحويل الصور إلى نص
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: معالجة OCR دفعيًا في C# – تحويل الصور إلى نص بسرعة
url: /ar/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# معالجة OCR دفعة في C# – تحويل الصور إلى نص بسرعة

هل تساءلت يومًا كيف تقوم بـ **معالجة OCR دفعة** لمجلد كامل من المسحات دون كتابة حلقة منفصلة لكل ملف؟ لست وحدك. في العديد من المشاريع—مثل أتمتة الفواتير، أرشفة المستندات القديمة، أو حتى أداة بسيطة لتحويل الصور إلى نص شخصيًا—تحتاج إلى **تحويل الصور إلى نص** على نطاق واسع.  

الأخبار السارة؟ مع Aspose.OCR يمكنك فعل ذلك في بضع أسطر فقط. يشرح هذا الدليل مثالًا كاملاً وجاهزًا للتنفيذ يوضح **كيفية استخراج النص من الصور** باستخدام معالجة OCR دفعة، ويشرح لماذا كل جزء مهم، ويعطيك نصائح لتجنب المشكلات الشائعة.

## ما ستتعلمه

- إعداد Aspose.OCR للعمليات الدفعية.
- تهيئة التوازي لتسريع المهام الكبيرة.
- كتابة نتائج OCR إلى ملفات `.txt` فردية تلقائيًا.
- معالجة أحداث التقدم لتعرف دائمًا ما يحدث.
- توسيع الكود لمعالجة الأخطاء المخصصة أو صيغ إخراج مختلفة.

لا يلزم أي خبرة سابقة مع Aspose؛ فقط خلفية أساسية في C# و .NET 6 (أو أحدث) مثبتة.

---

## الخطوة 1: إعداد مشروعك لمعالجة OCR دفعة

قبل أن نغوص في الكود، تأكد من أن لديك حزمة Aspose.OCR NuGet. افتح طرفية في مجلد مشروعك وشغّل:

```bash
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** استخدم أحدث نسخة مستقرة (اعتبارًا من يونيو 2026 هي 23.9) للحصول على تحسينات الأداء وأحدث دعم للغات.

أنشئ تطبيقًا جديدًا من نوع console إذا لم يكن لديك واحد بالفعل:

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

الآن أنت جاهز لكتابة منطق معالجة OCR دفعة الفعلي.

## الخطوة 2: تحديد ملفات الصور التي تريد تحويلها

الجزء الأول من **معالجة OCR دفعة** هو ببساطة إخبار المعرّف بأي الملفات يجب معالجتها. يمكنك كتابة قائمة ثابتة، أو القراءة من دليل، أو حتى سحب المسارات من قاعدة بيانات. للتوضيح سنستخدم قائمة ثابتة:

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **لماذا هذا مهم:** بتمرير مجموعة، يمكن لـ `BatchRecognizer` جدولة العمل داخليًا عبر عدة خيوط، وهو جوهر عمليات **تحويل الصور إلى نص** السريعة.

## الخطوة 3: إنشاء وتكوين BatchRecognizer

الآن يأتي قلب الدرس. فئة `BatchRecognizer` تُجرد تفاصيل الخيوط لك. يمكنك تعديل خاصية `Parallelism` لتتناسب مع عدد نوى المعالج لديك أو قيمة مخصصة إذا أردت ترك بعض النوى حرة لأعمال أخرى.

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **شرح:** ضبط `Parallelism = 4` يخبر المكتبة بتشغيل أربع مهام OCR في آن واحد. على حاسوب محمول رباعي النوى عادي، يمنحك ذلك زيادة سرعة جيدة دون إشباع النظام. إذا كنت تعمل على خادم بعدد كبير من النوى، زد هذا الرقم.

> **حالة حافة:** إذا كنت تعالج صورًا ضخمة جدًا، قد تواجه حدود الذاكرة. في هذه الحالة، قلل من التوازي أو عالج الملفات على دفعات أصغر.

## الخطوة 4: تشغيل OCR وجمع النتائج

استدعاء `Recognize` على `BatchRecognizer` يُعيد قاموسًا حيث المفتاح هو مسار الملف الأصلي والقيمة هي `OcrResult` تحتوي على النص المستخرج، درجات الثقة، وأكثر.

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **ما ستحصل عليه:** لكل صورة، يحتوي `OcrResult.Text` على تمثيل النص العادي. هذا هو بالضبط ما تحتاجه عندما تريد **كيفية استخراج النص من الصور** بطريقة برمجية.

## الخطوة 5: حفظ كل نتيجة في ملف .txt

معظم السيناريوهات الواقعية تتطلب حفظ مخرجات OCR للمعالجة لاحقًا—ربما إدخالها في فهرس بحث أو إرفاقها بسجل قاعدة بيانات. الحلقة التالية تكتب ملف `.txt` بجوار كل صورة مصدر، مع الحفاظ على اسم الملف الأصلي.

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **نصيحة:** إذا كنت تحتاج إلى صيغة مختلفة (JSON، CSV، إلخ)، ببساطة قم بتسلسل `entry.Value` كما تشاء. كائن `OcrResult` يتيح أيضًا `Confidence` و `PageCount` إذا كانت هذه المقاييس مفيدة لك.

## الخطوة 6: الإشارة إلى الانتهاء ومعالجة الأخطاء بلطف

إنهاء نظيف يجعل أداتك تبدو مصقولة. الكود النموذجي يطبع سطرًا نهائيًا بالفعل، لكن دعنا نضيف كتلة try‑catch لتظهر أي استثناءات غير متوقعة، مثل الملفات المفقودة أو صيغ الصور غير المدعومة.

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **لماذا نغلفه:** عند تشغيل البرنامج على مجلد كبير، قد يتسبب صورة واحدة تالفة في إلغاء المهمة بالكامل. مع معالجة الأخطاء بشكل صحيح يمكنك تسجيل المشكلة والاستمرار مع الملفات المتبقية.

## مثال كامل وجاهز للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في `Program.cs`. تأكد من أن مسارات الصور تشير إلى ملفات حقيقية على جهازك.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل `dotnet run`، سترى شيئًا مثل:

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

كل ملف `.txt` الآن يحتوي على النسخة النصية العادية لصورته المقابلة—بالضبط ما تحتاجه **لتحويل الصور إلى نص** على نطاق واسع.

---

## الأسئلة المتكررة وحالات الحافة

### ما صيغ الصور المدعومة؟

يتعامل Aspose.OCR مع JPEG، PNG، TIFF، BMP، و GIF مباشرة. إذا صادفت صيغة مثل WebP، قم بتحويلها أولاً أو استخدم محولًا من طرف ثالث.

### هل يمكنني تحديد لغة OCR إلى الإنجليزية فقط؟

نعم. اضبط خاصية `Language` على `BatchRecognizer` قبل استدعاء `Recognize`:

```csharp
ocrBatch.Language = "en";
```

تحديد اللغة يمكن أن يحسن الدقة والسرعة، خاصةً عندما تكون مهتمًا فقط **كيفية استخراج النص من الصور** بلغة واحدة.

### كيف أعالج آلاف الملفات دون استهلاك الذاكرة؟

قسم القائمة إلى دفعات أصغر (مثلاً 500 ملف لكل دفعة) وشغّل الروتين أعلاه داخل حلقة. هذا يحافظ على القاموس في الذاكرة بحجم قابل للإدارة ويسمح لك بتسجيل التقدم لكل دفعة.

### ماذا لو كنت أحتاج نتائج OCR في قاعدة بيانات بدلاً من ملفات؟

استبدل استدعاء `File.WriteAllText` بكود الوصول إلى البيانات المفضل لديك. على سبيل المثال، باستخدام Dapper:

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

---

## الخلاصة

لقد أتقنت الآن **معالجة OCR دفعة** في C# باستخدام Aspose.OCR، وتعلمت طريقة نظيفة **لتحويل الصور إلى نص**، واكتشفت عدة نصائح عملية **كيفية استخراج النص من الصور** بفعالية. سير العمل الكامل—جمع مسارات الملفات، تكوين `BatchRecognizer`، تشغيل OCR، وحفظ النتائج—يتضمن برنامجًا واحدًا سهل القراءة.

ما التالي؟ جرّب زيادة `Parallelism` على خادم متعدد النوى، جرب حزم اللغات، أو أضف معالجة لاحقة مثل التدقيق الإملائي. يمكنك أيضًا استكشاف إدخال النص المستخرج إلى Azure Cognitive Search لجعل مستنداتك الممسوحة قابلة للبحث في ثوانٍ.

هل لديك تعديل ترغب في مشاركته—ربما OCR لملفات PDF أو معالجة TIFF متعددة الصفحات؟ اترك تعليقًا أدناه، ولنستمر في النقاش. برمجة سعيدة!

---

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات الموضحة في هذا الدليل. كل مورد يتضمن أمثلة كود كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [كيفية معالجة صور OCR دفعة باستخدام قائمة في Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [كيفية استخراج النص من أرشيفات ZIP باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}