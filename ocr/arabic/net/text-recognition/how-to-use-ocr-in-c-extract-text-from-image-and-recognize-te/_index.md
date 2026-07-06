---
category: general
date: 2026-02-13
description: كيفية استخدام OCR في C# لاستخراج النص من الصورة، والتعرف على النص من
  صورة أو JPG، وتشغيل OCR على الصورة دون الإنترنت.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: ar
og_description: كيفية استخدام OCR في C# لاستخراج النص من الصورة، والتعرف على النص
  من الصورة الفوتوغرافية، وتشغيل OCR على الصورة مع مثال كامل وقابل للتنفيذ.
og_title: كيفية استخدام OCR في C# – استخراج النص من الصورة
tags:
- OCR
- C#
- Image Processing
title: كيفية استخدام OCR في C# – استخراج النص من الصورة والتعرف على النص من الصورة
  الفوتوغرافية
url: /ar/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# كيفية استخدام OCR في C# – استخراج النص من الصورة والتعرف على النص من الصورة

هل تساءلت يومًا **كيف تستخدم OCR** لاستخراج الكلمات من لقطة شاشة، أو إيصال ممسوح ضوئيًا، أو صورة عشوائية التقطتها بهاتفك؟ لست وحدك. في العديد من التطبيقات الواقعية نحتاج إلى تحويل الصور إلى نص قابل للبحث، والقيام بذلك محليًا—دون الحاجة إلى اتصال إنترنت غير مستقر—قد يبدو كلغز.

لهذا السبب يوضح لك هذا الدليل طريقة خطوة بخطوة **استخراج النص من الصورة** باستخدام محرك OCR بلغة C#، كما يغطي أيضًا كيفية **التعرف على النص من الصورة**، **التعرف على النص من JPG**، و**تشغيل OCR على الصورة** للملفات الموجودة مباشرة على قرصك. في النهاية ستحصل على برنامج كامل جاهز للنسخ واللصق يعمل مباشرةً.

## ما ستتعلمه

- كيفية تكوين محرك OCR للغة الصينية المبسطة (أو أي لغة أخرى تقوم بإضافتها).  
- الكود الدقيق اللازم **تحميل الموارد** من مجلد محلي—دون الحاجة إلى استدعاءات شبكة.  
- كيفية **التعرف على النص من الصورة** للملفات مثل JPEG أو PNG أو BMP.  
- نصائح للتعامل مع الحالات الشائعة مثل فقدان ملفات النموذج أو صيغ الصور غير المدعومة.  
- مثال كامل قابل للتنفيذ يمكنك إدراجه في Visual Studio ورؤية النتائج فورًا.

### المتطلبات المسبقة

- .NET 6.0 أو أحدث (واجهة البرمجة المستخدمة هنا تستهدف .NET Standard 2.0، لذا تعمل الإصدارات القديمة أيضًا).  
- إلمام أساسي بـ C# و Visual Studio (أو أي بيئة تطوير تحبها).  
- مكتبة OCR التي تستخدمها (المقتطف يفترض وجود فئة `OcrEngine` خيالية تأتي مع نماذج اللغة).  
- مجلد يحتوي على ملفات نماذج اللغة المطلوبة—اعتبره “العقل” الذي يستخدمه المحرك لقراءة الأحرف الصينية.

> **نصيحة احترافية:** إذا لم تكن لديك ملفات نموذج اللغة الصينية بعد، قم بتحميلها مرة واحدة من موقع البائع وضعها في مجلد مثل `C:\OcrResources`. لن يحتاج المحرك إلى الاتصال بالإنترنت مرة أخرى.

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## كيفية استخدام OCR: إعداد المحرك

أول شيء تحتاجه هو نسخة من محرك OCR، مُكوَّنة للغة التي تهتم بها. في هذا الدرس نستهدف **الصينية المبسطة**، لكن استبدال `OcrLanguage.ChineseSimplified` بـ `OcrLanguage.English` (أو أي قيمة تعداد أخرى) هو مجرد تغيير سطر واحد.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**لماذا هذا مهم:**  
تحديد الخاصية `Language` يخبر المحرك بمجموعة الأحرف التي يجب توقعها. `ResourceFolder` هو المكان الذي يبحث فيه المحرك عن أوزان الشبكة العصبية وقواميس اللغة—اعتبره مخزن ذاكرة “العقل”. إذا أشرت إلى المجلد الخطأ، سيُطلق المحرك استثناء `FileNotFoundException` وستعلق العملية.

## استخراج النص من الصورة – تحميل الموارد

قبل أن يتمكن المحرك من قراءة أي شيء، عليك تحميل ملفات النموذج تلك إلى الذاكرة. هذه الخطوة **حرجة** لأنها تتجنب استدعاء الشبكة في كل مرة تقوم فيها بمعالجة صورة.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**ما الذي قد يحدث خطأ؟**  
إذا كان مسار المجلد غير صحيح أو الملفات تالفة، سيُطلق `LoadResources()` استثناء. يُظهر كتلة `try/catch` أعلاه معالجة الأخطاء بشكل مرن—شيء ستحتاجه غالبًا في بيئة الإنتاج.

## التعرف على النص من الصورة – تشغيل OCR

الآن الجزء الممتع: إمداد المحرك بملف صورة والحصول على النص المُتعرف عليه. هذا هو جوهر سيناريوهات **تشغيل OCR على الصورة**، سواء كانت الصورة JPEG أو PNG أو حتى BMP.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

طريقة `RecognizeImage` تُعيد كائنًا من نوع `RecognitionResult` (أو أيًا كان ما تسميه مجموعة أدوات التطوير الخاصة بك) الذي عادةً يحتوي على:

- `Text` – النص العادي المستخرج.  
- `Confidence` – درجة رقمية تشير إلى مدى ثقة المحرك بكل سطر.  
- `BoundingBoxes` – إحداثيات اختيارية لموقع كل كلمة في الصورة.

**لماذا قد يهمك مستوى الثقة:**  
إذا كنت تبني أداة أتمتة إدخال بيانات، يمكنك تعيين عتبة (مثلاً 0.85) وطلب تأكيد المستخدم للسطور ذات الثقة المنخفضة. هذا يحسن الدقة العامة بشكل كبير.

## التعرف على النص من JPG – معالجة الصيغ المختلفة

يفترض الكثير من المطورين أن OCR يعمل فقط مع PNGs، لكن المحركات الحديثة تتعامل مع ملفات **JPG** بشكل جيد. العائق الوحيد هو أن ضغط JPEG قد يضيف تشوهات تُربك النموذج.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

إذا لم يكن لديك مساعد `DenoiseAndDeskew`، توفر العديد من المكتبات (مثل OpenCvSharp) هذه الدوال. الخلاصة الأساسية هي: **تشغيل OCR على الصورة** بعد قليل من التنظيف إذا كانت الصورة قادمة من ماسح ضوئي أو كاميرا هاتف.

## تشغيل OCR على الصورة – نصائح، حالات حافة، وأفضل الممارسات

### 1. إدارة الذاكرة
تحميل نماذج اللغة الكبيرة قد يستهلك مئات الميغابايت. قم بتحرير المحرك عندما تنتهي:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. المعالجة الدُفعية
إذا كنت بحاجة لمعالجة عشرات الصور، حمّل الموارد مرة واحدة، ثم استخدم حلقة:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. سيناريوهات متعددة اللغات
يمكنك تبديل اللغات أثناء التشغيل عن طريق إعادة تعيين `ocrEngine.Language` واستدعاء `LoadResources()` مرة أخرى. فقط احذر من زمن التحميل الإضافي.

### 4. التعامل مع النتائج الفارغة
أحيانًا يُعيد المحرك سلسلة فارغة. هذا عادةً يعني أن الصورة غير واضحة أو أن لون النص يندمج مع الخلفية. فحص سريع:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. اعتبارات الأمان
لا تقم أبداً بتمرير الملفات التي يرفعها المستخدم مباشرةً إلى محرك OCR دون التحقق. على الأقل، تحقق من امتداد الملف وحجمه، وفكر في فحصه للبرمجيات الخبيثة.

---

## مثال عملي كامل

فيما يلي برنامج واحد مستقل يمكنك نسخه إلى مشروع تطبيق Console جديد. يوضح **كيفية استخدام OCR**، **استخراج النص من الصورة**، **التعرف على النص من الصورة**، **التعرف على النص من JPG**، و**تشغيل OCR على الصورة**—كل ذلك في خطوة واحدة.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**الناتج المتوقع (مثال):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

النص الفعلي سيختلف بناءً على محتوى الصورة، لكن يجب أن ترى كتلة من الأحرف Unicode مطبوعة في وحدة التحكم مع نسبة مئوية للثقة.

---

## الخلاصة

لقد استعرضنا **كيفية استخدام OCR** في C# من البداية إلى النهاية—تكوين المحرك، تحميل موارد اللغة، وأخيرًا **التعرف على النص من الصورة** أو ملفات **JPG** دون الحاجة إلى الاتصال بالإنترنت. باتباع الخطوات أعلاه يمكنك **استخراج النص من الصورة**، **تشغيل OCR على الصورة**، ومعالجة أكثر المشكلات شيوعًا التي تواجه المبتدئين.

هل أنت مستعد للتحدي التالي؟ جرّب إمداد المحرك بصفحة PDF محوّلة إلى صورة، أو جرب حزمة لغة مختلفة لترى كيف تتغير درجات الثقة. قد

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}