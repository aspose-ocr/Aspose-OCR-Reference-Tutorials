---
category: general
date: 2026-02-25
description: كيفية استخدام OCR بسرعة في C# لاستخراج النص من الصورة، تحميل الصورة لـ
  OCR، وتعيين لغة OCR باستخدام Aspose OCR. دليل خطوة بخطوة.
draft: false
keywords:
- how to use OCR
- extract text from image
- load image for OCR
- set OCR language
language: ar
og_description: تعلم كيفية استخدام OCR في C# لاستخراج النص من الصورة، وتحميل الصورة
  للـ OCR، وتعيين لغة الـ OCR باستخدام Aspose OCR. مثال كامل غير متزامن.
og_title: كيفية استخدام OCR في C# – دليل كامل غير متزامن
tags:
- C#
- Aspose OCR
- async programming
title: كيفية استخدام OCR في C# – استخراج النص من الصورة بشكل غير متزامن
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-asynchronously/
---

-backtop-button >}}

All good.

Now produce final output with same formatting.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصورة بشكل غير متزامن

هل احتجت يومًا إلى **how to use OCR** على إيصال أو فاتورة أو نموذج ممسوح وتساءلت لماذا أمثلة الشيفرة التي تجدها إما غير مكتملة أو عالقة في التنفيذ المتزامن؟ لست وحدك. في العديد من التطبيقات الواقعية تريد **extract text from image** دون تجميد واجهة المستخدم، وتريد أيضًا مرونة اختيار اللغة المناسبة للتعرف.

في هذا الدرس سنستعرض مثالًا كاملًا وقابلًا للتنفيذ يوضح لك بالضبط كيفية **load image for OCR**، وتكوين خيار **set OCR language**، وتشغيل التعرف بشكل غير متزامن. في النهاية ستحصل على تطبيق console مستقل يطبع النص المعترف به إلى وحدة التحكم، بالإضافة إلى مجموعة من النصائح للتعامل مع الحالات الحدية وتوسيع الحل.

## المتطلبات المسبقة

- .NET 6.0 أو أحدث (الكود يعمل مع .NET Core و .NET Framework أيضًا)  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) مثبتة  
- ملف صورة تجريبي (مثال: `receipt.jpg`) موجود في مجلد يمكنك الإشارة إليه  
- معرفة أساسية بـ C# – لا تحتاج إلى أي حيل متقدمة للـ async، فقط الأساسيات  

إذا كنت تفتقد أيًا منها، احصل على حزمة NuGet باستخدام `dotnet add package Aspose.OCR` وأنشئ مجلدًا بسيطًا لصورة الاختبار الخاصة بك. لا شيء معقد.

---

## كيفية استخدام OCR: تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى أربع خطوات منطقية. كل خطوة لها عنوان H2 الخاص بها، والعنوان الأول يكرر الكلمة الرئيسية لتلبية متطلبات SEO.

### الخطوة 1 – تهيئة محرك OCR (How to Use OCR)

أول شيء تحتاجه هو نسخة من `OcrEngine`. فكر فيها كالعقل وراء العملية؛ فهي تحتفظ بالإعدادات، والصورة، والنتيجة.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task RunAsync()
    {
        // Create the OCR engine – this object will manage everything.
        var ocrEngine = new OcrEngine();

        // Next steps will configure it further.
```

**لماذا هذا مهم:**  
إنشاء المحرك مرة واحدة وإعادة استخدامه يمكن أن يحسن الأداء عندما تعالج العديد من الصور. كما يمنحك مكانًا واحدًا لتعيين الخيارات العامة مثل اللغة.

### الخطوة 2 – تعيين لغة OCR (Set OCR Language Properly)

إذا تخطيت اختيار اللغة، فإن Aspose OCR يفرض اللغة الإنجليزية افتراضيًا، قد يكون ذلك مناسبًا للإيصالات ولكن ليس للمستندات الأجنبية. تعيين اللغة يكون بسطر واحد فقط:

```csharp
        // Set the recognition language to English.
        // You can change OcrLanguage.French, OcrLanguage.Spanish, etc.
        ocrEngine.Config.Language = OcrLanguage.English;
```

**نصيحة احترافية:**  
عندما تحتاج إلى دعم متعدد اللغات، يمكنك تمرير مصفوفة من اللغات (`OcrLanguage.English | OcrLanguage.French`). سيحاول المحرك كل لغة بالترتيب، وهو مفيد للإيصالات ذات اللغات المختلطة.

### الخطوة 3 – تحميل الصورة لـ OCR (Load Image for OCR Efficiently)

الآن نوجه المحرك إلى الملف الذي نريد قراءته. توفر Aspose الدالة `ImageStream.FromFile`، التي تُجرد التعامل مع الـ stream الأساسي.

```csharp
        // Load the image you want to analyze.
        // Replace the path with the actual location of your image file.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

**حالة حدية:**  
إذا كان مسار الملف غير صحيح أو تنسيق الصورة غير مدعوم، فإن `FromFile` يرمي استثناءً. غلف ذلك بكتلة try/catch إذا كنت تبني واجهة مستخدم قوية.

### الخطوة 4 – تنفيذ التعرف غير المتزامن (Extract Text from Image)

هنا يحدث السحر. طريقة `RecognizeAsync` تشغل OCR على خيط خلفي، مما يحرر الخيط المستدعي—مثالي لواجهات المستخدم أو تطبيقات الويب.

```csharp
        // Run OCR asynchronously.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Display the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**ما ستراه:**  
إذا كان `receipt.jpg` يحتوي على النص “Total: $12.34”، فإن مخرجات وحدة التحكم ستكون:

```
OCR completed:
Total: $12.34
```

**لماذا غير متزامن؟**  
يمكن أن يحجز OCR المتزامن الخيط لعدة ثوانٍ، خاصةً مع الصور عالية الدقة. استخدام `await` يبقي تطبيقك مستجيبًا ويتعامل بسلاسة مع خطوط طلبات ASP.NET Core.

---

## مثال كامل يعمل

انسخ المقتطف الكامل أدناه إلى مشروع console جديد (`dotnet new console`) وشغّله. تذكر استبدال `YOUR_DIRECTORY/receipt.jpg` بالمسار الفعلي لصورتك.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Enums;

public class AsyncExample
{
    public static async Task Main(string[] args)
    {
        await RunAsync();
    }

    public static async Task RunAsync()
    {
        // Step 1: Create the OCR engine.
        var ocrEngine = new OcrEngine();

        // Step 2: Set the OCR language (English by default).
        ocrEngine.Config.Language = OcrLanguage.English;

        // Step 3: Load the image you want to process.
        // Ensure the file exists; otherwise an exception is thrown.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // Step 4: Perform asynchronous OCR recognition.
        var ocrResult = await ocrEngine.RecognizeAsync();

        // Output the recognized text.
        Console.WriteLine("OCR completed:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**المخرجات المتوقعة** (بافتراض أن الصورة تحتوي على نص إنجليزي قابل للقراءة):

```
OCR completed:
Your extracted text appears here, line by line.
```

إذا رأيت سلسلة فارغة، تحقق مرة أخرى من وضوح الصورة وأن إعداد اللغة يتطابق مع النص.

---

## الأخطاء الشائعة وكيفية تجنبها

| المشكلة | لماذا يحدث | الحل |
|-------|----------------|-----|
| **نتيجة فارغة** | صورة منخفضة الدقة أو لغة غير صحيحة | استخدم مسحًا بدقة أعلى، أو عيّن `ocrEngine.Config.Language` إلى اللغة الصحيحة |
| **استثناء في `FromFile`** | مسار خاطئ أو تنسيق غير مدعوم | تحقق من المسار، استخدم مسارات مطلقة، أو حوّل الصورة إلى PNG/JPEG أولاً |
| **بطء الأداء** | معالجة دفعة كبيرة بشكل متزامن | عالج الصور بالتوازي باستخدام `Task.WhenAll` وأعد استخدام نسخة واحدة من `OcrEngine` |
| **تسرب الذاكرة** | عدم تحرير الـ streams في كود التحميل المخصص | اعتمد على `ImageStream.FromFile` الذي يدير الإغلاق، أو استخدم كتل `using` إذا قمت بالتحميل يدويًا |

**نصيحة إضافية:**  
إذا كنت بحاجة لاستخراج بيانات منظمة (مثلاً أزواج المفتاح‑القيمة من الإيصالات)، فكر في معالجة `ocrResult.Text` لاحقًا باستخدام تعبيرات نمطية أو مكتبة NLP خفيفة.

---

## توسيع الحل

الآن بعد أن عرفت **how to use OCR** لصورة واحدة، قد تسأل، “ماذا لو كان لدي عشرات الإيصالات كل ليلة؟”

- **معالجة دفعات:** غلف منطق `RunAsync` داخل حلقة وجمع النتائج في قائمة.  
- **التوازي:** استخدم `Parallel.ForEach` مع دعم async (`Parallel.ForEachAsync` في .NET 6) لتشغيل عدة عمليات التعرف في وقت واحد.  
- **حفظ النتائج:** احفظ `ocrResult.Text` في قاعدة بيانات، أو اكتبها إلى ملف CSV للتحليلات اللاحقة.  

كل هذه الإضافات لا تزال تعتمد على الخطوات الأساسية التي غطيناها: تهيئة المحرك، تعيين اللغة، تحميل الصورة، واستدعاء `RecognizeAsync`.

---

## ملخص بصري

![مثال على كيفية استخدام OCR](/images/ocr-example.png "كيفية استخدام OCR في C# مع Aspose OCR")

*يوضح المخطط أعلاه التدفق من تحميل الصورة إلى استلام النص المعترف به.*

---

## الخلاصة

لقد استعرضنا للتو مثالًا كاملًا وجاهزًا للإنتاج يوضح **how to use OCR** في C# لـ **extract text from image**، **load image for OCR**، و **set OCR language** بشكل صحيح—كل ذلك مع الحفاظ على استجابة واجهة المستخدم باستخدام الاستدعاءات غير المتزامنة.

في برنامج نصي واحد ومستقل الآن لديك كل ما تحتاجه لبدء استخراج النص من الصور، الإيصالات، أو أي مستند ممسوح. من هنا يمكنك التوسع إلى دفعات، إضافة معالجة الأخطاء، أو دمج النتائج في سير عمل أكبر.

هل أنت مستعد للخطوة التالية؟ جرّب استبدال `OcrLanguage.English` بلغة أخرى، جرب صيغ صور مختلفة، أو اربط الناتج بقاعدة بيانات بسيطة. الاحتمالات واسعة بقدر المستندات التي تحتاج إلى قراءتها.

هل لديك أسئلة أو واجهت مشكلة؟ اترك تعليقًا أدناه، وتمنياتنا لك بالبرمجة السعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}