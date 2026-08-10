---
category: general
date: 2026-03-23
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية تحميل الصورة
  للتعرف الضوئي على الأحرف وإنشاء محرك OCR بشكل غير متزامن.
draft: false
keywords:
- extract text from image
- load image for OCR
- create OCR engine
- asynchronous OCR C#
- Aspose OCR guide
- C# image processing
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدليل
  كيفية تحميل الصورة للتعرف الضوئي على الأحرف وإنشاء محرك OCR للتعرف غير المتزامن.
og_title: استخراج النص من الصورة – دليل OCR غير المتزامن للغة C#
tags:
- OCR
- C#
- Aspose
title: استخراج النص من الصورة في C# – دليل OCR غير المتزامن
url: /ar/net/text-recognition/extract-text-from-image-in-c-async-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة – دليل C# الكامل للـ OCR غير المتزامن

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن لم تكن متأكدًا أي واجهة برمجة تطبيقات (API) تختار؟ لست وحدك. في العديد من المشاريع الواقعية—مثل ماسحات الفواتير، تطبيقات الإيصالات، أو أدوات النظرة السريعة—تُعد القدرة على استخراج النص من صورة مطلبًا يوميًا.  

في هذا الدرس سنوضح لك بالضبط كيفية **استخراج النص من الصورة** باستخدام Aspose.OCR، بدءًا من **تحميل الصورة للـ OCR** إلى **إنشاء محرك OCR** وتشغيل العملية بشكل غير متزامن. في النهاية ستحصل على برنامج جاهز للتنفيذ يطبع النص المُتعرف عليه في وحدة التحكم، وستفهم لماذا كل جزء مهم.

## ما ستتعلمه

- كيفية **إنشاء محرك OCR** بأمان مع التخلص المناسب من الموارد.  
- الطريقة الصحيحة **لتحميل الصورة للـ OCR** باستخدام `ImageStream` الخاصة بـ Aspose.  
- كيفية استدعاء `RecognizeAsync()` ومعالجة النجاح أو الفشل.  
- نصائح لاستكشاف المشكلات الشائعة (خطوط مفقودة، صيغ غير مدعومة، إلخ).  
- الناتج المتوقع في وحدة التحكم لتتمكن من التحقق من عمل كل شيء.

### المتطلبات المسبقة

- .NET 6.0 SDK أو أحدث (الكود يُترجم مع .NET Core و .NET Framework على حد سواء).  
- Visual Studio 2022 أو أي محرر يدعم C#.  
- حزمة NuGet الخاصة بـ Aspose.OCR (`Aspose.OCR`) مضافة إلى مشروعك.  
- صورة عينة PNG/JPG (`input.png`) موجودة في مجلد يمكنك الإشارة إليه.

لا توجد مكتبات إضافية مطلوبة—Aspose يتولى الجزء الأكبر من المعالجة.

![مثال لاستخراج النص من الصورة](https://example.com/ocr-result.png "لقطة شاشة تُظهر النص المستخرج – استخراج النص من الصورة")

## الخطوة 1 – تثبيت Aspose.OCR وإعداد المشروع

قبل أن نتمكن من **إنشاء محرك OCR**، يجب أن تكون المكتبة نفسها متاحة.

```bash
dotnet new console -n AsyncOcrDemo
cd AsyncOcrDemo
dotnet add package Aspose.OCR
```

> **نصيحة احترافية:** حافظ على تحديث حزم NuGet الخاصة بك. أحدث إصدار من Aspose.OCR (حتى مارس 2026) يتضمن تحسينات أداء للاتصالات غير المتزامنة.

## الخطوة 2 – إنشاء محرك OCR (مع ضمان التخلص السليم)

كتلة الكود الأولى تُظهر كيفية **إنشاء محرك OCR** داخل عبارة `using`. هذا يضمن تحرير الموارد غير المُدارة، وهو أمر حاسم للخدمات طويلة التشغيل.

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // Step 2.1: Instantiate the OCR engine – this is where we **create OCR engine**
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // The rest of the steps go here…
        }
    }
}
```

**لماذا نستخدم `using`؟**  
`OcrEngine` يلتف حول كود أصلي؛ إذا نسيت التخلص منه، قد تتسرب الذاكرة أو مقبض الملفات، مما يؤدي إلى تعطل متقطع عند معالجة عدد كبير من الصور.

## الخطوة 3 – تحميل الصورة للـ OCR

الآن سنقوم **بتحميل الصورة للـ OCR**. توفر Aspose الدالة `ImageStream.FromFile`، التي تُجردك من التعامل مع الـ bitmap وتعمل مع معظم الصيغ الشائعة.

```csharp
// Step 3.1: Define the path to the picture you want to process
string imagePath = "YOUR_DIRECTORY/input.png";

// Step 3.2: Feed the image into the engine
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **احذر:** إذا كان المسار غير صحيح أو الملف تالفًا، سيُعيد `RecognizeAsync()` القيمة `false`. تأكد دائمًا من وجود الملف قبل استدعاء طريقة OCR.

## الخطوة 4 – تشغيل التعرف على OCR بشكل غير متزامن

استدعاء `RecognizeAsync()` يحمّل تحليل الصورة الثقيل إلى خيط خلفي، مما يحافظ على استجابة واجهة المستخدم أو عدم حجب نقطة النهاية في الويب.

```csharp
// Step 4.1: Perform the async recognition
bool recognitionSucceeded = await ocrEngine.RecognizeAsync();
```

**ماذا يحدث خلف الكواليس؟**  
تقسّم Aspose الصورة إلى مناطق، وتشغّل شبكة عصبية على كل منطقة، ثم تُدمج النتائج. النسخة غير المتزامنة ببساطة تُغلف هذا الخط الأنابيب في `Task`، مما يسمح لمجمع خيوط .NET بإدارة التنفيذ.

## الخطوة 5 – استرجاع وعرض النص المستخرج

إذا نجح الاستدعاء غير المتزامن، فإن الخاصية `Text` الآن تحتوي على السلسلة التي أردت **استخراج النص من الصورة**. لنطبعها.

```csharp
// Step 5.1: Show the outcome
if (recognitionSucceeded)
    Console.WriteLine("Async OCR result:\n" + ocrEngine.Text);
else
    Console.WriteLine("Async recognition failed.");
```

### النتيجة المتوقعة

```
Async OCR result:
Hello, world!
This is a sample image containing text.
```

إذا رأيت ما فوق (أو محتويات صورتك الخاصة)، فقد نجحت في **استخراج النص من الصورة** باستخدام Aspose OCR.

## مثال كامل قابل للتنفيذ

بتجميع كل الأجزاء معًا، إليك البرنامج الكامل الذي يمكنك نسخه‑ولصقه في `Program.cs` وتشغيله.

```csharp
using Aspose.OCR;
using System;
using System.Threading.Tasks;

class AsyncDemo
{
    static async Task Main()
    {
        // Step 1: Create OCR engine (ensures proper disposal)
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Step 2: Load the image you want to process – this is how we **load image for OCR**
            string imagePath = "YOUR_DIRECTORY/input.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Step 3: Run the asynchronous recognition – this is the core of **extract text from image**
            bool recognitionSucceeded = await ocrEngine.RecognizeAsync();

            // Step 4: Display the result or an error message
            if (recognitionSucceeded)
                Console.WriteLine("Async OCR result:\n" + ocrEngine.Text);
            else
                Console.WriteLine("Async recognition failed.");
        }
    }
}
```

شغّله باستخدام:

```bash
dotnet run
```

إذا تم إعداد كل شيء بشكل صحيح، ستطبع وحدة التحكم النص المستخرج.

## أسئلة شائعة وحالات خاصة

### ماذا لو احتجت لمعالجة JPEG بدلاً من PNG؟

`ImageStream.FromFile` يكتشف الصيغة تلقائيًا، لذا يمكنك توجيه `imagePath` إلى `photo.jpg` دون أي تغييرات في الكود. فقط تأكد من أن حجم الملف ليس كبيرًا جدًا—توصي Aspose بصور لا تتجاوز 5 ميغابايت للحصول على أفضل سرعة.

### هل يمكنني تغيير اللغة أو مجموعة الأحرف؟

نعم. بعد إنشاء المحرك، عيّن `ocrEngine.Language = OcrLanguage.English;` أو أي لغة أخرى مدعومة. هذا يحسّن الدقة للخطوط غير اللاتينية.

### كيف أتعامل مع صفحات متعددة (مثل TIFF متعدد الصفحات)؟

يمكن لـ Aspose.OCR معالجة كل صفحة على حدة. قم بالتكرار عبر الصفحات، وعيّن كل واحدة إلى `ocrEngine.Image`، واستدعِ `RecognizeAsync()` لكل تكرار. اجمع النتائج في `StringBuilder` إذا كنت تحتاج إلى سلسلة ناتج واحدة.

### ماذا لو لم تُرجع الاستدعاءة غير المتزامنة أبدًا؟

عادةً ما يشير ذلك إلى حالة نفاد الذاكرة أو صورة تالفة. غلف الاستدعاء داخل `try/catch` وحدد مهلة باستخدام `Task.WhenAny`:

```csharp
var recognitionTask = ocrEngine.RecognizeAsync();
if (await Task.WhenAny(recognitionTask, Task.Delay(5000)) == recognitionTask)
{
    // success path
}
else
{
    Console.WriteLine("Recognition timed out.");
}
```

## نصائح للأداء

- **أعد استخدام محرك OCR** عند معالجة العديد من الصور في دفعة؛ إنشاء محرك جديد لكل ملف يضيف عبئًا.  
- **غيّر حجم الصور الكبيرة** إلى عرض أقصى 2000 بكسل قبل تمريرها إلى المحرك؛ هذا يسرّع التحليل دون الإضرار بالدقة.  
- **فعّل التسريع عبر العتاد** (إذا سمحت رخصتك) عن طريق تعيين `ocrEngine.UseGpu = true;`.

## الخلاصة

الآن لديك مثال متكامل من البداية إلى النهاية يوضح كيفية **استخراج النص من الصورة** باستخدام Aspose OCR في C#. من خلال تعلمك **تحميل الصورة للـ OCR**، **إنشاء محرك OCR**، وتشغيل `RecognizeAsync()`، يمكنك دمج استخراج النص الموثوق به في تطبيقات سطح المكتب، خدمات الويب، أو العمال الخلفيين.  

هل أنت مستعد للخطوة التالية؟ جرّب استبدال الصورة بملف PDF، أو تجربة لغات مختلفة، أو توجيه مخرجات OCR إلى فهرس بحث. الاحتمالات لا حصر لها، ومع نمط الـ async لن تحجز الخيط الرئيسي بينما يتم تنفيذ المعالجة الثقيلة في الخلفية.

برمجة سعيدة، ولتكن صورك دائمًا واضحة بما يكفي للحصول على OCR دقيق!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}