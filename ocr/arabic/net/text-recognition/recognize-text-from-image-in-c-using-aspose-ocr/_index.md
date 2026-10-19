---
category: general
date: 2026-02-24
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية استخراج
  النص من PNG، تحميل نموذج ONNX في C# واستخراج النص باستخدام Aspose في بضع خطوات فقط.
draft: false
keywords:
- recognize text from image
- how to extract text from png
- load onnx model c#
- extract text using aspose
language: ar
og_description: تعرّف على النص من الصورة بسرعة. يوضح هذا الدليل كيفية استخراج النص
  من ملف PNG، وتحميل نموذج ONNX باستخدام C#، واستخدام Aspose OCR للحصول على نتائج
  خالية من الأخطاء.
og_title: التعرف على النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- ONNX
- Image processing
title: التعرف على النص من الصورة في C# باستخدام Aspose OCR
url: /ar/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# باستخدام Aspose OCR

هل احتجت يومًا إلى **التعرف على النص من صورة** لكن لم تكن متأكدًا أي مكتبة ستتعامل مع خط مخصص؟ لست وحدك—العديد من المطورين يواجهون هذه المشكلة عندما يحتوي PNG على خط مملوك لا تلاحظه محركات OCR الافتراضية.  

في هذا الدرس سنوضح لك بالضبط **كيفية استخراج النص من png** باستخدام Aspose OCR، تحميل نموذج ONNX بأسلوب C#، وأخيرًا **استخراج النص باستخدام Aspose** دون مغادرة بيئة التطوير المتكاملة. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع السلسلة المعترف بها إلى الشاشة.

## ما ستتعلمه

- كيفية تثبيت وإضافة مرجع حزمة Aspose.OCR NuGet.  
- كيفية توجيه محرك OCR إلى نموذج ONNX مخصص (`load onnx model c#`).  
- كيفية تشغيل المحرك على ملف PNG (`how to extract text from png`).  
- نصائح لتصحيح الأخطاء الشائعة (مثل مشاكل مسار النموذج، خصوصيات تنسيق الصورة).  

لا تحتاج إلى خبرة سابقة في ONNX؛ ففهم أساسي لـ C# و .NET يكفي.

---

## المتطلبات المسبقة

| المتطلب | لماذا يهم |
|-------------|----------------|
| .NET 6.0 SDK (أو أحدث) | يوفر بيئة التشغيل لتطبيق الكونسول. |
| Visual Studio 2022 أو VS Code | يسهل التحرير وتصحيح الأخطاء. |
| حزمة Aspose.OCR NuGet (`Install-Package Aspose.OCR`) | توفر `OcrEngine` والفئات ذات الصلة. |
| نموذج ONNX مخصص (`*.onnx`) يعرف الخط الخاص بك | بدون ذلك يعود المحرك إلى النموذج العام وقد يفقد الأحرف. |
| صورة PNG نموذجية تستخدم الخط المخصص | هذا هو الملف الذي سنطبق عليه OCR. |

إذا كان لديك هذه العناصر بالفعل، رائع—لننتقل مباشرة إلى الكود.

---

## الخطوة 1: إعداد المشروع وإضافة Aspose.OCR

للحفاظ على النظام، أنشئ مشروع كونسول جديد:

```bash
dotnet new console -n AsposeOcrDemo
cd AsposeOcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** استخدم العلامة `--framework net6.0` إذا أردت تثبيت المشروع على .NET 6 صراحةً.

---

## الخطوة 2: تحميل نموذج ONNX في C# (load onnx model c#)

الآن سنخبر محرك OCR باستخدام نموذجنا المخصص. خاصية `OcrSettings.CustomModelPath` تتوقع مسارًا مطلقًا أو نسبيًا إلى ملف `.onnx`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create the OCR engine instance
            // -----------------------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // 2️⃣ Point the engine at your custom ONNX model
            // -----------------------------------------------------------------
            ocrEngine.Settings = new OcrSettings
            {
                // Replace with the real location of your model file
                CustomModelPath = @"YOUR_DIRECTORY/my_special_font.onnx"
            };
```

> **لماذا يهم هذا:** بتحميل نموذج ONNX مخصص تمنح المحرك معرفة بأشكال الحروف الدقيقة التي سيواجهها، مما يزيد الدقة بشكل كبير.

---

## الخطوة 3: التعرف على النص من صورة PNG (how to extract text from png)

مع تكوين المحرك، يمكننا الآن تمرير صورة PNG إليه. طريقة `RecognizeImage` تُعيد كائن `OcrResult` يحتوي على النص العادي.

```csharp
            // -----------------------------------------------------------------
            // 3️⃣ Recognize text from the PNG that uses the custom font
            // -----------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/custom_font_image.png";

            // The engine will automatically detect the image format.
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -----------------------------------------------------------------
            // 4️⃣ Show the result in the console
            // -----------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### النتيجة المتوقعة

إذا كانت الصورة تحتوي على العبارة “Hello World” مكتوبة بخطك الخاص، يجب أن يظهر في الكونسول:

```
=== Recognized Text ===
Hello World
```

إذا رأيت أحرفًا مشوشة، تحقق من أن ملف النموذج يطابق نمط الخط وأن صورة PNG غير تالفة.

---

## الخطوة 4: الحالات الخاصة الشائعة وكيفية إصلاحها

### مسار النموذج غير موجود
> *“النظام لا يمكنه العثور على الملف المحدد.”*

- تأكد من أن المسار يستخدم شرطات مائلة مزدوجة (`\\`) على Windows أو سلسلة حرفية (`@"C:\path\to\model.onnx"`).  
- تحقق من أن الملف تم نسخه إلى مجلد الإخراج (`<Project>/bin/Debug/net6.0/`). يمكنك إضافة ذلك إلى ملف `.csproj` الخاص بك:

```xml
<ItemGroup>
  <None Update="my_special_font.onnx">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
  </None>
</ItemGroup>
```

### دقة منخفضة على PNG منخفض الدقة
- قم بزيادة حجم الصورة إلى ما لا يقل عن 300 DPI قبل تمريرها إلى المحرك.  
- استخدم `ocrEngine.Settings.Dpi = 300;` لتسمح لـ Aspose بمعالجة التكبير داخليًا.

### تنسيق صورة غير مدعوم
يدعم Aspose OCR الصيغ PNG، JPEG، BMP، TIFF، و GIF. إذا كان لديك صيغة مختلفة، قم بتحويلها أولاً (مثلاً باستخدام `System.Drawing` أو `ImageSharp`).

---

## الخطوة 5: مثال كامل يعمل (كل الكود في مكان واحد)

فيما يلي البرنامج الكامل جاهز للنسخ واللصق. استبدل مسارات العناصر النائبة بالمسارات الفعلية لديك.

```csharp
// ---------------------------------------------------------------
// Full Example: recognize text from image using Aspose OCR
// ---------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Load your custom ONNX model (load onnx model c#)
            ocrEngine.Settings = new OcrSettings
            {
                CustomModelPath = @"YOUR_DIRECTORY/my_special_font.onnx"
            };

            // 3️⃣ Recognize text from a PNG (how to extract text from png)
            string imagePath = @"YOUR_DIRECTORY/custom_font_image.png";
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 4️⃣ Output the recognized string (extract text using aspose)
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

شغّل البرنامج باستخدام:

```bash
dotnet run
```

يجب أن ترى النص المعترف به مطبوعًا في الكونسول، مما يؤكد أن **التعرف على النص من صورة** يعمل من البداية إلى النهاية.

---

## إضافي: توضيح بصري

![مخطط يوضح التدفق من PNG → نموذج ONNX مخصص → محرك Aspose OCR → مخرجات الكونسول](https://example.com/ocr-flow.png "مخطط تدفق التعرف على النص من صورة")

*نص بديل:* *مخطط يوضح كيفية معالجة PNG عبر نموذج ONNX مخصص باستخدام Aspose OCR.*

---

## الخلاصة

الآن لديك وصفة قوية وجاهزة للإنتاج **للتعرف على النص من صورة** في C# باستخدام Aspose OCR. بتحميل نموذج ONNX مخصص، فتحت القدرة على **استخراج النص من png** التي تستخدم خطوطًا نادرة، ورأيت بالضبط **كيفية استخراج النص باستخدام Aspose** دون أي عناء إضافي.

ما الخطوة التالية؟ جرّب استبدال نموذج ONNX بنموذج لغة أخرى، أو جرب ملفات TIFF متعددة الصفحات، أو دمج استدعاء OCR في واجهة ويب API لمعالجة التحميلات مباشرة. النمط نفسه—إنشاء محرك، ضبط `CustomModelPath`، استدعاء `RecognizeImage`—ينطبق على جميع هذه السيناريوهات.

هل لديك أسئلة حول تحويل النموذج، تحسين الأداء، أو الترخيص؟ اترك تعليقًا أدناه، ونتمنى لك برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}