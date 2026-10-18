---
category: general
date: 2026-03-21
description: كيفية استخدام OCR في C# للتعرف على النص من ملفات الصور. تعلم استخراج
  النص العربي من ملف JPG وتحويله إلى نص عادي.
draft: false
keywords:
- how to use OCR
- extract arabic text
- recognize text from image
- image to text c#
- convert jpg to text
language: ar
og_description: كيفية استخدام OCR في C# للتعرف على النص من ملفات الصور. يوضح هذا الدليل
  كيفية استخراج النص العربي من ملف JPG وتحويله إلى نص قابل للتعديل.
og_title: كيفية استخدام OCR في C# – استخراج النص العربي من JPG
tags:
- OCR
- C#
- Aspose
- Arabic
title: كيفية استخدام OCR في C# – استخراج النص العربي من ملف JPG
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-arabic-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص العربي من JPG

هل تساءلت يوماً **كيف تستخدم OCR** عندما يكون لديك صورة لنص عربي مخزنة على القرص الصلب؟ لست وحدك. يواجه العديد من المطورين نفس المشكلة: لديهم ملف JPEG، يحتاجون إلى الكلمات الموجودة داخله، ولا يرغبون في كتابة شبكة عصبونية من الصفر.  

الخبر السار؟ ببضع أسطر من C# يمكنك **التعرف على النص من ملفات الصور**، استخراج كل حرف عربي، والحصول على سلسلة نصية نظيفة يمكنك تخزينها أو البحث فيها أو عرضها. في هذا الدرس سنستعرض العملية بالكامل—تثبيت المكتبة، ضبط نموذج اللغة، تشغيل الفحص، وأخيراً طباعة النتيجة. في النهاية ستتمكن من **تحويل JPG إلى نص** في ثوانٍ معدودة.

## ما ستتعلمه

- تثبيت حزمة NuGet **Aspose.OCR** لـ .NET.  
- تهيئة محرك OCR في وضع CPU (مثالي للمهام الصغيرة).  
- تحميل نموذج اللغة العربية تلقائيًا.  
- تشغيل OCR على صورة JPEG واسترجاع النص المُتعرف عليه.  
- التعامل مع المشكلات الشائعة مثل الملفات الكبيرة أو نقص بيانات اللغة.

لا تحتاج إلى خبرة سابقة في OCR؛ فقط فهم أساسي لـ C# وVisual Studio يكفي. جاهز؟ لنبدأ.

## تثبيت Aspose OCR لـ .NET

قبل تشغيل أي كود، تحتاج إلى مكتبة Aspose.OCR. تُوزَّع كمكتبة NuGet، لذا فإن التثبيت يكون بأمر واحد:

```bash
dotnet add package Aspose.OCR
```

أو، إذا كنت تفضّل واجهة Visual Studio، افتح **Tools → NuGet Package Manager → Manage NuGet Packages for Solution**، ابحث عن **Aspose.OCR**، وانقر **Install**. الحزمة تجلب لك كل ما تحتاجه، بما في ذلك ملفات بيانات اللغة التي سيقوم المحرك بتحميلها عند الاستخدام الأول.

> **نصيحة محترف:** احرص على أن يكون مشروعك يستهدف .NET 6 أو أحدث؛ الإطارات الأقدم ما زالت تعمل لكنك ستفقد تحسينات الأداء.

## تهيئة محرك OCR

الآن بعد أن أصبحت المكتبة موجودة، يمكننا إنشاء مثيل من `OcrEngine`. بالنسبة لمعظم المهام الصغيرة، وضع CPU الافتراضي يكفي—فهو يستخدم معالج الجهاز ويتجنب الإعدادات الإضافية المطلوبة لتسريع GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialise the OCR engine (CPU mode is sufficient for small jobs)
var ocrEngine = new OcrEngine();
```

لماذا ننشئ محركًا جديدًا في كل مرة؟ كائن `OcrEngine` يحمل إعدادات مثل اللغة، DPI، وتنسيق الإخراج. بالحفاظ عليه محصورًا في عملية واحدة تضمن حالة نظيفة وتتفادى التداخل غير المقصود بين نماذج لغات مختلفة.

## تحميل نموذج اللغة العربية

تُوفر Aspose حزم اللغة عند الطلب. في المرة الأولى التي تعيين فيها `Language.Arabic`، ستقوم المكتبة بتحميل حوالي 30 ميغابايت من البيانات إلى مجلد التخزين المؤقت على جهازك. هذا التحميل لمرة واحدة يجعل التشغيل اللاحق سريعًا جدًا.

```csharp
// Choose the language model to load.
// The first assignment triggers an automatic download of the language data (~30 MB).
ocrEngine.Settings.Language = Language.Arabic;
```

إذا احتجت إلى دعم نصوص إضافية (مثل الإنجليزية أو الهندية)، فقط غيّر قيمة الـ enum—لا حاجة لإضافة كود إضافي. سيخزن المحرك كل لغة في ذاكرة مؤقتة منفصلة.

## تشغيل OCR على صورة JPG

مع جاهزية المحرك وتحميل نموذج العربية، وجهه إلى الصورة التي تريد معالجتها. يمكن أن يكون المسار مطلقًا أو نسبيًا؛ فقط تأكد من وجود الملف وقابليته للقراءة.

```csharp
// Run OCR on the input image.
var recognitionResult = ocrEngine.Recognize(@"YOUR_DIRECTORY/arabic_doc.jpg");
```

**حالة حافة:** إذا كان ملف JPEG كبيرًا (أكثر من 5 ميغابايت) قد ترغب في تقليل حجمه أولًا. الصور الكبيرة تستهلك ذاكرة أكثر وتبطئ عملية التعرف. يمكن لتقليل الحجم مسبقًا باستخدام `System.Drawing` أو `ImageSharp` أن يقلل وقت المعالجة بشكل ملحوظ.

## استرجاع وعرض النص المُتعرف عليه

طريقة `Recognize` تُعيد كائن `OcrResult`. خاصية `Text` فيه تحتوي على تمثيل النص العادي لكل ما تمكن المحرك من قراءته.

```csharp
// Retrieve the recognised text and output it.
string extractedText = recognitionResult.Text;
Console.WriteLine(extractedText);
```

عند تشغيل البرنامج يجب أن ترى الأحرف العربية مطبوعة في وحدة التحكم، مع الحفاظ على الترتيب الأصلي وفواصل الأسطر. إذا رغبت في حفظ النص في ملف بدلاً من ذلك، استخدم `File.WriteAllText`.

### مثال كامل يعمل

بدمج كل ما سبق، إليك تطبيق console جاهز للتنفيذ:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine (CPU mode works fine for most cases)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the Arabic language pack – triggers a one‑time download (~30 MB)
        ocrEngine.Settings.Language = Language.Arabic;

        // 3️⃣ Specify the image path – replace with your actual file location
        string imagePath = @"YOUR_DIRECTORY/arabic_doc.jpg";

        // 4️⃣ Run OCR and capture the result
        var result = ocrEngine.Recognize(imagePath);

        // 5️⃣ Extract the text and display it
        string extractedText = result.Text;
        Console.WriteLine("=== Extracted Arabic Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**الناتج المتوقع (مثال):**

```
=== Extracted Arabic Text ===
هذا نص تجريبي باللغة العربية
تم استخراج هذا النص بنجاح
```

إذا ظهر النص مشوّهًا، تحقق من وضوح الصورة وأن اللغة تم ضبطها إلى `Arabic`. المسحات الضبابية أو الصفحات المائلة هي من أكثر الأسباب التي تُعرقل OCR.

## أسئلة شائعة ونصائح

- **ماذا لو احتوت الصورة على العربية والإنجليزية معًا؟**  
  اضبط `ocrEngine.Settings.Language = Language.Multilingual;` لتسمح لـ Aspose باكتشاف عدة نصوص تلقائيًا.

- **هل يمكن تسريع المعالجة باستخدام GPU؟**  
  نعم—استبدل المحرك الافتراضي بـ `new OcrEngine(OcrEngineMode.Gpu)` إذا كان لديك بطاقة رسومية متوافقة وبيئة تشغيل CUDA مثبتة.

- **كيف أتعامل مع العرض من اليمين إلى اليسار في الواجهة؟**  
  السلسلة الخام هي Unicode؛ معظم أطر الواجهة الحديثة (WinForms, WPF, ASP.NET) تدعم تخطيط RTL تلقائيًا عند ضبط `FlowDirection` المناسب.

- **هل هناك حد لحجم الصورة؟**  
  تقنيًا لا يوجد، لكن استهلاك الذاكرة يزداد مع الدقة. للماسحات الضخمة (مثل الكتب الممسوحة)، يفضَّل معالجة صفحة واحدة في كل مرة.

## نظرة بصرية عامة

فيما يلي مخطط بسيط يوضح تدفق العملية من ملف الصورة إلى النص المستخرج.  

![مخطط تدفق كيفية استخدام OCR – تحويل الصورة إلى نص](/images/ocr-flow.png)

*النص البديل:* *مخطط تدفق كيفية استخدام OCR يُظهر تحويل الصورة إلى نص في C#.*

## الخطوات التالية

الآن بعد أن أتقنت **كيفية استخدام OCR** للصور JPEG العربية، يمكنك توسيع الحل:

- **المعالجة الدفعية:** كرّر العملية على مجلد من الصور واكتب كل نتيجة في ملف `.txt` منفصل.  
- **ما بعد المعالجة:** استخدم تعبيرات نمطية (regex) لتنظيف علامات الترقيم أو فواصل الأسطر الزائدة.  
- **التكامل:** أدخل السلاسل المستخرجة في فهرس بحث (مثل Azure Cognitive Search) للبحث النصي الكامل عبر المستندات الممسوحة.

إذا كنت مهتمًا بلغات أخرى، فقط غيّر قيمة الـ `Language` enum. هل تريد استخراج الجداول أو الملاحظات المكتوبة يدويًا؟ تقدم Aspose.OCR أيضًا ميزات `LayoutAnalysis` التي يمكنها تقسيم الكتل قبل التعرف.

---

### TL;DR

أنت الآن تعرف **كيفية استخدام OCR** في C# **لاستخراج النص العربي** من ملف JPEG، أي **التعرف على النص من ملفات الصور** و**تحويل JPG إلى نص**. المثال الكامل القابل للتنفيذ أعلاه يوضح كل خطوة، من تثبيت حزمة NuGet إلى طباعة السلسلة النهائية. احصل على صورة تجريبية، الصق الكود، وشاهد السحر يحدث—بدون الحاجة إلى خدمات خارجية. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}