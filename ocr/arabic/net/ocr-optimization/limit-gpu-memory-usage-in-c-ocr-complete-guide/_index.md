---
category: general
date: 2026-05-02
description: قصر استهلاك ذاكرة GPU أثناء تشغيل OCR على صورة في C#. تعلم كيفية تمكين
  تسريع GPU، استخراج النص من الإيصال، وإتقان دليل OCR بلغة C#.
draft: false
keywords:
- limit gpu memory usage
- extract text from receipt
- how to enable gpu acceleration
- run OCR on image
- c# ocr tutorial
language: ar
og_description: تقليل استهلاك ذاكرة GPU أثناء تشغيل OCR على صورة في C#. يوضح هذا الدليل
  كيفية تمكين تسريع GPU، استخراج النص من الإيصال، وإتقان دليل OCR بلغة C#.
og_title: تحديد استخدام ذاكرة GPU في OCR باستخدام C# – دليل كامل
tags:
- Aspose OCR
- C#
- GPU acceleration
title: تقييد استخدام ذاكرة GPU في OCR باستخدام C# – دليل كامل
url: /ar/net/ocr-optimization/limit-gpu-memory-usage-in-c-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحديد حد استخدام ذاكرة GPU في C# OCR – دليل شامل

هل احتجت يومًا إلى **تحديد حد استخدام ذاكرة GPU** عند معالجة دفعة من الإيصالات؟ لست وحدك—غالبًا ما يواجه المطورون أخطاء نفاد الذاكرة عندما يُطلب من GPU التعامل مع عدد كبير من الصور في آنٍ واحد. الخبر السار هو أن Aspose.OCR يتيح لك تحديد حجم الذاكرة **وبالإضافة إلى ذلك** تشغيل تسريع GPU بسطر واحد من الشيفرة.

في هذا الدرس سنستعرض حلًا عمليًا خطوة بخطوة يوضح **كيفية تمكين تسريع GPU**، استخراج النص من صورة إيصال نموذجية، والحفاظ على استهلاك ذاكرة GPU تحت 1 جيجابايت منظم. في النهاية ستحصل على تطبيق C# Console جاهز للتنفيذ، بالإضافة إلى مجموعة من النصائح التي يمكنك إعادة استخدامها في أي سيناريو **run OCR on image**.

## ما الذي ستحتاجه

- .NET 6.0 SDK أو أحدث (الشيفرة تُجمّع أيضًا مع .NET 5+)  
- حزمة NuGet الخاصة بـ Aspose.OCR for .NET (`Aspose.OCR`) – تثبيت عبر `dotnet add package Aspose.OCR`  
- GPU يدعم CUDA أو جهاز Windows متوافق مع DirectML  
- صورة إيصال مثال (`receipt.jpg`) موجودة في مجلد يمكنك الإشارة إليه  

هذا كل ما تحتاجه—بدون مكتبات أصلية إضافية، ولا نسخ معقدة من DLLs. Aspose يخفف عنك تفاصيل الـ GPU، لتتمكن من التركيز على منطق عملك.

## الخطوة 1: تثبيت حزمة NuGet الخاصة بـ Aspose.OCR

أولًا، افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

هذا سيجلب أحدث نسخة مستقرة (حتى مايو 2026 النسخة هي 23.11). الحزمة تتضمن كل من ملفات الـ CPU وGPU، لذا لا تحتاج إلى تحميل CUDA أو DirectML يدويًا—Aspose يكتشف المتاح أثناء التشغيل.

> **نصيحة احترافية:** إذا كنت تستهدف خط أنابيب CI/CD، قم بتثبيت النسخة في ملف `.csproj` لتجنب الترقيات المفاجئة.

## الخطوة 2: إنشاء محرك OCR و**تحديد حد استخدام ذاكرة GPU**

الآن سننشئ كائن `OcrEngine` ونخبره صراحةً بعدم تجاوز 1 جيجابايت من ذاكرة GPU. هذا هو جوهر مطلب **limit GPU memory usage**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

public class GpuExample
{
    public static void Run()
    {
        // Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU mode – Aspose auto‑detects CUDA or DirectML
        ocrEngine.Settings.Engine = EngineMode.Gpu;

        // 👉 Limit GPU memory usage to 1024 MB (1 GB)
        ocrEngine.Settings.GpuMemoryLimitMb = 1024;

        // Load the receipt image and run OCR
        var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

        // Output the plain‑text result
        Console.WriteLine(result.Text);
    }
}
```

لاحظ التعليق `// 👉 Limit GPU memory usage…`—هذا السطر هو الجواب على الكلمة المفتاحية الأساسية. عبر ضبط `GpuMemoryLimitMb` تخبر محرك الاستدلال الأساسي بأن يخصص أقصى حجم محدد، مما يسمح بوجود مهام متزامنة متعددة دون استنزاف GPU.

## الخطوة 3: **كيفية تمكين تسريع GPU** (ولماذا هو مهم)

قد تتساءل، “لماذا لا أكتفي بالـ CPU فقط؟” الجواب هو السرعة. على بطاقة RTX 3080 الحديثة، يتم معالجة نفس الإيصال في أقل من 200 مللي ثانية مقابل 1.2 ثانية على معالج رباعي النوى.

تمكين تسريع GPU بسيط كقلب مفتاح `EngineMode`:

```csharp
ocrEngine.Settings.Engine = EngineMode.Gpu;
```

Aspose يختار الخلفية الأنسب تلقائيًا:

| الخلفية المكتشفة | ما تقوم به |
|------------------|------------|
| CUDA (NVIDIA)    | يستخدم نوى cuDNN للـ OCR، الأفضل لنظام Windows/Linux مع بطاقات NVIDIA |
| DirectML (Windows) | يستفيد من DirectX 12، يعمل على بطاقات AMD/Intel دون الحاجة إلى تعريفات إضافية |
| None (fallback)  | يعود إلى مسار CPU المحسّن |

إذا لم يتوفر CUDA ولا DirectML، يعود المحرك بهدوء إلى CPU—بدون تعطل، فقط بأداء أبطأ.

## الخطوة 4: **Run OCR on image** و**استخراج النص من الإيصال**

مع تكوين المحرك، يصبح تمرير الصورة أمرًا بسيطًا. طريقة `RecognizeImage` تقبل مسار ملف، أو `Stream`، أو حتى `Bitmap`. إليك الحد الأدنى من الاستدعاء:

```csharp
var result = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

بافتراض أن الإيصال يحتوي على:

```
Store XYZ
Date: 2026-04-30
Total: $23.45
```

يجب أن ترى مخرجات مشابهة لـ:

```
=== OCR Output ===
Store XYZ
Date: 2026-04-30
Total: $23.45
```

إذا ظهر النص مشوشًا، تأكد من أن الصورة ذات تباين عالي وموجهة بشكل صحيح—OCR يفضّل المسحات النظيفة.

## الخطوة 5: التحقق من حدود الذاكرة ومعالجة الحالات الخاصة

بعد التشغيل الأول، يمكنك الاستعلام عن مقدار ذاكرة GPU التي استخدمها المحرك فعليًا:

```csharp
Console.WriteLine($"GPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
```

إذا كنت تخطط لمعالجة عشرات الإيصالات بالتوازي، قد ترغب في خفض الحد إلى 512 ميجابايت وتشغيل عدة نسخ من المحرك. فقط تذكر أن كل نسخة تحترم الحد العالمي نفسه؛ المكتبة ستقيد التخصيصات تلقائيًا.

> **خطأ شائع:** ضبط الحد منخفضًا جدًا (مثلاً 100 ميجابايت) قد يجعل المحرك ينتقل إلى CPU أثناء التنفيذ، مما يسبب أداء غير متسق. اختبر مع حمل عملي قبل تثبيت القيمة.

## مثال كامل جاهز للعمل

فيما يلي برنامج Console كامل جاهز للنسخ واللصق. استبدل `YOUR_DIRECTORY` بالمسار الفعلي لصورة الإيصال الخاصة بك.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step‑by‑step demo
            GpuExample.Run();

            // Keep console window open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }

    class GpuExample
    {
        public static void Run()
        {
            // 1️⃣ Create OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable GPU acceleration (auto‑detects CUDA or DirectML)
            ocrEngine.Settings.Engine = EngineMode.Gpu;

            // 3️⃣ Limit GPU memory usage to 1 GB for concurrent jobs
            ocrEngine.Settings.GpuMemoryLimitMb = 1024;

            // 4️⃣ Load the image and run OCR
            var recognitionResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/receipt.jpg");

            // 5️⃣ Output the recognized plain‑text
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognitionResult.Text);

            // 6️⃣ Optional: Show how much GPU memory was actually used
            Console.WriteLine($"\nGPU memory used: {ocrEngine.Settings.GpuMemoryUsedMb} MB");
        }
    }
}
```

احفظ الملف، شغّل `dotnet run`، وسترى النص المستخرج من الإيصال يُطبع على الشاشة، مع تقرير صغير عن استهلاك ذاكرة GPU.

## استكشاف الأخطاء وإجابات الأسئلة الشائعة

**س: GPU الخاص بي غير مكتشف—لماذا؟**  
ج: تأكد من تثبيت أحدث تعريف NVIDIA (لـ CUDA) أو Windows 10 1809+ (لـ DirectML). كما يجب التحقق من أن ملفات DLL الخاصة بـ `Aspose.OCR` تتطابق مع بنية العملية (يفضل x64).

**س: المخرجات فارغة.**  
ج: افحص جودة الصورة—الإيصالات الضبابية أو المائلة غالبًا ما تحتاج إلى معالجة مسبقة (تصحيح الميل، تحويل إلى ثنائي). Aspose يوفر `ImagePreprocessor` يمكنك ربطه قبل `RecognizeImage`.

**س: هل يمكن تشغيل هذا على Linux؟**  
ج: نعم، طالما لديك GPU NVIDIA مع CUDA 11+ مثبت. الشيفرة نفسها تعمل دون تعديل.

## الخلاصة

غطّينا كل ما تحتاجه لت **limit GPU memory usage** أثناء **run OCR on image** باستخدام Aspose.OCR في C#. من تثبيت حزمة NuGet إلى تكوين المحرك، تمكين تسريع GPU، وأخيرًا **استخراج النص من الإيصال**، يقدم الدليل حلًا جاهزًا يكون صديقًا للذاكرة وسريعًا للغاية.

بعد ذلك، يمكنك استكشاف مواضيع **c# OCR tutorial** أكثر تقدمًا—مثل المعالجة الدفعية، حزم اللغات المخصصة، أو دمج النتائج في قاعدة بيانات. جرّب قيم مختلفة لـ `GpuMemoryLimitMb` لتجد الإعداد المثالي لحمل عملك، وراقب تشخيص استهلاك الذاكرة لتجنب المفاجآت.

برمجة سعيدة، ولتظل بطاقتك الرسومية باردة بينما يبقى OCR حادًا!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}