---
category: general
date: 2026-04-06
description: كيفية استخدام OCR في C# لاستخراج النص العادي من صور JPG، بما في ذلك الأحرف
  السيريلية. تعلم كيفية تحميل الصورة للتعرف الضوئي على الأحرف، التعرف على نص JPG والحصول
  على نتائج موثوقة.
draft: false
keywords:
- how to use OCR
- extract plain text
- extract cyrillic text
- recognize text jpg
- load image for OCR
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص العادي من ملفات JPG. يوضح هذا
  الدليل كيفية تحميل الصورة للتعرف الضوئي على الأحرف، والتعرف على نص JPG، ومعالجة
  النص السيريلي.
og_title: كيفية استخدام OCR في C# – استخراج النص العادي من الصور
tags:
- C#
- OCR
- Aspose
- Image Processing
title: كيفية استخدام OCR في C# – استخراج النص العادي من الصور
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-plain-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص العادي من الصور

هل تساءلت يومًا **كيفية استخدام OCR** في مشروع .NET دون الحاجة للمعركة مع المكتبات الأصلية؟ ربما لديك مجلد يحتوي على إيصالات ممسوحة ضوئيًا، أو مجموعة من لقطات الشاشة ذات التسميات السيريالية، أو فقط تحتاج لاستخراج النص من صورة JPEG للتحليل السريع. الخبر السار هو أن Aspose OCR يجعل هذه العملية سهلة كقطعة من الكعك.

في هذا الدرس سنستعرض مثالًا كاملاً وقابلًا للتنفيذ يُظهر **كيفية استخدام OCR** لـ **استخراج النص العادي** من صورة JPEG، وكيفية **تحميل الصورة لـ OCR**، وحتى كيفية **استخراج النص السيريالي** عندما لا تكون لغة المصدر لاتينية. في النهاية ستحصل على تطبيق console صغير يطبع النص المُتعرف عليه مباشرةً في وحدة التحكم—بدون ملفات إضافية، دون تأثيرات جانبية غامضة.

> **ما ستحصل عليه**  
> * دليل خطوة بخطوة يمكنك نسخه ولصقه في Visual Studio.  
> * شروحات *لماذا* كل سطر مهم، وليس فقط *ماذا* يفعل.  
> * نصائح للتعامل مع الصور الكبيرة، واللغات المتعددة، والمشكلات الشائعة.

## المتطلبات المسبقة

* .NET 6 SDK أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا).  
* Visual Studio 2022 (أو أي محرر تفضله).  
* اتصال بالإنترنت في المرة الأولى التي تشغل فيها العينة—Aspose OCR يقوم بتنزيل حزم اللغات عند الطلب.

إذا كنت تفتقد حزمة Aspose OCR عبر NuGet، سنغطي ذلك في الخطوة الأولى.

## الخطوة 1 – تثبيت Aspose OCR عبر NuGet (ولماذا يهم ذلك)

لا يمكن تنفيذ خطوة **تحميل الصورة لـ OCR** حتى تكون المكتبة موجودة. استخدام NuGet يضمن حصولك على أحدث الملفات الثنائية المحدثة أمانًا ويجلب تلقائيًا أي تبعيات مطلوبة.

```bash
dotnet add package Aspose.OCR
```

*لماذا يهم ذلك*: Aspose OCR يأتي مع DLL أساسي صغير ويسحب بيانات اللغة فقط عندما تطلبها. هذا يحافظ على خفة تطبيقك ويتجنب تجميع ميغابايتات من ملفات اللغات غير المستخدمة.

## الخطوة 2 – تهيئة محرك OCR (قلب **كيفية استخدام OCR**)

إنشاء نسخة من `OcrEngine` هو أول سطر حقيقي من الكود يهم **كيفية استخدام OCR**. المحرك يضع افتراضيًا على وضع “حسب الطلب”، مما يعني أنه سيقوم بتنزيل حزمة اللغة في المرة الأولى التي تطلب فيها لغة محددة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Step 2: Create the engine – it will fetch language data when needed.
var ocrEngine = new OcrEngine();
```

> **نصيحة احترافية**: إذا كنت تعمل خلف بروكسي مؤسسي، قم بتعيين `OcrEngine.Proxy` قبل أول استدعاء للتعرف حتى ينجح التحميل.

## الخطوة 3 – اختيار اللغة – **استخراج النص السيريالي** عند الحاجة

Aspose OCR يدعم العشرات من الأنظمة الكتابية. لاستخراج **النص السيريالي**، قم ببساطة بتعيين خاصية `Language` إلى `OcrLanguage.Cyrillic`. في المرة الأولى التي يُنفّذ فيها هذا السطر، يتم سحب وحدة السيريالي (≈ 5 MB) من شبكة CDN الخاصة بـ Aspose.

```csharp
// Step 3: Tell the engine which language to look for.
// This will automatically download the Cyrillic language pack on first use.
ocrEngine.Language = OcrLanguage.Cyrillic;
```

إذا كانت صورتك تحتوي على أحرف لاتينية فقط، يمكنك استبدال `Cyrillic` بـ `English`. نفس النمط يعمل مع أي لغة مدعومة.

## الخطوة 4 – **تحميل الصورة لـ OCR** – من القرص أو من تدفق

الآن نقوم فعليًا **بتحميل الصورة لـ OCR**. فئة `System.Drawing.Image` تتعامل مع معظم الصيغ الشائعة (JPG، PNG، BMP). إذا كنت على منصة غير Windows، فكر في استخدام `ImageSharp` بدلاً منها، لكن لهذا الدرس النوع المدمج يكفي.

```csharp
using System.Drawing;

// Step 4: Load the picture that holds the text.
using var image = Image.FromFile(@"C:\Images\cyrillic_sample.jpg");
```

> **لماذا يهم ذلك**: تحميل الصورة داخل كتلة `using` يضمن تحرير موارد GDI+ غير المُدارة بسرعة، مما يمنع تسرب الذاكرة في الخدمات التي تعمل لفترات طويلة.

## الخطوة 5 – **التعرف على نص JPG** – تشغيل عملية OCR

مع تكوين المحرك وتحميل الصورة، ن finally **نتعرف على نص jpg**. طريقة `Recognize` تُرجع كائن `OcrResult` يحتوي على السلسلة النصية العادية، درجات الثقة، وحتى إطارات الحدود إذا احتجتها لاحقًا.

```csharp
// Step 5: Perform the recognition.
var ocrResult = ocrEngine.Recognize(image);
```

إذا رغبت في تحسين الدقة، يمكنك تعديل `ocrEngine.Config` (مثلاً، تمكين `AutoRotate` أو تعيين `TextOrientation`). بالنسبة لمعظم السيناريوهات البسيطة، الإعدادات الافتراضية تعمل بشكل مفاجئ جيد.

## الخطوة 6 – **استخراج النص العادي** – عرض النتيجة

الجزء الأخير من **كيفية استخدام OCR** هو استخراج السلسلة المتعرف عليها من `ocrResult` والقيام بشيء بها. هنا نكتبها ببساطة إلى وحدة التحكم، مما يوضح أيضًا كيفية **استخراج النص العادي** من كائن النتيجة.

```csharp
// Step 6: Output the plain text to the console.
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrResult.Text);
```

### النتيجة المتوقعة

إذا كان ملف `cyrillic_sample.jpg` يحتوي على العبارة “Привет мир” (مرحبًا بالعالم)، يجب أن ترى:

```
=== Recognized Text ===
Привет мир
```

إذا كانت الصورة غير واضحة أو النص صغير جدًا، قد يحتوي الناتج على أخطاء؛ يمكنك فحص `ocrResult.Confidence` لتقرر ما إذا كنت ستعيد المحاولة باستخدام مصدر بدقة أعلى.

## مثال كامل وجاهز للتنفيذ

فيما يلي البرنامج الكامل. انسخه إلى مشروع تطبيق Console جديد (`dotnet new console`) وشغّله. لا تحتاج إلى ملفات إضافية بخلاف الصورة التي تشير إليها.

```csharp
// ---------------------------------------------------------------
// How to Use OCR in C# – Complete Example
// ---------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet first (dotnet add package Aspose.OCR)

        // 2️⃣ Initialize the OCR engine – on‑demand language download.
        var ocrEngine = new OcrEngine();

        // 3️⃣ Select Cyrillic to **extract Cyrillic text**.
        ocrEngine.Language = OcrLanguage.Cyrillic;

        // 4️⃣ **Load image for OCR** – change the path to your own file.
        using var image = Image.FromFile(@"YOUR_DIRECTORY\cyrillic_sample.jpg");

        // 5️⃣ **Recognize text jpg** – run the engine.
        var ocrResult = ocrEngine.Recognize(image);

        // 6️⃣ **Extract plain text** – display it.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **ملاحظة**: استبدل `YOUR_DIRECTORY\cyrillic_sample.jpg` بالمسار الفعلي لملف JPEG الخاص بك.

## أسئلة شائعة وحالات حافة

### ماذا لو احتجت إلى **التعرف على نص jpg** من تدفق بدلاً من ملف؟

يمكنك تمرير `MemoryStream` مباشرةً:

```csharp
using var ms = new MemoryStream(File.ReadAllBytes("myImage.jpg"));
using var img = Image.FromStream(ms);
var result = ocrEngine.Recognize(img);
```

### كيف أتعامل مع لغات متعددة في نفس الصورة؟

قم بتعيين `ocrEngine.Language` إلى `OcrLanguage.Multilingual`. سيحاول المحرك اكتشاف كل نظام كتابة تلقائيًا، وهو مفيد عندما يخلط الإيصال بين الإنجليزية والسيريالية.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

### صوريّة ضخمة (أكثر من 5 MP). هل سيتعطل المحرك؟

الصور الكبيرة تزيد من استهلاك الذاكرة ويمكن أن تبطئ عملية التعرف. إعادة تحجيم سريعة مسبقًا تساعد:

```csharp
var resized = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
var result = ocrEngine.Recognize(resized);
```

### هل يمكنني الحصول على درجة الثقة لكل سطر؟

نعم—`ocrResult.Lines` يحتوي على `Confidence` لكل سطر. التكرار عبرها يتيح لك تصفية النتائج ذات الثقة المنخفضة.

```csharp
foreach (var line in ocrResult.Lines)
{
    if (line.Confidence > 0.8)
        Console.WriteLine(line.Text);
}
```

## نصائح احترافية لـ OCR جاهز للإنتاج

* **تخزين حزم اللغات مؤقتًا** – التنزيل الأول قد يستغرق بضع ثوانٍ؛ احفظ الملفات في مجلد معروف واضبط `ocrEngine.LanguageDataPath` لإعادة استخدامها.  
* **المعالجة الدفعية** – أعد استخدام نسخة واحدة من `OcrEngine` للعديد من الصور؛ إنشاء محرك جديد لكل ملف يضيف عبئًا غير ضروري.  
* **معالجة الأخطاء** – غلف استدعاء `Recognize` بكتلة try/catch. Aspose يطرح `OcrException` للصور التالفة أو الصيغ غير المدعومة.  
* **التسجيل** – سجّل `ocrResult.Confidence` لتتمكن لاحقًا من تدقيق الصفحات التي احتاجت مراجعة يدوية.

## الخلاصة

لقد غطينا للتو **كيفية استخدام OCR** في C# لـ **استخراج النص العادي** من صورة JPEG، وأظهرنا الخطوات لـ **تحميل الصورة لـ OCR**، وبيّنّا كيفية **التعرف على نص jpg**، وحتى استخراج **النص السيريالي** من الصورة. العينة تعمل بالكامل، وتحتاج فقط إلى حزمة NuGet واحدة، ويمكن توسيعها للتعامل مع مستندات متعددة اللغات، أو وظائف دفعية، أو سيناريوهات المسح في الوقت الحقيقي.

هل أنت مستعد للتحدي التالي؟ جرّب استبدال اللغة السيريالية بالعربية، جرب علم `AutoRotate`، أو دمج الناتج في فهرس بحث. الاحتمالات لا حصر لها

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}