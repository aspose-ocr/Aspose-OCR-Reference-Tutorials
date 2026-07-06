---
category: general
date: 2026-02-19
description: كيفية التعرف الضوئي على النص العربي من الصور باستخدام Aspose OCR في C#.
  تعلم استخراج النص العربي، تحويل الصورة إلى نص، وقراءة الصورة العربية بسرعة.
draft: false
keywords:
- how to ocr arabic
- extract arabic text
- convert image to text
- c# image to text
- read arabic image
language: ar
og_description: كيفية التعرف الضوئي على النص العربي من الصور باستخدام Aspose OCR.
  يوضح هذا الدليل كيفية استخراج النص العربي، تحويل الصورة إلى نص، وقراءة الصورة العربية
  في C#.
og_title: كيفية التعرف الضوئي على الحروف العربية في C# – دليل خطوة بخطوة
tags:
- OCR
- C#
- Aspose
- Arabic
title: كيفية إجراء OCR للغة العربية في C# – دليل برمجة شامل
url: /ar/net/text-recognition/how-to-ocr-arabic-in-c-complete-programming-guide/
---

italics markers.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية التعرف الضوئي على الأحرف العربية في C# – دليل برمجة كامل

هل تساءلت يومًا **كيفية التعرف الضوئي على الأحرف العربية** من مستند ممسوح ضوئيًا دون قضاء ساعات في تعديل الإعدادات؟ لست وحدك—المطورون يواجهون دائمًا صعوبات عندما تتشوه الأحرف العربية أو تختفي تمامًا. الخبر السار؟ مع Aspose OCR يمكنك تحويل صورة عربية إلى نص نظيف وقابل للبحث في بضع أسطر فقط.

في هذا الدرس سنستعرض استخراج النص العربي، تحويل الصورة إلى نص، وقراءة ملفات الصور العربية مباشرةً من تطبيق C# Console. في النهاية ستحصل على برنامج جاهز للتنفيذ يطبع السلسلة العربية المعترف بها على وحدة التحكم، بالإضافة إلى بعض النصائح للتعامل مع الحالات الصعبة.

## ما ستحتاجه

- **.NET 6.0 أو أحدث** – الإصدار الحالي طويل الدعم (يعمل أيضًا مع .NET Framework 4.8).  
- **Visual Studio 2022** (أو أي بيئة تطوير تفضلها).  
- حزمة NuGet **Aspose.OCR** – المكتبة التي تقوم بالعمل الفعلي.  
- ملف صورة عربية (مثال: `arabic_doc.jpg`).  

هذا كل شيء. لا محركات OCR إضافية، لا ملفات DLL أصلية، مجرد إشارة NuGet واحدة.

![مثال على كيفية التعرف الضوئي على الأحرف العربية](/images/ocr-arabic.png "لقطة شاشة لكيفية التعرف الضوئي على الأحرف العربية")

## الخطوة 1 – تثبيت حزمة Aspose.OCR NuGet

للبدء، افتح **Package Manager Console** الخاص بالمشروع وشغّل:

```powershell
Install-Package Aspose.OCR
```

أو، إذا كنت تفضّل الواجهة الرسومية، انقر بزر الماوس الأيمن على *Dependencies → Manage NuGet Packages* وابحث عن **Aspose.OCR**. هذه الخطوة تمنحك الوصول إلى الفئة `OcrEngine`، التي تدعم أكثر من 60 لغة—بما فيها العربية.

> **نصيحة احترافية:** حافظ على تحديث نسخة الحزمة. حتى فبراير 2026 الإصدار المستقر الأخير هو **23.11**؛ الإصدارات الأحدث غالبًا ما تجلب تحسينات خاصة باللغات.

## الخطوة 2 – الإشارة إلى صورة العربية الخاصة بك

محرك OCR يحتاج إلى مسار ملف. احفظ الصورة في مكان يمكن للمشروع الوصول إليه (مثال: `Resources/arabic_doc.jpg`) واستخدم مسارًا **نسبيًا** أو **مطلقًا**:

```csharp
// Step 2: Define the path to the Arabic image you want to process
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "Resources", "arabic_doc.jpg");

// Quick sanity check – does the file exist?
if (!File.Exists(imagePath))
{
    Console.WriteLine($"File not found: {imagePath}");
    return;
}
```

إضافة فحص بسيط يمنع استثناء *FileNotFoundException* المزعج ويجعل الكود أكثر صلابة عندما تقوم لاحقًا بأتمتة معالجة دفعات متعددة.

## الخطوة 3 – إنشاء مثيل لمحرك OCR للغة العربية

تأتي Aspose.OCR مع تعداد `Language`. تعيينه إلى `Language.Arabic` يخبر المحرك باستخدام مجموعة الأحرف الصحيحة، وتخطيط من اليمين إلى اليسار، وقواعد تشكيل السياق.

```csharp
// Step 3: Create an OCR engine instance and set it to recognize Arabic text
var ocrEngine = new OcrEngine
{
    Language = Language.Arabic,
    // Optional: increase accuracy for low‑resolution images
    // Settings = new OcrSettings { ImageResolution = 300 }
};
```

> **لماذا هذا مهم:** الخط العربي متصل؛ الأحرف تتغير شكلها حسب موقعها. استخدام نموذج اللغة المخصص يتجنب النتيجة الشائعة “?????” التي تظهر عندما يستخدم المحرك اللغة اللاتينية افتراضيًا.

## الخطوة 4 – تنفيذ عملية التعرف

الآن يقوم المحرك بقراءة البكسلات وإرجاع `OcrResult`. يمكن للطريقة `RecognizeImage` قبول مسار ملف، أو `Stream`، أو `Bitmap`. هنا نستخدم المسار الذي عرّفناه مسبقًا.

```csharp
// Step 4: Perform OCR on the specified image
OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);
```

إذا كنت بحاجة لمعالجة صور متعددة، ما عليك سوى التكرار عبر قائمة من المسارات وإعادة استخدام نفس مثيل `ocrEngine`—هذا يوفر الذاكرة ويحسن الإنتاجية.

## الخطوة 5 – إخراج النص العربي المعترف به

أخيرًا، اطبع النتيجة على وحدة التحكم. يمكنك أيضًا كتابة النص إلى ملف، قاعدة بيانات، أو إرساله إلى واجهة برمجة تطبيقات ترجمة.

```csharp
// Step 5: Output the recognized Arabic text to the console
Console.WriteLine("Arabic OCR result:");
Console.WriteLine(ocrResult.Text);

// Optional: Save to a .txt file for later analysis
File.WriteAllText("ArabicOcrOutput.txt", ocrResult.Text, Encoding.UTF8);
```

### النتيجة المتوقعة

بافتراض أن `arabic_doc.jpg` يحتوي على العبارة **"مرحبا بالعالم"** (Hello World)، يجب أن ترى شيئًا مشابهًا لـ:

```
Arabic OCR result:
مرحبا بالعالم
```

إذا كان الإخراج مشوشًا، تحقق من جودة الصورة (ينصح بحد أدنى 150 dpi) وتأكد من ضبط خاصية `Language` بشكل صحيح.

## التعامل مع الحالات الشائعة

| الحالة                                 | ما الذي يجب فعله                                                            |
|----------------------------------------|-----------------------------------------------------------------------------|
| **صورة منخفضة الدقة**                  | زد `ImageResolution` في `OcrSettings` أو عالج الصورة بفلتر تعزيز الحدة.   |
| **صفحات متعددة في ملف واحد**           | استخدم `RecognizeImage` لكل صفحة على حدة، ثم اجمع `ocrResult.Text`.       |
| **مزيج من العربية والإنجليزية**        | عيّن `Language = Language.Multilingual` لتمكين المحرك من الكشف التلقائي. |
| **مشكلات عرض من اليمين إلى اليسار**   | عند الكتابة إلى عنصر واجهة مستخدم، اضبط `FlowDirection = RightToLeft`.   |
| **ملفات كبيرة (> 10 ميغابايت)**       | استخدم `FileStream` لبث الصورة وتجنب تحميل الملف بالكامل في الذاكرة.      |

هذه التعديلات تحافظ على استقرار خط **c# image to text** حتى عندما لا تكون المدخلات مثالية.

## مثال كامل قابل للتنفيذ

فيما يلي البرنامج الكامل الذي يمكنك نسخه ولصقه في مشروع Console جديد. يتضمن جميع الخطوات، معالجة الأخطاء، والتحسينات الاختيارية التي نوقشت أعلاه.

```csharp
// ------------------------------------------------------------
// Complete example: how to ocr arabic using Aspose.OCR in C#
// ------------------------------------------------------------
using Aspose.OCR;
using System;
using System.IO;
using System.Text;

class ArabicDemo
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // Step 1: Locate the Arabic image (adjust the relative path as needed)
        // -----------------------------------------------------------------
        string imagePath = Path.Combine(
            AppDomain.CurrentDomain.BaseDirectory,
            "Resources",
            "arabic_doc.jpg");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at: {imagePath}");
            return;
        }

        // -----------------------------------------------------------------
        // Step 2: Create and configure the OCR engine for Arabic language
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.Arabic,
            // Uncomment the line below if you have low‑resolution images
            // Settings = new OcrSettings { ImageResolution = 300 }
        };

        // -----------------------------------------------------------------
        // Step 3: Run the recognition
        // -----------------------------------------------------------------
        OcrResult result = ocrEngine.RecognizeImage(imagePath);

        // -----------------------------------------------------------------
        // Step 4: Display and optionally save the extracted Arabic text
        // -----------------------------------------------------------------
        Console.WriteLine("✅ Arabic OCR result:");
        Console.WriteLine(result.Text);

        string outputPath = "ArabicOcrOutput.txt";
        File.WriteAllText(outputPath, result.Text, Encoding.UTF8);
        Console.WriteLine($"🗒️ Text saved to {outputPath}");
    }
}
```

شغّل البرنامج (`dotnet run` من سطر الأوامر أو اضغط **F5** في Visual Studio) وسترى وحدة التحكم تُظهر الأحرف العربية. هذا كل شيء—**لقد حولت صورة إلى نص** وتعلمت كيفية **استخراج النص العربي** ببضع أسطر من C#.

## الخلاصة

غطّينا **كيفية التعرف الضوئي على الأحرف العربية** خطوة بخطوة، من تثبيت Aspose.OCR إلى التعامل مع المشكلات الشائعة عند **تحويل الصورة إلى نص**. المقتطف الكامل أعلاه يُظهر طريقة نظيفة وجاهزة للإنتاج **لقراءة ملفات الصور العربية** وتحويلها إلى سلاسل قابلة للبحث، مما يلبي حالة الاستخدام الكلاسيكية “c# image to text”.

هل أنت مستعد للتحدي التالي؟ جرّب:

- حفظ نتيجة OCR كطبقة PDF قابلة للبحث.  
- استخدام وضع `Language.Multilingual` لمعالجة المستندات التي تمزج بين العربية واللاتينية.  
- دمج سير العمل في واجهة API ASP.NET Core بحيث يمكن للعملاء رفع الصور واستلام النص المشفر بصيغة JSON.

جرّب هذه الأفكار، وستصبح سريعًا الشخص المرجعي لتقنية OCR العربية في فريقك. برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}