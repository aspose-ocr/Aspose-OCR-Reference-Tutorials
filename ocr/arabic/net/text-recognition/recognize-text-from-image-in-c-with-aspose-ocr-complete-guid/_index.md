---
category: general
date: 2026-06-25
description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية قراءة
  النص من PNG، وتحميل الصورة للتعرف الضوئي على الأحرف، وتمكين الكشف التلقائي عن اللغة
  في مثال بسيط.
draft: false
keywords:
- recognize text from image
- read text from png
- load image for ocr
- aspose ocr c# example
- enable automatic language detection
language: ar
og_description: التعرف على النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية قراءة النص من PNG، وتحميل الصورة للتعرف الضوئي على الأحرف، وتمكين الكشف التلقائي
  عن اللغة.
og_title: التعرف على النص من الصورة في C# – Aspose OCR خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Recognize text from image using Aspose OCR in C#. Learn how to read
    text from PNG, load image for OCR, and enable automatic language detection in
    a simple example.
  headline: Recognize Text from Image in C# with Aspose OCR – Complete Guide
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
- OCR
title: التعرف على النص من الصورة في C# باستخدام Aspose OCR – دليل كامل
url: /ar/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr-complete-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من صورة في C# باستخدام Aspose OCR – دليل شامل

هل احتجت يوماً إلى **التعرف على النص من صورة** لكنك لم تكن متأكدًا أي API سيتعامل مع الصور متعددة اللغات دون عناء؟ لست وحدك. في العديد من التطبيقات الواقعية—مثل ماسحات الفواتير أو قارئات اللوحات متعددة اللغات—تحتاج إلى **قراءة النص من ملفات PNG**، وتريد أيضًا أن يحدد المحرك اللغة تلقائيًا.

في هذا الدرس سنستعرض مثالًا مختصرًا **Aspose OCR C#** يقوم بتحميل صورة للتعرف الضوئي على الحروف (OCR)، يفعّل الكشف التلقائي عن اللغة، وأخيرًا يطبع النص المستخرج. في النهاية ستحصل على تطبيق وحدة تحكم جاهز للتنفيذ يمكنه **التعرف على النص من صور** بأي مزيج لغوي.

## ما ستتعلمه

- كيفية **تحميل صورة للتعرف الضوئي على الحروف** باستخدام طريقة `OcrImage.FromFile` الخاصة بـ Aspose.  
- الخطوات الدقيقة **لتفعيل الكشف التلقائي عن اللغة** حتى لا تحتاج إلى كتابة رموز اللغة يدويًا.  
- كيفية **قراءة النص من PNG** (أو أي صورة نقطية مدعومة) وعرض كل من اللغات المكتشفة والنص الخام الناتج عن OCR.  
- المشكلات الشائعة مثل مسارات الملفات المفقودة، صيغ الصور غير المدعومة، وكيفية استكشاف الأخطاء وإصلاحها.  

**المتطلبات المسبقة** – .NET 6 (أو أحدث) SDK، مشروع وحدة تحكم جديد، وحزمة NuGet `Aspose.OCR`. لا توجد مكتبات طرف ثالث أخرى مطلوبة.

---

![Diagram illustrating the flow of recognizing text from image with Aspose OCR in C#](recognize-text-from-image-aspnet-ocr-diagram.png){.align-center alt="التعرف على النص من صورة باستخدام مثال Aspose OCR C#"}

## الخطوة 1 – التعرف على النص من صورة باستخدام Aspose OCR

أول شيء تحتاجه هو نسخة من `OcrEngine`. فكر فيها كالعقل وراء العملية؛ فهي تحتفظ بجميع الإعدادات، بما في ذلك وضع اللغة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class AutoDetectExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this object will do all the heavy lifting.
        var ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** إنشاء المحرك مرة واحدة وإعادة استخدامه عبر صور متعددة يقلل من الحمل الزائد. في الخدمات الأكبر عادةً ما تحتفظ بنسخة مفردة (singleton).

## الخطوة 2 – تحميل صورة للتعرف الضوئي على الحروف وقراءة النص من PNG

الآن بعد أن تم إنشاء المحرك، نحتاج إلى إعطائه شيئًا ليقرأه. تدعم Aspose مجموعة متنوعة من الصيغ، لكن PNG خيار شائع لأنه يحافظ على الجودة بدون فقدان.

```csharp
        // 2️⃣ Tell the engine which file to process.
        //    OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
        var image = OcrImage.FromFile("YOUR_DIRECTORY/mixed_languages.png");
```

> **نصيحة:** إذا لم تكن متأكدًا من المسار الدقيق، استخدم `Path.Combine(Environment.CurrentDirectory, "mixed_languages.png")`. هذا يمنع حدوث أخطاء “الملف غير موجود” عند تشغيل التطبيق من دليل عمل مختلف.

## الخطوة 3 – تفعيل الكشف التلقائي عن اللغة

معظم مكتبات OCR تجبرك على تحديد رمز لغة (مثال: `Language.English`). هذا يعمل جيدًا للوثائق أحادية اللغة، لكنه يصبح عبئًا عندما تحتوي الصورة على الإنجليزية **و** الفرنسية، أو أي مزيج آخر. تحل Aspose هذه المشكلة باستخدام تعداد `Language.AutoDetect`.

```csharp
        // 3️⃣ Switch on auto‑detect so the engine guesses the language(s) on the fly.
        ocrEngine.Settings.Language = Language.AutoDetect;
```

> **ما الذي يحدث خلف الكواليس؟** يقوم المحرك بتحليل إحصائي سريع على الحروف، يقارنها بنماذج اللغة المدمجة، ثم يختار المجموعة الأكثر احتمالًا. هذه العملية تضيف تكلفة أداء ضئيلة لكنها تحسّن الدقة بشكل كبير للمحتوى متعدد اللغات.

## الخطوة 4 – تنفيذ عملية التعرف الضوئي على الحروف

مع تحميل الصورة وتفعيل الكشف عن اللغة، نستدعي أخيرًا `Recognize`. تُعيد الطريقة كائن `RecognitionResult` يحتوي على كل من النص المستخرج وقائمة اللغات المكتشفة.

```csharp
        // 4️⃣ Run the OCR process.
        var recognitionResult = ocrEngine.Recognize(image);
```

> **حالة حافة:** إذا كانت الصورة صاخبة جدًا، قد يحتوي الناتج على أحرف مشوشة. فكر في معالجة مسبقة باستخدام `image.AdjustContrast` أو `image.RemoveNoise` قبل عملية التعرف.

## الخطوة 5 – عرض اللغات المكتشفة والنص المستخرج

الخطوة الأخيرة هي ببساطة طباعة النتائج. في خدمة حقيقية ربما تُعيد حمولة JSON، لكن في هذا العرض التوضيحي لوحدة التحكم يكفي `Console.WriteLine`.

```csharp
        // 5️⃣ Show what the engine found.
        Console.WriteLine("Detected languages: " + string.Join(", ", recognitionResult.DetectedLanguages));
        Console.WriteLine("Extracted text:");
        Console.WriteLine(recognitionResult.Text);
    }
}
```

### النتيجة المتوقعة

```
Detected languages: English, French
Extracted text:
Welcome to our store!
Bienvenue dans notre magasin!
```

إذا رأيت قائمة لغات فارغة، تحقق مرة أخرى من أن الصورة تحتوي فعلاً على أحرف يمكن التعرف عليها وأن رخصة Aspose OCR (إذا كنت تستخدم نسخة مدفوعة) مُطبقة بشكل صحيح.

---

## أسئلة شائعة ونصائح احترافية

| السؤال | الجواب |
|----------|--------|
| **هل يمكنني معالجة JPEG أو BMP بدلاً من PNG؟** | بالتأكيد. `OcrImage.FromFile` يعمل مع أي صيغة يدعمها Aspose OCR. فقط غيّر امتداد الملف. |
| **ماذا لو أردت حصر الكشف على مجموعة لغات محددة؟** | اضبط `ocrEngine.Settings.Language = Language.English | Language.Spanish;` باستخدام عامل OR البتّي. |
| **هل هناك طريقة للحصول على درجات الثقة؟** | نعم. `recognitionResult.Confidence` يُعطي قيمة عائمة بين 0 و 1 لكل سطر مُعترف به. |
| **كيف أتعامل مع دفعات كبيرة؟** | أعد استخدام نفس نسخة `OcrEngine` ولفّ الحلقة داخل `Parallel.ForEach` للمعالجة المتوازية. |

---

## المثال الكامل (جاهز للنسخ واللصق)

فيما يلي البرنامج الكامل، جاهز للترجمة بعد إضافة حزمة NuGet `Aspose.OCR` (`dotnet add package Aspose.OCR`) ووضع ملف `mixed_languages.png` في المجلد المحدد.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

class AutoDetectExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Enable automatic language detection
        ocrEngine.Settings.Language = Language.AutoDetect;

        // Step 3: Load the image that contains mixed languages
        // Replace YOUR_DIRECTORY with the actual folder path.
        var image = OcrImage.FromFile("YOUR_DIRECTORY/mixed_languages.png");

        // Step 4: Perform OCR recognition on the image
        var recognitionResult = ocrEngine.Recognize(image);

        // Step 5: Display the detected languages and extracted text
        Console.WriteLine("Detected languages: " + string.Join(", ", recognitionResult.DetectedLanguages));
        Console.WriteLine("Extracted text:");
        Console.WriteLine(recognitionResult.Text);
    }
}
```

شغّل البرنامج باستخدام `dotnet run` وسترى اللغات المكتشفة تليها النص المستخرج يُطبع في وحدة التحكم.

---

## الخلاصة – لماذا هذا مهم

لقد قمنا للتو **بالتعرف على النص من صور** باستخدام Aspose OCR، وأظهرنا كيفية **قراءة النص من PNG**، وبيّنّا أبسط طريقة **لتفعيل الكشف التلقائي عن اللغة**. هذه الأسطر القليلة هي العمود الفقري لأي حل مسح متعدد اللغات—سواء كنت تبني محلل فواتير، ماسح جوازات سفر، أو أداة مراقبة محتوى صور على وسائل التواصل.

### الخطوات التالية

- **جرب صيغًا أخرى** – جرّب JPEG عالي الدقة وقارن الدقة.  
- **دمج درجات الثقة** – استبعد السطور ذات الثقة المنخفضة قبل تخزينها.  
- **الدمج مع Azure Blob Storage** – حمّل الصور مباشرة من السحابة بدلًا من نظام الملفات المحلي.  
- **استكشف الخيارات المتقدمة في Aspose OCR** – مثل `ocrEngine.Settings.ImagePreprocessing` لتقليل الضوضاء.

إذا كنت مهتمًا بتوسيع هذا إلى واجهة ويب API، اطلع على دليلنا “**ASP.NET Core OCR endpoint**” حيث نعيد استخدام نفس المحرك لتقديم طلبات HTTP.

برمجة سعيدة، ولتقرأ مشاريعك القادمة النص من PNGs بسهولة كما قرأت هذا الدرس!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مصدر يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف نهج تنفيذ بديلة في مشاريعك.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}