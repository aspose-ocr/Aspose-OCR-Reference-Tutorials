---
category: general
date: 2026-01-12
description: دليل C# OCR يوضح لك كيفية التعرف على صورة نصية، استخراج النص من الصورة
  باستخدام C# وإنشاء ملف OCR من صورة إلى PDF مع درجات الثقة.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: ar
og_description: تعلم دورة شاملة في OCR باستخدام C# للتعرف على النص في الصور، استخراج
  النص من الصور باستخدام C# وإنشاء مستند OCR من صورة إلى PDF مع درجات الثقة.
og_title: دليل C# OCR – تحويل الصور إلى ملفات PDF قابلة للبحث
tags:
- OCR
- C#
- PDF
title: دروس OCR بلغة C# – تحويل الصور إلى ملفات PDF قابلة للبحث
url: /ar/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# دليل c# ocr – تحويل الصور إلى ملفات PDF قابلة للبحث

هل تساءلت يومًا كيف **recognize text image** الملفات في مشروع C# دون البحث عن خدمات طرف ثالث؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، متتبعات الإيصالات، أو أرشيف المستندات متعددة اللغات—يحتاج المطورون إلى محرك OCR موثوق يعمل محليًا ويعطي أيضًا درجات الثقة.  

هذا **c# ocr tutorial** سيقودك خطوة بخطوة عبر كل ما تحتاجه: من تحميل الصورة، اختيار نماذج اللغات، تشغيل تسريع GPU، إلى حفظ النتيجة كملف PDF قابل للبحث. في النهاية ستحصل على عينة كود جاهزة للتنفيذ تستخرج النص، تُظهر ثقة OCR، وتُنشئ اختياريًا ملف *image to pdf ocr*—كل ذلك في أقل من دقيقة من البرمجة.

## ما ستبنيه

- تحميل صورة متعددة اللغات (`sample_multi_lang.jpg` تُستخدم كعنصر نائب).  
- اختيار نماذج اللغة العربية، الهندية، والروسية (يمكنك إضافة المزيد).  
- تشغيل معالجة GPU إذا كان جهازك يدعمها.  
- الحصول على نتيجة OCR الخام **with confidence scores**.  
- تسلسل النتيجة إلى JSON منسق **or** كتابة ملف PDF قابل للبحث.  

لا خدمات ويب خارجية، لا سحر مخفي—فقط Aspose.OCR for .NET، بضع أسطر من C#، وتوضيح واضح **why** كل سطر مهم.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يُجمع على .NET Core و .NET Framework).  
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها).  
- رخصة Aspose.OCR for .NET (الإصدار التجريبي المجاني يكفي للاختبار).  
- اختياري: GPU متوافق مع CUDA إذا أردت تسريع التعرف.

> **Pro tip:** إذا لم يكن لديك GPU، فقط اضبط `UseGpu = false` وستعود المحرك إلى CPU دون أي تغييرات في الكود.

## الخطوة 1: تثبيت حزم NuGet المطلوبة

افتح **Package Manager Console** وشغّل:

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

هذه الحزم الثلاث توفر لك محرك OCR، تسريع GPU، ومُسلسل JSON جميل لإخراج الثقة.

## الخطوة 2: إعداد هيكل المشروع

أنشئ مشروع console جديد (`dotnet new console -n AsposeOcrDemo`) واستبدل ملف `Program.cs` المُولَّد بالكود أدناه.  
كل المنطق موجود داخل فئة `Program`؛ النوع الإضافي الوحيد هو طريقة امتداد صغيرة تُنسق نتيجة OCR إلى JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### لماذا يعمل هذا الكود

1. **GPU toggle** – `GpuOcrEngine` يستخدم نوى CUDA؛ عامل الشرط الثلاثي يجعل التبديل سهلًا.  
2. **Automatic language download** – `AutoDownloadResources = true` يضمن تحميل نماذج العربية، الهندية، والروسية في المرة الأولى التي تشغّل فيها التطبيق.  
3. **Confidence scores** – `result.Words` يحتوي على `Confidence` لكل كلمة مُعترف بها؛ طريقة الامتداد تُنسقها إلى كائن JSON نظيف.  
4. **Searchable PDF** – `result.Pdf` هو بالفعل PDF قابل للبحث بالكامل، لذا نكتب مصفوفة البايتات إلى القرص. لا حاجة لمكتبات إضافية.

## الخطوة 6: تشغيل العينة

افتح طرفية، انتقل إلى مجلد المشروع، ونفّذ:

```bash
dotnet run
```

إذا اخترت إخراج **JSON**، ستظهر لك نتيجة مشابهة لـ:

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

إذا تحولت إلى **PDF**، سيطبع الطرفية المسار وستجد ملف PDF قابل للبحث بجوار صورة المصدر.

## الأسئلة الشائعة وحالات الاستخدام الخاصة

- **What if a language model isn’t available?**  
  محرك OCR يرمي استثناء واضح `ResourceNotFoundException`. لأننا ضبطنا `AutoDownloadResources = true`، يتم تحميل النموذج المفقود تلقائيًا في المرة الأولى، لذا نادرًا ما يظهر الاستثناء في بيئة الإنتاج.

- **Can I process a batch of images?**  
  بالتأكيد. غلف استدعاء `engine.Recognize` داخل حلقة `foreach` على دليل يحتوي على ملفات. طريقة `OcrResultExtensions` نفسها تعمل مع كل صورة.

- **Do I need a license for GPU?**  
  لا. الإصدار التجريبي المجاني يعمل مع كل من CPU وGPU. الرخصة الكاملة تُزيل علامة التجربة وتُزيل قيود عدد الصفحات.

- **How accurate are the confidence scores?**  
  تتراوح الدرجات من 0.0 (لا ثقة) إلى 1.0 (ثقة كاملة). عمليًا، أي قيمة فوق 0.90 تُعد موثوقة للمعالجة اللاحقة؛ يمكنك تصفية الكلمات ذات الثقة الأقل إذا احتجت إلى تحقق أكثر صرامة.

## الخطوة 7: الخطوات التالية (توسيع مجموعة أدوات OCR الخاصة بك)

1. **Add more languages** – فقط أضف `LanguageModel.French` (أو أي نموذج مدعوم) إلى مصفوفة `Languages`.  
2. **Combine OCR with PDF/A conversion** – Aspose.PDF يمكنه دمج طبقة OCR داخل مستند PDF/A‑2b متوافق للأرشفة.  
3. **Integrate with Azure Functions** – غلف المنطق في نقطة نهاية serverless لمعالجة التحميلات فورًا.  
4. **Fine‑tune confidence thresholds** – استخدم `result.Words.Where(w => w.Confidence < 0.85)` لتعليم الكلمات غير المؤكدة للمراجعة اليدوية.

---

### ملخص سريع

هذا **c# ocr tutorial** يُظهر لك كيف:

- تحميل صورة واختيار نماذج لغات متعددة.  
- تشغيل تسريع GPU بعلم منطقي واحد.  
- استرجاع نتائج OCR **with confidence scores** وتسلسلها إلى JSON.  
- كتابة ملف PDF قابل للبحث اختياريًا (**image to pdf ocr**).  

كل ذلك ممكن باستخدام بضع أسطر فقط، نسخة تجريبية مجانية من Aspose.OCR، والكود أعلاه. جرّبه، عدّل قائمة اللغات، وستحصل على خط أنابيب OCR جاهز للإنتاج في دقائق.

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}