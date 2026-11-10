---
category: general
date: 2026-03-05
description: كيفية الحصول على OCR بسرعة باستخدام Aspose.OCR والتعرف على النص من التدفق
  في بضع خطوات بسيطة. تعلّم الكود الكامل بلغة C# ونصائح لبث بيانات الصورة.
draft: false
keywords:
- how to get OCR
- recognize text from stream
- Aspose OCR
- streaming OCR C#
- image chunk processing
language: ar
og_description: كيفية الحصول على OCR في C# والتعرف على النص من تدفق باستخدام Aspose.OCR.
  اتبع هذا الدليل خطوة بخطوة للحصول على حل جاهز للتنفيذ.
og_title: كيفية الحصول على OCR في C# – دليل شامل للتعرف على التدفق
tags:
- OCR
- C#
- Aspose
title: كيفية الحصول على OCR في C# – التعرف على النص من الدفق
url: /ar/net/text-recognition/how-to-get-ocr-in-c-recognize-text-from-stream/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية الحصول على OCR في C# – التعرف على النص من تدفق

هل تساءلت يومًا **كيف تحصل على OCR** يعمل في تطبيق .NET دون حفظ الصورة بالكامل على القرص أولاً؟ لست وحدك. يحتاج العديد من المطورين إلى **التعرف على النص من تدفق** — على سبيل المثال عند معالجة الصور التي تصل عبر الشبكة، أو تدفق كاميرا، أو واجهة برمجة تطبيقات التخزين السحابي.

في هذا الدرس سنستعرض مثالًا كاملًا وجاهزًا للتنفيذ يُظهر ذلك بالضبط. في النهاية ستحصل على برنامج C# مستقل يُنشئ محرك Aspose OCR، يبث أجزاء الصورة إليه، ويطبع النص المستخرج على وحدة التحكم. لا أدوات خارجية غامضة، فقط كود واضح وبعض النصائح العملية.

## ما ستتعلمه

- كيفية تثبيت وترخيص مكتبة Aspose.OCR.
- كيفية تغذية بيانات الصورة قطعةً بقطعة باستخدام طريقة `AppendChunk`.
- كيفية بدء وإنهاء دورة التعرف (`BeginRecognize` / `EndRecognize`).
- كيفية التعامل مع الحالات الحدية الشائعة مثل القطع غير المكتملة أو أخطاء الترخيص.
- ما هو شكل المخرجات وكيفية التحقق منها.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).
- ملف ترخيص Aspose OCR صالح (`Aspose.OCR.lic`). يمكنك الحصول على نسخة تجريبية مجانية من موقع Aspose.
- إلمام أساسي بـ C# و `async`/`await` إذا كنت تريد القراءة من تدفق غير متزامن (المثال يستخدم دالة تجريبية متزامنة للتوضيح).

> **لماذا هذا مهم:** يتيح لك OCR المتدفق الحفاظ على استهلاك الذاكرة منخفضًا وتقليل الكمون عند التعامل مع صور كبيرة أو تدفقات فيديو مستمرة. إنه نمط ستراه في ماسحات المستندات الفورية، التطبيقات المحمولة، وسلاسل المعالجة على الخادم.

## الخطوة 1: إعداد المشروع وإضافة Aspose.OCR

أولاً، أنشئ مشروعًا جديدًا من نوع console وأضف حزمة Aspose.OCR من NuGet.

```bash
dotnet new console -n StreamOcrDemo
cd StreamOcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → *Manage NuGet Packages* → ابحث عن “Aspose.OCR” وقم بتثبيت أحدث نسخة مستقرة.

الآن أضف ملف الترخيص إلى جذر المشروع واضبط خاصية **Copy to Output Directory** إلى **Copy always**. هذا يضمن توفر الملف أثناء التشغيل.

```csharp
// Program.cs – top of the file
using System;
using System.IO;
using Aspose.OCR;
```

## الخطوة 2: تهيئة محرك OCR وتطبيق الترخيص

إنشاء المحرك سهل، لكن تطبيق الترخيص **يجب** أن يحدث قبل أي استدعاء للتعرف؛ وإلا ستواجه قيود وضع التجربة.

```csharp
static OcrEngine InitializeOcrEngine()
{
    var engine = new OcrEngine();

    // Load the license – adjust the path if your file lives elsewhere
    string licensePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Aspose.OCR.lic");
    if (!File.Exists(licensePath))
    {
        Console.Error.WriteLine("License file not found at " + licensePath);
        Environment.Exit(1);
    }

    engine.SetLicense(licensePath);
    return engine;
}
```

> **لماذا نفعل ذلك:** ضبط الترخيص مبكرًا يضمن أن جميع استدعاءات API اللاحقة تعمل في وضع كامل المميزات، متجنبًا علامة “إصدار التقييم”.

## الخطوة 3: محاكاة مصدر تدفق

في تطبيق حقيقي ستقرأ من `NetworkStream` أو `FileStream` أو SDK للكاميرا. للعرض، سنحاكي تدفقًا بمساعدة دالة تُعيد مصفوفة بايت تمثل جزء صورة JPEG.

```csharp
static byte[] GetNextChunk()
{
    // Replace this with your actual streaming logic.
    // Here we simply read the whole file and pretend it’s a single chunk.
    string sampleImagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "sample.jpg");
    if (!File.Exists(sampleImagePath))
    {
        Console.Error.WriteLine("Sample image not found at " + sampleImagePath);
        Environment.Exit(1);
    }

    return File.ReadAllBytes(sampleImagePath);
}
```

> **ملاحظة حالة حدية:** إذا استلمت العديد من القطع الصغيرة، يمكنك استدعاء `engine.Image.AppendChunk(chunk)` بشكل متكرر قبل إنهاء التعرف. المحرك يخزن داخليًا حتى يتوفر لديه بيانات كافية لبدء المعالجة.

## الخطوة 4: تغذية بيانات الصورة قطعةً بقطعة وتشغيل OCR

الآن نجمع كل شيء معًا. التسلسل هو:

1. `BeginRecognize()` – يُخبر المحرك أننا على وشك تغذية البيانات.
2. `AppendChunk()` – يضيف كل مصفوفة بايت (يمكنك التكرار على العديد من القطع).
3. `EndRecognize()` – يُشير إلى أن آخر قطعة قد أُرسلت ويُطلق عملية التعرف الفعلية.

```csharp
static string PerformOcr(OcrEngine engine, byte[] imageChunk)
{
    // Start the recognition session
    engine.BeginRecognize();

    // Feed the image data. If you have multiple chunks, call this in a loop.
    engine.Image.AppendChunk(imageChunk);

    // End the session – the engine now processes the accumulated data.
    engine.EndRecognize();

    // Retrieve the result object; .Text holds the plain string.
    return engine.GetResult().Text;
}
```

## الخطوة 5: تجميع كل شيء في `Main`

إليك طريقة `Main` الكاملة التي تُربط كل شيء، تطبع النص المُتعرف عليه، وتُفرغ المحرك بشكل نظيف.

```csharp
static void Main(string[] args)
{
    // 1️⃣ Initialize OCR engine with license
    var ocrEngine = InitializeOcrEngine();

    try
    {
        // 2️⃣ Get a chunk of image data (replace with your streaming source)
        byte[] imageChunk = GetNextChunk();

        // 3️⃣ Run OCR on the streamed data
        string recognizedText = PerformOcr(ocrEngine, imageChunk);

        // 4️⃣ Output the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
    catch (Exception ex)
    {
        // Helpful error handling – you’ll often see OCR exceptions when the image is corrupted.
        Console.Error.WriteLine("OCR failed: " + ex.Message);
    }
    finally
    {
        // Release any native resources held by the engine.
        ocrEngine.Dispose();
    }
}
```

### الناتج المتوقع

إذا كان `sample.jpg` يحتوي على العبارة “Hello, World!” يجب أن ترى:

```
=== Recognized Text ===
Hello, World!
```

إذا كانت الصورة غير واضحة أو القطعة غير مكتملة، قد يكون الناتج فارغًا أو يحتوي على أحرف مشوشة – لهذا السبب يُعد التعامل السليم مع القطع (التأكد من إرسال آخر قطعة) أمرًا حاسمًا.

## معالجة عدة قطع (متقدم)

عند التعامل مع بيانات تدفق حقيقية، من المحتمل أن تستقبل العديد من القطع الصغيرة. النمط أدناه يُظهر كيفية التكرار حتى ينتهي المصدر.

```csharp
static string OcrFromStream(OcrEngine engine, Stream source)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192]; // 8 KB per read – adjust as needed
    int bytesRead;
    while ((bytesRead = source.Read(buffer, 0, buffer.Length)) > 0)
    {
        // If the last read returned fewer bytes, copy only that many.
        if (bytesRead < buffer.Length)
        {
            byte[] chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

> **لماذا هذا مفيد:** من خلال البث مباشرةً من `NetworkStream` أو `FileStream`، لا تقوم بتحميل الصورة بالكامل في الذاكرة، وهو ما يكون مفيدًا خاصةً للملفات PDF الكبيرة أو الصور عالية الدقة.

## المشكلات الشائعة وكيفية تجنبها

| المشكلة | العَرَض | الحل |
|---------|----------|-----|
| الترخيص غير موجود | `SetLicense` يطرح استثناء `FileNotFoundException` | تحقق من المسار واضبط *Copy to Output Directory* إلى *Copy always*. |
| نتيجة فارغة | لم يُطبع أي نص | تأكد من استدعاء `BeginRecognize` **قبل** `AppendChunk` و `EndRecognize` **بعد** آخر قطعة. |
| تسرب الذاكرة | يتباطأ التطبيق بعد العديد من استدعاءات OCR | قم بتحرير `OcrEngine` بعد كل استخدام أو أعد استخدام نسخة واحدة مع استدعاءات `Dispose` الصحيحة. |
| قطعة تالفة | أحرف مشوشة | تحقق من حجم القطعة؛ بالنسبة لـ JPEG/PNG يجب أن تبدأ البايتات الأولى بـ `0xFF 0xD8` أو `0x89 0x50`. |

## المكافأة: استخدام التدفقات غير المتزامنة

إذا كان مصدر البيانات هو تدفق استجابة `HttpClient`، يمكنك تعديل الحلقة لتستخدم `await` للقراءات:

```csharp
static async Task<string> OcrFromAsyncStream(OcrEngine engine, Stream asyncSource)
{
    engine.BeginRecognize();

    byte[] buffer = new byte[8192];
    int bytesRead;
    while ((bytesRead = await asyncSource.ReadAsync(buffer, 0, buffer.Length)) > 0)
    {
        if (bytesRead < buffer.Length)
        {
            var chunk = new byte[bytesRead];
            Array.Copy(buffer, chunk, bytesRead);
            engine.Image.AppendChunk(chunk);
        }
        else
        {
            engine.Image.AppendChunk(buffer);
        }
    }

    engine.EndRecognize();
    return engine.GetResult().Text;
}
```

## الخلاصة

أنت الآن تمتلك **حلًا كاملًا ومستقلاً لكيفية الحصول على OCR** في C# و **التعرف على النص من تدفق** باستخدام Aspose.OCR. غطى الدرس كل شيء من الترخيص والتهيئة إلى تغذية قطع الصورة، التعامل مع الحالات الحدية، وحتى النسخة غير المتزامنة.

جرّبه—استبدل `sample.jpg` بتدفق كاميرا مباشر، صورة مخزنة سحابيًا، أو تحميل متعدد الأجزاء عبر HTTP. بمجرد أن تشعر بالراحة، استكشف الميزات المتقدمة مثل حزم اللغات، المعالجة المسبقة المخصصة، أو المعالجة الدفعية لعدة تدفقات.

**الخطوات التالية:**  
- جرّب OCR على ملفات PDF بتحويل كل صفحة إلى صورة أولاً.  
- جرّب `engine.Config` لتحسين الدقة للخطوط المحددة.  
- ادمج ذلك مع Azure Functions أو AWS Lambda لإنشاء خطوط استخراج نص بدون خادم.

برمجة سعيدة، ولتكن تدفقاتك دائمًا واضحة ونتائج OCR خالية من العيوب!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}