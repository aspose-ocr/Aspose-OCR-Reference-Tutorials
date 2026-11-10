---
category: general
date: 2026-06-19
description: التعرف على النص في الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحويل
  الصورة إلى ePub، وتحويل الصورة إلى نص باستخدام OCR، وتصدير ملفات Excel المستخرجة
  عبر OCR في دقائق.
draft: false
keywords:
- recognize text image
- convert image to epub
- image to txt ocr
- export ocr excel
language: ar
og_description: التعرف على النص في الصورة فورًا. يوضح هذا الدليل كيفية تحويل الصورة
  إلى ePub، وتحويل الصورة إلى نص باستخدام OCR، وتصدير نتائج OCR إلى Excel باستخدام
  Aspose OCR.
og_title: التعرف على نص الصورة باستخدام Aspose OCR – دليل C# الكامل
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: recognize text image using Aspose OCR in C#. Learn to convert image
    to ePub, image to txt OCR, and export OCR Excel files in minutes.
  headline: recognize text image with Aspose OCR – Full C# Guide
  type: TechArticle
tags:
- Aspose OCR
- C#
- OCR
- ePub
- Excel
title: التعرف على نص الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/recognize-text-image-with-aspose-ocr-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص في الصورة باستخدام Aspose OCR – دليل C# كامل

هل احتجت يومًا إلى **recognize text image** لكنك لم تكن متأكدًا أي مكتبة ستعطيك نتائج نظيفة دون إعداد معقد؟ لست وحدك. في العديد من المشاريع—معالجة الفواتير، أرشفة الكتب الممسوحة ضوئيًا، أو إدخال البيانات السريع—إمكانية استخراج النص من صورة تُعد مشكلة يومية.  

الأخبار السارة؟ باستخدام Aspose OCR يمكنك **recognize text image** في بضع أسطر فقط، ثم فورًا **convert image to ePub**، حفظ ملف **image to txt OCR**، وحتى **export OCR Excel** لجداول البيانات للتحليل اللاحق. لننطلق مباشرةً إلى حل عملي.

![recognize text image example](ocr_flow.png "recognize text image example")

## ما ستحتاجه

- .NET 6 SDK أو أحدث (الكود يعمل على .NET Core 3.1+ أيضًا)  
- حزمة Aspose.OCR NuGet صالحة (الحزمة الأساسية بالإضافة إلى الحزمة الاختيارية *Aspose.OCR.ExtendedFormats* لـ ePub)  
- ملف صورة يحتوي على نص إنجليزي قابل للقراءة (PNG يعمل بشكل ممتاز)  
- بيئة تطوير مفضلة—Visual Studio، VS Code، Rider، أو أيًا كان ما تفضله  

لا متطلبات مسبقة معقدة بخلاف ذلك. إذا كان لديك مشروع C# بالفعل، فأنت جاهز.

## الخطوة 1 – recognize text image في C#  

أولًا، علينا تشغيل محرك OCR وإبلاغه أننا نتعامل مع اللغة الإنجليزية. هذا هو الأساس لكل تصدير لاحق.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.IO;

class ExportDemo
{
    static void Main()
    {
        // 1️⃣ Configure the OCR engine for English language
        var ocrConfig = new OcrEngineConfig { Language = Language.English };
        using var ocrEngine = new OcrEngine(ocrConfig);
```

**لماذا هذا مهم:** يتيح لك `OcrEngineConfig` اختيار قاموس اللغة، مما يحسن الدقة بشكل كبير. إذا تخطيت هذه الخطوة سيعود المحرك إلى نموذج عام غالبًا ما يخطئ في التعرف على الأحرف.

## الخطوة 2 – استخراج النص من الصورة  

الآن بعد أن أصبح المحرك جاهزًا، نقوم بتمرير صورتنا المصدرية إليه. تُعيد استدعاء `RecognizeImage` كائنًا من نوع `OcrResult` يحتوي على النص العادي، درجات الثقة، وبيانات التخطيط.

```csharp
        // 2️⃣ Recognize text from the input image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/input.png");
```

**نصيحة:** حافظ على دقة الصورة حوالي 300 dpi للحصول على أفضل النتائج؛ الدقة الأقل قد تتسبب في مخرجات مشوشة، خاصةً مع الخطوط الصغيرة.

## الخطوة 3 – image to txt OCR – حفظ النص العادي  

إذا كان كل ما تحتاجه هو استخراج سريع للكلمات، فإن كتابة الخاصية `Text` إلى ملف `.txt` تكفي.

```csharp
        // 3️⃣ Save the recognized plain text (default output)
        File.WriteAllText("YOUR_DIRECTORY/output.txt", ocrResult.Text);
```

الآن لديك ملف **image to txt OCR** يمكنك تمريره إلى أي عملية لاحقة—فهرسة البحث، استخراج البيانات، أو مجرد الأرشفة.

## الخطوة 4 – تصدير إلى JSON (اختياري لكنه مفيد)  

يوفر لك JSON عرضًا منظمًا لمربع حدود كل كلمة، الثقة، وفواصل الأسطر. إنه مثالي لبناء طبقات واجهة مستخدم مخصصة.

```csharp
        // 4️⃣ Export the result to JSON format
        File.WriteAllText("YOUR_DIRECTORY/output.json", ocrResult.ToJson());
```

## الخطوة 5 – كيفية تحويل الصورة إلى ePub باستخدام Aspose OCR  

للقارئين الذين يحبون الكتب الإلكترونية، تحويل الصفحة الممسوحة إلى ePub سهل للغاية. كل ما تحتاجه هو حزمة *Aspose.OCR.ExtendedFormats* الإضافية.

```csharp
        // 5️⃣ Export the result to ePub (requires Aspose.OCR.ExtendedFormats package)
        ocrEngine.ExportToEpub(ocrResult, "YOUR_DIRECTORY/output.epub");
```

سيحتوي `output.epub` الناتج على نص قابل للبحث، مما يجعل كتبك الرقمية قابلة للبحث فعليًا على أي قارئ إلكتروني.

## الخطوة 6 – export OCR Excel – إنشاء ملفات XLSX  

غالبًا ما يرغب محللو الأعمال في الحصول على مخرجات OCR في جدول بيانات لإعداد جداول محورية أو تعديلات جماعية. يمكن لـ Aspose OCR كتابة دفتر عمل Excel مباشرة.

```csharp
        // 6️⃣ Export the result to Excel (XLSX)
        ocrEngine.ExportToExcel(ocrResult, "YOUR_DIRECTORY/output.xlsx");
    }
}
```

افتح `output.xlsx` وسترى كل سطر من النص المعترف به في صف منفصل، جاهز للتصفية، الصيغ، أو التصورات.

## مثال كامل يعمل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهز للترجمة. استبدل `YOUR_DIRECTORY` بالمسار الفعلي للمجلد الذي توجد فيه صورتك.

```csharp
using Aspose.OCR;
using Aspose.OCR.Configuration;
using System.IO;

class ExportDemo
{
    static void Main()
    {
        // Configure the OCR engine for English language
        var ocrConfig = new OcrEngineConfig { Language = Language.English };
        using var ocrEngine = new OcrEngine(ocrConfig);

        // Recognize text from the input image
        var ocrResult = ocrEngine.RecognizeImage("C:/Data/input.png");

        // Save the recognized plain text (image to txt OCR)
        File.WriteAllText("C:/Data/output.txt", ocrResult.Text);

        // Export the result to JSON (optional)
        File.WriteAllText("C:/Data/output.json", ocrResult.ToJson());

        // Convert image to ePub (requires ExtendedFormats package)
        ocrEngine.ExportToEpub(ocrResult, "C:/Data/output.epub");

        // Export OCR result to Excel (export OCR Excel)
        ocrEngine.ExportToExcel(ocrResult, "C:/Data/output.xlsx");
    }
}
```

### النتيجة المتوقعة

- **output.txt** – نص عادي، مثال: `Hello world! This is a sample image.`  
- **output.json** – JSON يحتوي على إحداثيات مستوى الكلمة ودرجات الثقة.  
- **output.epub** – كتاب إلكتروني قابل للبحث يمكن عرضه في Kindle، Apple Books، إلخ.  
- **output.xlsx** – جدول بيانات حيث يحتوي كل صف على سطر من النص المعترف به.

## المشكلات الشائعة وكيفية تجنبها  

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| حروف مشوشة | PNG منخفض الدقة أو آثار ضغط JPEG | استخدم PNG غير مضغوط بدقة ≥ 300 dpi |
| ملف `output.txt` فارغ | مسار ملف غير صحيح أو نقص في أذونات القراءة | تحقق من وجود المسار وأن التطبيق لديه صلاحيات كتابة |
| لم يتم إنشاء ePub | حزمة NuGet `Aspose.OCR.ExtendedFormats` مفقودة | أضف `dotnet add package Aspose.OCR.ExtendedFormats` |
| خلايا Excel تحتوي على JSON بدلاً من نص عادي | تم استدعاء `ExportToExcel` بطريق الخطأ مع سلسلة JSON | مرّر كائن `OcrResult`، وليس تمثيله بصيغة JSON |

## نصائح احترافية من الميدان  

- **Batch processing:** غلف المنطق الأساسي داخل حلقة `foreach` لمعالجة عشرات الصور في تشغيل واحد.  
- **Language detection:** إذا كنت بحاجة للتعامل مع لغات متعددة، أنشئ قاموسًا من تعداد `Language` واختر المناسب لكل ملف.  
- **Performance tweak:** أعد استخدام نسخة واحدة من `OcrEngine` للدفعة؛ إنشاء نسخة جديدة في كل مرة يضيف عبئًا.  
- **Post‑processing:** نفّذ استبدال regex بسيط على `ocrResult.Text` لتنظيف فواصل الأسطر العشوائية (`\r\n` → ` `) قبل الحفظ إلى TXT.

## الخطوات التالية – إلى أين تذهب من هنا  

الآن بعد أن يمكنك **recognize text image**، **convert image to ePub**، تنفيذ **image to txt OCR**، و**export OCR Excel**، فكر في هذه الإضافات:

- [كيفية استخراج النص من الصورة باستخدام Aspose.OCR لـ .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [تحويل الصورة إلى نص – تنفيذ OCR على صورة من URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}