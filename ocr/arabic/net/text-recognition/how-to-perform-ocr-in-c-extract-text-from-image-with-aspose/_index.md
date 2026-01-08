---
category: general
date: 2026-01-07
description: كيفية تنفيذ OCR واستخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم
  قراءة النص من الصورة، التعرف على النص الهندي، واحصل على مثال كامل للكود.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from image
- recognize hindi text
- how to extract text from image
language: ar
og_description: كيفية تنفيذ OCR في C# لاستخراج النص من الصورة. يوضح هذا البرنامج التعليمي
  كيفية قراءة النص من الصورة، والتعرف على النص الهندي، واستخراج النص من الصورة باستخدام
  Aspose OCR.
og_title: كيفية تنفيذ OCR في C# – دليل كامل
tags:
- OCR
- C#
- Aspose
title: كيفية تنفيذ OCR في C# – استخراج النص من الصورة باستخدام Aspose OCR
url: /ar/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية تنفيذ OCR في C# – استخراج النص من الصورة باستخدام Aspose OCR

هل تساءلت يومًا **كيف تقوم بتنفيذ OCR** على فاتورة ممسوحة ضوئيًا أو صورة لعلامة؟ لست وحدك. في العديد من المشاريع الواقعية تحتاج إلى **استخراج النص من صورة**، سواء كانت إيصالًا، أو مسحًا ضوئيًا لجواز سفر، أو ملاحظة مكتوبة بخط اليد. الخبر السار؟ باستخدام Aspose.OCR يمكنك فعل ذلك ببضع أسطر من كود C#، وستتعلم أيضًا كيفية **التعرف على النص الهندي** أثناء ذلك.

في هذا الدرس سنستعرض مثالًا كاملاً جاهزًا للتنفيذ **يقرأ النص من صورة**، يوضح لك كيفية **استخراج النص من صورة** باستخدام محرك Aspose OCR، ويشرح “السبب” وراء كل خطوة. لا إشارات غامضة إلى وثائق خارجية—فقط حل متكامل يمكنك نسخه ولصقه وتشغيله اليوم.

## ما ستحتاجه

- .NET 6.0 أو أحدث (الكود يُترجم أيضًا ضد .NET Standard 2.0)
- Visual Studio 2022 (أو أي بيئة تطوير تفضلها)
- حزمة Aspose.OCR من NuGet (`Install-Package Aspose.OCR`)
- ملف صورة يحتوي على نص هندي (مثال: `hindi_invoice.jpg`)
- مجلد موارد لغة OCR المرفق مع Aspose (قم بتنزيله من موقع Aspose)

> **نصيحة احترافية:** احتفظ بمجلد موارد OCR بجوار مشروعك لتسهيل التعامل مع المسارات.

## تنفيذ خطوة بخطوة

فيما يلي نقسم العملية إلى ست خطوات منطقية. كل خطوة لها عنوان H2 الخاص بها (حتى تتمكن محركات البحث والنماذج الذكية من العثور على المعلومات بسرعة) وعنوان فرعي H3 قصير يتضمن كلمات مفتاحية ثانوية.

### الخطوة 1 – تعيين مسار موارد OCR  
**لماذا هذا مهم:** يعتمد Aspose.OCR على حزم اللغة (الخطوط، القواميس، وملفات النماذج) التي توجد في مجلد تحدده. إذا كان المسار غير صحيح، سيطرح المحرك استثناء `FileNotFoundException` ولن تحصل على أي نص من الصورة.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Tell the OCR engine where to find language resources
OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");
```

### الخطوة 2 – إنشاء نسخة من محرك OCR  
**لماذا هذا مهم:** `OcrEngine` هو الكائن الضخم الذي يحمل نموذج التعرف في الذاكرة. وضعه داخل كتلة `using` يضمن التخلص السليم منه، وهو أمر مهم خاصةً عند معالجة عدد كبير من الصور على دفعة.

```csharp
// Instantiate the OCR engine inside a using block
using (var ocrEngine = new OcrEngine())
{
    // Subsequent steps go here...
}
```

### الخطوة 3 – تكوين إعدادات التعرف (اختيار اللغة الهندية)  
**لماذا هذا مهم:** بشكل افتراضي يحاول Aspose اكتشاف اللغة تلقائيًا، لكن تعيين `Language.Hindi` صراحةً يحسن الدقة للخط الديفاناغاري ويسرّع المعالجة.

```csharp
    // Configure the engine to recognize Hindi text
    var recognitionSettings = new RecognitionSettings
    {
        Language = Language.Hindi   // Recognize Hindi characters
    };
```

### الخطوة 4 – تحميل الصورة التي تريد قراءتها  
**لماذا هذا مهم:** `ImageStream.FromFile` يخفف عنك التعامل مع الـ bitmap الأساسي ويقوم ببث البيانات بكفاءة. يمكنك أيضًا استخدام `MemoryStream` إذا كانت الصورة تأتي من طلب ويب.

```csharp
    // Load the target image (replace with your own path)
    var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");
```

### الخطوة 5 – تشغيل عملية OCR  
**لماذا هذا مهم:** طريقة `Recognize` تقوم بالعمل الشاق—المعالجة المسبقة، التجزئة، تصنيف الأحرف، وأخيرًا تجميع النص. تُعيد سلسلة نصية عادية يمكنك تخزينها أو عرضها أو معالجتها لاحقًا.

```csharp
    // Execute OCR and capture the recognized text
    string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);
```

### الخطوة 6 – عرض النص المستخرج  
**لماذا هذا مهم:** للتصحيح السريع عادةً ما تريد كتابة النتيجة إلى وحدة التحكم أو ملف سجل. في بيئة الإنتاج قد تحفظها في قاعدة بيانات أو تمررها إلى سير عمل لاحق.

```csharp
    // Output the result to the console
    Console.WriteLine("=== OCR Result ===");
    Console.WriteLine(recognizedText);
}
```

## مثال كامل يعمل

بتجميع كل ما سبق، إليك البرنامج الكامل الذي يمكنك وضعه في مشروع تطبيق كونسول. تأكد من استبدال مسارات العناصر النائبة بالمسارات الفعلية لديك.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Set the folder that contains language resources
        OcrEngine.SetResourcesPath(@"C:\MyProject\OcrResources");

        // 2️⃣ Create the OCR engine (auto‑disposed)
        using (var ocrEngine = new OcrEngine())
        {
            // 3️⃣ Tell the engine to look for Hindi characters
            var recognitionSettings = new RecognitionSettings
            {
                Language = Language.Hindi
            };

            // 4️⃣ Load the image you want to read
            var imageStream = ImageStream.FromFile(@"C:\MyProject\Images\hindi_invoice.jpg");

            // 5️⃣ Perform OCR
            string recognizedText = ocrEngine.Recognize(imageStream, recognitionSettings);

            // 6️⃣ Show the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);
        }

        // Keep console open (useful when running from VS)
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

**الناتج المتوقع** (مقتطع للوضوح):

```
=== OCR Result ===
Invoice No: 12345
Date: 01/01/2024
Amount: ₹ 15,000
धन्यवाद
```

إذا رأيت رموزًا غير مفهومة بدلاً من الأحرف الهندية، تحقق مرة أخرى من أن مجلد الموارد يشير إلى النسخة الصحيحة من حزمة اللغة الهندية.

## المشكلات الشائعة وكيفية تجاوزها  

| المشكلة | لماذا يحدث | الحل السريع |
|-------|----------------|-----------|
| **حروف غير صحيحة** | موارد لغة خاطئة أو مفقودة | تحقق أن `SetResourcesPath` يشير إلى المجلد الذي يحتوي على `Hindi.cognates` والملفات المرتبطة |
| **أخطاء نفاد الذاكرة** | تحميل صورة ضخمة دون تصغير | استخدم `ImageStream.FromFile(..., maxWidth: 2000)` لتقليل الحجم أثناء التحميل |
| **أداء بطيء** | وضع الكشف التلقائي يفحص لغات متعددة | عيّن صراحةً `Language = Language.Hindi` (أو أي لغة مستهدفة أخرى) |
| **عدم وجود أي ناتج** | الصورة بيضاء تمامًا أو غير واضحة | عالج الصورة مسبقًا (تحسين التباين، التحويل إلى ثنائي) قبل تمريرها إلى OCR |

## توسيع الحل: لغات وسيناريوهات أخرى  

إذا كنت بحاجة إلى **قراءة النص من صورة** بالإنجليزية أو الإسبانية أو أي لغة أخرى، ما عليك سوى تغيير قيمة تعداد `Language`:

```csharp
recognitionSettings.Language = Language.English;   // or Language.Spanish, etc.
```

يمكنك أيضًا دمج عدة لغات:

```csharp
recognitionSettings.Language = Language.English | Language.Hindi;
```

للمعالجة على دفعات، ضع كتلة `using (var ocrEngine = new OcrEngine())` حول حلقة `foreach` التي تتنقل عبر مجلد الصور. سيعيد المحرك استخدام النموذج المحمّل، مما يقلل بشكل كبير من زمن التهيئة.

## اختبار دقة OCR الخاصة بك  

1. شغّل البرنامج باستخدام صورة اختبار معروفة (يمكنك إنشاء PNG بسيط يحتوي على نص هندي باستخدام أي محرر رسومات).  
2. قارن ناتج وحدة التحكم بالنص الأصلي.  
3. إذا كان معدل الخطأ أعلى من 5 %، فكر في تحسين جودة الصورة (زيادة DPI إلى 300 dpi) أو تطبيق خطوة معالجة مسبقة مثل `imageStream = imageStream.ApplyGaussianBlur(1.5)` (توفر Aspose فلاتر أساسية).

## الخلاصة  

لقد أظهرنا **كيفية تنفيذ OCR** في C# باستخدام Aspose.OCR، وبيّنّا كيف **نستخرج النص من صورة**، وتناولنا مثالًا عمليًا ي **يتعرف على النص الهندي**. باتباع الخطوات الست—تعيين مسار الموارد، إنشاء المحرك، ضبط اللغة، تحميل الصورة، تشغيل التعرف، وعرض النتيجة—أصبح لديك الآن مكوّن موثوق لأي مشروع رقمنة مستندات.

الخطوة التالية: جرّب استبدال `Language.Hindi` بلغة أخرى، أو مرّر ناتج OCR إلى خط أنابيب معالجة لغة طبيعية لتصنيف الفواتير تلقائيًا. الاحتمالات لا حصر لها، والنمط الأساسي يبقى نفسه: **قراءة النص من صورة**، ثم القيام بما تحتاجه تطبيقك بالنص المستخرج.

هل لديك أسئلة حول حالات الحافة، تحسين الأداء، أو الترخيص؟ اترك تعليقًا أدناه، وتمنياتنا لك ببرمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}