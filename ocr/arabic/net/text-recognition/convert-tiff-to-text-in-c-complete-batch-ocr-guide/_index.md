---
category: general
date: 2026-05-25
description: تحويل ملفات TIFF إلى نص باستخدام Aspose.OCR في C#. تعلم تحويل الصور إلى
  نص على دفعات واستخراج النص من ملفات TIFF بكفاءة.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: ar
og_description: تحويل ملفات TIFF إلى نص باستخدام Aspose.OCR. يوضح هذا الدليل تحويل
  الصور إلى نص على دفعات وكيفية استخراج النص من ملفات TIFF ببضع أسطر من C#.
og_title: تحويل ملفات TIFF إلى نص في C# – دليل OCR كامل للمعالجة الدفعية
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: تحويل TIFF إلى نص في C# – دليل OCR كامل للدفعات
url: /ar/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل TIFF إلى نص في C# – دليل OCR دفعي كامل

هل احتجت يوماً إلى **تحويل TIFF إلى نص** ولكن لم تعرف من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون صعوبات مع OCR الدفعي عند التعامل مع المستندات الممسوحة. في هذا الدرس سنستعرض حلًا عمليًا **يستخرج النص من ملفات TIFF** باستخدام Aspose.OCR، وسنقوم بذلك بشكل متوازي بحيث تنتهي معالجة المجلدات الكبيرة في ثوانٍ.

سنتطرق أيضًا إلى أفضل الممارسات لـ **تحويل دفعة من الصور إلى نص**، حتى تحصل في النهاية على مقتطف قابل لإعادة الاستخدام يحول دليلًا كاملاً من الصور الممسوحة إلى ملفات *.txt* مرتبة—مثالي للفهرسة، البحث، أو إدخاله في تحليلات لاحقة.

## ما ستحتاجه

- **.NET 6.0** أو أحدث (الكود يُجمّع أيضًا على .NET Framework)  
- حزمة NuGet **Aspose.OCR for .NET** (`Install-Package Aspose.OCR`)  
- مجلد يحتوي على ملف أو أكثر بصيغة *.tif* (صيغة المسح الكلاسيكية TIFF)  
- بيئة التطوير المفضلة لديك (Visual Studio، VS Code، Rider—أيًا كان)

هذا كل شيء. لا خدمات خارجية، لا مفاتيح API، فقط C# صافية وAspose.

![لقطة شاشة لملف TIFF يتم معالجته والملف النصي الناتج](/images/ocr-result.png "نتيجة OCR تُظهر تحويل TIFF إلى نص")

*(نص بديل: لقطة شاشة تُظهر تحويل TIFF إلى نص على الشاشة)*

## الخطوة 1: إعداد محرك OCR – تحويل TIFF إلى نص

أولاً، نحتاج إلى إنشاء كائن `OcrEngine` يعرف أنه يجب قراءة الأحرف الإنجليزية. المحرك هو قلب عملية التحويل؛ ضبطه بشكل صحيح يضمن نتائج موثوقة.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*لماذا هذا مهم:*  
يدعم Aspose.OCR عشرات اللغات. إذا كنت تتعامل مع مسحات متعددة اللغات، ما عليك سوى تغيير `OcrLanguage.English` إلى القيمة المناسبة من الـ enum. ترك اللغة غير محددة يجعل المحرك يعمل في وضع الكشف التلقائي، مما قد يكون أبطأ وأقل دقة.

## الخطوة 2: جمع جميع ملفات TIFF – استخراج النص من TIFF بكفاءة

الآن نجلب كل ملف *.tif* من المجلد الذي تحدده. استخدام `Directory.GetFiles` يمنحنا مصفوفة نظيفة يمكن تمريرها إلى معالج الدفعة.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*نصيحة احترافية:* يمكن استخدام العلم `SearchOption.AllDirectories` إذا كانت مسحاتك متداخلة في مجلدات فرعية. فقط تذكر أن التعمق قد يزيد من استهلاك الذاكرة أثناء خطوة الدفعة.

## الخطوة 3: تنفيذ OCR المتوازي – تحويل دفعة من الصور إلى نص

الجزء الممتع الآن. يأتي Aspose.OCR بمساعد ثابت `BatchOcr.RecognizeAll` يقبل مصفوفة من مسارات الملفات، محركًا، وتلميح `parallelism`. سننشئ أربعة خيوط، وهو ما يمنح جهاز لابتوب رباعي النواة تسارعًا شبه خطي.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*لماذا التوازي؟*  
معالجة دفعة من ملفات TIFF عالية الدقة يمكن أن تكون مكثفة على المعالج. بتوزيع العمل على عدة خيوط نبقي جميع الأنوية مشغولة، مما يقلل زمن التنفيذ بشكل كبير. إذا نفذت هذا على خادم بعدد أكبر من الأنوية، زد قيمة `parallelism` وفقًا لذلك.

## الخطوة 4: كتابة المخرجات – تحويل الصور الممسوحة إلى ملفات TXT

أخيرًا نمر على القاموس ونكتب كل نص في ملف *.txt* يحمل نفس الاسم الأساسي الأصلي. هذه هي اللحظة التي يصبح فيها **convert scanned images txt** حقيقة واقعة.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### ما يفعله الكود، بلغة بسيطة

1. **إنشاء** محرك OCR مخصص للإنجليزية.  
2. **جمع** كل ملفات TIFF من المجلد المستهدف.  
3. **تشغيل** `BatchOcr.RecognizeAll` بأربعة خيوط، محولًا كل صورة إلى سلسلة نصية.  
4. **التكرار** على النتائج، استبدال امتداد `.tif` بـ `.txt` وكتابة السلسلة إلى القرص.

بهذا تكون قد أكملت سير عمل **convert TIFF to text** في أقل من 50 سطرًا من الكود.

## التعامل مع الحالات الخاصة – عندما لا تسير الأمور بسلاسة

- **ملفات TIFF مفقودة أو تالفة** – سيُطلق `BatchOcr` استثناءً من نوع `OcrException`. احيط الاستدعاء بـ `try / catch` إذا أردت معالجة الأخطاء برفق.  
- **مستندات غير إنجليزية** – غيّر `OcrLanguage.English` إلى `OcrLanguage.Spanish` أو `OcrLanguage.French`، إلخ، أو استخدم `OcrLanguage.AutoDetect`.  
- **صور كبيرة جدًا** – فكر في خفض DPI قبل OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) لتقليل استهلاك الذاكرة، مع احتمال فقدان بعض الدقة.  
- **ترميز الإخراج** – إذا كنت بحاجة إلى صفحة ترميز محددة (مثل Windows‑1252)، مرّرها إلى `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## نصائح احترافية لتحويلات دفعية قوية

- **سجّل الأخطاء**: أنشئ `List<string> failedFiles` وأضف أي ملف يسبب استثناء؛ اكتب القائمة إلى سجل بعد الحلقة.  
- **أعد استخدام المحرك**: يمكن إعادة استعمال نفس كائن `OcrEngine` عبر ملفات متعددة؛ لا تنشئه داخل الحلقة.  
- **تحقق من النتيجة**: فحص سريع `if (string.IsNullOrWhiteSpace(extractedText))` يمكنه اكتشاف المسحات الفارغة أو غير القابلة للقراءة.  
- **دمج مع PDF**: إذا كان المصدر PDF متعدد الصفحات، حوّل كل صفحة إلى TIFF أولاً (Aspose.PDF يقوم بذلك) ثم نفّذ هذه الدفعة.

## الخطوات التالية – تجاوز التحويل البسيط

الآن بعد أن أصبحت قادرًا على **استخراج النص من ملفات TIFF** دفعيًا، قد ترغب في:

- إدخال ملفات *.txt* في فهرس بحث (Elasticsearch، Azure Cognitive Search).  
- تشغيل كشف اللغة على كل نتيجة لتوجيه المستندات إلى خطوط معالجة مخصصة حسب اللغة.  
- إنشاء ملفات PDF قابلة للبحث عبر دمج نص OCR مرة أخرى فوق الصور الأصلية (Aspose.PDF مرة أخرى).  

جميع هذه السيناريوهات تبني على الفكرة الأساسية: **batch image to text conversion** هو حجر الأساس لأنظمة معالجة المستندات الأكبر.

---

### الخلاصة

لقد تعلمت الآن كيفية **تحويل TIFF إلى نص** باستخدام Aspose.OCR، معالجة مجلد كامل بشكل متوازي، وحفظ كل نتيجة كملف *.txt* نظيف. الحل خفيف، قابل للتكوين بالكامل، وجاهز للإنتاج—سواء كنت تقوم برقمنة فواتير قديمة، أرشفة عقود ممسوحة، أو تشغيل محرك بحث نصي.  

جرّبه، عدّل قيمة التوازي، وابدأ في تغذية تلك الملفات النصية الجديدة في أي سير عمل تحتاجه. نتمنى لك OCR موفق!

---

## دروس ذات صلة

- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)
- [استخراج نص الصورة في C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}