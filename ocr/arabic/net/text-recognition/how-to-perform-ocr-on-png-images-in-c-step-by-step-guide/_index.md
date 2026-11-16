---
category: general
date: 2026-03-29
description: كيفية تنفيذ OCR في C# وقراءة النص من ملفات PNG. تعلم استخراج النص الروسي،
  قراءة النص من PNG، وكيفية استخراج النص باستخدام Aspose OCR.
draft: false
keywords:
- how to perform ocr
- read text from png
- how to extract text
- extract russian text
- c# ocr tutorial
language: ar
og_description: كيفية تنفيذ OCR في C# باستخدام Aspose OCR. يوضح هذا الدليل كيفية قراءة
  النص من ملف PNG، استخراج النص الروسي، وتنفيذ حل OCR كامل بلغة C#.
og_title: كيفية تنفيذ OCR في C# – استخراج النص الكامل من PNG
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR على صور PNG في C# – دليل خطوة بخطوة
url: /ar/net/text-recognition/how-to-perform-ocr-on-png-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية إجراء OCR على صور PNG في C# – دليل كامل

هل احتجت يوماً إلى **إجراء OCR** على لقطة شاشة أو مستند ممسوح ضوئياً لكنك لم تكن متأكدًا من أين تبدأ في C#؟ لست وحدك. يسأل المطورون باستمرار: “كيف يمكنني قراءة النص من ملفات PNG دون إرسالها إلى خدمة خارجية؟” الخبر السار هو أنه باستخدام Aspose.OCR يمكنك **استخراج النص الروسي**، **قراءة النص من png**، والحصول على سلسلة نصية نظيفة في بضع أسطر من الشيفرة فقط.

في هذا الدرس سنستعرض كل ما تحتاجه: إعداد المكتبة، اختيار نموذج اللغة المناسب، تشغيل التعرف، ومعالجة المشكلات الشائعة. بنهاية الدرس ستتمكن من **كيفية استخراج النص** من أي صورة PNG، سواء كانت إنجليزية أو روسية أو أي من أكثر من 70 لغة تدعمها Aspose. لا إطالة، مجرد مثال عملي يمكنك وضعه مباشرةً في تطبيق Console الآن.

---

## ما ستتعلمه

- تثبيت وإضافة مرجع حزمة Aspose.OCR عبر NuGet.  
- تهيئة محرك OCR في وضع التحميل التلقائي الافتراضي.  
- ضبط المحرك **لاستخراج النص الروسي** باستخدام نموذج اللغة السيريلي.  
- تشغيل OCR على ملف PNG محلي وعرض النتيجة.  
- نصائح لتصحيح مشاكل ملفات اللغة المفقودة وتحسين الدقة.

**المتطلبات المسبقة**: .NET 6+ (أو .NET Framework 4.7.2+)، Visual Studio 2022 أو VS Code، واتصال بالإنترنت للتشغيل الأول (يتم تنزيل نموذج اللغة تلقائيًا).

---

## الخطوة 1 – تثبيت حزمة Aspose.OCR

للبدء، أضف مكتبة Aspose.OCR إلى مشروعك. افتح الطرفية في مجلد المشروع وشغّل:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل واجهة Visual Studio، انقر بزر الماوس الأيمن على **Dependencies → Manage NuGet Packages**، ابحث عن **Aspose.OCR**، ثم اضغط **Install**.

> **نصيحة احترافية**: الحزمة لا تتعدى بضعة ميغابايت، ونماذج اللغات تُجلب عند الحاجة، لذا لن تثقل تطبيقك بملفات غير ضرورية.

---

## الخطوة 2 – تهيئة محرك OCR (الكلمة المفتاحية الأساسية في التنفيذ)

إنشاء المحرك سهل. المُنشئ يُفعّل تلقائيًا *وضع التحميل التلقائي*، ما يعني أنه في المرة الأولى التي تطلب فيها لغة غير موجودة محليًا، سيقوم Aspose بتنزيلها لك.

```csharp
using System;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine – it will download missing models automatically.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Choose the language model – Russian Cyrillic (downloads if missing).
        ocrEngine.Language = Language.RussianCyrillic;

        // 3️⃣ Run OCR on the PNG image.
        var ocrResult = ocrEngine.RecognizeImage("sample_russian.png");

        // 4️⃣ Output the recognized text.
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **لماذا هذا مهم**: باستخدام وضع التحميل التلقائي الافتراضي تتجنب التعامل اليدوي مع الملفات. إذا احتجت لاحقًا إلى **قراءة النص من png** بلغة أخرى، ما عليك سوى تغيير `Language.RussianCyrillic` إلى القيمة المناسبة من الـ enum.

---

## الخطوة 3 – تحضير صورة PNG الخاصة بك

تأكد من أن الصورة التي تريد معالجتها متاحة أثناء وقت التشغيل. ضع `sample_russian.png` في نفس المجلد الذي يحتوي على ملف `.exe` المُجمع، أو استخدم مسارًا مطلقًا إذا رغبت. يجب أن تكون الصورة مسحًا واضحًا أو لقطة شاشة؛ فدقة OCR تنخفض بشكل كبير مع PNG غير واضح أو مضغوط بشدة.

**حالة شائعة**: إذا كانت PNG تحتوي على لغات متعددة، يمكنك ضبط `ocrEngine.Language = Language.Multilingual;` لتمكين المحرك من اكتشاف كل كتلة تلقائيًا.

---

## الخطوة 4 – تشغيل التطبيق والتحقق من المخرجات

قم بترجمة البرنامج وتشغيله:

```bash
dotnet run
```

يجب أن ترى النص الروسي المستخرج يُطبع في وحدة التحكم، مثلًا:

```
Привет, мир! Это пример текста на русском языке.
```

إذا حصلت على سلسلة فارغة، تحقق من التالي:

1. أن مسار الملف صحيح.  
2. أن الصورة ليست بيضاء بالكامل أو سوداء بالكامل.  
3. أن نموذج اللغة تم تنزيله بنجاح (ابحث عن مجلد `Aspose.OCR` ضمن ملف تعريف المستخدم الخاص بك).

---

## الخطوة 5 – تحسينات متقدمة لزيادة الدقة

على الرغم من أن الإعدادات الافتراضية تعمل في معظم الحالات، قد ترغب في ضبط المحرك:

| الإعداد | ما يفعله | متى تستخدمه |
|---------|----------|--------------|
| `ocrEngine.PreprocessOptions.Deskew = true;` | يصحح الانحراف الطفيف | المستندات الممسوحة التي ليست محاذية تمامًا |
| `ocrEngine.PreprocessOptions.RemoveNoise = true;` | يزيل الضوضاء الخلفية | PNG منخفض الجودة من كاميرات الهواتف |
| `ocrEngine.RecognitionOptions.CharWhitelist = "0123456789";` | يقتصر على الأرقام فقط | استخراج الأرقام من الفواتير |

أضف أي من هذه قبل استدعاء `RecognizeImage`:

```csharp
ocrEngine.PreprocessOptions.Deskew = true;
ocrEngine.PreprocessOptions.RemoveNoise = true;
```

---

## الخطوة 6 – تصدير النتائج إلى ملف (اختياري)

إذا رغبت في **كيفية استخراج النص** إلى ملف للمعالجة لاحقًا، ما عليك سوى كتابة النتيجة إلى القرص:

```csharp
System.IO.File.WriteAllText("ocr_output.txt", ocrResult.Text);
Console.WriteLine("OCR output saved to ocr_output.txt");
```

الآن لديك نسخة مستمرة يمكن إدخالها إلى قاعدة بيانات، فهرس بحث، أو محرك ترجمة.

---

## الأسئلة المتكررة

**س: هل يعمل هذا مع صيغ صور أخرى مثل JPEG أو BMP؟**  
ج: بالتأكيد. `RecognizeImage` تقبل أي صيغة يدعمها مكتبة .NET `System.Drawing`، بما فيها JPEG و BMP و TIFF.

**س: ماذا لو أردت استخراج النص الإنجليزي في نفس التشغيل؟**  
ج: أنشئ نسخة ثانية من `OcrEngine` باستخدام `Language.English` أو غيّر خاصية اللغة بين الاستدعاءات.

**س: هل يمكن تشغيل OCR في واجهة ويب API دون حجز الخيط الرئيسي؟**  
ج: نعم. غلف استدعاء التعرف داخل `Task.Run` أو استخدم النسخة غير المتزامنة `RecognizeImageAsync` (متوفرة في إصدارات Aspose الأحدث).

**س: هل هناك حد لحجم PNG؟**  
ج: المكتبة تستطيع معالجة صور كبيرة، لكن استهلاك الذاكرة يزداد مع الدقة. إذا واجهت `OutOfMemoryException`، فكر في تقليل حجم الصورة أولًا.

---

## مثال كامل جاهز للتنفيذ (انسخه‑الصقه)

فيما يلي البرنامج الكامل الذي يمكنك لصقه في مشروع Console جديد (`dotnet new console`) وتشغيله فورًا بعد تثبيت حزمة NuGet.

```csharp
// File: Program.cs
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize OCR engine – auto‑download enabled.
            var ocrEngine = new OcrEngine();

            // Choose Russian Cyrillic language model.
            ocrEngine.Language = Language.RussianCyrillic;

            // Optional: improve accuracy for skewed or noisy images.
            ocrEngine.PreprocessOptions.Deskew = true;
            ocrEngine.PreprocessOptions.RemoveNoise = true;

            // Path to the PNG file you want to read.
            string imagePath = "sample_russian.png";

            // Perform OCR.
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Output the recognized text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(result.Text);

            // Save to a text file for later use.
            System.IO.File.WriteAllText("ocr_output.txt", result.Text);
            Console.WriteLine("Result saved to ocr_output.txt");
        }
    }
}
```

**الناتج المتوقع في وحدة التحكم** (مع افتراض أن العينة تحتوي على العبارة “Привет, мир!”):

```
=== OCR Result ===
Привет, мир! Это пример текста на русском языке.
Result saved to ocr_output.txt
```

---

## الخلاصة

غطّينا **كيفية إجراء OCR** على صور PNG باستخدام C#، بدءًا من تثبيت Aspose.OCR إلى تخصيص خيارات ما قبل المعالجة وتصدير النتائج. الآن تعرف كيف **قراءة النص من png**، **كيفية استخراج النص** بلغات مختلفة، وبشكل خاص **استخراج النص الروسي** بأقل قدر من الشيفرة.

هل أنت مستعد للتحدي التالي؟ جرّب إمداد مخرجات OCR إلى مكتبة اكتشاف لغة، أو دمجها مع Azure Cognitive Services للترجمة. السماء هي الحد عندما تجمع محرك OCR موثوق مع نظام C# القوي.

إذا وجدت هذا **c# ocr tutorial** مفيدًا، أعطه نجمة، شاركه مع زملائك، أو اترك تعليقًا بنصائحك الخاصة. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}