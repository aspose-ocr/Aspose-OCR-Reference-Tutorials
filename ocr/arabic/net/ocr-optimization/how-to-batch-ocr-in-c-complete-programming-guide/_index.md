---
category: general
date: 2026-03-13
description: كيفية تنفيذ التعرف الضوئي على الحروف (OCR) دفعةً بسرعة وموثوقية مع تعلم
  استخراج النص من ملفات TIFF باستخدام Aspose.OCR. اتبع هذا الدليل خطوة بخطوة.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: ar
og_description: تعلم كيفية تنفيذ OCR دفعيًا في C# واستخراج النص من ملفات TIFF باستخدام
  Aspose.OCR. يغطي هذا الدليل الإعداد، الكود، ونصائح أفضل الممارسات.
og_title: كيفية تنفيذ OCR على دفعات في C# – دليل البرمجة الكامل
tags:
- OCR
- C#
- Aspose
- Batch processing
title: كيفية تنفيذ OCR على دفعات في C# – دليل برمجة شامل
url: /ar/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR دفعيًا في C# – دليل برمجة كامل

هل تساءلت يومًا **كيف تقوم بعمل OCR دفعي** لجبال من الفواتير الممسوحة ضوئيًا دون كتابة سكريبت منفصل لكل ملف؟ لست وحدك. في العديد من المشاريع الواقعية، ليست مشكلة دقة OCR هي النقطة المؤلمة بل حجم الصور الهائل—غالبًا ما تكون ملفات TIFF—التي تحتاج إلى تحويلها إلى نص قابل للبحث.  

هذا الدرس يوضح لك **كيف تقوم بعمل OCR دفعي** باستخدام `BatchProcessor` من Aspose.OCR بينما يعلمك أيضًا **كيفية استخراج النص من tiff** في تشغيل واحد نظيف. في النهاية ستحصل على تطبيق console جاهز للتشغيل يعالج مجلدًا كاملاً، يستفيد من تسريع GPU اختياريًا، ويضع نتائج النص العادي أينما تحتاجها.

## ما ستحتاجه

- **.NET 6+** (أو .NET Framework 4.7.2 إذا كنت تفضل بيئة التشغيل الكلاسيكية)  
- **Aspose.OCR for .NET** – يمكنك الحصول على حزمة NuGet باستخدام `dotnet add package Aspose.OCR`.  
- مجلد يحتوي على صور **TIFF** التي تريد قراءتها (يستخدم الدرس مثال `Invoices`).  
- اختياري: وحدة معالجة رسومية (GPU) تدعم DirectX 11 أو CUDA إذا أردت تسريع العملية.  

لا خدمات إضافية، لا مفاتيح سحابية—فقط مشروع C# محلي ومكتبة Aspose.

## الخطوة 1: إعداد المشروع وتثبيت Aspose.OCR

أولاً، أنشئ تطبيقًا من نوع console.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Windows وتخطط لاستخدام تسريع GPU، تأكد من تثبيت أحدث برنامج تشغيل للرسومات. وإلا فإن علامة `UseGpu = true` ستعود تلقائيًا إلى المعالج المركزي (CPU).

## الخطوة 2: إنشاء إعدادات BatchProcessor

الآن سنقوم بإعداد `BatchProcessor`. هذا هو جوهر **كيفية تنفيذ OCR دفعي**—تخبر Aspose ما اللغة المتوقعة، أي فلاتر ما قبل المعالجة يجب تطبيقها، وما إذا كنت تريد الاستفادة من GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**لماذا هذه الإعدادات؟**  
- `Language = Language.English` يخبر المحرك باستخدام نموذج اللغة الإنجليزية، وهو أكثر دقة بكثير من النموذج العام.  
- `UseGpu` يمكنه تقليل وقت المعالجة إلى النصف على GPU جيد، لكن من الآمن تركه `false` إذا كنت تستخدم لابتوب بدون GPU.  
- خط أنابيب الفلاتر يعكس ما يفعله الإنسان: تصحيح استقامة الصفحة وتنظيف البقع قبل تمريرها إلى محرك OCR.

## الخطوة 3: توجيه المعالج إلى مجلد TIFF الخاص بك

الجزء التالي من **كيفية تنفيذ OCR دفعي** هو إخبار المكتبة بمكان وجود ملفات المصدر. يتم دعم الأحرف البدل، لذا يمكنك التقاط كل ملف `.tif` مرة واحدة.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **حالة حافة:** إذا كانت صورك ذات امتدادات مختلطة (`.tiff`, `.tif`, `.png`)، استدعِ `AddFolder` عدة مرات أو استخدم `*.*` ثم صَفِّها لاحقًا في الكود.

## الخطوة 4: اختيار مكان حفظ نتائج OCR

قد تتساءل، “أين ينتهي النص المستخرج؟” هذا هو الركن الثالث من **كيفية تنفيذ OCR دفعي**—تحديد موقع الإخراج والصيغة. سنخزن ملفات النص العادي جنبًا إلى جنب مع الأصليين.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

إذا كنت تحتاج إلى JSON أو XML بدلاً من النص العادي، فقط استبدل `OutputFormat.PlainText` بـ `OutputFormat.Json` أو `OutputFormat.Xml`. المكتبة تتولى التحويل لك.

## الخطوة 5: تشغيل مهمة الدفعة وتقرير النتائج

أخيرًا، شغّل المهمة. طريقة `Execute` تحجب التنفيذ حتى يتم معالجة كل ملف، ثم يمكنك فحص `ProcessedCount` لتأكيد النجاح.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### النتيجة المتوقعة

عند تشغيل البرنامج، سيطبع الـ console شيئًا مثل:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

في مجلد `Output` ستجد ملف `.txt` واحد لكل TIFF مصدر، كل ملف مسمى بعد الصورة الأصلية (مثال: `Invoice_001.txt`). افتح أي ملف وسترى النص الخام من OCR—مثالي لتغذيته إلى فهرس بحث أو خط أنابيب استخراج بيانات لاحق.

## معالجة المشكلات الشائعة

### 1. عدم توفر GPU

إذا كان `UseGpu = true` ولكن لا يُعثر على جهاز متوافق، فإن Aspose يعود إلى CPU بصمت. لتكون صريحًا، يمكنك التقاط الاستثناء `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. ملفات غير TIFF في نفس المجلد

عند وجود مجلد مختلط، صَفِّ برمجيًا:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. ملفات كبيرة تتجاوز الذاكرة

للـ TIFF متعددة الصفحات الضخمة، فعّل البث:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## نصائح احترافية لتحسين الدقة عند **استخراج النص من tiff**

- **الدقة مهمة** – استهدف 300 dpi أو أعلى. أقل من ذلك قد يتخطى محرك OCR بعض الأحرف.  
- **اللون مقابل التدرج الرمادي** – حوّل المسحات الضوئية الملونة إلى تدرج رمادي قبل OCR؛ فـ `DeskewFilter` يقوم بذلك بالفعل، لكن يمكنك إضافة `ColorDepthReductionFilter` لزيادة السرعة.  
- **معالجة ما بعد** – بعد الحصول على النص العادي، نفّذ تدقيق إملائي أو تنظيف باستخدام regex لإصلاح الأخطاء الشائعة في OCR (مثل “0” مقابل “O”).

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله. فقط استبدل مسارات العناصر النائبة بأدلةك الخاصة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

تجميع وتشغيل:

```bash
dotnet run
```

يجب الآن أن يكون لديك مجموعة مرتبة من ملفات `.txt`—كل منها نتيجة **استخراج النص من tiff** عبر عملية دفعية مؤتمتة بالكامل.

## الخلاصة

لقد استعرضنا **كيفية تنفيذ OCR دفعي** في C# من البداية إلى النهاية، مغطين كل ما تحتاجه **لاستخراج النص من tiff** بكفاءة. النقاط الرئيسية هي:

1. استخدم `BatchProcessor` من Aspose.OCR لتجنب كتابة حلقات متكررة.  
2. استفد من فلاتر ما قبل المعالجة (تصحيح الاستقامة، إزالة البقع) للحصول على دقة أعلى.  
3. فعّل تسريع GPU عندما يكون متاحًا، لكن احرص دائمًا على وجود بديل CPU.  
4. احفظ النتائج في بنية مجلدات متوقعة حتى تتمكن الوظائف اللاحقة من التقاطها تلقائيًا.

من هنا قد تستكشف:

- إدخال النص العادي في **فهرس بحث** (مثل Elasticsearch) لجعل الفواتير قابلة للبحث.  
- تحويل المخرجات إلى **JSON** وإدخالها إلى نموذج تعلم آلي يستخرج بنود الفاتورة.  
- إضافة **معالجة أخطاء** للملفات TIFF التالفة أو مشاكل الأذونات.

جرّبه،

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}