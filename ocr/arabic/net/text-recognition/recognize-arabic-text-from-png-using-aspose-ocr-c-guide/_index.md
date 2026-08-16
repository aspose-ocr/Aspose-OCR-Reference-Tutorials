---
category: general
date: 2026-03-13
description: تعرّف على النص العربي بسرعة – تعلم كيفية التعرف على النص من ملف PNG،
  تحميل الصورة للتعرف الضوئي على الأحرف واستخراج النص العربي باستخدام Aspose OCR في
  C#.
draft: false
keywords:
- recognize arabic text
- recognize text from png
- load image for ocr
- extract arabic text
- how to recognize arabic
language: ar
og_description: تعلم كيفية التعرف على النص العربي من صور PNG باستخدام Aspose OCR.
  دليل خطوة بخطوة يوضح كيفية تحميل الصورة للتعرف الضوئي على الأحرف واستخراج النص العربي.
og_title: التعرف على النص العربي من PNG – دليل OCR كامل بلغة C#
tags:
- Aspose OCR
- C#
- Arabic OCR
title: التعرف على النص العربي من PNG باستخدام Aspose OCR – دليل C#
url: /ar/net/text-recognition/recognize-arabic-text-from-png-using-aspose-ocr-c-guide/
---

Let's translate.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص العربي من PNG باستخدام Aspose OCR – دليل C# كامل

هل احتجت يوماً إلى **التعرف على النص العربي** الموجود داخل لقطة شاشة أو نموذج ممسوح ضوئياً؟ لست وحدك في هذه المشكلة. في العديد من التطبيقات الإقليمية—مثل الفوترة، ماسحات جوازات السفر، أو بوتات الصور على وسائل التواصل الاجتماعي—تظهر الأحرف العربية في ملفات PNG، واستخراجها بشكل موثوق قد يبدو كالسعي وراء سراب.

الأمر بسيط: باستخدام Aspose OCR يمكنك **التعرف على النص العربي** في ثوانٍ قليلة، دون الحاجة إلى البحث عن حزم لغات يدوياً. في هذا الدرس سنستعرض تحميل صورة للـ OCR، التعرف على النص من PNG، وأخيراً استخراج النص العربي لتتمكن من تمريره إلى سير العمل الخاص بك. في النهاية ستحصل على تطبيق C# Console جاهز للتنفيذ يقوم بذلك تماماً.

## ما ستتعلمه

- كيفية إعداد Aspose OCR في مشروع .NET (بدون خطوات مخفية).
- الكود الدقيق لـ **تحميل صورة للـ OCR** من ملف PNG.
- لماذا اختيار `Language.Arabic` يؤدي إلى تحميل تلقائي لبيانات اللغة.
- كيفية **استخراج النص العربي** وعرضه في وحدة التحكم.
- المشكلات الشائعة—مثل الخطوط المفقودة أو الصور التالفة—والحلول السريعة.

كل هذا مقدم في مثال واحد متكامل، بحيث يمكنك نسخه، تشغيله، ورؤية النتائج فوراً.

---

## المتطلبات المسبقة

قبل أن نبدأ، تأكد من وجود ما يلي:

1. **.NET 6 SDK** (أو أحدث) مثبت – أحدث نسخة توفر أفضل أداء.
2. **رخصة Aspose OCR صالحة** أو يمكنك البدء بتجربة مجانية لمدة 30 يوماً (المكتبة تعمل مباشرةً للتقييم).
3. ملف صورة باسم `arabic_sample.png` موجود في مجلد يمكنك الإشارة إليه (مثال: `C:\OCRDemo\Images\`).
4. إلمام أساسي بتطبيقات C# Console—لا شيء معقد، مجرد `dotnet new console` يكفي.

إذا كان أي من هذه غير مألوف لك، توقف وقم بتثبيت SDK أولاً؛ العملية تستغرق بضع دقائق فقط.

---

## الخطوة 1 – تثبيت حزمة NuGet الخاصة بـ Aspose OCR

أولاً، افتح الطرفية في مجلد المشروع وشغّل الأمر التالي:

```bash
dotnet add package Aspose.OCR
```

هذا الأمر الواحد يجلب أحدث ملفات Aspose OCR الثنائية وجميع تبعياتها. لا حاجة لتنزيل حزم اللغات يدوياً؛ المكتبة ستحملها عند الحاجة.

> **نصيحة احترافية:** إذا كنت تعمل خلف بروكسي مؤسسي، أضف `--ignore-failed-sources` إلى الأمر أو اضبط إعدادات بروكسي NuGet في `nuget.config`.

---

## الخطوة 2 – تهيئة محرك OCR (بدون لغة أولاً)

```csharp
using Aspose.OCR;

// Create a fresh OCR engine instance. At this point no language is selected.
OcrEngine ocrEngine = new OcrEngine();
```

لماذا ننشئ المحرك بدون تحديد لغة أولاً؟ Aspose OCR يفصل بين إنشاء المحرك واختيار اللغة، مما يمنحك المرونة لتغيير اللغات أثناء التشغيل دون الحاجة لإعادة بناء الكائن. هذا مفيد خصوصاً عندما تحتاج إلى **التعرف على النص من png** قد يحتوي على عدة سكريبتات.

---

## الخطوة 3 – تعيين اللغة إلى العربية (تحميل تلقائي)

```csharp
// Pick Arabic – the library will download the Arabic language data automatically
ocrEngine.Language = Language.Arabic;
```

عند تعيين `Language.Arabic`، يتحقق Aspose من ذاكرة التخزين المؤقت المحلية. إذا لم تكن ملفات بيانات اللغة العربية موجودة، يقوم بتحميلها من شبكة CDN الخاصة بـ Aspose بصمت. هذا يعني أنك لست مضطراً لتضمين ملفات `.traineddata` الكبيرة مع تطبيقك.

> **حالة حافة:** على جهاز بدون اتصال بالإنترنت، سيفشل التحميل ويرمي استثناء `LicenseException`. في هذه الحالة، قم بتحميل حزمة اللغة مسبقاً على جهاز متصل وانسخ ملف `Arabic.traineddata` إلى مجلد `Aspose.OCR` داخل مشروعك.

---

## الخطوة 4 – تحميل صورة PNG للـ OCR

```csharp
// Provide the full path to your PNG file
string imagePath = @"C:\OCRDemo\Images\arabic_sample.png";
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

طريقة `ImageStream.FromFile` تُجردك من تفاصيل `System.Drawing` أو `SkiaSharp` الداخلية. تدعم PNG، JPEG، BMP، وحتى TIFF، لذا أنت مغطى سواء كان المصدر لقطة شاشة أو مستند ممسوح.

إذا احتجت يوماً إلى **تحميل صورة للـ OCR** من تدفق (مثلاً ملف مرفوع في ASP.NET)، استبدل `FromFile` بـ `FromStream(yourStream)`—يبقى باقي الكود كما هو.

---

## الخطوة 5 – تنفيذ عملية التعرف

```csharp
// Trigger OCR processing
ocrEngine.Recognize();
```

خلف الكواليس، يقوم Aspose بتشغيل نموذج تعلم عميق مخصص للخط العربي. الطريقة متزامنة، وهو مناسب للصور الصغيرة. للمعالجة الضخمة، فكر في استخدام `RecognizeAsync` (متوفر في إصدارات المكتبة الأحدث) للحفاظ على استجابة الواجهة.

---

## الخطوة 6 – إخراج النص العربي المُتعرف عليه

```csharp
// The recognized text is stored in the Text property
Console.WriteLine("=== Extracted Arabic Text ===");
Console.WriteLine(ocrEngine.Text);
```

في هذه المرحلة، يحتوي `ocrEngine.Text` على سلسلة Unicode تضم جميع الأحرف العربية المفككة. يمكنك تمريرها إلى قاعدة بيانات، إرسالها عبر API، أو ببساطة عرضها في وحدة التحكم كما هو موضح.

**الناتج المتوقع** (مثال):

```
=== Extracted Arabic Text ===
مرحبا بكم في دليل التعرف على النص العربي باستخدام Aspose OCR
```

إذا ظهر الناتج مشوّشاً، تأكد من أن خط وحدة التحكم يدعم العربية (مثل “Consolas” أو “Courier New” مع دعم العربية). في Windows PowerShell، يمكنك ضبط ترميز الإخراج باستخدام `chcp 65001` قبل تشغيل التطبيق.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الجاهز للتنفيذ. الصقه في `Program.cs` لمشروع Console جديد، عدّل مسار الصورة، واضغط **F5**.

```csharp
// Program.cs
using System;
using Aspose.OCR;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine (no language selected yet)
            OcrEngine ocrEngine = new OcrEngine();

            // 2️⃣ Set the language to Arabic – triggers automatic download if missing
            ocrEngine.Language = Language.Arabic;

            // 3️⃣ Load the image containing Arabic text (recognize text from png)
            string imagePath = @"C:\OCRDemo\Images\arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Perform the recognition
            ocrEngine.Recognize();

            // 5️⃣ Output the recognized text (extract arabic text)
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

> **نصيحة:** ضع استدعاء OCR داخل كتلة `try/catch` للتعامل بلطف مع الملفات المفقودة أو الصور التالفة. مثال:
> ```csharp
> try { ocrEngine.Recognize(); }
> catch (Exception ex) { Console.Error.WriteLine($"OCR failed: {ex.Message}"); }
> ```

---

## أسئلة شائعة وكيفية التعامل معها

### 1. *ماذا لو كان PNG يحتوي على العربية والإنجليزية معاً؟*  
Aspose OCR يستطيع التعرف على سكريبتات مختلطة. بعد تعيين `ocrEngine.Language = Language.Arabic;` يمكنك أيضاً تمكين `ocrEngine.AdditionalLanguages = new[] { Language.English };`. سيُنتج المحرك سلسلة مدمجة تحافظ على كلا السكريبتين.

### 2. *هل يعمل OCR على صور منخفضة الدقة؟*  
تنخفض دقة التعرف تحت 100 dpi. للحصول على أفضل النتائج، قم بزيادة حجم الصورة باستخدام `ImageProcessor` (جزء من Aspose) قبل تمريرها إلى المحرك:
```csharp
ocrEngine.Image = ImageProcessor.Resize(ocrEngine.Image, 300, 300);
```

### 3. *هل يمكن تشغيله على Linux/macOS؟*  
بالتأكيد. Aspose OCR متعدد المنصات. فقط تأكد من أن البيئة تحتوي على المكتبات الأصلية اللازمة (`libgdiplus` على Linux) وأن دعم الخطوط العربية مثبت (`fonts-arabic` على Ubuntu).

### 4. *كيف أتجنب التحميل التلقائي لبيانات اللغة في بيئة الإنتاج؟*  
حمّل حزمة اللغة مسبقاً خلال خط أنابيب CI الخاص بك:
```bash
dotnet run --project MyApp.csproj -- -downloadLanguage Arabic
```
ثم وزّع ملف `Arabic.traineddata` مع عملية النشر.

---

## تحسينات الأداء (اختياري)

- **وضع الدفعات:** إذا كنت تعالج عشرات PNG، أعد استخدام نفس كائن `OcrEngine` بدلاً من إنشاء جديد في كل مرة. هذا يقلل من زمن التهيئة بنحو ~30 %.
- **التوازي:** غلف حلقة التعرف بـ `Parallel.ForEach` مع `OcrEnginePool` آمن للخطوط (أنشئ مجموعة من 4‑8 محركات حسب عدد نوى المعالج).
- **إدارة الذاكرة:** استدعِ `ocrEngine.Dispose()` بعد الانتهاء، خاصة في الخدمات طويلة التشغيل، لتحرير الموارد الأصلية.

---

## الخلاصة

لقد تعلمنا الآن **التعرف على النص العربي** من ملف PNG باستخدام Aspose OCR، بدءاً من تثبيت حزمة NuGet وحتى التعامل مع الحالات الخاصة مثل اللغات المختلطة والصور منخفضة الدقة. الشيفرة الكاملة أعلاه هي حل جاهز للتنفيذ—انسخه، وجهه إلى صورتك، وسترى الأحرف العربية تظهر فوراً.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال `Language.Arabic` بـ `Language.French` أو `Language.ChineseSimplified` لتلاحظ كيف يتعامل المحرك مع سكريبتات أخرى. أو دمج استدعاء OCR في API بـ ASP.NET Core ليتمكن العملاء من رفع الصور والحصول على النص المستخرج مباشرة. الاحتمالات لا حصر لها، والآن لديك أساس صلب لأي مشروع **كيفية التعرف على النص العربي** تصادفه.

برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالبلور!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}