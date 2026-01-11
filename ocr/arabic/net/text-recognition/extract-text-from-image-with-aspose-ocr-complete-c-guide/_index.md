---
category: general
date: 2026-01-10
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف، التعرف على النص الهندي، وتشغيل عملية التعرف الضوئي على
  الأحرف في بضع خطوات بسيطة.
draft: false
keywords:
- extract text from image
- recognize hindi text
- load image for ocr
- run ocr recognition
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. اتبع هذا الدليل
  خطوة بخطوة لتحميل الصورة للتعرف الضوئي على الحروف، والتعرف على النص الهندي، وتشغيل
  التعرف الضوئي على الحروف.
og_title: استخراج النص من الصورة باستخدام Aspose OCR – دليل كامل بلغة C#
tags:
- Aspose OCR
- C#
- Image Processing
title: استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل
url: /ar/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة باستخدام Aspose OCR – دليل C# الكامل

هل احتجت يومًا إلى **استخراج النص من صورة** لكنك لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك—فالكثير من المطورين يواجهون هذه المشكلة عندما يتعاملون لأول مرة مع OCR في .NET. الخبر السار هو أن Aspose OCR يجعل العملية بأكملها سهلة بشكل مدهش، حتى عندما تتعامل مع نصوص معقدة مثل الهندية.

في هذا الدرس سنستعرض كل ما تحتاجه **لتحميل صورة للـ OCR**، **لتعرف على النص الهندي**، و**لتشغيل التعرف الضوئي على الأحرف** في C#. في النهاية ستحصل على تطبيق كونسول جاهز للتنفيذ يطبع النص المستخرج مباشرةً على الشاشة.

## ما ستقوم ببنائه

سننشئ تطبيق كونسول صغير يقوم بـ:

1. توجيه محرك OCR إلى مجلد يحتوي على نماذج اللغات.  
2. إيقاف التحميل التلقائي للموارد—مفيد للبيئات المقفلة.  
3. اختيار الهندية كلغة مستهدفة.  
4. تحميل صورة JPEG (أو PNG) تحتوي على نص هندي.  
5. تنفيذ خط أنابيب التعرف.  
6. كتابة السلسلة الناتجة إلى الكونسول.

بدون خدمات خارجية، بدون مفاتيح سحابية، فقط OCR محلي بالكامل.

## المتطلبات المسبقة

- **.NET 6.0** أو أحدث (الكود يعمل أيضًا على .NET Framework 4.7+).  
- حزمة **Aspose.OCR for .NET** من NuGet مثبتة.  
  ```bash
  dotnet add package Aspose.OCR
  ```
- مجلد اسمه `OcrResources` يحتوي على نموذج اللغة الهندية (`hin.traineddata`).  
  يمكنك تنزيله من صفحة تحميل Aspose OCR ووضعه داخل `YOUR_DIRECTORY/OcrResources`.  
- ملف صورة (`input.jpg`) يحتوي على نص هندي واضح.  
  للتوضيح، تخيل صورة لعلامة متجر مكتوب عليها “स्वागत है”.  

> **نصيحة احترافية:** حافظ على دقة الصورة فوق 300 dpi؛ الدقة الأقل قد تؤدي إلى فقدان الأحرف.

---

## الخطوة 1: توجيه محرك OCR إلى مواردك – *extract text from image*

أول شيء يحتاجه Aspose OCR هو موقع نماذج اللغات. إذا تخطيت هذه الخطوة، سيحاول المحرك تنزيل الملفات تلقائيًا—وهو ما قد لا ترغب به في شبكة مؤمنة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;

// Step 1: Tell Aspose where the language resources live
OcrEngine.Config.ResourcesPath = @"YOUR_DIRECTORY/OcrResources";
```

*لماذا هذا مهم:* بتعيين `ResourcesPath` تضمن أن المحرك يحمل بيانات التدريب الصحيحة محليًا، مما يسرّع التشغيل الأول ويزيل أي حركة مرور غير متوقعة على الشبكة.

---

## الخطوة 2: إيقاف التحميل التلقائي للموارد – *load image for OCR*

في العديد من بيئات الشركات، يتم حظر الوصول إلى الإنترنت الخارجي. يدعم Aspose OCR علمًا يوقفه من محاولة جلب الملفات المفقودة تلقائيًا.

```csharp
// Step 2: Prevent the engine from reaching out to the internet
OcrEngine.Config.AllowAutomaticResourceDownload = false;
```

إذا نسيت إضافة هذا السطر ولم يكن نموذج الهندية موجودًا، سيظهر استثناء يشبه “Unable to download required resource”. ضبط العلم على `false` يمنحك فشلًا واضحًا ومحددًا يمكنك معالجته بنفسك.

---

## الخطوة 3: اختيار اللغة – *recognize hindi text*

يدعم Aspose OCR عشرات اللغات، لكن عليك إخبار المحرك أي لغة تريد استخدامها. تُحدد اللغة الهندية بـ `OcrLanguage.Hindi`.

```csharp
// Step 3: Create the OCR engine and set the target language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Hindi
};
```

*ماذا لو احتجت إلى عدة لغات؟* يمكنك تعيين `Language = OcrLanguage.AutoDetect` للسماح للمحرك بالتخمين، لكن الكشف التلقائي أبطأ وقد يخطئ أحيانًا مع النصوص المختلطة. بالنسبة للهندية النقية، الاختيار الصريح هو الأكثر أمانًا.

---

## الخطوة 4: تحميل صورتك – *load image for OCR*

الآن نمرر للمحرك الصورة التي نريد قراءتها. يوفر Aspose المساعد `ImageStream.FromFile` الذي يُبسط الاعتماد على `System.Drawing`.

```csharp
// Step 4: Load the image containing Hindi text
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

إذا كان مسار الملف غير صحيح، سيُطلق Aspose استثناء `FileNotFoundException`. فحص سريع بـ `File.Exists` قبل هذا السطر يمكن أن يوفر عليك جلسة تصحيح الأخطاء.

---

## الخطوة 5: تشغيل محرك OCR – *run OCR recognition*

بعد ضبط كل شيء، نبدأ عملية التعرف. هذه الدالة متزامنة وتُحجب التنفيذ حتى يُستخرج النص.

```csharp
// Step 5: Execute the OCR process
ocrEngine.Recognize();
```

خلف الكواليس، يقوم Aspose بعدة مراحل: ما قبل المعالجة (إزالة الميل، إزالة الضوضاء)، التجزئة، تصنيف الأحرف، وأخيرًا المعالجة اللاحقة الخاصة باللغة. كل هذا يحدث داخل استدعاء الطريقة الواحدة.

---

## الخطوة 6: إخراج النص المستخرج – *extract text from image*

النتيجة تُخزن في خاصية `Text` للمحرك. نكتبها ببساطة إلى الكونسول، لكن يمكنك أيضًا حفظها في قاعدة بيانات، إرسالها عبر API، أو تمريرها إلى خط أنابيب NLP آخر.

```csharp
// Step 6: Print the recognized text
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrEngine.Text);
```

**الناتج المتوقع** (بافتراض أن الصورة تحتوي على “स्वागत है”):

```
=== OCR RESULT ===
स्वागत है
```

إذا رأيت رموزًا مشوشة، تحقق من أن نموذج الهندية موجود في المكان الصحيح وأن الصورة غير مضغوطة بشكل مفرط.

---

## مثال كامل يعمل

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع كونسول جديد (`dotnet new console`). استبدل `YOUR_DIRECTORY` بالمسار الفعلي على جهازك.

```csharp
// ------------------------------------------------------------
// Complete Aspose OCR example – extract text from image
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

class Program
{
    static void Main()
    {
        // 1️⃣ Set the folder where language models are stored
        OcrEngine.Config.ResourcesPath = @"YOUR_DIRECTORY/OcrResources";

        // 2️⃣ Turn off automatic download – useful for offline builds
        OcrEngine.Config.AllowAutomaticResourceDownload = false;

        // 3️⃣ Create the engine and tell it to read Hindi
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Hindi
        };

        // 4️⃣ Load the image file that contains Hindi text
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

        // 5️⃣ Run the OCR process
        ocrEngine.Recognize();

        // 6️⃣ Output the result to the console
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

> **نصيحة:** إذا كنت تخطط لمعالجة العديد من الصور داخل حلقة، أنشئ كائن `OcrEngine` واحد وأعد استخدامه—هذا يقلل من زمن التهيئة.

---

## التعامل مع المشكلات الشائعة

| المشكلة | السبب | الحل السريع |
|-------|----------------|-----------|
| **إخراج فارغ** | نموذج لغة غير صحيح أو صورة منخفضة الجودة. | تحقق من `ResourcesPath`، زد DPI الصورة، أو جرّب `ocrEngine.Image = ImageStream.FromFile(..., true)` لتفعيل التحسين التلقائي. |
| **استثناء: المورد غير موجود** | نقص ملف `.traineddata` للهندية. | نزّل نموذج الهندية من Aspose، وضعه في `OcrResources`، وتأكد من أن اسم الملف هو `hin.traineddata`. |
| **رموز غير مفهومة** | عدم توافق الترميز عند الطباعة إلى الكونسول. | عيّن ترميز الإخراج: `Console.OutputEncoding = System.Text.Encoding.UTF8;`. |
| **بطء الأداء** | معالجة صور كبيرة دون تصغير. | قلّص حجم الصورة إلى عرض/ارتفاع أقصى 2000 px قبل تمريرها إلى OCR. |

---

## الخطوات التالية والمواضيع ذات الصلة

- **المعالجة الدفعية:** غلف الكود داخل حلقة `foreach` لمعالجة مجلد من الصور.  
- **لغات مختلفة:** استبدل `OcrLanguage.Hindi` بـ `OcrLanguage.English` أو `OcrLanguage.Arabic` وغيرها.  
- **تنسيقات الإخراج:** بدلاً من `Console.WriteLine`، احفظ إلى ملف نصي (`File.WriteAllText("result.txt", ocrEngine.Text);`).  
- **التكامل مع ASP.NET Core:** أنشئ نقطة API تستقبل تحميل صورة وتعيد النص المستخرج كـ JSON.  

جميع هذه الامتدادات تتبع نفس النمط—تهيئة المحرك، تحميل صورة، التعرف، واستخدام النتيجة.

---

## الخلاصة

لقد أظهرنا لك كيفية **استخراج النص من الصورة** باستخدام Aspose OCR في C#. يغطي الدليل كل خطوة تحتاجها **لتحميل صورة للـ OCR**، **لتعرف على النص الهندي**، و**لتشغيل التعرف الضوئي**—كل ذلك في تطبيق كونسول مستقل.

جرّبه مع صورك الخاصة، جرب لغات مختلفة، ولا تتردد في تعديل الشيفرة لتناسب الخدمات السحابية أو الوظائف الخلفية. الفكرة الأساسية تبقى واحدة: ضبط الموارد، اختيار اللغة، إمداد صورة، وقراءة خاصية `Text`.

إذا واجهت أي صعوبات، راجع جدول استكشاف الأخطاء أعلاه أو اترك تعليقًا. برمجة سعيدة، ولتكن نتائج OCR دائمًا واضحة كالبلور!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}