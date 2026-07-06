---
category: general
date: 2026-06-19
description: كيفية استخدام Aspose OCR في C# لاستخراج النص من الصور، وتشغيل OCR على
  الصور، والتعرف على النص من المسحات الضوئية – دليل خطوة بخطوة.
draft: false
keywords:
- how to use aspose
- extract text from images
- run ocr on images
- recognize text from scans
language: ar
og_description: كيفية استخدام Aspose OCR في C# لاستخراج النص من الصور، وتشغيل OCR
  على الصور، والتعرف على النص من المسحات الضوئية – دليل كامل.
og_title: كيفية استخدام Aspose OCR في C# – استخراج النص من الصور
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to use Aspose OCR in C# to extract text from images, run OCR on
    images, and recognize text from scans – step‑by‑step guide.
  headline: How to Use Aspose OCR in C# – Extract Text from Images
  type: TechArticle
tags:
- Aspose
- OCR
- C#
- Image Processing
title: كيفية استخدام Aspose OCR في C# – استخراج النص من الصور
url: /ar/net/text-recognition/how-to-use-aspose-ocr-in-c-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام Aspose OCR في C# – استخراج النص من الصور

هل تساءلت يومًا **كيف تستخدم Aspose** لاستخراج الكلمات من صورة مستند؟ لست الوحيد الذي يحاول حل هذه المشكلة. في هذا الدرس سنستعرض مثالًا عمليًا من البداية إلى النهاية يوضح لك بالضبط كيفية استخراج النص من الصور، تشغيل OCR على مجموعة من الصور دفعة واحدة، وحتى التعرف على النص من المسحات الضوئية ببضع أسطر من C# فقط.

سنبدأ بإعداد محرك Aspose OCR، ثم نمرره قائمة بملفات JPEG، وأخيرًا نطبع كل نتيجة على وحدة التحكم. في النهاية ستحصل على مقطع شفرة يمكن إعادة استخدامه في أي مشروع .NET—بدون خطوات غامضة، بدون مراجع مفقودة.

## ما ستحتاجه

قبل أن نبدأ، تأكد من توفر التالي:

* .NET 6.0 SDK أو أحدث (الكود يعمل على .NET Core و .NET Framework على حد سواء)  
* حزمة **Aspose.OCR** NuGet صالحة (يمكنك الحصول على مفتاح تجريبي مجاني من موقع Aspose)  
* مجلد يحتوي على بعض الصور الممسوحة ضوئيًا أو صور نصية (JPEG أو PNG يعملان بشكل جيد)  
* بيئة التطوير المفضلة لديك—Visual Studio أو Rider أو حتى VS Code.

هذا كل ما تحتاجه. لا مكتبات OCR ثقيلة، ولا أدوات سطر أوامر خارجية. فقط Aspose وبضع أسطر من الشفرة.

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

افتح الطرفية في مجلد مشروعك وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

يقوم الأمر بجلب أحدث نسخة (اعتبارًا من يونيو 2026 الإصدار 22.9) وإضافة المرجع إلى ملف `.csproj` الخاص بك. إذا كنت تفضّل واجهة Visual Studio، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages** وابحث عن “Aspose.OCR”.

> **نصيحة احترافية:** راقب تاريخ انتهاء صلاحية الترخيص؛ النسخة التجريبية المجانية صالحة لمدة 30 يومًا ثم ستحتاج إلى مفتاح تجاري.

## الخطوة 2: تكوين محرك OCR – بدء “كيفية استخدام Aspose”

الآن بعد أن تم تثبيت الحزمة، لننشئ محرك OCR ونحدّد اللغة التي نريد التعرف عليها. في معظم الحالات تكون الإنجليزية كافية، لكن Aspose يدعم أكثر من 70 لغة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.Collections.Generic;

// Configure the OCR engine to use English language
var ocrConfig = new OcrEngineConfig { Language = Language.English };
using var ocrEngine = new OcrEngine(ocrConfig);
```

لماذا نغلف `OcrEngine` بعبارة `using`؟ لأنّه يطبق الواجهة `IDisposable`. عملية التخلص (Dispose) تُحرّر الموارد الأصلية (مثل الذاكرة غير المُدارة) التي يخصصها محرك OCR داخليًا—وهو أمر ضروري في خدمة إنتاجية تعالج عشرات الملفات في الدقيقة.

## الخطوة 3: بناء قائمة بمسارات الصور – التحضير لـ **تشغيل OCR على الصور**

الجزء التالي هو `List<string>` بسيط يشير إلى كل صورة تريد معالجتها. يمكنك بناء هذه القائمة يدويًا (كما في المثال أدناه) أو توليدها ديناميكيًا باستخدام `Directory.GetFiles`.

```csharp
// Prepare a list of image file paths to be processed
var imagePaths = new List<string>
{
    @"C:\Scans\page1.jpg",
    @"C:\Scans\page2.jpg",
    @"C:\Scans\page3.jpg"
};
```

إذا كانت صورك موجودة في مجلد فرعي بالنسبة للملف التنفيذي، فقط أضف `Path.Combine` هناك. المفتاح هو أن ترتيب القائمة يُحافظ عليه—ستُعيد Aspose النتائج بنفس التسلسل، مما يجعل مطابقة المخرجات مع المدخلات أمرًا سهلًا.

## الخطوة 4: **تشغيل OCR على الصور** دفعة واحدة

يتألق Aspose OCR عندما تحتاج إلى معالجة العديد من الملفات في آنٍ واحد. طريقة `ProcessBatch` تقبل القائمة التي أنشأناها للتو وتعيد `IList<OcrResult>` حيث يحتوي كل عنصر على النص المُتعرف عليه، درجات الثقة، وحتى إطارات الحدود إذا احتجت إليها لاحقًا.

```csharp
// Run OCR on the entire batch and obtain results in the same order
IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);
```

تحت الغطاء، يُنشئ Aspose خيوطًا أصلية لتسريع العملية، لذا ستحصل على تقريبًا توسع خطي مع عدد نوى المعالج. للعبء الضخم قد ترغب في ضبط خاصية `OcrEngineConfig.ThreadCount`، لكن الإعداد الافتراضي للتحديد التلقائي يعمل جيدًا لمعظم سيناريوهات سطح المكتب.

## الخطوة 5: عرض **النص المُتعرف عليه من المسحات** – التحقق من النتيجة

أخيرًا، لنُكرّر النتائج ونطبع كل كتلة نصية. سنعيد أيضًا طباعة اسم الملف الأصلي لتتمكن من معرفة أي ناتج ينتمي إلى أي مسح.

```csharp
// Iterate through the results and display the recognized text for each image
for (int i = 0; i < ocrResults.Count; i++)
{
    System.Console.WriteLine($"--- Result for {imagePaths[i]} ---");
    System.Console.WriteLine(ocrResults[i].Text);
}
```

عند تشغيل البرنامج، ستظهر وحدة التحكم شيئًا مثل:

```
--- Result for C:\Scans\page1.jpg ---
Invoice #12345
Date: 06/15/2026
Total: $1,250.00

--- Result for C:\Scans\page2.jpg ---
Terms and Conditions
...
```

هذا هو الهدف—**كيفية استخدام Aspose** لتحويل مجموعة من ملفات PDF أو JPEG الممسوحة ضوئيًا إلى نص قابل للبحث والتحرير.

![مثال ناتج Aspose OCR](image-placeholder.png "مثال ناتج Aspose OCR")

*نص بديل للصورة: “مثال ناتج Aspose OCR يُظهر النص المُتعرف عليه من المسحات.”*

## اختياري: تحسين الدقة – عندما تحتاج **استخراج النص من الصور** إلى تعزيز

إذا لاحظت فقدان أحرف أو كلمات مشوشة، جرّب التعديلات التالية:

| الإعداد | ما يفعله | متى يُستخدم |
|---------|----------|-------------|
| `ocrConfig.DetectOrientation = true` | يدور الصور تلقائيًا إذا كانت مائلة | الكتب الممسوحة غالبًا ما تكون بوضعية عمودية |
| `ocrConfig.Preprocess = true` | يطبق تحسين التباين وتقليل الضوضاء | صور منخفضة الجودة تم التقاطها بهاتف |
| `ocrConfig.CharacterWhitelist = "0123456789"` | يقتصر التعرف على الأرقام فقط | استخراج إجماليات الفواتير أو أرقام السيريال |
| `ocrEngine.SetPageSegmentationMode(PageSegMode.SingleBlock)` | يعامل الصفحة بأكملها ككتلة نص واحدة | عندما يكون التخطيط بسيطًا وتريد السرعة |

جرّب هذه العلامات حتى ترتفع درجات الثقة (المتاحة عبر `ocrResults[i].Confidence`) إلى ما فوق 0.9. تذكّر، كلما كان مصدر الصورة أفضل، كلما كان ناتج OCR أفضل—لذا فإن بعض المعالجة المسبقة في Photoshop أو ImageMagick يمكن أن يوفر لك ساعات من التصحيح.

## مثال كامل جاهز للتنفيذ – نسخ‑لصق

فيما يلي البرنامج الكامل الذي يمكنك تجميعه وتشغيله كما هو. فقط استبدل مسارات الملفات بمسارات مجلدك الخاص.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine (how to use Aspose OCR)
        var ocrConfig = new OcrEngineConfig
        {
            Language = Language.English,
            DetectOrientation = true,          // optional: auto‑rotate
            Preprocess = true                  // optional: improve low‑quality scans
        };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // 2️⃣ List of image files (run OCR on images)
        var imagePaths = new List<string>
        {
            @"C:\Scans\page1.jpg",
            @"C:\Scans\page2.jpg",
            @"C:\Scans\page3.jpg"
        };

        // 3️⃣ Process the batch (extract text from images)
        IList<OcrResult> ocrResults = ocrEngine.ProcessBatch(imagePaths);

        // 4️⃣ Show the results (recognize text from scans)
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Result for {imagePaths[i]} ---");
            Console.WriteLine(ocrResults[i].Text);
            Console.WriteLine($"Confidence: {ocrResults[i].Confidence:P2}");
            Console.WriteLine(); // blank line for readability
        }
    }
}
```

قم بالتجميع باستخدام `dotnet run` وشاهد وحدة التحكم تمتلئ بنص نظيف قابل للبحث. هذا هو سير عمل **كيفية استخدام Aspose** بالكامل في أقل من 50 سطرًا من الشفرة.

## الأخطاء الشائعة وكيفية حلها

* **NullReferenceException على `ocrResults[i]`** – عادةً ما يعني أن المحرك لم يتمكن من فتح الملف (مسار خاطئ، صيغة غير مدعومة). تحقق من امتداد الملف والأذونات.  
* **حروف غريبة** – إذا رأيت رموز “�”، فربما تم حفظ الصورة بترميز غير UTF‑8. حوّل الصورة إلى PNG غير مضغوط أولًا، أو فعّل `ocrConfig.Preprocess`.  
* **عنق زجاجة في الأداء** – للدفعات التي تتجاوز 100 صورة، فكر في المعالجة المتوازية باستخدام `Parallel.ForEach` وإنشاء نسخة منفصلة من `OcrEngine` لكل خيط. Aspose آمن للاستخدام المتعدد للخطوط طالما أن كل خيط يمتلك محركه الخاص.

## الخطوات التالية – تعمّق أكثر

الآن بعد أن أتقنت أساسيات **كيفية استخدام Aspose** للـ OCR، قد ترغب في استكشاف:

* **التصدير إلى PDF قابل للبحث** – استخدم `Aspose.Pdf` لدمج النص المُتعرف عليه داخل ملف PDF، محولًا المستند الممسوح إلى عنصر قابل للبحث فعليًا.  
* **التكامل مع Azure Functions** – تشغيل OCR تلقائيًا عند وصول صورة جديدة إلى حاوية Azure Blob.  
* **الدمج مع نماذج اللغة الذكية** – مرّر النص المستخرج إلى ChatGPT أو Claude للتلخيص، استخراج الكيانات، أو الترجمة.

كل من هذه المواضيع يتضمن كلماتنا المفتاحية الثانوية—**استخراج النص من الصور**، **تشغيل OCR على الصور**، و**التعرف على النص من المسحات**—وبالتالي ستستمر في رؤية الأنماط نفسها أثناء توسيع مهاراتك.

## الخلاصة

استعرضنا مثالًا كاملًا وجاهزًا للإنتاج يجيب على سؤال **كيفية استخدام Aspose** لاستخراج النص من الصور، تشغيل OCR على مجموعة من الصور دفعة واحدة، والتعرف على النص من المسحات بأقل قدر من الشفرة. من خلال تكوين المحرك، إعداد قائمة مسارات الملفات، معالجة الدفعة، وطباعة النتائج، أصبحت الآن تمتلك أساسًا قويًا لأي مشروع أتمتة مستندات.

جرّبه، عدّل إعدادات التكوين، وسرعان ما ستحوّل أكوامًا من الورق إلى نصوص قابلة للبحث.

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [استخراج النص من الصور باستخدام عملية OCR على المجلدات](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [استخراج النص من الصورة – تحسين OCR باستخدام Aspose.OCR لـ .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}