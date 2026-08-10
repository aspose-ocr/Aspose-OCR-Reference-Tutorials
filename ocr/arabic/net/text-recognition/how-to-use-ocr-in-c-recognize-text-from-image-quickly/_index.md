---
category: general
date: 2026-02-16
description: كيفية استخدام OCR في C# للتعرف على النص من الصورة، استخراج النص من JPEG،
  وتحويل الصورة إلى نص باستخدام Aspose OCR. دليل خطوة بخطوة.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from jpeg
- convert image to text
- how to extract text
language: ar
og_description: تعلم كيفية استخدام OCR في C# للتعرف على النص من الصورة، استخراج النص
  من JPEG، وتحويل الصورة إلى نص. يتضمن الكود الكامل والنصائح.
og_title: كيفية استخدام OCR في C# – التعرف على النص من الصورة
tags:
- C#
- Aspose OCR
- Image Processing
title: كيفية استخدام OCR في C# – التعرف على النص من الصورة بسرعة
url: /ar/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-image-quickly/
---

to keep them unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – التعرف على النص من الصورة بسرعة

هل تساءلت يومًا **كيفية استخدام OCR** في مشروع .NET لاستخراج النص من صورة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى *التعرف على النص من صورة*، خاصة ملفات JPEG، وينتهي بهم الأمر بالبحث عن قطعة “سحرية” تعمل فورًا.

الأمر بسيط—Aspose OCR يجعل العملية كلها سهلة للغاية. في هذا الدرس سنستعرض كل ما تحتاجه **لتحويل الصورة إلى نص**، استخراج ذلك النص من ملف JPEG، و—نعم—سترى النتيجة الدقيقة على وحدة التحكم الخاصة بك. لا مراجع غامضة، مجرد مثال كامل قابل للتنفيذ.

## ما ستتعلمه

- تثبيت حزمة Aspose OCR عبر NuGet.
- تهيئة محرك OCR في **الوضع عبر الإنترنت** بحيث يتم جلب حزم اللغات المفقودة تلقائيًا.
- تحميل نموذج اللغة السيريلية (أو أي لغة أخرى تحتاجها).
- تمرير صورة JPEG إلى المحرك و **التعرف على النص من صورة**.
- التعامل مع المشكلات الشائعة مثل الملفات المفقودة أو الصيغ غير المدعومة.
- مشاهدة الكود الكامل الذي يمكنك نسخه‑ولصقه في Visual Studio اليوم.

> **نصيحة احترافية:** إذا كنت تعمل مع ملفات PDF الممسوحة ضوئيًا، يمكنك استخراج كل صفحة كصورة وتمريرها إلى نفس المحرك—لا يتغير شيء في الكود.

---

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود التالي:

| Requirement | Why it matters |
|-------------|----------------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Aspose OCR يستهدف بيئات تشغيل حديثة. |
| Visual Studio 2022 (or any IDE you like) | تصحيح سهل وIntelliSense مفيد. |
| A JPEG image containing text (e.g., `cyrillic_sample.jpg`) | سنقوم **باستخراج النص من JPEG** في العرض. |
| Internet connection (for the first run) | المحرك يقوم بتحميل حزم اللغات في **الوضع عبر الإنترنت**. |

إذا كان أي من هذه العناصر مفقودًا، سيظل الدرس يُترجم، لكن محرك OCR قد يرمي استثناءً عندما لا يتمكن من العثور على نموذج اللغة.

## الخطوة 1 – تثبيت حزمة Aspose OCR عبر NuGet

أول شيء تحتاجه هو المكتبة نفسها. افتح **Package Manager Console** وشغّل الأمر:

```powershell
Install-Package Aspose.OCR
```

أو، إذا كنت تفضّل الواجهة الرسومية، ابحث عن “Aspose.OCR” في مدير الحزم NuGet واضغط **Install**. سيقوم ذلك بجلب جميع ملفات DLL المطلوبة، بما في ذلك محرك OCR الأساسي ونماذج اللغات التي يمكن جلبها عند الحاجة.

> **لماذا هذه الخطوة مهمة:** بدون الحزمة، لا توجد أي من الفئات مثل `OcrEngine` أو `LanguageModel`، لذا لن يتم تجميع الكود.

## الخطوة 2 – تهيئة محرك OCR (الكلمة المفتاحية الأساسية)

الآن بعد أن أصبحت المكتبة جاهزة، يمكننا **كيفية استخدام OCR** بإنشاء مثيل من `OcrEngine`. استخدام `ResourceMode.Online` يخبر Aspose بجلب أي حزم لغات مفقودة تلقائيًا، وهو مثالي للنماذج الأولية السريعة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine in online mode.
// This will download language packs if they aren’t already present.
OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);
```

> **ماذا يحدث خلف الكواليس؟** يتواصل المحرك مع CDN الخاص بـ Aspose، يتحقق من نماذج اللغات التي طلبتها، ويجلب الملفات اللازمة إلى ذاكرة تخزين محلية. عمليات التشغيل اللاحقة تكون دون اتصال، مما يسرّع المعالجة.

## الخطوة 3 – تحميل نموذج اللغة المطلوب

إذا كنت تتعامل مع نص إنجليزي، فإن `LanguageModel.English` هو الافتراضي. في مثالنا سنحمّل **Cyrillic**، لكن يمكنك استبداله بأي لغة مدعومة.

```csharp
// Load the Cyrillic language model so the engine knows which characters to look for.
ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
```

> **حالة حافة:** إذا حاولت تحميل لغة غير مدعومة (مثلاً `LanguageModel.Klingon`)، سيتم رمي استثناء `UnsupportedLanguageException`. ضع الاستدعاء داخل كتلة try‑catch إذا كنت تبني واجهة تسمح للمستخدمين باختيار اللغات في الوقت الفعلي.

## الخطوة 4 – توفير الصورة (الكلمة المفتاحية الثانوية: استخراج النص من jpeg)

هنا نوجه المحرك إلى ملف JPEG الذي يحتوي على النص الذي نريد قراءته. `ImageStream.FromFile` يقبل أي صيغة صورة يمكن لـ Aspose فك تشفيرها، لكن JPEG هو الأكثر شيوعًا للصور الفوتوغرافية ولقطات الشاشة.

```csharp
// Replace the path with the actual location of your JPEG image.
string imagePath = @"C:\Images\cyrillic_sample.jpg";

if (!File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Load the image into the OCR engine.
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **لماذا هذا مهم:** توفير مسار غير موجود سيسبب استثناء `FileNotFoundException`. شرط الحماية أعلاه يمنع البرنامج من الانهيار ويعطي المستخدم رسالة واضحة.

## الخطوة 5 – التعرف على النص من الصورة وإخراجه

جوهر **كيفية استخدام OCR** هو طريقة `Recognize`. تُعيد سلسلة نصية عادية تحتوي على جميع الأحرف المكتشفة، مع الحفاظ على فواصل الأسطر حيثما أمكن.

```csharp
try
{
    // Perform the OCR operation.
    string recognizedText = ocrEngine.Recognize();

    // Output the extracted text to the console.
    Console.WriteLine("📝 Recognized Text:");
    Console.WriteLine(recognizedText);
}
catch (Exception ex)
{
    Console.WriteLine($"⚠️ OCR failed: {ex.Message}");
}
```

### النتيجة المتوقعة في وحدة التحكم

إذا كان JPEG يحتوي على العبارة “Привет мир” (Hello world بالروسية)، سترى شيئًا مثل:

```
📝 Recognized Text:
Привет мир
```

إذا كانت الصورة غير واضحة، قد يحتوي الناتج على أحرف مشوشة—هنا يأتي دور ما قبل المعالجة (مثل زيادة التباين) التي سنذكرها لاحقًا.

## الخطوة 6 – مثال كامل يعمل (جميع الخطوات مجمعة)

فيما يلي البرنامج الكامل الذي يمكنك نسخه إلى مشروع **Console App** جديد. يتضمن كل شيء من تثبيت الحزمة إلى معالجة الأخطاء، بحيث يمكنك تشغيله فورًا.

```csharp
// ------------------------------------------------------------
// Complete OCR Example – How to use OCR in C#
// ------------------------------------------------------------
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine (online mode auto‑downloads language packs)
            OcrEngine ocrEngine = new OcrEngine(ResourceMode.Online);

            // 2️⃣ Load the language model you need (Cyrillic in this demo)
            try
            {
                ocrEngine.LoadLanguage(LanguageModel.Cyrillic);
            }
            catch (Exception langEx)
            {
                Console.WriteLine($"❌ Language load error: {langEx.Message}");
                return;
            }

            // 3️⃣ Provide the image – this is where we **extract text from jpeg**
            string imagePath = @"YOUR_DIRECTORY\cyrillic_sample.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Cannot find image at {imagePath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Recognize text – the heart of **how to use OCR**
            try
            {
                string recognizedText = ocrEngine.Recognize();

                // 5️⃣ Output – **convert image to text** and display it
                Console.WriteLine("📝 Recognized Text:");
                Console.WriteLine(recognizedText);
            }
            catch (Exception ocrEx)
            {
                Console.WriteLine($"⚠️ OCR operation failed: {ocrEx.Message}");
            }
        }
    }
}
```

> **اختبار سريع:** استبدل `YOUR_DIRECTORY\cyrillic_sample.jpg` بالمسار الفعلي لملف JPEG يحتوي على نص واضح. شغّل المشروع (F5) وشاهد وحدة التحكم تطبع السلسلة المستخرجة.

## الخطوة 7 – نصائح، حالات حافة، وأسئلة شائعة

### كيف يمكنني **التعرف على النص من صورة** غير ملفات JPEG؟

Aspose OCR يدعم PNG و BMP و TIFF وحتى صفحات PDF (عند تحويلها إلى صور أولاً). فقط غير امتداد الملف في `ImageStream.FromFile`. الكود نفسه يعمل—لا حاجة لإعدادات إضافية.

### ماذا لو كانت الصورة منخفضة الدقة؟

دقة OCR تنخفض بشكل كبير تحت 300 dpi. يمكنك تحسين النتائج عن طريق:

1. تكبير حجم الصورة باستخدام مكتبة مثل **ImageSharp**.
2. تطبيق عتبة ثنائية لزيادة التباين.
3. استخدام `ocrEngine.Settings.Deskew = true` لتصحيح النص المائل.

```csharp
ocrEngine.Settings.Deskew = true; // Auto‑corrects rotated text
```

### هل يمكنني **تحويل الصورة إلى نص** بشكل جماعي؟

بالطبع. ضع منطق التعرف داخل حلقة `foreach` على مجلد من الصور. تذكر إعادة استخدام نفس مثيل `OcrEngine`—فهو يخزن حزم اللغات في الذاكرة ويُسرّع المعالجة الدفعية.

```csharp
string[] files = Directory.GetFiles(@"C:\Images", "*.jpg");
foreach (var file in files)
{
    ocrEngine.Image = ImageStream.FromFile(file);
    string txt = ocrEngine.Recognize();
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), txt);
}
```

### هل يعمل هذا على Linux/macOS؟

نعم. Aspose OCR متعدد المنصات طالما تم تثبيت بيئة تشغيل .NET. العقبة الوحيدة هي الاعتمادات الأصلية لفك تشفير الصور، والتي تُضمّن مع حزمة NuGet.

### كيف يمكنني **استخراج النص من jpeg** مع الحفاظ على التخطيط؟

قم بتعيين `ocrEngine.Settings.PreserveFormatting = true`. هذا يحافظ على فواصل الأسطر والجداول البسيطة، مما يجعل الناتج أكثر قابلية للقراءة.

```csharp
ocrEngine.Settings.PreserveFormatting = true;
```

## الخلاصة

في بضع خطوات أظهرنا **كيفية استخدام OCR** في C# لـ **التعرف على النص من صورة**، **استخراج النص من JPEG**، و**تحويل الصورة إلى نص** باستخدام Aspose OCR. المثال الكامل يعمل مباشرة، يتعامل مع الملفات المفقودة، ويعطيك رد فعل فوري على وحدة التحكم.

من هنا يمكنك:

- استبدال `LanguageModel.Cyrillic` بأي لغة أخرى (English, Arabic, Chinese, إلخ).
- معالجة دفعية لمجلدات الصور لأتمتة إدخال البيانات.
- دمج OCR مع معالجة اللغة الطبيعية لفهرسة المستندات الممسوحة.

لذا انطلق—جرّب الكود، جرب جودة صور مختلفة، ودع المحرك يتولى العمل الشاق. إذا واجهت مشكلة، فإن المجتمع (وثائق Aspose) على بعد بحث واحد. برمجة سعيدة!

![مثال على كيفية استخدام OCR](placeholder-image.png "مثال على كيفية استخدام OCR في C#")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}