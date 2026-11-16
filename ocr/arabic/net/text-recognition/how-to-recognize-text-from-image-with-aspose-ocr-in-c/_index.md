---
category: general
date: 2026-08-22
description: تعلم كيفية التعرف على النص من الصورة باستخدام Aspose.OCR. يغطي هذا الدليل
  أيضًا تحويل الصورة إلى نص باستخدام OCR واستخراج النص من ملف JPG في بضع خطوات.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- ocr image to text
- extract text from jpg
- convert image to text
- read cyrillic text image
language: ar
lastmod: 2026-08-22
og_description: التعرف على النص من الصورة باستخدام Aspose.OCR في C#. اتبع هذا الدرس
  لتحويل الصورة إلى نص، استخراج النص من ملف JPG، وقراءة النص السيريلي من الصورة.
og_image_alt: Screenshot of C# console output showing recognized Cyrillic text from
  a JPG image
og_title: التعرف على النص من الصورة باستخدام Aspose.OCR – دليل خطوة بخطوة بلغة C#
schemas:
- author: Aspose
  dateModified: '2026-08-22'
  description: Learn to recognize text from image using Aspose.OCR. This guide also
    covers OCR image to text and extract text from jpg in a few steps.
  headline: How to recognize text from image with Aspose.OCR in C#
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: كيفية التعرف على النص من الصورة باستخدام Aspose.OCR في C#
url: /ar/net/text-recognition/how-to-recognize-text-from-image-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# التعرف على النص من الصورة باستخدام Aspose.OCR – دليل C# كامل

إذا كنت بحاجة إلى التعرف على النص من صورة في مشروع .NET، يوضح لك هذا الدليل حلاً جاهزًا للتنفيذ. ستتعرف على كيفية إعداد محرك OCR، اختيار وحدة اللغة الصحيحة، وإخراج الأحرف المستخرجة. كما يوضح المثال كيفية تحويل صورة سيريليّة إلى نص، وهو ما يغطي الحالة الشائعة لقراءة ملفات الصور التي تحتوي على نص سيريلي.

إلى جانب الخطوات الأساسية، ستتعلم كيفية استخراج النص من ملفات jpg، تحويل الصورة إلى نص لصيغ أخرى، ومعالجة الحالات التي يجب فيها تنزيل وحدة اللغة تلقائيًا. لا توجد خدمات خارجية مطلوبة بخلاف حزمة Aspose.OCR NuGet.

## المتطلبات المسبقة

قبل أن تبدأ، تأكد من وجود ما يلي:

- .NET 6.0 SDK أو أحدث مثبت  
- Visual Studio 2022 (أو أي محرر يدعم C#)  
- اتصال بالإنترنت للتشغيل الأول (يتم جلب وحدة اللغة السيريليّة عند الطلب)  
- حزمة Aspose.OCR NuGet (`dotnet add package Aspose.OCR`)  

هذه العناصر تسمح لك بتجميع وتشغيل الشيفرة دون أي إعدادات إضافية.

## الخطوة 1: إنشاء مشروع وحدة تحكم جديد

افتح الطرفية ونفّذ الأوامر التالية لإنشاء تطبيق وحدة تحكم بسيط:

```bash
dotnet new console -n ImageOcrDemo
cd ImageOcrDemo
dotnet add package Aspose.OCR
```

أمر `dotnet new console` ينشئ ملف `Program.cs` وملف مشروع يراجع مكتبة Aspose.OCR. إضافة الحزمة تحل جميع التجميعات المطلوبة.

## الخطوة 2: استيراد مساحة الأسماء Aspose.OCR

حرّر **Program.cs** وأضف توجيه `using Aspose.OCR;` في أعلى الملف. هذا يجعل فئات OCR متاحة دون الحاجة إلى أسماء مؤهلة بالكامل.

```csharp
using System;
using Aspose.OCR;
```

عبارة `using` تحسّن قابلية القراءة وتبقي الشيفرة مركّزة على سير عمل OCR.

## الخطوة 3: تهيئة محرك OCR

أنشئ كائن `OcrEngine`. المحرك يحمل إعدادات مثل وحدة اللغة وإعدادات التعرف.

```csharp
// Initialise the OCR engine
var ocrEngine = new OcrEngine();
```

إنشاء المحرك مرة واحدة لكل تطبيق يكون فعالًا لأن المكتبات الأصلية تُحمَّل مرة واحدة فقط.

## الخطوة 4: اختيار وحدة اللغة

للنص السيريلي، اضبط الخاصية `Language` إلى `Language.Cyrillic`. Aspose.OCR يقوم بتنزيل الوحدة تلقائيًا إذا كانت مفقودة، لذا قد تستغرق التنفيذ الأول بضع ثوانٍ.

```csharp
// Choose Cyrillic language module – it will be downloaded if absent
ocrEngine.Language = Language.Cyrillic;
```

إذا احتجت لاحقًا إلى تحويل صورة إلى نص بلغة أخرى (مثل الإنجليزية أو العربية)، استبدل `Language.Cyrillic` بالقيمة المناسبة من الـ enum. هذه المرونة تتيح لك تحويل الصورة إلى نص لأي نص مدعوم.

## الخطوة 5: التعرف على النص من ملف JPG

استدعِ `RecognizeImage` مع المسار الكامل للصورة. تُعيد الطريقة كائن `OcrResult` يحتوي على السلسلة المستخرجة.

```csharp
// Path to the source image – replace with your own file
string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

// Perform OCR – this extracts text from the JPG file
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

يعمل الاستدعاء مع أي صيغة صورة نقطية يدعمها Aspose.OCR (JPG، PNG، BMP، TIFF). استخدام JPG يضمن إمكانية استخراج النص من ملفات jpg دون خطوات تحويل إضافية.

## الخطوة 6: إخراج النص المُعترف به

أخيرًا، اكتب النص المُعترف به إلى وحدة التحكم. هذا يُظهر طريقة بسيطة لقراءة صورة نص سيريلي وعرضها.

```csharp
// Show the recognised text in the console
Console.WriteLine("Recognised text:");
Console.WriteLine(result.Text);
```

عند تشغيل البرنامج، يجب أن ترى الأحرف السيريليّة مطبوعة تمامًا كما تظهر في الصورة الأصلية.

## مثال عملي كامل

فيما يلي ملف **Program.cs** الكامل الذي يمكنك نسخه، لصقه، وتشغيله فورًا.

```csharp
using System;
using Aspose.OCR;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Choose the language module required for recognition (Cyrillic in this case)
            // The language module will be downloaded automatically if not present
            ocrEngine.Language = Language.Cyrillic;

            // Step 3: Provide the path to the image you want to process
            // You can replace the file name with any JPG, PNG, BMP, or TIFF image
            string imagePath = @"YOUR_DIRECTORY/sample_image.jpg";

            // Step 4: Recognise text from the image file
            OcrResult result = ocrEngine.RecognizeImage(imagePath);

            // Step 5: Output the recognised text
            Console.WriteLine("Recognised text:");
            Console.WriteLine(result.Text);
        }
    }
}
```

### النتيجة المتوقعة

```
Recognised text:
Пример текста на кириллице
```

تختلف النتيجة الدقيقة حسب محتوى `sample_image.jpg`. إذا كانت الصورة تحتوي على نص إنجليزي، سيعيد نفس الكود السلسلة الإنجليزية طالما ضبطت `ocrEngine.Language = Language.English;`.

## معالجة المشكلات الشائعة

| المشكلة | لماذا يحدث | كيفية الحل |
|-------|----------------|----------------|
| لم يتم العثور على وحدة اللغة | يحاول التشغيل الأول تنزيل الوحدة لكن العملية تفشل بسبب قيود الجدار الناري. | تأكد من أن الجهاز يستطيع الوصول إلى `https://downloads.aspose.com/ocr` أو قم بتنزيل الوحدة يدويًا من بوابة Aspose وضعها في المجلد الافتراضي (`%APPDATA%\Aspose\OCR\`). |
| دقة منخفضة على الصور الضوضائية | تعتمد محركات OCR على تباين واضح بين النص والخلفية. | عالج الصورة مسبقًا (مثلاً، زيادة التباين، التحويل إلى تدرج الرمادي) قبل استدعاء `RecognizeImage`. توفر Aspose.OCR خيارات `ImagePreprocessing` يمكنك استكشافها. |
| صيغ غير JPG | يظن بعض المطورين أن الشيفرة تعمل فقط مع ملفات JPG. | الـ API يقبل PNG، BMP، وTIFF أيضًا. غيّر امتداد الملف في `imagePath` وفقًا لذلك. |
| الملفات الكبيرة تسبب وقت معالجة طويل | الصور الأكبر تحتاج إلى المزيد من الذاكرة ودورات المعالج. | قلّص حجم الصورة إلى دقة معقولة (مثلاً 1500 × 1500) قبل التعرف. |

هذه النصائح تساعدك على تحويل الصورة إلى نص بشكل موثوق عبر سيناريوهات مختلفة.

## توسيع الحل

بعد أن تتمكن من التعرف على النص من الصورة، قد ترغب في:

- **حفظ النتيجة إلى ملف** – اكتب `result.Text` إلى مستند `.txt` أو `.docx`.  
- **معالجة دفعة من الملفات في مجلد** – كرّر العملية على جميع الملفات في دليل وطبق نفس منطق OCR.  
- **دمج مع التعبيرات النمطية** – استخرج أرقام الهواتف، التواريخ، أو أنماط أخرى من السلسلة المُعترف بها.  

جميع هذه الامتدادات تعيد استخدام الشيفرة الأساسية نفسها، مما يبقي التنفيذ مختصرًا.

## الخلاصة

أصبح لديك الآن دليل كامل للتعرف على النص من الصورة باستخدام Aspose.OCR في C#. غطى الدليل كيفية إعداد المشروع، تهيئة محرك OCR، اختيار وحدة اللغة السيريليّة، واستخراج النص من ملف JPG. باتباع هذه الخطوات يمكنك أيضًا تحويل الصورة إلى نص للغات أخرى، استخراج النص من ملفات jpg، وتحويل الصورة إلى نص في أي تطبيق .NET.

لا تتردد في تجربة لغات إضافية، دفعات أكبر، أو منطق ما بعد المعالجة. إذا احتجت إلى قراءة صورة نص سيريلي في سياق مختلف—مثل واجهة برمجة تطبيقات ويب أو خدمة Windows—فالنمط نفسه ينطبق. برمجة سعيدة!

## ما الذي يجب أن تتعلمه لاحقًا؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شيفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [استخراج نص الصورة C# مع اختيار اللغة باستخدام Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [التعرف على نص الصورة باستخدام Aspose OCR لعدة لغات](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [خط أنابيب ما قبل معالجة OCR – كيفية التعرف على النص من الصورة في C#](/ocr/english/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}