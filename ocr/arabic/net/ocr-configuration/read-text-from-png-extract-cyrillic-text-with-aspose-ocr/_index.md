---
category: general
date: 2026-03-07
description: تعلم كيفية قراءة النص من ملفات PNG واستخراج النص السيريلي باستخدام Aspose
  OCR، وتحويل الصورة إلى نص، وتنزيل حزمة اللغة السيريالية.
draft: false
keywords:
- read text from png
- extract cyrillic text
- convert image to text
- load image for ocr
- download cyrillic language pack
language: ar
og_description: تعلم كيفية قراءة النص من ملف PNG، استخراج النص السيريلي، وتحويل الصورة
  إلى نص باستخدام Aspose OCR في C#.
og_title: قراءة النص من PNG – استخراج النص السيريلي باستخدام Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: قراءة النص من PNG – استخراج النص السيريلي باستخدام Aspose OCR
url: /ar/net/ocr-configuration/read-text-from-png-extract-cyrillic-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# قراءة النص من PNG – استخراج النص السيريلي باستخدام Aspose OCR

هل تحتاج إلى **قراءة النص من PNG** واستخراج الأحرف السيريليّة؟ في هذا الدليل سنوضح لك كيفية قراءة النص من PNG باستخدام Aspose OCR، استخراج النص السيريلي، و**تحويل الصورة إلى نص** في بضع أسطر فقط من C#.

إذا سبق لك أن نظرت إلى لقطة شاشة لفاتورة روسية وتساءلت كيف يمكنك تحويل الكلمات إلى سلسلة قابلة للبحث، فأنت في المكان الصحيح. سنغطي أيضًا كيفية **تنزيل حزمة اللغة السيريليّة** تلقائيًا، حتى لا تحتاج للبحث عن ملفات إضافية.

## ما ستحققه

بنهاية هذا البرنامج التعليمي ستكون قادرًا على:

* **تحميل صورة للـ OCR** مباشرةً من القرص أو من تدفق بيانات.  
* ضبط المحرك على **اللغة السيريليّة** دون الحاجة لتنزيلات يدوية.  
* تشغيل التعرف و**استخراج النص السيريلي** من ملف PNG.  
* رؤية النص المستخرج يُطبع على وحدة التحكم – نتيجة نصية نظيفة يمكنك إدخالها في قواعد البيانات، فهارس البحث، أو أي سير عمل آخر.

بدون خدمات خارجية، بدون مفاتيح سحابة، فقط حزمة Aspose OCR NuGet وبضع أسطر من C#.

## المتطلبات المسبقة

* .NET 6.0 أو أحدث (الكود يعمل على .NET Core، .NET Framework، و .NET 5+).  
* Visual Studio 2022 أو أي محرر تفضله.  
* حزمة Aspose.OCR NuGet (`dotnet add package Aspose.OCR`).  
* صورة PNG تحتوي على أحرف سيريليّة – على سبيل المثال `cyrillic_sample.png` موجودة في مجلد اسمه `YOUR_DIRECTORY`.

> **نصيحة احترافية:** إذا كنت تستخدم Visual Studio، انقر بزر الماوس الأيمن على المشروع → **Manage NuGet Packages** → ابحث عن “Aspose.OCR” وقم بتثبيت أحدث نسخة مستقرة.

---

## الخطوة 1 – تثبيت Aspose OCR وإنشاء المحرك

أولاً نحتاج إلى كائن محرك OCR. فئة `OcrEngine` هي نقطة الدخول لجميع العمليات.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Create an OCR engine – this object holds all settings and results
var ocrEngine = new OcrEngine();
```

> **لماذا هذا مهم:** المحرك يضم حزم اللغات، بيانات الصورة، وخيارات التعرف. إنشاء نسخة واحدة وإعادة استخدامها عبر صور متعددة يمكن أن يحسّن الأداء.

---

## الخطوة 2 – **تحميل الصورة للـ OCR** وتحديد اللغة

الآن نخبر المحرك أي صورة يجب معالجتها وأي لغة يبحث عنها. ضبط `Language.Cyrillic` يقوم تلقائيًا بتنزيل حزمة اللغة المطلوبة في المرة الأولى التي يُشغل فيها.

```csharp
// 1️⃣ Load the PNG that contains Cyrillic text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");

// 2️⃣ Tell Aspose we want to read Cyrillic characters
ocrEngine.Settings.Language = Language.Cyrillic;   // downloads pack if missing
```

> **حالة خاصة:** إذا كان ملف PNG كبيرًا (أكثر من 5 ميغابايت) قد ترغب في تغيير حجمه أولًا لتسريع عملية التعرف. خاصية `Image` تقبل أيضًا `Stream`، لذا يمكنك التحميل من الذاكرة، طلب ويب، أو Azure Blob دون الحاجة للوصول إلى نظام الملفات.

---

## الخطوة 3 – **تحويل الصورة إلى نص** باستدعاء واحد

عملية التعرف بسيطة كما في استدعاء `Recognize()`. بعد هذا الاستدعاء، خاصية `Text` تحتوي على السلسلة المستخرجة.

```csharp
// Run the OCR engine – this does the heavy lifting
ocrEngine.Recognize();

// Grab the result; it’s plain Unicode text
string extractedText = ocrEngine.Text;
```

> **ماذا يحدث خلف الكواليس؟** Aspose يستخدم مصنفًا معتمدًا على الشبكات العصبية تم تدريبه على ملايين الحروف السيريليّة. المكتبة تُجرد كل هذه التعقيدات، لتُعطيك Unicode نظيفًا.

---

## الخطوة 4 – إخراج النتيجة (أو تمريرها لمكان آخر)

لأغراض العرض سنطبع النص على وحدة التحكم، لكن يمكنك بسهولة كتابته إلى ملف، قاعدة بيانات، أو تمريره إلى فهرس بحث.

```csharp
// Show the OCR result in the console
Console.WriteLine("=== Recognized Cyrillic Text ===");
Console.WriteLine(extractedText);
```

**الناتج المتوقع** (بافتراض أن `cyrillic_sample.png` يحتوي على العبارة “Привет мир”):

```
=== Recognized Cyrillic Text ===
Привет мир
```

إذا ظهر الناتج مشوّهًا، تحقق من وضوح الصورة وأنك ضبطت `Language.Cyrillic`. المحرك يفرض اللغة الإنجليزية افتراضيًا، مما سيعامل الأحرف السيريليّة كرموز غير معروفة.

---

## الخطوة 5 – مثال كامل قابل للتنفيذ

نجمع كل ما سبق في برنامج مستقل يمكنك نسخه ولصقه في مشروع وحدة تحكم جديد.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Create the OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // 2️⃣ Load the PNG and select Cyrillic language
        // -------------------------------------------------
        // Replace the path with the location of your PNG
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_sample.png");
        ocrEngine.Settings.Language = Language.Cyrillic; // auto‑downloads pack

        // -------------------------------------------------
        // 3️⃣ Perform recognition
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 4️⃣ Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Cyrillic Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

احفظ الملف باسم `Program.cs`، نفّذ `dotnet run`، ويجب أن ترى النص السيريلي يُطبع على الشاشة.

---

## أسئلة شائعة & استكشاف الأخطاء

| السؤال | الجواب |
|----------|--------|
| **ماذا لو لم يتم تنزيل حزمة اللغة؟** | تأكد من أن الجهاز متصل بالإنترنت. الحزمة تُخزن مؤقتًا في `%USERPROFILE%\.Aspose\OCR\Languages`. حذف هذا المجلد يجبر البرنامج على إعادة التنزيل. |
| **هل يمكن قراءة لغات أخرى غير السيريليّة؟** | بالطبع – استبدل `Language.Cyrillic` بـ `Language.English` أو `Language.Arabic` وغيرها. منطق التنزيل التلقائي يعمل بنفس الطريقة. |
| **صورة PNG مشوشة – النتائج سيئة. ماذا أفعل؟** | عالج الصورة مسبقًا: زد التباين، حوّلها إلى تدرج رمادي، أو طبّق مرشح متوسط. Aspose OCR يوفر أيضًا خيارات `Settings.ImagePreprocess`. |
| **هل يمكن الحصول على إطارات حدودية لكل كلمة؟** | نعم، بعد `Recognize()` يمكنك فحص `ocrEngine.Regions` التي تُعيد مستطيلات لكل كلمة مكتشفة. |
| **هل أحتاج رخصة للاستخدام في الإنتاج؟** | النسخة التجريبية المجانية تعمل حتى 100 صفحة. للمشاريع التجارية يُنصح بشراء رخصة – تُزيل علامة التقييم وتفتح معالجة دفعات عالية السرعة. |

---

## الخطوات التالية – توسيع الحل

* **معالجة دفعات:** حلقة تمر على مجلد PNGs، تجمع كل النصوص في ملف CSV.  
* **التكامل مع Azure Cognitive Search:** فهرسة السلاسل السيريليّة المستخرجة للبحث السريع.  
* **دمج مع تحويل PDF:** استخدم Aspose.PDF لتحويل ملفات PDF الممسوحة ضوئيًا إلى PNG أولًا، ثم نفّذ نفس تدفق OCR.  

جميع هذه السيناريوهات تعيد استخدام النمط الأساسي الذي غطيناه: **تحميل الصورة للـ OCR → تحديد اللغة → التعرف → استخدام النص**.

---

## الخلاصة

أصبحت الآن تعرف كيف **تقرا النص من PNG**، **تستخرج النص السيريلي**، و**تحول الصورة إلى نص** باستخدام Aspose OCR في C#. الخطوات الأساسية هي إنشاء المحرك، تحميل الصورة، اختيار اللغة المناسبة (التي تُنزل حزمة اللغة السيريليّة تلقائيًا)، وأخيرًا استدعاء `Recognize()`.

جرّب ذلك مع صور مختلفة، جرب خيارات `Settings`، وشاهد تطبيقاتك تصبح قابلة للبحث، متعددة اللغات، وأكثر ذكاءً.

برمجة سعيدة، ولا تتردد في ترك تعليق إذا واجهت أي صعوبات!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}