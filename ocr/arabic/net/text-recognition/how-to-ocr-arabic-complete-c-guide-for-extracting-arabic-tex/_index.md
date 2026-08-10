---
category: general
date: 2026-02-25
description: كيفية إجراء OCR للغة العربية في C# باستخدام Aspose.OCR. تعلّم كيفية تحميل
  الصورة للتعرف الضوئي، تحويل صورة النص العربي، والتعرف على الأحرف العربية في دقائق.
draft: false
keywords:
- how to ocr arabic
- extract arabic text
- load image for ocr
- convert image arabic text
- recognize arabic characters
language: ar
og_description: كيفية التعرف الضوئي على النص العربي فورًا. اتبع هذا الدليل لتحميل
  الصورة للتعرف الضوئي، تحويل النص العربي في الصورة واستخراج الأحرف العربية باستخدام
  Aspose.OCR.
og_title: كيفية التعرف الضوئي على العربية – دليل C# خطوة بخطوة
tags:
- OCR
- C#
- Aspose
title: كيفية التعرف الضوئي على العربية – دليل C# الكامل لاستخراج النص العربي
url: /ar/net/text-recognition/how-to-ocr-arabic-complete-c-guide-for-extracting-arabic-tex/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على الأحرف العربية – دليل C# الكامل لاستخراج النص العربي

هل تساءلت يومًا **how to OCR Arabic** من صورة لعلامة شارع دون قضاء ساعات في تعديل الإعدادات؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يتحول اتجاه اللغة إلى اليمين‑إلى‑اليسار ولا تكون مجموعة الأحرف لاتينية. الخبر السار؟ مع Aspose.OCR يمكنك **load image for OCR**، **convert image arabic text**، و **recognize arabic characters** في بضع أسطر فقط من C#.

في هذا الدليل سنستعرض كل ما تحتاجه لتحويل صورة PNG لعلامة عربية إلى سلسلة نصية نظيفة يمكنك تخزينها أو البحث فيها أو ترجمتها. في النهاية ستتمكن من **extract arabic text** من أي صورة نقطية، وفهم لماذا كل إعداد مهم، ورؤية مثال شفرة جاهز للتنفيذ يمكنك إضافته إلى مشروعك اليوم.

## ما الذي ستحتاجه

قبل أن نبدأ، تأكد من وجود ما يلي:

- .NET 6.0 أو أحدث (تعمل الواجهة البرمجية مع .NET Core و .NET Framework أيضًا)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)
- حزمة Aspose.OCR عبر NuGet (`Aspose.OCR`) مثبتة في مشروعك
- صورة نموذجية تحتوي على أحرف عربية، مثل `arabic_sign.png`

لا تحتاج إلى محركات OCR إضافية، ولا إلى خدمات خارجية—فقط مكتبة Aspose وبعض الأسطر البرمجية.

## الخطوة 1: تثبيت حزمة Aspose.OCR عبر NuGet

للبدء، أضف Aspose.OCR إلى مشروعك. افتح وحدة تحكم مدير الحزم واكتب:

```powershell
Install-Package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم .NET CLI، فإن الأمر المكافئ هو `dotnet add package Aspose.OCR`. هذا يضمن حصولك على أحدث نسخة (حالياً 23.11) التي تتضمن تحسينات في معالجة الأحرف العربية.

## الخطوة 2: تهيئة محرك OCR

إنشاء كائن `OcrEngine` هو الخطوة الأولى الملموسة نحو **recognize arabic characters**. فكر في المحرك كالعقل الذي سيفسر البكسلات لاحقًا.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

public class ArabicOcrDemo
{
    public static void Run()
    {
        // Step 2: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

لماذا نقوم بإنشاء المحرك *قبل* تحميل الصورة؟ يحتفظ المحرك ببيانات التكوين—مثل إعدادات اللغة—التي يجب تطبيقها قبل أي معالجة للصورة. تخطي هذا الترتيب قد يؤدي إلى رجوع OCR إلى النموذج الافتراضي للإنجليزية، والذي لن يتعرف على الأحرف العربية بشكل صحيح.

## الخطوة 3: ضبط المحرك للغة العربية

تأتي Aspose.OCR مع العديد من حزم اللغات، لكن عليك إخبارها أي واحدة تريد استخدامها. ضبط `OcrLanguage.Arabic` يبدل المعرّف الداخلي إلى النص من اليمين إلى اليسار ويحمّل جداول الأحرف المناسبة.

```csharp
        // Step 3: Configure the engine to recognize Arabic text
        ocrEngine.Config.Language = OcrLanguage.Arabic;
```

> **لماذا هذا مهم:** الأحرف العربية لها أشكال سياقية (أولية، وسطية، نهائية، منفصلة). نموذج اللغة العربية يعرف كيف يربط هذه الأشكال معًا، بينما النموذج العام سيعامل كل حرف كرمز غير معروف.

## الخطوة 4: تحميل الصورة لـ OCR

الآن نقوم فعليًا بـ **load image for OCR**. توفر Aspose طريقة مريحة `ImageStream.FromFile` التي تقرأ الصورة النقطية إلى الذاكرة.

```csharp
        // Step 4: Load the image containing Arabic characters
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.png");
```

إذا كانت صورتك موجودة في مجلد مختلف أو استلمتها كمصفوفة بايت (مثلاً من رفع ويب)، يمكنك استبدال مسار الملف بـ stream:

```csharp
        // Alternative: load from a byte[] (useful for web APIs)
        // byte[] imageBytes = ...;
        // ocrEngine.Image = ImageStream.FromBytes(imageBytes);
```

> **حالة خاصة:** تأكد أن الصورة بدقة لا تقل عن 300 dpi؛ الصور منخفضة الدقة غالبًا ما تؤدي إلى فقدان الأحرف. يمكنك تكبيرها باستخدام `System.Drawing` قبل تمريرها إلى المحرك إذا لزم الأمر.

## الخطوة 5: تنفيذ OCR و **extract arabic text**

مع جاهزية المحرك والصورة في الذاكرة، نصل أخيرًا إلى **convert image arabic text** إلى سلسلة نصية. طريقة `Recognize` تقوم بالعمل الشاق.

```csharp
        // Step 5: Perform OCR recognition
        var ocrResult = ocrEngine.Recognize();
```

كائن `ocrResult` يحتوي على عدة خصائص مفيدة، لكن ما يهمنا هو `Text`. هنا يتواجد ناتج **extract arabic text**.

```csharp
        // Step 6: Display the recognized Arabic text
        Console.WriteLine("Arabic text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### النتيجة المتوقعة

إذا كانت `arabic_sign.png` تحتوي على العبارة “مرحبا بالعالم”، سيطبع الطرفية:

```
Arabic text:
مرحبا بالعالم
```

لاحظ كيف تحافظ النتيجة تلقائيًا على ترتيب النص من اليمين إلى اليسار—Aspose تتعامل مع تخطيط bidi (ثنائي الاتجاه) نيابةً عنك.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في تطبيق Console جديد. يتضمن جميع الخطوات، توجيهات `using` المناسبة، وقليل من معالجة الأخطاء.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace ArabicOcrSample
{
    class Program
    {
        static void Main(string[] args)
        {
            try
            {
                // Initialize the OCR engine
                OcrEngine ocrEngine = new OcrEngine();

                // Set Arabic as the target language
                ocrEngine.Config.Language = OcrLanguage.Arabic;

                // Load the image you want to process
                string imagePath = "YOUR_DIRECTORY/arabic_sign.png";
                ocrEngine.Image = ImageStream.FromFile(imagePath);

                // Run the recognition
                var result = ocrEngine.Recognize();

                // Output the extracted Arabic text
                Console.WriteLine("Arabic text:");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

شغّل المشروع (`dotnet run` أو اضغط **F5** في Visual Studio) وسترى السلسلة العربية مطبوعة في الطرفية.

## الأخطاء الشائعة وكيفية تجنّبها

| المشكلة | السبب | الحل |
|-------|----------------|-----|
| **حروف غير مفهومة** | DPI الصورة منخفض أو خلفية صاخبة | معالجة مسبقة للصورة: زيادة التباين، تطبيق التثبيت الثنائي |
| **نتيجة فارغة** | ضبط لغة غير صحيح (الافتراضي هو الإنجليزية) | دائمًا اضبط `ocrEngine.Config.Language = OcrLanguage.Arabic` قبل `Recognize()` |
| **نص جزئي** | الصورة تحتوي على لغات مختلطة دون تقسيم صحيح | استخدم `ocrEngine.Config.MultiLanguage = true` وحدد لغة احتياطية |
| **بطء الأداء** | صورة كبيرة (مثلاً >5 MP) تُعالج على خيط الواجهة | انقل OCR إلى مهمة خلفية (`Task.Run`) |

## الخطوات التالية: ما بعد الاستخراج البسيط

الآن بعد أن أتقنت **how to OCR Arabic**، قد ترغب في:

- **تخزين النص المستخرج** في قاعدة بيانات لفهرسة البحث.
- **ترجمة** السلسلة العربية باستخدام Azure Cognitive Services أو واجهات برمجة تطبيقات Google Translate.
- **معالجة دفعات** لمجلد من الصور باستخدام حلقة `foreach` وتوازي (`Parallel.ForEach`).
- **دمج لغات أخرى** بإضافة `ocrEngine.Config.MultiLanguage = true` وتضمين `OcrLanguage.English`.

كل من هذه الإضافات يبنى على النمط الأساسي الذي غطيناه: التهيئة، الضبط، التحميل، التعرف، والاستهلاك.

## الخلاصة

استعرضنا كامل سير عمل **how to OCR Arabic**—من تثبيت Aspose.OCR إلى **recognize arabic characters** و **extract arabic text** من ملف PNG. النقاط الأساسية هي:

1. ضبط اللغة إلى العربية **قبل** تحميل الصورة.  
2. استخدام مصدر عالي الدقة أو معالجة مسبقة للصور منخفضة الجودة.  
3. طريقة `Recognize()` تُعيد خاصية `Text` التي تحترم ترتيب النص من اليمين إلى اليسار تلقائيًا.

جرّبها مع صورك الخاصة، عدّل الـ DPI، وجرب المعالجة الدفعية. بمجرد أن تشعر بالراحة، يصبح دمج OCR في أنظمة أكبر (مثل إدارة المستندات أو خطوط الترجمة) أمرًا سهلًا.

---

![Screenshot showing how to OCR Arabic output in console](/images/ocr-arabic-output.png "how to OCR Arabic example")

*نص بديل للصورة: مثال ناتج OCR للغة العربية في الطرفية*

لا تتردد في ترك تعليق إذا واجهت أي صعوبة أو اكتشفت طريقة معالجة مسبقة ذكية. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}