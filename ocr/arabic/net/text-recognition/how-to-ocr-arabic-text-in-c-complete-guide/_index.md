---
category: general
date: 2026-05-28
description: كيفية التعرف الضوئي على الأحرف (OCR) للغة العربية في C# باستخدام Aspose.OCR.
  تعلم التعرف على النص العربي من ملفات PNG، استخراج النص من الصورة وتحميل الصورة للتعرف
  الضوئي على الأحرف في دقائق.
draft: false
keywords:
- how to OCR Arabic
- recognize Arabic text
- extract text from image
- recognize text from PNG
- load image for OCR
language: ar
og_description: كيفية التعرف الضوئي على الحروف (OCR) للغة العربية في C# باستخدام Aspose.OCR.
  يوضح لك هذا الدرس كيفية التعرف على النص العربي من صور PNG، استخراج النص من الصورة،
  وتحميل الصورة للتعرف الضوئي على الحروف.
og_title: كيفية التعرف الضوئي على النص العربي في C# – دليل خطوة بخطوة
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to OCR Arabic in C# using Aspose.OCR. Learn to recognize Arabic
    text from PNG files, extract text from image and load image for OCR in minutes.
  headline: How to OCR Arabic Text in C# – Complete Guide
  type: TechArticle
- description: How to OCR Arabic in C# using Aspose.OCR. Learn to recognize Arabic
    text from PNG files, extract text from image and load image for OCR in minutes.
  name: How to OCR Arabic Text in C# – Complete Guide
  steps:
  - name: 1. *What if the Arabic language pack doesn’t download?*
    text: 'Aspose.OCR attempts to fetch the pack from its CDN. If the download fails
      (e.g., due to firewall restrictions), download the `Arabic.zip` manually from
      Aspose’s support portal and set:'
  - name: 2. *Can I OCR multiple images in a loop?*
    text: Absolutely. Just move the `engine.Image = …` line inside a `foreach` that
      iterates over your file list. Re‑using the same `OcrEngine` instance saves memory
      because the language model stays cached.
  - name: 3. *What about mixed‑language documents (Arabic + English)?*
    text: 'Set `engine.Configuration.Language = Language.Multilingual` or specify
      a list like:'
  - name: 4. *Do I need to pre‑process the image?*
    text: For best results, ensure the PNG is high‑contrast and not heavily compressed.
      Simple preprocessing—like converting to grayscale or applying a slight blur
      removal—can be done with `engine.Image = ImageProcessor.ApplyFilters(engine.Image,
      ...)` (Aspose provides a set of filters).
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: كيفية التعرف الضوئي على النص العربي في C# – دليل كامل
url: /ar/net/text-recognition/how-to-ocr-arabic-text-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على النص العربي في C# – دليل كامل

هل تساءلت يومًا **كيف تقوم بالتعرف الضوئي على النص العربي** باستخدام C# دون قضاء أيام في البحث عن المكتبة المناسبة؟ لست وحدك. يواجه العديد من المطورين صعوبة عندما يحتاجون إلى التعرف على النص العربي من ملف PNG، خاصةً لأن النصوص من اليمين إلى اليسار تحتاج إلى عناية إضافية.  

في هذا الدرس سنستعرض مثالًا عمليًا بالكامل ي **يتعرف على النص العربي**، **يستخرج النص من الصورة**، ويظهر لك الخطوات الدقيقة **لتحميل الصورة للتعرف الضوئي** باستخدام Aspose.OCR. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع السلسلة العربية مباشرةً في الكونسول.

> **ما ستحصل عليه:** قائمة كاملة بالكود، شرح واضح لكل علم من أعلام الإعداد، ونصائح للتعامل مع المشكلات الشائعة مثل حزم اللغات المفقودة أو المستندات ذات الاتجاه المختلط.

## المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يعمل أيضًا على .NET Core 3.1)
- Visual Studio 2022 أو أي محرر يمكنه بناء مشاريع C#
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) – قم بتثبيتها باستخدام `dotnet add package Aspose.OCR`
- صورة PNG نموذجية تحتوي على نص عربي (سنطلق عليها `arabic_sign.png`)

لا تحتاج إلى أي محركات OCR إضافية أو أدوات خارجية؛ تقوم Aspose.OCR بتنزيل بيانات اللغة العربية تلقائيًا في المرة الأولى التي تشغل فيها الكود.

![مثال على كيفية التعرف الضوئي على النص العربي](/images/how-to-ocr-arabic.png "مثال على كيفية التعرف الضوئي على النص العربي")

*نص بديل للصورة: مثال على كيفية التعرف الضوئي على النص العربي يُظهر مخرجات الكونسول للنص العربي المُتعرف عليه.*

## الخطوة 1: إنشاء مشروع كونسول جديد

أولاً، أنشئ مشروع كونسول جديد لتتمكن من اختبار الكود بشكل منفصل.

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** إذا كنت على نظام Windows وتفضّل Visual Studio، فقط أنشئ مشروع *Console App* وأضف حزمة NuGet عبر الواجهة الرسومية.

## الخطوة 2: تهيئة محرك OCR

جوهر العملية هو الفئة `OcrEngine`. إنشاء كائن منها يضبط خط أنابيب OCR الداخلي.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Step 2: Create an OCR engine instance
var engine = new OcrEngine();
```

*لماذا هذا مهم:* المحرك يحتفظ بالإعدادات مثل اللغة، اتجاه النص، ومصدر الصورة. بدون محرك مهيأ بشكل صحيح، لن يعرف المعرّف أي نموذج لغة يجب تطبيقه.

## الخطوة 3: ضبط اللغة العربية واتجاه النص

العربية لغة من اليمين إلى اليسار، لذا نحتاج إلى إبلاغ المحرك باللغتين والاتجاه. تقوم Aspose.OCR بتنزيل حزمة اللغة العربية تلقائيًا إذا لم تكن مخزنة مسبقًا.

```csharp
// Step 3: Set language to Arabic (auto‑download if missing)
engine.Configuration.Language = Language.Arabic;

// Preserve right‑to‑left ordering for Arabic text
engine.Configuration.TextDirection = TextDirection.RightToLeft;
```

> **حالة خاصة:** إذا شغّلت الكود خلف بروكسي مؤسسي، قد يفشل التنزيل التلقائي. في هذه الحالة، قم بتنزيل حزمة اللغة يدويًا من موقع Aspose وعيّن `engine.Configuration.LanguageDataPath` إلى المجلد.

## الخطوة 4: تحميل الصورة للتعرف الضوئي

الآن نقوم بتحميل ملف PNG إلى الذاكرة. المساعد `ImageStream.FromFile` يقرأ الملف وينشئ تمثيلًا داخليًا للصورة متوافقًا مع Aspose.OCR.

```csharp
// Step 4: Load the image you want to recognize
engine.Image = ImageStream.FromFile(@"./arabic_sign.png");
```

*لماذا هذه الخطوة حاسمة:* محرك OCR لا يمكنه العمل إلا على كائن صورة، وليس على مسار ملف. استخدام `ImageStream.FromFile` يعزل معالجة الصيغ، بحيث يمكنك لاحقًا استبدال JPEG أو BMP دون تعديل باقي الكود.

## الخطوة 5: إجراء التعرف

بعد ضبط اللغة والاتجاه والصورة، استدعِ `Recognize()` لاستخراج السلسلة العربية.

```csharp
// Step 5: Run the recognition
string recognizedText = engine.Recognize();
```

تُعيد الطريقة `string` عادي. إذا احتوت الصورة على عدة أسطر، يتم فصلها بواسطة أحرف السطر الجديد (`\n`).

## الخطوة 6: إخراج النص العربي المتعرف عليه

أخيرًا، اطبع النتيجة إلى الكونسول. ستظهر الأحرف العربية بشكل صحيح إذا كان الكونسول يدعم Unicode (Windows Terminal أو الطرفية المدمجة في VS Code تعمل بشكل جيد).

```csharp
// Step 6: Display the result
Console.WriteLine("Recognized Arabic text:");
Console.WriteLine(recognizedText);
```

**الناتج المتوقع (مثال):**

```
Recognized Arabic text:
مطار
```

إذا رأيت رموزًا مشوشة، تحقق مرة أخرى من أن صفحة الترميز في الكونسول مضبوطة على UTF‑8:

```cmd
chcp 65001
```

## مثال كامل يعمل

فيما يلي ملف `Program.cs` الكامل الذي يمكنك نسخه ولصقه في مشروعك. لا توجد أجزاء مفقودة—هذا مقطع جاهز للنسخ والتنفيذ.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            var engine = new OcrEngine();

            // Configure for Arabic language and RTL direction
            engine.Configuration.Language = Language.Arabic;
            engine.Configuration.TextDirection = TextDirection.RightToLeft;

            // Load the PNG image (replace with your actual path)
            engine.Image = ImageStream.FromFile(@"./arabic_sign.png");

            // Run recognition
            string recognizedText = engine.Recognize();

            // Output result
            Console.WriteLine("Recognized Arabic text:");
            Console.WriteLine(recognizedText);
        }
    }
}
```

شغّله باستخدام:

```bash
dotnet run
```

يجب أن ترى العبارة العربية مطبوعة في الكونسول، مما يؤكد أنك نجحت في **التعرف على النص العربي** من صورة PNG.

## التعامل مع الأسئلة الشائعة

### 1. *ماذا لو لم يتم تنزيل حزمة اللغة العربية؟*  
تحاول Aspose.OCR جلب الحزمة من شبكة CDN الخاصة بها. إذا فشل التنزيل (مثلاً بسبب قيود الجدار الناري)، قم بتنزيل `Arabic.zip` يدويًا من بوابة دعم Aspose واضبط:

```csharp
engine.Configuration.LanguageDataPath = @"C:\Aspose\OCR\Languages";
```

### 2. *هل يمكنني التعرف على عدة صور في حلقة؟*  
بالتأكيد. فقط انقل سطر `engine.Image = …` داخل حلقة `foreach` التي تت iterates over your file list. إعادة استخدام نفس كائن `OcrEngine` يوفر الذاكرة لأن نموذج اللغة يبقى مخزنًا مؤقتًا.

### 3. *ماذا عن المستندات متعددة اللغات (العربية + الإنجليزية)؟*  
عيّن `engine.Configuration.Language = Language.Multilingual` أو حدد قائمة مثل:

```csharp
engine.Configuration.Language = Language.Arabic | Language.English;
```

سيحاول المحرك كلا النموذجين ويختار الأنسب لكل جزء.

### 4. *هل أحتاج إلى معالجة مسبقة للصورة؟*  
للحصول على أفضل النتائج، تأكد من أن PNG ذات تباين عالي وغير مضغوطة بشكل كبير. يمكن إجراء معالجة بسيطة—مثل التحويل إلى تدرج الرمادي أو إزالة الضبابية الخفيفة—باستخدام `engine.Image = ImageProcessor.ApplyFilters(engine.Image, ...)` (توفر Aspose مجموعة من الفلاتر).

## نصائح احترافية وأفضل الممارسات

- **تخزين المحرك في الذاكرة المؤقتة:** إنشاء `OcrEngine` جديد لكل صورة يضيف عبئًا. احتفظ بنسخة واحدة حية للمعالجة الدفعية.
- **ضبط DPI يدويًا** إذا كانت الصور المصدرية ممسوحة بدقة منخفضة؛ يعمل Aspose.OCR بأفضل أداء عند 300 DPI أو أعلى.
- **تسجيل درجات الثقة الخام** (`engine.Result.Confidence`) عندما تحتاج لتحديد ما إذا كنت ستقبل أو ترفض نتيجة التعرف.
- **دمج مع تحويل PDF:** إذا كان لديك ملفات PDF ممسوحة، استخرج كل صفحة كصورة (باستخدام Aspose.PDF) ومرّرها إلى نفس خط أنابيب OCR.

## الخلاصة

أنت الآن تعرف **كيفية التعرف الضوئي على النص العربي** في C# باستخدام Aspose.OCR، من تحميل ملف PNG إلى استخراج الأحرف العربية النقية. يغطي الدرس جميع أعلام الإعداد التي تحتاجها **للتعرف على النص العربي**، وكيفية **استخراج النص من الصورة**، والطريقة الدقيقة **لتحميل الصورة للتعرف الضوئي**.

من هنا، جرّب إمداد المحرك بمجموعة من صور لعلامات الشوارع، جرب صيغ صور مختلفة، أو أضف معالجة لاحقة لترجمة العربية المتعرف عليها إلى لغة أخرى. الاحتمالات واسعة، والنمط الأساسي يبقى كما هو.

هل لديك المزيد من الأسئلة حول التعرف على النص من ملفات PNG، أو التعامل مع لغات أخرى من اليمين إلى اليسار، أو تحسين سرعة OCR؟ اترك تعليقًا أدناه، وبرمجة سعيدة!

## دروس ذات صلة

- [استخراج نص الصورة في C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [كيفية استخراج النص من الصورة عن طريق إعداد المستطيلات في OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}