---
category: general
date: 2026-02-11
description: تعلم كيفية تنفيذ التعرف الضوئي على الحروف (OCR) على الصورة باستخدام GPU
  OCR في C#. يغطي هذا الدليل خطوة بخطوة الإعداد، الكود، وأفضل الممارسات.
draft: false
keywords:
- perform OCR on image
- use GPU OCR
- Aspose OCR C#
- GPU acceleration OCR
- OCR performance tuning
language: ar
og_description: قم بتنفيذ التعرف الضوئي على الأحرف (OCR) على الصورة باستخدام GPU OCR
  في C#. اتبع هذا الدليل للحصول على حل سريع وموثوق مع Aspose OCR.
og_title: إجراء التعرف الضوئي على الحروف في الصورة باستخدام وحدة معالجة الرسومات –
  تنفيذ كامل بلغة C#
tags:
- OCR
- C#
- Aspose
- GPU Computing
title: إجراء التعرف الضوئي على الأحرف في الصورة باستخدام تسريع GPU – دليل C# الكامل
url: /ar/net/ocr-optimization/perform-ocr-on-image-with-gpu-acceleration-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# إجراء التعرف الضوئي على الحروف (OCR) على الصورة باستخدام تسريع GPU – دليل C# كامل

هل احتجت يومًا إلى **perform OCR on image** لكن معالجك كان يواجه صعوبة مع ملفات TIFF الضخمة؟ لست وحدك. في العديد من المشاريع الواقعية، يمكن أن يتحول معالجة المستندات الكبيرة من بضع ثوانٍ إلى دقائق، وهذا البطء يؤثر سلبًا على كل من المستخدمين والميزانيات.  

الأخبار السارة؟ باستخدام GPU يمكنك تقليل أوقات المعالجة بشكل كبير. في هذا الدرس سنستعرض مثالًا عمليًا يوضح بالضبط **how to perform OCR on image** باستخدام محرك Aspose المدعوم بـ GPU، بالإضافة إلى مجموعة من النصائح العملية التي لن تجدها في الوثائق العامة.

> **ما ستحصل عليه:** تطبيق C# Console جاهز للتشغيل، شرح لكل سطر، وإرشادات لحل المشكلات الشائعة. لا حاجة لمراجع خارجية—كل ما تحتاجه موجود هنا.

## ما ستحتاجه

قبل أن نبدأ، تأكد من تثبيت ما يلي على جهاز التطوير الخاص بك:

| المتطلب | الإصدار الأدنى |
|--------------|-----------------|
| .NET 6.0 SDK أو أحدث | 6.0 |
| Visual Studio 2022 (أو أي بيئة تطوير تفضّلها) | 17.0 |
| Aspose.OCR for .NET (حزمة NuGet) | 23.11 أو أحدث |
| وحدة معالجة رسومية تدعم CUDA (NVIDIA) | Compute Capability 3.5+ |
| صورة نموذجية – مثال: `large_document.tif` | أي حجم |

إذا كان أي من هذه غير مألوف لك، لا تقلق. قدرة **use GPU OCR** تعمل حتى على وحدات معالجة رسومية متواضعة، وستقوم حزمة NuGet بجلب جميع الثنائيات الأصلية اللازمة لك.

## الخطوة 1: إجراء التعرف الضوئي على الحروف (OCR) على الصورة باستخدام تسريع GPU

أول شيء نحتاجه هو إنشاء مثيل لمحرك OCR المدعوم بـ GPU. هذا الكائن يقوم بالمعالجة الثقيلة على بطاقة الرسومات، مع الحفاظ على واجهة برمجة تطبيقات (API) نظيفة ومتزامنة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System.Drawing;

// Create a GPU‑accelerated OCR engine and configure it
var ocrEngine = new GpuOcrEngine
{
    // Select the first GPU in the system (device index 0)
    DeviceId = 0,
    // Let the engine download language packs automatically if they’re missing
    AutomaticResourceDownload = true,
    // Specify the language you want to recognize – English in this case
    Language = OcrLanguage.English
};
```

**لماذا هذا مهم:**  
- `DeviceId = 0` يُخبر المكتبة باستخدام GPU الأساسي؛ يمكنك تغييره إذا كان لديك عدة بطاقات.  
- `AutomaticResourceDownload = true` يمنع حدوث خطأ وقت التشغيل عندما لا تكون بيانات اللغة الإنجليزية موجودة محليًا.  
- تعيين `Language` صراحةً يمنع المحرك من الرجوع إلى نموذج عام أبطأ بشكل افتراضي.

> **نصيحة احترافية:** إذا كنت تشغل على خادم بدون واجهة (headless)، تأكد من تثبيت برنامج تشغيل NVIDIA وأن أمر `nvidia-smi` يُظهر أن الـ GPU “متصل”. وإلا سيعود المحرك إلى المعالج (CPU) بصمت.

## الخطوة 2: تحميل ملف الصورة الخاص بك

بعد ذلك، قم بتحميل الصورة التي تريد تطبيق OCR عليها. Aspose يدعم أي `System.Drawing.Image`، لذا يمكنك تمرير JPEG أو PNG أو TIFF أو حتى ملفات PDF متعددة الصفحات (بعد التحويل).

```csharp
// Load the image from disk – replace the path with your own file location
using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");
```

**لماذا هذا مهم:**  
- استخدام جملة `using` يضمن تحرير الموارد غير المُدارة للصورة بسرعة، وهو أمر حاسم عندما تقوم بمعالجة العديد من الملفات في حلقة.  
- إذا كانت صورتك كبيرة جدًا (مثلاً > 500 ميغابايت)، فكر في تقليل دقتها أولاً للحفاظ على استهلاك ذاكرة GPU تحت السيطرة.

## الخطوة 3: التعرف على النص باستخدام محرك OCR المدعوم بـ GPU

الآن نمرر الصورة إلى محرك GPU وننتظر النتيجة. طريقة `Recognize` تُعيد كائن `OcrResult` يحتوي على النص المستخرج ومقاييس الأداء.

```csharp
// Perform OCR – this call runs on the GPU
var ocrResult = ocrEngine.Recognize(image);
```

**لماذا هذا مهم:**  
- الاستدعاء متزامن، أي أن الخيط يتوقف حتى ينتهي الـ GPU. في تطبيق واجهة المستخدم (UI) ستحتاج إلى تشغيله في خيط خلفي للحفاظ على استجابة الواجهة.  
- `ocrResult.ProcessingTime` يزودك بالوقت المستغرق بالميليثانية، وهو مثالي لمقارنة **use GPU OCR** مع البدائل التي تعتمد على CPU فقط.

## الخطوة 4: عرض النتائج والإحصائيات

أخيرًا، نعرض طول النص المُعترف به والمدة التي استغرقها العملية. في تطبيق حقيقي ربما تقوم بكتابة `ocrResult.Text` إلى ملف أو قاعدة بيانات.

```csharp
// Show a quick summary on the console
Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

// Optionally, dump the full text (commented out for brevity)
// Console.WriteLine(ocrResult.Text);
```

**الإخراج المتوقع (مثال):**

```
Recognized 12457 characters in 312 ms
```

لاحظ كيف يتم قياس وقت المعالجة بمئات الميليثانية القليلة لملف TIFF متعدد الميجابايت—وهو بالضبط التسريع الذي تتوقعه عند **use GPU OCR**.

![مثال على إجراء OCR على الصورة](/images/perform-ocr-on-image.png "لقطة شاشة تُظهر مخرجات وحدة التحكم بعد إجراء OCR على الصورة")

*تُظهر لقطة الشاشة أعلاه مخرجات وحدة التحكم بعد إجراء OCR على الصورة باستخدام تسريع GPU.*

## كيفية استخدام GPU OCR بفعالية

على الرغم من أن الكود أعلاه يعمل مباشرةً، إلا أن عمليات النشر في بيئات الإنتاج غالبًا ما تواجه بعض المشكلات. أدناه أكثر القضايا شيوعًا وكيفية حلها.

| المشكلة | السبب | الحل |
|-------|-------|----------|
| **نفاد الذاكرة (GPU)** | الصورة كبيرة جدًا بالنسبة لذاكرة VRAM الخاصة بالـ GPU | قلل أبعاد الصورة (`Bitmap` resize) قبل استدعاء `Recognize`. |
| **حزمة اللغة غير موجودة** | `AutomaticResourceDownload` معطلة أو لا يوجد إنترنت | قم بتحميل حزمة اللغة مسبقًا عبر `ocrEngine.DownloadResources(OcrLanguage.English)`. |
| **بطء التشغيل الأول** | تجميع برنامج تشغيل GPU (JIT) | قم بتسخين المحرك بتشغيل صورة تجريبية صغيرة مرة واحدة عند بدء التشغيل. |
| **مجموعة أحرف غير صحيحة** | خاصية `Language` خاطئة | اضبط `Language` إلى القيمة الصحيحة (مثال: `OcrLanguage.French`). |

**نصيحة احترافية:** عند معالجة العشرات من الملفات على دفعات، أعد استخدام نفس مثيل `GpuOcrEngine`. إنشاء محرك جديد لكل ملف يسبب تبديل سياق GPU مكلف.

## مثال كامل يعمل

إليك البرنامج الكامل مجمعًا في ملف واحد يمكنك نسخه ولصقه في مشروع Console جديد.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Drawing;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize GPU OCR engine
            var ocrEngine = new GpuOcrEngine
            {
                DeviceId = 0,
                AutomaticResourceDownload = true,
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the image (adjust the path to your file)
            using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");

            // 3️⃣ Run recognition on the GPU
            var ocrResult = ocrEngine.Recognize(image);

            // 4️⃣ Output statistics
            Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

            // Optional: write the extracted text to a file
            // System.IO.File.WriteAllText("output.txt", ocrResult.Text);
        }
    }
}
```

احفظ الملف، شغّل `dotnet run`، وسترى عدد الأحرف ووقت المعالجة يُطبع في وحدة التحكم. إذا فتحت `output.txt` (أزل التعليق عن السطر)، سترى النص الأصلي للـ OCR جاهزًا للمعالجة اللاحقة.

## الخلاصة

لقد أظهرنا لك الآن **how to perform OCR on image** باستخدام محرك Aspose المدعوم بـ GPU، بدءًا من إعداد `GpuOcrEngine` إلى معالجة النتيجة وحل المشكلات الشائعة. من خلال تفويض المعالجة الثقيلة إلى بطاقة الرسومات، ستحصل على تحسينات سرعة بمقاييس ضخمة—وهو ما تحتاجه عند التعامل مع مستندات كبيرة أو سيناريوهات المسح في الوقت الفعلي.

> **الخلاصة:** الجمع بين `GpuOcrEngine`، معالجة الموارد تلقائيًا، وتحديد حجم الصورة بعناية يمنحك خط أنابيب قوي وعالي الأداء لأي مشروع C# يحتاج إلى **use GPU OCR**.

### ما التالي؟

- **معالجة دفعات:** غلف المنطق الأساسي داخل حلقة `foreach` لمعالجة مجلدات الصور.  
- **التوازي:** دمج GPU OCR مع `Parallel.ForEach` لخوادم متعددة الـ GPU.  
- **معالجة لاحقة:** تمرير `ocrResult.Text` إلى مدقق إملائي أو مستخرج كيانات لتحليلات ذكية لاحقة.  

لا تتردد في التجربة—استبدل `OcrLanguage.English` بلغة أخرى، جرّب صيغ صور مختلفة، أو دمج المحرك في API ASP.NET. السماء هي الحد عندما **use GPU OCR** بمسؤولية.

برمجة سعيدة، ولتعمل مهام OCR الخاصة بك بسرعة البرق!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}