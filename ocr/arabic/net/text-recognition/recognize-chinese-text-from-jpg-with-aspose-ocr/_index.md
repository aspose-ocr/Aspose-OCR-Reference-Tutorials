---
category: general
date: 2026-04-08
description: تعلم كيفية التعرف على النص الصيني من صور JPG باستخدام Aspose OCR. يوضح
  لك هذا الدليل خطوة بخطوة أيضًا كيفية استخراج النص من الصورة بسرعة.
draft: false
keywords:
- recognize chinese text
- extract text from image
- recognize text from jpg
- Aspose OCR C#
- offline OCR resources
language: ar
og_description: التعرف على النص الصيني من صور JPG باستخدام Aspose OCR. اتبع هذا الدليل
  الكامل لاستخراج النص من الصورة دون اتصال.
og_title: التعرف على النص الصيني من JPG باستخدام Aspose OCR
tags:
- OCR
- C#
- Aspose
title: التعرف على النص الصيني من JPG باستخدام Aspose OCR
url: /ar/net/text-recognition/recognize-chinese-text-from-jpg-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص الصيني من JPG باستخدام Aspose OCR

هل احتجت يومًا إلى **التعرف على النص الصيني** من ملف JPG لكن لم تكن متأكدًا من أين تبدأ؟ لست وحدك—العديد من المطورين يواجهون هذه العقبة عند بناء تطبيقات مسح متعددة اللغات. الخبر السار هو أن Aspose OCR يجعل الأمر سهلًا للغاية، حتى عندما تحتاج إلى العمل دون اتصال.

في هذا الدرس سنستعرض العملية الكاملة لاستخراج النص من صورة، بأسلوب **extract text from image**، وسنوضح لك بالضبط كيفية **recognize text from jpg** باستخدام C#. في النهاية ستحصل على برنامج قابل للتنفيذ يقرأ صورة باللغة الصينية ويطبع الأحرف التي تم التعرف عليها في وحدة التحكم.

## ما ستحتاجه

- .NET 6.0 أو أحدث (أي نسخة حديثة تعمل)
- حزمة NuGet الخاصة بـ Aspose.OCR (`Install-Package Aspose.OCR`)
- ملف موارد اللغة الصينية (يظهر الدرس كيفية تحميله دون اتصال)
- ملف صورة باسم `chinese_sample.jpg` موجود في مجلد تتحكم فيه

لا تحتاج إلى حيل متقدمة في بيئة التطوير—Visual Studio أو Rider أو حتى VS Code كافية.

## الخطوة 1: إعداد المشروع وتثبيت Aspose OCR

أولاً، أنشئ مشروع وحدة تحكم جديد واستورد مكتبة Aspose OCR.

```bash
dotnet new console -n ChineseOcrDemo
cd ChineseOcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت خلف بروكسي مؤسسي، أضف العلامة `--no-cache` لإجبار تحميل نسخة جديدة.

## الخطوة 2: تعطيل تحميل الموارد تلقائيًا

يمكن لـ Aspose OCR جلب حزم اللغات عند الحاجة، لكن في بيئة الإنتاج عادةً ما تريد تضمين الملفات مع تطبيقك. تعطيل التحميل التلقائي يمنع المكالمات الشبكية غير المتوقعة.

```csharp
using Aspose.Ocr;

// Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Turn off the auto‑download feature
ocrEngine.Options.EnableAutomaticResourceDownload = false;
```

لماذا نفعل ذلك؟ الحفاظ على الموارد محليًا يضمن أداءً ثابتًا ويسمح لك بتشغيل التطبيق على أجهزة بدون اتصال بالإنترنت.

## الخطوة 3: تحميل موارد اللغة الصينية دون اتصال

تُرسل Aspose بيانات اللغة كملفات منفصلة. بافتراض أنك وضعت حزمة اللغة الصينية (`zh`) في مجلد `Resources` بجوار الملف التنفيذي، قم بتحميلها هكذا:

```csharp
// Path to the folder that contains the language files
string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");

// Tell the engine where to look for resources
ocrEngine.Options.ResourcesFolder = resourcePath;

// Load the Simplified Chinese resources (offline = true)
ocrEngine.LoadLanguageResources("zh", offline: true);
```

> **احذر:** إذا كان المسار غير صحيح، ستحصل على استثناء `FileNotFoundException`. تحقق مرة أخرى من اسم المجلد وحساسية الأحرف في نظام Linux.

## الخطوة 4: تعيين لغة المحرك إلى الصينية

الآن بعد تحميل البيانات، وجه المحرك إلى رمز اللغة الصحيح.

```csharp
ocrEngine.Language = "zh"; // “zh” = Simplified Chinese
```

تعيين اللغة صراحةً يحسن الدقة لأن الـ OCR لن يضيع الوقت في تخمين النصوص.

## الخطوة 5: التعرف على النص من صورة JPG

هذا هو جوهر الدرس—إعطاء صورة JPG للمحرك واستخراج النص.

```csharp
// Full path to the image you want to process
string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");

// Run the OCR operation
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

// Output the raw result
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

إذا سارت الأمور بسلاسة، ستعرض وحدة التحكم الأحرف الصينية الموجودة في `chinese_sample.jpg`. يمكنك أيضًا الوصول إلى `ocrResult.Confidence` للحصول على مقياس الجودة.

## الخطوة 6: مثال كامل يعمل

جمع كل الأجزاء معًا يمنحك برنامجًا جاهزًا للتنفيذ. احفظه كـ `Program.cs` داخل مجلد مشروعك.

```csharp
using System;
using System.IO;
using Aspose.Ocr;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Disable automatic resource download
        // -------------------------------------------------
        ocrEngine.Options.EnableAutomaticResourceDownload = false;

        // -------------------------------------------------
        // 3️⃣ Load Chinese language resources (offline)
        // -------------------------------------------------
        string resourcePath = Path.Combine(AppContext.BaseDirectory, "Resources");
        ocrEngine.Options.ResourcesFolder = resourcePath;
        ocrEngine.LoadLanguageResources("zh", offline: true);

        // -------------------------------------------------
        // 4️⃣ Set language to Simplified Chinese
        // -------------------------------------------------
        ocrEngine.Language = "zh";

        // -------------------------------------------------
        // 5️⃣ Recognize text from a JPG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppContext.BaseDirectory, "chinese_sample.jpg");
        OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

        // -------------------------------------------------
        // 6️⃣ Show the result
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine($"\nConfidence: {ocrResult.Confidence:P2}");
    }
}
```

### النتيجة المتوقعة

```
=== Recognized Chinese Text ===
欢迎使用Aspose OCR示例
Confidence: 96.45%
```

ستختلف النتيجة الدقيقة حسب صورة المصدر، لكن يجب أن ترى مجموعة من الأحرف الصينية متبوعة بنسبة الثقة.

## الخطوة 7: الاختلافات الشائعة وحالات الحافة

### التعرف على النص من PNG أو BMP

طريقة `RecognizeImage` تقبل أي صيغة يدعمها `System.Drawing` في .NET. فقط غيّر امتداد الملف:

```csharp
ocrEngine.RecognizeImage("sample.png");
```

### التعامل مع لغات متعددة

إذا كنت بحاجة إلى **extract text from image** التي تمزج بين الإنجليزية والصينية، قم بتحميل حزم اللغتين واضبط `ocrEngine.Language = "zh,en";`. سيقوم المحرك بالتبديل تلقائيًا بين النصوص.

### التعامل مع الصور منخفضة الدقة

قيمة DPI منخفضة يمكن أن تضعف دقة الـ OCR. قبل استدعاء `RecognizeImage`، قد تحتاج إلى تكبير الصورة:

```csharp
using System.Drawing;

Bitmap bmp = new Bitmap(imagePath);
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
highRes.Save("highres.jpg");
ocrResult = ocrEngine.RecognizeImage("highres.jpg");
```

تذكر أن التكبير لا يضيف تفاصيل سحرية، لكنه قد يمنح الخوارزمية المزيد من البكسلات للعمل معها.

## الخطوة 8: الاختبار والتحقق

فحص سريع للتأكد هو مقارنة ناتج الـ OCR مع سلسلة معرفة مسبقًا.

```csharp
string expected = "欢迎使用Aspose OCR示例";
bool matches = ocrResult.Text.Trim() == expected;
Console.WriteLine($"Match with expected? {matches}");
```

إذا كان `matches` يساوي `false`، فكر في تعديل الصورة (مثلاً زيادة التباين) أو تمكين `ocrEngine.Options.UseAdvancedPreprocessing = true`.

## الخلاصة

لقد تعلمت الآن كيفية **recognize chinese text** من ملف JPG باستخدام Aspose OCR، وتعرفت أيضًا على كيفية **extract text from image** في سيناريو كامل دون اتصال. الحل الكامل—التهيئة، تحميل الموارد، اختيار اللغة، ومعالجة الصورة—يتضمنه برنامج وحدة تحكم واحد سهل التشغيل.

ما الخطوة التالية؟ جرّب تمرير مجموعة من الصور إلى نفس المحرك، جرب حزم لغات مختلفة، أو دمج خطوة الـ OCR في واجهة برمجة تطبيقات ASP .NET Web API بحيث يمكن للمستخدمين رفع الصور والحصول على النص المترجم فورًا. لا حدود لما يمكنك تحقيقه عندما تجمع بين OCR موثوق وأدوات .NET الحديثة.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي صعوبات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}