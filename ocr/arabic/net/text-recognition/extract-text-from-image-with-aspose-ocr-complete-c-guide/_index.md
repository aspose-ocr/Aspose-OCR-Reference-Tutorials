---
category: general
date: 2026-01-04
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل الصورة
  للـ OCR وتعيين لغة الـ OCR للمعالجة دون اتصال.
draft: false
keywords:
- extract text from image
- load image for ocr
- set ocr language
- offline ocr csharp
- aspose ocr tutorial
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف وتعيين لغة OCR لمعالجة موثوقة دون اتصال.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
tags:
- C#
- OCR
- Aspose
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من صورة باستخدام Aspose OCR – دليل C# كامل

هل احتجت يوماً إلى **استخراج النص من صورة** لكن واجهت سؤال “كيف أحصل على البكسلات في الكود؟”؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير، التحقق من الهوية، أو مجرد تحويل الملاحظات المكتوبة بخط اليد إلى نص—الحصول على نتائج OCR موثوقة هو ميزة حاسمة.

الأمر ببساطة: Aspose OCR يتيح لك **تحميل الصورة للـ OCR** و **تحديد لغة الـ OCR** دون الحاجة للاتصال بالإنترنت. في هذا الدرس سنستعرض مثالًا كاملًا قابلاً للتنفيذ بلغة C# يوضح بالضبط كيفية القيام بذلك، بالإضافة إلى مجموعة من النصائح التي كنت ستتمنى معرفتها مسبقًا.

> **ما ستحصل عليه**  
> • برنامج كامل يمكنك نسخه ولصقه لاستخراج النص من صورة.  
> • فهم لماذا يجب توجيه المحرك إلى حزمة لغة محلية.  
> • نصائح عملية للتعامل مع الحالات الطرفية (موارد مفقودة، مسارات ملفات خاطئة، إلخ).

---

## ما ستحتاجه

- **.NET 6+** (الكود يُمكن أن يُترجم على .NET Framework أيضًا، لكن .NET 6 هو الخيار المثالي).  
- حزمة **Aspose.OCR for .NET** عبر NuGet (`Install-Package Aspose.OCR`).  
- مجلد لغة OCR محلي (سنستخدم حزمة Tamil في المثال).  
- ملف صورة تريد معالجته (مثال: `tamil_note.jpg`).  

لا يلزم اتصال بالإنترنت بمجرد وجود موارد اللغة على القرص، مما يجعل هذا النهج مثاليًا للبيئات غير المتصلة أو الآمنة.

---

## الخطوة 1: استخراج النص من صورة – تحضير الموارد

أولاً، نحتاج إلى إخبار Aspose OCR بمكان وجود ملفات اللغة. إذا لم تقم بتحميل حزمة Tamil بعد، احصل عليها من موقع Aspose وضعها في مجلد يُسمى **Resources** بجوار الملف التنفيذي.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

// Define the path to the local OCR language resources
string resourcesPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Resources");

// Ensure the folder exists – a simple guard against a common pitfall
if (!Directory.Exists(resourcesPath))
{
    Console.WriteLine($"Resources folder not found at {resourcesPath}");
    return;
}
```

**لماذا هذا مهم:** من خلال ضبط `ResourcesPath` نجبر المحرك على العمل في **وضع غير متصل**. هذا يمنع أي استدعاءات شبكة غير متوقعة ويضمن نتائج ثابتة عبر جميع النشر.

---

## الخطوة 2: تحميل الصورة للـ OCR

الآن بعد أن علم المحرك أين يبحث عن بيانات اللغة، نحتاج إلى تزويده بالصورة التي نريد قراءتها. هنا يبرز دور خطوة **load image for OCR**—Aspose يدعم مجموعة واسعة من الصيغ (JPG، PNG، BMP، TIFF، إلخ).

```csharp
// Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Config =
    {
        ResourcesPath = resourcesPath,      // Force offline mode
        AutoDownloadResources = false,     // Disable on‑demand download
        Language = Language.Tamil          // Set OCR language (see next step)
    }
};

// Load the image you want to recognize
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "tamil_note.jpg");

// Defensive check – helps you avoid the dreaded FileNotFoundException
if (!File.Exists(imagePath))
{
    Console.WriteLine($"Image not found at {imagePath}");
    return;
}

ocrEngine.LoadImage(imagePath);
```

**نصيحة احترافية:** غلف استدعاء `LoadImage` بكتلة try‑catch إذا كان تطبيقك يعالج ملفات يرفعها المستخدم. بهذه الطريقة يمكنك إظهار رسالة خطأ ودية بدلاً من تتبع الأخطاء.

---

## الخطوة 3: تعيين لغة الـ OCR – اختيار الحزمة المناسبة

إذا تخطيت هذه الخطوة، سيستخدم Aspose اللغة الإنجليزية افتراضيًا، مما سيؤدي إلى نتائج غير مفهومة عندما يكون النص الأصلي بـ Tamil أو العربية أو أي نص آخر. تعيين اللغة بسيط كإسناد قيمة enum، ويمكنك أيضًا تمرير رمز ISO‑639‑2 مخصص إذا أضفت حزمة طرف ثالث.

```csharp
// The language was already set in the config above, but you can change it at runtime:
ocrEngine.Config.Language = Language.Tamil; // Options: English, Arabic, ChineseSimplified, etc.
```

**لماذا يهمك ذلك:** دقة الـ OCR تعتمد على نماذج الأحرف الخاصة بكل لغة. استخدام الحزمة الصحيحة يمكن أن يرفع معدلات التعرف من 60 % إلى أكثر من 95 % للعديد من النصوص.

---

## الخطوة 4: تنفيذ التعرف والحصول على النتائج

مع كل شيء في مكانه—الموارد، الصورة، اللغة—نصبح جاهزين لاستخراج النص فعليًا. طريقة `Recognize` تقوم بكل العمل وتعيد كائن `OcrResult` يحتوي على السلسلة الخام، درجات الثقة، وحتى إطارات الحد إذا احتجت إليها لاحقًا.

```csharp
// Perform the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();

// Output the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**الناتج المتوقع:** بافتراض أن `tamil_note.jpg` يحتوي على كتابة يدوية واضحة بـ Tamil، ستظهر الأحرف Unicode Tamil مطبوعة في وحدة التحكم. إذا كانت الصورة غير واضحة، قد يتضمن الناتج علامات استفهام أو رموز مشوهة—هنا يصبح التحسين المسبق (تصحيح الميل، إزالة الضوضاء) مفيدًا.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه‑لصقه في مشروع console جديد. يتضمن جميع الحمايات التي ناقشناها، لذا يمكنك تشغيله فورًا.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Define resources folder (offline OCR)
        // -------------------------------------------------
        string resourcesPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Resources");
        if (!Directory.Exists(resourcesPath))
        {
            Console.WriteLine($"Resources folder not found at {resourcesPath}");
            return;
        }

        // -------------------------------------------------
        // Step 2: Configure OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            Config =
            {
                ResourcesPath = resourcesPath,
                AutoDownloadResources = false,
                Language = Language.Tamil // <-- set OCR language here
            }
        };

        // -------------------------------------------------
        // Step 3: Load the image you want to process
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "tamil_note.jpg");
        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        ocrEngine.LoadImage(imagePath);

        // -------------------------------------------------
        // Step 4: Run OCR and display the result
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize();

        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**تشغيله:**  
1. ضع مجلد `Resources` (الذي يحتوي على ملفات لغة Tamil) بجوار ملف `.exe` المترجم.  
2. ضع `tamil_note.jpg` في نفس الدليل.  
3. نفّذ `dotnet run` (أو شغّل الـ EXE).  

سترى النص المستخرج بـ Tamil مطبوعًا في وحدة التحكم.

---

## أسئلة شائعة وحالات طرفية

| السؤال | الجواب |
|----------|--------|
| **ماذا لو أردت معالجة عدة صور؟** | أعد استخدام نفس كائن `OcrEngine`—فقط استدعِ `LoadImage` مرة أخرى قبل كل `Recognize`. |
| **هل يمكنني تبديل اللغات أثناء التشغيل؟** | بالتأكيد. عيّن `ocrEngine.Config.Language = Language.English;` (أو أي enum مدعوم آخر) قبل تحميل الصورة التالية. |
| **صوري هي صفحات PDF—هل يعمل هذا؟** | ليس مباشرة. حوّل صفحة PDF إلى صورة (مثلاً باستخدام Aspose.PDF) ثم مرّر الـ bitmap إلى `LoadImage`. |
| **ماذا لو كانت حزمة اللغة مفقودة؟** | سيطلق المحرك استثناء `FileNotFoundException`. احمِ الكود بالتحقق من وجود المجلد عبر `Directory.Exists(resourcesPath)` (كما هو موضح). |
| **هل يمكن الحصول على درجات الثقة؟** | `ocrResult.Confidence` يعطي درجة عامة؛ `ocrResult.Regions` يحتوي على ثقة كل حرف إذا احتجت بيانات تفصيلية. |

---

## نصائح احترافية لتطبيق OCR جاهز للإنتاج

1. **معالجة الصور مسبقًا** – صحّح الميل، زد التباين، وأزل الضوضاء. فلاتر `System.Drawing` البسيطة يمكن أن تعزز الدقة بشكل كبير.  
2. **خزن المحرك في الذاكرة** – إنشاء `OcrEngine` جديد لكل طلب مكلف. احتفظ بـ singleton لكل لغة في خدمة الويب.  
3. **تعامل مع Unicode بشكل صحيح** – تأكد أن وحدة التحكم أو الواجهة تستخدم UTF‑8؛ وإلا ستظهر الأحرف غير اللاتينية كـ “�”.  
4. **سجّل المخرجات الخام** – احفظ `ocrResult.Text` جنبًا إلى جنب مع الصورة الأصلية لتتبع التدقيق.  
5. **العودة بخطوة عند انخفاض الثقة** – إذا انخفضت الثقة عن 0.6، فكر في طلب إعادة المسح من المستخدم أو تشغيل محرك OCR ثانوي.

---

## الخاتمة

لقد قمنا الآن **باستخراج النص من صورة** باستخدام Aspose OCR، وعرضنا كيفية **تحميل الصورة للـ OCR**، وأظهرنا الطريقة الصحيحة لـ **تعيين لغة الـ OCR** للحصول على نتائج غير متصلة وعالية الدقة. المثال الكامل القابل للتنفيذ يجب أن يضعك على الطريق خلال دقائق، والنصائح الإضافية ستجعل تطبيقك قويًا مع التوسع.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال حزمة Tamil بحزمة لغة أخرى، أو جرب المعالجة الدفعة لعدة ملفات بالتوازي. يمكنك أيضًا استكشاف **أدوات ما قبل معالجة الصور** من Aspose للحصول على دقة أعلى في المسحات الصعبة.

إذا واجهت أي مشكلة، اترك تعليقًا أدناه—برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}