---
category: general
date: 2026-03-05
description: حوّل ملفات TIFF إلى نص في C# بسرعة باستخدام Aspose OCR. تعلّم كيفية عرض
  نص OCR من ملفات TIFF متعددة الصفحات في دقائق.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: ar
og_description: تحويل ملفات TIFF إلى نص في C# باستخدام Aspose OCR. يوضح لك هذا الدليل
  كيفية عرض نص OCR من صور TIFF متعددة الصفحات خطوة بخطوة.
og_title: تحويل TIFF إلى نص في C# – دليل Aspose OCR الكامل
tags:
- Aspose
- OCR
- C#
- TIFF
title: تحويل ملف TIFF إلى نص في C# باستخدام Aspose OCR
url: /ar/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تحويل TIFF إلى نص في C# باستخدام Aspose OCR

هل تحتاج إلى **تحويل TIFF إلى نص** في C#؟ لست وحدك—العديد من المطورين يواجهون صعوبة في استخراج السلاسل القابلة للقراءة من ملفات TIFF متعددة الصفحات. الخبر السار هو أن Aspose OCR C# يجعل المهمة شبه خالية من المتاعب، ويمكنك **عرض نص OCR** على وحدة التحكم أو إرساله إلى نظام آخر في ثوانٍ.

في هذا البرنامج التعليمي سنستعرض مثالًا كاملاً جاهزًا للتنفيذ يوضح بالضبط كيفية تحميل ملف TIFF متعدد الصفحات، تشغيل OCR، وطباعة نص كل صفحة. لا خطوات مخفية، ولا اختصارات “انظر الوثائق”. في النهاية ستحصل على برنامج مستقل يمكنك إدراجه في أي مشروع .NET.

## ما ستحتاجه

- .NET 6.0 أو أحدث (المثال يستهدف .NET 6، لكن .NET 5 يعمل أيضًا)  
- ملف ترخيص Aspose OCR صالح (`Aspose.OCR.lic`). المكتبة تعمل بدون ترخيص، لكن ستحصل على علامة مائية تجريبية لمدة 20 ثانية.  
- ملف TIFF متعدد الصفحات تريد معالجته (سنسميه `multipage.tif`).  
- Visual Studio 2022 أو أي محرر تفضله—لا شيء غير عادي.

إذا كانت كل هذه المتطلبات متوفرة، لنبدأ.

## الخطوة 1: تثبيت حزمة Aspose OCR NuGet

قبل تشغيل أي كود، تحتاج إلى المكتبة نفسها. افتح طرفية في مجلد المشروع ونفّذ:

```bash
dotnet add package Aspose.OCR
```

هذا السطر الواحد يجلب أحدث نسخة مستقرة (حتى مارس 2026 الإصدار هو 23.9).  

> **نصيحة احترافية:** حافظ على تحديث الحزم؛ الإصدارات الأحدث غالبًا ما تتضمن تحسينات أداء للـ TIFF الكبيرة.

## الخطوة 2: إعداد ترخيص Aspose OCR C# (اختياري لكن مُستحسن)

تشغيل محرك OCR بدون ترخيص ممكن، لكن الناتج سيُسبق بإنذار تجريبي. لتجنب ذلك، وجه المحرك إلى ملف `.lic` الخاص بك:

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

إذا تخطيت هذه الخطوة، سيظل الكود يعمل—فقط تذكر النص الإضافي في النتائج.

## الخطوة 3: تحميل وتعرف على الـ Multi‑Page TIFF

الآن نقوم فعليًا **بتحويل TIFF إلى نص**. المساعد `ImageStream.FromFile` يقرأ الملف إلى صيغة يفهمها المحرك. بعد ذلك نستدعي `Recognize()` التي تُعيد كائن `OcrResult` يحتوي على نص كل صفحة.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **لماذا هذا مهم:** `Recognize()` تقوم بالعمل الشاق—تحليل البكسل، اكتشاف اللغة، وإعادة بناء سطر النص—كل ذلك في كود C# أصلي. كائن النتيجة يمنحك وصولًا صفحةً بصفحة، وهو مثالي لـ **عرض نص OCR** لاحقًا.

## الخطوة 4: التكرار عبر الصفحات و**عرض نص OCR**

مع النتيجة في المتناول، نمر ببساطة على الصفحات ونطبع كل واحدة. هذه هي اللحظة التي ترى فيها التحويل من صورة إلى نص عادي.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

تشغيل البرنامج ينتج مخرجات مشابهة للتالي (النص الفعلي سيختلف بناءً على محتوى TIFF):

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

هذا كل شيء—لقد نجحت في **تحويل TIFF إلى نص** و**عرض نص OCR** لكل صفحة.

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد (`dotnet new console`). يتضمن جميع توجيهات `using`، معالجة الترخيص، وفحص الأخطاء.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**المخرجات المتوقعة** (مقتطفة للاختصار) موضحة أعلاه. إذا رأيت علامة مائية تجريبية، تحقق مرة أخرى من صحة مسار الترخيص.

## المشكلات الشائعة عند تحويل TIFF إلى نص

| المشكلة | لماذا يحدث | كيفية الإصلاح |
|-------|----------------|------------|
| **نفاد الذاكرة في TIFF الكبيرة** | المحرك يحمل الصورة بالكامل في الذاكرة. | استخدم `ImageStream.FromFile(..., loadOnlyFirstPage: false)` وعالج الصفحات على دفعات، أو زد حد الذاكرة للعملية. |
| **حروف غير مفهومة** | الصور منخفضة الدقة تُربك محرك OCR. | عالج الـ TIFF مسبقًا (مثلاً، زد DPI إلى 300) قبل إرساله إلى Aspose OCR. |
| **عدم تطبيق الترخيص** | `SetLicense` يرمي استثناءً وتتجاهله. | غلف الاستدعاء بـ try/catch (كما هو موضح) وسجّل الخطأ. |
| **غياب بيانات اللغة** | بشكل افتراضي يفترض OCR اللغة الإنجليزية. | عيّن `ocrEngine.Language = OcrLanguage.French;` (أو أي لغة مدعومة) قبل `Recognize()`. |

معالجة هذه الحالات تضمن تشغيل التحويل بسلاسة في بيئة الإنتاج.

## الخطوات التالية: ما بعد العرض البسيط

الآن بعد أن أصبحت قادرًا على **تحويل TIFF إلى نص** و**عرض نص OCR**، قد ترغب في:

- **حفظ النص المستخرج** إلى ملف `.txt` أو قاعدة بيانات للتحليل لاحقًا.  
- **دمج عدة ملفات TIFF** في ملف PDF قابل للبحث باستخدام Aspose.PDF.  
- **تطبيق معالجة لاحقة** (تدقيق إملائي، تنظيف باستخدام regex) لتحسين الدقة.  

كل هذه الامتدادات تُبنى على النمط الأساسي الذي غطيناه للتو.

---

### TL;DR

لقد استعرضنا حلًا كاملًا بلغة C# **يحول TIFF إلى نص** باستخدام Aspose OCR C#. الكود ينشئ `OcrEngine`، يحمل الترخيص اختياريًا، يقرأ TIFF متعدد الصفحات، ينفّذ OCR، و**يعرض نص OCR** صفحةً بصفحة. مع المثال الكامل المرفق، يمكنك إدراجه في أي مشروع .NET والبدء في استخراج النص فورًا.

هل لديك أسئلة حول الأداء، دعم اللغات، أو التكامل مع منتجات Aspose الأخرى؟ اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}