---
category: general
date: 2026-04-17
description: استخراج النص من الصورة باستخدام Aspose OCR في C#. تعلم كيفية قراءة النص
  من PNG، تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف في دقائق.
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: ar
og_description: استخراج النص من الصورة باستخدام Aspose OCR في C#. يوضح هذا الدرس كيفية
  قراءة النص من PNG، تحويل الصورة إلى نص، وتحميل الصورة للتعرف الضوئي على الأحرف (OCR)
  بكفاءة.
og_title: استخراج النص من الصورة في C# – دليل Aspose OCR الكامل
tags:
- Aspose OCR
- C#
- Image Processing
title: استخراج النص من الصورة في C# – تحويل الصورة إلى نص باستخدام Aspose OCR
url: /ar/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# استخراج النص من الصورة في C# – دليل Aspose OCR الكامل

هل احتجت يومًا إلى **استخراج النص من الصورة** لكن لم تكن متأكدًا أي مكتبة تختار؟ لست وحدك. يواجه العديد من المطورين هذه المشكلة عندما يكون لديهم لقطة شاشة PNG، أو فاتورة ممسوحة ضوئيًا، أو علامة متعددة اللغات ويرغبون في تحويل البكسلات إلى نص قابل للبحث.  

في هذا الدرس سنستعرض حلًا عمليًا يتيح لك **قراءة النص من PNG**، **تحويل الصورة إلى نص**، و**تحميل الصورة للتعرف الضوئي على الأحرف (OCR)** باستخدام Aspose OCR — كل ذلك بلغة C# الحديثة والنظيفة. في النهاية ستحصل على برنامج جاهز للتنفيذ يمكنك إدراجه في أي مشروع .NET.

## ما ستتعلمه

- كيفية تحميل ملف صورة للتعرف الضوئي على الأحرف (خطوة “تحميل الصورة للتعرف الضوئي على الأحرف”)
- كيفية تكوين Aspose OCR لمجموعة لغات معينة
- كيفية استخراج السلسلة المعترف بها وعرضها في وحدة التحكم
- نصائح للتعامل مع لغات متعددة، ملفات كبيرة، وإدارة الذاكرة

لا حاجة إلى وثائق خارجية؛ كل ما تحتاجه موجود في مقتطفات الشيفرة أدناه.

## المتطلبات المسبقة

- .NET 6+ SDK (أو .NET Core 3.1+ – الواجهة البرمجية نفسها)
- Visual Studio 2022، VS Code، أو أي بيئة تطوير تفضلها
- حزمة NuGet **Aspose.OCR** (تثبيت باستخدام `dotnet add package Aspose.OCR`)  

إذا كان لديك هذه المتطلبات، لنبدأ.

![استخراج النص من الصورة باستخدام Aspose OCR في C#](https://example.com/aspsoe-ocr-demo.png "استخراج النص من الصورة باستخدام Aspose OCR")

## الخطوة 1 – تحميل الصورة للتعرف الضوئي على الأحرف

أول شيء عليك فعله هو إعطاء محرك OCR شيئًا ليقرأه. يعمل Aspose OCR مع مجموعة متنوعة من الصيغ، لكن PNG هو اختيار شائع للقطات الشاشة والرسومات الممسوحة ضوئيًا.

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **لماذا هذا مهم:** تحميل الصورة بشكل صحيح يضمن أن المحرك يرى بيانات البكسل الدقيقة التي تتوقعها. إذا مررت تدفقًا فاسدًا، سيفشل التعرف بصمت.

## الخطوة 2 – إنشاء وتكوين محرك OCR

بعد ذلك، أنشئ كائن `OcrEngine`. يمكنك اختياريًا تعيين مجموعة اللغة؛ بالنسبة للعديد من النصوص الغربية الإعداد الافتراضي يعمل، لكن إذا كنت تتعامل مع السيريالية أو العربية أو الأحرف الآسيوية فستحتاج إلى إخبار المحرك مسبقًا.

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **نصيحة احترافية:** ضبط اللغة يحد من مجموعة الأحرف التي يبحث عنها المحرك، مما يسرّع عملية التعرف ويحسن الدقة.

## الخطوة 3 – تنفيذ OCR واستخراج النص

الآن يحدث الجزء الثقيل. استدعِ `Recognize` مع الصورة التي حمّلتها مسبقًا، ثم اقرأ الخاصية `Text` من النتيجة.

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### النتيجة المتوقعة

إذا كان ملف `sample.png` يحتوي على العبارة “Hello, World!” فستظهر لك:

```
=== OCR Output ===
Hello, World!
```

إذا كانت الصورة أكثر تعقيدًا (مثلاً إيصالًا متعدد الأسطر)، يحافظ المحرك على فواصل الأسطر، مما يمنحك كتلة نص جاهزة للمعالجة.

## الخطوة 4 – تجميع كل ذلك في برنامج كامل

فيما يلي التطبيق الكامل المستقل لوحدة التحكم الذي يمكنك نسخه ولصقه في مشروع C# جديد. يتضمن معالجة الأخطاء وتعليقات تشرح كل جزء.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

شغّل البرنامج (`dotnet run` من مجلد المشروع) وراقب وحدة التحكم تطبع السلسلة المستخرجة. هذه هي عملية **استخراج النص من الصورة** بالكامل في أقل من 30 سطرًا من الشيفرة.

## الخطوة 5 – الاختلافات الشائعة والحالات الخاصة

### قراءة النص من PNG مقابل الصيغ الأخرى

بينما يستخدم المثال PNG، يدعم Aspose OCR أيضًا JPEG و BMP و TIFF و GIF. فقط غيّر امتداد الملف؛ استدعاء `OcrImage.FromFile` نفسه يعمل دون تعديل.

### تحويل الصورة إلى نص في واجهة برمجة تطبيقات ويب

إذا كنت بحاجة إلى إتاحة هذه الوظيفة عبر نقطة نهاية HTTP، يمكنك قبول تحميل `IFormFile`، تحويل التدفق إلى `OcrImage` باستخدام `OcrImage.FromStream`، وإرجاع السلسلة كـ JSON. يبقى منطق OCR الأساسي هو نفسه.

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### معالجة الصور الكبيرة

الصور الكبيرة وعالية الدقة يمكن أن تستهلك الكثير من الذاكرة. نهج عملي هو تقليل حجم الصورة قبل تمريرها إلى المحرك:

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### مستندات متعددة اللغات

إذا كان المستند يخلط بين الإنجليزية والسيريالية، اجمع علامات اللغة:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

سيحاول المحرك التعرف على الأحرف من كلا المجموعتين.

### تحرير الموارد

يضمن بيان `using` حول `OcrEngine` تحرير الموارد الأصلية. نسيان ذلك قد يؤدي إلى تسرب الذاكرة، خاصة في الخدمات التي تعمل لفترات طويلة.

## نصائح احترافية للحصول على OCR موثوق

- **الصور الواضحة تفوز:** عالج الصور مسبقًا (إزالة الانحراف، تقليل الضوضاء) باستخدام مكتبات مثل **ImageSharp** قبل OCR.  
- **حجم الخط مهم:** النص الأصغر من 10 px غالبًا ما يُفوت؛ فكر في تكبير الصورة.  
- **تحقق من `ocrResult.Confidence`:** كائن `OcrResult` يعرض أيضًا درجة الثقة لكل كلمة — استخدمها لتعليم الأقسام ذات الثقة المنخفضة للمراجعة اليدوية.  
- **معالجة دفعات:** لعدة ملفات، أعد استخدام نسخة واحدة من `OcrEngine` لتجنب عبء تهيئة متكرر.

## الخلاصة

لقد تعلمت الآن كيفية **استخراج النص من الصورة** في C# باستخدام Aspose OCR، مع تغطية كل شيء من **تحميل الصورة للتعرف الضوئي على الأحرف** إلى **تحويل الصورة إلى نص** و**قراءة النص من PNG**. المثال الكامل القابل للتنفيذ يعرض الشيفرة الدقيقة التي تحتاجها، يشرح سبب وجود كل خطوة، ويقدم تنويعات عملية لسيناريوهات العالم الحقيقي.

هل أنت مستعد للتحدي التالي؟ جرّب إدخال السلسلة المستخرجة في فهرس بحث، ترجمتها باستخدام Azure Cognitive Services، أو إنشاء PDF قابل للبحث بنفس طبقة النص. الاحتمالات لا حصر لها، والآن لديك أساس قوي لأي مشروع **c# image to text**.

لا تتردد في التجربة، تعديل إعدادات اللغة، أو دمج هذا المقتطف في تطبيق أكبر. إذا واجهت أي مشاكل، اترك تعليقًا أدناه — برمجة سعيدة!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}